---
title: "aaaHow Azure 訂用帳戶相關聯 Azure Active Directory |Microsoft 文件"
description: "登入 tooMicrosoft Azure 和相關的問題，例如 hello Azure 訂用帳戶與 Azure Active Directory 之間的關聯性。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a><span data-ttu-id="1aa0d-103">Azure 訂用帳戶如何與 Azure Active Directory 產生關聯</span><span class="sxs-lookup"><span data-stu-id="1aa0d-103">How Azure subscriptions are associated with Azure Active Directory</span></span>
<span data-ttu-id="1aa0d-104">本文涵蓋 hello Azure 訂用帳戶與 Azure Active Directory (Azure AD) 之間的關聯性的相關資訊及如何 tooadd 現有的訂用帳戶 tooyour Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-104">This article covers information about hello relationship between an Azure subscription and Azure Active Directory (Azure AD), and how tooadd an existing subscription tooyour Azure AD directory.</span></span>

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a><span data-ttu-id="1aa0d-105">您的 Azure 訂閱關聯性 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="1aa0d-105">Your Azure subscription's relationship tooAzure AD</span></span>
<span data-ttu-id="1aa0d-106">您的 Azure 訂用帳戶已與 Azure AD，表示其信任 hello directory tooauthenticate 使用者、 服務和裝置的信任關係。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-106">Your Azure subscription has a trust relationship with Azure AD, which means that it trusts hello directory tooauthenticate users, services, and devices.</span></span> <span data-ttu-id="1aa0d-107">多個訂閱可以信任 hello 相同的目錄，但每個訂閱只能信任一個目錄。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-107">Multiple subscriptions can trust hello same directory, but each subscription trusts only one directory.</span></span> 

<span data-ttu-id="1aa0d-108">hello 之間的信任關係的訂用帳戶的目錄是不同於它與其他資源 （網站、 資料庫等等） 的 Azure 中的 hello 關係。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-108">hello trust relationship that a subscription has with a directory is unlike hello relationship that it has with other resources in Azure (websites, databases, and so on).</span></span> <span data-ttu-id="1aa0d-109">如果訂閱已過期，存取 toohello hello 訂用帳戶相關聯的其他資源也會停止。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-109">If a subscription expires, access toohello other resources associated with hello subscription also stops.</span></span> <span data-ttu-id="1aa0d-110">Azure AD 目錄會保留在 Azure 中，但您可以將不同的訂用帳戶與該目錄產生關聯，並管理 hello 目錄使用 hello 新訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-110">But an Azure AD directory remains in Azure, and you can associate a different subscription with that directory and manage hello directory using hello new subscription.</span></span>

