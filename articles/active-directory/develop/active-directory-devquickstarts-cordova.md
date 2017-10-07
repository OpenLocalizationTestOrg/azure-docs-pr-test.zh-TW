---
title: "開始使用 AD Cordova aaaAzure |Microsoft 文件"
description: "如何 toobuild Cordova 應用程式的整合 Azure AD 進行登入及使用 OAuth 呼叫 Azure AD 保護應用程式開發介面。"
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>整合 Azure AD 與 Apache Cordova 應用程式
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

您可以使用 Apache Cordova toodevelop HTML5/JavaScript 應用程式可以在單純的原生應用程式的行動裝置上執行。 與 Azure Active Directory (Azure AD)，您可以加入企業等級驗證功能 tooyour Cordova 應用程式。

iOS、Android、Windows 市集和 Windows Phone 上的 Cordova 外掛程式包裝了 Azure AD 原生 SDK。 使用的外掛程式，您可以增強您的應用程式登入與使用者的 Windows Server Active Directory 帳戶、 改善存取 tooOffice 365 及 Azure 應用程式開發介面，而且甚至 toosupport 保護呼叫 tooyour 自己自訂的 web 應用程式開發介面。

在本教學課程中，我們將藉由新增下列功能的 hello hello Apache Cordova 外掛程式使用的 Active Directory 驗證程式庫 (ADAL) tooimprove 簡單的應用程式：

* 只要短短幾行程式碼，就可驗證使用者並取得權杖。
* 使用該語彙基元 tooinvoke hello Graph API tooquery 該目錄，並顯示 hello 結果。  
* 使用 hello ADAL 權杖快取 toominimize 驗證提示 hello 使用者。

toomake 這些增強功能，您需要：

1. 向 Azure AD 註冊應用程式。
2. 加入程式碼 tooyour 應用程式 toorequest 語彙基元。
3. 加入程式碼來查詢 Graph API hello toouse hello 語彙基元，並顯示結果。
4. 建立 hello Cordova 部署專案與所有 hello 平台 tootarget，新增 hello Cordova ADAL 外掛程式，然後在模擬器中測試 hello 方案。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要：

* Azure AD 租用戶，您在其中有一個帳戶具備應用程式開發權限。
* 已設定 toouse Apache Cordova 開發環境。  

如果您已經有同時設定，直接繼續 toostep 1。

如果您沒有 Azure AD 租用戶，請使用 hello[指示一個 tooget](active-directory-howto-tenant.md)。

如果您沒有在您的電腦上設定的 Apache Cordova，安裝 hello 下列：

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/) (可以輕鬆地透過 NPM 封裝管理員來安裝：`npm install -g cordova`)

hello PC 與 hello mac 上，應該運作之前安裝的 hello

每個目標平台各有不同的必要條件：

* toobuild 和執行應用程式 Windows 平板電腦或 Windows Phone:
  * 安裝 [Visual Studio 2013 for Windows (含 Update 2) 或更新版本](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express 或其他版本) 或 [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community)。

