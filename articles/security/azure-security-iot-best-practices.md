---
title: "項目安全性最佳做法的 aaaInternet |Microsoft 文件"
description: "hello 發行項提供的項目安全性最佳作法和一般建議的 Microsoft Internet 策劃的清單。"
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
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="8ff12-103">物聯網安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="8ff12-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="8ff12-104">保護的 hello 物聯網 (IoT) 基礎結構是個 IoT 解決方案所需的任何人的重要任務。</span><span class="sxs-lookup"><span data-stu-id="8ff12-104">Securing hello Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="8ff12-105">由於包含裝置 hello 數目與 hello 分散式的本質，這些裝置，hello 影響安全性事件的相關 toocompromise 數百萬個 IoT 裝置為非一般的而且可以有廣泛的影響。</span><span class="sxs-lookup"><span data-stu-id="8ff12-105">Because of hello number of devices involved and hello distributed nature of these devices, hello impact a security event related toocompromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="8ff12-106">因此，IoT 安全性需要一套深度安全性作法。</span><span class="sxs-lookup"><span data-stu-id="8ff12-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="8ff12-107">資料需求 toobe 安全 hello 雲端中，因為它會透過私人和公用網路移動。</span><span class="sxs-lookup"><span data-stu-id="8ff12-107">Data needs toobe secure in hello cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="8ff12-108">需要的地方 toosecurely 佈建 hello IoT 裝置本身在 toobe 方法。</span><span class="sxs-lookup"><span data-stu-id="8ff12-108">Methods need toobe in place toosecurely provision hello IoT devices themselves.</span></span> <span data-ttu-id="8ff12-109">每個圖層，從裝置、 toonetwork、 toocloud 後端需要增強式安全性保證。</span><span class="sxs-lookup"><span data-stu-id="8ff12-109">Each layer, from device, toonetwork, toocloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="8ff12-110">IoT 最佳作法可以分類在 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="8ff12-110">IoT best practices can be categorized in hello following way:</span></span>

* <span data-ttu-id="8ff12-111">IoT 硬體製造商或整合者</span><span class="sxs-lookup"><span data-stu-id="8ff12-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="8ff12-112">IoT 解決方案開發人員</span><span class="sxs-lookup"><span data-stu-id="8ff12-112">IoT solution developer</span></span>
* <span data-ttu-id="8ff12-113">IoT 解決方案部署人員</span><span class="sxs-lookup"><span data-stu-id="8ff12-113">IoT solution deployer</span></span>
* <span data-ttu-id="8ff12-114">IoT 解決方案操作人員</span><span class="sxs-lookup"><span data-stu-id="8ff12-114">IoT solution operator</span></span>

