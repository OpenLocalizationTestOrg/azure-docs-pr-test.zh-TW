---
title: "將安全性整合至 Azure 架構設計 | Microsoft Docs"
description: " 本文將協助您了解 Azure 上的應用程式及服務架構，可以更輕易地將安全性整合至設計及實作。 "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 91e46d690d3e7c298bc3b4020cc383ca99c43c4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="521a9-103">Azure 的應用程式架構</span><span class="sxs-lookup"><span data-stu-id="521a9-103">Application architecture on Azure</span></span>
<span data-ttu-id="521a9-104">為了協助保護您在 Microsoft Azure 上以雲端為基礎的解決方案，堅強的架構基礎相當重要。</span><span class="sxs-lookup"><span data-stu-id="521a9-104">To help secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="521a9-105">架構設計人員、設計人員和實作者都受益於對於應用程式及服務架構的強大知識。</span><span class="sxs-lookup"><span data-stu-id="521a9-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="521a9-106">此基本知識將幫助您了解所有以雲端為基礎的解決方案的元件，並輕鬆地將安全性整合至您的設計和實作的所有層面。</span><span class="sxs-lookup"><span data-stu-id="521a9-106">This foundational knowledge helps you understand all the components of your cloud-based solutions and make it easier to integrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="521a9-107">我們有下列項目可以協助您的架構調查與設計︰</span><span class="sxs-lookup"><span data-stu-id="521a9-107">We have the following to help you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="521a9-108">架構資訊圖</span><span class="sxs-lookup"><span data-stu-id="521a9-108">Architectural infographics</span></span>
* <span data-ttu-id="521a9-109">架構藍圖</span><span class="sxs-lookup"><span data-stu-id="521a9-109">Architectural blueprints</span></span>
* <span data-ttu-id="521a9-110">雲端和企業符號集</span><span class="sxs-lookup"><span data-stu-id="521a9-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="521a9-111">3D 藍圖 Visio 範本</span><span class="sxs-lookup"><span data-stu-id="521a9-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="521a9-112">架構資訊圖</span><span class="sxs-lookup"><span data-stu-id="521a9-112">Architectural infographics</span></span>
<span data-ttu-id="521a9-113">Microsoft 發佈數個與架構相關的海報/資訊圖。</span><span class="sxs-lookup"><span data-stu-id="521a9-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="521a9-114">這些包括：</span><span class="sxs-lookup"><span data-stu-id="521a9-114">They include:</span></span>

* [<span data-ttu-id="521a9-115">建置真實世界的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="521a9-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="521a9-116">調整雲端服務</span><span class="sxs-lookup"><span data-stu-id="521a9-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="521a9-117">架構藍圖</span><span class="sxs-lookup"><span data-stu-id="521a9-117">Architectural blueprints</span></span>
<span data-ttu-id="521a9-118">Microsoft 發佈一組高階 [架構藍圖](http://aka.ms/azblueprints) ，示範如何使用 Microsoft 產品來建置特定類型的系統。</span><span class="sxs-lookup"><span data-stu-id="521a9-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how to build specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="521a9-119">每個藍圖都包含：</span><span class="sxs-lookup"><span data-stu-id="521a9-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="521a9-120">一般以 2D Visio 2003 為基礎的檔案，您可以下載並修改</span><span class="sxs-lookup"><span data-stu-id="521a9-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="521a9-121">彩色的 3D 透視 PDF 檔案，為技術較低的對象介紹藍圖</span><span class="sxs-lookup"><span data-stu-id="521a9-121">Colorful 3D perspective PDF file to introduce the blueprint to less technical audiences</span></span>
* <span data-ttu-id="521a9-122">逐步解說 3D 版本的影片</span><span class="sxs-lookup"><span data-stu-id="521a9-122">Video that walks through the 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="521a9-123">雲端和企業符號集</span><span class="sxs-lookup"><span data-stu-id="521a9-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="521a9-124">[檢視 Visio 和符號訓練影片](http://aka.ms/CnESymbolsVideo)，然後[下載雲端和企業符號集](http://aka.ms/CnESymbols)以協助建立可說明 Azure、Windows Server、SQL Server 和其他產品的技術資料。</span><span class="sxs-lookup"><span data-stu-id="521a9-124">[View the Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download the Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) to help create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="521a9-125">您可以將符號用在架構圖表、訓練教材、簡報、資料工作表、資訊圖、白皮書，甚至是協力廠商書籍 (如果書籍訓練人員使用 Microsoft 產品)。</span><span class="sxs-lookup"><span data-stu-id="521a9-125">You can use the symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if the book trains people to use Microsoft products.</span></span> <span data-ttu-id="521a9-126">不過，它們不一定用於使用者介面。</span><span class="sxs-lookup"><span data-stu-id="521a9-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="521a9-127">3D 藍圖 Visio 範本</span><span class="sxs-lookup"><span data-stu-id="521a9-127">3D blueprint Visio template</span></span>
<span data-ttu-id="521a9-128">3D 版的 [Microsoft 架構藍圖](http://aka.ms/azblueprints) 一開始建立在非 Microsoft 工具中。</span><span class="sxs-lookup"><span data-stu-id="521a9-128">The 3D versions of the [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="521a9-129">新的 Visio 2013 (和更新版本) 範本於 2015 年 8 月 5 日推出，做為 [分佈在 EDX.ORG 上之 Microsoft 架構憑證課程](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course)的一部分。</span><span class="sxs-lookup"><span data-stu-id="521a9-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="521a9-130">此範本在課程外也可供使用。</span><span class="sxs-lookup"><span data-stu-id="521a9-130">The template is also available outside the course.</span></span>

* <span data-ttu-id="521a9-131">[檢視訓練影片](http://aka.ms/3dBlueprintTemplateVideo) ，讓您知道它的功能</span><span class="sxs-lookup"><span data-stu-id="521a9-131">[View the training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="521a9-132">下載 [Microsoft 3D 藍圖 Visio 範本](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="521a9-132">Download the [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="521a9-133">下載 [雲端和企業符號](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) 以搭配 3D 範本使用</span><span class="sxs-lookup"><span data-stu-id="521a9-133">Download the [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) to use with the 3D template</span></span>
