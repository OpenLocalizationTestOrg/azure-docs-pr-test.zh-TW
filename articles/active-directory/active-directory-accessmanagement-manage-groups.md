---
title: "在 Azure Active Directory aaaManaging 群組 |Microsoft 文件"
description: "如何 toocreate 和管理群組 toomanage Azure 使用 Azure Active Directory 的使用者。"
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
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="cb979-103">在 Azure Active Directory 中管理群組</span><span class="sxs-lookup"><span data-stu-id="cb979-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb979-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cb979-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="cb979-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="cb979-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="cb979-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb979-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="cb979-107">Hello 能力 toocreate 使用者群組的其中一個 hello Azure Active Directory (Azure AD) 使用者管理功能。</span><span class="sxs-lookup"><span data-stu-id="cb979-107">One of hello features of Azure Active Directory (Azure AD) user management is hello ability toocreate groups of users.</span></span> <span data-ttu-id="cb979-108">您使用群組 tooperform 管理工作，例如指派授權或權限的使用者 tooa 數目一次。</span><span class="sxs-lookup"><span data-stu-id="cb979-108">You use a group tooperform management tasks such as assigning licenses or permissions tooa number of users at once.</span></span> <span data-ttu-id="cb979-109">您也可以使用群組 tooassign 存取的權限</span><span class="sxs-lookup"><span data-stu-id="cb979-109">You can also use groups tooassign access permission to</span></span>

* <span data-ttu-id="cb979-110">資源，例如 hello 目錄中的物件</span><span class="sxs-lookup"><span data-stu-id="cb979-110">Resources such as objects in hello directory</span></span>
* <span data-ttu-id="cb979-111">資源外部 toohello 目錄，例如 SaaS 應用程式、 Azure 服務、 SharePoint 網站或內部部署資源</span><span class="sxs-lookup"><span data-stu-id="cb979-111">Resources external toohello directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="cb979-112">此外，資源擁有者也可以指派存取 tooa 資源 tooan Azure AD 群組由他人所擁有。</span><span class="sxs-lookup"><span data-stu-id="cb979-112">In addition, a resource owner can also assign access tooa resource tooan Azure AD group owned by someone else.</span></span> <span data-ttu-id="cb979-113">此指派會授與該群組存取 toohello 資源 hello 成員。</span><span class="sxs-lookup"><span data-stu-id="cb979-113">This assignment grants hello members of that group access toohello resource.</span></span> <span data-ttu-id="cb979-114">然後，hello hello 群組擁有者管理 hello 群組的成員資格。</span><span class="sxs-lookup"><span data-stu-id="cb979-114">Then, hello owner of hello group manages membership in hello group.</span></span> <span data-ttu-id="cb979-115">實際上，hello 資源擁有者的委派 toohello 資源擁有者 hello 群組 hello 權限 tooassign 使用者 tootheir。</span><span class="sxs-lookup"><span data-stu-id="cb979-115">Effectively, hello resource owner delegates toohello owner of hello group hello permission tooassign users tootheir resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb979-116">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="cb979-116">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="cb979-117">Toomanage 群組的方式在 hello Azure AD 系統管理中心，請參閱[建立群組並新增 Azure Active Directory 中的成員](active-directory-groups-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="cb979-117">For how toomanage groups in hello Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="cb979-118">如何建立群組？</span><span class="sxs-lookup"><span data-stu-id="cb979-118">How do I create a group?</span></span>
<span data-ttu-id="cb979-119">根據您組織已訂閱 hello 服務 toowhich，您可以建立使用 hello 下列其中一種群組：</span><span class="sxs-lookup"><span data-stu-id="cb979-119">Depending on hello services toowhich your organization has subscribed, you can create a group using one of hello following:</span></span>

* <span data-ttu-id="cb979-120">hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="cb979-120">hello Azure classic portal</span></span>
* <span data-ttu-id="cb979-121">hello Office 365 帳戶入口網站</span><span class="sxs-lookup"><span data-stu-id="cb979-121">hello Office 365 account portal</span></span>
* <span data-ttu-id="cb979-122">hello Windows Intune 帳戶入口網站</span><span class="sxs-lookup"><span data-stu-id="cb979-122">hello Windows Intune account portal</span></span>

