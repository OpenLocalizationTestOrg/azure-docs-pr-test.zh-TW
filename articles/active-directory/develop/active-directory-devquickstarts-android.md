---
title: "開始使用 AD Android aaaAzure |Microsoft 文件"
description: "如何 toobuild 與 Azure AD 進行登入並呼叫 Azure AD 整合的 Android 應用程式會將使用 OAuth 保護應用程式開發介面。"
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>將 Azure AD 整合至 Android 應用程式
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> 嘗試的新 hello 預覽[開發人員入口網站](https://identity.microsoft.com/Docs/Android)，這將會幫助您獲得 Azure AD 在短短幾分鐘內啟動且正在執行。 hello 開發人員入口網站將引導您完成註冊應用程式與 Azure AD 整合您的程式碼 hello 程序。 當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。
>
>

如果您正在開發的桌面應用程式，Azure Active Directory (Azure AD) 使其簡單又直接您 tooauthenticate 為您的使用者使用其內部部署 Active Directory 帳戶。 它也可讓您的應用程式 toosecurely 取用任何 web API 受到 Azure AD，例如 hello Office 365 Api 或 hello Azure API。

對於 Android 用戶端需要 tooaccess 受保護的資源，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL)。 hello 的 ADAL 的唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。 toodemonstrate 多麼容易，所以我們將會建置 Android 待辦事項清單應用程式：

* 取得存取權杖呼叫待辦事項清單應用程式開發介面使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。
* 取得使用者的待辦事項清單。
* 登出使用者。

tooget 開始，您需要 Azure AD 租用戶，您可以建立使用者，並註冊應用程式。 如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>步驟 1： 下載並執行 hello Node.js REST API TODO 範例伺服器
特別是針對現有的 Azure ad 中建立單一租用戶待辦事項 REST API 範例 toowork 寫入 hello Node.js REST API TODO 範例。 這是快速入門的 hello 的必要條件。

如需有關如何 tooset 其設定，請參閱我們現有的範例中詳細[Microsoft Azure Active Directory 範例 REST API 服務 for Node.js](active-directory-devquickstarts-webapi-nodejs.md)。


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>步驟 2：向 Azure AD 租用戶註冊 Web API
Active Directory 支援加入兩種類型的應用程式：

- Web 應用程式開發介面中提供服務 toousers
- 存取應用程式 （hello 網站上或在裝置上執行） 的 web 應用程式開發介面

在此步驟中，您正在註冊您在本機執行的測試這個範例的 hello web API。 一般來說，此 web API 是 REST 服務的供應項目功能的應用程式 tooaccess。 Azure AD 可以保護任何端點。

我們假設您正在註冊 hello TODO REST API 參考之前。 但這適用於您想要 Azure Active Directory toohelp 保護任何 web 應用程式開發介面。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶。 在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 輸入 hello 應用程式的易記名稱 (例如， **TodoListService**)，請選取**Web 應用程式和/或 Web API**，按一下**下一步**。
6. 對於 hello 登入 URL，請輸入 hello 範例 hello 基底 URL。 依預設，這會是 `https://localhost:8080`。
7. 按一下**確定**toocomplete hello 註冊。
8. 仍在 hello Azure 入口網站，移至 tooyour 應用程式頁面、 尋找 hello 應用程式識別碼值，並將它複製。 您稍後在設定應用程式時需要此資訊。
9. 從 hello**設定** -> **屬性**頁面上，更新 hello 應用程式識別碼 URI-輸入`https://<your_tenant_name>/TodoListService`。 取代`<your_tenant_name>`hello Azure AD 租用戶名稱。

## <a name="step-3-register-hello-sample-android-native-client-application"></a>步驟 3： 註冊 hello 範例 Android 原生用戶端應用程式
在此範例中，您必須註冊您的 Web 應用程式。 這可讓您的應用程式 toocommunicate 與 hello 剛註冊 web 應用程式開發介面。 Azure AD 會拒絕 tooeven 允許登入您的應用程式 tooask，除非它登錄。 屬於 hello hello 模型安全性。

我們假設您正在註冊 hello 範例應用程式先前已參考。 但此程序適用於任何您正在開發的應用程式。

