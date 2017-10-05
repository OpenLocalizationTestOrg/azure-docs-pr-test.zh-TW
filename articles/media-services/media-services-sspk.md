---
title: "Licensing Microsoft® Smooth Streaming Client Porting Kit"
description: "了解如何授權 Microsoft® Smooth Streaming Client Porting Kit。"
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: b5a36ac6771bef220afe29446cd56c1b65a498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="ef3e3-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="ef3e3-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="ef3e3-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ef3e3-104">Overview</span></span>
<span data-ttu-id="ef3e3-105">Microsoft Smooth Streaming Client Porting Kit (簡稱**SSPK** ) 是最佳化的 Smooth Streaming 用戶端實作，可協助內嵌裝置製造商、有線電視和行動業者、內容服務提供者、手持式裝置製造商、獨立軟體廠商 (ISV) 和解決方案提供者打造產品和服務，以供串流 Smooth Streaming 格式的彈性資料流內容。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="ef3e3-106">SSPK 是 Smooth Streaming 用戶端的裝置和平台獨立實作，可由被授權者移植到任何裝置和平台。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="ef3e3-107">以下是一個高層級架構，而 IIS Smooth Streaming Porting Kit 方塊是 Microsoft 所提供的 Smooth Streaming 用戶端實作並包含播放 Smooth Streaming 內容的所有核心邏輯。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="ef3e3-108">然而，特定裝置或平台的合作夥伴可藉由實作適當的介面來移植該架構。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="ef3e3-110">說明</span><span class="sxs-lookup"><span data-stu-id="ef3e3-110">Description</span></span>
<span data-ttu-id="ef3e3-111">SSPK 是根據可提供絕佳商業價值的條款授權。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="ef3e3-112">SSPK 授權提供給業界：</span><span class="sxs-lookup"><span data-stu-id="ef3e3-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="ef3e3-113">Smooth Streaming Porting Kit 的 C++ 原始碼</span><span class="sxs-lookup"><span data-stu-id="ef3e3-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="ef3e3-114">實作 Smooth Streaming 用戶端功能</span><span class="sxs-lookup"><span data-stu-id="ef3e3-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="ef3e3-115">新增格式剖析、啟發學習法、緩衝處理邏輯等等</span><span class="sxs-lookup"><span data-stu-id="ef3e3-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="ef3e3-116">播放器應用程式 API</span><span class="sxs-lookup"><span data-stu-id="ef3e3-116">Player application APIs</span></span> 
  * <span data-ttu-id="ef3e3-117">可與媒體播放器應用程式互動的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="ef3e3-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="ef3e3-118">平台抽象層 (PAL) 介面</span><span class="sxs-lookup"><span data-stu-id="ef3e3-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="ef3e3-119">用於與作業系統 (執行緒、通訊端) 互動的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="ef3e3-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="ef3e3-120">硬體抽象層 (HAL) 介面</span><span class="sxs-lookup"><span data-stu-id="ef3e3-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="ef3e3-121">用於與硬體 A/V 解碼器 (解碼、轉譯) 互動的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="ef3e3-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="ef3e3-122">數位版權管理 (DRM) 介面</span><span class="sxs-lookup"><span data-stu-id="ef3e3-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="ef3e3-123">可透過 DRM 抽象層 (DAL) 處理 DRM 的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="ef3e3-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="ef3e3-124">Microsoft PlayReady Porting Kit 個別出貨，但可透過這個介面整合。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="ef3e3-125">如需 Microsoft PlayReady Device 授權的詳細資訊，請按一下 [這裡](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl)。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="ef3e3-126">實作範例</span><span class="sxs-lookup"><span data-stu-id="ef3e3-126">Implementation samples</span></span> 
  * <span data-ttu-id="ef3e3-127">適用於 Linux 的 PAL 實作範例</span><span class="sxs-lookup"><span data-stu-id="ef3e3-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="ef3e3-128">適用於 GStreamer 的 HAL 實作範例</span><span class="sxs-lookup"><span data-stu-id="ef3e3-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="ef3e3-129">授權選項</span><span class="sxs-lookup"><span data-stu-id="ef3e3-129">Licensing Options</span></span>
