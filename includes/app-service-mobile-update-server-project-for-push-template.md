在本節中，每當您更新程式碼中您現有的行動應用程式後端專案 toosend 推播通知加入新項目。 這由 hello[範本](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)Azure 通知中樞，啟用跨平台推播通知的功能。 hello 各種用戶端會註冊推播通知使用範本，且單一的通用發送可以取得 tooall 用戶端平台。

選擇其中一個符合您的後端專案類型的下列程序 hello&mdash;任一[.NET 後端](#dotnet)或[Node.js 後端](#nodejs)。

### <a name="dotnet"></a>.NET 後端專案
1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello 伺服器專案，然後按一下**管理 NuGet 封裝**。 搜尋 `Microsoft.Azure.NotificationHubs`，然後按一下安裝。 這會安裝適用於傳送通知從您的後端的 hello 通知中心程式庫。
2. 在 hello 伺服器專案中，開啟**控制器** > **TodoItemController.cs**，並加入 hello 下列 using 陳述式：

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. 在 hello **PostTodoItem**方法，新增下列程式碼 hello 呼叫之後，太 hello**InsertAsync**:  

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

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    這會將傳送範本通知，其中包含 hello 項目。插入新項目時的文字。
4. 重新發佈 hello 伺服器專案。

### <a name="nodejs"></a>Node.js 後端專案
1. 如果您沒有這樣做，[下載 hello 快速入門後端專案](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)，或其他使用 hello [hello Azure 入口網站中的線上編輯器](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。
2. 取代 hello 下列 hello todoitem.js 中的現有程式碼：

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
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

    這會將傳送範本通知，其中包含 hello item.text 插入新項目時。
3. 編輯本機電腦上的 hello 檔案時，重新發行 hello 伺服器專案。