<span data-ttu-id="cb979-123">執行 hello Azure 傳統入口網站中，我們將說明的工作。</span><span class="sxs-lookup"><span data-stu-id="cb979-123">We'll describe tasks as performed in hello Azure classic portal.</span></span> <span data-ttu-id="cb979-124">如需使用非 Azure 入口網站 toomanage Azure AD 目錄的詳細資訊，請參閱[管理 Azure AD 目錄](active-directory-administer.md)。</span><span class="sxs-lookup"><span data-stu-id="cb979-124">For more information about using non-Azure portals toomanage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="cb979-125">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="cb979-125">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="cb979-126">選取 hello**群組** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cb979-126">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="cb979-127">選取 [新增群組] 。</span><span class="sxs-lookup"><span data-stu-id="cb979-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="cb979-128">在 hello**加入群組**視窗中，指定 hello 名稱和 hello 群組的描述。</span><span class="sxs-lookup"><span data-stu-id="cb979-128">In hello **Add Group** window, specify hello name and hello description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="cb979-129">如何新增或移除安全性群組中的個別使用者？</span><span class="sxs-lookup"><span data-stu-id="cb979-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="cb979-130">**tooadd 的個別使用者 tooa 群組**</span><span class="sxs-lookup"><span data-stu-id="cb979-130">**tooadd an individual user tooa group**</span></span>

1. <span data-ttu-id="cb979-131">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="cb979-131">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="cb979-132">選取 hello**群組** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cb979-132">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="cb979-133">開啟您想要 tooadd 成員 hello 群組 toowhich。</span><span class="sxs-lookup"><span data-stu-id="cb979-133">Open hello group toowhich you want tooadd members.</span></span> <span data-ttu-id="cb979-134">開啟 hello**成員**hello 索引標籤上選取的群組，如果尚未顯示它。</span><span class="sxs-lookup"><span data-stu-id="cb979-134">Open hello **Members** tab of hello selected group if it not already displaying.</span></span>
4. <span data-ttu-id="cb979-135">選取 [新增成員] 。</span><span class="sxs-lookup"><span data-stu-id="cb979-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="cb979-136">在 hello**新增成員**頁面上，選取 hello hello 使用者或群組的名稱要 tooadd 為此群組的成員。</span><span class="sxs-lookup"><span data-stu-id="cb979-136">On hello **Add Members** page, select hello name of hello user or a group that you want tooadd as a member of this group.</span></span> <span data-ttu-id="cb979-137">請確定這個名稱已加入 toohello**選取**窗格。</span><span class="sxs-lookup"><span data-stu-id="cb979-137">Make sure that this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="cb979-138">**tooremove 個別使用者從群組**</span><span class="sxs-lookup"><span data-stu-id="cb979-138">**tooremove an individual user from a group**</span></span>

1. <span data-ttu-id="cb979-139">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="cb979-139">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="cb979-140">選取 hello**群組** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cb979-140">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="cb979-141">開啟您想要從中 tooremove 成員 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="cb979-141">Open hello group from which you want tooremove members.</span></span>
4. <span data-ttu-id="cb979-142">選取 hello**成員**索引標籤，選取 hello 成員名稱的 hello 您想要從這個群組中，tooremove，然後按一下**移除**。</span><span class="sxs-lookup"><span data-stu-id="cb979-142">Select hello **Members** tab, select hello name of hello member that you want tooremove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="cb979-143">在 hello 提示字元中，確認您想 tooremove hello 群組從這個成員。</span><span class="sxs-lookup"><span data-stu-id="cb979-143">Confirm at hello prompt that you want tooremove this member from hello group.</span></span>

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a><span data-ttu-id="cb979-144">如何以動態方式管理 hello 群組成員資格？</span><span class="sxs-lookup"><span data-stu-id="cb979-144">How can I manage hello membership of a group dynamically?</span></span>
<span data-ttu-id="cb979-145">在 Azure AD 中，您可以非常輕鬆地設定哪些使用者是 toobe 群組成員的 hello 簡單規則 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="cb979-145">In Azure AD, you can very easily set up a simple rule toodetermine which users are toobe members of hello group.</span></span> <span data-ttu-id="cb979-146">簡單的規則是指僅進行一項比較的規則。</span><span class="sxs-lookup"><span data-stu-id="cb979-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="cb979-147">例如，如果一個群組被指派 tooa SaaS 應用程式，您可以設定規則 tooadd 使用者職稱為 「 銷售代表 」。</span><span class="sxs-lookup"><span data-stu-id="cb979-147">For example, if a group is assigned tooa SaaS application, you can set up a rule tooadd users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="cb979-148">此規則然後授與存取 toothis SaaS 應用程式 tooall 使用者具有該目錄中的職稱。</span><span class="sxs-lookup"><span data-stu-id="cb979-148">This rule then grants access toothis SaaS application tooall users with that job title in your directory.</span></span>

