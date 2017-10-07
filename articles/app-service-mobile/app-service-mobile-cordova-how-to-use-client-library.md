---
title: "aaaHow tooUse Azure 行動應用程式的 Apache Cordova 外掛程式"
description: "如何 tooUse Azure 行動應用程式的 Apache Cordova 外掛程式"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>如何針對 Azure 行動應用程式的 toouse Apache Cordova 用戶端程式庫
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

本指南將教導您 tooperform 常見的案例，使用最新的 hello [Azure 行動應用程式的 Apache Cordova 外掛程式]。 如果您是新 tooAzure 行動應用程式，請先完成[Azure 行動應用程式快速入門]toocreate 後端，建立資料表，並下載預先建立的 Apache Cordova 專案。 本指南中，我們將重點放在用戶端 hello Apache Cordova 外掛程式。

## <a name="supported-platforms"></a>支援的平台
此 SDK 可在 iOS、Android 和 Windows 裝置上支援 Apache Cordova v6.0.0 和更新版本。  hello 平台支援如下所示：

* Android API 19-24 (KitKat 至 Nougat)。
* iOS 8.0 版和更新版本。
* Windows Phone 8.1。
* 通用 Windows 平台。

## <a name="Setup"></a>設定和必要條件
本指南假設您已建立包含資料表的後端。 本指南假設該 hello 資料表具有 hello 以這些教學課程中的 hello 資料表相同的結構描述。 本指南也會假設您已經加入 hello tooyour Apache Cordova 外掛程式的程式碼。  如果您不這麼做，您可以加入 hello Apache Cordova 外掛程式 tooyour 專案 hello 命令列上：

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

如需有關建立 [第一個 Apache Cordova 應用程式]的詳細資訊，請參閱其文件。

## <a name="ionic"></a>設定 Ionic v2 應用程式

tooproperly Ionic v2 專案設定中，第一次建立基本應用程式，並加入 hello Cordova 外掛程式：

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

新增下列幾行太 hello`app.component.ts` toocreate hello 用戶端物件：

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

您可以立即建立，並在 hello 瀏覽器中執行 hello 專案：

```
ionic platform add browser
ionic run browser
```

hello Azure 行動應用程式的 Cordova 外掛程式支援兩個 Ionic v1 和 v2 應用程式。  只有 hello Ionic v2 應用程式需要的其他宣告 hello`WindowsAzure`物件。

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>作法：驗證使用者
Azure App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶及 Twitter) 來驗證與授權應用程式使用者。 您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。 您也可以使用伺服器指令碼中的 hello 身分識別通過驗證的使用者 tooimplement 授權規則。 如需詳細資訊，請參閱 hello[開始使用驗證]教學課程。

使用驗證時的 Apache Cordova 應用程式中，必須具備下列 Cordova 外掛程式的 hello:

* [cordova-plugin-device]
* [cordova-plugin-inappbrowser]

支援兩個驗證流程：伺服器流程和用戶端流程。  hello 伺服器流程提供 hello 最簡單的驗證體驗，因為它是倚賴 hello 提供者 web 驗證介面。 hello 用戶端流程可讓與裝置特定功能的更深入整合這類單一登入為依賴特定提供者裝置特有的 Sdk。

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>做法︰設定行動 App Service 以使用外部重新導向 URL。
Apache Cordova 應用程式的數種使用回送功能 toohandle OAuth UI 流動。  在 localhost 上的 OAuth UI 流量會造成問題，因為 hello 驗證服務只知道如何 tooutilize 您預設的服務。  有問題的 OAuth UI 流程範例包括︰

* hello Ripple 模擬器。
* Ionic 的即時重新載入。
* 在本機執行 hello 行動後端
* 執行比 hello 一個提供給驗證的不同 Azure App Service 中的 hello 行動後端。

請遵循這些指示 tooadd 您的本機設定 toohello 組態：

1. 登入 toohello [Azure 入口網站]
2. 選取**所有資源**或**應用程式服務**然後按一下 [hello 行動應用程式名稱。
3. 按一下 [工具] 
4. 按一下**資源總管**hello 觀察功能表中，然後按一下**移**。  新的視窗或索引標籤隨即開啟。
5. 展開 hello **config**， **authsettings** hello 左側導覽中您站台的節點。
6. 按一下 [編輯] 
7. 尋找 hello"allowedExternalRedirectUrls"項目。  它可能設定 toonull 或值的陣列。  變更 hello 值 toohello 下列值：

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Hello Url 取代為您的服務的 hello Url。  範例包括"http://localhost:3000 」 （適用於 hello Node.js 範例服務) 或 「 http://localhost:4400"（針對 hello Ripple 服務）。  不過，這些 Url 是範例-您的情況，包括 hello 範例中所述的 hello 服務可能會不同。
8. 按一下 hello**讀/寫**hello hello 畫面右上角的按鈕。
9. 按一下綠色的 hello**放**] 按鈕。

此時會儲存 hello 設定。  請勿關閉 hello 瀏覽器視窗中，直到 hello 設定儲存。
也新增回送 Url toohello CORS 的這些設定您的應用程式服務：

1. 登入 toohello [Azure 入口網站]
2. 選取**所有資源**或**應用程式服務**然後按一下 [hello 行動應用程式名稱。
3. hello 設定] 刀鋒視窗會自動開啟。  如果沒有，請按一下 [所有設定] 。
4. 按一下**CORS** hello 應用程式開發介面] 功能表底下。
5. 輸入您想 tooadd hello 提供的方塊中的 hello URL，然後按 Enter。
6. 視需要輸入其他的 URL。
7. 按一下**儲存**toosave hello 設定。

需要大約 10-15 秒 hello 新設定 tootake 效果。

## <a name="register-for-push"></a>作法：註冊推播通知
安裝 hello [phonegap 外掛程式的推播]toohandle 推播通知。  此外掛程式可以輕鬆地新增使用`cordova plugin add`命令 hello 命令列上，或透過 Visual Studio 中的 hello Git 外掛程式安裝程式。  以下在 Apache Cordova 應用程式中的程式碼會為您的裝置註冊推播通知：

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

使用從 hello 伺服器 hello 通知中樞 SDK toosend 推播通知。  永遠不要直接從用戶端傳送推播通知。 這樣做，可以使用的 tootrigger 阻絕服務攻擊通知中樞或 hello PNS。  hello PNS 可能禁止您的流量，因為這類攻擊。

## <a name="more-information"></a>詳細資訊

您可以在 [API 文件](http://azure.github.io/azure-mobile-apps-js-client/)中找到 API 詳細資訊。

<!-- URLs. -->
[Azure 入口網站]: https://portal.azure.com
[Azure Mobile Apps 快速啟動]: app-service-mobile-cordova-get-started.md
[開始使用驗證]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[適用於 Azure Mobile Apps 的 Apache Cordova 外掛程式]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[第一個 Apache Cordova 應用程式]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
