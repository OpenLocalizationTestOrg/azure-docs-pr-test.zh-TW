---
title: "aaaCreate iOS 應用程式在 Azure App Service 行動應用程式 |Microsoft 文件"
description: "請遵循此教學課程 tooget 開始使用適用於 iOS 開發 Swift Objective C 中的 Azure 行動應用程式後端"
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 869fa971f7b5ab4a7119bbfa92808185d2ecdf8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="778d7-103">建立 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="778d7-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="778d7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="778d7-104">Overview</span></span>
<span data-ttu-id="778d7-105">本教學課程示範如何 tooadd [Azure 行動應用程式](app-service-mobile-value-prop.md)，雲端後端服務、 tooan iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="778d7-105">This tutorial shows how tooadd [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, tooan iOS app.</span></span> <span data-ttu-id="778d7-106">首先我們會建立新的行動後端。</span><span class="sxs-lookup"><span data-stu-id="778d7-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="778d7-107">然後，我們會使用簡單*Todo 清單*Azure 中的 iOS 應用程式 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="778d7-107">Then, we'll use a simple *Todo list* iOS app toostore data in Azure.</span></span>

<span data-ttu-id="778d7-108">toocomplete 本教學課程中，您需要 Mac 和[Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="778d7-108">toocomplete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="778d7-109">步驟 I：建立新的 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="778d7-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-hello-backend-project"></a><span data-ttu-id="778d7-110">步驟二： 設定 hello 後端專案</span><span class="sxs-lookup"><span data-stu-id="778d7-110">Step II: Configure hello backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-hello-ios-app"></a><span data-ttu-id="778d7-111">步驟三： 下載並執行 hello iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="778d7-111">Step III: Download and run hello iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
