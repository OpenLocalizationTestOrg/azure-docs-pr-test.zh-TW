---
title: "在 Azure 中的 Linux Vm 的 aaaResource 群組 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作指導方針在 Azure 基礎結構服務中部署資源群組。"
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
ms.openlocfilehash: 8809cb5eeb9a166d2bcf1946cd26b0ee748f8cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a><span data-ttu-id="8ead1-103">適用於 Linux VM 的 Azure 資源群組指導方針</span><span class="sxs-lookup"><span data-stu-id="8ead1-103">Azure resource group guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="8ead1-104">本文著重在了解如何 toologically 建置您的環境和所有資源群組中的 hello 元件都群組。</span><span class="sxs-lookup"><span data-stu-id="8ead1-104">This article focuses on understanding how toologically build out your environment and group all hello components in Resource Groups.</span></span>

## <a name="implementation-guidelines-for-resource-groups"></a><span data-ttu-id="8ead1-105">資源群組的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="8ead1-105">Implementation guidelines for Resource Groups</span></span>
<span data-ttu-id="8ead1-106">决策：</span><span class="sxs-lookup"><span data-stu-id="8ead1-106">Decisions:</span></span>

* <span data-ttu-id="8ead1-107">要何種 toobuild 出資源群組由 hello 核心基礎結構元件，或完整的應用程式部署嗎？</span><span class="sxs-lookup"><span data-stu-id="8ead1-107">Are you going toobuild out Resource Groups by hello core infrastructure components, or by complete application deployment?</span></span>
* <span data-ttu-id="8ead1-108">您需要 toorestrict 存取 tooResource 群組使用角色型存取控制？</span><span class="sxs-lookup"><span data-stu-id="8ead1-108">Do you need toorestrict access tooResource Groups using Role-Based Access Controls?</span></span>

<span data-ttu-id="8ead1-109">工作：</span><span class="sxs-lookup"><span data-stu-id="8ead1-109">Tasks:</span></span>

