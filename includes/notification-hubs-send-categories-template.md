
<span data-ttu-id="4a26f-101">本節說明如何 toosend 最新消息，做為標記來自.NET 主控台應用程式中的範本通知。</span><span class="sxs-lookup"><span data-stu-id="4a26f-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="4a26f-102">如果您使用行動應用程式，請參閱 toohello[行動應用程式的新增推播通知]教學課程，選取您在 hello 最上方的平台。</span><span class="sxs-lookup"><span data-stu-id="4a26f-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="4a26f-103">如果您想 toouse Java 或 PHP 參照太[如何從 Java/PHP 的通知中樞 toouse]。</span><span class="sxs-lookup"><span data-stu-id="4a26f-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="4a26f-104">您可以使用[通知中樞 REST 介面]，從任何後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="4a26f-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="4a26f-105">如果您建立 hello 主控台應用程式來傳送通知，當您完成時，略過步驟 1-3[開始使用通知中樞]。</span><span class="sxs-lookup"><span data-stu-id="4a26f-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="4a26f-106">在 Visual Studio 中建立新的 Visual C# 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="4a26f-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="4a26f-107">在 hello Visual Studio 主功能表中，按一下 **工具**，**程式庫套件管理員**，和**Package Manager Console**、 hello 主控台視窗中輸入下列命令，然後按下**輸入**:</span><span class="sxs-lookup"><span data-stu-id="4a26f-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="4a26f-108">這會將參考 toohello Azure 通知中樞 SDK 使用 hello [Microsoft.Azure.Notification 集線器 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="4a26f-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="4a26f-109">開啟 hello 檔 Program.cs，然後加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="4a26f-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="4a26f-110">在 hello`Program`類別，加入下列方法，hello 或取代它，如果已經存在：</span><span class="sxs-lookup"><span data-stu-id="4a26f-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="4a26f-111">此程式碼會傳送 hello 六個標記 hello 字串陣列中的每個範本通知。</span><span class="sxs-lookup"><span data-stu-id="4a26f-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="4a26f-112">標記的 hello 使用可確保裝置收到 hello 註冊類別目錄的通知。</span><span class="sxs-lookup"><span data-stu-id="4a26f-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="4a26f-113">在上述程式碼的 hello，取代 hello`<hub name>`和`<connection string with full access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultFullSharedAccessSignature*從您的通知中樞的 hello 儀表板.</span><span class="sxs-lookup"><span data-stu-id="4a26f-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="4a26f-114">加入下列行 hello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="4a26f-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="4a26f-115">建置 hello 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a26f-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[開始使用通知中樞]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[通知中樞 REST 介面]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[行動應用程式的新增推播通知]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[如何從 Java/PHP 的通知中樞 toouse]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification 集線器 NuGet 封裝]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
