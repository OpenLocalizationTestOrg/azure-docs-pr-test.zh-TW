---
title: "aaaMicrosoft Azure 堆疊開發套件架構 |Microsoft 文件"
description: "檢視 hello Microsoft Azure 堆疊開發套件架構。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: helaw
ms.openlocfilehash: 32a19ced7ddd57b97ba796679c116132090402e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a><span data-ttu-id="75117-103">Microsoft Azure Stack 開發套件架構</span><span class="sxs-lookup"><span data-stu-id="75117-103">Microsoft Azure Stack Development Kit architecture</span></span>
<span data-ttu-id="75117-104">hello Azure 堆疊開發套件是單一節點部署 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="75117-104">hello Azure Stack Development Kit is a single-node deployment of Azure Stack.</span></span> <span data-ttu-id="75117-105">所有的 hello 元件會安裝在單一主機電腦上執行的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="75117-105">All hello components are installed in virtual machines running on a single host machine.</span></span> 

## <a name="logical-architecture-diagram"></a><span data-ttu-id="75117-106">邏輯架構圖</span><span class="sxs-lookup"><span data-stu-id="75117-106">Logical architecture diagram</span></span>
<span data-ttu-id="75117-107">hello 下列圖表說明 hello hello Azure 堆疊開發套件和其元件的邏輯架構。</span><span class="sxs-lookup"><span data-stu-id="75117-107">hello following diagram illustrates hello logical architecture of hello Azure Stack development kit and its components.</span></span>

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a><span data-ttu-id="75117-108">虛擬機器角色</span><span class="sxs-lookup"><span data-stu-id="75117-108">Virtual machine roles</span></span>
<span data-ttu-id="75117-109">hello Azure 堆疊開發套件提供使用 hello 遵循 hello 主機上 Vm 的服務：</span><span class="sxs-lookup"><span data-stu-id="75117-109">hello Azure Stack development kit offers services using hello following VMs on hello host:</span></span>

| <span data-ttu-id="75117-110">名稱</span><span class="sxs-lookup"><span data-stu-id="75117-110">Name</span></span> | <span data-ttu-id="75117-111">說明</span><span class="sxs-lookup"><span data-stu-id="75117-111">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="75117-112">**AzS-ACS01**</span><span class="sxs-lookup"><span data-stu-id="75117-112">**AzS-ACS01**</span></span> | <span data-ttu-id="75117-113">Azure Stack 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="75117-113">Azure Stack storage services.</span></span>|
| <span data-ttu-id="75117-114">**AzS-ADFS01**</span><span class="sxs-lookup"><span data-stu-id="75117-114">**AzS-ADFS01**</span></span> | <span data-ttu-id="75117-115">Active Directory 同盟服務 (AD FS)。</span><span class="sxs-lookup"><span data-stu-id="75117-115">Active Directory Federation Services (ADFS).</span></span>  |
| <span data-ttu-id="75117-116">**AzS-BGPNAT01**</span><span class="sxs-lookup"><span data-stu-id="75117-116">**AzS-BGPNAT01**</span></span> | <span data-ttu-id="75117-117">邊緣路由器，並提供適用於 Azure Stack 的 NAT 和 VPN 功能。</span><span class="sxs-lookup"><span data-stu-id="75117-117">Edge router and provides NAT and VPN capabilities for Azure Stack.</span></span> |
| <span data-ttu-id="75117-118">**AzS-CA01**</span><span class="sxs-lookup"><span data-stu-id="75117-118">**AzS-CA01**</span></span> | <span data-ttu-id="75117-119">適用於 Azure Stack 角色服務的憑證授權單位服務。</span><span class="sxs-lookup"><span data-stu-id="75117-119">Certificate authority services for Azure Stack role services.</span></span>|
| <span data-ttu-id="75117-120">**AzS-DC01**</span><span class="sxs-lookup"><span data-stu-id="75117-120">**AzS-DC01**</span></span> | <span data-ttu-id="75117-121">適用於 Microsoft Azure Stack 的 Active Directory、DNS 及 DHCP 服務。</span><span class="sxs-lookup"><span data-stu-id="75117-121">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span></span>|
| <span data-ttu-id="75117-122">**AzS-ERCS01**</span><span class="sxs-lookup"><span data-stu-id="75117-122">**AzS-ERCS01**</span></span> | <span data-ttu-id="75117-123">緊急修復主控台 VM。</span><span class="sxs-lookup"><span data-stu-id="75117-123">Emergency Recovery Console VM.</span></span> |
| <span data-ttu-id="75117-124">**AzS-GWY01**</span><span class="sxs-lookup"><span data-stu-id="75117-124">**AzS-GWY01**</span></span> | <span data-ttu-id="75117-125">邊緣閘道服務，例如適用於租用戶網路的 VPN 站對站連線。</span><span class="sxs-lookup"><span data-stu-id="75117-125">Edge gateway services such as VPN site-to-site connections for tenant networks.</span></span>|
| <span data-ttu-id="75117-126">**AzS-NC01**</span><span class="sxs-lookup"><span data-stu-id="75117-126">**AzS-NC01**</span></span> | <span data-ttu-id="75117-127">管理 Azure Stack 網路服務的網路控制器。</span><span class="sxs-lookup"><span data-stu-id="75117-127">Network Controller, which manages Azure Stack network services.</span></span>  |
| <span data-ttu-id="75117-128">**AzS-SLB01**</span><span class="sxs-lookup"><span data-stu-id="75117-128">**AzS-SLB01**</span></span> | <span data-ttu-id="75117-129">Azure Stack 中適用於租用戶和 Azure Stack 基礎結構服務的負載平衡多工器服務。</span><span class="sxs-lookup"><span data-stu-id="75117-129">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span></span>  |
| <span data-ttu-id="75117-130">**AzS-SQL01**</span><span class="sxs-lookup"><span data-stu-id="75117-130">**AzS-SQL01**</span></span> | <span data-ttu-id="75117-131">適用於 Azure Stack 基礎結構角色的內部資料存放區。</span><span class="sxs-lookup"><span data-stu-id="75117-131">Internal data store for Azure Stack infrastructure roles.</span></span>  |
| <span data-ttu-id="75117-132">**AzS-WAS01**</span><span class="sxs-lookup"><span data-stu-id="75117-132">**AzS-WAS01**</span></span> | <span data-ttu-id="75117-133">Azure Stack 管理入口網站和 Azure Resource Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="75117-133">Azure Stack administrative portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="75117-134">**AzS-WASP01**</span><span class="sxs-lookup"><span data-stu-id="75117-134">**AzS-WASP01**</span></span>| <span data-ttu-id="75117-135">Azure Stack 使用者 (租用戶) 入口網站和 Azure Resource Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="75117-135">Azure Stack user (tenant) portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="75117-136">**AzS-XRP01**</span><span class="sxs-lookup"><span data-stu-id="75117-136">**AzS-XRP01**</span></span> | <span data-ttu-id="75117-137">Microsoft Azure 堆疊，包括 hello 運算、 網路和儲存體資源提供者的基礎結構管理控制器。</span><span class="sxs-lookup"><span data-stu-id="75117-137">Infrastructure management controller for Microsoft Azure Stack, including hello Compute, Network, and Storage resource providers.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="75117-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75117-138">Next steps</span></span>
[<span data-ttu-id="75117-139">部署 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="75117-139">Deploy Azure Stack</span></span>](azure-stack-deploy.md)

[<span data-ttu-id="75117-140">第一個案例 tootry</span><span class="sxs-lookup"><span data-stu-id="75117-140">First scenarios tootry</span></span>](azure-stack-first-scenarios.md)

