
<span data-ttu-id="762ae-101">hello 之前的範例顯示的標準登入，這需要 hello 用戶端 toocontact 這兩個 hello 身分識別提供者和 hello 後端 Azure 服務每次啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="762ae-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="762ae-102">這個方法沒有效率，而且如果許多客戶嘗試 toostart 您的應用程式同時，您可以讓使用方式相關的問題。</span><span class="sxs-lookup"><span data-stu-id="762ae-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="762ae-103">更好的方法是 toocache hello 授權權杖傳回 hello Azure 服務，並再試一次 toouse 這第一次使用之前在根據提供者的登入。</span><span class="sxs-lookup"><span data-stu-id="762ae-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="762ae-104">您可以在 hello 後端 Azure 服務，不論您是否使用用戶端管理或服務管理驗證所發出的 hello 權杖快取。</span><span class="sxs-lookup"><span data-stu-id="762ae-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="762ae-105">本教學課程使用服務管理驗證。</span><span class="sxs-lookup"><span data-stu-id="762ae-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="762ae-106">開啟 hello ToDoActivity.java 檔案並加入下列 import 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="762ae-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="762ae-107">新增下列成員 toohello hello`ToDoActivity`類別。</span><span class="sxs-lookup"><span data-stu-id="762ae-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="762ae-108">在 hello ToDoActivity.java 檔案中，加入下列定義 hello hello`cacheUserToken`方法。</span><span class="sxs-lookup"><span data-stu-id="762ae-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="762ae-109">這個方法會標示為 私人喜好設定檔案中儲存 hello 使用者識別碼和語彙基元。</span><span class="sxs-lookup"><span data-stu-id="762ae-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="762ae-110">這應該保護存取 toohello 快取，因此 hello 裝置上的其他應用程式沒有存取 toohello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="762ae-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="762ae-111">hello 喜好設定為沙箱化 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="762ae-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="762ae-112">不過，如果有人取得存取 toohello 裝置時，很可能就會獲得存取 toohello 權杖快取透過其他方式。</span><span class="sxs-lookup"><span data-stu-id="762ae-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="762ae-113">如果語彙基元存取 tooyour 資料會被視為高度敏感，而且其他人可能會獲得存取 toohello 裝置，您可以進一步保護加密，hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="762ae-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="762ae-114">不過，完全安全的解決方案已超出此教學課程中，hello 範圍和安全性需求而定。</span><span class="sxs-lookup"><span data-stu-id="762ae-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="762ae-115">在 hello ToDoActivity.java 檔案中，加入下列定義 hello hello`loadUserTokenCache`方法。</span><span class="sxs-lookup"><span data-stu-id="762ae-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

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
5. <span data-ttu-id="762ae-116">在 hello *ToDoActivity.java*檔案中，取代 hello`authenticate`以下列方法，會使用權杖快取的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="762ae-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="762ae-117">如果您想 toouse Google 以外的帳戶，請變更 hello 登入提供者。</span><span class="sxs-lookup"><span data-stu-id="762ae-117">Change hello login provider if you want toouse an account other than Google.</span></span>

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
6. <span data-ttu-id="762ae-118">建置 hello 應用程式和測試驗證使用有效的帳戶。</span><span class="sxs-lookup"><span data-stu-id="762ae-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="762ae-119">至少執行 2 次此動作。</span><span class="sxs-lookup"><span data-stu-id="762ae-119">Run it at least twice.</span></span> <span data-ttu-id="762ae-120">期間第一次執行的 hello，您應該會收到提示 toosign 中的，並建立 hello 權杖快取。</span><span class="sxs-lookup"><span data-stu-id="762ae-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="762ae-121">在這之後，每次執行會嘗試驗證的 tooload hello 權杖快取。</span><span class="sxs-lookup"><span data-stu-id="762ae-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="762ae-122">您不應該在需要的 toosign。</span><span class="sxs-lookup"><span data-stu-id="762ae-122">You should not be required toosign in.</span></span>