* <span data-ttu-id="8ead1-110">定義核心基礎結構元件，以及您所需的專屬資源群組。</span><span class="sxs-lookup"><span data-stu-id="8ead1-110">Define what core infrastructure components and dedicated Resource Groups you need.</span></span>
* <span data-ttu-id="8ead1-111">檢閱如何將資源管理員範本 tooimplement 一致、 可重現的部署。</span><span class="sxs-lookup"><span data-stu-id="8ead1-111">Review how tooimplement Resource Manager templates for consistent, reproducible deployments.</span></span>
* <span data-ttu-id="8ead1-112">如需可控制哪些使用者存取角色存取 tooResource 群組的定義。</span><span class="sxs-lookup"><span data-stu-id="8ead1-112">Define what user access roles you need for controlling access tooResource Groups.</span></span>
* <span data-ttu-id="8ead1-113">建立資源群組使用您的命名慣例 hello 組。</span><span class="sxs-lookup"><span data-stu-id="8ead1-113">Create hello set of Resource Groups using your naming convention.</span></span> <span data-ttu-id="8ead1-114">您可以使用 Azure CLI hello 或入口網站。</span><span class="sxs-lookup"><span data-stu-id="8ead1-114">You can use hello Azure CLI or portal.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="8ead1-115">資源群組</span><span class="sxs-lookup"><span data-stu-id="8ead1-115">Resource Groups</span></span>
<span data-ttu-id="8ead1-116">在 Azure 中，您以邏輯方式群組相關的資源，例如儲存體帳戶、 虛擬網路以及虛擬機器 (Vm) toodeploy、 管理和維護它們當做單一實體。</span><span class="sxs-lookup"><span data-stu-id="8ead1-116">In Azure, you logically group related resources such as storage accounts, virtual networks, and virtual machines (VMs) toodeploy, manage, and maintain them as a single entity.</span></span> <span data-ttu-id="8ead1-117">這個方法可讓它更容易 toodeploy 應用程式時保留所有 hello 相關聯的資源一起從管理的觀點來看或 toogrant 其他人存取 toothat 群組的資源。</span><span class="sxs-lookup"><span data-stu-id="8ead1-117">This approach makes it easier toodeploy applications while keeping all hello related resources together from a management perspective, or toogrant others access toothat group of resources.</span></span> <span data-ttu-id="8ead1-118">資源群組名稱長度最多可以有 90 個字元。</span><span class="sxs-lookup"><span data-stu-id="8ead1-118">Resource group names can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="8ead1-119">資源群組的更完整了解，您可以參閱 hello [Azure 資源管理員概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8ead1-119">For a more comprehensive understanding of Resource Groups, you can read hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="8ead1-120">TooResource 群組是一項重要功能 hello 能力 toobuild 使用 JSON 檔案宣告 hello 儲存體、 網路、 環境和運算資源。</span><span class="sxs-lookup"><span data-stu-id="8ead1-120">A key feature tooResource Groups is hello ability toobuild your environment using a JSON file that declares hello storage, networking, and compute resources.</span></span> <span data-ttu-id="8ead1-121">您也可以定義任何相關的自訂指令碼或組態 tooapply。</span><span class="sxs-lookup"><span data-stu-id="8ead1-121">You can also define any related custom scripts or configurations tooapply.</span></span> <span data-ttu-id="8ead1-122">透過使用這些 JSON 範本，您可以為應用程式建立一致且可重現的部署。</span><span class="sxs-lookup"><span data-stu-id="8ead1-122">By using these JSON templates, you create consistent, reproducible deployments for your applications.</span></span> <span data-ttu-id="8ead1-123">這種方法可讓您建置在開發環境，然後使用該相同的範本 toocreate 生產部署，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="8ead1-123">This approach lets you build an environment in development and then use that same template toocreate a production deployment, or vice versa.</span></span> <span data-ttu-id="8ead1-124">進一步了解有關使用範本，讀取[hello 範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)，引導您完成建置出 JSON 範本的每個步驟。</span><span class="sxs-lookup"><span data-stu-id="8ead1-124">For a better understanding about using templates, read [hello template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) that guides you through each step of building out a JSON template.</span></span>

<span data-ttu-id="8ead1-125">您在使用資源群組設計環境時，有兩種不同的執行方式：</span><span class="sxs-lookup"><span data-stu-id="8ead1-125">There are two different approaches you can take when designing your environment with Resource Groups:</span></span>

* <span data-ttu-id="8ead1-126">資源群組結合了 hello 儲存體帳戶、 虛擬網路和子網路的 Vm，每個應用程式部署的負載平衡器等。</span><span class="sxs-lookup"><span data-stu-id="8ead1-126">Resource Groups for each application deployment that combines hello storage accounts, virtual networks, and subnets, VMs, load balancers, etc.</span></span>
* <span data-ttu-id="8ead1-127">集中式資源群組，其中包含您的核心虛擬網路和子網路或儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ead1-127">Centralized Resource Groups that contain your core virtual networking and subnets or storage accounts.</span></span> <span data-ttu-id="8ead1-128">接著，您的應用程式會位於它們自己的資源群組中，其中只會包含 VM、負載平衡器、網路介面等項目。</span><span class="sxs-lookup"><span data-stu-id="8ead1-128">Your applications are then in their own Resource Groups that only contain VMs, load balancers, network interfaces, etc.</span></span>

<span data-ttu-id="8ead1-129">當您向外延展，建立您的虛擬網路的集中式的資源群組和子網路可讓您更輕鬆 toobuild 跨單位網路連線的混合式連線選項。</span><span class="sxs-lookup"><span data-stu-id="8ead1-129">As you scale out, creating centralized Resource Groups for your virtual networking and subnets makes it easier toobuild cross-premises network connections for hybrid connectivity options.</span></span> <span data-ttu-id="8ead1-130">hello 替代方法是針對每個應用程式 toohave 自己需要設定和維護的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8ead1-130">hello alternative approach is for each application toohave their own virtual network that requires configuration and maintenance.</span></span> <span data-ttu-id="8ead1-131">[角色型存取控制](../../active-directory/role-based-access-control-what-is.md)提供細微的方式 toocontrol 存取 tooResource 群組。</span><span class="sxs-lookup"><span data-stu-id="8ead1-131">[Role-Based Access Controls](../../active-directory/role-based-access-control-what-is.md) provide a granular way toocontrol access tooResource Groups.</span></span> <span data-ttu-id="8ead1-132">對於生產應用程式，您可以控制 hello 使用者可以存取這些資源，或 hello 核心基礎結構資源，您可以限制只有基礎結構工程師 toowork 它們。</span><span class="sxs-lookup"><span data-stu-id="8ead1-132">For production applications, you can control hello users that may access those resources, or for hello core infrastructure resources you can limit only infrastructure engineers toowork with them.</span></span> <span data-ttu-id="8ead1-133">您的應用程式擁有者只能有其資源群組和不 hello 核心 Azure 基礎結構，您的環境中存取 toohello 應用程式元件。</span><span class="sxs-lookup"><span data-stu-id="8ead1-133">Your application owners only have access toohello application components within their Resource Group and not hello core Azure infrastructure of your environment.</span></span> <span data-ttu-id="8ead1-134">當您設計您的環境，請考慮 hello 使用者需要存取 toohello 資源，並據此設計您的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8ead1-134">As you design your environment, consider hello users that require access toohello resources and design your Resource Groups accordingly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8ead1-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ead1-135">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

