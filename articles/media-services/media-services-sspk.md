---
title: "Microsoft® Smooth Streaming Client Porting Kit aaaLicensing"
description: "深入了解如何 toolicensing hello Microsoft® Smooth Streaming Client Porting Kit。"
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
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="878ba-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="878ba-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="878ba-104">概觀</span><span class="sxs-lookup"><span data-stu-id="878ba-104">Overview</span></span>
<span data-ttu-id="878ba-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK**縮寫) 是最佳化的 toohelp 內嵌裝置製造商、 纜線和行動業者、 內容服務提供者、 手持式 Smooth Streaming 用戶端實作製造商、 獨立軟體廠商 (Isv) 和方案提供者 toocreate 產品和服務的串流 Smooth Streaming 格式的彈性串流內容。</span><span class="sxs-lookup"><span data-stu-id="878ba-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="878ba-106">SSPK 是 Smooth Streaming 的用戶端 hello 願 tooany 裝置的平台都可移植的裝置和平台獨立實作。</span><span class="sxs-lookup"><span data-stu-id="878ba-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="878ba-107">包含在下面是高層級架構和 IIS Smooth Streaming Porting Kit 方塊是由 Microsoft 提供的 hello Smooth Streaming 的用戶端實作，並包含 Smooth Streaming 內容的播放的所有 hello 核心邏輯。</span><span class="sxs-lookup"><span data-stu-id="878ba-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="878ba-108">然而，特定裝置或平台的合作夥伴可藉由實作適當的介面來移植該架構。</span><span class="sxs-lookup"><span data-stu-id="878ba-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="878ba-110">說明</span><span class="sxs-lookup"><span data-stu-id="878ba-110">Description</span></span>
<span data-ttu-id="878ba-111">SSPK 是根據可提供絕佳商業價值的條款授權。</span><span class="sxs-lookup"><span data-stu-id="878ba-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="878ba-112">SSPK 授權提供與 hello 業界：</span><span class="sxs-lookup"><span data-stu-id="878ba-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="878ba-113">Smooth Streaming Porting Kit 的 C++ 原始碼</span><span class="sxs-lookup"><span data-stu-id="878ba-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="878ba-114">實作 Smooth Streaming 用戶端功能</span><span class="sxs-lookup"><span data-stu-id="878ba-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="878ba-115">新增格式剖析、啟發學習法、緩衝處理邏輯等等</span><span class="sxs-lookup"><span data-stu-id="878ba-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="878ba-116">播放器應用程式 API</span><span class="sxs-lookup"><span data-stu-id="878ba-116">Player application APIs</span></span> 
  * <span data-ttu-id="878ba-117">可與媒體播放器應用程式互動的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="878ba-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="878ba-118">平台抽象層 (PAL) 介面</span><span class="sxs-lookup"><span data-stu-id="878ba-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="878ba-119">程式設計介面的互動 hello 作業系統 （執行緒、 通訊端）</span><span class="sxs-lookup"><span data-stu-id="878ba-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="878ba-120">硬體抽象層 (HAL) 介面</span><span class="sxs-lookup"><span data-stu-id="878ba-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="878ba-121">用於與硬體 A/V 解碼器 (解碼、轉譯) 互動的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="878ba-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="878ba-122">數位版權管理 (DRM) 介面</span><span class="sxs-lookup"><span data-stu-id="878ba-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="878ba-123">處理 DRM 透過 hello DRM 抽象層 (DAL) 的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="878ba-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="878ba-124">Microsoft PlayReady Porting Kit 個別出貨，但可透過這個介面整合。</span><span class="sxs-lookup"><span data-stu-id="878ba-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="878ba-125">如需 Microsoft PlayReady Device 授權的詳細資訊，請按一下 [這裡](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl)。</span><span class="sxs-lookup"><span data-stu-id="878ba-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="878ba-126">實作範例</span><span class="sxs-lookup"><span data-stu-id="878ba-126">Implementation samples</span></span> 
  * <span data-ttu-id="878ba-127">適用於 Linux 的 PAL 實作範例</span><span class="sxs-lookup"><span data-stu-id="878ba-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="878ba-128">適用於 GStreamer 的 HAL 實作範例</span><span class="sxs-lookup"><span data-stu-id="878ba-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="878ba-129">授權選項</span><span class="sxs-lookup"><span data-stu-id="878ba-129">Licensing Options</span></span>