<span data-ttu-id="cb979-149">當使用者變更的任何屬性，hello 系統評估所有的動態群組規則目錄 toosee 如果 hello 使用者 hello 屬性變更會觸發任何群組中加入或移除。</span><span class="sxs-lookup"><span data-stu-id="cb979-149">When any attributes of a user change, hello system evaluates all dynamic group rules in a directory toosee if hello attribute change of hello user would trigger any group adds or removes.</span></span> <span data-ttu-id="cb979-150">如果使用者滿足群組中的規則，它們會新增為成員 toothat 群組。</span><span class="sxs-lookup"><span data-stu-id="cb979-150">If a user satisfies a rule on a group, they are added as a member toothat group.</span></span> <span data-ttu-id="cb979-151">如果它們不再滿足其所隸屬的群組的 hello 規則，則會從該群組移除做為成員。</span><span class="sxs-lookup"><span data-stu-id="cb979-151">If they no longer satisfy hello rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="cb979-152">您可以為安全性群組或 Office 365 群組的動態成員資格設定規則。</span><span class="sxs-lookup"><span data-stu-id="cb979-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="cb979-153">群組為基礎的指派 tooapplications 目前不支援巢狀的群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="cb979-153">Nested group memberships aren't currently supported for group-based assignment tooapplications.</span></span>
>
> <span data-ttu-id="cb979-154">群組動態成員資格要求指派給 Azure AD Premium 授權 toobe</span><span class="sxs-lookup"><span data-stu-id="cb979-154">Dynamic memberships for groups require an Azure AD Premium license toobe assigned to</span></span>
>
> * <span data-ttu-id="cb979-155">負責管理群組中的 hello 規則 hello 系統管理員</span><span class="sxs-lookup"><span data-stu-id="cb979-155">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="cb979-156">Hello 群組的所有成員</span><span class="sxs-lookup"><span data-stu-id="cb979-156">All members of hello group</span></span>
>
>

<span data-ttu-id="cb979-157">**tooenable 群組動態成員資格**</span><span class="sxs-lookup"><span data-stu-id="cb979-157">**tooenable dynamic membership for a group**</span></span>

1. <span data-ttu-id="cb979-158">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="cb979-158">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="cb979-159">選取 hello**群組**索引標籤，而且您想要 tooedit 開啟 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="cb979-159">Select hello **Groups** tab, and open hello group you want tooedit.</span></span>
3. <span data-ttu-id="cb979-160">選取 hello**設定**索引標籤，然後再設定**啟用動態成員資格**太**是**。</span><span class="sxs-lookup"><span data-stu-id="cb979-160">Select hello **Configure** tab, and then set **Enable Dynamic Memberships** too**Yes**.</span></span>
4. <span data-ttu-id="cb979-161">設定 hello 群組 toocontrol 一個簡單的單一規則的這個群組的功能如何動態成員資格。</span><span class="sxs-lookup"><span data-stu-id="cb979-161">Set up a simple single rule for hello group toocontrol how dynamic membership for this group functions.</span></span> <span data-ttu-id="cb979-162">請確定 hello**新增使用者位置**選項已選取，然後選取 hello 清單 （例如，department、 jobTitle 等），從的 使用者屬性</span><span class="sxs-lookup"><span data-stu-id="cb979-162">Make sure hello **Add users where** option is selected, and then select a user property from hello list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="cb979-163">接著，選取一個條件 (不等於、等於、開頭不是、開頭為、不包含、包含、不符合、符合)。</span><span class="sxs-lookup"><span data-stu-id="cb979-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="cb979-164">指定的比較值為 hello 選取的使用者內容。</span><span class="sxs-lookup"><span data-stu-id="cb979-164">Specify a comparison value for hello selected user property.</span></span>

<span data-ttu-id="cb979-165">有關如何 toolearn toocreate*進階*規則 （可以包含多個比較的規則） 的動態群組成員資格，請參閱[使用屬性 toocreate 進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="cb979-165">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="cb979-166">其他資訊</span><span class="sxs-lookup"><span data-stu-id="cb979-166">Additional information</span></span>
<span data-ttu-id="cb979-167">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="cb979-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="cb979-168">使用 Azure Active Directory 群組來管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="cb979-168">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="cb979-169">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="cb979-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="cb979-170">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="cb979-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="cb979-171">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="cb979-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="cb979-172">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb979-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
