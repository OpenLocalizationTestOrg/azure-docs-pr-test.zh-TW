---
title: "aaaCreate Azure App Service 行動應用程式上的 Android 應用程式 |Microsoft 文件"
description: "請遵循此教學課程 tooget 開始使用 Azure 行動應用程式後端進行 Android 開發"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a>建立 Android 應用程式
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 tooadd 雲端架構後端服務使用 Azure 行動應用程式後端的 tooan Android 行動應用程式。  您將建立新的行動應用程式後端，以及可在 Azure 中儲存應用程式資料的簡易「待辦事項清單」 Android 應用程式。

完成本教學課程是所有其他 Android 教學課程使用 Azure App Service 中的 hello 行動應用程式功能相關的必要條件。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要遵循的 hello:

* [Android 開發人員工具](https://developer.android.com/sdk/index.html)，包括 hello Android Studio 整合式的開發環境，以及 hello 最新版的 Android 平台。
* Azure Mobile Android SDK，會自動為您所下載的 hello 快速入門專案的一部分參考。
* 有效的 [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="create-a-new-azure-mobile-app-backend"></a>建立新的 Azure 行動應用程式後端
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>設定 hello 伺服器專案
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a>下載並執行 hello Android 應用程式
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
