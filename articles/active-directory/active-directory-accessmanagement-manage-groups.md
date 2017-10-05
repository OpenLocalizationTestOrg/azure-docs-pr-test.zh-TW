---
title: "在 Azure Active Directory 中管理群組 | Microsoft Docs"
description: "如何使用 Azure Active Directory 來建立和管理群組，進而管理使用者。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 2cc2b63312b331a19c61cd7b59a4cac78edf32e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="c1fca-103">在 Azure Active Directory 中管理群組</span><span class="sxs-lookup"><span data-stu-id="c1fca-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1fca-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c1fca-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="c1fca-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="c1fca-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="c1fca-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1fca-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="c1fca-107">Azure Active Directory (Azure AD) 使用者管理的其中一項功能是能夠建立使用者群組。</span><span class="sxs-lookup"><span data-stu-id="c1fca-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="c1fca-108">您可以使用群組來執行管理工作，例如一次指派授權或權限給多名使用者。</span><span class="sxs-lookup"><span data-stu-id="c1fca-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="c1fca-109">您也可以使用群組來指派存取權限給</span><span class="sxs-lookup"><span data-stu-id="c1fca-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="c1fca-110">資源，例如目錄中的物件</span><span class="sxs-lookup"><span data-stu-id="c1fca-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="c1fca-111">目錄外部的資源，例如 SaaS 應用程式、Azure 服務、SharePoint 網站或內部部署資源</span><span class="sxs-lookup"><span data-stu-id="c1fca-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="c1fca-112">此外，資源擁有者也可以指派資源存取權給其他人擁有的 Azure AD 群組。</span><span class="sxs-lookup"><span data-stu-id="c1fca-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="c1fca-113">這項指派會將資源的存取權授與該群組的成員。</span><span class="sxs-lookup"><span data-stu-id="c1fca-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="c1fca-114">然後，群組擁有者負責管理群組中的成員資格。</span><span class="sxs-lookup"><span data-stu-id="c1fca-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="c1fca-115">實際上，資源擁有者是將指派使用者至其資源的權限委派給群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="c1fca-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1fca-116">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="c1fca-116">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="c1fca-117">如需了解如何在 Azure AD 系統管理中心管理群組，請參閱[在 Azure Active Directory 中建立群組並新增成員](active-directory-groups-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c1fca-117">For how to manage groups in the Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="c1fca-118">如何建立群組？</span><span class="sxs-lookup"><span data-stu-id="c1fca-118">How do I create a group?</span></span>
<span data-ttu-id="c1fca-119">根據組織已訂閱的服務，您可以使用下列其中一項來建立群組︰</span><span class="sxs-lookup"><span data-stu-id="c1fca-119">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="c1fca-120">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="c1fca-120">the Azure classic portal</span></span>
* <span data-ttu-id="c1fca-121">Office 365 帳戶入口網站</span><span class="sxs-lookup"><span data-stu-id="c1fca-121">the Office 365 account portal</span></span>
* <span data-ttu-id="c1fca-122">Windows Intune 帳戶入口網站</span><span class="sxs-lookup"><span data-stu-id="c1fca-122">the Windows Intune account portal</span></span>

