---
title: "Azure Active Directory 中的 aaaAssign 授權 tooa 群組 |Microsoft 文件"
description: "Tooassign 如何授權 toousers 透過 Azure Active Directory 群組授權"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a><span data-ttu-id="896f1-104">指派授權 toousers 由 Azure Active Directory 中的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="896f1-104">Assign licenses toousers by group membership in Azure Active Directory</span></span>

<span data-ttu-id="896f1-105">這篇文章會逐步引導您指派的使用者在 Azure Active Directory (Azure AD) 中的產品授權 tooa 群組，然後確認 他們要正確授權。</span><span class="sxs-lookup"><span data-stu-id="896f1-105">This article walks you through assigning product licenses tooa group of users in Azure Active Directory (Azure AD) and then verifying that they're licensed correctly.</span></span>

<span data-ttu-id="896f1-106">在此範例中，hello 租用戶包含安全性群組**人力資源部門皆**。</span><span class="sxs-lookup"><span data-stu-id="896f1-106">In this example, hello tenant contains a security group called **HR Department**.</span></span> <span data-ttu-id="896f1-107">此群組包含 hello 人力資源部門 （約 1,000 位使用者） 的所有成員。</span><span class="sxs-lookup"><span data-stu-id="896f1-107">This group includes all members of hello human resources department (around 1,000 users).</span></span> <span data-ttu-id="896f1-108">您想 tooassign Office 365 Enterprise E3 授權 toohello 整個部門。</span><span class="sxs-lookup"><span data-stu-id="896f1-108">You want tooassign Office 365 Enterprise E3 licenses toohello entire department.</span></span> <span data-ttu-id="896f1-109">hello 部門之前準備好使用它的 toostart hello Yammer 企業服務包含在 hello 產品中，必須暫時停用。</span><span class="sxs-lookup"><span data-stu-id="896f1-109">hello Yammer Enterprise service that's included in hello product must be temporarily disabled until hello department is ready toostart using it.</span></span> <span data-ttu-id="896f1-110">您也想 toodeploy 企業行動力 + 安全性授權 toohello 相同的使用者群組。</span><span class="sxs-lookup"><span data-stu-id="896f1-110">You also want toodeploy Enterprise Mobility + Security licenses toohello same group of users.</span></span>

> [!NOTE]
> <span data-ttu-id="896f1-111">並非所有位置都可使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="896f1-111">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="896f1-112">Tooa 使用者可以指派授權之前，hello 系統管理員會對使用者 hello toospecify hello Usage 位置屬性。</span><span class="sxs-lookup"><span data-stu-id="896f1-112">Before a license can be assigned tooa user, hello administrator has toospecify hello Usage location property on hello user.</span></span>

> <span data-ttu-id="896f1-113">取得群組的授權指派，指定使用位置沒有任何使用者將會繼承 hello hello 目錄位置。</span><span class="sxs-lookup"><span data-stu-id="896f1-113">For group license assignment, any users without a usage location specified will inherit hello location of hello directory.</span></span> <span data-ttu-id="896f1-114">如果您有多個位置中的使用者，我們建議您一律將使用位置做為您的使用者建立流程的一部分 （例如透過 AAD Connect 組態）-可確保授權指派的 hello 結果永遠正確，且使用者未收到的 Azure AD 中不允許的位置中的服務。</span><span class="sxs-lookup"><span data-stu-id="896f1-114">If you have users in multiple locations, we recommend that you always set usage location as part of your user creation flow in Azure AD (e.g. via AAD Connect configuration) - that will ensure hello result of license assignment is always correct and users do not receive services in locations that are not allowed.</span></span>

## <a name="step-1-assign-hello-required-licenses"></a><span data-ttu-id="896f1-115">步驟 1： 指派所需的 hello 授權</span><span class="sxs-lookup"><span data-stu-id="896f1-115">Step 1: Assign hello required licenses</span></span>

