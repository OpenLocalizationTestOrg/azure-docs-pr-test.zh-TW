---
title: "Azure 訂用帳戶如何與 Azure Active Directory 產生關聯 | Microsoft Docs"
description: "登入 Microsoft Azure 及相關問題，例如 Azure 訂用帳戶與 Azure Active Directory 之間的關係。"
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
ms.openlocfilehash: 283c9903501a1e497e4dde81146d21edb869e9e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a><span data-ttu-id="39b9d-103">Azure 訂用帳戶如何與 Azure Active Directory 產生關聯</span><span class="sxs-lookup"><span data-stu-id="39b9d-103">How Azure subscriptions are associated with Azure Active Directory</span></span>
<span data-ttu-id="39b9d-104">本文涵蓋有關 Azure 訂用帳戶與 Azure Active Directory (Azure AD) 之間關係，以及如何將現有訂用帳戶新增至 Azure AD 目錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="39b9d-104">This article covers information about the relationship between an Azure subscription and Azure Active Directory (Azure AD), and how to add an existing subscription to your Azure AD directory.</span></span>

## <a name="your-azure-subscriptions-relationship-to-azure-ad"></a><span data-ttu-id="39b9d-105">您的 Azure 訂用帳戶與 Azure AD 的關係</span><span class="sxs-lookup"><span data-stu-id="39b9d-105">Your Azure subscription's relationship to Azure AD</span></span>
<span data-ttu-id="39b9d-106">Azure 訂用帳戶具有 Azure AD 目錄的信任關係，這表示它信任此目錄來驗證使用者、服務和裝置。</span><span class="sxs-lookup"><span data-stu-id="39b9d-106">Your Azure subscription has a trust relationship with Azure AD, which means that it trusts the directory to authenticate users, services, and devices.</span></span> <span data-ttu-id="39b9d-107">多個訂用帳戶可以信任相同的目錄，但是每個訂用帳戶只能信任一個目錄。</span><span class="sxs-lookup"><span data-stu-id="39b9d-107">Multiple subscriptions can trust the same directory, but each subscription trusts only one directory.</span></span> 

<span data-ttu-id="39b9d-108">訂用帳戶與目錄之間存在的信任關係不同於訂用帳戶與 Azure 中其他資源 (網站、資料庫等) 之間的關係。</span><span class="sxs-lookup"><span data-stu-id="39b9d-108">The trust relationship that a subscription has with a directory is unlike the relationship that it has with other resources in Azure (websites, databases, and so on).</span></span> <span data-ttu-id="39b9d-109">如果訂用帳戶已過期，也會停止存取與訂用帳戶相關聯的其他資源。</span><span class="sxs-lookup"><span data-stu-id="39b9d-109">If a subscription expires, access to the other resources associated with the subscription also stops.</span></span> <span data-ttu-id="39b9d-110">但 Azure AD 目錄會保留在 Azure 中，而且您可以將不同的訂用帳戶與該目錄產生關聯，以及使用新的訂用帳戶管理此目錄。</span><span class="sxs-lookup"><span data-stu-id="39b9d-110">But an Azure AD directory remains in Azure, and you can associate a different subscription with that directory and manage the directory using the new subscription.</span></span>

