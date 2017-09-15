<span data-ttu-id="0462c-101">使用符合您後端專案類型的程序 (&mdash;[.NET 後端](#dotnet)或 [Node.js 後端](#nodejs))。</span><span class="sxs-lookup"><span data-stu-id="0462c-101">Use the procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="0462c-102"><a name="dotnet"></a>.NET 後端專案</span><span class="sxs-lookup"><span data-stu-id="0462c-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="0462c-103">In Visual Studio, right-click the server project, and click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="0462c-103">In Visual Studio, right-click the server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="0462c-104">搜尋 `Microsoft.Azure.NotificationHubs`，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="0462c-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="0462c-105">這會安裝通知中樞用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="0462c-105">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="0462c-106">在 Controllers 資料夾中，開啟 TodoItemController.cs 並新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="0462c-106">In the Controllers folder, open TodoItemController.cs and add the following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="0462c-107">以下列程式碼取代 `PostTodoItem` 方法：</span><span class="sxs-lookup"><span data-stu-id="0462c-107">Replace the `PostTodoItem` method with the following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
            // Get the settings for the server project.
            HttpConfiguration config = this.Configuration;

            MobileAppSettingsDictionary settings =
                this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

            // Get the Notification Hubs credentials for the Mobile App.
            string notificationHubName = settings.NotificationHubName;
            string notificationHubConnection = settings
                .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

            // Create a new Notification Hub client.
            NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send the push notification and log the results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write the success result to the logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write the failure result to the logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="0462c-108">發佈伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="0462c-108">Republish the server project.</span></span>

### <span data-ttu-id="0462c-109"><a name="nodejs"></a>Node.js 後端專案</span><span class="sxs-lookup"><span data-stu-id="0462c-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="0462c-110">如果您還沒這麼做，請[下載快速入門專案](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)或使用 [Azure 入口網站中的線上編輯器](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。</span><span class="sxs-lookup"><span data-stu-id="0462c-110">If you haven't already done so, [download the quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="0462c-111">在 todoitem.js 檔案中，以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="0462c-111">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="0462c-112">插入新的 todo 項目時，這會傳送包含 item.text 的 GCM 通知。</span><span class="sxs-lookup"><span data-stu-id="0462c-112">This sends a GCM notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="0462c-113">在本機電腦中編輯檔案時，重新發布伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="0462c-113">When editing the file in your local computer, republish the server project.</span></span>
