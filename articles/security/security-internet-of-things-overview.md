---
title: "在 Azure 中保護您的物聯網 (IoT) | Microsoft Docs"
description: " Azure 物聯網 (IoT) 服務提供廣泛的功能。 本文章協助您了解如何在 Azure 中保護您的 IoT 解決方案。 "
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
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="1fccc-104">物聯網安全性概觀</span><span class="sxs-lookup"><span data-stu-id="1fccc-104">Internet of Things security overview</span></span>
<span data-ttu-id="1fccc-105">Azure 物聯網 (IoT) 服務提供廣泛的功能。</span><span class="sxs-lookup"><span data-stu-id="1fccc-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="1fccc-106">這些企業等級的服務可讓您：</span><span class="sxs-lookup"><span data-stu-id="1fccc-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="1fccc-107">從裝置收集資料</span><span class="sxs-lookup"><span data-stu-id="1fccc-107">Collect data from devices</span></span>
* <span data-ttu-id="1fccc-108">分析移動中的資料串流</span><span class="sxs-lookup"><span data-stu-id="1fccc-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="1fccc-109">儲存和查詢大型資料集</span><span class="sxs-lookup"><span data-stu-id="1fccc-109">Store and query large data sets</span></span>
* <span data-ttu-id="1fccc-110">視覺化即時和歷程記錄資料</span><span class="sxs-lookup"><span data-stu-id="1fccc-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="1fccc-111">與後端辦公室系統整合</span><span class="sxs-lookup"><span data-stu-id="1fccc-111">Integrate with back-office systems</span></span>

<span data-ttu-id="1fccc-112">為了提供這些功能，Azure IoT 套件將多個 Azure 服務與自訂延伸模組封裝在一起做為預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1fccc-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="1fccc-113">這些預先設定的解決方案是常見 IoT 解決方案模式的基礎實作，可幫助您減少實行 IoT 解決方案所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="1fccc-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="1fccc-114">透過使用 IoT 軟體開發套件，您將可自訂和擴充這些解決方案來滿足您自己的需求。</span><span class="sxs-lookup"><span data-stu-id="1fccc-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="1fccc-115">您也可以使用這些解決方案做為開發新 IoT 解決方案時的範例或範本。</span><span class="sxs-lookup"><span data-stu-id="1fccc-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="1fccc-116">Azure IoT 套件是針對您的 IoT 需求的功能強大的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1fccc-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="1fccc-117">不過，最重要的是您的 IoT 解決方案一開始就是以安全性為考量而設計的。</span><span class="sxs-lookup"><span data-stu-id="1fccc-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="1fccc-118">因為有大量的 IoT 裝置，所以任何安全性事件可能很快就會造成有嚴重後果的大規模事件。</span><span class="sxs-lookup"><span data-stu-id="1fccc-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="1fccc-119">為了協助您了解如何保護您的 IoT 解決方案，我們提供下列資訊。</span><span class="sxs-lookup"><span data-stu-id="1fccc-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="1fccc-120">安全性架構</span><span class="sxs-lookup"><span data-stu-id="1fccc-120">Security architecture</span></span>
<span data-ttu-id="1fccc-121">在設計系統時，我們應了解該系統的潛在威脅並加入適當的防禦機制，以妥善設計系統與其架構。</span><span class="sxs-lookup"><span data-stu-id="1fccc-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="1fccc-122">在一開始設計產品時就先考量安全性是很重要的，因為了解攻擊者可能如何破壞系統，有助於從一開始就備妥適當的安全防護功能。</span><span class="sxs-lookup"><span data-stu-id="1fccc-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="1fccc-123">您可以了解 IoT 安全性架構，方法是閱讀 [物聯網安全性架構](../iot-suite/iot-security-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="1fccc-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="1fccc-124">本文章討論下列主題：</span><span class="sxs-lookup"><span data-stu-id="1fccc-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="1fccc-125">保障安全從威脅模型開始</span><span class="sxs-lookup"><span data-stu-id="1fccc-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="1fccc-126">IoT 中的安全性</span><span class="sxs-lookup"><span data-stu-id="1fccc-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="1fccc-127">為 Azure IoT 參考架構進行威脅模型化作業</span><span class="sxs-lookup"><span data-stu-id="1fccc-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="1fccc-128">從頭建立安全性</span><span class="sxs-lookup"><span data-stu-id="1fccc-128">Security from the ground up</span></span>
<span data-ttu-id="1fccc-129">IoT 使得全球企業面臨獨特的安全性、隱私權及相容性挑戰。</span><span class="sxs-lookup"><span data-stu-id="1fccc-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="1fccc-130">不同於傳統網路技術 (這類問題是以軟體及其實作方式為中心)，IoT 在意的是當網路與實體世界交會時會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="1fccc-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="1fccc-131">保護 IoT 解決方案要求確保安全佈建裝置，保護這些裝置與雲端之間的連接，以及在處理和儲存期間保護雲端中資料保護的安全。</span><span class="sxs-lookup"><span data-stu-id="1fccc-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="1fccc-132">但是，會針對這類功能運作的是資源受限的裝置、根據地理位置分佈的部署，以及解決方案中的許多裝置。</span><span class="sxs-lookup"><span data-stu-id="1fccc-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="1fccc-133">您可以藉由閱讀 [徹底保護物聯網安全性](../iot-suite/securing-iot-ground-up.md)，了解如何處理這些區域中的安全性。</span><span class="sxs-lookup"><span data-stu-id="1fccc-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="1fccc-134">本文章討論下列主題：</span><span class="sxs-lookup"><span data-stu-id="1fccc-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="1fccc-135">徹底保護基礎結構的安全</span><span class="sxs-lookup"><span data-stu-id="1fccc-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="1fccc-136">Microsoft Azure - 適用於貴公司的安全 IoT 基礎結構</span><span class="sxs-lookup"><span data-stu-id="1fccc-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="1fccc-137">最佳作法</span><span class="sxs-lookup"><span data-stu-id="1fccc-137">Best Practices</span></span>
<span data-ttu-id="1fccc-138">保護 IoT 基礎結構需要嚴格的深度安全性防禦策略。</span><span class="sxs-lookup"><span data-stu-id="1fccc-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="1fccc-139">從保護雲端資料的安全、保護資料在公用網際網路上傳輸時的資料完整性，到安全佈建裝置，在整體基礎結構的每一階層建置更強大的安全性保證。</span><span class="sxs-lookup"><span data-stu-id="1fccc-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="1fccc-140">您可以藉由閱讀 [物聯網安全性最佳作法](../iot-suite/iot-security-best-practices.md)，了解物聯網安全性最佳作法。</span><span class="sxs-lookup"><span data-stu-id="1fccc-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="1fccc-141">本文章討論下列主題：</span><span class="sxs-lookup"><span data-stu-id="1fccc-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="1fccc-142">IoT 硬體製造商/整合者</span><span class="sxs-lookup"><span data-stu-id="1fccc-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="1fccc-143">IoT 解決方案開發人員</span><span class="sxs-lookup"><span data-stu-id="1fccc-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="1fccc-144">IoT 解決方案部署人員</span><span class="sxs-lookup"><span data-stu-id="1fccc-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="1fccc-145">IoT 解決方案操作人員</span><span class="sxs-lookup"><span data-stu-id="1fccc-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