<span data-ttu-id="878ba-130">Microsoft Smooth Streaming Client Porting Kit 兩個不同的授權合約下進行可用 toolicensees： 一個用於開發 Smooth Streaming 用戶端暫時產品和另一個用於散發 Smooth Streaming 用戶端最終產品 tooend 使用者。</span><span class="sxs-lookup"><span data-stu-id="878ba-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="878ba-131">晶片組製造商、 系統整合者，或獨立軟體廠商 (Isv) 要求來源的程式碼移植套件 toodevelop 暫時產品 Microsoft Smooth Streaming Client Porting Kit**暫時產品授權**應該執行。</span><span class="sxs-lookup"><span data-stu-id="878ba-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="878ba-132">如裝置製造商或 Smooth Streaming 用戶端最終產品 tooend 對於使用者而言，需要散布權利 Isv hello Microsoft Smooth Streaming Client Porting Kit**最終產品授權**應該執行。</span><span class="sxs-lookup"><span data-stu-id="878ba-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="878ba-133">Microsoft Smooth Streaming Client Porting Kit 中期產品授權</span><span class="sxs-lookup"><span data-stu-id="878ba-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="878ba-134">依據本授權，Microsoft 提供 Smooth Streaming Client Porting Kit hello 必要智慧財產的權限 toodevelop 及散發 Smooth Streaming 用戶端暫時產品 tooother Smooth Streaming Client Porting Kit 裝置被授權人的將 Smooth Streaming 用戶端最後一個產品。</span><span class="sxs-lookup"><span data-stu-id="878ba-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="878ba-135">免費結構</span><span class="sxs-lookup"><span data-stu-id="878ba-135">Fee structure</span></span>
<span data-ttu-id="878ba-136">美國 $50,000 單次許可費用提供存取 toohello Smooth Streaming Client Porting Kit。</span><span class="sxs-lookup"><span data-stu-id="878ba-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="878ba-137">Microsoft Smooth Streaming Client Porting Kit 最終產品授權</span><span class="sxs-lookup"><span data-stu-id="878ba-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="878ba-138">依據本授權，Microsoft 會提供所有必要的智慧財產的權限 tooreceive Smooth Streaming 用戶端暫時產品與其他的 Smooth Streaming Client Porting Kit 人均 toodistribute 公司品牌 Smooth Streaming 用戶端最後產品 tooend 使用者。</span><span class="sxs-lookup"><span data-stu-id="878ba-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="878ba-139">免費結構</span><span class="sxs-lookup"><span data-stu-id="878ba-139">Fee structure</span></span>
<span data-ttu-id="878ba-140">hello Smooth Streaming 用戶端最終產品提供獲微軟授權使用模型做為下：</span><span class="sxs-lookup"><span data-stu-id="878ba-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="878ba-141">送交的每一裝置實作為 $0.10 美元</span><span class="sxs-lookup"><span data-stu-id="878ba-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="878ba-142">hello 獲微軟授權使用的上限為 50000 每年</span><span class="sxs-lookup"><span data-stu-id="878ba-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="878ba-143">每年前 10,000 個裝置實作不需權利金</span><span class="sxs-lookup"><span data-stu-id="878ba-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="878ba-144">授權程序和 SSPK 存取</span><span class="sxs-lookup"><span data-stu-id="878ba-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="878ba-145">有關所有授權查詢，請寄送電子郵件至 [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) 。</span><span class="sxs-lookup"><span data-stu-id="878ba-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="878ba-146">hello [SSPK 發佈入口網站](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/)是可存取 tooregistered 暫時被授權人。</span><span class="sxs-lookup"><span data-stu-id="878ba-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="878ba-147">過渡期間和最終 SSPK 被授權人可以送出技術問題太[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="878ba-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="878ba-148">Microsoft Smooth Streaming 用戶端中期產品合約被授權者</span><span class="sxs-lookup"><span data-stu-id="878ba-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="878ba-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="878ba-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="878ba-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="878ba-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="878ba-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="878ba-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="878ba-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="878ba-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-153">Alticast Corporation</span></span>
* <span data-ttu-id="878ba-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="878ba-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="878ba-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="878ba-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-157">Cavium, Inc.</span></span>
* <span data-ttu-id="878ba-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="878ba-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-159">Enseo, Inc.</span></span>
* <span data-ttu-id="878ba-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="878ba-160">Fluendo S.A.</span></span>
* <span data-ttu-id="878ba-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="878ba-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="878ba-162">Infomir GMBH</span></span>
* <span data-ttu-id="878ba-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="878ba-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="878ba-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="878ba-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="878ba-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="878ba-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-166">MediaTek Inc.</span></span>
* <span data-ttu-id="878ba-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="878ba-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="878ba-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="878ba-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="878ba-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="878ba-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="878ba-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="878ba-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="878ba-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="878ba-172">SoftAtHome</span></span>
* <span data-ttu-id="878ba-173">索尼公司</span><span class="sxs-lookup"><span data-stu-id="878ba-173">Sony Corporation</span></span>
* <span data-ttu-id="878ba-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="878ba-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="878ba-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="878ba-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="878ba-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="878ba-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="878ba-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="878ba-180">Microsoft Smooth Streaming 用戶端最終產品合約被授權者</span><span class="sxs-lookup"><span data-stu-id="878ba-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="878ba-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="878ba-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="878ba-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="878ba-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="878ba-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="878ba-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="878ba-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="878ba-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="878ba-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="878ba-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="878ba-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="878ba-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="878ba-189">VE TİC.</span></span> <span data-ttu-id="878ba-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="878ba-190">A.Ş</span></span>
* <span data-ttu-id="878ba-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="878ba-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="878ba-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="878ba-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="878ba-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="878ba-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="878ba-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="878ba-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-196">Enseo, Inc.</span></span>
* <span data-ttu-id="878ba-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="878ba-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="878ba-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="878ba-198">Fluendo S.A.</span></span>
* <span data-ttu-id="878ba-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="878ba-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="878ba-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="878ba-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="878ba-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="878ba-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="878ba-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="878ba-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="878ba-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="878ba-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="878ba-205">Infomir GMBH</span></span>
* <span data-ttu-id="878ba-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="878ba-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-207">KDDI Corporation</span></span>
* <span data-ttu-id="878ba-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="878ba-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="878ba-209">Orange SA</span></span>
* <span data-ttu-id="878ba-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="878ba-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="878ba-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="878ba-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="878ba-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="878ba-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="878ba-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="878ba-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="878ba-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="878ba-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="878ba-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="878ba-216">致振企業股份有限公司</span><span class="sxs-lookup"><span data-stu-id="878ba-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="878ba-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="878ba-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="878ba-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="878ba-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="878ba-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="878ba-219">SoftAtHome</span></span>
* <span data-ttu-id="878ba-220">索尼公司</span><span class="sxs-lookup"><span data-stu-id="878ba-220">Sony Corporation</span></span>
* <span data-ttu-id="878ba-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="878ba-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="878ba-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="878ba-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="878ba-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="878ba-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="878ba-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="878ba-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="878ba-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="878ba-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="878ba-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="878ba-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="878ba-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-228">Wistron Corporation</span></span>
* <span data-ttu-id="878ba-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="878ba-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="878ba-230">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="878ba-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="878ba-231">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="878ba-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

