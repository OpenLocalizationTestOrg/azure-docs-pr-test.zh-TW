---
title: "Azure 的架構設計成 aaaIntegrate 安全性 |Microsoft 文件"
description: " 本文將協助您了解 hello Azure toomake 上的應用程式及服務架構它更容易 toointegrate 安全性設計及實作。 "
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
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="07ed6-103">Azure 的應用程式架構</span><span class="sxs-lookup"><span data-stu-id="07ed6-103">Application architecture on Azure</span></span>
<span data-ttu-id="07ed6-104">toohelp 安全上 Microsoft Azure 雲端方案架構穩固相當重要。</span><span class="sxs-lookup"><span data-stu-id="07ed6-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="07ed6-105">架構設計人員、設計人員和實作者都受益於對於應用程式及服務架構的強大知識。</span><span class="sxs-lookup"><span data-stu-id="07ed6-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="07ed6-106">這項基本知識可協助您了解雲端方案的所有 hello 元件，並使其更容易 toointegrate 安全性，您設計和實作的所有層面。</span><span class="sxs-lookup"><span data-stu-id="07ed6-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="07ed6-107">我們有 hello 下列 toohelp 您架構的調查與設計：</span><span class="sxs-lookup"><span data-stu-id="07ed6-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="07ed6-108">架構資訊圖</span><span class="sxs-lookup"><span data-stu-id="07ed6-108">Architectural infographics</span></span>
* <span data-ttu-id="07ed6-109">架構藍圖</span><span class="sxs-lookup"><span data-stu-id="07ed6-109">Architectural blueprints</span></span>
* <span data-ttu-id="07ed6-110">雲端和企業符號集</span><span class="sxs-lookup"><span data-stu-id="07ed6-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="07ed6-111">3D 藍圖 Visio 範本</span><span class="sxs-lookup"><span data-stu-id="07ed6-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="07ed6-112">架構資訊圖</span><span class="sxs-lookup"><span data-stu-id="07ed6-112">Architectural infographics</span></span>
<span data-ttu-id="07ed6-113">Microsoft 發佈數個與架構相關的海報/資訊圖。</span><span class="sxs-lookup"><span data-stu-id="07ed6-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="07ed6-114">這些包括：</span><span class="sxs-lookup"><span data-stu-id="07ed6-114">They include:</span></span>

* [<span data-ttu-id="07ed6-115">建置真實世界的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="07ed6-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="07ed6-116">調整雲端服務</span><span class="sxs-lookup"><span data-stu-id="07ed6-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="07ed6-117">架構藍圖</span><span class="sxs-lookup"><span data-stu-id="07ed6-117">Architectural blueprints</span></span>
<span data-ttu-id="07ed6-118">Microsoft 發行的高層級的一組[架構藍圖](http://aka.ms/azblueprints)顯示如何使用 Microsoft 產品的系統 toobuild 特定類型。</span><span class="sxs-lookup"><span data-stu-id="07ed6-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="07ed6-119">每個藍圖都包含：</span><span class="sxs-lookup"><span data-stu-id="07ed6-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="07ed6-120">一般以 2D Visio 2003 為基礎的檔案，您可以下載並修改</span><span class="sxs-lookup"><span data-stu-id="07ed6-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="07ed6-121">彩色的 3D 遠近 PDF 檔案 toointroduce hello 藍圖 tooless 技術對象</span><span class="sxs-lookup"><span data-stu-id="07ed6-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="07ed6-122">逐步解說 hello 3D 版本的視訊</span><span class="sxs-lookup"><span data-stu-id="07ed6-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="07ed6-123">雲端和企業符號集</span><span class="sxs-lookup"><span data-stu-id="07ed6-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="07ed6-124">[檢視 hello Visio 和訓練影片符號](http://aka.ms/CnESymbolsVideo)然後[下載 hello 雲端和企業符號組](http://aka.ms/CnESymbols)toohelp 建立說明 Azure、 Windows Server、 SQL Server 和更多的技術資料。</span><span class="sxs-lookup"><span data-stu-id="07ed6-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="07ed6-125">如果 hello 書籍訓練人員 toouse Microsoft 產品，您可以使用的架構圖表、 訓練教材、 簡報、 資料工作表、 圖形、 技術白皮書和甚至協力廠商叢書 》 中的 hello 符號。</span><span class="sxs-lookup"><span data-stu-id="07ed6-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="07ed6-126">不過，它們不一定用於使用者介面。</span><span class="sxs-lookup"><span data-stu-id="07ed6-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="07ed6-127">3D 藍圖 Visio 範本</span><span class="sxs-lookup"><span data-stu-id="07ed6-127">3D blueprint Visio template</span></span>
<span data-ttu-id="07ed6-128">hello 3D 新版 hello [Microsoft 架構藍圖](http://aka.ms/azblueprints)一開始所建立的非 Microsoft 工具。</span><span class="sxs-lookup"><span data-stu-id="07ed6-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="07ed6-129">新的 Visio 2013 (和更新版本) 範本於 2015 年 8 月 5 日推出，做為 [分佈在 EDX.ORG 上之 Microsoft 架構憑證課程](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course)的一部分。</span><span class="sxs-lookup"><span data-stu-id="07ed6-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="07ed6-130">hello 範本也會提供外部 hello 課程的。</span><span class="sxs-lookup"><span data-stu-id="07ed6-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="07ed6-131">[檢視 hello 訓練影片](http://aka.ms/3dBlueprintTemplateVideo)第一個讓您知道它可以執行的動作</span><span class="sxs-lookup"><span data-stu-id="07ed6-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="07ed6-132">下載 hello [Microsoft 3d 藍圖 Visio 範本](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="07ed6-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="07ed6-133">下載 hello[雲端和企業符號](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets)toouse hello 3D 範本</span><span class="sxs-lookup"><span data-stu-id="07ed6-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
