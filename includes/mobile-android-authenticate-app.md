
1. <span data-ttu-id="e3f12-101">在 Android Studio 中開啟 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="e3f12-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="e3f12-102">在**Project Explorer**在 Android Studio 中，開啟 hello ToDoActivity.java 檔案並加入下列 import 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3f12-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="e3f12-103">新增下列方法 toohello hello **ToDoActivity**類別：</span><span class="sxs-lookup"><span data-stu-id="e3f12-103">Add hello following method toohello **ToDoActivity** class:</span></span>

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="e3f12-104">此程式碼會建立方法 toohandle hello Google 驗證程序。</span><span class="sxs-lookup"><span data-stu-id="e3f12-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="e3f12-105">對話方塊會顯示 hello hello 驗證使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="e3f12-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="e3f12-106">您只能繼續進行成功驗證。</span><span class="sxs-lookup"><span data-stu-id="e3f12-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e3f12-107">如果您使用 Google 以外的身分識別提供者，將變更傳遞 toohello hello 值**登入**方法 tooone 的 hello 下列值： _MicrosoftAccount_， _Facebook_， _twitter_，或_windowsazureactivedirectory_。</span><span class="sxs-lookup"><span data-stu-id="e3f12-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="e3f12-108">在 hello **onCreate**方法，加入下列一行程式碼會具現化 hello 的 hello 程式碼之後的 hello`MobileServiceClient`物件。</span><span class="sxs-lookup"><span data-stu-id="e3f12-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="e3f12-109">此呼叫會啟動 hello 驗證程序。</span><span class="sxs-lookup"><span data-stu-id="e3f12-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="e3f12-110">移動其餘程式碼之後的 hello`authenticate();`在 hello **onCreate**方法 tooa 新**createTable**方法：</span><span class="sxs-lookup"><span data-stu-id="e3f12-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="e3f12-111">tooensure 重新導向的運作方式如預期般，加入下列程式碼片段的 hello _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="e3f12-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="e3f12-112">新增 redirectUriScheme too_build.gradle_ Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3f12-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. <span data-ttu-id="e3f12-113">加入您的 build.gradle com.android.support:customtabs:23.0.1 toohello 相依性：</span><span class="sxs-lookup"><span data-stu-id="e3f12-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="e3f12-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="e3f12-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="e3f12-115">從 hello**執行**功能表上，按一下 **執行應用程式**toostart hello 應用程式並使用您所選擇的身分識別提供者登入。</span><span class="sxs-lookup"><span data-stu-id="e3f12-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="e3f12-116">hello 提及的 URL 配置是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="e3f12-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="e3f12-117">請確認所有發生次數`{url_scheme_of_you_app}`使用 hello 相同案例。</span><span class="sxs-lookup"><span data-stu-id="e3f12-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="e3f12-118">當您成功登入時，hello 應用程式應執行且沒有錯誤，以及您應該能夠 tooquery hello 後端服務並進行更新 toodata。</span><span class="sxs-lookup"><span data-stu-id="e3f12-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
