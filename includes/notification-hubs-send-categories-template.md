
本節說明如何 toosend 最新消息，做為標記來自.NET 主控台應用程式中的範本通知。

如果您使用行動應用程式，請參閱 toohello[行動應用程式的新增推播通知]教學課程，選取您在 hello 最上方的平台。

如果您想 toouse Java 或 PHP 參照太[如何從 Java/PHP 的通知中樞 toouse]。 您可以使用[通知中樞 REST 介面]，從任何後端傳送通知。

如果您建立 hello 主控台應用程式來傳送通知，當您完成時，略過步驟 1-3[開始使用通知中樞]。

1. 在 Visual Studio 中建立新的 Visual C# 主控台應用程式：
   
       ![][13]
2. 在 hello Visual Studio 主功能表中，按一下 **工具**，**程式庫套件管理員**，和**Package Manager Console**、 hello 主控台視窗中輸入下列命令，然後按下**輸入**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    這會將參考 toohello Azure 通知中樞 SDK 使用 hello [Microsoft.Azure.Notification 集線器 NuGet 封裝]。
3. 開啟 hello 檔 Program.cs，然後加入下列 hello`using`陳述式：
   
        using Microsoft.Azure.NotificationHubs;
4. 在 hello`Program`類別，加入下列方法，hello 或取代它，如果已經存在：
   
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
   
    此程式碼會傳送 hello 六個標記 hello 字串陣列中的每個範本通知。 標記的 hello 使用可確保裝置收到 hello 註冊類別目錄的通知。
5. 在上述程式碼的 hello，取代 hello`<hub name>`和`<connection string with full access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultFullSharedAccessSignature*從您的通知中樞的 hello 儀表板.
6. 加入下列行 hello hello **Main**方法：
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. 建置 hello 主控台應用程式。

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[開始使用通知中樞]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[通知中樞 REST 介面]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[行動應用程式的新增推播通知]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[如何從 Java/PHP 的通知中樞 toouse]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification 集線器 NuGet 封裝]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
