## <a name="create-hello-webapi-project"></a>建立 hello WebAPI 專案
Hello 以下各節中建立新的 ASP.NET WebAPI 後端，而且會有三個主要用途：

1. **驗證用戶端**： 更新 tooauthenticate 用戶端要求和關聯的 hello 與 hello 要求的使用者，將會加入訊息處理常式。
2. **用戶端通知註冊**： 之後，您將加入新的用戶端裝置 tooreceive 通知註冊控制器 toohandle。 hello 已驗證的使用者名稱會自動加入做為 toohello 註冊[標記](https://msdn.microsoft.com/library/azure/dn530749.aspx)。
3. **傳送通知 tooClients**： 更新版本中，您也會加入控制器 tooprovide 方法，讓使用者 tootrigger 安全發送 toodevices 和與 hello 標籤相關聯的用戶端。 

hello 下列步驟顯示如何 toocreate hello 新的 ASP.NET WebAPI 後端： 

> [!IMPORTANT]
> 如果您使用 Visual Studio 2015 或更早版本，再開始本教學課程，請確定您已安裝的 NuGet 套件管理員 hello hello 最新版本。 toocheck 啟動 Visual Studio。 從 hello**工具**功能表上，按一下 **擴充功能和更新**。 搜尋**NuGet 套件管理員**您版本的 Visual Studio 中，並確定您擁有 hello 最新版本。 如果沒有，請解除安裝，然後再重新安裝 hello NuGet 套件管理員。
> 
> ![][B4]
> 
> [!NOTE]
> 請確定您已安裝 Visual Studio hello [Azure SDK](https://azure.microsoft.com/downloads/)網站部署。
> 
> 

1. 啟動 Visual Studio 或 Visual Studio Express。 按一下**伺服器總管**並登入 tooyour Azure 帳戶。 Visual Studio 將會需要您登入 toocreate hello 網站資源，在您的帳戶。
2. 在 Visual Studio 中，按一下 **檔案**，然後按一下**新增**，然後**專案**，依序展開**範本**， **Visual C#**，然後按一下 **Web**和**ASP.NET Web 應用程式**，型別 hello 名稱**AppBackend**，然後按一下**確定**。 
   
    ![][B1]
3. 在 hello**新增 ASP.NET 專案** 對話方塊中，按一下**Web API**，然後按一下**確定**。
   
    ![][B2]
4. 在 [hello**設定的 Microsoft Azure Web 應用程式**] 對話方塊中，選擇訂用帳戶，和**App Service 方案**您已經建立。 您也可以選擇**建立新的應用程式服務方案**建立一個從 hello 對話方塊。 在此教學課程中您不需要資料庫。 一旦您已選取您的應用程式服務方案中，按一下 **確定**toocreate hello 專案。
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>驗證用戶端 toohello WebAPI 後端
在本節中，您將建立新的訊息處理常式類別，名為**AuthenticationTestHandler** hello 新的後端。 這個類別衍生自[DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx)並加入做為訊息處理常式，所以它可以處理傳入 hello 後端的所有要求。 

1. 在 方案總管 中，以滑鼠右鍵按一下 hello **AppBackend**專案中，按一下 **新增**，然後按一下 **類別**。 Hello 新類別命名**AuthenticationTestHandler.cs**，然後按一下**新增**toogenerate hello 類別。 這個類別會使用的 tooauthenticate 使用者使用*基本驗證*為了簡單起見。 請注意，您的應用程式可以使用任何驗證結構描述。
2. 在 AuthenticationTestHandler.cs，加入 hello 下列`using`陳述式：
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. 在 AuthenticationTestHandler.cs，取代 hello`AuthenticationTestHandler`以下列程式碼的 hello 類別定義。 
   
    Hello 下列三個條件都成立時，這個處理常式會授權 hello 要求：
   
   * hello 要求包含*授權*標頭。 
   * hello 要求使用*基本*驗證。 
   * hello 使用者名稱字串 hello 密碼會是與字串 hello 相同的字串。
     
     否則，將會拒絕 hello 要求。 這不是真正的驗證和授權方法。 這只是本教學課程中一個非常簡單的範例。
     
     如果 hello 要求訊息已驗證，及授權的 hello `AuthenticationTestHandler`，hello 基本驗證的使用者將會附加的 toohello 目前要求上 hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx)。 Hello HttpContext 中的使用者資訊將供另一個控制站 (RegisterController) 更新 tooadd[標記](https://msdn.microsoft.com/library/azure/dn530749.aspx)toohello 通知註冊要求。
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **安全性注意事項**: hello`AuthenticationTestHandler`類別不提供，則為 true 的驗證。 它是使用唯一 toomimic 基本驗證，並不安全。 您必須在生產應用程式和服務中實作安全的驗證機制。                
     > 
     > 
4. 新增下列程式碼結尾 hello hello hello`Register`方法在 hello **App_Start/WebApiConfig.cs**類別 tooregister hello 訊息處理常式：
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. 儲存您的變更。

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>註冊使用 hello WebAPI 後端的通知
在本節中，我們將新的控制器 toohello WebAPI 後端 toohandle 要求 tooregister 使用者和裝置 hello 用戶端程式庫使用通知中樞的通知。 hello 控制器會加入使用者標記 hello 使用者通過驗證，並附加 toohello HttpContext 由 hello `AuthenticationTestHandler`。 hello 標記將會有 hello 字串格式， `"username:<actual username>"`。

1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **AppBackend**專案，然後按一下**管理 NuGet 封裝**。
2. 在 hello 左側，按一下 **線上**，並搜尋**Microsoft.Azure.NotificationHubs**在 hello**搜尋**方塊。
3. 在 hello 結果清單中，按一下  **Microsoft Azure 通知中樞**，然後按一下**安裝**。 完成 hello 安裝，然後關閉 hello NuGet 封裝管理員 視窗。
   
    這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。
4. 現在，我們將建立新的類別檔案，表示與通知中樞用 toosend 通知 hello 連接。 在 hello 方案總管 中，以滑鼠右鍵按一下 hello**模型**資料夾中，按一下**新增**，然後按一下 **類別**。 Hello 新類別命名**Notifications.cs**，然後按一下 **新增**toogenerate hello 類別。 
   
    ![][B6]
5. 在 Notifications.cs，加入 hello 下列`using`在 hello hello 檔案最上方的陳述式：
   
        using Microsoft.Azure.NotificationHubs;
6. 取代 hello`Notifications`類別 hello 下列定義，請確定 tooreplace hello 兩預留位置取代 hello 連接字串 （具有完整權限） 您的通知中樞，和 hello 中樞名稱 (可在[Azure 傳統入口網站](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. 接下來我們將建立名為 **RegisterController** 的新控制器。 在 方案總管 中，以滑鼠右鍵按一下 hello**控制器**資料夾，然後按一下 **新增**，然後按一下 **控制器**。 按一下 hello **Web API 2 控制器-空白**項目，然後再按一下**新增**。 Hello 新類別命名**RegisterController**，然後按一下**新增**再次 toogenerate hello 控制站。
   
    ![][B7]
   
    ![][B8]
8. 在 RegisterController.cs，加入 hello 下列`using`陳述式：
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. 新增下列程式碼內 hello hello`RegisterController`類別定義。 請注意，在這段程式碼中，我們將加入使用者標記，這是 hello 使用者附加 toohello HttpContext。 hello 使用者通過驗證，並附加 toohello HttpContext hello 訊息篩選器，我們加入， `AuthenticationTestHandler`。 您也可以加入 hello 使用者的選用檢查 tooverify 具有權限的 hello tooregister 要求標記。
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. 儲存您的變更。

## <a name="sending-notifications-from-hello-webapi-backend"></a>從 hello WebAPI 後端傳送通知
本節中，您會加入新的控制站可公開方法，讓用戶端裝置 toosend hello hello ASP.NET WebAPI 後端中使用 Azure 通知中心服務管理程式庫的使用者名稱標記為基礎的通知。

1. 建立另一個名為 **NotificationsController**的新控制器。 建立 hello 相同的方式建立 hello **RegisterController** hello 前一節。
2. 在 NotificationsController.cs，加入 hello 下列`using`陳述式：
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. 新增下列方法 toohello hello **NotificationsController**類別。
   
    此程式碼傳送 hello 平台通知服務 (PNS) 為基礎的通知類型`pns`參數。 hello 值`to_tag`為使用的 tooset hello *username*標記的 hello 訊息。 此標記必須符合作用中通知中樞註冊的使用者名稱標記。 hello 通知訊息是取自 hello hello POST 要求主體，而且 hello 目標 PNS 格式化。 
   
    Hello 平台通知服務 (PNS) 支援的裝置使用 tooreceive 通知，根據不同的通知使用不同格式支援。 例如在 Windows 裝置上，您可以搭配 WNS 使用不受其他 PNS 直接支援的 [快顯通知](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) 。 因此您的後端 hello PNS 的裝置必須受支援的通知至 tooformat hello 通知您計劃 toosupport。 然後使用 hello 適當的傳送應用程式開發介面上 hello [NotificationHubClient 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. 按**F5** toorun hello 應用程式和 tooensure hello 工作的準確性為止。 hello 應用程式應該啟動網頁瀏覽器，並顯示 hello ASP.NET 首頁。 

## <a name="publish-hello-new-webapi-backend"></a>發行 hello 新 WebAPI 後端
1. 現在我們將部署此應用程式 tooan Azure 網站順序 toomake 中的所有的裝置可以存取它。 以滑鼠右鍵按一下 hello **AppBackend**專案，然後選取**發行**。
2. 選取 [Microsoft Azure App Service] 作為發佈目標，然後按一下 [發佈]。 這會開啟 hello 建立應用程式服務 對話方塊可幫助您在 Azure 中建立所有 hello 所需的 Azure 資源 toorun hello ASP.NET web 應用程式。

    ![][B15]
3. 在 [hello**建立 App Service** ] 對話方塊中，選取您的 Azure 帳戶。 按一下 [變更類型] 並選取 [Web 應用程式]。 保留 hello **Web 應用程式名稱**給定的並選取 hello**訂用帳戶**，**資源群組**，和**App Service 方案**。  按一下 [建立] 。

4. 請記下 hello**網站 URL**屬性在 hello**摘要**> 一節。 我們將 toothis URL 做為您*後端端點*稍後在本教學課程。 按一下 [發行] 。

5. Hello 精靈完成後，其所發行 hello ASP.NET web 應用程式 tooAzure，然後啟動 hello hello 預設瀏覽器中的應用程式。  您的應用程式將可在 Azure App Service 中檢視。

hello URL 會使用您稍早，指定與 hello 格式 http://<app_name>.azurewebsites.net hello web 應用程式名稱。

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
