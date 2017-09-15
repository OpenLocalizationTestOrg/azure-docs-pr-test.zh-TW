<span data-ttu-id="f10f3-101">在本節中，您會更新現有 Mobile Apps 後端專案中的程式碼，以在每次新增項目時傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="f10f3-101">In this section, you update code in your existing Mobile Apps back-end project to send a push notification every time a new item is added.</span></span> <span data-ttu-id="f10f3-102">這是由 Azure 通知中樞的[範本](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)功能所提供，可啟用跨平台推播。</span><span class="sxs-lookup"><span data-stu-id="f10f3-102">This is powered by the [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="f10f3-103">各種用戶端會使用範本來註冊推播通知，而單一通用推播即可送達所有的用戶端平台。</span><span class="sxs-lookup"><span data-stu-id="f10f3-103">The various clients are registered for push notifications using templates, and a single universal push can get to all client platforms.</span></span>

<span data-ttu-id="f10f3-104">請選擇下列其中一個符合您後端專案類型(&mdash;[.NET 後端](#dotnet)或 [Node.js 後端](#nodejs))的程序。</span><span class="sxs-lookup"><span data-stu-id="f10f3-104">Choose one of the following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="f10f3-105"><a name="dotnet"></a>.NET 後端專案</span><span class="sxs-lookup"><span data-stu-id="f10f3-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="f10f3-106">在 Visual Studio 中，以滑鼠右鍵按一下伺服器專案並按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="f10f3-106">In Visual Studio, right-click the server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="f10f3-107">搜尋 `Microsoft.Azure.NotificationHubs`，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="f10f3-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="f10f3-108">這會安裝通知中樞程式庫，以便從後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="f10f3-108">This installs the Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="f10f3-109">在伺服器專案中，開啟 **Controllers** >   **TodoItemController.cs**，並新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="f10f3-109">In the server project, open **Controllers** > **TodoItemController.cs**, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="f10f3-110">在 **PostTodoItem** 方法中，於呼叫 **InsertAsync** 之後新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f10f3-110">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>  

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

        // Sending the message so that all template registrations that contain "messageParam"
        // will receive the notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added to the list.";

        try
        {
            // Send the push notification and log the results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="f10f3-111">插入新的項目時，這會傳送包含 item.Text 的範本通知。</span><span class="sxs-lookup"><span data-stu-id="f10f3-111">This sends a template notification that contains the item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="f10f3-112">發佈伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="f10f3-112">Republish the server project.</span></span>

### <span data-ttu-id="f10f3-113"><a name="nodejs"></a>Node.js 後端專案</span><span class="sxs-lookup"><span data-stu-id="f10f3-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="f10f3-114">如果您還沒這麼做，請[下載快速入門後端專案](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)或使用 [Azure 入口網站中的線上編輯器](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)。</span><span class="sxs-lookup"><span data-stu-id="f10f3-114">If you haven't already done so, [download the quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="f10f3-115">在 todoitem.js 中，以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f10f3-115">Replace the existing code in todoitem.js with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="f10f3-116">插入新的項目時，這會傳送包含 item.Text 的範本通知。</span><span class="sxs-lookup"><span data-stu-id="f10f3-116">This sends a template notification that contains the item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="f10f3-117">當您在本機電腦上編輯檔案時，請重新發佈伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="f10f3-117">When editing the file on your local computer, republish the server project.</span></span>
