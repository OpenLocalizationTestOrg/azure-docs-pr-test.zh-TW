---
title: "使用 RBAC 管理存取權與權限 - Azure RBAC | Microsoft Docs"
description: "在 Azure 入口網站中使用 Azure 角色型存取控制開始進行存取管理。 使用角色指派在您的目錄中指派權限。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 0462fe8ff75bdda397decb301c459795886e9e58
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-role-based-access-control-in-the-azure-portal"></a><span data-ttu-id="5c521-104">在 Azure 入口網站中開始使用角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="5c521-104">Get started with Role-Based Access Control in the Azure portal</span></span>
<span data-ttu-id="5c521-105">安全性導向公司應該將焦點放在提供員工所需的確切權限。</span><span class="sxs-lookup"><span data-stu-id="5c521-105">Security-oriented companies should focus on giving employees the exact permissions they need.</span></span> <span data-ttu-id="5c521-106">權限太多可能會讓帳戶暴露在攻擊者的威脅下。</span><span class="sxs-lookup"><span data-stu-id="5c521-106">Too many permissions can expose an account to attackers.</span></span> <span data-ttu-id="5c521-107">權限太少則會讓員工無法有效率地完成工作。</span><span class="sxs-lookup"><span data-stu-id="5c521-107">Too few permissions means that employees can't get their work done efficiently.</span></span> <span data-ttu-id="5c521-108">Azure「角色型存取控制」(RBAC) 可以為 Azure 提供更細緻的存取管理來協助解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="5c521-108">Azure Role-Based Access Control (RBAC) helps address this problem by offering fine-grained access management for Azure.</span></span>

<span data-ttu-id="5c521-109">RBAC 可讓您區隔小組內的職責，而僅授與使用者執行作業所需的存取權。</span><span class="sxs-lookup"><span data-stu-id="5c521-109">Using RBAC, you can segregate duties within your team and grant only the amount of access to users that they need to perform their jobs.</span></span> <span data-ttu-id="5c521-110">您可以不授與每個人 Azure 訂用帳戶或資源中無限制的權限，而是只允許執行特定的動作。</span><span class="sxs-lookup"><span data-stu-id="5c521-110">Instead of giving everybody unrestricted permissions in your Azure subscription or resources, you can allow only certain actions.</span></span> <span data-ttu-id="5c521-111">例如，使用 RBAC 讓一位員工管理某個訂用帳戶中的虛擬機器，而讓另一位員工管理相同訂用帳戶中的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5c521-111">For example, use RBAC to let one employee manage virtual machines in a subscription, while another can manage SQL databases within the same subscription.</span></span>

## <a name="basics-of-access-management-in-azure"></a><span data-ttu-id="5c521-112">Azure 存取權管理的基礎</span><span class="sxs-lookup"><span data-stu-id="5c521-112">Basics of access management in Azure</span></span>
<span data-ttu-id="5c521-113">每個 Azure 訂用帳戶都會與一個 Azure Active Directory (AD) 目錄相關聯。</span><span class="sxs-lookup"><span data-stu-id="5c521-113">Each Azure subscription is associated with one Azure Active Directory (AD) directory.</span></span> <span data-ttu-id="5c521-114">該目錄中的使用者、群組和應用程式可以管理 Azure 訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="5c521-114">Users, groups, and applications from that directory can manage resources in the Azure subscription.</span></span> <span data-ttu-id="5c521-115">請使用 Azure 入口網站、Azure 命令列工具或「Azure 管理」API 來指派這些存取權限。</span><span class="sxs-lookup"><span data-stu-id="5c521-115">Assign these access rights using the Azure portal, Azure command-line tools, and Azure Management APIs.</span></span>

<span data-ttu-id="5c521-116">您可以藉由在特定範圍將適當的 RBAC 角色指派給使用者、群組及應用程式，來授與存取權。</span><span class="sxs-lookup"><span data-stu-id="5c521-116">Grant access by assigning the appropriate RBAC role to users, groups, and applications at a certain scope.</span></span> <span data-ttu-id="5c521-117">角色指派的範圍可以是訂用帳戶、資源群組或單一資源。</span><span class="sxs-lookup"><span data-stu-id="5c521-117">The scope of a role assignment can be a subscription, a resource group, or a single resource.</span></span> <span data-ttu-id="5c521-118">在父範圍指派的角色也會授與其內含子系的存取權。</span><span class="sxs-lookup"><span data-stu-id="5c521-118">A role assigned at a parent scope also grants access to the children contained within it.</span></span> <span data-ttu-id="5c521-119">例如，具有資源群組存取權的使用者可以管理其內含的所有資源，例如網站、虛擬機器和子網路。</span><span class="sxs-lookup"><span data-stu-id="5c521-119">For example, a user with access to a resource group can manage all the resources it contains, like websites, virtual machines, and subnets.</span></span>

