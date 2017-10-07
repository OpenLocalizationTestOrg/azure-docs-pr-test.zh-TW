---
title: "aaaCreate Cordova 應用程式在 Azure App Service 行動應用程式 |Microsoft 文件"
description: "請遵循此教學課程 tooget 開始使用 Apache Cordova 開發的 Azure 行動應用程式後端"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova, javascript, mobile, 用戶端"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>建立 Apache Cordova 應用程式
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 tooadd 雲端架構後端服務使用 Azure 行動應用程式後端的 tooan Apache Cordova 的行動裝置應用程式。  您會建立新的行動應用程式後端，以及可在 Azure 中儲存應用程式資料的簡易「待辦事項清單」 Apache Cordova 應用程式。

完成本教學課程是所有其他 Apache Cordova 的教學課程使用 Azure App Service 中的 hello 行動應用程式功能相關的必要條件。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要下列必要條件 hello:

* 具有 [Visual Studio Community 2017] 或更新版本的電腦。
* [Visual Studio Tools for Apache Cordova]。
* 有效的 [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。

您也可能會略過 Visual Studio，並直接使用 hello Apache Cordova 命令列。  當完成 hello 教學課程的 Mac 電腦上，使用 hello 命令列很有用。  本教學課程未涵蓋編譯 Apache Cordova 使用 hello 命令列的用戶端應用程式。

## <a name="create-an-azure-mobile-app-backend"></a>建立 Azure 行動應用程式後端
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[觀看示範類似步驟的影片](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>設定 hello 伺服器專案
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>下載並執行 hello Apache Cordova 應用程式
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>後續步驟
現在，您會完成此快速入門教學課程中，移動 tooone hello 遵循教學課程的上：

* [新增離線資料](app-service-mobile-cordova-get-started-offline-data.md)tooyour Apache Cordova 應用程式。
* [將驗證新增](app-service-mobile-cordova-get-started-users.md)tooyour Apache Cordova 應用程式。
* [加入推播通知](app-service-mobile-cordova-get-started-push.md)tooyour Apache Cordova 應用程式。

深入了解使用 Azure App Service 的相關重要概念。

* [離線資料]
* [驗證]
* [推播通知]

了解如何 toouse hello Sdk。

* [Apache Cordova SDK]
* [ASP.NET Server SDK]
* [Node.js Server SDK]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[離線資料]: app-service-mobile-offline-data-sync.md
[驗證]: app-service-mobile-auth.md
[推播通知]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