> [!NOTE]
> 也許您會納悶，為什麼要將應用程式和 Web API 都放在一個租用戶。 答案您可能已經猜到，您可以建置應用程式來存取在另一個租用戶的 Azure AD 中註冊的外部 API。 如果您這樣做，您的客戶將會提示您 tooconsent toohello hello API hello 應用程式中使用。 Active Directory Authentication Library for iOS 會替您處理此同意舉動。 當我們瀏覽更進階的功能，您會看到這是從 Azure 和 Office，以及任何其他服務提供者的 Microsoft 應用程式開發介面的 hello 工作所需的 tooaccess hello 套件很重要的一部分。 現在，因為您註冊您的 web 應用程式開發介面和應用程式在 hello 相同租用戶，您不會看到任何提示，以取得同意。 如果您正在開發應用程式僅供您自己的公司 toouse，這是通常 hello 情況。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶。 在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 輸入 hello 應用程式的易記名稱 (例如， **TodoListClient Android**)，請選取**原生用戶端應用程式**，按一下**下一步**。
6. Hello 重新導向 URI 中，輸入`http://TodoListClient`。 按一下 [完成] 。
7. Hello 應用程式頁面中，找出 hello 應用程式識別碼值，並將它複製。 您稍後在設定應用程式時需要此資訊。
8. 從 hello**設定**頁面上，選取**必要的使用權限**選取**新增**。  找出並選取 TodoListService，並將 hello**存取 TodoListService**權限下的**委派的權限**，然後按一下**完成**。

與 Maven toobuild，您可以使用 pom.xml hello 上方層級：

1. 將此儲存機制複製到您選擇的目錄：

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Hello 中的 hello 步驟[Maven 環境適用於 Android 的必要條件 tooset](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android)。
3. 設定 SDK 19 hello 模擬器。
4. 移 toohello 您再製 hello 儲存機制的根資料夾。
5. 執行這個命令：`mvn clean install`
6. 變更 hello 目錄 toohello 快速入門範例：`cd samples\hello`
7. 執行這個命令：`mvn android:deploy android:run`

   您應該會看到 hello 啟動應用程式。
8. 輸入測試使用者認證 tootry。

JAR 封裝將立即送出 hello AAR 封裝旁邊。

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>步驟 4： 下載 Android ADAL hello，並將它加入 tooyour Eclipse 工作區
我們已經讓您 toohave 輕鬆多個選項 toouse ADAL Android 專案中：

* 您可以使用 hello 來源的程式碼 tooimport 此文件庫，到 Eclipse 和連結 tooyour 應用程式。
* 如果您使用 Android Studio 中，您可以使用 hello AAR 封裝格式，並參考 hello 二進位檔。

### <a name="option-1-source-zip"></a>選項 1：原始檔 Zip
toodownload 副本 hello 原始程式碼中，按一下**Download ZIP**右邊 hello hello 頁面。 或者，可以[從 GitHub 下載](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz)。