* toobuild 並執行 iOS 應用程式：

  * 安裝 Xcode 6.x 或更新版本。 下載從 hello [Apple 開發人員網站](http://developer.apple.com/downloads)或 hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12)。
  * 安裝 [ios-sim](https://www.npmjs.org/package/ios-sim)。 您可以使用它 toostart iOS 應用程式中 hello 命令列上的 iOS 模擬器。 (您可以輕鬆地將它安裝透過終端機 hello: `npm install -g ios-sim`。)
* toobuild 和適用於 Android 的應用程式執行：

  * 安裝 [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。 請確定`JAVA_HOME`根據 toohello JDK 安裝路徑 (例如，C:\Program Files\Java\jdk1.7.0_75) 正確設定 （環境變數）。
  * 安裝[Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools)和新增 hello`<android-sdk-location>\tools`位置 (例如，C:\tools\Android\android-sdk\tools) tooyour`PATH`環境變數。
  * 開啟 Android SDK 管理員 (例如，透過終端機 hello: `android`) 並安裝：
    * *Android 5.0.1 (API 21)* 平台 SDK
    * Android SDK Build Tools 19.1.0 版或更新版本
    * *Android Support Repository* (Extras)

  hello Android SDK 不提供任何預設模擬器執行個體。 建立一個執行`android avd`hello 終端機，然後選取 從**建立**，如果您想 toorun hello Android 應用程式在模擬器上的。 我們建議 API 層級 19 或更高。 如需 hello Android 模擬器和建立選項的詳細資訊，請參閱[AVD Manager](http://developer.android.com/tools/help/avd-manager.html) hello Android 網站上。

## <a name="step-1-register-an-application-with-azure-ad"></a>步驟 1︰向 Azure AD 註冊應用程式
此為選用步驟。 本教學課程提供您可以使用 toosee 預先佈建的值而不需要執行任何佈建在自己的租用戶 hello 動作中的範例。 不過，我們建議您不要執行這個步驟，並熟悉 hello 程序，因為它會在必要時建立自己的應用程式。

Azure AD 發出權杖 tooonly 已知的應用程式。 您可以使用 Azure AD 從您的應用程式之前，您需要 toocreate 項目，在您的租用戶。 tooregister 租用戶中新的應用程式：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶。 在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 依照 hello 提示，並建立**原生用戶端應用程式**。 (雖然 Cordova 應用程式是 HTML 架構，我們在此要建立的是原生用戶端應用程式。 hello**原生用戶端應用程式**必須選取選項，或 hello 應用程式將無法運作。)
  * **名稱**描述應用程式 toousers。
  * **重新導向 URI**為 hello 已使用 tooreturn 語彙基元 tooyour 應用程式的 URI。 輸入 **http://MyDirectorySearcherApp**。

完成註冊之後，Azure AD 會指派唯一的應用程式識別碼 tooyour 應用程式。 您必須以 hello 下一節中的值。 您可以將它找到新建立的應用程式的 hello hello 應用程式 索引標籤上。

toorun `DirSearchClient Sample`，授與 hello 新建立的應用程式的權限 tooquery hello Azure AD Graph API:

1. 從 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。  
2. Hello Azure Active Directory 應用程式中，選取**Microsoft Graph**為 hello 應用程式開發介面，並加入 hello **hello 登入的使用者身分存取 hello 目錄**權限下的**委派權限**。  這可讓使用者您應用程式 tooquery hello Graph API。

## <a name="step-2-clone-hello-sample-app-repository"></a>步驟 2： 複製 hello 範例應用程式儲存機制
從殼層或命令列中，輸入下列命令的 hello:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>步驟 3： 建立 hello Cordova 應用程式
有多個方式 toocreate Cordova 應用程式。 在本教學課程中，我們將使用 hello Cordova 命令列介面 (CLI)。

1. 從殼層或命令列中，輸入下列命令的 hello:

        cordova create DirSearchClient

   該命令會建立 hello 資料夾結構和 scaffolding hello Cordova 專案。

2. 移動 toohello 新 DirSearchClient 資料夾：

        cd .\DirSearchClient

3. 使用檔案管理員或使用下列命令，在您的 shell 中的 hello hello www 子資料夾中複製 hello hello 入門專案內容：

  * Windows：`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac：`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. 新增 hello 白名單外掛程式。 這是必要的叫用 hello Graph API。

        cordova plugin add cordova-plugin-whitelist

5. 新增所有您想 toosupport hello 平台。 toohave 工作範例，您需要下列命令的 hello 的 tooexecute 至少一個。 請注意，將不會在 Windows 上的無法 tooemulate iOS 或模擬在 mac 上的 Windows

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. 加入 Cordova 外掛程式 tooyour 專案 hello ADAL:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>步驟 4： 加入程式碼 tooauthenticate 使用者，並從 Azure AD 取得權杖
在本教學課程，您正在開發的 hello 應用程式會提供簡單的目錄搜尋功能。 hello 使用者即可輸入 hello 目錄中的 hello 別名的任何使用者或以視覺化方式檢視一些基本的屬性。 hello 入門專案包含 hello hello 基本使用者介面 （在 www/index.html) hello 應用程式的定義和基本應用程式事件繫結在一起的 hello scaffolding 循環，使用者介面的繫結，並產生顯示邏輯 （在 www/js/index.js)。 hello 留下您的唯一工作是 tooadd hello 邏輯實作識別工作。

hello 第一件事您在程式碼中需要 toodo 是導入 hello Azure AD 來識別您的應用程式所使用的通訊協定值與 hello 您設定為目標的資源。 這些值將在稍後會使用的 tooconstruct hello 權杖要求。 插入下列程式碼片段在 hello hello index.js 檔案最上方的 hello:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

hello`redirectUri`和`clientId`值應符合您的應用程式描述 Azure AD 中的 hello 值。 您可以找到與 hello**設定**hello Azure 入口網站中索引標籤，如稍早在本教學課程步驟 1 中所述。

> [!NOTE]
> 如果您選擇不在您自己的租用戶中註冊新的應用程式，您只可以貼上 hello 預先設定的值。 您可以看見 hello 範例執行，但您應該一律適用於實際執行的應用程式建立自己的項目。

接下來，加入 hello 權杖要求程式碼。 插入下列程式碼片段之間 hello hello`search`和`renderData`定義：

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
讓我們將該函式分成兩個主要部分來檢查一下。
這個範例是設計的 toowork 搭配任何租用戶，但不要的 toobeing 繫結 tooa 特定的。 它會使用 hello"/ 常見"的端點，這可讓 hello 使用者 tooenter 任何帳戶，在驗證階段，並指示 hello 要求 toohello 租用戶所屬的位置。

Hello 方法的第一部分會檢查 hello ADAL 快取 toosee，如果已儲存的語彙基元。 如果是這樣，hello 方法會使用 hello 租用戶 hello 語彙基元來自何處來重新初始化 ADAL。 這是必要 tooavoid 額外的提示，因為 hello 使用的"/ 常見"永遠會導致詢問 hello 使用者 tooenter 新帳戶。

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
hello 的 hello 方法的第二個部分執行 hello 適當的權杖要求。 hello`acquireTokenSilentAsync`方法要求 ADAL tooreturn 語彙基元 hello 指定資源不會顯示任何 UX 如果 hello 快取中已經有適當的存取語彙基元儲存，可以發生的如果可以在重新整理權杖用 tooget 新存取權杖，而不會顯示任何提示。 如果該嘗試失敗，我們會切換回`acquireTokenAsync`-這會明顯地提示 hello 使用者 tooauthenticate。

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
現在，我們已經 hello 語彙基元，但我們最後會叫用 hello Graph API，並執行 hello 我們想要的搜尋查詢。 插入下列程式碼片段如下 hello hello`authenticate`定義：

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
hello 起點檔案提供簡單的 UX 在文字方塊中輸入使用者的別名。 這個方法會使用該值 tooconstruct 查詢、 結合 hello 存取語彙基元、 將它送出 tooMicrosoft 圖形，和剖析 hello 結果。 hello`renderData`已經存在於 hello 起點檔案，方法會負責視覺化 hello 結果。

## <a name="step-5-run-hello-app"></a>步驟 5： 執行 hello 應用程式
您的應用程式是最後準備 toorun。 作業系統就相當簡單： hello 應用程式啟動時，輸入您想 toolook，hello 使用者 hello 別名，然後再按一下 [hello] 按鈕。 系統會提示您進行驗證。 在驗證成功，成功的搜尋會顯示 hello hello 搜尋使用者屬性。

後續執行將不會顯示任何提示字元執行 hello 搜尋，這 toohello 與否 hello 先前取得快取中的語彙基元。

hello 執行 hello 應用程式的具象步驟會因平台而異。

### <a name="windows-10"></a>Windows 10
   平板電腦/PC： `cordova run windows --archs=x64 -- --appx=uap`

   行動 （需要 Windows 10 行動裝置版 」 裝置連接 tooa PC）：`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > 在第一次執行的 hello，可能會要求您在 toosign 的開發人員授權。 如需詳細資訊，請參閱[開發人員授權](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)。

### <a name="windows-81-tabletpc"></a>Windows 8.1 平板電腦/PC
   `cordova run windows`

   > [!NOTE]
   > 在第一次執行的 hello，可能會要求您在 toosign 的開發人員授權。 如需詳細資訊，請參閱[開發人員授權](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)。

### <a name="windows-phone-81"></a>Windows Phone 8.1
   toorun 連線的裝置上：`cordova run windows --device -- --phone`

   toorun hello 預設模擬器上：`cordova emulate windows -- --phone`

   使用`cordova run windows --list -- --phone`toosee 所有可用的目標和`cordova run windows --target=<target_name> -- --phone`toorun hello 應用程式的特定裝置或模擬器上 (例如， `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`)。

### <a name="android"></a>Android
   toorun 連線的裝置上：`cordova run android --device`

   toorun hello 預設模擬器上：`cordova emulate android`

   請確定您已使用 AVD Manager 建立的模擬器執行個體，如稍早在 hello < 先決條件 > 一節中所述。

   使用`cordova run android --list`toosee 所有可用的目標和`cordova run android --target=<target_name>`toorun hello 應用程式的特定裝置或模擬器上 (例如， `cordova run android --target="Nexus4_emulator"`)。

### <a name="ios"></a>iOS
   toorun 連線的裝置上：`cordova run ios --device`

   toorun hello 預設模擬器上：`cordova emulate ios`

   > [!NOTE]
   > 請確定您擁有 hello `ios-sim` hello 模擬器上的安裝套件 toorun。 如需詳細資訊，請參閱 hello < 先決條件 > 一節。

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>後續步驟
參考，完成的 hello 範例 （不含您的組態值） 會提供[GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient)。

您可以現在移動 toomore 進階 （以及更多有趣） 案例。 您可能會想 tootry:[安全與 Azure AD Node.js Web API](active-directory-devquickstarts-webapi-nodejs.md)。

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
