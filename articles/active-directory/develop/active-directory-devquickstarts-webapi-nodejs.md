---
title: "開始使用 AD Node.js aaaAzure |Microsoft 文件"
description: "如何 toobuild Node.js REST web API，與整合 Azure AD 進行驗證。"
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>開始使用適用於 Node.js 的 Web API
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* 是 Node.js 的驗證中介軟體。 彈性和模組化，在 tooany 暗中卸除 Passport Express 為基礎或 Restify web 應用程式。 一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他等驗證。 我們已為 Microsoft Azure Active Directory (Azure AD) 開發一項策略。 我們安裝此模組，然後新增 Microsoft Azure Active Directory hello`passport-azure-ad`外掛程式。

toodo，您需要：

1. 向 Azure AD 註冊應用程式。
2. 設定您的應用程式 toouse Passport 的`passport-azure-ad`外掛程式。
3. 設定用戶端應用程式 toocall hello tooDo 清單 web API。

此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/Azure-Samples/active-directory-node-webapi)。

> [!NOTE]
> 本文並未列舉如何 tooimplement 登入、 註冊，或使用 Azure AD B2C 管理設定檔。 它著重在呼叫 web Api 之後 hello 使用者已經過驗證。  我們建議您開始[如何與 Azure Active Directory 文件 toointegrate](active-directory-how-to-integrate.md) toolearn 需 hello Azure Active directory 的基本概念。
>
>

我們已經發行所有 hello 的原始程式碼執行本例 GitHub 中 MIT 授權，所以您可以免費 tooclone （或更好的是，「 分叉 」），並提供意見反應，提取要求。

## <a name="about-nodejs-modules"></a>關於 Node.js 模組
我們會在本逐步解說中使用 Node.js 模組。 模組是指可載入的 JavaScript 封裝，可為您的應用程式提供特定功能。 您通常使用 hello NPM 安裝目錄中的 hello Node.js 的 NPM 命令列工具安裝模組。 不過，某些模組，例如 hello HTTP 模組，都包含在 hello 核心 Node.js 套件。

已安裝的模組會儲存在 hello **node_modules** hello 根 Node.js 安裝目錄的目錄。 每個模組中 hello **node_modules**目錄維護自己**node_modules**包含它所依存的任何模組的目錄。 此外，每個必要模組都有**node_modules** 目錄。 這個遞迴目錄結構代表 hello 相依性鏈結。

此相依性鏈結結構會導致較高的應用程式使用量。 但是，它也可保證確認符合所有的相依性，然後在生產環境中也使用的 hello 模組 hello 版開發中使用。 這讓 hello 實際應用程式的行為更容易預測，並防止可能會影響使用者的版本控制問題。

## <a name="step-1-register-an-azure-ad-tenant"></a>步驟 1：註冊 Azure AD 租用戶
這個範例 toouse，您需要 Azure Active Directory 租用戶。 如果您不確定哪個租用戶，或如何 tooget 其中一個，請參閱[tooget 的 Azure AD 的租用戶](active-directory-howto-tenant.md)。

## <a name="step-2-create-an-application"></a>步驟 2：建立應用程式
接下來您需要 toosecurely 讓 Azure AD 資訊與您的應用程式的目錄中建立應用程式。  Hello 用戶端應用程式和 web API 由單一**應用程式識別碼**在此情況下，因為它們組成一個邏輯應用程式。  toocreate 的應用程式，請遵循[這些指示](active-directory-how-applications-are-added.md)。 如果您要建置企業營運應用程式，[這些額外的指示可能很實用](../active-directory-applications-guiding-developers-for-lob-applications.md)。

toocreate 應用程式：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 在 hello 上方功能表中，選取您的帳戶。 然後，在 hello**目錄**清單中，選擇您想要 tooregister hello Active Directory 租用戶應用程式。

3. 在左側 hello hello 功能表中選取**更服務**，然後選取**Azure Active Directory**。

4. 選取 [應用程式註冊]，然後選取 [新增]。

5. 請遵循 hello 提示 toocreate **Web 應用程式和/或 WebAPI**。

      * hello**名稱**hello 的應用程式描述您的應用程式 tooend 使用者。

      * hello**登入 URL**是 hello 基底 URL 的應用程式。  hello hello 範例程式碼的 URL 是的預設`https://localhost:8080`。

6. 註冊之後，Azure AD 會指派唯一的應用程式識別碼給您的應用程式。 您需要這個值在 hello 下一步 區段中，因此將它複製從 hello 應用程式頁面。

