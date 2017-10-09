## <a name="webapi-project"></a>WebAPI 專案
1. 在 Visual Studio 中，開啟 hello **AppBackend** hello 中建立的專案**通知使用者**教學課程。
2. 在 Notifications.cs，取代 hello 整個**通知**以下列程式碼的 hello 的類別。 為確定 tooreplace hello 預留位置使用的連接字串 （具有完整權限） 您的通知中樞和 hello 中樞名稱。 您可以取得這些值從 hello [Azure 傳統入口網站](http://manage.windowsazure.com)。 此模組現在代表 hello 不同安全通知會傳送。 在完整的實作中，hello 通知將會儲存在資料庫中。為了簡單起見，在此情況下我們將其儲存在記憶體中。
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. 在 NotificationsController.cs，取代 hello hello 內的程式碼**NotificationsController**以下列程式碼的 hello 類別定義。 這個元件會安全地實作 hello 裝置 tooretrieve hello 通知的方式，而且也提供安全的推播 tooyour 裝置方式 （基於本教學課程的 hello 目的） tootrigger。 請注意，當傳送嗨通知 toohello 通知中樞，我們只傳送原始通知 hello 識別碼 hello 通知 （以及任何實際的訊息）：
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


請注意該 hello`Post`方法現在不會傳送快顯通知。 它會傳送包含只 hello 通知識別碼，以及不含任何機密內容的未經處理通知。 此外，請確定 toocomment hello 傳送嗨平台，您沒有在您的通知中樞上設定的認證，將會導致錯誤的作業。

1. 現在我們將會重新部署此應用程式 tooan Azure 網站順序 toomake 中的所有的裝置可以存取它。 以滑鼠右鍵按一下 hello **AppBackend**專案，然後選取**發行**。
2. 選取 Azure 網站作為您的發行目標。 登入您的 Azure 帳戶並選取現有或新網站，並記下 hello**目的地 URL**屬性在 hello**連接** 索引標籤。我們將 toothis URL 做為您*後端端點*稍後在本教學課程。 按一下 [發行] 。

