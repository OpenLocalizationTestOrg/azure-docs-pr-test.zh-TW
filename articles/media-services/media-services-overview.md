---
title: "aaaAzure Media Services 概觀 |Microsoft 文件"
description: "本主題提供 Azure 媒體服務的概觀"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="229d5-103">Azure 媒體服務概觀</span><span class="sxs-lookup"><span data-stu-id="229d5-103">Azure Media Services overview</span></span> 

<span data-ttu-id="229d5-104">Microsoft Azure Media Services 是可擴充雲端為基礎的平台，可讓開發人員 toobuild 可擴充媒體管理和傳遞應用程式。</span><span class="sxs-lookup"><span data-stu-id="229d5-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="229d5-105">Media Services 為基礎的 REST Api 可讓您 toosecurely 上傳、 儲存、 編碼，和封裝視訊或音訊內容的隨選及即時串流傳遞 toovarious 用戶端 （例如，電視、 PC 和行動裝置）。</span><span class="sxs-lookup"><span data-stu-id="229d5-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="229d5-106">您可以建置完全採用媒體服務的端對端工作流程。</span><span class="sxs-lookup"><span data-stu-id="229d5-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="229d5-107">您也可以選擇 toouse 協力廠商元件工作流程的某些部分。</span><span class="sxs-lookup"><span data-stu-id="229d5-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="229d5-108">例如，使用第三方編碼器來進行編碼；</span><span class="sxs-lookup"><span data-stu-id="229d5-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="229d5-109">然後使用媒體服務上傳、保護、封裝、傳遞。</span><span class="sxs-lookup"><span data-stu-id="229d5-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="229d5-110">您可以選擇 toostream 即時內容，或提供點播內容。</span><span class="sxs-lookup"><span data-stu-id="229d5-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="229d5-111">hello 主題也會連結 tooother 相關主題。</span><span class="sxs-lookup"><span data-stu-id="229d5-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="229d5-112">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="229d5-112">Media Services learning paths</span></span>
<span data-ttu-id="229d5-113">您可以在此檢視 AMS 學習路徑：</span><span class="sxs-lookup"><span data-stu-id="229d5-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="229d5-114">AMS 即時資料流工作流程</span><span class="sxs-lookup"><span data-stu-id="229d5-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="229d5-115">AMS 隨選串流工作流程</span><span class="sxs-lookup"><span data-stu-id="229d5-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="229d5-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="229d5-116">Prerequisites</span></span>

