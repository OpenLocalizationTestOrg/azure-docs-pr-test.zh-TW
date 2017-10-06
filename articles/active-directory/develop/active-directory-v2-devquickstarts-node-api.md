---
title: "使用 Node.js 的 Azure Active Directory v2.0 web API aaaSecure |Microsoft 文件"
description: "了解如何 toobuild Node.js web API 可接受同時從個人 Microsoft 帳戶和工作或學校帳戶的語彙基元。"
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a>使用 Node.js 保護 Web API 安全
> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能搭配 hello v2.0 端點。 toodetermine 是否應該使用 hello v2.0 端點或 hello v1.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

當您使用 hello Azure Active Directory (Azure AD) v2.0 的端點時，您可以使用[OAuth 2.0](active-directory-v2-protocols.md)存取權杖 tooprotect 您的 web API。 如果使用者同時有個人 Microsoft 帳戶及公司或學校帳戶，只要透過 OAuth 2.0 存取權杖，就能安全地存取您的 Web API。

*Passport* 是 Node.js 的驗證中介軟體。 您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 resitify Web 應用程式。 在 Passport 中，一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他選項進行驗證。 我們已為 Azure AD 開發一個策略。 在本文中，我們會示範如何 tooinstall hello 模組，並再新增 hello Azure AD`passport-azure-ad`外掛程式。

## <a name="download"></a>下載
此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs)。 toofollow hello 教學課程中，您可以[下載為.zip 檔案的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip)，或再製 hello 基本架構：

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

您也可以取得 hello 完成應用程式在此教學課程中的 hello 結尾處。

