<span data-ttu-id="7a821-101">在本節中，每當您更新程式碼中您現有的行動應用程式後端專案 toosend 推播通知加入新項目。</span><span class="sxs-lookup"><span data-stu-id="7a821-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="7a821-102">這由 hello[範本](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)Azure 通知中樞，啟用跨平台推播通知的功能。</span><span class="sxs-lookup"><span data-stu-id="7a821-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="7a821-103">hello 各種用戶端會註冊推播通知使用範本，且單一的通用發送可以取得 tooall 用戶端平台。</span><span class="sxs-lookup"><span data-stu-id="7a821-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="7a821-104">選擇其中一個符合您的後端專案類型的下列程序 hello&mdash;任一[.NET 後端](#dotnet)或[Node.js 後端](#nodejs)。</span><span class="sxs-lookup"><span data-stu-id="7a821-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="7a821-105"><a name="dotnet"></a>.NET 後端專案</span><span class="sxs-lookup"><span data-stu-id="7a821-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="7a821-106">在 Visual Studio 中，以滑鼠右鍵按一下 hello 伺服器專案，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="7a821-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="7a821-107">搜尋 `Microsoft.Azure.NotificationHubs`，然後按一下安裝。</span><span class="sxs-lookup"><span data-stu-id="7a821-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="7a821-108">這會安裝適用於傳送通知從您的後端的 hello 通知中心程式庫。</span><span class="sxs-lookup"><span data-stu-id="7a821-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="7a821-109">在 hello 伺服器專案中，開啟**控制器** > **TodoItemController.cs**，並加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7a821-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="7a821-110">在 hello **PostTodoItem**方法，新增下列程式碼 hello 呼叫之後，太 hello**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="7a821-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

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

    <span data-ttu-id="7a821-111">這會將傳送範本通知，其中包含 hello 項目。插入新項目時的文字。</span><span class="sxs-lookup"><span data-stu-id="7a821-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="7a821-112">重新發佈 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="7a821-112">Republish hello server project.</span></span>

### <span data-ttu-id="7a821-113"><a name="nodejs"></a>Node.js 後端專案</span><span class="sxs-lookup"><span data-stu-id="7a821-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="7a821-114">如果您沒有這樣做，[下載 hello 快速入門後端專案](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)，或其他使用 hello [hello Azure 入口網站中的線上編輯器](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。</span><span class="sxs-lookup"><span data-stu-id="7a821-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="7a821-115">取代 hello 下列 hello todoitem.js 中的現有程式碼：</span><span class="sxs-lookup"><span data-stu-id="7a821-115">Replace hello existing code in todoitem.js with hello following:</span></span>

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

    <span data-ttu-id="7a821-116">這會將傳送範本通知，其中包含 hello item.text 插入新項目時。</span><span class="sxs-lookup"><span data-stu-id="7a821-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="7a821-117">編輯本機電腦上的 hello 檔案時，重新發行 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="7a821-117">When editing hello file on your local computer, republish hello server project.</span></span>