<span data-ttu-id="c1fca-123">我們會說明在 Azure 傳統入口網站中執行的工作。</span><span class="sxs-lookup"><span data-stu-id="c1fca-123">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="c1fca-124">如需使用非 Azure 入口網站管理 Azure AD 目錄的詳細資訊，請參閱 [管理 Azure AD 目錄](active-directory-administer.md)。</span><span class="sxs-lookup"><span data-stu-id="c1fca-124">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="c1fca-125">[在 Azure 傳統入口網站](https://manage.windowsazure.com) 中選取 [Active Directory]，然後選取組織的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="c1fca-125">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="c1fca-126">選取 [群組]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c1fca-126">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="c1fca-127">選取 [新增群組] 。</span><span class="sxs-lookup"><span data-stu-id="c1fca-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="c1fca-128">在 [加入群組]  視窗中，指定群組的名稱與描述。</span><span class="sxs-lookup"><span data-stu-id="c1fca-128">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="c1fca-129">如何新增或移除安全性群組中的個別使用者？</span><span class="sxs-lookup"><span data-stu-id="c1fca-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="c1fca-130">**新增個別使用者到群組**</span><span class="sxs-lookup"><span data-stu-id="c1fca-130">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="c1fca-131">[在 Azure 傳統入口網站](https://manage.windowsazure.com) 中選取 [Active Directory]，然後選取組織的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="c1fca-131">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="c1fca-132">選取 [群組]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c1fca-132">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="c1fca-133">開啟要在其中新增成員的群組。</span><span class="sxs-lookup"><span data-stu-id="c1fca-133">Open the group to which you want to add members.</span></span> <span data-ttu-id="c1fca-134">開啟所選取群組的 [成員]  索引標籤 (如果尚未顯示)。</span><span class="sxs-lookup"><span data-stu-id="c1fca-134">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="c1fca-135">選取 [新增成員] 。</span><span class="sxs-lookup"><span data-stu-id="c1fca-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="c1fca-136">在 [新增成員]  頁面上，選取您想要加入成為此群組成員之使用者或群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="c1fca-136">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="c1fca-137">確定這個名稱加入了 [已選取]  窗格中。</span><span class="sxs-lookup"><span data-stu-id="c1fca-137">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="c1fca-138">**從群組中移除個別使用者**</span><span class="sxs-lookup"><span data-stu-id="c1fca-138">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="c1fca-139">[在 Azure 傳統入口網站](https://manage.windowsazure.com) 中選取 [Active Directory]，然後選取組織的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="c1fca-139">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="c1fca-140">選取 [群組]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c1fca-140">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="c1fca-141">開啟要從中移除成員的群組。</span><span class="sxs-lookup"><span data-stu-id="c1fca-141">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="c1fca-142">選取 [成員] 索引標籤，選取您想要從這個群組移除之成員的名稱，然後按一下 [移除]。</span><span class="sxs-lookup"><span data-stu-id="c1fca-142">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="c1fca-143">在提示中確認您想要從群組中移除這個成員。</span><span class="sxs-lookup"><span data-stu-id="c1fca-143">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="c1fca-144">如何動態管理群組的成員資格？</span><span class="sxs-lookup"><span data-stu-id="c1fca-144">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="c1fca-145">在 Azure AD 中，您可以非常輕鬆地設定一個簡單的規則來判斷哪些使用者要成為群組的成員。</span><span class="sxs-lookup"><span data-stu-id="c1fca-145">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="c1fca-146">簡單的規則是指僅進行一項比較的規則。</span><span class="sxs-lookup"><span data-stu-id="c1fca-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="c1fca-147">例如，如果某個群組指派給 SaaS 應用程式，您即可設定規則來新增職稱為「業務代表」的使用者。</span><span class="sxs-lookup"><span data-stu-id="c1fca-147">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="c1fca-148">此規則接著便會授與此 SaaS 應用程式的存取權給目錄中所有具有該職稱的使用者。</span><span class="sxs-lookup"><span data-stu-id="c1fca-148">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="c1fca-149">當使用者的任何屬性變更時，系統會評估目錄中的所有動態群組規則，以查看使用者的屬性變更是否會觸發任何的群組新增或移除。</span><span class="sxs-lookup"><span data-stu-id="c1fca-149">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="c1fca-150">如果使用者滿足群組規則，則使用者會新增為該群組的成員。</span><span class="sxs-lookup"><span data-stu-id="c1fca-150">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="c1fca-151">如果他們不再滿足其所屬群組的規則，則會從該群組的成員中移除。</span><span class="sxs-lookup"><span data-stu-id="c1fca-151">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="c1fca-152">您可以為安全性群組或 Office 365 群組的動態成員資格設定規則。</span><span class="sxs-lookup"><span data-stu-id="c1fca-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="c1fca-153">目前對應用程式的群組式指派並不支援巢狀群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="c1fca-153">Nested group memberships aren't currently supported for group-based assignment to applications.</span></span>
>
> <span data-ttu-id="c1fca-154">群組的動態成員資格需要將 Azure AD Premium 授權指派給：</span><span class="sxs-lookup"><span data-stu-id="c1fca-154">Dynamic memberships for groups require an Azure AD Premium license to be assigned to</span></span>
>
> * <span data-ttu-id="c1fca-155">負責管理群組規則的系統管理員</span><span class="sxs-lookup"><span data-stu-id="c1fca-155">The administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="c1fca-156">群組的所有成員</span><span class="sxs-lookup"><span data-stu-id="c1fca-156">All members of the group</span></span>
>
>

<span data-ttu-id="c1fca-157">**啟用群組的動態成員資格**</span><span class="sxs-lookup"><span data-stu-id="c1fca-157">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="c1fca-158">[在 Azure 傳統入口網站](https://manage.windowsazure.com) 中選取 [Active Directory]，然後選取組織的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="c1fca-158">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="c1fca-159">選取 [群組]  索引標籤，然後開啟您想要編輯的群組。</span><span class="sxs-lookup"><span data-stu-id="c1fca-159">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="c1fca-160">選取 [設定] 索引標籤，然後將 [啟用動態成員資格] 設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="c1fca-160">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="c1fca-161">為群組設定一個簡單的規則，以控制此群組的動態成員資格的運作方式。</span><span class="sxs-lookup"><span data-stu-id="c1fca-161">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="c1fca-162">請確定已選取 [ **新增使用者位置** ] 選項，然後從清單 (例如，department、jobTitle 等) 中選取一個使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="c1fca-162">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="c1fca-163">接著，選取一個條件 (不等於、等於、開頭不是、開頭為、不包含、包含、不符合、符合)。</span><span class="sxs-lookup"><span data-stu-id="c1fca-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="c1fca-164">指定所選使用者屬性的比較值。</span><span class="sxs-lookup"><span data-stu-id="c1fca-164">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="c1fca-165">若要了解如何為動態群組成員資格建立「進階」  規則 (可包含多個比較的規則)，請參閱 [使用屬性來建立進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="c1fca-165">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="c1fca-166">其他資訊</span><span class="sxs-lookup"><span data-stu-id="c1fca-166">Additional information</span></span>
<span data-ttu-id="c1fca-167">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="c1fca-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c1fca-168">使用 Azure Active Directory 群組管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="c1fca-168">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="c1fca-169">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="c1fca-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="c1fca-170">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="c1fca-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c1fca-171">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="c1fca-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="c1fca-172">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1fca-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
