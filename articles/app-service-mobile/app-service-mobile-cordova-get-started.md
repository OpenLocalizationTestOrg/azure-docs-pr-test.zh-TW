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
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="c85ec-104">建立 Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="c85ec-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c85ec-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c85ec-105">Overview</span></span>
<span data-ttu-id="c85ec-106">本教學課程會示範如何 tooadd 雲端架構後端服務使用 Azure 行動應用程式後端的 tooan Apache Cordova 的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="c85ec-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="c85ec-107">您會建立新的行動應用程式後端，以及可在 Azure 中儲存應用程式資料的簡易「待辦事項清單」 Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c85ec-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="c85ec-108">完成本教學課程是所有其他 Apache Cordova 的教學課程使用 Azure App Service 中的 hello 行動應用程式功能相關的必要條件。</span><span class="sxs-lookup"><span data-stu-id="c85ec-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c85ec-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="c85ec-109">Prerequisites</span></span>
<span data-ttu-id="c85ec-110">toocomplete 本教學課程中，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="c85ec-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="c85ec-111">具有 [Visual Studio Community 2017] 或更新版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="c85ec-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="c85ec-112">[Visual Studio Tools for Apache Cordova]。</span><span class="sxs-lookup"><span data-stu-id="c85ec-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="c85ec-113">有效的 [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="c85ec-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="c85ec-114">您也可能會略過 Visual Studio，並直接使用 hello Apache Cordova 命令列。</span><span class="sxs-lookup"><span data-stu-id="c85ec-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="c85ec-115">當完成 hello 教學課程的 Mac 電腦上，使用 hello 命令列很有用。</span><span class="sxs-lookup"><span data-stu-id="c85ec-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="c85ec-116">本教學課程未涵蓋編譯 Apache Cordova 使用 hello 命令列的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="c85ec-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="c85ec-117">建立 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="c85ec-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="c85ec-118">觀看示範類似步驟的影片</span><span class="sxs-lookup"><span data-stu-id="c85ec-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="c85ec-119">設定 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="c85ec-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="c85ec-120">下載並執行 hello Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="c85ec-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="c85ec-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c85ec-121">Next Steps</span></span>
<span data-ttu-id="c85ec-122">現在，您會完成此快速入門教學課程中，移動 tooone hello 遵循教學課程的上：</span><span class="sxs-lookup"><span data-stu-id="c85ec-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="c85ec-123">[新增離線資料](app-service-mobile-cordova-get-started-offline-data.md)tooyour Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c85ec-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="c85ec-124">[將驗證新增](app-service-mobile-cordova-get-started-users.md)tooyour Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c85ec-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="c85ec-125">[加入推播通知](app-service-mobile-cordova-get-started-push.md)tooyour Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c85ec-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="c85ec-126">深入了解使用 Azure App Service 的相關重要概念。</span><span class="sxs-lookup"><span data-stu-id="c85ec-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="c85ec-127">[離線資料]</span><span class="sxs-lookup"><span data-stu-id="c85ec-127">[Offline Data]</span></span>
* <span data-ttu-id="c85ec-128">[驗證]</span><span class="sxs-lookup"><span data-stu-id="c85ec-128">[Authentication]</span></span>
* <span data-ttu-id="c85ec-129">[推播通知]</span><span class="sxs-lookup"><span data-stu-id="c85ec-129">[Push Notifications]</span></span>

<span data-ttu-id="c85ec-130">了解如何 toouse hello Sdk。</span><span class="sxs-lookup"><span data-stu-id="c85ec-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="c85ec-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="c85ec-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="c85ec-132">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="c85ec-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="c85ec-133">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="c85ec-133">[Node.js Server SDK]</span></span>

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
