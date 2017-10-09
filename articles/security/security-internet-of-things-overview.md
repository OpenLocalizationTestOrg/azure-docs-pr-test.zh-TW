---
title: "aaaSecure 您物聯網 (IoT) 在 Azure 中 |Microsoft 文件"
description: " Azure 物聯網 (IoT) 服務提供廣泛的功能。 這篇文章可協助您了解如何 toosecure 您在 Azure 中的 IoT 解決方案。 "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="dd449-104">物聯網安全性概觀</span><span class="sxs-lookup"><span data-stu-id="dd449-104">Internet of Things security overview</span></span>
<span data-ttu-id="dd449-105">Azure 物聯網 (IoT) 服務提供廣泛的功能。</span><span class="sxs-lookup"><span data-stu-id="dd449-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="dd449-106">這些企業等級的服務可讓您：</span><span class="sxs-lookup"><span data-stu-id="dd449-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="dd449-107">從裝置收集資料</span><span class="sxs-lookup"><span data-stu-id="dd449-107">Collect data from devices</span></span>
* <span data-ttu-id="dd449-108">分析移動中的資料串流</span><span class="sxs-lookup"><span data-stu-id="dd449-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="dd449-109">儲存和查詢大型資料集</span><span class="sxs-lookup"><span data-stu-id="dd449-109">Store and query large data sets</span></span>
* <span data-ttu-id="dd449-110">視覺化即時和歷程記錄資料</span><span class="sxs-lookup"><span data-stu-id="dd449-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="dd449-111">與後端辦公室系統整合</span><span class="sxs-lookup"><span data-stu-id="dd449-111">Integrate with back-office systems</span></span>

<span data-ttu-id="dd449-112">toodeliver 一起封裝這些功能，Azure IoT 套件多個 Azure 服務使用自訂延伸模組做為預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="dd449-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="dd449-113">這些預先設定的解決方案是常見的 IoT 解決方案模式可協助您採取 toodeliver IoT 解決方案 tooreduce hello 時間的基底實作。</span><span class="sxs-lookup"><span data-stu-id="dd449-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="dd449-114">使用 hello IoT 軟體開發套件，您可以自訂及擴充這些解決方案 toomeet 您自己的需求。</span><span class="sxs-lookup"><span data-stu-id="dd449-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="dd449-115">您也可以使用這些解決方案作為開發新 IoT 解決方案時的範例或範本。</span><span class="sxs-lookup"><span data-stu-id="dd449-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="dd449-116">hello Azure IoT 套件是功能強大的解決方案，針對您的 IoT 需求。</span><span class="sxs-lookup"><span data-stu-id="dd449-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="dd449-117">不過，它是您的安全性考量事項從 hello 開始設計的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="dd449-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="dd449-118">Hello 單單只有 IoT 裝置數目，因為任何安全性事件可能很快就會造成嚴重的後果的廣泛事件。</span><span class="sxs-lookup"><span data-stu-id="dd449-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="dd449-119">toohelp 您了解如何 toosecure 您的 IoT 解決方案，我們有下列資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="dd449-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="dd449-120">安全性架構</span><span class="sxs-lookup"><span data-stu-id="dd449-120">Security architecture</span></span>
<span data-ttu-id="dd449-121">在設計系統時，它是重要的 toounderstand hello 潛在威脅 toothat 系統，而且同理，加入適當的措施，因為 hello 系統是設計和架構。</span><span class="sxs-lookup"><span data-stu-id="dd449-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="dd449-122">請務必 toodesign 會 hello 的安全性考量事項產品從 hello 開始因為了解如何攻擊者可能會無法 toocompromise 系統可協助確定適當的安全防護處於從 hello 開頭的位置。</span><span class="sxs-lookup"><span data-stu-id="dd449-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="dd449-123">您可以了解 IoT 安全性架構，方法是閱讀 [物聯網安全性架構](../iot-suite/iot-security-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="dd449-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="dd449-124">本文將討論下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd449-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="dd449-125">保障安全從威脅模型開始</span><span class="sxs-lookup"><span data-stu-id="dd449-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="dd449-126">IoT 中的安全性</span><span class="sxs-lookup"><span data-stu-id="dd449-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="dd449-127">威脅模型化 hello Azure IoT 參考架構</span><span class="sxs-lookup"><span data-stu-id="dd449-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="dd449-128">從 hello 接地安全性</span><span class="sxs-lookup"><span data-stu-id="dd449-128">Security from hello ground up</span></span>
<span data-ttu-id="dd449-129">hello IoT 帶來唯一的安全性、 隱私權和相容性挑戰 toobusinesses 全球。</span><span class="sxs-lookup"><span data-stu-id="dd449-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="dd449-130">與傳統網路技術，其中這些問題心力都圍繞軟體和實作的方式，不同的是 IoT 有關 hello e-security 與 hello 實體領域聚合時會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="dd449-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="dd449-131">保護 IoT 解決方案需要確保安全佈建裝置，這些裝置與 hello 雲端，以及在處理與儲存期間 hello 雲端中的安全資料保護之間的安全連線。</span><span class="sxs-lookup"><span data-stu-id="dd449-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="dd449-132">但是，會針對這類功能運作的是資源受限的裝置、根據地理位置分佈的部署，以及解決方案中的許多裝置。</span><span class="sxs-lookup"><span data-stu-id="dd449-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="dd449-133">您可以了解如何 toohandle 閱讀這些區域中的安全性[從 hello 地面物聯網安全性](../iot-suite/securing-iot-ground-up.md)。</span><span class="sxs-lookup"><span data-stu-id="dd449-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="dd449-134">hello 篇文章會討論下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd449-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="dd449-135">從接地 hello 的安全基礎結構</span><span class="sxs-lookup"><span data-stu-id="dd449-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="dd449-136">Microsoft Azure - 適用於貴公司的安全 IoT 基礎結構</span><span class="sxs-lookup"><span data-stu-id="dd449-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="dd449-137">最佳作法</span><span class="sxs-lookup"><span data-stu-id="dd449-137">Best Practices</span></span>
<span data-ttu-id="dd449-138">保護 IoT 基礎結構需要嚴格的深度安全性防禦策略。</span><span class="sxs-lookup"><span data-stu-id="dd449-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="dd449-139">從保護 hello 雲端中的資料保護資料的完整性，而傳送 hello 透過公用網際網路，toosecurely 佈建裝置，每個圖層組建中更高的安全性保證 hello 整體基礎結構。</span><span class="sxs-lookup"><span data-stu-id="dd449-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="dd449-140">您可以藉由閱讀 [物聯網安全性最佳作法](../iot-suite/iot-security-best-practices.md)，了解物聯網安全性最佳作法。</span><span class="sxs-lookup"><span data-stu-id="dd449-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="dd449-141">hello 篇文章會討論下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd449-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="dd449-142">IoT 硬體製造商/整合者</span><span class="sxs-lookup"><span data-stu-id="dd449-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="dd449-143">IoT 解決方案開發人員</span><span class="sxs-lookup"><span data-stu-id="dd449-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="dd449-144">IoT 解決方案部署人員</span><span class="sxs-lookup"><span data-stu-id="dd449-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="dd449-145">IoT 解決方案操作人員</span><span class="sxs-lookup"><span data-stu-id="dd449-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