### <a name="option-2-source-via-git"></a>選項 2：透過 Git 取得原始檔
透過 Git，SDK 輸入 hello tooget hello 原始碼：

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>選項 3：透過 Gradle 取得二進位檔
您可以從 hello Maven 中央儲存機制取得 hello 二進位檔。 hello AAR 封裝可以包含在 Android Studio 中的專案中，如下所示：

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>選項 4：透過 Maven 取得 AAR
如果您使用 hello M2Eclipse 外掛程式，您可以指定 pom.xml 檔案中的 hello 相依性：

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>選項 5: Hello 程式庫資料夾內的 JAR 封裝
從 hello Maven 儲存機制取得 hello JAR 檔案，並將其放置到 hello**程式庫**專案資料夾中的。 您需要 toocopy hello 所需的資源 tooyour 專案，因為 hello JAR 套件不包含它們。

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>步驟 5： 加入參考 tooAndroid ADAL tooyour 專案
1. 新增參考 tooyour 專案，並將它指定為 Android 程式庫。 如果您不確定如何 toodo，您可以取得更多有關 hello [Android Studio 網站](http://developer.android.com/tools/projects/projects-eclipse.html)。
2. 新增您的專案設定成偵錯 hello 專案相依性。
3. 更新您的專案 AndroidManifest.xml 檔案 tooinclude:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. 在您的主要活動建立 AuthenticationContext 的執行個體。 這個呼叫的 hello 詳細資料已超出本主題中，hello 範圍，但是可以藉由查看 hello 很不錯的起點[Android 原生用戶端範例](https://github.com/AzureADSamples/NativeClient-Android)。 在下列範例的 hello，SharedPreferences hello 預設快取，而且授權單位是 hello 形式`https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Hello 使用者輸入認證，並接收授權碼之後，請複製此程式碼區塊 toohandle hello 結尾 AuthenticationActivity:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask 權杖，來定義回呼：

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. 最後，使用該回呼來要求權杖：

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

以下是 hello 參數說明：

* *資源*無須且您正嘗試 tooaccess hello 資源。
* clientid 是必要參數，來自 AzureAD。
* *RedirectUri*不是必要的 toobe hello acquireToken 呼叫所提供。 您可以將它設定為您的套件名稱。
* *PromptBehavior* tooask 認證 tooskip hello 快取與 cookie 可幫助。
* *回呼*後權杖交換 hello 授權程式碼呼叫。 它有一個 AuthenticationResult 物件，提供存取權杖、過期日期和識別碼權杖資訊。
* acquireTokenSilent 為選擇性。 Toohandle 快取和權杖重新整理，您可以呼叫它。 它也提供 hello 的同步處理版本。 它接受 userid 作為參數。

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

使用本逐步解說，您應該有您需要 toosuccessfully 與 Azure Active Directory 整合。 如需此工作的範例，請瀏覽 hello AzureADSamples / GitHub 上的儲存機制。

## <a name="important-information"></a>重要資訊
### <a name="customization"></a>自訂
您的應用程式資源可以覆寫程式庫專案資源。 當您建置應用程式時會發生這種情況。 基於這個理由，您可以自訂您想要的驗證活動配置 hello 方式。 是確定 tookeep hello 識別碼 hello 控制項，ADAL 會使用 (WebView)。

### <a name="broker"></a>Broker
hello Microsoft Intune 公司入口網站應用程式提供 hello broker 元件。 hello 帳戶會建立在 AccountManager。 hello 帳戶類型是"com.microsoft.workaccount。 」 AccountManager 只允許一個 SSO (單一登入) 帳戶。 完成 hello 裝置挑戰的其中一個 hello 應用程式之後，它就會建立 hello 使用者的 SSO cookie。

ADAL 使用 hello broker 帳戶，如果在這個驗證器建立一個使用者帳戶，而且您選擇不 tooskip 它。 您可以略過與 hello broker 使用者：

   `AuthenticationSettings.Instance.setSkipBroker(true);`

您需要特殊的 RedirectUri tooregister broker 使用量。 RedirectUri 是 hello 格式`msauth://packagename/Base64UrlencodedSignature`。 您可以使用 hello 指令碼 brokerRedirectPrint.ps1 或 hello API 呼叫 mContext.getBrokerRedirectUri，應用程式取得您的 RedirectUri。 hello 簽章是相關的 tooyour 簽署憑證。

hello 目前 broker 模型是針對一個使用者。 AuthenticationContext 提供 hello API 方法 tooget hello broker 使用者。

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

您的應用程式資訊清單應該具有下列權限 toouse AccountManager 帳戶 hello。 如需詳細資訊，請參閱 hello [hello Android 網站上的 AccountManager 資訊](http://developer.android.com/reference/android/accounts/AccountManager.html)。

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>授權單位 URL 和 AD FS
Active Directory Federation Services (AD FS) 無法辨識為生產 STS，因此您需要的執行個體探索 tooturn 和在 hello AuthenticationContext 建構函式傳遞 false。

hello 授權 URL 需要 STS 執行個體和[租用戶名稱](https://login.microsoftonline.com/yourtenant.onmicrosoft.com)。

### <a name="querying-cache-items"></a>查詢快取項目
ADAL 在 SharedPreferences 中提供預設快取與一些簡單的快取查詢函式。 您可以使用從 AuthenticationContext 取得 hello 目前快取：

    ITokenCacheStore cache = mContext.getCache();

您也可以提供您的快取實作，如果您想 toocustomize 它。

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>提示行為
ADAL 提供選項 toospecify 提示行為。 PromptBehavior.Auto 如果 hello 重新整理權杖無效，而且不需要使用者的認證，將會顯示 hello UI。 PromptBehavior.Always 會略過 hello 快取使用量，並永遠顯示 hello UI。

### <a name="silent-token-request-from-cache-and-refresh"></a>從快取無訊息地要求權杖並重新整理
無訊息的權杖要求不會使用 hello UI 快顯，而且不需要的活動。 從 hello 快取，如果有的話，它就會傳回語彙基元。 如果 hello 權杖到期時，這個方法會嘗試 toorefresh 它。 如果 hello 重新整理權杖已過期或失敗，它會傳回 AuthenticationException。

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

您也可以使用此方法進行同步呼叫。 您可以設定 null toocallback 或 acquireTokenSilentSync。

### <a name="diagnostics"></a>診斷
這些是 hello 主要資訊來源的診斷問題：

* 例外狀況
* 記錄檔
* 網路追蹤

請注意，相互關聯識別碼 hello 文件庫中的中央 toohello 診斷。 如果您想的 toocorrelate ADAL 要求與其他程式碼中的作業，您可以依每個要求來設定相互關聯識別碼。 如果您沒有設定相互關聯識別碼，ADAL 會隨機產生一個。 所有記錄訊息和網路呼叫，會再印有 hello 相互關聯識別碼。 hello 自我產生每一個要求的識別碼的變更。

#### <a name="exceptions"></a>例外狀況
例外狀況是 hello 先診斷。 我們嘗試 tooprovide 有用的錯誤訊息。 如果您發現沒有幫助的錯誤訊息，請提出問題來告訴我們。 請同時提供裝置資訊，例如機型和 SDK 號碼。

#### <a name="logs"></a>記錄檔
您可以設定 hello 文件庫 toogenerate 記錄檔訊息，您可以使用 toohelp 診斷問題。 您可以進行 hello 下列呼叫 tooconfigure 回呼，ADAL 會使用 toohand 關閉每個記錄檔訊息，它會產生作為設定記錄。

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

Hello，下列程式碼所示，訊息可以寫入 tooa 自訂記錄檔。 不幸的是，從裝置取得記錄檔沒有標準方法。 有一些服務可協助您處理這部份。 您也可以設計您自己的資源，例如傳送嗨檔案 tooa 伺服器。

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

這些是 hello 記錄層級：
* Error (例外狀況)
* Warn (警告)
* Info (參考用途)
* Verbose (更多詳細資料)

您設定 hello 記錄層級，像這樣：

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 所有的記錄訊息會傳送 toologcat，加法 tooany 自訂記錄回呼中。
您可以從 logcat 取得記錄 tooa 檔，如下所示：

    adb logcat > "C:\logmsg\logfile.txt"

 如需 adb 命令的詳細資訊，請參閱 hello [hello Android 網站上的 logcat 資訊](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat)。

#### <a name="network-traces"></a>網路追蹤
您可以使用各種工具 toocapture hello HTTP 流量，ADAL 會產生。  如果您已熟悉 hello OAuth 通訊協定，或您需要 tooprovide 診斷資訊 tooMicrosoft 或其他支援管道，這是最有用。

Fiddler 是 hello 最簡單的 HTTP 追蹤工具。 使用 hello 下列連結 tooset 它 toocorrectly 記錄 ADAL 的網路流量。 Fiddler 或 Charles toobe 有用追蹤工具，您必須設定它以未加密的 toorecord SSL 流量。  

> [!NOTE]
> 這種方式產生的追蹤可能包含極機密的資訊，例如存取權杖、使用者名稱和密碼。 如果您使用實際執行帳戶，請勿將這些追蹤洩漏給第三方。 如果您需要 toosupply 追蹤 toosomeone 順序 tooget 支援，請使用暫時帳戶使用者名稱和密碼與您不介意共用重現 hello 問題。

* 從 hello Telerik 網站：[設定總 Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* 從 GitHub：[設定適用於 ADAL 的 Fiddler 規則](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>對話方塊模式
hello acquireToken 方法，而活動不支援對話方塊提示字元。

### <a name="encryption"></a>加密
ADAL 會加密 hello 語彙基元和 SharedPreferences 中預設的存放區。 您可以查看 hello StorageHelper 類別 toosee hello 詳細資料。 Android 引進 Android KeyStore 4.3 (API 18) 安全儲存體來存放私密金鑰。 ADAL 對 API 18 和更新版本使用此機制。 如果您想要 toouse ADAL 較低的 SDK 版本，您需要 tooprovide 在 AuthenticationSettings.INSTANCE.setSecretKey 祕密金鑰。

### <a name="oauth2-bearer-challenge"></a>OAuth2 持有者挑戰
hello AuthenticationParameters 類別提供的功能 tooget authorization_uri 從 hello OAuth2 bearer 挑戰。

### <a name="session-cookies-in-webview"></a>WebView 中的工作階段 Cookie
Android WebView hello 應用程式關閉後，不會清除工作階段 cookie。 您可以使用以下範例程式碼來處理這部分：

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

如需 cookie 的詳細資訊，請參閱 hello [hello Android 網站上的 CookieSyncManager 資訊](http://developer.android.com/reference/android/webkit/CookieSyncManager.html)。

### <a name="resource-overrides"></a>資源覆寫
hello ADAL 程式庫包含英文 ProgressDialog 訊息字串。 如果想要當地語系化的字串，您的應用程式應該覆寫這些英文字串。

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>NTLM 對話方塊
ADAL 1.1.0 版支援透過從 WebViewClient hello onReceivedHttpAuthRequest 事件處理 [NTLM] 對話方塊。 您可以自訂 hello 配置和字串 hello 對話方塊。

### <a name="cross-app-sso"></a>跨應用程式的 SSO
深入了解[如何 tooenable 跨應用程式使用 ADAL 在 Android 上的 SSO](active-directory-sso-android.md)。  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