<span data-ttu-id="8ff12-115">本文摘要說明 [物聯網安全性最佳作法](../iot-suite/iot-security-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="8ff12-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="8ff12-116">請如需詳細資訊，參閱 toothat 發行項。</span><span class="sxs-lookup"><span data-stu-id="8ff12-116">Please refer toothat article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="8ff12-117">IoT 硬體製造商或整合者</span><span class="sxs-lookup"><span data-stu-id="8ff12-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="8ff12-118">如果您是 IoT 硬體製造商或硬體整合器，請遵循 hello 以下的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="8ff12-118">Follow hello best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="8ff12-119">**範圍硬體 toominimum 需求**: hello 硬體設計應該包含最少的 hello 硬體，而無其他作業所需的功能。</span><span class="sxs-lookup"><span data-stu-id="8ff12-119">**Scope hardware toominimum requirements**: hello hardware design should include minimum features required for operation of hello hardware, and nothing more.</span></span> 
* <span data-ttu-id="8ff12-120">**進行硬體竄改**： 建置機制 toodetect 實體竄改的硬體，例如開啟 hello 裝置封面，移除 hello 裝置等等的一部分。</span><span class="sxs-lookup"><span data-stu-id="8ff12-120">**Make hardware tamper proof**: build in mechanisms toodetect physical tampering of hardware, such as opening hello device cover, removing a part of hello device, etc.</span></span> 
* <span data-ttu-id="8ff12-121">**建立周圍安全的硬體**：如果 [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) 允許，請建立安全性功能，例如以安全與加密儲存體及信任的平台模組 (TPM) 為基礎的開機功能。</span><span class="sxs-lookup"><span data-stu-id="8ff12-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="8ff12-122">**進行升級安全**: hello 裝置存留期間升級韌體是無可避免的。</span><span class="sxs-lookup"><span data-stu-id="8ff12-122">**Make upgrades secure**: upgrading firmware during lifetime of hello device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="8ff12-123">IoT 解決方案開發人員</span><span class="sxs-lookup"><span data-stu-id="8ff12-123">IoT solution developer</span></span>
<span data-ttu-id="8ff12-124">如果您的 IoT 解決方案開發人員，請遵循 hello 以下的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="8ff12-124">Follow hello best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="8ff12-125">**請遵循安全軟體開發方法**： 開發安全的軟體需要從頭關於 hello 開始 hello 專案的安全性，所有 hello 方式 tooits 實作、 測試和部署。</span><span class="sxs-lookup"><span data-stu-id="8ff12-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from hello inception of hello project all hello way tooits implementation, testing, and deployment.</span></span>
* <span data-ttu-id="8ff12-126">**選擇小心使用的開放原始碼軟體**： 開放原始碼軟體提供了一個機會 tooquickly 開發方案。</span><span class="sxs-lookup"><span data-stu-id="8ff12-126">**Choose open source software with care**: open source software provides an opportunity tooquickly develop solutions.</span></span>
* <span data-ttu-id="8ff12-127">**整合小心**： 許多 hello 軟體安全性缺陷在於程式庫和應用程式開發介面的 hello 界限。</span><span class="sxs-lookup"><span data-stu-id="8ff12-127">**Integrate with care**: many of hello software security flaws exist at hello boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="8ff12-128">IoT 解決方案部署人員</span><span class="sxs-lookup"><span data-stu-id="8ff12-128">IoT solution deployer</span></span>
<span data-ttu-id="8ff12-129">如果您的 IoT 解決方案部署器，請遵循 hello 以下的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="8ff12-129">Follow hello best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="8ff12-130">**安全地部署硬體**: IoT 部署可能需要硬體 toobe 部署在不安全的位置，例如公用空間或不受監督的地區設定。</span><span class="sxs-lookup"><span data-stu-id="8ff12-130">**Deploy hardware securely**: IoT deployments may require hardware toobe deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="8ff12-131">**維護安全的驗證金鑰**： 在部署期間，每個裝置需要裝置識別碼和相關聯 hello 雲端服務所產生的驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="8ff12-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by hello cloud service.</span></span> <span data-ttu-id="8ff12-132">即使在 hello 部署之後保留這些金鑰實際安全。</span><span class="sxs-lookup"><span data-stu-id="8ff12-132">Keep these keys physically safe even after hello deployment.</span></span> <span data-ttu-id="8ff12-133">惡意裝置 toomasquerade 可以使用任何受危害的金鑰作為現有的裝置。</span><span class="sxs-lookup"><span data-stu-id="8ff12-133">Any compromised key can be used by a malicious device toomasquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="8ff12-134">IoT 解決方案操作人員</span><span class="sxs-lookup"><span data-stu-id="8ff12-134">IoT solution operator</span></span>
<span data-ttu-id="8ff12-135">如果您的 IoT 解決方案運算子，請遵循 hello 以下的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="8ff12-135">Follow hello best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="8ff12-136">**保留系統向上 toodate**： 確保裝置的作業系統和所有裝置驅動程式更新的 toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="8ff12-136">**Keep systems up toodate**: ensure device operating systems and all device drivers are updated toohello latest versions.</span></span> 
* <span data-ttu-id="8ff12-137">**防範惡意活動**: hello 作業系統允許時，如果將 hello 最新的防毒和反惡意程式碼功能放在每個裝置作業系統上。</span><span class="sxs-lookup"><span data-stu-id="8ff12-137">**Protect against malicious activity**: if hello operating system permits, place hello latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="8ff12-138">**經常稽核**： 稽核 IoT 基礎結構的安全性相關問題回應 toosecurity 事件時，是索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8ff12-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding toosecurity incidents.</span></span>
* <span data-ttu-id="8ff12-139">**實際保護 hello IoT 基礎結構**: hello 最差的 IoT 基礎結構的安全性攻擊所使用的實體存取 toodevices 加以啟動。</span><span class="sxs-lookup"><span data-stu-id="8ff12-139">**Physically protect hello IoT infrastructure**: hello worst security attacks against IoT infrastructure are launched using physical access toodevices.</span></span>
* <span data-ttu-id="8ff12-140">**保護雲端認證**： 用來設定和操作 IoT 部署的雲端驗證認證可能是最簡單方式 toogain 存取 hello 和入侵 IoT 系統。</span><span class="sxs-lookup"><span data-stu-id="8ff12-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly hello easiest way toogain access and compromise an IoT system.</span></span> 

