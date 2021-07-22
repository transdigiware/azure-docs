---
title: Use JavaScript to create a chat room with Azure Functions and SignalR Service
description: A quickstart for using Azure SignalR Service and Azure Functions to create an App showing GitHub star count using JavaScript.
author: sffamily
ms.author: zhshang
ms.date: 06/09/2021
ms.topic: quickstart
ms.service: signalr
ms.devlang: javascript
ms.custom:
  - devx-track-js
  - mode-api
---
# Quickstart: Use JavaScript to create an App showing GitHub star count with Azure Functions and SignalR Service

Azure SignalR Service lets you easily add real-time functionality to your application and Azure Functions is a serverless platform that lets you run your code without managing any infrastructure. In this quickstart, learn how to use SignalR Service and Azure Functions to build a serverless application with JavaScript to broadcast messages to clients.

> [!NOTE]
> You can get all codes mentioned in the article from [GitHub](https://github.com/aspnet/AzureSignalR-samples/tree/main/samples/QuickStartServerless/javascript)

## Prerequisites

- A code editor, such as [Visual Studio Code](https://code.visualstudio.com/)
- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).
- [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools#installing), version 2 or above. Used to run Azure Function apps locally.
- [Node.js](https://nodejs.org/en/download/), version 10.x

   > [!NOTE]
   > The examples should work with other versions of Node.js, see [Azure Functions runtime versions documentation](../azure-functions/functions-versions.md#languages) for more information.

> [!NOTE]
> This quickstart can be run on macOS, Windows, or Linux.

Having issues? Try the [troubleshooting guide](signalr-howto-troubleshoot-guide.md) or [let us know](https://aka.ms/asrs/qsjs).

## Log in to Azure

Sign in to the Azure portal at <https://portal.azure.com/> with your Azure account.

Having issues? Try the [troubleshooting guide](signalr-howto-troubleshoot-guide.md) or [let us know](https://aka.ms/asrs/qsjs).

[!INCLUDE [Create instance](includes/signalr-quickstart-create-instance.md)]

Having issues? Try the [troubleshooting guide](signalr-howto-troubleshoot-guide.md) or [let us know](https://aka.ms/asrs/qsjs).


## Setup and run the Azure Function locally

1. Make sure you have Azure Function Core Tools installed. And create an empty directory and navigate to the directory with command line.

    ```bash
    # Initialize a function project
    func init --worker-runtime javascript
    ```

2. After you initialize a project, you need to create functions. In this sample, we need to create 3 functions.

    1. Run the following command to create a `index` function, which will host a web page for client.

        ```bash
        func new -n index -t HttpTrigger
        ```
        
        Open `index/index.js` and copy the following codes.

        ```javascript
        var fs = require('fs').promises
    
        module.exports = async function (context, req) {
            const path = context.executionContext.functionDirectory + '/../content/index.html'
            try {
                var data = await fs.readFile(path);
                context.res = {
                    headers: {
                        'Content-Type': 'text/html'
                    },
                    body: data
                }
                context.done()
            } catch (error) {
                context.log.error(err);
                context.done(err);
            }
        }
        ```
    
    2. Create a `negotiate` function for clients to get access token.
    
        ```bash
        func new -n negotiate -t SignalRNegotiateHTTPTrigger
        ```
        
        Open `negotiate/function.json` and copy the following json codes:
    
        ```json
        {
          "disabled": false,
          "bindings": [
            {
              "authLevel": "anonymous",
              "type": "httpTrigger",
              "direction": "in",
              "methods": [
                "post"
              ],
              "name": "req",
              "route": "negotiate"
            },
            {
              "type": "http",
              "direction": "out",
              "name": "res"
            },
            {
              "type": "signalRConnectionInfo",
              "name": "connectionInfo",
              "hubName": "serverless",
              "connectionStringSetting": "AzureSignalRConnectionString",
              "direction": "in"
            }
          ]
        }
        ```
    
    3. Create a `broadcast` function to broadcast messages to all clients. In the sample, we use time trigger to broadcast messages periodically.
    
        ```bash
        func new -n broadcast -t TimerTrigger
        ```
    
        Open `broadcast/function.json` and copy the following codes.
    
        ```json
        {
          "bindings": [
            {
              "name": "myTimer",
              "type": "timerTrigger",
              "direction": "in",
              "schedule": "*/5 * * * * *"
            },
            {
              "type": "signalR",
              "name": "signalRMessages",
              "hubName": "serverless",
              "connectionStringSetting": "AzureSignalRConnectionString",
              "direction": "out"
            }
          ]
        }
        ```
    
        Open `broadcast/index.js` and copy the following codes.
    
        ```javascript
        var https = require('https');
        
        module.exports = function (context) {
            var req = https.request("https://api.github.com/repos/azure/azure-signalr", {
                method: 'GET',
                headers: {'User-Agent': 'serverless'}
            }, res => {
                var body = "";
        
                res.on('data', data => {
                    body += data;
                });
                res.on("end", () => {
                    var jbody = JSON.parse(body);
                    context.bindings.signalRMessages = [{
                        "target": "newMessage",
                        "arguments": [ `Current star count of https://github.com/Azure/azure-signalr is: ${jbody['stargazers_count']}` ]
                    }]
                    context.done();
                });
            }).on("error", (error) => {
                context.log(error);
                context.res = {
                  status: 500,
                  body: error
                };
                context.done();
            });
            req.end();
        }    
        ```

3. The client interface of this sample is a web page. Considered we read HTML content from `content/index.html` in `index` function, create a new file `index.html` in `content` directory. And copy the following content.

    ```html
    <html>
    
    <body>
      <h1>Azure SignalR Serverless Sample</h1>
      <div id="messages"></div>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/microsoft-signalr/3.1.7/signalr.min.js"></script>
      <script>
        let messages = document.querySelector('#messages');
        const apiBaseUrl = window.location.origin;
        const connection = new signalR.HubConnectionBuilder()
            .withUrl(apiBaseUrl + '/api')
            .configureLogging(signalR.LogLevel.Information)
            .build();
          connection.on('newMessage', (message) => {
            document.getElementById("messages").innerHTML = message;
          });
    
          connection.start()
            .catch(console.error);
      </script>
    </body>
    
    </html>
    ```

4. It's almost done now. The last step is to set a connection string of the SignalR Service to Azure Function settings.

    1. In the browser where the Azure portal is opened, confirm the SignalR Service instance you deployed earlier was successfully created by searching for its name in the search box at the top of the portal. Select the instance to open it.

        ![Search for the SignalR Service instance](media/signalr-quickstart-azure-functions-csharp/signalr-quickstart-search-instance.png)

    1. Select **Keys** to view the connection strings for the SignalR Service instance.
    
        ![Screenshot that highlights the primary connection string.](media/signalr-quickstart-azure-functions-javascript/signalr-quickstart-keys.png)

    1. Copy the primary connection string. And execute the command below.
    
        ```bash
        func settings add AzureSignalRConnectionString '<signalr-connection-string>'
        ```
    
5. Run the Azure Function in local:

    ```bash
    func start
    ```

    After Azure Function running locally. Use your browser to visit `http://localhost:7071/api/index` and you can see the current start count. And if you star or unstar in the GitHub, you will get a start count refreshing every few seconds.

    > [!NOTE]
    > SignalR binding needs Azure Storage, but you can use local storage emulator when the Function is running locally.
    > If you got some error like `There was an error performing a read operation on the Blob Storage Secret Repository. Please ensure the 'AzureWebJobsStorage' connection string is valid.` You need to download and enable [Storage Emulator](../storage/common/storage-use-emulator.md)

Having issues? Try the [troubleshooting guide](signalr-howto-troubleshoot-guide.md) or [let us know](https://aka.ms/asrs/qscsharp)

[!INCLUDE [Cleanup](includes/signalr-quickstart-cleanup.md)]

Having issues? Try the [troubleshooting guide](signalr-howto-troubleshoot-guide.md) or [let us know](https://aka.ms/asrs/qsjs).

## Next steps

In this quickstart, you built and ran a real-time serverless application in local. Learn more how to use SignalR Service bindings for Azure Functions.
Next, learn more about how to bi-directional communicating between clients and Azure Function with SignalR Service.

> [!div class="nextstepaction"]
> [SignalR Service bindings for Azure Functions](../azure-functions/functions-bindings-signalr-service.md)

> [!div class="nextstepaction"]
> [Bi-directional communicating in Serverless](https://github.com/aspnet/AzureSignalR-samples/tree/main/samples/BidirectionChat)

> [!div class="nextstepaction"]
> [Deploy Azure Functions with VS Code](/azure/developer/javascript/tutorial-vscode-serverless-node-01)