7. 從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。 hello**應用程式識別碼 URI**是您的應用程式的唯一識別碼。 hello 慣例是 toouse `https://<tenant-domain>/<app-name>`，例如： `https://contoso.onmicrosoft.com/my-first-aad-app`。

8. 建立**金鑰**應用程式從 hello**設定**頁面，然後再將它複製某處。 稍後您將會用到此資訊。

## <a name="step-3-download-nodejs-for-your-platform"></a>步驟 3：下載您的平台適用的 Node.js
toosuccessfully 使用這個範例中，您必須擁有使用中的 Node.js 的安裝。

從 [http://nodejs.org](http://nodejs.org)安裝 Node.js。

## <a name="step-4-install-mongodb-on-your-platform"></a>步驟 4：在您的平台上安裝 MongoDB
toosuccessfully 使用這個範例中，您必須擁有使用中的 MongoDB 的安裝。 您可以使用 MongoDB toomake hello 永續性的 REST API 在伺服器執行個體。

從 [http://mongodb.org](http://www.mongodb.org)安裝 MongoDB。

> [!NOTE]
> 本逐步解說假設您 hello 預設安裝和伺服器端點針對使用 MongoDB，這在撰寫本文 hello 階段是 mongodb://localhost。
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>步驟 5: Hello Restify 模組安裝在您的 web 應用程式開發介面
我們使用 Restify toobuild REST API。 Restify 是衍生自 Express 的最小且具彈性的 Node.js 應用程式架構。 它有一組強大的功能，可在 Connect 之上建置 REST API。

### <a name="install-restify"></a>安裝 Restify
1. 從 hello 命令列，變更目錄 toohello **azure ad**目錄。 如果 hello **azure ad**目錄不存在，建立它。

        `cd azuread - or- mkdir azuread; cd azuread`

2. 輸入下列命令的 hello:

    `npm install restify`

    此命令會安裝 Restify。

#### <a name="did-you-get-an-error"></a>您有收到錯誤訊息嗎？
當您在某些作業系統上使用 NPM 時，可能會收到以下錯誤：**Error: EPERM, chmod '/usr/local/bin/..'** 與您嘗試以系統管理員身分執行 hello 帳戶的建議。 如果發生這種情況，請使用 hello sudo 命令 toorun NPM 較高的權限層級。

#### <a name="did-you-get-an-error-regarding-dtrace"></a>您有收到有關 DTRACE 的錯誤訊息嗎？
安裝 Restify 時，您可能會看到如下的錯誤：

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```
Restify 提供強大機制來使用 DTrace 追蹤 REST 呼叫。 不過，許多作業系統沒有 DTrace。 您可以放心地忽略這些錯誤。

hello 這個命令的輸出應該看起來類似 toohello 下列輸出：

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a>步驟 6：在您的 Web API 中安裝 Passport.js
[Passport](http://passportjs.org/) 是 Node.js 的驗證中介軟體。 彈性和模組化，在 tooany 暗中卸除 Passport Express 為基礎或 Restify web 應用程式。 一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他等驗證。

我們已為 Azure Active Directory 開發一個策略。 我們會安裝此模組，然後再新增外掛程式的 hello Azure Active Directory 策略。

1. 從 hello 命令列，變更目錄 toohello **azure ad**目錄。

2. tooinstall passport.js 輸入 hello 下列命令：

    `npm install passport`

    hello hello 命令輸出應該看起來類似 toohello 下列：

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>步驟 7： 加入 Azure AD Passport tooyour web API
接下來我們加入 hello OAuth 策略使用`passport-azure-ad`，一套連接 Azure Active Directory tooPassport 的策略。 在這個 Rest API 範例中，我們會對持有人權杖使用此策略。

> [!NOTE]
> 雖然 OAuth2 提供可發行任何已知權杖類型的架構，但只有某些權杖類型經常使用。 承載權杖是用於保護端點 hello 最常使用的權杖。 它們是在 OAuth2 權杖的 hello 最廣泛發出型別。 許多實作假設持有者權杖是 hello 的核發權杖的唯一類型。
>
>

從 hello 命令列，變更目錄 toohello **azure ad**目錄。

型別 hello 下列命令 tooinstall hello Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

hello hello 命令輸出應該看起來類似 toohello 下列輸出：


    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>步驟 8： 加入 MongoDB 模組 tooyour web API
我們使用 MongoDB 做為資料存放區。 因此，我們需要 tooinstall hello，廣泛使用的外掛程式被呼叫的 1 toomanage 模型和結構描述。 我們也 for MongoDB。 （這也稱為 MongoDB） 需要 tooinstall hello 資料庫驅動程式。

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>步驟 9：安裝其他模組
接下來，我們會安裝其餘的必要的模組的 hello。

1. 從 hello 命令列，變更目錄 toohello **azure ad**資料夾，如果您已經不存在。

    `cd azuread`

2. 這些模組中的輸入下列命令 tooinstall hello 您**node_modules**目錄：

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>步驟 10：使用您的相依性建立 server.js
hello 立即轉譯 server.js 檔案提供我們的 web API 伺服器的大部分的 hello 功能。 我們加入大部分我們的程式碼 toothis 檔案。 生產環境中使用，我們建議您重構 hello 成較小的檔案，例如個別的路由和控制站的功能。 在此示範中，我們會在這項功能中使用 server.js。

1. 從 hello 命令列，變更目錄 toohello **azure ad**資料夾，如果您已經不存在。

    `cd azuread`

2. 建立`server.js`檔案您最愛的編輯器中，然後再加入 hello 下列資訊：

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. 儲存 hello 檔案。 我們將儘速傳回 tooit。

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>步驟 11： 建立組態檔 toostore 您 Azure AD 的設定
這個程式碼檔會從您的 Azure Active Directory 入口網站 tooPassport.js 傳遞 hello 組態參數。 當您新增 hello hello 逐步解說的第一個組件中的 hello web API toohello 入口網站時，您會建立這些組態值。 在複製 hello 程式碼之後，我們會說明哪些 tooput hello 這些參數值。

1. 從 hello 命令列，變更目錄 toohello **azure ad**資料夾，如果您已經不存在。

    `cd azuread`

2. 建立`config.js`檔案您最愛的編輯器中，然後再加入 hello 下列資訊：

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. 儲存 hello 檔案。

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>步驟 12： 加入組態值 tooyour 立即轉譯 server.js 檔
我們需要 tooread hello.config 檔案，您建立這些值在我們的應用程式。 toodo，我們在我們的應用程式新增為所需的資源 hello.config 檔案。 然後我們會在 hello config.js 文件中設定 hello 全域變數 toomatch hello 變數。

1. 從 hello 命令列，變更目錄 toohello **azure ad**資料夾，如果您已經不存在。

    `cd azuread`

2. 開啟您`server.js`檔案您最愛的編輯器中，然後再加入 hello 下列資訊：

    ```Javascript
    var config = require('./config');
    ```
3. 然後加入新的區段太`server.js`以下列程式碼的 hello:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. 儲存 hello 檔案。

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>步驟 13： 使用 1 新增 hello MongoDB 模型和結構描述資訊
此項準備現在 toostart 付清我們將這三個檔案合併成 REST API 服務。

這個逐步解說中，我們使用 MongoDB toostore 我們在步驟 4 中所述的工作。

在 hello`config.js`檔案，我們建立步驟 11 中，我們打給我們的資料庫`tasklist`，因為這是我們放在 hello 結尾我們**mogoose_auth_local**連接 URL。 您不需要 toocreate MongoDB 事先的這個資料庫。 相反地，MongoDB 這我們上建立 hello 第一次執行的伺服器應用程式 （假設該 hello 資料庫不存在）。

既然我們已告知 hello 伺服器 MongoDB 資料庫，我們都希望 toouse，我們需要 toowrite 一些額外的程式碼 toocreate hello 模型和結構描述我們的伺服器工作。

### <a name="discussion-of-hello-model"></a>Hello 模型的討論
我們的結構描述模型很簡單。 您可視需要加以擴充。

名稱： hello 分派 toohello 工作的 hello 人員名稱。 **字串**。

工作： hello 工作本身。 **字串**。

日期： hello 日期該 hello 工作會到期。 **DATETIME**。

完成： Hello 工作是否已完成。 **布林值**。

### <a name="creating-hello-schema-in-hello-code"></a>在 hello 程式碼中建立 hello 結構描述
1. 從 hello 命令列，變更目錄 toohello **azure ad**資料夾，如果您已經不存在。

    `cd azuread`

2. 開啟您`server.js`檔案您最愛的編輯器中，然後再加入 hello 下列 hello 組態項目下方的資訊：

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
    var TaskSchema = new Schema({
        owner: String,
        task: String,
        completed: Boolean,
        date: Date
    });

    // Use hello schema tooregister a model.
    mongoose.model('Task', TaskSchema);
    var Task = mongoose.model('Task');
    ```
如您所見從 hello 程式碼，我們建立結構描述第一次。 然後我們建立的 toostore hello 整個資料程式碼，因此我們定義時，我們使用的模型物件我們**路由**。

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>步驟 14：新增工作 REST API 伺服器的路由
現在，我們已經使用資料庫模型 toowork，讓我們加入 hello 路由，我們會持續使用我們的 REST API 伺服器。

### <a name="about-routes-in-restify"></a>關於 Restify 中的路由
路由在 Restify hello 相同他們沒有在 hello Express 堆疊的方式。 您可以使用 hello 您預期 hello 用戶端應用程式 toocall 的 URI，以定義路由。 通常，您會在個別的檔案中定義您的路由。 基於我們的目的，我們會將我們的路線 hello 立即轉譯 server.js 檔案中。 在生產環境中，建議您將這些路由分散到其各自的檔案。

Restify 路由的典型模式如下：

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


這是在其最基本的層級的 hello 模式。 Resitfy (及 Express) 可提供更深入的功能，例如定義應用程式類型和提供不同端點之間的複雜路由。 基於本文的目的，我們會讓這些路由保持簡單。

### <a name="add-default-routes-tooour-server"></a>新增預設路由 tooour 伺服器
我們現在將 hello 基本 CRUD 路由的建立、 擷取、 更新和刪除。

1. 從 hello 命令列，變更目錄 toohello **azure ad**資料夾，如果您已經不存在：

    `cd azuread`

2. 開啟 hello`server.js`檔案在您最愛的編輯器中，然後再新增 hello 遵循 hello 先前資料庫的項目所做的下列資訊：

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}


// Delete a task by name.

function removeTask(req, res, next) {

    Task.remove({
        task: req.params.task,
        owner: owner
    }, function(err) {
        if (err) {
            req.log.warn(err,
                'removeTask: unable toodelete %s',
                req.params.task);
            next(err);
        } else {
            log.info('Deleted task:', req.params.task);
            res.send(204);
            next();
        }
    });
}

// Delete all tasks.

function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
}