![訂用帳戶如何與圖表產生關聯](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

<span data-ttu-id="39b9d-112">所有使用者都有會對他們進行驗證的單一主目錄，但是他它們也可以是其他目錄中的來賓。</span><span class="sxs-lookup"><span data-stu-id="39b9d-112">All users have a single home directory that authenticates them, but they can also be guests in other directories.</span></span> <span data-ttu-id="39b9d-113">在 Azure AD 中，您可以看到您的使用者帳戶為其成員或來賓的目錄。</span><span class="sxs-lookup"><span data-stu-id="39b9d-113">In Azure AD, you can see the directories of which your user account is a member or guest.</span></span>

## <a name="azure-ad-and-cloud-service-subscriptions"></a><span data-ttu-id="39b9d-114">Azure AD 和雲端服務訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="39b9d-114">Azure AD and cloud service subscriptions</span></span>
<span data-ttu-id="39b9d-115">Azure AD 提供大部分 Microsoft 雲端服務的核心目錄和身分識別管理功能，包括：</span><span class="sxs-lookup"><span data-stu-id="39b9d-115">Azure AD provides the core directory and identity management capabilities behind most of Microsoft’s cloud services, including:</span></span>

* <span data-ttu-id="39b9d-116">Azure</span><span class="sxs-lookup"><span data-stu-id="39b9d-116">Azure</span></span>
* <span data-ttu-id="39b9d-117">Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="39b9d-117">Microsoft Office 365</span></span>
* <span data-ttu-id="39b9d-118">Microsoft Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="39b9d-118">Microsoft Dynamics CRM Online</span></span>
* <span data-ttu-id="39b9d-119">Microsoft Intune</span><span class="sxs-lookup"><span data-stu-id="39b9d-119">Microsoft Intune</span></span>

<span data-ttu-id="39b9d-120">當您註冊上述任何 Microsoft 雲端服務時，會免費取得 Azure AD 服務。</span><span class="sxs-lookup"><span data-stu-id="39b9d-120">You get the Azure AD service free when you sign up for any of these Microsoft cloud services.</span></span> <span data-ttu-id="39b9d-121">如果您需要將額外的 Azure 訂用帳戶新增至 Azure AD 目錄，您必須使用 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="39b9d-121">If you want to add an additional Azure subscription to an Azure AD directory, you must be signed in with a Microsoft account.</span></span> <span data-ttu-id="39b9d-122">如果您使用工作或學校帳戶來登入 Azure，則無法將 Azure 訂用帳戶新增至現有的目錄，因為 Azure 無法直接驗證您的工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="39b9d-122">If you sign in to Azure with a work or school account, you can't add an Azure subscription to an existing directory because your work or school account can't be authenticated directly by Azure.</span></span> 

## <a name="to-add-an-existing-subscription-to-your-azure-ad-directory"></a><span data-ttu-id="39b9d-123">將現有的訂用帳戶新增至您的 Azure AD 目錄</span><span class="sxs-lookup"><span data-stu-id="39b9d-123">To add an existing subscription to your Azure AD directory</span></span>
<span data-ttu-id="39b9d-124">您用於登入的帳戶必須同時存在於與訂用帳戶相關聯的目前目錄中和您想要將訂用帳戶新增至的目錄中。</span><span class="sxs-lookup"><span data-stu-id="39b9d-124">You must sign in with an account that exists in both the current directory with which the subscription is associated and in the directory you want to add it to.</span></span> 

1. <span data-ttu-id="39b9d-125">以您想要移轉擁有權之訂用帳戶的帳戶管理員之帳戶登入 [Azure 帳戶中心](https://account.windowsazure.com/Home/Index)。</span><span class="sxs-lookup"><span data-stu-id="39b9d-125">Sign in to the [Azure Account Center](https://account.windowsazure.com/Home/Index) with an account that is the Account Administrator of the subscription whose ownership you want to transfer.</span></span>
2. <span data-ttu-id="39b9d-126">確定您希望成為訂用帳戶擁有者的使用者位於目標目錄中。</span><span class="sxs-lookup"><span data-stu-id="39b9d-126">Ensure that the user who you want to be the subscription owner is in the targeted directory.</span></span>
3. <span data-ttu-id="39b9d-127">按一下 [移轉訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="39b9d-127">Click **Transfer subscription**.</span></span>
4. <span data-ttu-id="39b9d-128">指定接受者。</span><span class="sxs-lookup"><span data-stu-id="39b9d-128">Specify the recipient.</span></span> <span data-ttu-id="39b9d-129">接受者會自動收到含有接受連結的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="39b9d-129">The recipient automatically gets an email with an acceptance link.</span></span>
5. <span data-ttu-id="39b9d-130">接受者按一下連結並遵循指示進行，包括輸入他們的付款資訊。</span><span class="sxs-lookup"><span data-stu-id="39b9d-130">The recipient clicks the link and follows the instructions, including entering their payment information.</span></span> <span data-ttu-id="39b9d-131">當接受者成功時，訂用帳戶就轉移完成。</span><span class="sxs-lookup"><span data-stu-id="39b9d-131">When the recipient succeeds, the subscription is transferred.</span></span> 
6. <span data-ttu-id="39b9d-132">訂用帳戶的預設目錄會變更為使用者所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="39b9d-132">The default directory of the subscription is changed to the directory that the user is in.</span></span>


## <a name="suggestions-to-manage-both-a-subscription-and-a-directory"></a><span data-ttu-id="39b9d-133">管理訂用帳戶和目錄的建議</span><span class="sxs-lookup"><span data-stu-id="39b9d-133">Suggestions to manage both a subscription and a directory</span></span>
<span data-ttu-id="39b9d-134">Azure 訂用帳戶的系統管理角色會管理繫結至 Azure 訂用帳戶的資源。</span><span class="sxs-lookup"><span data-stu-id="39b9d-134">The administrative roles for an Azure subscription manage resources tied to the Azure subscription.</span></span> <span data-ttu-id="39b9d-135">本節說明 Azure 訂用帳戶管理員與 Azure AD 目錄管理員之間的差異。</span><span class="sxs-lookup"><span data-stu-id="39b9d-135">This section explains the differences between Azure subscription admins and Azure AD directory admins.</span></span> <span data-ttu-id="39b9d-136">系統管理角色和使用這些角色來管理訂用帳戶的其他建議，均涵蓋於[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="39b9d-136">Administrative roles and other suggestions for using them to manage your subscription are covered at [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="39b9d-137">根據預設，當您註冊時，您會被指派服務管理員角色。</span><span class="sxs-lookup"><span data-stu-id="39b9d-137">By default, you are assigned the Service Administrator role when you sign up.</span></span> <span data-ttu-id="39b9d-138">如果其他人必須使用相同的訂用帳戶來登入和存取服務，您可以將他們新增為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="39b9d-138">If others need to sign in and access services using the same subscription, you can add them as co-administrators.</span></span> 

<span data-ttu-id="39b9d-139">Azure AD 有一組不同的系統管理角色，可用來管理目錄和識別相關功能。</span><span class="sxs-lookup"><span data-stu-id="39b9d-139">Azure AD has a different set of administrative roles to manage the directory and identity-related features.</span></span> <span data-ttu-id="39b9d-140">例如，目錄的全域管理員可以將使用者和群組加入至目錄，或要求使用者的多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="39b9d-140">For example, the global administrator of a directory can add users and groups to the directory, or require multifactor authentication for users.</span></span> <span data-ttu-id="39b9d-141">建立目錄的使用者會被指派全域管理員角色，而且他們可以將系統管理角色指派給其他使用者。</span><span class="sxs-lookup"><span data-stu-id="39b9d-141">A user who creates a directory is assigned to the global administrator role and they can assign administrative roles to other users.</span></span> <span data-ttu-id="39b9d-142">其他服務 (例如 Office 365 和 Microsoft Intune) 也會使用 Azure AD 系統管理角色。</span><span class="sxs-lookup"><span data-stu-id="39b9d-142">Azure AD administrative roles are also used by other services such as Office 365 and Microsoft Intune.</span></span> 

<span data-ttu-id="39b9d-143">Azure 訂用帳戶管理員和 Azure AD 目錄管理員是兩個不同的角色。</span><span class="sxs-lookup"><span data-stu-id="39b9d-143">Azure subscription admins and Azure AD directory admins are two separate roles.</span></span> 
* <span data-ttu-id="39b9d-144">Azure 訂用帳戶管理員可以管理 Azure 中的資源，而且可以在 Azure 入口網站中使用 Azure AD (因為 Azure 入口網站本身是 Azure 資源)。</span><span class="sxs-lookup"><span data-stu-id="39b9d-144">Azure subscription admins can manage resources in Azure and can use Azure AD in the Azure portal (because the Azure portal itself is an Azure resource).</span></span> 
* <span data-ttu-id="39b9d-145">目錄管理員止可以管理 Azure AD 目錄中的屬性。</span><span class="sxs-lookup"><span data-stu-id="39b9d-145">Directory admins can manage properties only in the Azure AD directory.</span></span>

<span data-ttu-id="39b9d-146">使用者可以同時擔任這兩個角色，但並非必要。</span><span class="sxs-lookup"><span data-stu-id="39b9d-146">A person can be in both roles but it isn’t required.</span></span> <span data-ttu-id="39b9d-147">無法將目錄全域管理員指派為 Azure 訂用帳戶的服務管理員或共同管理員 (反之亦然)。</span><span class="sxs-lookup"><span data-stu-id="39b9d-147">A directory global administrator might not be assigned as service administrator or co-administrator of an Azure subscription, or vice versa.</span></span> <span data-ttu-id="39b9d-148">使用者不需是訂用帳戶的管理員，即可登入 Azure 入口網站，但無法在入口網站中管理該訂用帳戶的目錄。</span><span class="sxs-lookup"><span data-stu-id="39b9d-148">Without being an administrator of the subscription, the user can sign in to the Azure portal, but can't manage the directories for that subscription in the portal.</span></span> <span data-ttu-id="39b9d-149">不過，此使用者可以使用其他工具 (例如 Azure AD PowerShell 或 Office 365 系統管理中心) 來管理目錄。</span><span class="sxs-lookup"><span data-stu-id="39b9d-149">However, this user can manage directories using other tools such as Azure AD PowerShell or the Office 365 Admin Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39b9d-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39b9d-150">Next steps</span></span>
* <span data-ttu-id="39b9d-151">若要深入了解如何變更 Azure 訂用帳戶的系統管理員，請參閱[將 Azure 訂用帳戶的擁有權轉移至另一個帳戶](../billing/billing-subscription-transfer.md)</span><span class="sxs-lookup"><span data-stu-id="39b9d-151">To learn more about how to change administrators for an Azure subscription, see [Transfer ownership of an Azure subscription to another account](../billing/billing-subscription-transfer.md)</span></span>
* <span data-ttu-id="39b9d-152">若要深入了解如何在 Microsoft Azure 中控制資源存取，請參閱 [了解 Azure 中的資源存取](active-directory-understanding-resource-access.md)</span><span class="sxs-lookup"><span data-stu-id="39b9d-152">To learn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](active-directory-understanding-resource-access.md)</span></span>
* <span data-ttu-id="39b9d-153">如需有關如何在 Azure AD 中指派角色的詳細資訊，請參閱 [在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="39b9d-153">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
