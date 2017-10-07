---
title: "aaaAzure 容器執行個體概觀 |Azure 文件"
description: "了解 Azure Container Instances"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="024be-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="024be-103">Azure Container Instances</span></span>

<span data-ttu-id="024be-104">容器快速成為 hello 慣用方式 toopackage、 部署及管理雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="024be-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="024be-105">Azure 容器執行個體提供最快的 hello 和最簡單方式 toorun 容器在 Azure 中，而不需要 tooprovision 任何虛擬機器，而不需要 tooadopt 較高層級的服務。</span><span class="sxs-lookup"><span data-stu-id="024be-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="024be-106">對於可在隔離容器中運作的任何情節，包括簡單的應用程式、工作自動化及建置工作，Azure Container Instances 是很棒的解決方案。</span><span class="sxs-lookup"><span data-stu-id="024be-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="024be-107">您需要在此完整容器協調流程，包括跨多個容器、 自動縮放功能，以及協調應用程式升級，服務探索的案例中，我們建議 hello [Azure 容器服務](https://docs.microsoft.com/azure/container-service/)。</span><span class="sxs-lookup"><span data-stu-id="024be-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="024be-108">快速啟動時間</span><span class="sxs-lookup"><span data-stu-id="024be-108">Fast startup times</span></span>

<span data-ttu-id="024be-109">容器提供比虛擬機器更多的啟動優點。</span><span class="sxs-lookup"><span data-stu-id="024be-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="024be-110">Azure 容器執行個體中，您可以在 Azure 中啟動容器，以秒為單位，而不 hello 需要 tooprovision 並管理 Vm。</span><span class="sxs-lookup"><span data-stu-id="024be-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="024be-111">Hypervisor 等級安全性</span><span class="sxs-lookup"><span data-stu-id="024be-111">Hypervisor-level security</span></span>

<span data-ttu-id="024be-112">在過去，雖然容器提供應用程式相依性隔離和資源控管，但並沒有足夠的能力防範惡意的多租用戶使用方式。</span><span class="sxs-lookup"><span data-stu-id="024be-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="024be-113">Azure Container Instances 可以將您的應用程式隔離在容器中，就像在 VM 中一樣。</span><span class="sxs-lookup"><span data-stu-id="024be-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="024be-114">自訂大小</span><span class="sxs-lookup"><span data-stu-id="024be-114">Custom sizes</span></span>

<span data-ttu-id="024be-115">容器是通常最佳化的 toorun 只是單一的應用程式，而 hello 的特定需求，這些應用程式可以有明顯的差異。</span><span class="sxs-lookup"><span data-stu-id="024be-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="024be-116">Azure Container Instances 可讓您要求剛好符合所需的 CPU 核心和記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="024be-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="024be-117">您必須支付根據要求什麼方法，計費由 hello 秒，讓您精密地可以將您的需求為基礎的費用。</span><span class="sxs-lookup"><span data-stu-id="024be-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="024be-118">公用 IP 連線能力</span><span class="sxs-lookup"><span data-stu-id="024be-118">Public IP connectivity</span></span>

<span data-ttu-id="024be-119">Azure 容器執行個體中，您可以將您的容器公開直接 toohello 網際網路的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="024be-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="024be-120">在未來的 hello，我們將會展開我們網路功能 tooinclude 與虛擬網路整合、 負載平衡器、 與 hello Azure 網路基礎結構的其他核心部分。</span><span class="sxs-lookup"><span data-stu-id="024be-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="024be-121">永續性儲存體</span><span class="sxs-lookup"><span data-stu-id="024be-121">Persistent storage</span></span>

<span data-ttu-id="024be-122">tooretrieve 和保存 Azure 容器執行個體的狀態，因此我們提供的 Azure 直接掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="024be-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="024be-123">Linux 和 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="024be-123">Linux and Windows containers</span></span>

<span data-ttu-id="024be-124">Azure 容器執行個體中，您可以排程 Windows 和 Linux 容器與 hello 相同的 API。</span><span class="sxs-lookup"><span data-stu-id="024be-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="024be-125">只會表示都有相同基底 OS 類型 hello 和其他項目。</span><span class="sxs-lookup"><span data-stu-id="024be-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="024be-126">共同排程的群組</span><span class="sxs-lookup"><span data-stu-id="024be-126">Co-scheduled groups</span></span>

<span data-ttu-id="024be-127">Azure Container Instances 支援排程多個共用主機、區域網路、儲存體和生命週期的容器群組。</span><span class="sxs-lookup"><span data-stu-id="024be-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="024be-128">這可讓您 toocombine 主應用程式與其他人扮演支援的角色，例如記錄。</span><span class="sxs-lookup"><span data-stu-id="024be-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="024be-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="024be-129">Next steps</span></span>

<span data-ttu-id="024be-130">嘗試部署與單一命令，使用容器 tooAzure 我們[快速入門指南](container-instances-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="024be-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
