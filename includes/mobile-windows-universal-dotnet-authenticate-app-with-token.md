
1. 在 hello MainPage.xaml.cs 專案檔中加入 hello 下列**使用**陳述式：
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. 取代 hello **AuthenticateAsync**方法，以下列程式碼的 hello:
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    在這個版本的**AuthenticateAsync**，hello 應用程式會嘗試 toouse 認證儲存在 hello **PasswordVault** tooaccess hello 服務。 如果沒有儲存任何認證，也會執行一般登入。
   
   > [!NOTE]
   > 可能過期的快取的權杖，以及權杖的到期日也可能發生在驗證後 hello 應用程式正在使用中。 如何 toodetermine 如果權杖已過期，請參閱的 toolearn[檢查是否有過期的驗證語彙基元](http://aka.ms/jww5vp)。 方案 toohandling 授權錯誤相關的 tooexpiring 語彙基元，請參閱文章 hello[管理 SDK 的快取和處理 Azure Mobile Services 中的過期語彙基元](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx)。 
   > 
   > 
3. 重新啟動兩次 hello 應用程式。
   
    請注意，在 hello 第一次啟動時，使用 hello 提供者登入一次是必要的。 不過，快取的 hello 認證會用在 hello 第二個重新啟動，而且登入則會略過。 

