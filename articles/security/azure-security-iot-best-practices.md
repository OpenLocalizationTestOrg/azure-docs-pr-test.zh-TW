---
title: "物聯網安全性最佳作法 | Microsoft Docs"
description: "本文提供 Microsoft 物聯網安全性最佳作法的策劃清單及一般建議。"
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 8efc0053458e338ac1afe98d9ce970c1d5cbfa81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="54811-103">物聯網安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="54811-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="54811-104">保護物聯網 (IoT) 基礎結構是任何涉入 IoT 解決方案的人的重要任務。</span><span class="sxs-lookup"><span data-stu-id="54811-104">Securing the Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="54811-105">由於涉及的裝置數目和這些裝置的分散式質性，危及數百萬個 IoT 裝置的相關安全性事件影響廣泛，不可等閒視之。</span><span class="sxs-lookup"><span data-stu-id="54811-105">Because of the number of devices involved and the distributed nature of these devices, the impact a security event related to compromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="54811-106">因此，IoT 安全性需要一套深度安全性作法。</span><span class="sxs-lookup"><span data-stu-id="54811-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="54811-107">資料在雲端中及流動於私人和公用網路上時都需要安全保護。</span><span class="sxs-lookup"><span data-stu-id="54811-107">Data needs to be secure in the cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="54811-108">需要備妥方法來安全地佈建 IoT 裝置本身。</span><span class="sxs-lookup"><span data-stu-id="54811-108">Methods need to be in place to securely provision the IoT devices themselves.</span></span> <span data-ttu-id="54811-109">從裝置到網路，以至於雲端後端，每一層都需要確保絕對的安全性。</span><span class="sxs-lookup"><span data-stu-id="54811-109">Each layer, from device, to network, to cloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="54811-110">IoT 最佳作法可分類如下︰</span><span class="sxs-lookup"><span data-stu-id="54811-110">IoT best practices can be categorized in the following way:</span></span>

* <span data-ttu-id="54811-111">IoT 硬體製造商或整合者</span><span class="sxs-lookup"><span data-stu-id="54811-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="54811-112">IoT 解決方案開發人員</span><span class="sxs-lookup"><span data-stu-id="54811-112">IoT solution developer</span></span>
* <span data-ttu-id="54811-113">IoT 解決方案部署人員</span><span class="sxs-lookup"><span data-stu-id="54811-113">IoT solution deployer</span></span>
* <span data-ttu-id="54811-114">IoT 解決方案操作人員</span><span class="sxs-lookup"><span data-stu-id="54811-114">IoT solution operator</span></span>