// Get a specific task based on name.

function getTask(req, res, next) {

    log.info('getTask was called for: ', owner);
    Task.find({
        owner: owner
    }, function(err, data) {
        if (err) {
            req.log.warn(err, 'get: unable tooread %s', owner);
            next(err);
            return;
        }

        res.json(data);
    });

    return next();
}

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}

```

### <a name="add-error-handling-in-our-apis"></a>在我們的 API 中新增錯誤處理
```

///--- Errors for communicating something interesting back toohello client.

function MissingTaskError() {
    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'MissingTask',
        message: '"task" is a required parameter',
        constructorOpt: MissingTaskError
    });

    this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);


function TaskExistsError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'TaskExists',
        message: owner + ' already exists',
        constructorOpt: TaskExistsError
    });

    this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);


function TaskNotFoundError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 404,
        restCode: 'TaskNotFound',
        message: owner + ' was not found',
        constructorOpt: TaskNotFoundError
    });

    this.name = 'TaskNotFoundError';
}

util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="step-15-create-your-server"></a>步驟 15：建立伺服器
我們已定義資料庫並已備妥路由。 最後一件事 toodo hello 會新增管理我們呼叫 hello 伺服器執行個體。

在 Restify （和 Express） 中，您可以執行的自訂作業的 REST API 伺服器，但我們還是 toouse hello 最基本的安裝程式基於我們的目的。

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>步驟 16： 新增 hello 路由 toohello 伺服器 （不含現在驗證）
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler.
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>步驟 17： 執行 hello 伺服器 （如果您之前新增 OAuth 支援）
新增驗證之前，請先測試您的伺服器。

