---
title: "aaaHow tooUse hello Azure 行動應用程式的 JavaScript SDK"
description: "如何 tooUse v Azure 行動應用程式"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>如何 tooUse hello Azure 行動應用程式的 JavaScript 用戶端程式庫
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

本指南將教導您 tooperform 常見的案例，使用最新的 hello [Azure 行動應用程式的 JavaScript SDK]。 如果您是新 tooAzure 行動應用程式，請先完成[Azure 行動應用程式快速入門]toocreate 後端及建立資料表。 在本指南中，我們會著重在使用 HTML/JavaScript Web 應用程式中的 hello 行動後端。

## <a name="supported-platforms"></a>支援的平台
我們限制瀏覽器支援 toohello 目前，和最後一個版本的 hello 主要瀏覽器： Google Chrome、 Microsoft Edge、 Microsoft Internet Explorer 和 Mozilla Firefox。  我們預期 hello SDK toofunction 任何較新型的瀏覽器。

hello 發佈套件為通用 JavaScript 模組，讓它支援 AMD 的全域與 CommonJS 格式。

## <a name="Setup"></a>設定和必要條件
本指南假設您已建立包含資料表的後端。 本指南假設該 hello 資料表具有 hello 以這些教學課程中的 hello 資料表相同的結構描述。

安裝 Azure 行動應用程式 JavaScript SDK hello 可透過 hello`npm`命令：

```
npm install azure-mobile-apps-client --save
```

hello 程式庫也可用為 ES2015 模組，例如 Browserify 和 Webpack，以及為 AMD 程式庫的 CommonJS 環境內。  例如：

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

您也可以直接從我們 CDN 下載使用的預先建立的 hello SDK 版本：

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>作法：驗證使用者
Azure App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶及 Twitter) 來驗證與授權應用程式使用者。 您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。 您也可以使用伺服器指令碼中的 hello 身分識別通過驗證的使用者 tooimplement 授權規則。 如需詳細資訊，請參閱 hello[開始使用驗證]教學課程。

支援兩個驗證流程：伺服器流程和用戶端流程。  hello 伺服器流程提供 hello 最簡單的驗證體驗，因為它是倚賴 hello 提供者 web 驗證介面。 hello 用戶端流程可讓與裝置特定功能的更深入整合這類單一登入因為這樣必須提供者特有的 Sdk。

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>做法︰設定行動 App Service 以使用外部重新導向 URL。
JavaScript 應用程式的數種使用回送功能 toohandle OAuth UI 流動。  這些功能包括：

* 在本機執行服務
* 使用即時重新載入以 hello Ionic 架構
* 重新導向 tooApp 服務進行驗證。

在本機執行會造成問題，因為根據預設，應用程式服務驗證，才設定 tooallow 從您的行動裝置應用程式後端的存取。 使用下列步驟 toochange hello 應用程式服務設定 tooenable 驗證時在本機執行 hello 伺服器 hello:

1. 登入 toohello [Azure 入口網站]
2. 瀏覽 tooyour 行動裝置應用程式後端。
3. 選取**資源總管**在 hello**開發工具**功能表。
4. 按一下**移**tooopen hello 資源總管，您的行動裝置應用程式後端，在新的索引標籤或視窗中。
5. 展開 hello **config** > **authsettings**您應用程式節點。
6. 按一下 hello**編輯**按鈕 tooenable 編輯 hello 資源。
7. 尋找 hello **allowedExternalRedirectUrls**元素，其應為 null。 在陣列中新增 URL：

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Hello hello 陣列中的 Url 取代為您的服務，即在此範例中的 hello Url `http://localhost:3000` hello 本機 Node.js 範例服務。 您也可以使用`http://localhost:4400`hello Ripple 服務或某些其他 URL，根據您的應用程式的設定方式。
8. 在 hello hello 頁面頂端，按一下 [**讀/寫**，然後按一下 [**放**toosave 您的更新。

您也需要 tooadd hello 相同回送 Url toohello CORS 白名單的設定：

1. 瀏覽後 toohello [Azure 入口網站]。
2. 瀏覽 tooyour 行動裝置應用程式後端。
3. 按一下**CORS**在 hello **API**功能表。
4. 輸入每個 URL 中空白 hello**允許出處**文字方塊。  隨即會建立新的文字方塊。
5. 按一下 [儲存] 

Hello 後端的更新之後，您將應用程式中是無法 toouse hello 新的回送 Url。

<!-- URLs. -->
[Azure Mobile Apps 快速啟動]: app-service-mobile-cordova-get-started.md
[開始使用驗證]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure 入口網站]: https://portal.azure.com/
[適用於 Azure Mobile Apps 的 JavaScript SDK]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
