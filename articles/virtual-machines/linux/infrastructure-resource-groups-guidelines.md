---
title: "Azure 中 Linux VM 的資源群組 | Microsoft Docs"
description: "了解適合用來在 Azure 基礎結構服務中部署資源群組的關鍵設計和實作指導方針。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 452acde571164a3ab4ce2dcccf99d2aed90361fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a><span data-ttu-id="c4f6f-103">適用於 Linux VM 的 Azure 資源群組指導方針</span><span class="sxs-lookup"><span data-stu-id="c4f6f-103">Azure resource group guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="c4f6f-104">本文著重於了解如何在資源群組中以邏輯方式建置環境，並將所有元件分組的方式。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-104">This article focuses on understanding how to logically build out your environment and group all the components in Resource Groups.</span></span>

## <a name="implementation-guidelines-for-resource-groups"></a><span data-ttu-id="c4f6f-105">資源群組的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="c4f6f-105">Implementation guidelines for Resource Groups</span></span>
<span data-ttu-id="c4f6f-106">决策：</span><span class="sxs-lookup"><span data-stu-id="c4f6f-106">Decisions:</span></span>

* <span data-ttu-id="c4f6f-107">您要以核心基礎結構元件建置資源群組，還是以完整的應用程式部署？</span><span class="sxs-lookup"><span data-stu-id="c4f6f-107">Are you going to build out Resource Groups by the core infrastructure components, or by complete application deployment?</span></span>
* <span data-ttu-id="c4f6f-108">您是否需要使用角色型存取控制來限制資源群組的存取？</span><span class="sxs-lookup"><span data-stu-id="c4f6f-108">Do you need to restrict access to Resource Groups using Role-Based Access Controls?</span></span>

<span data-ttu-id="c4f6f-109">工作：</span><span class="sxs-lookup"><span data-stu-id="c4f6f-109">Tasks:</span></span>

* <span data-ttu-id="c4f6f-110">定義核心基礎結構元件，以及您所需的專屬資源群組。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-110">Define what core infrastructure components and dedicated Resource Groups you need.</span></span>
* <span data-ttu-id="c4f6f-111">檢閱如何實作 Resource Manager 範本以取得一致且可重現的部署。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-111">Review how to implement Resource Manager templates for consistent, reproducible deployments.</span></span>
* <span data-ttu-id="c4f6f-112">定義針對控制資源群組存取所需的使用者存取角色。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-112">Define what user access roles you need for controlling access to Resource Groups.</span></span>
* <span data-ttu-id="c4f6f-113">使用您的命名慣例來建立資源群組組合。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-113">Create the set of Resource Groups using your naming convention.</span></span> <span data-ttu-id="c4f6f-114">您可以使用 Azure CLI 或入口網站。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-114">You can use the Azure CLI or portal.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="c4f6f-115">資源群組</span><span class="sxs-lookup"><span data-stu-id="c4f6f-115">Resource Groups</span></span>
<span data-ttu-id="c4f6f-116">在 Azure 中，您可以邏輯方式將相關資源 (例如儲存體帳戶、虛擬網路及虛擬機器 (VM)) 分組，以將它們當成單一實體進行部署、管理及維護。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-116">In Azure, you logically group related resources such as storage accounts, virtual networks, and virtual machines (VMs) to deploy, manage, and maintain them as a single entity.</span></span> <span data-ttu-id="c4f6f-117">從管理的角度來看，這個方式可讓您在將所有相關資源保持在一起的情況下，更輕鬆地部署應用程式，或是授與其他人存取該資源群組。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-117">This approach makes it easier to deploy applications while keeping all the related resources together from a management perspective, or to grant others access to that group of resources.</span></span> <span data-ttu-id="c4f6f-118">資源群組名稱長度最多可以有 90 個字元。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-118">Resource group names can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="c4f6f-119">如需針對資源群組取得更完整的了解，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-119">For a more comprehensive understanding of Resource Groups, you can read the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="c4f6f-120">資源群組的其中一個關鍵功能，是使用宣告儲存體、網路及計算資源的 JSON 檔案來建置環境的能力。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-120">A key feature to Resource Groups is the ability to build your environment using a JSON file that declares the storage, networking, and compute resources.</span></span> <span data-ttu-id="c4f6f-121">您也可以定義任何要套用的相關自訂指令碼或設定。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-121">You can also define any related custom scripts or configurations to apply.</span></span> <span data-ttu-id="c4f6f-122">透過使用這些 JSON 範本，您可以為應用程式建立一致且可重現的部署。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-122">By using these JSON templates, you create consistent, reproducible deployments for your applications.</span></span> <span data-ttu-id="c4f6f-123">這種方式讓您可以建置開發環境，然後使用相同的範本建立生產環境部署，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-123">This approach lets you build an environment in development and then use that same template to create a production deployment, or vice versa.</span></span> <span data-ttu-id="c4f6f-124">如需深入了解範本的使用方式，請參閱 [範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md) ，它將能引導您完成建置 JSON 範本的每個步驟。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-124">For a better understanding about using templates, read [the template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) that guides you through each step of building out a JSON template.</span></span>