最簡單方式 tootest hello 您的伺服器是使用 curl 命令列中。 這樣做之前，我們需要公用程式，讓我們 tooparse 輸出為 JSON。

1. 安裝下列 JSON 工具 （所有 hello 遵循範例會都使用此工具） 的 hello:

    `$npm install -g jsontool`

    這會安裝 hello JSON 工具全域。 既然我們已經完成動作，讓我們來播放與 hello 伺服器：

2. 首先，確定您的 MongoDB 執行個體正在執行：

    `$sudo mongod`

3. 然後，變更 toohello 目錄，並啟動捲曲：

    `$ cd azuread` `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4. 接著，我們可以透過以下方式新增工作：

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    應該 hello 回應：

        ```Shell
        HTTP/1.1 201 Created
        Connection: close
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Headers: X-Requested-With
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 5
        Date: Tue, 04 Feb 2014 01:02:26 GMT
        Hello
        ```
    而且我們可以透過以下方式列出 Brandon 的工作：

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

如果所有可以運作，我們準備 tooadd OAuth toohello REST API 伺服器。

您必須將 REST API 伺服器搭配 MongoDB 使用！

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>步驟 18： 加入驗證 tooour REST API 伺服器
既然我們已有執行中的 REST API，我們就可以讓它在 Azure AD 中發揮其價值。

從 hello 命令列，變更目錄 toohello **azure ad**資料夾，如果您已經不存在。

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>使用 hello OIDCBearerStrategy 所包含的 passport azure ad
到目前為止，我們已經建置典型的 REST TODO 伺服器，且其中不含任何授權種類。 這是我們將其結合在一起的起點。

1. 首先，我們需要 tooindicate 我們想要 toouse Passport。 在其他伺服器設定之後緊接著執行此動作：

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > 當您撰寫應用程式開發介面，我們建議您一律連結 hello 資料 toosomething 唯一從 hello 使用者的 hello 權杖無法偽造。 當這個伺服器儲存 TODO 項目時，它會儲存根據 hello hello 語彙基元 （透過 token.oid 稱為） 中的 hello 使用者我們放在 hello 「 擁有者 」 欄位中物件識別碼。 這可確保只有該使用者可以存取自己的 TODO。 讓外部使用者可以要求 hello TODOs 的其他人，即使它們驗證 「 擁有者 」 的 hello 應用程式開發介面中沒有任何風險。                    

2. 下一步我們將使用隨附的 hello 承載策略`passport-azure-ad`。 現在看看 hello 程式碼，我們將稍後說明 hello rest。 將這段程式碼放在您上面所貼內容的後面：

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
    **/

    var findById = function(id, fn) {
        for (var i = 0, len = users.length; i < len; i++) {
            var user = users[i];
            if (user.sub === id) {
                log.info('Found user: ', user);
                return fn(null, user);
            }
        }
        return fn(null, null);
    };


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Passport 會使用適用於它的所有策略 (Twitter、Facebook 等) 且所有策略寫入器都依循的類似模式。 查看 hello 策略，您會看到我們做為 hello 參數傳遞它具有語彙基元和完成的函式。 其功能之後，來自回 toous hello 策略。 它之後，我們 hello 使用者和儲存存放 hello 語彙基元，我們就不需要為其 tooask 一次。

> [!IMPORTANT]
> hello 先前的程式碼會發生 tooauthenticate tooour 伺服器的任何使用者。 這就是所謂的自動註冊。 在生產伺服器中，我們建議您要讓所有人都必須先經歷您所決定的註冊過程。 這通常是您在取用者應用程式，這可讓您與 Facebook tooregister 但然後要求 toofill 出額外的資訊，請參閱 hello 模式。 如果這不是命令列程式，我們無法從傳回並再要求其他資訊的 hello 使用者 toofill hello token 物件擷取已 hello 電子郵件。 因為這是在測試伺服器，我們直接將它們 toohello 記憶體中資料庫。
>
>

### <a name="protect-some-endpoints"></a>保護某些端點
您藉由指定 hello 保護端點`passport.authenticate()`想 toouse hello 通訊協定呼叫。

toomake 我們伺服端程式碼進行了多個有趣，讓我們來編輯 hello 路由。

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>步驟 19：再次執行應用程式伺服器，並確保它會拒絕您的要求
讓我們使用`curl`再次 toosee 如果我們現在有 OAuth2 保護對我們的端點。 我們會在對此端點執行任何用戶端 SDK 之前，執行此動作。 hello 所傳回的標頭應為足夠 tootell 我們如果我們要向 hello 正確的路徑。

1. 首先，確定您的 MongoDB 執行個體正在執行：

    `$sudo mongod`

2. 然後，變更 toohello 目錄，並啟動捲曲。

      `$ cd azuread` `$ node server.js`

3. 嘗試基本 POST。

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401 是您所需這裡的 hello 回應。 此回應指出 hello Passport 該層正嘗試 tooredirect toohello 授權端點，而這正是您想要。

## <a name="next-steps"></a>後續步驟
在未使用 OAuth2 相容用戶端的情況下，您已經儘可能地使用此伺服器的所有功能。 您必須透過其他的逐步解說 toogo。

您現在已經學會如何 tooimplement 使用 REST API Restify 和 OAuth2。 您也可以開發您的服務，並學習更多程式碼 tookeep 如何 toobuild 在此範例。

如果您想要在下一個步驟中 hello ADAL 旅程中，以下是我們建議您將使用的一些支援的 ADAL 用戶端。

複製下 tooyour 開發人員電腦，並設定 hello 逐步解說中所述。

[ADAL for iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[ADAL for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
