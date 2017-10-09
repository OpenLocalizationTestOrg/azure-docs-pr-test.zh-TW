
* <span data-ttu-id="a943d-101">**.NET 後端 (C#)**：</span><span class="sxs-lookup"><span data-stu-id="a943d-101">**.NET backend (C#)**:</span></span>      
  
  1. <span data-ttu-id="a943d-102">在 Visual Studio 中，以滑鼠右鍵按一下 hello 伺服器專案，然後按一下**管理 NuGet 封裝**，搜尋`Microsoft.Azure.NotificationHubs`，然後按一下 **安裝**。</span><span class="sxs-lookup"><span data-stu-id="a943d-102">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.NotificationHubs`, then click **Install**.</span></span> <span data-ttu-id="a943d-103">這會安裝適用於傳送通知從您的後端的 hello 通知中心程式庫。</span><span class="sxs-lookup"><span data-stu-id="a943d-103">This installs hello Notification Hubs library for sending notifications from your backend.</span></span>
  2. <span data-ttu-id="a943d-104">在後端 hello Visual Studio 專案中，開啟**控制器** > **TodoItemController.cs**。</span><span class="sxs-lookup"><span data-stu-id="a943d-104">In hello backend's Visual Studio project, open **Controllers** > **TodoItemController.cs**.</span></span> <span data-ttu-id="a943d-105">在 hello hello 檔案頂端，加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="a943d-105">At hello top of hello file, add hello following `using` statement:</span></span>
     
          using Microsoft.Azure.Mobile.Server.Config;
          using Microsoft.Azure.NotificationHubs;

    3. <span data-ttu-id="a943d-106">取代 hello`PostTodoItem`方法，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a943d-106">Replace hello `PostTodoItem` method with hello following code:</span></span>  

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

                // iOS payload
                var appleNotificationPayload = "{\"aps\":{\"alert\":\"" + item.Text + "\"}}";

                try
                {
                    // Send hello push notification and log hello results.
                    var result = await hub.SendAppleNativeNotificationAsync(appleNotificationPayload);

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

    4. <span data-ttu-id="a943d-107">重新發佈 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="a943d-107">Republish hello server project.</span></span>

* <span data-ttu-id="a943d-108">**Node.js 後端** ：</span><span class="sxs-lookup"><span data-stu-id="a943d-108">**Node.js backend** :</span></span> 
  
  1. <span data-ttu-id="a943d-109">如果您沒有這樣做，[下載 hello 快速入門專案](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)或其他使用 hello [hello Azure 入口網站中的線上編輯器](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。</span><span class="sxs-lookup"><span data-stu-id="a943d-109">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>    
  2. <span data-ttu-id="a943d-110">取代下列程式碼的 hello hello todoitem.js 資料表指令碼：</span><span class="sxs-lookup"><span data-stu-id="a943d-110">Replace hello todoitem.js table script with hello following code:</span></span>

            var azureMobileApps = require('azure-mobile-apps'),
                promises = require('azure-mobile-apps/src/utilities/promises'),
                logger = require('azure-mobile-apps/src/logger');

            var table = azureMobileApps.table();

            // When adding record, send a push notification via APNS
            table.insert(function (context) {
                // For details of hello Notification Hubs JavaScript SDK, 
                // see http://aka.ms/nodejshubs
                logger.info('Running TodoItem.insert');

                // Create a payload that contains hello new item Text.
                var payload = "{\"aps\":{\"alert\":\"" + context.item.text + "\"}}";

                // Execute hello insert; Push as a post-execute action when results are returned as a Promise.
                return context.execute()
                    .then(function (results) {
                        // Only do hello push if configured
                        if (context.push) {
                            context.push.apns.send(null, payload, function (error) {
                                if (error) {
                                    logger.error('Error while sending push notification: ', error);
                                } else {
                                    logger.info('Push notification sent successfully!');
                                }
                            });
                        }
                        return results;
                    })
                    .catch(function (error) {
                        logger.error('Error while running context.execute: ', error);
                    });
            });

            module.exports = table;

    2. <span data-ttu-id="a943d-111">編輯本機電腦上的 hello 檔案時，重新發行 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="a943d-111">When editing hello file on your local computer, republish hello server project.</span></span>
