



<span data-ttu-id="56fe3-101">當您傳送範本通知，您只需要 tooprovide 一組屬性時，在本例中我們會傳送 hello 集的執行個體包含 hello hello 最新消息，當地語系化的版本的屬性：</span><span class="sxs-lookup"><span data-stu-id="56fe3-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="56fe3-102">本節說明如何使用主控台應用程式的 toosend 通知</span><span class="sxs-lookup"><span data-stu-id="56fe3-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="56fe3-103">hello 包含程式碼的廣播 tooboth Windows 市集和 iOS 裝置，因為 hello 後端可以廣播 tooany 的 hello 支援裝置。</span><span class="sxs-lookup"><span data-stu-id="56fe3-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="56fe3-104">使用 C# 主控台應用程式的 toosend 通知</span><span class="sxs-lookup"><span data-stu-id="56fe3-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="56fe3-105">修改 hello`SendTemplateNotificationAsync`您先前建立以下列程式碼的 hello hello 主控台應用程式中的方法。</span><span class="sxs-lookup"><span data-stu-id="56fe3-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="56fe3-106">請注意如何在此情況下有不需要 toosend 用於不同的地區設定和平台的多個通知。</span><span class="sxs-lookup"><span data-stu-id="56fe3-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
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


<span data-ttu-id="56fe3-107">請注意這個簡單的呼叫將會太傳送 hello 當地語系化的段新聞**所有**您的裝置，無論 hello 平台，因為您的通知中樞建立並傳遞 hello 正確原生裝載 tooall hello 裝置訂閱tooa 特定的標記。</span><span class="sxs-lookup"><span data-stu-id="56fe3-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="56fe3-108">使用行動服務傳送 hello 通知</span><span class="sxs-lookup"><span data-stu-id="56fe3-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="56fe3-109">在您的行動服務排程器，您可以使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="56fe3-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

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


