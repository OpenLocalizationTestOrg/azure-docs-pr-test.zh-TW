



<span data-ttu-id="68d3c-101">傳送範本通知時，您只需提供一組屬性，在我們的案例中，我們將傳送一組包含已當地語系化版本的目前新聞屬性，例如：</span><span class="sxs-lookup"><span data-stu-id="68d3c-101">When you send template notifications you only need to provide a set of properties, in our case we will send the set of properties containing the localized version of the current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="68d3c-102">本節將使用主控台應用程式示範傳送通知的方式</span><span class="sxs-lookup"><span data-stu-id="68d3c-102">This section shows how to send notifications using a console app</span></span>

<span data-ttu-id="68d3c-103">後端可廣播至任何支援的裝置，因此隨附的程式碼會廣播至 Windows 市集和 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="68d3c-103">The included code broadcasts to both Windows Store and iOS devices, since the backend can broadcast to any of the supported devices.</span></span>

### <a name="to-send-notifications-using-a-c-console-app"></a><span data-ttu-id="68d3c-104">使用 C# 主控台應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="68d3c-104">To send notifications using a C# console app</span></span>
<span data-ttu-id="68d3c-105">在先前建立的主控台應用程式中以下列程式碼修改 `SendTemplateNotificationAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="68d3c-105">Modify the `SendTemplateNotificationAsync` method in the console app you previously created with the following code.</span></span> <span data-ttu-id="68d3c-106">請注意，此案例不需要針對不同地區設定和平台傳送多次通知。</span><span class="sxs-lookup"><span data-stu-id="68d3c-106">Notice how in this case there is no need to send multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending the notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and the proper tags will receive the notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="68d3c-107">請注意，此簡單呼叫會將已當地語系化的新聞片段傳送到您的 **所有** 裝置 (不論平台為何)，因為您的通知中樞會建立並傳遞正確的原生裝載給訂用特定標籤的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="68d3c-107">Note that this simple call will deliver the localized piece of news to **all** your devices, irrespective of the platform, as your Notification Hub builds and delivers the correct native payload to all the devices subscribed to a specific tag.</span></span>

### <a name="sending-the-notification-with-mobile-services"></a><span data-ttu-id="68d3c-108">使用行動服務傳送通知</span><span class="sxs-lookup"><span data-stu-id="68d3c-108">Sending the notification with Mobile Services</span></span>
<span data-ttu-id="68d3c-109">在您的行動服務排程器中，您可以使用下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="68d3c-109">In your Mobile Service scheduler, you can use the following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


