---
title: "行動應用程式與 Apache Cordova aaaAdd 驗證 |Microsoft 文件"
description: "深入了解如何在您的 Apache Cordova 應用程式透過不同的身分識別提供者，包括 Google、 Facebook、 Twitter 和 Microsoft Azure App Service tooauthenticate 使用者 toouse 行動應用程式。"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>新增驗證 tooyour Apache Cordova 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>摘要
在本教學課程中，您可以將驗證 toohello todolist 快速入門專案上使用支援的身分識別提供者的 Apache Cordova。 本教學課程根據 hello[開始使用行動應用程式]教學課程中，您必須先完成。

## <a name="register"></a>註冊您的應用程式進行驗證並設定 hello 應用程式服務
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[觀看示範類似步驟的影片](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>限制 tooauthenticated 使用者權限
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

現在，您可以確認已停用該匿名存取 tooyour 後端。 在 Visual Studio 中：

* 開啟 hello 時完成 hello 教學課程所建立的專案[開始使用行動應用程式]。
* 執行您的應用程式在 hello **Google Android 模擬器**。
* 請確認 hello 應用程式啟動之後，會顯示非預期的連線失敗。

接下來，從 hello 行動裝置應用程式後端要求的資源之前更新 hello tooauthenticate 的應用程式使用者。

## <a name="add-authentication"></a>新增驗證 toohello 應用程式
1. 開啟您的專案中**Visual Studio**，然後開啟 hello`www/index.html`檔案進行編輯。
2. 找出 hello `Content-Security-Policy` hello 標頭區段中的中繼標籤。  新增 hello OAuth 主機 toohello 允許來源清單。

   | 提供者 | SDK 提供者名稱 | OAuth 主機 |
   |:--- |:--- |:--- |
   | Azure Active Directory | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://accounts.google.com |
   | Microsoft | microsoftaccount | https://login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    content-security-policy (針對 Azure Active Directory 實作) 的範例如下所示：

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    取代`https://login.microsoftonline.com`與 hello OAuth host hello 上述資料表。  如需 hello meta 標記，內容安全性原則的詳細資訊，請參閱 hello[內容安全性原則文件]。

    在適當的行動裝置上使用時，某些驗證提供者不需要變更 Content-Security-Policy。  例如，在 Android 裝置上使用 Google 驗證時不需要 Content-Security-Policy 變更。

3. 開啟 hello`www/js/index.js`檔案進行編輯，找出 hello`onDeviceReady()`方法，並在建立 hello 用戶端程式碼會加入下列程式碼的 hello:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    此程式碼取代 hello 的現有程式碼會建立 hello 資料表參考，並重新整理 hello UI。

    hello login() 方法開頭 hello 提供者的驗證。 hello login() 方法是傳回 JavaScript 承諾 async 函式。  hello rest 的 hello 初始化置於 hello 承諾回應，使它不會執行直到 hello login() 方法完成為止。

4. 在您剛才加入的 hello 程式碼，取代`SDK_Provider_Name`與 hello 登入提供者名稱。 例如，針對 Azure Active Directory，請使用 `client.login('aad')`。
5. 執行專案。  當 hello 專案已完成初始化時，您的應用程式會顯示 hello 選擇驗證提供者的 hello OAuth 登入頁面。

## <a name="next-steps"></a>後續步驟
* 深入了解 Azure App Service [驗證相關資訊] 。
* 藉由新增繼續 hello 教學課程[推播通知]tooyour Apache Cordova 應用程式。

了解如何 toouse hello Sdk。

* [Apache Cordova SDK]
* [ASP.NET Server SDK]
* [Node.js Server SDK]

<!-- URLs. -->
[開始使用 Mobile Apps]: app-service-mobile-cordova-get-started.md
[Content-Security-Policy 文件]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[推播通知]: app-service-mobile-cordova-get-started-push.md
[驗證相關資訊]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