<span data-ttu-id="ef3e3-130">Microsoft Smooth Streaming Client Porting Kit 乃根據兩份不同的授權合約提供給被授權者：一份適用於開發 Smooth Streaming 用戶端中期產品，另一份適用於將 Smooth Streaming 用戶端最終產品散發給使用者。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="ef3e3-131">對於需要原始程式碼移植套件來開發中期產品的晶片組製造商、系統整合業者或獨立軟體廠商 (ISV)，應該執行 Microsoft Smooth Streaming Client Porting Kit **中期產品授權** 。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="ef3e3-132">對於需要對使用者散發 Smooth Streaming 用戶端最終產品之權利的裝置製造商或 ISV，應該執行 Microsoft Smooth Streaming Client Porting Kit **最終產品授權** 。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="ef3e3-133">Microsoft Smooth Streaming Client Porting Kit 中期產品授權</span><span class="sxs-lookup"><span data-stu-id="ef3e3-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="ef3e3-134">Microsoft 依據本授權提供 Smooth Streaming Client Porting Kit 和必要的智慧財產權，以便開發 Smooth Streaming 用戶端中期產品並散發給其他可散發 Smooth Streaming 用戶端最終產品的 Smooth Streaming Client Porting Kit 裝置被授權者。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="ef3e3-135">免費結構</span><span class="sxs-lookup"><span data-stu-id="ef3e3-135">Fee structure</span></span>
<span data-ttu-id="ef3e3-136">$50,000 美元的一次性授權費可供存取 Smooth Streaming Client Porting Kit。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="ef3e3-137">Microsoft Smooth Streaming Client Porting Kit 最終產品授權</span><span class="sxs-lookup"><span data-stu-id="ef3e3-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="ef3e3-138">Microsoft 依據本授權提供所有必要的智慧財產權，以便從其他 Smooth Streaming Client Porting Kit 被授權者接收 Smooth Streaming 用戶端中期產品，並將公司自有品牌的 Smooth Streaming 用戶端最終產品散發給一般使用者。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="ef3e3-139">免費結構</span><span class="sxs-lookup"><span data-stu-id="ef3e3-139">Fee structure</span></span>
<span data-ttu-id="ef3e3-140">Smooth Streaming 用戶端最終產品乃根據權利金模型提供，細節如下：</span><span class="sxs-lookup"><span data-stu-id="ef3e3-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="ef3e3-141">送交的每一裝置實作為 $0.10 美元</span><span class="sxs-lookup"><span data-stu-id="ef3e3-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="ef3e3-142">每年的權利金上限為 $50,000 美元</span><span class="sxs-lookup"><span data-stu-id="ef3e3-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="ef3e3-143">每年前 10,000 個裝置實作不需權利金</span><span class="sxs-lookup"><span data-stu-id="ef3e3-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="ef3e3-144">授權程序和 SSPK 存取</span><span class="sxs-lookup"><span data-stu-id="ef3e3-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="ef3e3-145">有關所有授權查詢，請寄送電子郵件至 [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) 。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="ef3e3-146">已註冊的中期被授權者可以存取 [SSPK 發佈入口網站](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) 。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="ef3e3-147">中期和最終 SSPK 被授權者都可以將技術問題提交到 [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ef3e3-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="ef3e3-148">Microsoft Smooth Streaming 用戶端中期產品合約被授權者</span><span class="sxs-lookup"><span data-stu-id="ef3e3-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="ef3e3-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="ef3e3-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="ef3e3-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="ef3e3-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="ef3e3-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="ef3e3-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="ef3e3-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-153">Alticast Corporation</span></span>
* <span data-ttu-id="ef3e3-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="ef3e3-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="ef3e3-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-157">Cavium, Inc.</span></span>
* <span data-ttu-id="ef3e3-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="ef3e3-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-159">Enseo, Inc.</span></span>
* <span data-ttu-id="ef3e3-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-160">Fluendo S.A.</span></span>
* <span data-ttu-id="ef3e3-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="ef3e3-162">Infomir GMBH</span></span>
* <span data-ttu-id="ef3e3-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="ef3e3-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="ef3e3-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="ef3e3-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="ef3e3-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-166">MediaTek Inc.</span></span>
* <span data-ttu-id="ef3e3-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="ef3e3-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="ef3e3-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="ef3e3-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="ef3e3-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="ef3e3-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="ef3e3-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="ef3e3-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="ef3e3-172">SoftAtHome</span></span>
* <span data-ttu-id="ef3e3-173">索尼公司</span><span class="sxs-lookup"><span data-stu-id="ef3e3-173">Sony Corporation</span></span>
* <span data-ttu-id="ef3e3-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="ef3e3-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="ef3e3-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="ef3e3-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="ef3e3-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="ef3e3-180">Microsoft Smooth Streaming 用戶端最終產品合約被授權者</span><span class="sxs-lookup"><span data-stu-id="ef3e3-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="ef3e3-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="ef3e3-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="ef3e3-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="ef3e3-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="ef3e3-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="ef3e3-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="ef3e3-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="ef3e3-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="ef3e3-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-189">VE TİC.</span></span> <span data-ttu-id="ef3e3-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="ef3e3-190">A.Ş</span></span>
* <span data-ttu-id="ef3e3-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="ef3e3-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="ef3e3-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="ef3e3-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="ef3e3-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="ef3e3-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="ef3e3-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="ef3e3-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-196">Enseo, Inc.</span></span>
* <span data-ttu-id="ef3e3-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="ef3e3-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="ef3e3-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-198">Fluendo S.A.</span></span>
* <span data-ttu-id="ef3e3-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="ef3e3-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="ef3e3-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="ef3e3-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="ef3e3-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="ef3e3-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="ef3e3-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="ef3e3-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="ef3e3-205">Infomir GMBH</span></span>
* <span data-ttu-id="ef3e3-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-207">KDDI Corporation</span></span>
* <span data-ttu-id="ef3e3-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="ef3e3-209">Orange SA</span></span>
* <span data-ttu-id="ef3e3-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="ef3e3-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="ef3e3-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="ef3e3-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="ef3e3-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="ef3e3-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="ef3e3-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="ef3e3-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="ef3e3-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="ef3e3-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="ef3e3-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="ef3e3-216">致振企業股份有限公司</span><span class="sxs-lookup"><span data-stu-id="ef3e3-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="ef3e3-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="ef3e3-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="ef3e3-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="ef3e3-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="ef3e3-219">SoftAtHome</span></span>
* <span data-ttu-id="ef3e3-220">索尼公司</span><span class="sxs-lookup"><span data-stu-id="ef3e3-220">Sony Corporation</span></span>
* <span data-ttu-id="ef3e3-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="ef3e3-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="ef3e3-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="ef3e3-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="ef3e3-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="ef3e3-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="ef3e3-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="ef3e3-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="ef3e3-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="ef3e3-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="ef3e3-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-228">Wistron Corporation</span></span>
* <span data-ttu-id="ef3e3-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="ef3e3-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="ef3e3-230">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="ef3e3-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ef3e3-231">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ef3e3-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

