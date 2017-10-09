---
title: "在 Azure 資訊安全中心 aaaPermissions |Microsoft 文件"
description: "這篇文章說明 Azure 資訊安全中心如何使用角色型存取控制 tooassign 權限 toousers 並找出 hello 允許每個角色的動作。"
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
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="26f8c-103">Azure 資訊安全中心的權限</span><span class="sxs-lookup"><span data-stu-id="26f8c-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="26f8c-104">使用 azure 資訊安全中心[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)，這樣會提供[內建角色](../active-directory/role-based-access-built-in-roles.md)toousers、 群組和服務在 Azure 中的可獲指派。</span><span class="sxs-lookup"><span data-stu-id="26f8c-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="26f8c-105">資訊安全中心會評估 hello 和組態都資源 tooidentify 安全性問題的弱點。</span><span class="sxs-lookup"><span data-stu-id="26f8c-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="26f8c-106">資訊安全中心，因此您只看到資訊相關 tooa 資源時指派資源所屬的 hello 訂用帳戶或資源群組的擁有者、 參與者或讀取器 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="26f8c-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="26f8c-107">在加法 toothese 角色中，有兩個特定的資訊安全中心角色：</span><span class="sxs-lookup"><span data-stu-id="26f8c-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="26f8c-108">**安全性讀取器**： 使用者所屬 toothis 角色有檢視權限 tooSecurity 中心。</span><span class="sxs-lookup"><span data-stu-id="26f8c-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="26f8c-109">hello 使用者可以檢視建議、 警示、 安全性原則，以及安全性狀態，但無法進行變更。</span><span class="sxs-lookup"><span data-stu-id="26f8c-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="26f8c-110">**安全性系統管理員**： 使用者所屬 toothis 角色具有相同權限為 hello 安全性讀取器的 hello 和也更新 hello 安全性原則及關閉警示和建議。</span><span class="sxs-lookup"><span data-stu-id="26f8c-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="26f8c-111">hello 的安全性角色，安全讀取器和安全性系統管理員，可以存取只有在資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="26f8c-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="26f8c-112">hello 安全性角色沒有存取 tooother 服務區域的 Azure 儲存體、 Web 和行動裝置、 或物聯網等。</span><span class="sxs-lookup"><span data-stu-id="26f8c-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="26f8c-113">角色和允許的動作</span><span class="sxs-lookup"><span data-stu-id="26f8c-113">Roles and allowed actions</span></span>

<span data-ttu-id="26f8c-114">hello 下表顯示角色，並允許資訊安全中心中的動作。</span><span class="sxs-lookup"><span data-stu-id="26f8c-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="26f8c-115">X 表示該角色允許 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="26f8c-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="26f8c-116">角色</span><span class="sxs-lookup"><span data-stu-id="26f8c-116">Role</span></span> | <span data-ttu-id="26f8c-117">編輯安全性原則</span><span class="sxs-lookup"><span data-stu-id="26f8c-117">Edit security policy</span></span> | <span data-ttu-id="26f8c-118">針對資源套用安全性建議</span><span class="sxs-lookup"><span data-stu-id="26f8c-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="26f8c-119">關閉警示和建議</span><span class="sxs-lookup"><span data-stu-id="26f8c-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="26f8c-120">檢視警示和建議</span><span class="sxs-lookup"><span data-stu-id="26f8c-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="26f8c-121">訂用帳戶擁有者</span><span class="sxs-lookup"><span data-stu-id="26f8c-121">Subscription Owner</span></span> | <span data-ttu-id="26f8c-122">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-122">X</span></span> | <span data-ttu-id="26f8c-123">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-123">X</span></span> | <span data-ttu-id="26f8c-124">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-124">X</span></span> | <span data-ttu-id="26f8c-125">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-125">X</span></span> |
| <span data-ttu-id="26f8c-126">訂用帳戶參與者</span><span class="sxs-lookup"><span data-stu-id="26f8c-126">Subscription Contributor</span></span> | <span data-ttu-id="26f8c-127">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-127">X</span></span> | <span data-ttu-id="26f8c-128">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-128">X</span></span> | <span data-ttu-id="26f8c-129">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-129">X</span></span> | <span data-ttu-id="26f8c-130">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-130">X</span></span> |
| <span data-ttu-id="26f8c-131">資源群組擁有者</span><span class="sxs-lookup"><span data-stu-id="26f8c-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="26f8c-132">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-132">X</span></span> | -- | <span data-ttu-id="26f8c-133">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-133">X</span></span> |
| <span data-ttu-id="26f8c-134">資源群組參與者</span><span class="sxs-lookup"><span data-stu-id="26f8c-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="26f8c-135">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-135">X</span></span> | -- | <span data-ttu-id="26f8c-136">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-136">X</span></span> |
| <span data-ttu-id="26f8c-137">讀取者</span><span class="sxs-lookup"><span data-stu-id="26f8c-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="26f8c-138">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-138">X</span></span> |
| <span data-ttu-id="26f8c-139">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="26f8c-139">Security Administrator</span></span> | <span data-ttu-id="26f8c-140">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-140">X</span></span> | -- | <span data-ttu-id="26f8c-141">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-141">X</span></span> | <span data-ttu-id="26f8c-142">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-142">X</span></span> |
| <span data-ttu-id="26f8c-143">安全性讀取者</span><span class="sxs-lookup"><span data-stu-id="26f8c-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="26f8c-144">X</span><span class="sxs-lookup"><span data-stu-id="26f8c-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="26f8c-145">我們建議您將指派 hello 最寬鬆的角色所需的使用者 toocomplete 其工作。</span><span class="sxs-lookup"><span data-stu-id="26f8c-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="26f8c-146">例如，指派 hello 讀取器角色 toousers 者只需要 tooview hello 安全性健全狀況的資訊資源，但未採取任何動作，例如套用建議，或編輯原則。</span><span class="sxs-lookup"><span data-stu-id="26f8c-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="26f8c-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26f8c-147">Next steps</span></span>
<span data-ttu-id="26f8c-148">這篇文章說明如何資訊安全中心使用 RBAC tooassign 權限 toousers，並識別 hello 允許每個角色的動作。</span><span class="sxs-lookup"><span data-stu-id="26f8c-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="26f8c-149">既然您已熟悉 hello 角色指派所需 toomonitor hello 的訂用帳戶的安全性狀態，編輯安全性原則，並套用建議，了解如何：</span><span class="sxs-lookup"><span data-stu-id="26f8c-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="26f8c-150">在資訊安全中心設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="26f8c-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="26f8c-151">管理資訊安全中心的安全性建議</span><span class="sxs-lookup"><span data-stu-id="26f8c-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="26f8c-152">監視您的 Azure 資源 hello 安全性健全狀況</span><span class="sxs-lookup"><span data-stu-id="26f8c-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="26f8c-153">管理及回應 toosecurity 警示資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="26f8c-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="26f8c-154">監視合作夥伴安全性解決方案</span><span class="sxs-lookup"><span data-stu-id="26f8c-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