![Azure Active Directory 元素之間的關聯性 - 圖表](./media/role-based-access-control-what-is/rbac_aad.png)

<span data-ttu-id="5c521-121">您指派的 RBAC 角色，指定使用者、群組或應用程式可以在該範圍內管理的資源。</span><span class="sxs-lookup"><span data-stu-id="5c521-121">The RBAC role that you assign dictates what resources the user, group, or application can manage within that scope.</span></span>

## <a name="built-in-roles"></a><span data-ttu-id="5c521-122">內建角色</span><span class="sxs-lookup"><span data-stu-id="5c521-122">Built-in roles</span></span>
<span data-ttu-id="5c521-123">Azure RBAC 有適用於所有資源類型的三個基本角色：</span><span class="sxs-lookup"><span data-stu-id="5c521-123">Azure RBAC has three basic roles that apply to all resource types:</span></span>

* <span data-ttu-id="5c521-124">**擁有者** 具有所有資源的完整存取權，包括將存取權委派給其他人的權限。</span><span class="sxs-lookup"><span data-stu-id="5c521-124">**Owner** has full access to all resources including the right to delegate access to others.</span></span>
* <span data-ttu-id="5c521-125">**參與者** 可以建立和管理所有類型的 Azure 資源，但是不能將存取權授與其他人。</span><span class="sxs-lookup"><span data-stu-id="5c521-125">**Contributor** can create and manage all types of Azure resources but can’t grant access to others.</span></span>
* <span data-ttu-id="5c521-126">**讀者** 可以檢視現有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="5c521-126">**Reader** can view existing Azure resources.</span></span>

<span data-ttu-id="5c521-127">Azure 中其餘的 RBAC 角色可以管理特定 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="5c521-127">The rest of the RBAC roles in Azure allow management of specific Azure resources.</span></span> <span data-ttu-id="5c521-128">例如，「虛擬機器參與者」角色可讓使用者建立和管理虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5c521-128">For example, the Virtual Machine Contributor role allows the user to create and manage virtual machines.</span></span> <span data-ttu-id="5c521-129">但不會授予他們存取虛擬機器所連接的虛擬網路或子網路的存取權。</span><span class="sxs-lookup"><span data-stu-id="5c521-129">It does not give them access to the virtual network or the subnet that the virtual machine connects to.</span></span> 

<span data-ttu-id="5c521-130">[RBAC 內建角色](role-based-access-built-in-roles.md) 會列出 Azure 中可用的角色。</span><span class="sxs-lookup"><span data-stu-id="5c521-130">[RBAC built-in roles](role-based-access-built-in-roles.md) lists the roles available in Azure.</span></span> <span data-ttu-id="5c521-131">它會指定每個內建角色授與使用者的作業和範圍。</span><span class="sxs-lookup"><span data-stu-id="5c521-131">It specifies the operations and scope that each built-in role grants to users.</span></span> <span data-ttu-id="5c521-132">如果您想要定義自己的角色，獲得更進一步控制，請參閱如何建立 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="5c521-132">If you're looking to define your own roles for even more control, see how to build [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-hierarchy-and-access-inheritance"></a><span data-ttu-id="5c521-133">資源階層和存取繼承</span><span class="sxs-lookup"><span data-stu-id="5c521-133">Resource hierarchy and access inheritance</span></span>
* <span data-ttu-id="5c521-134">Azure 中的每個 **訂用帳戶** 只屬於一個目錄。</span><span class="sxs-lookup"><span data-stu-id="5c521-134">Each **subscription** in Azure belongs to only one directory.</span></span> <span data-ttu-id="5c521-135">(但每個目錄可以有多個訂用帳戶)。</span><span class="sxs-lookup"><span data-stu-id="5c521-135">(But each directory can have more than one subscription.)</span></span>
* <span data-ttu-id="5c521-136">每個 **資源群組** 只屬於一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c521-136">Each **resource group** belongs to only one subscription.</span></span>
* <span data-ttu-id="5c521-137">每個 **資源** 只屬於一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="5c521-137">Each **resource** belongs to only one resource group.</span></span>

<span data-ttu-id="5c521-138">您在父範圍授與的存取權會在子範圍繼承。</span><span class="sxs-lookup"><span data-stu-id="5c521-138">Access that you grant at parent scopes is inherited at child scopes.</span></span> <span data-ttu-id="5c521-139">例如：</span><span class="sxs-lookup"><span data-stu-id="5c521-139">For example:</span></span>

