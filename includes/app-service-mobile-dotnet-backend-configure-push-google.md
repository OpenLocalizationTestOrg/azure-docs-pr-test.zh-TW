<span data-ttu-id="4aced-101">使用符合您的後端專案類型的 hello 程序&mdash;任一[.NET 後端](#dotnet)或[Node.js 後端](#nodejs)。</span><span class="sxs-lookup"><span data-stu-id="4aced-101">Use hello procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="4aced-102"><a name="dotnet"></a>.NET 後端專案</span><span class="sxs-lookup"><span data-stu-id="4aced-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="4aced-103">在 Visual Studio 中，hello 伺服器專案，以滑鼠右鍵按一下，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="4aced-103">In Visual Studio, right-click hello server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="4aced-104">搜尋 `Microsoft.Azure.NotificationHubs`，然後按一下安裝。</span><span class="sxs-lookup"><span data-stu-id="4aced-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="4aced-105">這會安裝 hello 通知中樞的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4aced-105">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="4aced-106">在 hello Controllers 資料夾中，開啟 TodoItemController.cs 並加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="4aced-106">In hello Controllers folder, open TodoItemController.cs and add hello following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="4aced-107">取代 hello`PostTodoItem`方法，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="4aced-107">Replace hello `PostTodoItem` method with hello following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
            // Get hello settings for hello server project.
            HttpConfiguration config = this.Configuration;

            MobileAppSettingsDictionary settings =
                this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

            // Get hello Notification Hubs credentials for hello Mobile App.
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
                // Send hello push notification and log hello results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write hello success result toohello logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write hello failure result toohello logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="4aced-108">重新發佈 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="4aced-108">Republish hello server project.</span></span>

### <span data-ttu-id="4aced-109"><a name="nodejs"></a>Node.js 後端專案</span><span class="sxs-lookup"><span data-stu-id="4aced-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="4aced-110">如果您沒有這樣做，[下載 hello 快速入門專案](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)，或其他使用 hello [hello Azure 入口網站中的線上編輯器](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。</span><span class="sxs-lookup"><span data-stu-id="4aced-110">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="4aced-111">取代 hello 下列 hello hello todoitem.js 檔案中的現有程式碼：</span><span class="sxs-lookup"><span data-stu-id="4aced-111">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
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
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="4aced-112">這會在傳送 GCM 通知包含 hello item.text 插入新的 todo 項目時。</span><span class="sxs-lookup"><span data-stu-id="4aced-112">This sends a GCM notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="4aced-113">編輯本機電腦中的 hello 檔案時，重新發行 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="4aced-113">When editing hello file in your local computer, republish hello server project.</span></span>
