
hello 之前的範例顯示的標準登入，這需要 hello 用戶端 toocontact 這兩個 hello 身分識別提供者和 hello 後端 Azure 服務每次啟動 hello 應用程式。 這個方法沒有效率，而且如果許多客戶嘗試 toostart 您的應用程式同時，您可以讓使用方式相關的問題。 更好的方法是 toocache hello 授權權杖傳回 hello Azure 服務，並再試一次 toouse 這第一次使用之前在根據提供者的登入。

> [!NOTE]
> 您可以在 hello 後端 Azure 服務，不論您是否使用用戶端管理或服務管理驗證所發出的 hello 權杖快取。 本教學課程使用服務管理驗證。
>
>

1. 開啟 hello ToDoActivity.java 檔案並加入下列 import 陳述式的 hello:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. 新增下列成員 toohello hello`ToDoActivity`類別。

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. 在 hello ToDoActivity.java 檔案中，加入下列定義 hello hello`cacheUserToken`方法。

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    這個方法會標示為 私人喜好設定檔案中儲存 hello 使用者識別碼和語彙基元。 這應該保護存取 toohello 快取，因此 hello 裝置上的其他應用程式沒有存取 toohello 語彙基元。 hello 喜好設定為沙箱化 hello 應用程式。 不過，如果有人取得存取 toohello 裝置時，很可能就會獲得存取 toohello 權杖快取透過其他方式。

   > [!NOTE]
   > 如果語彙基元存取 tooyour 資料會被視為高度敏感，而且其他人可能會獲得存取 toohello 裝置，您可以進一步保護加密，hello 語彙基元。 不過，完全安全的解決方案已超出此教學課程中，hello 範圍和安全性需求而定。
   >
   >
4. 在 hello ToDoActivity.java 檔案中，加入下列定義 hello hello`loadUserTokenCache`方法。

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. 在 hello *ToDoActivity.java*檔案中，取代 hello`authenticate`以下列方法，會使用權杖快取的 hello 方法。 如果您想 toouse Google 以外的帳戶，請變更 hello 登入提供者。

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. 建置 hello 應用程式和測試驗證使用有效的帳戶。 至少執行 2 次此動作。 期間第一次執行的 hello，您應該會收到提示 toosign 中的，並建立 hello 權杖快取。 在這之後，每次執行會嘗試驗證的 tooload hello 權杖快取。 您不應該在需要的 toosign。