## <a name="1-register-an-app"></a>1：註冊應用程式
建立新的應用程式在[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或遵循[這些詳細步驟](active-directory-v2-app-registration.md)tooregister 應用程式。 請確定您已執行下列動作：

* 複製 hello**應用程式識別碼**指派 tooyour 應用程式。 您在本教學課程中將需要用到它。
* 新增 hello**行動**平台應用程式。
* 複製 hello**重新導向 URI**從 hello 入口網站。 您必須使用 hello 預設 URI 值`urn:ietf:wg:oauth:2.0:oob`。

## <a name="2-install-nodejs"></a>2：安裝 Node.js
您必須在此教學課程 toouse hello 範例，[安裝 Node.js](http://nodejs.org)。

## <a name="3-install-mongodb"></a>3︰安裝 MongoDB
toosuccessfully 使用這個範例中，您必須[安裝 MongoDB](http://www.mongodb.org)。 在此範例中，您使用 MongoDB toomake 您持續性的 REST API 在伺服器執行個體。

> [!NOTE]
> 在本文中，我們假設您使用 MongoDB hello 預設安裝和伺服器端點： mongodb://localhost。
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a>4： 安裝 hello restify 模組在您的 web 應用程式開發介面
我們使用 Resitfy toobuild REST API。 Restify 是衍生自 Express 的最小且具彈性的 Node.js 應用程式架構。 Restify 具有一組強固的功能，您可以使用 toobuild 連接之上的 REST Api。

### <a name="install-restify"></a>安裝 restify
1.  在命令提示字元中，變更 hello 目錄太**azure ad**:

    `cd azuread`

    如果 hello **azure ad**目錄不存在，建立它：

    `mkdir azuread`

2.  安裝 restify：

    `npm install restify`

    hello 這個命令的輸出應該看起來像這樣：

    ```
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
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a>您有收到錯誤訊息嗎？
某些在作業系統上，當您使用 hello`npm`命令時，您可能會看到此訊息： `Error: EPERM, chmod '/usr/local/bin/..'`。 hello 錯誤後再次嘗試執行 hello 帳戶系統管理員身分的要求。 如果發生這種情況，使用 hello 命令`sudo`toorun`npm`較高的權限層級。

#### <a name="did-you-get-an-error-related-toodtrace"></a>您是否已取得相關的錯誤 tooDTrace？
當您安裝 restify 時，您可能會看到此訊息︰

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
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

Restify 具有強大的機制，tootrace 使用 DTrace REST 呼叫。 不過，在許多作業系統上無法使用 DTrace。 您可以放心地忽略此錯誤訊息。


## <a name="5-install-passportjs-in-your-web-api"></a>5：在您的 Web API 中安裝 Passport.js
1.  Hello 命令提示字元，變更 hello 目錄太**azure ad**。

2.  安裝 Passport.js：

    `npm install passport`

    hello hello 命令輸出應該看起來像這樣：

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a>6： 加入 passport azure ad tooyour web API
接下來，加入 hello OAuth 策略中，使用 passport azure ad。 `passport-azuread` 是一套將 Azure AD 連線至 Passport 的策略。 在這個 Rest API 範例中，我們會對持有人權杖使用此策略。

> [!NOTE]
> 雖然 OAuth2.0 提供可發行任何已知權杖類型的架構，但只有某些權杖類型經常使用。 持有者權杖是常用的 tooprotect 的端點。 持有者權杖會在 OAuth 2.0 權杖的 hello 最廣泛發出型別。 許多的 OAuth 2.0 實作假設持有者權杖是 hello 的發行權杖的唯一類型。
> 
> 

1.  在命令提示字元中，變更 hello 目錄太**azure ad**。

    `cd azuread`

2.  安裝 hello Passport.js`passport-azure-ad`模組：

    `npm install passport-azure-ad`

    hello hello 命令輸出應該看起來像這樣：

    ```
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
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a>7： 加入 MongoDB 模組 tooyour web API
在此範例中，我們將使用 MongoDB 作為資料存放區。 

1.  安裝 1，廣泛使用外掛程式，toomanage 模型和結構描述： 

    `npm install mongoose`

2.  安裝適用於 MongoDB，這也稱為 MongoDB hello 資料庫驅動程式。

    `npm install mongodb`

## <a name="8-install-additional-modules"></a>8：安裝其他模組
安裝 hello 剩餘所需的模組。

1.  在命令提示字元中，變更 hello 目錄太**azure ad**:

    `cd azuread`

2.  輸入下列命令的 hello。 hello 命令會安裝下列 node_modules 目錄中的模組的 hello:

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a>9：為您的相依性建立 Server.js 檔案
立即轉譯 Server.js 檔案保存 hello 大部分的 web API 伺服器的 hello 功能。 將大部分的程式碼 toothis 檔案。 生產環境中使用，您可以像重構 hello 功能較小的檔案不同的路徑及控制站。 在本文中，我們會針對此目的使用 Server.js。

1.  在命令提示字元中，變更 hello 目錄太**azure ad**:

    `cd azuread`

2.  使用您選擇的編輯器，建立 Server.js 檔案。 新增下列資訊 toohello 檔的 hello:

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  儲存 hello 檔案。 您很快就會傳回 tooit。

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a>10： 建立您的 Azure AD 設定的組態檔 toostore
這個程式碼檔會從您的 Azure AD 入口網站 tooPassport.js 傳遞 hello 組態參數。 當您在 hello 文章 hello 開頭加入 hello web API toohello 入口網站，您會建立這些組態值。 複製 hello 程式碼之後，我們將說明哪些 tooput hello 這些參數值。

1.  在命令提示字元中，變更 hello 目錄太**azure ad**:

    `cd azuread`

2.  在編輯器中，建立 Config.js 檔案。 新增 hello 下列資訊：

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a>必要值

*   **IdentityMetadata**： 這是 where `passport-azure-ad` hello 身分識別提供者 (IDP) 和 hello 金鑰 toovalidate hello JSON Web 權杖 (Jwt) 的組態資料的外觀。 如果您使用 Azure AD，您可能不想 toochange 這。

*   **對象**: hello 入口網站從您重新導向 URI。

> [!NOTE]
> 請經常變換金鑰。 請務必一律提取從 hello"openid_keys 」 的 URL，，和該 hello 應用程式可以存取網際網路 hello。
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a>11： 加入 hello 組態 tooyour 立即轉譯 Server.js 檔
您的應用程式必須從您剛才建立的 hello 組態檔 tooread hello 值。 為您的應用程式中有項必要資源新增 hello.config 檔案。 設定 hello 全域變數 toothose Config.js 中。

1.  Hello 命令提示字元，變更 hello 目錄太**azure ad**:

    `cd azuread`

2.  在編輯器中開啟 Server.js。 新增 hello 下列資訊：

    ```Javascript
    var config = require('./config');
    ```

3.  加入新的區段 tooServer.js:

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>12: hello MongoDB 模型和結構描述資訊加入使用 1
接著，在 REST API 服務中連接這三個檔案。

在本文中，我們使用 MongoDB toostore 我們的工作。 我們在「步驟 4」中討論到這一點。

在您建立的步驟 11 hello Config.js 檔案，您的資料庫稱為*tasklist*。 這是您放置在 hello mongoose_auth_local 連線 URL 的結尾。 您不需要 toocreate MongoDB 事先的這個資料庫。 hello 資料庫上建立 hello 第一次執行的伺服器應用程式 （假設 hello 資料庫尚未存在）。

您告知 hello 伺服器哪些 MongoDB 資料庫 toouse。 接下來，您需要 toowrite 一些額外的程式碼 toocreate hello 模型和結構描述伺服器的工作。

### <a name="hello-model"></a>hello 模型
hello 結構描述模型是非常基本。 需要的話，您可以展開它。 

hello 結構描述模型有下列值：

*   **NAME**。 hello 人員指派的 toohello 工作。 這是**字串**值。
*   **TASK**。 hello hello 工作名稱。 這是**字串**值。
*   **DATE**。 hello 日期該 hello 工作會到期。 這是**日期時間**值。
*   **COMPLETED**。 Hello 工作是否完成。 這是**布林**值。

### <a name="create-hello-schema-in-hello-code"></a>建立 hello 程式碼中的 hello 結構描述
1.  在命令提示字元中，變更 hello 目錄太**azure ad**:

    `cd azuread`

2.  在編輯器中開啟 Server.js。 下方 hello 組態項目加入 hello 下列資訊：

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

此程式碼會 toohello MongoDB 伺服器連接。 它也會傳回結構描述物件。

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a>使用 hello 結構描述，在 hello 程式碼中建立您的模型
下方 hello 前面程式碼，加入下列程式碼的 hello:

```Javascript
// Create a basic schema toostore your tasks and users.
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

如您所見從 hello 程式碼，首先請建立您的結構描述。 接下來，您可以建立模型物件。 使用 hello 模型物件 toostore hello 整個資料程式碼，當您定義您**路由**。

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a>13：新增工作 REST API 伺服器的路由
現在您有與資料庫模型 toowork，新增 hello 路由，您會使用 REST API 伺服器。

### <a name="about-routes-in-restify"></a>關於 restify 中的路由
中的路由 restify 完全 hello 如此當您使用的相同方式 hello Express 堆疊的工作。 您可以使用 hello 您預期 hello 用戶端應用程式 toocall 的 URI，以定義路由。 通常，您會在個別的檔案中定義您的路由。 在本教學課程中，我們會將路由放在 Server.js 中。 在生產用途上，建議您將這些路由納入您自己的檔案中。

Restify 路由的典型模式是：

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


這是在 hello 最基本的層級的 hello 模式。 Restify （和 Express） 提供更深層的功能，例如 hello 能力 toodefine 應用程式類型和複雜的路由，不同的端點上。

#### <a name="add-default-routes-tooyour-server"></a>新增預設路由 tooyour 伺服器
新增基本 CRUD 路由 hello:**建立**，**擷取**，**更新**，和**刪除**。

1.  在命令提示字元中，變更 hello 目錄太**azure ad**:

    `cd azuread`

2.  在編輯器中開啟 Server.js。 下面 hello 您稍早建立的資料庫項目、 新增 hello 下列資訊：

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
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
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
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

### <a name="add-error-handling-for-hello-routes"></a>加入 hello 路由的錯誤處理
加入一些錯誤，處理讓您能夠通訊回復 toohello hello 您遇到的問題相關的用戶端。

新增下列 hello 程式碼，您已經撰寫下列程式碼的 hello:

```Javascript
///--- Errors for communicating something more information back toohello client.
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


## <a name="14-create-your-server"></a>14：建立伺服器
hello 最後一件事 toodo 是 tooadd 您的伺服器執行個體。 hello 伺服器執行個體都會管理您的呼叫。

Restify (及 Express) 有深入的自訂功能可搭配 REST API 伺服器使用。 在本教學課程中，我們使用 hello 最基本的安裝程式。

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a>15： 加入 hello 路由 （不含的立即驗證）
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
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
// Register a default '/' handler
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
## <a name="16-run-hello-server"></a>16： 執行 hello 伺服器
它是個不錯的主意 tootest 您之前加入驗證的伺服器。

最簡單方式 tootest hello 您的伺服器是在命令提示字元使用 curl。 toodo，您需要簡單的公用程式，可讓您 tooparse 輸出為 JSON。 

1.  安裝 hello 遵循範例中的 hello JSON 工具，我們使用：

    `$npm install -g jsontool`

    這會安裝 hello JSON 工具全域。

2.  請確定您的 MongoDB 執行個體正在執行：

    `$sudo mongod`

3.  變更 hello 目錄太**azure ad**，然後執行 curl:

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
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

4.  tooadd 工作：

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

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

5.  Brandon 的工作清單︰

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

如果所有這些命令會執行不會發生錯誤，您就準備好 tooadd OAuth toohello REST API 伺服器。

「您現在已具有 REST API 伺服器和 MongoDB！」

## <a name="17-add-authentication-tooyour-rest-api-server"></a>17： 加入驗證 tooyour REST API 伺服器
既然您已執行的 REST API 時，設定 toouse 它與 Azure AD。

在命令提示字元中，變更 hello 目錄太**azure ad**:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a>使用 hello oidcbearerstrategy，並包含的 passport azure ad
到目前為止，您已經建置典型的 REST TODO 伺服器，且其中不含任何授權種類。 現在，新增驗證。

首先，表示您想要 toouse Passport。 將這段程式碼放在緊鄰您先前的伺服器設定後面：

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> 當您撰寫應用程式開發介面時，它會為從 hello 使用者的 hello 權杖的唯一資料 toosomething 無法偽造最好 tooalways 連結 hello。 當這個伺服器儲存 TODO 項目時，它會儲存根據 hello 權杖 （稱為透過 token.sub） 中的 hello 使用者訂用帳戶 ID。 您可以將 hello token.sub hello 「 擁有者 」 欄位中。 這可確保只有該使用者可以存取 hello 使用者 TODOs。 沒有其他人可以存取已輸入的 hello TODOs。 沒有公開正在 hello 應用程式開發介面的 「 擁有者 」。 外部使用者可以要求其他使用者的 TODO (即使通過驗證)。
> 
> 

接下來，使用隨附的 hello 開啟識別碼連接承載策略`passport-azure-ad`。 將這段程式碼放在您稍早貼上的程式碼後面：

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
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
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

Passport 會針對其所有策略 (Twitter、Facebook 等) 使用類似的模式。 所有的策略寫入器會遵守 toohello 模式。 傳送嗨策略`function()`使用語彙基元和`done`做為參數。 所有其功能之後，就會傳回 hello 策略。 儲存 hello 使用者並存放 hello 語彙基元，因此您不需要為其 tooask 一次。

> [!IMPORTANT]
> hello 上述程式碼會採用任何使用者，可以驗證 tooyour 伺服器。 這就是所謂的自動註冊。 在實際執行伺服器上，您不想 toolet 任何人而不需要先經過您選擇註冊程序，它們。 這通常是您在取用者應用程式中看到的 hello 模式。 hello 應用程式可能會讓您與 Facebook tooregister 但然後它會要求您 tooenter 其他資訊。 如果您沒有使用命令列程式在此教學課程，您無法從 hello 傳回的語彙基元物件擷取 hello 電子郵件。 然後，您可能會要求 hello 使用者 tooenter 額外資訊。 因為這是在測試伺服器，您會加入 hello 使用者直接 toohello 記憶體中資料庫。
> 
> 

### <a name="protect-endpoints"></a>保護端點
藉由指定 hello 保護端點**passport.authenticate()**想 toouse hello 通訊協定呼叫。

您可以在伺服器程式碼中編輯路由，以利用更進階的選項︰

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a>18︰再次執行伺服器應用程式
使用 curl 再次 toosee，如果您有 OAuth 2.0 保護對您的端點。 請在您針對這個端點執行任何用戶端 SDK 之前這樣做。 傳回的 hello 標頭應該告知您的驗證是否正常運作。

1.  請確定您的 MongoDB 執行個體正在執行：

    `$sudo mongod`

2.  變更 toohello **azure ad**目錄，再使用 curl:

    `$ cd azuread`

    `$ node server.js`

3.  嘗試基本的 POST 方法：

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401 回應指出 hello Passport 該層正嘗試 tooredirect toohello 授權端點，而這正是您想要。

「您現在擁有一項使用 OAuth 2.0 的 REST API 服務！」

在未使用 OAuth 2.0 相容用戶端的情況下，您已經儘可能地使用此伺服器的所有功能。 因此，您需要 tooreview 其他教學課程。

## <a name="next-steps"></a>後續步驟
供參考，完成的 hello 範例 （不含您的組態值） 依現狀[.zip 檔案](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip)。 您也可以從 GitHub 加以複製：

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

現在，您可以移動 toomore 進階主題上。 您可能會想 tootry[安全 Node.js web 應用程式使用 hello v2.0 端點](active-directory-v2-devquickstarts-node-web.md)。

以下是一些其他資源：

* [Azure AD v2.0 開發人員指南](active-directory-appmodel-v2-overview.md)
* [Stack Overflow "azure-active-directory" 標籤 (英文)](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>取得產品的安全性更新
我們鼓勵 toosign 向上 toobe 安全性事件發生時收到通知。 在 hello [Microsoft 技術安全性通知](https://technet.microsoft.com/security/dd252948)頁面上，訂閱 tooSecurity 摘要報告警示。