<span data-ttu-id="c4f6f-125">您在使用資源群組設計環境時，有兩種不同的執行方式：</span><span class="sxs-lookup"><span data-stu-id="c4f6f-125">There are two different approaches you can take when designing your environment with Resource Groups:</span></span>

* <span data-ttu-id="c4f6f-126">適用於每個應用程式部署的資源群組，其中結合了儲存體帳戶、虛擬網路和子網路、VM、負載平衡器等項目。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-126">Resource Groups for each application deployment that combines the storage accounts, virtual networks, and subnets, VMs, load balancers, etc.</span></span>
* <span data-ttu-id="c4f6f-127">集中式資源群組，其中包含您的核心虛擬網路和子網路或儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-127">Centralized Resource Groups that contain your core virtual networking and subnets or storage accounts.</span></span> <span data-ttu-id="c4f6f-128">接著，您的應用程式會位於它們自己的資源群組中，其中只會包含 VM、負載平衡器、網路介面等項目。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-128">Your applications are then in their own Resource Groups that only contain VMs, load balancers, network interfaces, etc.</span></span>

<span data-ttu-id="c4f6f-129">隨著您相應放大，為虛擬網路和子網路建立集中式資源群組，將能讓您更輕鬆地為混合式連線能力選項建立跨單位網路連線。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-129">As you scale out, creating centralized Resource Groups for your virtual networking and subnets makes it easier to build cross-premises network connections for hybrid connectivity options.</span></span> <span data-ttu-id="c4f6f-130">另一個替代方式是讓每個應用程式自行擁有需要個別設定和維護的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-130">The alternative approach is for each application to have their own virtual network that requires configuration and maintenance.</span></span> <span data-ttu-id="c4f6f-131">[角色型存取控制](../../active-directory/role-based-access-control-what-is.md) 提供更細微的資源群組存取控制方法。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-131">[Role-Based Access Controls](../../active-directory/role-based-access-control-what-is.md) provide a granular way to control access to Resource Groups.</span></span> <span data-ttu-id="c4f6f-132">針對實際執行應用程式，您可以控制可以存取那些資源的使用者，或是針對核心基礎結構資源限制只有基礎結構工程師可以使用它們。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-132">For production applications, you can control the users that may access those resources, or for the core infrastructure resources you can limit only infrastructure engineers to work with them.</span></span> <span data-ttu-id="c4f6f-133">您的應用程式使用者只能存取他們資源群組內的應用程式元件，而非環境的核心 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-133">Your application owners only have access to the application components within their Resource Group and not the core Azure infrastructure of your environment.</span></span> <span data-ttu-id="c4f6f-134">當您設計環境時，請考慮需要存取資源的使用者，並據以設計您的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c4f6f-134">As you design your environment, consider the users that require access to the resources and design your Resource Groups accordingly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c4f6f-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4f6f-135">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

