---
title: "在 Azure App Service Mobile Apps 上建立 Android 應用程式 | Microsoft Docs"
description: "請遵循此教學課程，以開始使用 Azure 行動應用程式後端進行 Android 開發"
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
ms.openlocfilehash: 418a5229a084d570bc6cab5925dbd8d30945a3c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="794d1-103">建立 Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="794d1-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="794d1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="794d1-104">Overview</span></span>
<span data-ttu-id="794d1-105">本教學課程將示範如何使用 Azure 行動應用程式後端，將雲端式後端服務加入 Android 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="794d1-105">This tutorial shows you how to add a cloud-based backend service to an Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="794d1-106">您將建立新的行動應用程式後端，以及可在 Azure 中儲存應用程式資料的簡易「待辦事項清單」 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="794d1-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="794d1-107">對於在 Azure App Service 中使用 Mobile Apps 功能的所有其他 Android 教學課程，完成本教學課程是必要條件。</span><span class="sxs-lookup"><span data-stu-id="794d1-107">Completing this tutorial is a prerequisite for all other Android tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="794d1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="794d1-108">Prerequisites</span></span>
<span data-ttu-id="794d1-109">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="794d1-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="794d1-110">[Android Developer Tools](https://developer.android.com/sdk/index.html)，其中包括 Android Studio 整合式開發環境，以及最新的 Android 平台。</span><span class="sxs-lookup"><span data-stu-id="794d1-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>
* <span data-ttu-id="794d1-111">Azure Mobile Android SDK，會自動受到參考，包含在您下載的快速入門專案中。</span><span class="sxs-lookup"><span data-stu-id="794d1-111">Azure Mobile Android SDK, which is automatically referenced as part of the quickstart project you download.</span></span>
* <span data-ttu-id="794d1-112">有效的 [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="794d1-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="794d1-113">建立新的 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="794d1-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="794d1-114">設定伺服器專案</span><span class="sxs-lookup"><span data-stu-id="794d1-114">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-android-app"></a><span data-ttu-id="794d1-115">下載並執行 Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="794d1-115">Download and run the Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
