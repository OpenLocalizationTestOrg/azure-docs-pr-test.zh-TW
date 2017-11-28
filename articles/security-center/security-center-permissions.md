---
title: "Azure 資訊安全中心的權限 | Microsoft Docs"
description: "本文說明 Azure 資訊安全中心如何使用角色型存取控制，將權限指派給使用者，並識別每個角色允許的動作。"
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="82349-103">Azure 資訊安全中心的權限</span><span class="sxs-lookup"><span data-stu-id="82349-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="82349-104">Azure 資訊安全中心會使用[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)，以提供可在 Azure 中指派給使用者、群組與服務的[內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="82349-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="82349-105">資訊安全中心會評估資源的組態，以識別安全性問題與弱點。</span><span class="sxs-lookup"><span data-stu-id="82349-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="82349-106">在「資訊安全中心」中，當您獲指派為資源所屬的訂用帳戶或資源群組「擁有者」、「參與者」或「讀取者」角色時，您只會看到與資源相關的項目。</span><span class="sxs-lookup"><span data-stu-id="82349-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="82349-107">除了這些角色，有兩個特定的資訊安全中心角色：</span><span class="sxs-lookup"><span data-stu-id="82349-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="82349-108">**安全性讀取者**：屬於此角色的使用者有檢視資訊安全中心的權限。</span><span class="sxs-lookup"><span data-stu-id="82349-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="82349-109">使用者可以檢視建議、警示、安全性原則和安全性狀態，但無法進行變更。</span><span class="sxs-lookup"><span data-stu-id="82349-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="82349-110">**安全性系統管理員**：屬於此角色的使用者和「安全性讀取者」有相同的權限，而且還能更新安全性原則，以及解除警示和建議。</span><span class="sxs-lookup"><span data-stu-id="82349-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="82349-111">安全性角色 (安全讀取者和安全性系統管理員) 只在資訊安全中心內有存取權。</span><span class="sxs-lookup"><span data-stu-id="82349-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="82349-112">上述安全性角色無法存取 Azure 的其他服務區域，例如儲存體、Web 和行動或物聯網。</span><span class="sxs-lookup"><span data-stu-id="82349-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="82349-113">角色和允許的動作</span><span class="sxs-lookup"><span data-stu-id="82349-113">Roles and allowed actions</span></span>

<span data-ttu-id="82349-114">下表會顯示資訊安全中心的角色和允許的動作。</span><span class="sxs-lookup"><span data-stu-id="82349-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="82349-115">X 表示該角色允許的動作。</span><span class="sxs-lookup"><span data-stu-id="82349-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="82349-116">角色</span><span class="sxs-lookup"><span data-stu-id="82349-116">Role</span></span> | <span data-ttu-id="82349-117">編輯安全性原則</span><span class="sxs-lookup"><span data-stu-id="82349-117">Edit security policy</span></span> | <span data-ttu-id="82349-118">針對資源套用安全性建議</span><span class="sxs-lookup"><span data-stu-id="82349-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="82349-119">關閉警示和建議</span><span class="sxs-lookup"><span data-stu-id="82349-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="82349-120">檢視警示和建議</span><span class="sxs-lookup"><span data-stu-id="82349-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="82349-121">訂用帳戶擁有者</span><span class="sxs-lookup"><span data-stu-id="82349-121">Subscription Owner</span></span> | <span data-ttu-id="82349-122">X</span><span class="sxs-lookup"><span data-stu-id="82349-122">X</span></span> | <span data-ttu-id="82349-123">X</span><span class="sxs-lookup"><span data-stu-id="82349-123">X</span></span> | <span data-ttu-id="82349-124">X</span><span class="sxs-lookup"><span data-stu-id="82349-124">X</span></span> | <span data-ttu-id="82349-125">X</span><span class="sxs-lookup"><span data-stu-id="82349-125">X</span></span> |
| <span data-ttu-id="82349-126">訂用帳戶參與者</span><span class="sxs-lookup"><span data-stu-id="82349-126">Subscription Contributor</span></span> | <span data-ttu-id="82349-127">X</span><span class="sxs-lookup"><span data-stu-id="82349-127">X</span></span> | <span data-ttu-id="82349-128">X</span><span class="sxs-lookup"><span data-stu-id="82349-128">X</span></span> | <span data-ttu-id="82349-129">X</span><span class="sxs-lookup"><span data-stu-id="82349-129">X</span></span> | <span data-ttu-id="82349-130">X</span><span class="sxs-lookup"><span data-stu-id="82349-130">X</span></span> |
| <span data-ttu-id="82349-131">資源群組擁有者</span><span class="sxs-lookup"><span data-stu-id="82349-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="82349-132">X</span><span class="sxs-lookup"><span data-stu-id="82349-132">X</span></span> | -- | <span data-ttu-id="82349-133">X</span><span class="sxs-lookup"><span data-stu-id="82349-133">X</span></span> |
| <span data-ttu-id="82349-134">資源群組參與者</span><span class="sxs-lookup"><span data-stu-id="82349-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="82349-135">X</span><span class="sxs-lookup"><span data-stu-id="82349-135">X</span></span> | -- | <span data-ttu-id="82349-136">X</span><span class="sxs-lookup"><span data-stu-id="82349-136">X</span></span> |
| <span data-ttu-id="82349-137">讀取者</span><span class="sxs-lookup"><span data-stu-id="82349-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="82349-138">X</span><span class="sxs-lookup"><span data-stu-id="82349-138">X</span></span> |
| <span data-ttu-id="82349-139">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="82349-139">Security Administrator</span></span> | <span data-ttu-id="82349-140">X</span><span class="sxs-lookup"><span data-stu-id="82349-140">X</span></span> | -- | <span data-ttu-id="82349-141">X</span><span class="sxs-lookup"><span data-stu-id="82349-141">X</span></span> | <span data-ttu-id="82349-142">X</span><span class="sxs-lookup"><span data-stu-id="82349-142">X</span></span> |
| <span data-ttu-id="82349-143">安全性讀取者</span><span class="sxs-lookup"><span data-stu-id="82349-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="82349-144">X</span><span class="sxs-lookup"><span data-stu-id="82349-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="82349-145">我們建議您指派所需的最寬鬆角色，以便使用者完成其工作。</span><span class="sxs-lookup"><span data-stu-id="82349-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="82349-146">例如，將「讀取者」角色指派給只需要檢視資源安全性狀態的相關資訊，但不採取行動的使用者，例如套用建議或編輯原則。</span><span class="sxs-lookup"><span data-stu-id="82349-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="82349-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82349-147">Next steps</span></span>
<span data-ttu-id="82349-148">本文說明資訊安全中心如何使用 RBAC，將權限指派給使用者，並識別每個角色允許的動作。</span><span class="sxs-lookup"><span data-stu-id="82349-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="82349-149">現在，您已熟悉監視您的訂用帳戶的安全性狀態所需的角色指派，編輯安全性原則和套用建議，接著了解如何︰</span><span class="sxs-lookup"><span data-stu-id="82349-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="82349-150">在資訊安全中心設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="82349-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="82349-151">管理資訊安全中心的安全性建議</span><span class="sxs-lookup"><span data-stu-id="82349-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="82349-152">監視您的 Azure 資源的安全性健全狀況</span><span class="sxs-lookup"><span data-stu-id="82349-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="82349-153">在資訊安全中心管理和回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="82349-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="82349-154">監視合作夥伴安全性解決方案</span><span class="sxs-lookup"><span data-stu-id="82349-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