<span data-ttu-id="229d5-117">toostart 使用 Azure Media Services 中，您應該有下列 hello:</span><span class="sxs-lookup"><span data-stu-id="229d5-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="229d5-118">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="229d5-118">An Azure account.</span></span> <span data-ttu-id="229d5-119">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="229d5-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="229d5-120">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="229d5-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="229d5-121">Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="229d5-121">An Azure Media Services account.</span></span> <span data-ttu-id="229d5-122">如需詳細資訊，請參閱[建立帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="229d5-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="229d5-123">(選擇性) 設定開發環境。</span><span class="sxs-lookup"><span data-stu-id="229d5-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="229d5-124">針對開發環境選擇 .NET 或 REST API。</span><span class="sxs-lookup"><span data-stu-id="229d5-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="229d5-125">如需詳細資訊，請參閱 [設定環境](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="229d5-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="229d5-126">此外，了解如何太[以程式設計方式連接 tooAMS API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="229d5-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="229d5-127">已啟動狀態的標準或進階串流端點。</span><span class="sxs-lookup"><span data-stu-id="229d5-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="229d5-128">如需詳細資訊，請參閱[管理串流端點](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="229d5-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="229d5-129">SDK 及工具</span><span class="sxs-lookup"><span data-stu-id="229d5-129">SDKs and tools</span></span>

<span data-ttu-id="229d5-130">toobuild Media Services 解決方案，您可以使用：</span><span class="sxs-lookup"><span data-stu-id="229d5-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="229d5-131">媒體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="229d5-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="229d5-132">其中一個 hello 可用的用戶端 Sdk:</span><span class="sxs-lookup"><span data-stu-id="229d5-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="229d5-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services)、</span><span class="sxs-lookup"><span data-stu-id="229d5-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="229d5-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java)、</span><span class="sxs-lookup"><span data-stu-id="229d5-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="229d5-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)、</span><span class="sxs-lookup"><span data-stu-id="229d5-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="229d5-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (這是非 Microsoft 版本的 Node.js SDK。</span><span class="sxs-lookup"><span data-stu-id="229d5-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="229d5-137">它由社群維護並目前並沒有 100%的涵蓋範圍 hello AMS 應用程式開發介面）。</span><span class="sxs-lookup"><span data-stu-id="229d5-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="229d5-138">現有的工具：</span><span class="sxs-lookup"><span data-stu-id="229d5-138">Existing tools:</span></span>
    * [<span data-ttu-id="229d5-139">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="229d5-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="229d5-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure 媒體服務總管 (AMSE) 是適用於 Windows 的 Winforms/C# 應用程式)</span><span class="sxs-lookup"><span data-stu-id="229d5-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="229d5-141">概念和概觀</span><span class="sxs-lookup"><span data-stu-id="229d5-141">Concepts and overview</span></span>
<span data-ttu-id="229d5-142">如需 Azure 媒體服務概念，請參閱 [概念](media-services-concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="229d5-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="229d5-143">如何為 tooseries 介紹 Azure Media services tooall hello 主要元件，請參閱[Azure 媒體服務的逐步教學課程](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series)。</span><span class="sxs-lookup"><span data-stu-id="229d5-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="229d5-144">此序列有很棒的概念概觀，並使用 hello AMSE 工具 toodemonstrate AMS 工作。</span><span class="sxs-lookup"><span data-stu-id="229d5-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="229d5-145">AMSE 工具是一種 Windows 工具。</span><span class="sxs-lookup"><span data-stu-id="229d5-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="229d5-146">這項工具支援大部分的 hello 工作，可讓您以程式設計的方式與[AMS SDK for.NET](https://github.com/Azure/azure-sdk-for-media-services)， [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java)，或[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)。</span><span class="sxs-lookup"><span data-stu-id="229d5-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="229d5-147">跨資料中心支援的媒體服務情節和可用性</span><span class="sxs-lookup"><span data-stu-id="229d5-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="229d5-148">如需詳細資訊，請參閱[跨資料中心的 AMS 功能和服務情節和可用性](scenarios-and-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="229d5-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="229d5-149">服務等級協定 (SLA)</span><span class="sxs-lookup"><span data-stu-id="229d5-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="229d5-150">對於媒體服務編碼，我們保證 REST API 交易可用性高達 99.9%。</span><span class="sxs-lookup"><span data-stu-id="229d5-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="229d5-151">對於串流，我們在購買一個標準或近界串流端點時，針對現有的媒體內容，可保證以 99.9% 的可用性成功服務要求。</span><span class="sxs-lookup"><span data-stu-id="229d5-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="229d5-152">即時通道，我們保證，執行通道將會具有外部連線能力至少 99.9%的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="229d5-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="229d5-153">內容保護，我們保證，我們將會成功地滿足金鑰要求至少 99.9%的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="229d5-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="229d5-154">索引子，我們將會成功服務索引子工作要求處理編碼保留單元 99.9%的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="229d5-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="229d5-155">如需詳細資訊，請參閱 [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="229d5-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="229d5-156">如需在資料中心內的可用性資訊，請參閱 hello [Avaiability](scenarios-and-availability.md#availability) > 一節。</span><span class="sxs-lookup"><span data-stu-id="229d5-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="229d5-157">支援</span><span class="sxs-lookup"><span data-stu-id="229d5-157">Support</span></span>

<span data-ttu-id="229d5-158">[Azure 支援](https://azure.microsoft.com/support/options/) 提供 Azure 的支援選項，包括媒體服務。</span><span class="sxs-lookup"><span data-stu-id="229d5-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="229d5-159">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="229d5-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