<span data-ttu-id="54811-115">本文摘要說明 [物聯網安全性最佳作法](../iot-suite/iot-security-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="54811-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="54811-116">如需詳細資訊，請參閱該文件。</span><span class="sxs-lookup"><span data-stu-id="54811-116">Please refer to that article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="54811-117">IoT 硬體製造商或整合者</span><span class="sxs-lookup"><span data-stu-id="54811-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="54811-118">如果您是 IoT 硬體製造商或硬體整合者，請依循下面的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="54811-118">Follow the best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="54811-119">**設定符合最小需求的硬體範圍**：硬體設計應包括硬體運作時所需的最少功能，僅此而已。</span><span class="sxs-lookup"><span data-stu-id="54811-119">**Scope hardware to minimum requirements**: the hardware design should include minimum features required for operation of the hardware, and nothing more.</span></span> 
* <span data-ttu-id="54811-120">**讓硬體具備防竄改功能**：內建偵測硬體實體竄改 (例如開啟裝置外蓋、移除裝置零件等等) 的機制。</span><span class="sxs-lookup"><span data-stu-id="54811-120">**Make hardware tamper proof**: build in mechanisms to detect physical tampering of hardware, such as opening the device cover, removing a part of the device, etc.</span></span> 
* <span data-ttu-id="54811-121">**建立周圍安全的硬體**：如果 [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) 允許，請建立安全性功能，例如以安全與加密儲存體及信任的平台模組 (TPM) 為基礎的開機功能。</span><span class="sxs-lookup"><span data-stu-id="54811-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="54811-122">**保護在裝置升級安全**：在裝置存留期間升級韌體是不可避免的。</span><span class="sxs-lookup"><span data-stu-id="54811-122">**Make upgrades secure**: upgrading firmware during lifetime of the device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="54811-123">IoT 解決方案開發人員</span><span class="sxs-lookup"><span data-stu-id="54811-123">IoT solution developer</span></span>
<span data-ttu-id="54811-124">如果您是 IoT 解決方案開發人員，請依循下面的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="54811-124">Follow the best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="54811-125">**依循安全軟體開發方法**：開發安全軟體需要從專案一開始時就思考安全性相關事項，一直到專案的實作、測試及部署。</span><span class="sxs-lookup"><span data-stu-id="54811-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from the inception of the project all the way to its implementation, testing, and deployment.</span></span>
* <span data-ttu-id="54811-126">**小心選擇開放原始碼軟體**：開放原始碼軟體可提供快速開發解決方案的機會。</span><span class="sxs-lookup"><span data-stu-id="54811-126">**Choose open source software with care**: open source software provides an opportunity to quickly develop solutions.</span></span>
* <span data-ttu-id="54811-127">**小心整合**：程式庫和 API 的界限中存在許多軟體安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="54811-127">**Integrate with care**: many of the software security flaws exist at the boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="54811-128">IoT 解決方案部署人員</span><span class="sxs-lookup"><span data-stu-id="54811-128">IoT solution deployer</span></span>
<span data-ttu-id="54811-129">如果您是 IoT 解決方案部署人員，請依循下面的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="54811-129">Follow the best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="54811-130">**安全地部署硬體**：IoT 部署可能需要將硬體部署在不安全的位置，例如公共空間或不受監督的區域。</span><span class="sxs-lookup"><span data-stu-id="54811-130">**Deploy hardware securely**: IoT deployments may require hardware to be deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="54811-131">**維護驗證金鑰安全**：在部署期間，每個裝置都需要由雲端服務所產生的裝置識別碼和關聯的驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="54811-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by the cloud service.</span></span> <span data-ttu-id="54811-132">在部署之後也務必保護這些金鑰的實體安全。</span><span class="sxs-lookup"><span data-stu-id="54811-132">Keep these keys physically safe even after the deployment.</span></span> <span data-ttu-id="54811-133">任何洩漏的金鑰都可能被惡意裝置用來偽裝成現有的裝置。</span><span class="sxs-lookup"><span data-stu-id="54811-133">Any compromised key can be used by a malicious device to masquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="54811-134">IoT 解決方案操作人員</span><span class="sxs-lookup"><span data-stu-id="54811-134">IoT solution operator</span></span>
<span data-ttu-id="54811-135">如果您是 IoT 解決方案操作人員，請依循下面的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="54811-135">Follow the best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="54811-136">**讓系統維持在最新狀態**：確保裝置的作業系統和所有裝置驅動程式都已更新至最新版本。</span><span class="sxs-lookup"><span data-stu-id="54811-136">**Keep systems up to date**: ensure device operating systems and all device drivers are updated to the latest versions.</span></span> 
* <span data-ttu-id="54811-137">**針對惡意活動提供保護**：如果作業系統允許，請在每部裝置的作業系統中加裝防毒或反惡意程式碼功能。</span><span class="sxs-lookup"><span data-stu-id="54811-137">**Protect against malicious activity**: if the operating system permits, place the latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="54811-138">**經常稽核**：回應安全性事件時，針對安全性相關問題稽核 IoT 基礎結構是關鍵所在。</span><span class="sxs-lookup"><span data-stu-id="54811-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding to security incidents.</span></span>
* <span data-ttu-id="54811-139">**實體保護 IoT 基礎結構**：對 IoT 基礎結構最嚴重的安全性攻擊是透過實際接觸裝置的方式進行攻擊。</span><span class="sxs-lookup"><span data-stu-id="54811-139">**Physically protect the IoT infrastructure**: the worst security attacks against IoT infrastructure are launched using physical access to devices.</span></span>
* <span data-ttu-id="54811-140">**保護雲端認證**：用來設定及操作 IoT 部署的雲端驗證認證可能是存取及危及 IoT 系統的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="54811-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly the easiest way to gain access and compromise an IoT system.</span></span> 

