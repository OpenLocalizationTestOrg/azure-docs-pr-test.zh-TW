
1. 在 Android Studio 中開啟 hello 專案。

2. 在**Project Explorer**在 Android Studio 中，開啟 hello ToDoActivity.java 檔案並加入下列 import 陳述式的 hello:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. 新增下列方法 toohello hello **ToDoActivity**類別：

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

    此程式碼會建立方法 toohandle hello Google 驗證程序。 對話方塊會顯示 hello hello 驗證使用者識別碼。 您只能繼續進行成功驗證。

    > [!NOTE]
    > 如果您使用 Google 以外的身分識別提供者，將變更傳遞 toohello hello 值**登入**方法 tooone 的 hello 下列值： _MicrosoftAccount_， _Facebook_， _twitter_，或_windowsazureactivedirectory_。

4. 在 hello **onCreate**方法，加入下列一行程式碼會具現化 hello 的 hello 程式碼之後的 hello`MobileServiceClient`物件。

        authenticate();

    此呼叫會啟動 hello 驗證程序。

5. 移動其餘程式碼之後的 hello`authenticate();`在 hello **onCreate**方法 tooa 新**createTable**方法：

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

6. tooensure 重新導向的運作方式如預期般，加入下列程式碼片段的 hello _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. 新增 redirectUriScheme too_build.gradle_ Android 應用程式。

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

8. 加入您的 build.gradle com.android.support:customtabs:23.0.1 toohello 相依性：

      dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }

9. 從 hello**執行**功能表上，按一下 **執行應用程式**toostart hello 應用程式並使用您所選擇的身分識別提供者登入。

> [!WARNING]
> hello 提及的 URL 配置是區分大小寫。  請確認所有發生次數`{url_scheme_of_you_app}`使用 hello 相同案例。

當您成功登入時，hello 應用程式應執行且沒有錯誤，以及您應該能夠 tooquery hello 後端服務並進行更新 toodata。