* <span data-ttu-id="5c521-140">您可將讀者角色指派給訂用帳戶範圍內的 Azure AD 群組。</span><span class="sxs-lookup"><span data-stu-id="5c521-140">You assign the Reader role to an Azure AD group at the subscription scope.</span></span> <span data-ttu-id="5c521-141">該群組的成員可以檢視訂用帳戶中的每個資源群組和資源。</span><span class="sxs-lookup"><span data-stu-id="5c521-141">The members of that group can view every resource group and resource in the subscription.</span></span>
* <span data-ttu-id="5c521-142">您可將參與者角色指派給資源群組範圍內的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c521-142">You assign the Contributor role to an application at the resource group scope.</span></span> <span data-ttu-id="5c521-143">它可以管理該資源群組中所有類型的資源，但是無法管理訂用帳戶中的其他資源群組。</span><span class="sxs-lookup"><span data-stu-id="5c521-143">It can manage resources of all types in that resource group, but not other resource groups in the subscription.</span></span>

## <a name="azure-rbac-vs-classic-subscription-administrators"></a><span data-ttu-id="5c521-144">Azure RBAC 與傳統訂用帳戶系統管理員</span><span class="sxs-lookup"><span data-stu-id="5c521-144">Azure RBAC vs. classic subscription administrators</span></span>
<span data-ttu-id="5c521-145">傳統訂用帳戶系統管理員和共同管理員具有 Azure 訂用帳戶的完整存取權。</span><span class="sxs-lookup"><span data-stu-id="5c521-145">Classic subscription administrators and co-admins have full access to the Azure subscription.</span></span> <span data-ttu-id="5c521-146">他們可以使用 [Azure 入口網站](https://portal.azure.com)搭配 Azure Resource Manager API，或是使用 [Azure 傳統入口網站](https://manage.windowsazure.com)和 Azure 傳統部署模型，來管理資源。</span><span class="sxs-lookup"><span data-stu-id="5c521-146">They can manage resources using the [Azure portal](https://portal.azure.com) with Azure Resource Manager APIs, or the [Azure classic portal](https://manage.windowsazure.com) and Azure classic deployment model.</span></span> <span data-ttu-id="5c521-147">在 RBAC 模型中，傳統系統管理員會獲指派訂用帳戶範圍的擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="5c521-147">In the RBAC model, classic administrators are assigned the Owner role at the subscription scope.</span></span>

<span data-ttu-id="5c521-148">只有 Azure 入口網站和新的 Azure Resource Manager API 支援 Azure RBAC。</span><span class="sxs-lookup"><span data-stu-id="5c521-148">Only the Azure portal and the new Azure Resource Manager APIs support Azure RBAC.</span></span> <span data-ttu-id="5c521-149">獲指派 RBAC 角色的使用者和應用程式無法使用傳統管理入口網站和 Azure 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5c521-149">Users and applications that are assigned RBAC roles cannot use the classic management portal and the Azure classic deployment model.</span></span>

## <a name="authorization-for-management-vs-data-operations"></a><span data-ttu-id="5c521-150">管理與資料作業的授權</span><span class="sxs-lookup"><span data-stu-id="5c521-150">Authorization for management vs. data operations</span></span>
<span data-ttu-id="5c521-151">Azure RBAC 僅支援在 Azure 入口網站和 Azure Resource Manager API 中的 Azure 資源管理作業。</span><span class="sxs-lookup"><span data-stu-id="5c521-151">Azure RBAC only supports management operations of the Azure resources in the Azure portal and Azure Resource Manager APIs.</span></span> <span data-ttu-id="5c521-152">它無法授權 Azure 資源的所有資料層級作業。</span><span class="sxs-lookup"><span data-stu-id="5c521-152">It cannot authorize all data level operations for Azure resources.</span></span> <span data-ttu-id="5c521-153">例如，您可以授權某個人管理「儲存體帳戶」，但無法授權他管理「儲存體帳戶」內的 blob 或資料表。</span><span class="sxs-lookup"><span data-stu-id="5c521-153">For example, you can authorize someone to manage Storage Accounts, but not to the blobs or tables within a Storage Account.</span></span> <span data-ttu-id="5c521-154">同樣地，可以管理 SQL Database，但無法管理其中的資料表。</span><span class="sxs-lookup"><span data-stu-id="5c521-154">Similarly, a SQL database can be managed, but not the tables within it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c521-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c521-155">Next Steps</span></span>
* <span data-ttu-id="5c521-156">在 Azure 入口網站中開始使用 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="5c521-156">Get started with [Role-Based Access Control in the Azure portal](role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="5c521-157">參閱 [RBAC 內建角色](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="5c521-157">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="5c521-158">定義您自己的 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="5c521-158">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