![訂用帳戶如何與圖表產生關聯](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

<span data-ttu-id="1aa0d-112">所有使用者都有會對他們進行驗證的單一主目錄，但是他它們也可以是其他目錄中的來賓。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-112">All users have a single home directory that authenticates them, but they can also be guests in other directories.</span></span> <span data-ttu-id="1aa0d-113">在 Azure AD 中，您可以看到其中您的使用者帳戶是成員或來賓 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-113">In Azure AD, you can see hello directories of which your user account is a member or guest.</span></span>

## <a name="azure-ad-and-cloud-service-subscriptions"></a><span data-ttu-id="1aa0d-114">Azure AD 和雲端服務訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1aa0d-114">Azure AD and cloud service subscriptions</span></span>
<span data-ttu-id="1aa0d-115">Azure AD 提供 hello 核心目錄和身分識別管理功能的支援大部分的 Microsoft 雲端服務，包括：</span><span class="sxs-lookup"><span data-stu-id="1aa0d-115">Azure AD provides hello core directory and identity management capabilities behind most of Microsoft’s cloud services, including:</span></span>

* <span data-ttu-id="1aa0d-116">Azure</span><span class="sxs-lookup"><span data-stu-id="1aa0d-116">Azure</span></span>
* <span data-ttu-id="1aa0d-117">Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="1aa0d-117">Microsoft Office 365</span></span>
* <span data-ttu-id="1aa0d-118">Microsoft Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="1aa0d-118">Microsoft Dynamics CRM Online</span></span>
* <span data-ttu-id="1aa0d-119">Microsoft Intune</span><span class="sxs-lookup"><span data-stu-id="1aa0d-119">Microsoft Intune</span></span>

<span data-ttu-id="1aa0d-120">當您註冊的任何這些 Microsoft 雲端服務，您會收到 hello 免費的 Azure AD 服務。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-120">You get hello Azure AD service free when you sign up for any of these Microsoft cloud services.</span></span> <span data-ttu-id="1aa0d-121">如果您想 tooadd 其他 Azure 訂用帳戶 tooan Azure AD 目錄，您必須登入 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-121">If you want tooadd an additional Azure subscription tooan Azure AD directory, you must be signed in with a Microsoft account.</span></span> <span data-ttu-id="1aa0d-122">如果您登入 tooAzure 的工作或學校帳戶，您無法加入 tooan 現有 Azure 訂用帳戶的目錄，因為您工作或學校帳戶，無法直接由 Azure 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-122">If you sign in tooAzure with a work or school account, you can't add an Azure subscription tooan existing directory because your work or school account can't be authenticated directly by Azure.</span></span> 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a><span data-ttu-id="1aa0d-123">tooadd 現有的訂用帳戶 tooyour Azure AD 目錄</span><span class="sxs-lookup"><span data-stu-id="1aa0d-123">tooadd an existing subscription tooyour Azure AD directory</span></span>
<span data-ttu-id="1aa0d-124">您必須使用這兩個 hello 目前的目錄中的 hello 與相關聯的訂用帳戶已存在的帳戶，登入，而且希望在 hello 目錄 tooadd 它。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-124">You must sign in with an account that exists in both hello current directory with which hello subscription is associated and in hello directory you want tooadd it to.</span></span> 

1. <span data-ttu-id="1aa0d-125">登入 toohello [Azure 帳戶中心](https://account.windowsazure.com/Home/Index)想 tootransfer 是 hello hello 訂用帳戶的帳戶管理員的擁有權的帳戶。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-125">Sign in toohello [Azure Account Center](https://account.windowsazure.com/Home/Index) with an account that is hello Account Administrator of hello subscription whose ownership you want tootransfer.</span></span>
2. <span data-ttu-id="1aa0d-126">請確定您想 toobe hello 訂用帳戶擁有者為目標的 hello 目錄中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-126">Ensure that hello user who you want toobe hello subscription owner is in hello targeted directory.</span></span>
3. <span data-ttu-id="1aa0d-127">按一下 [移轉訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-127">Click **Transfer subscription**.</span></span>
4. <span data-ttu-id="1aa0d-128">指定 hello 收件者。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-128">Specify hello recipient.</span></span> <span data-ttu-id="1aa0d-129">hello 收件者自動取得含有接受連結的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-129">hello recipient automatically gets an email with an acceptance link.</span></span>
5. <span data-ttu-id="1aa0d-130">hello 收件者按一下 hello 連結，並遵循 hello 指示，包括輸入其付款資訊。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-130">hello recipient clicks hello link and follows hello instructions, including entering their payment information.</span></span> <span data-ttu-id="1aa0d-131">Hello 收件者成功時，會傳送 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-131">When hello recipient succeeds, hello subscription is transferred.</span></span> 
6. <span data-ttu-id="1aa0d-132">hello hello 訂用帳戶的預設目錄變更 toohello 目錄中的 hello 使用者是。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-132">hello default directory of hello subscription is changed toohello directory that hello user is in.</span></span>


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a><span data-ttu-id="1aa0d-133">建議 toomanage 的訂閱和目錄</span><span class="sxs-lookup"><span data-stu-id="1aa0d-133">Suggestions toomanage both a subscription and a directory</span></span>
<span data-ttu-id="1aa0d-134">hello Azure 訂用帳戶的系統管理角色來管理資源繫結 toohello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-134">hello administrative roles for an Azure subscription manage resources tied toohello Azure subscription.</span></span> <span data-ttu-id="1aa0d-135">本節說明 hello Azure 訂用帳戶系統管理員與 Azure AD 目錄管理員之間的差異。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-135">This section explains hello differences between Azure subscription admins and Azure AD directory admins.</span></span> <span data-ttu-id="1aa0d-136">系統管理角色和其他建議使用這些訂用帳戶均涵蓋於 toomanage[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-136">Administrative roles and other suggestions for using them toomanage your subscription are covered at [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="1aa0d-137">根據預設，您獲指派 hello 服務系統管理員角色，當您註冊。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-137">By default, you are assigned hello Service Administrator role when you sign up.</span></span> <span data-ttu-id="1aa0d-138">如果其他人需要 toosign 中的並使用 hello 存取服務相同的訂用帳戶，您可以將它們新增為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-138">If others need toosign in and access services using hello same subscription, you can add them as co-administrators.</span></span> 

<span data-ttu-id="1aa0d-139">Azure AD 有一組不同的系統管理角色 toomanage hello 目錄和身分識別相關功能。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-139">Azure AD has a different set of administrative roles toomanage hello directory and identity-related features.</span></span> <span data-ttu-id="1aa0d-140">例如，hello 目錄全域管理員可以新增使用者和群組 toohello 目錄，或需要多重要素驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-140">For example, hello global administrator of a directory can add users and groups toohello directory, or require multifactor authentication for users.</span></span> <span data-ttu-id="1aa0d-141">建立目錄的使用者指派 toohello 全域管理員角色，他們可以指派管理角色 tooother 使用者。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-141">A user who creates a directory is assigned toohello global administrator role and they can assign administrative roles tooother users.</span></span> <span data-ttu-id="1aa0d-142">其他服務 (例如 Office 365 和 Microsoft Intune) 也會使用 Azure AD 系統管理角色。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-142">Azure AD administrative roles are also used by other services such as Office 365 and Microsoft Intune.</span></span> 

<span data-ttu-id="1aa0d-143">Azure 訂用帳戶管理員和 Azure AD 目錄管理員是兩個不同的角色。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-143">Azure subscription admins and Azure AD directory admins are two separate roles.</span></span> 
* <span data-ttu-id="1aa0d-144">Azure 訂用帳戶系統管理員可以管理 Azure 中的資源，而且可以在 hello Azure 入口網站中使用 Azure AD，（因為 hello Azure 入口網站本身是一項 Azure 資源）。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-144">Azure subscription admins can manage resources in Azure and can use Azure AD in hello Azure portal (because hello Azure portal itself is an Azure resource).</span></span> 
* <span data-ttu-id="1aa0d-145">目錄管理員可以管理屬性只能在 hello Azure AD 目錄中。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-145">Directory admins can manage properties only in hello Azure AD directory.</span></span>

<span data-ttu-id="1aa0d-146">使用者可以同時擔任這兩個角色，但並非必要。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-146">A person can be in both roles but it isn’t required.</span></span> <span data-ttu-id="1aa0d-147">無法將目錄全域管理員指派為 Azure 訂用帳戶的服務管理員或共同管理員 (反之亦然)。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-147">A directory global administrator might not be assigned as service administrator or co-administrator of an Azure subscription, or vice versa.</span></span> <span data-ttu-id="1aa0d-148">不是 hello 訂用帳戶的系統管理員，hello 使用者可以登入 toohello Azure 入口網站，但無法管理該訂用帳戶在 hello 入口網站中的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-148">Without being an administrator of hello subscription, hello user can sign in toohello Azure portal, but can't manage hello directories for that subscription in hello portal.</span></span> <span data-ttu-id="1aa0d-149">不過，這位使用者可以管理使用 Azure AD PowerShell 或 Office 365 系統管理中心 hello 之類的其他工具的目錄。</span><span class="sxs-lookup"><span data-stu-id="1aa0d-149">However, this user can manage directories using other tools such as Azure AD PowerShell or hello Office 365 Admin Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa0d-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1aa0d-150">Next steps</span></span>
* <span data-ttu-id="1aa0d-151">toolearn 深入了解如何 toochange 管理員 Azure 訂用帳戶，請參閱[的 Azure 訂用帳戶 tooanother 帳戶的擁有權轉移](../billing/billing-subscription-transfer.md)</span><span class="sxs-lookup"><span data-stu-id="1aa0d-151">toolearn more about how toochange administrators for an Azure subscription, see [Transfer ownership of an Azure subscription tooanother account](../billing/billing-subscription-transfer.md)</span></span>
* <span data-ttu-id="1aa0d-152">toolearn 深入了解如何控制資源存取 Microsoft Azure 中，請參閱[了解 Azure 中的資源存取](active-directory-understanding-resource-access.md)</span><span class="sxs-lookup"><span data-stu-id="1aa0d-152">toolearn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](active-directory-understanding-resource-access.md)</span></span>
* <span data-ttu-id="1aa0d-153">如需有關如何 tooassign 角色在 Azure AD 中，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1aa0d-153">For more information on how tooassign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