1. <span data-ttu-id="896f1-116">登入 toohello [ **Azure 入口網站**](https://portal.azure.com)以系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="896f1-116">Sign in toohello [**Azure portal**](https://portal.azure.com) with an Administrator account.</span></span> <span data-ttu-id="896f1-117">toomanage 授權，hello 帳戶必須是全域管理員角色或使用者帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="896f1-117">toomanage licenses, hello account must be a global administrator role or user account administrator.</span></span>

2. <span data-ttu-id="896f1-118">選取**更多服務**在 hello 左側瀏覽窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="896f1-118">Select **More services** in hello left navigation pane, and then select **Azure Active Directory**.</span></span> <span data-ttu-id="896f1-119">您可以新增此刀鋒視窗 tooFavorites，或將其釘選 toohello 入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="896f1-119">You can add this blade tooFavorites or pin it toohello portal dashboard.</span></span>

3. <span data-ttu-id="896f1-120">在 hello **Azure Active Directory**刀鋒視窗中，選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="896f1-120">On hello **Azure Active Directory** blade, select **Licenses**.</span></span> <span data-ttu-id="896f1-121">這會開啟刀鋒視窗，您可以在此檢視並管理 hello 租用戶中的所有授權產品。</span><span class="sxs-lookup"><span data-stu-id="896f1-121">This opens a blade where you can see and manage all licensable products in hello tenant.</span></span>

4. <span data-ttu-id="896f1-122">在下**所有產品**，選取 Office 365 Enterprise E3 和 Enterprise Mobility + Security 選取 hello 產品名稱。</span><span class="sxs-lookup"><span data-stu-id="896f1-122">Under **All products**, select both Office 365 Enterprise E3 and Enterprise Mobility + Security by selecting hello product names.</span></span> <span data-ttu-id="896f1-123">toostart hello 分派，選取**指派**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="896f1-123">toostart hello assignment, select **Assign** at hello top of hello blade.</span></span>

   ![所有產品、指派授權](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. <span data-ttu-id="896f1-125">在 hello**指派授權**刀鋒視窗中，按一下 **使用者和群組**tooopen hello**使用者和群組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="896f1-125">On hello **Assign license** blade, click **Users and groups** tooopen hello **Users and groups** blade.</span></span> <span data-ttu-id="896f1-126">Hello 群組名稱的搜尋*人力資源部門皆*選取 hello 群組，然後依序按一下要確定 tooconfirm**選取**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="896f1-126">Search for hello group name *HR Department*, select hello group, and then be sure tooconfirm by clicking **Select** at hello bottom of hello blade.</span></span>

   ![選取群組](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. <span data-ttu-id="896f1-128">在 hello**指派授權**刀鋒視窗中，按一下 **指派選項 （選擇性）**，其中顯示所有服務方案包含在 hello 我們先前選取的兩個產品。</span><span class="sxs-lookup"><span data-stu-id="896f1-128">On hello **Assign license** blade, click **Assignment options (optional)**, which displays all service plans included in hello two products that we selected previously.</span></span> <span data-ttu-id="896f1-129">尋找**Yammer 企業**並使其**關閉**toodisable 從 hello 產品授權服務。</span><span class="sxs-lookup"><span data-stu-id="896f1-129">Find **Yammer Enterprise** and turn it **Off** toodisable that service from hello product license.</span></span> <span data-ttu-id="896f1-130">按一下以確認**確定**底部的 hello**指派選項**。</span><span class="sxs-lookup"><span data-stu-id="896f1-130">Confirm by clicking **OK** at hello bottom of **Assignment options**.</span></span>

   ![指派選項](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. <span data-ttu-id="896f1-132">hello 上的 toocomplete hello 指派**指派授權**刀鋒視窗中，按一下 **指派**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="896f1-132">toocomplete hello assignment, on hello **Assign license** blade, click **Assign** at hello bottom of hello blade.</span></span>

8. <span data-ttu-id="896f1-133">Hello 右上角，其中顯示 hello 狀態和 hello 程序結果中會顯示通知。</span><span class="sxs-lookup"><span data-stu-id="896f1-133">A notification is displayed in hello upper-right corner that shows hello status and outcome of hello process.</span></span> <span data-ttu-id="896f1-134">如果 hello 分派 toohello 群組無法完成 （例如，由於 hello 群組中的現有預先授權） 中，按一下 hello hello 失敗的通知 tooview 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="896f1-134">If hello assignment toohello group couldn't be completed (for example, because of pre-existing licenses in hello group), click hello notification tooview details of hello failure.</span></span>

<span data-ttu-id="896f1-135">我們現在已經指定 hello 人力資源部門皆群組的授權範本。</span><span class="sxs-lookup"><span data-stu-id="896f1-135">We've now specified a license template for hello HR Department group.</span></span> <span data-ttu-id="896f1-136">在 Azure AD 中的背景處理序已啟動的 tooprocess 該群組的所有現有的成員。</span><span class="sxs-lookup"><span data-stu-id="896f1-136">A background process in Azure AD has been started tooprocess all existing members of that group.</span></span> <span data-ttu-id="896f1-137">這項初始作業可能需要一些時間，視 hello hello 群組目前大小而定。</span><span class="sxs-lookup"><span data-stu-id="896f1-137">This initial operation might take some time, depending on hello current size of hello group.</span></span> <span data-ttu-id="896f1-138">在 hello 下一個步驟中，我們將說明如何 tooverify hello 程序已完成，並判斷是否需要的 tooresolve 問題進一步注意。</span><span class="sxs-lookup"><span data-stu-id="896f1-138">In hello next step, we'll describe how tooverify that hello process has finished and determine if further attention is required tooresolve problems.</span></span>

> [!NOTE]
> <span data-ttu-id="896f1-139">您可以啟動 hello 從替代位置的同一個指派：**使用者和群組**在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="896f1-139">You can start hello same assignment from an alternative location: **Users and groups** in Azure AD.</span></span> <span data-ttu-id="896f1-140">跳過**Azure Active Directory** > **使用者和群組** > **所有群組**。</span><span class="sxs-lookup"><span data-stu-id="896f1-140">Go too**Azure Active Directory** > **Users and groups** > **All groups**.</span></span> <span data-ttu-id="896f1-141">然後尋找 hello 群組、 選取它，並移 toohello**授權** 索引標籤 hello**指派**hello 刀鋒視窗頂端的按鈕會開啟 hello 授權指派 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="896f1-141">Then find hello group, select it, and go toohello **Licenses** tab. hello **Assign** button on top of hello blade opens hello license assignment blade.</span></span>

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a><span data-ttu-id="896f1-142">步驟 2： 驗證 hello 初始作業已完成</span><span class="sxs-lookup"><span data-stu-id="896f1-142">Step 2: Verify that hello initial assignment has finished</span></span>

1. <span data-ttu-id="896f1-143">跳過**Azure Active Directory** > **使用者和群組** > **所有群組**。</span><span class="sxs-lookup"><span data-stu-id="896f1-143">Go too**Azure Active Directory** > **Users and groups** > **All groups**.</span></span> <span data-ttu-id="896f1-144">然後尋找 hello**人力資源部門皆**授權指派給群組。</span><span class="sxs-lookup"><span data-stu-id="896f1-144">Then find hello **HR Department** group that licenses were assigned to.</span></span>

2. <span data-ttu-id="896f1-145">在 hello**人力資源部門皆**群組刀鋒視窗中，選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="896f1-145">On hello **HR Department** group blade, select **Licenses**.</span></span> <span data-ttu-id="896f1-146">這可讓您快速確認授權已獲完全指派 toousers，而且如果有需要 toolook 到任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="896f1-146">This lets you quickly confirm if licenses have been fully assigned toousers and if there are any errors that you need toolook into.</span></span> <span data-ttu-id="896f1-147">使用位於 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="896f1-147">hello following information is available:</span></span>

   - <span data-ttu-id="896f1-148">目前的產品授權清單指派 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="896f1-148">List of product licenses that are currently assigned toohello group.</span></span> <span data-ttu-id="896f1-149">選取項目 tooshow hello 特定服務已啟用，並 toomake 變更。</span><span class="sxs-lookup"><span data-stu-id="896f1-149">Select an entry tooshow hello specific services that have been enabled and toomake changes.</span></span>

   - <span data-ttu-id="896f1-150">Hello 最新授權所做的變更 toohello 群組 （如果正在處理 hello 變更，或處理已完成的所有使用者的成員） 的狀態。</span><span class="sxs-lookup"><span data-stu-id="896f1-150">Status of hello latest license changes that were made toohello group (if hello changes are being processed or if processing has finished for all user members).</span></span>

   - <span data-ttu-id="896f1-151">處於錯誤狀態，因為 toothem 無法指派授權的使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="896f1-151">Information about users who are in an error state because licenses couldn't be assigned toothem.</span></span>

   ![指派選項](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. <span data-ttu-id="896f1-153">如需授權處理的詳細資訊，請參閱 [Azure Active Directory] > [使用者和群組] > 群組名稱 > [稽核記錄]。</span><span class="sxs-lookup"><span data-stu-id="896f1-153">See more detailed information about license processing under **Azure Active Directory** > **Users and groups** > *group name* > **Audit logs**.</span></span> <span data-ttu-id="896f1-154">請注意下列活動的 hello:</span><span class="sxs-lookup"><span data-stu-id="896f1-154">Note hello following activities:</span></span>

   - <span data-ttu-id="896f1-155">活動：**開始套用群組的基礎授權 toousers**。</span><span class="sxs-lookup"><span data-stu-id="896f1-155">Activity: **Start applying group based license toousers**.</span></span> <span data-ttu-id="896f1-156">這會記錄 hello 系統拾取 hello hello 群組和啟動時將它套用 tooall 使用者成員上的授權指派變更時。</span><span class="sxs-lookup"><span data-stu-id="896f1-156">This is logged when hello system picks up hello license-assignment change on hello group and starts applying it tooall user members.</span></span> <span data-ttu-id="896f1-157">它包含 hello 所做變更的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="896f1-157">It contains information about hello change that was made.</span></span>

   - <span data-ttu-id="896f1-158">活動：**結束套用群組的基礎授權 toousers**。</span><span class="sxs-lookup"><span data-stu-id="896f1-158">Activity: **Finish applying group based license toousers**.</span></span> <span data-ttu-id="896f1-159">這會記錄當 hello 系統完成處理 hello 群組中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="896f1-159">This is logged when hello system finishes processing all users in hello group.</span></span> <span data-ttu-id="896f1-160">它包含已成功處理的使用者人數和無法獲得群組授權指派的使用者人數之摘要。</span><span class="sxs-lookup"><span data-stu-id="896f1-160">It contains a summary of how many users were successfully processed and how many users couldn't be assigned group licenses.</span></span>

   <span data-ttu-id="896f1-161">[閱讀本節](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity)toolearn 深入了解如何稽核記錄檔可能會使用的 tooanalyze 變更群組為基礎的授權。</span><span class="sxs-lookup"><span data-stu-id="896f1-161">[Read this section](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn more about how audit logs can be used tooanalyze changes made by group-based licensing.</span></span>

## <a name="step-3-check-for-license-problems-and-resolve-them"></a><span data-ttu-id="896f1-162">步驟 3︰檢查授權問題及解決這些問題</span><span class="sxs-lookup"><span data-stu-id="896f1-162">Step 3: Check for license problems and resolve them</span></span>

1. <span data-ttu-id="896f1-163">跳過**Azure Active Directory** > **使用者和群組** > **所有群組**，並尋找 hello**人力資源部門皆**授權指派給群組。</span><span class="sxs-lookup"><span data-stu-id="896f1-163">Go too**Azure Active Directory** > **Users and groups** > **All groups**, and find hello **HR Department** group that licenses were assigned to.</span></span>
2. <span data-ttu-id="896f1-164">在 hello**人力資源部門皆**群組刀鋒視窗中，選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="896f1-164">On hello **HR Department** group blade, select **Licenses**.</span></span> <span data-ttu-id="896f1-165">在 [hello] 刀鋒視窗頂端的 hello 通知顯示無法指派授權給 10 個使用者。</span><span class="sxs-lookup"><span data-stu-id="896f1-165">hello notification on top of hello blade shows that there are 10 users that licenses couldn't be assigned to.</span></span> <span data-ttu-id="896f1-166">按一下通知，隨即開啟一份此群組為授權錯誤狀態的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="896f1-166">Clicking it opens a list of all users in a licensing-error state for this group.</span></span>
3. <span data-ttu-id="896f1-167">hello**無法指派**資料行告訴我們這兩個產品的授權，無法指派 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="896f1-167">hello **Failed assignments** column tells us that both product licenses couldn't be assigned toohello users.</span></span> <span data-ttu-id="896f1-168">hello**排名最前面的失敗原因**資料行包含 hello hello 失敗原因。</span><span class="sxs-lookup"><span data-stu-id="896f1-168">hello **Top reason for failure** column contains hello cause of hello failure.</span></span> <span data-ttu-id="896f1-169">在此案例中為 [衝突的服務方案]。</span><span class="sxs-lookup"><span data-stu-id="896f1-169">In this case, it's **Conflicting service plans**.</span></span>

   ![失敗的指派](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. <span data-ttu-id="896f1-171">選取使用者 tooopen hello**授權**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="896f1-171">Select a user tooopen hello **Licenses** blade.</span></span> <span data-ttu-id="896f1-172">此刀鋒視窗會顯示所有目前已指派 toohello 使用者的授權。</span><span class="sxs-lookup"><span data-stu-id="896f1-172">This blade shows all licenses that are currently assigned toohello user.</span></span> <span data-ttu-id="896f1-173">在此範例中，hello 使用者具有繼承自 hello 的 hello Office 365 Enterprise E1 授權**Kiosk 使用者**群組。</span><span class="sxs-lookup"><span data-stu-id="896f1-173">In this example, hello user has hello Office 365 Enterprise E1 license that was inherited from hello **Kiosk users** group.</span></span> <span data-ttu-id="896f1-174">這與 hello 系統嘗試 tooapply 從 hello 的 hello E3 授權衝突**人力資源部門皆**群組。</span><span class="sxs-lookup"><span data-stu-id="896f1-174">This conflicts with hello E3 license that hello system tried tooapply from hello **HR Department** group.</span></span> <span data-ttu-id="896f1-175">如此一來，無該群組中的 hello 授權已被指派 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="896f1-175">As a result, none of hello licenses from that group has been assigned toohello user.</span></span>

   ![檢視使用者的授權](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. <span data-ttu-id="896f1-177">toosolve 這項衝突，移除 hello 使用者從 hello **Kiosk 使用者**群組。</span><span class="sxs-lookup"><span data-stu-id="896f1-177">toosolve this conflict, remove hello user from hello **Kiosk users** group.</span></span> <span data-ttu-id="896f1-178">Azure AD 處理 hello 變更之後，hello**人力資源部門皆**正確指派授權。</span><span class="sxs-lookup"><span data-stu-id="896f1-178">After Azure AD processes hello change, hello **HR Department** licenses are correctly assigned.</span></span>

   ![已正確指派的授權](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a><span data-ttu-id="896f1-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="896f1-180">Next steps</span></span>

<span data-ttu-id="896f1-181">toolearn hello 功能有關的詳細資訊設定的授權管理透過群組，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="896f1-181">toolearn more about hello feature set for license management through groups, see hello following articles:</span></span>

* [<span data-ttu-id="896f1-182">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="896f1-182">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="896f1-183">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="896f1-183">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="896f1-184">如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者</span><span class="sxs-lookup"><span data-stu-id="896f1-184">How toomigrate individual licensed users toogroup-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="896f1-185">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="896f1-185">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
