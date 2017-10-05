---
title: "將授權指派給 Azure Active Directory 中的群組 | Microsoft Docs"
description: "如何使用 Azure Active Directory 群組授權的方式將授權指派給使用者"
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
ms.openlocfilehash: 42b18eab9cb419e6ada72ba72dc8be8d7f7b2eed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="assign-licenses-to-users-by-group-membership-in-azure-active-directory"></a><span data-ttu-id="aa40d-104">依據 Azure Active Directory 中的群組成員資格將授權指派給使用者</span><span class="sxs-lookup"><span data-stu-id="aa40d-104">Assign licenses to users by group membership in Azure Active Directory</span></span>

<span data-ttu-id="aa40d-105">這篇文章會逐步引導您將產品授權指派給 Azure Active Directory (Azure AD) 中的使用者群組，然後確認他們正確獲得授權。</span><span class="sxs-lookup"><span data-stu-id="aa40d-105">This article walks you through assigning product licenses to a group of users in Azure Active Directory (Azure AD) and then verifying that they're licensed correctly.</span></span>

<span data-ttu-id="aa40d-106">在本範例中，租用戶包含名為「人力資源部門」的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="aa40d-106">In this example, the tenant contains a security group called **HR Department**.</span></span> <span data-ttu-id="aa40d-107">這個群組包括人力資源部門的所有成員 (大約是 1,000 位使用者)。</span><span class="sxs-lookup"><span data-stu-id="aa40d-107">This group includes all members of the human resources department (around 1,000 users).</span></span> <span data-ttu-id="aa40d-108">您想要將 Office 365 Enterprise E3 授權指派給整個部門。</span><span class="sxs-lookup"><span data-stu-id="aa40d-108">You want to assign Office 365 Enterprise E3 licenses to the entire department.</span></span> <span data-ttu-id="aa40d-109">產品中包含的 Yammer Enterprise 服務需要暫時停用，直到部門準備好要開始使用它為止。</span><span class="sxs-lookup"><span data-stu-id="aa40d-109">The Yammer Enterprise service that's included in the product must be temporarily disabled until the department is ready to start using it.</span></span> <span data-ttu-id="aa40d-110">您也要將 Enterprise Mobility + Security 授權部署到相同群組的使用者。</span><span class="sxs-lookup"><span data-stu-id="aa40d-110">You also want to deploy Enterprise Mobility + Security licenses to the same group of users.</span></span>

> [!NOTE]
> <span data-ttu-id="aa40d-111">並非所有位置都可使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="aa40d-111">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="aa40d-112">系統管理員必須指定使用者的使用位置屬性，才能將授權指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="aa40d-112">Before a license can be assigned to a user, the administrator has to specify the Usage location property on the user.</span></span>

> <span data-ttu-id="aa40d-113">如果是群組授權指派，未指定使用位置的任何使用者會繼承目錄的位置。</span><span class="sxs-lookup"><span data-stu-id="aa40d-113">For group license assignment, any users without a usage location specified will inherit the location of the directory.</span></span> <span data-ttu-id="aa40d-114">如果您在多個位置擁有使用者，我們建議您一律將使用位置設為 Azure AD 中使用者建立流程的一部分 (例如，透過 AAD Connect 設定) - 確保授權指派的結果一律是正確的，且使用者不會在不允許的位置收到服務。</span><span class="sxs-lookup"><span data-stu-id="aa40d-114">If you have users in multiple locations, we recommend that you always set usage location as part of your user creation flow in Azure AD (e.g. via AAD Connect configuration) - that will ensure the result of license assignment is always correct and users do not receive services in locations that are not allowed.</span></span>

## <a name="step-1-assign-the-required-licenses"></a><span data-ttu-id="aa40d-115">步驟 1︰指派所需的授權</span><span class="sxs-lookup"><span data-stu-id="aa40d-115">Step 1: Assign the required licenses</span></span>

1. <span data-ttu-id="aa40d-116">使用系統管理員帳戶登入 [**Azure 入口網站**](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="aa40d-116">Sign in to the [**Azure portal**](https://portal.azure.com) with an Administrator account.</span></span> <span data-ttu-id="aa40d-117">若要管理授權，帳戶必須是全域管理員角色或使用者帳戶管理員角色。</span><span class="sxs-lookup"><span data-stu-id="aa40d-117">To manage licenses, the account must be a global administrator role or user account administrator.</span></span>

2. <span data-ttu-id="aa40d-118">選取左瀏覽窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-118">Select **More services** in the left navigation pane, and then select **Azure Active Directory**.</span></span> <span data-ttu-id="aa40d-119">您可以將此刀鋒視窗新增至 [我的最愛]，或將其釘選到入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="aa40d-119">You can add this blade to Favorites or pin it to the portal dashboard.</span></span>

3. <span data-ttu-id="aa40d-120">在 [Azure Active Directory] 刀鋒視窗中，選取 [授權]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-120">On the **Azure Active Directory** blade, select **Licenses**.</span></span> <span data-ttu-id="aa40d-121">這會開啟一個刀鋒視窗，您可以在其中查看及管理租用戶中的所有可授權產品。</span><span class="sxs-lookup"><span data-stu-id="aa40d-121">This opens a blade where you can see and manage all licensable products in the tenant.</span></span>

4. <span data-ttu-id="aa40d-122">在 [所有產品] 下，選取產品名稱，以選取 Office 365 Enterprise E3 和 Enterprise Mobility + Security。</span><span class="sxs-lookup"><span data-stu-id="aa40d-122">Under **All products**, select both Office 365 Enterprise E3 and Enterprise Mobility + Security by selecting the product names.</span></span> <span data-ttu-id="aa40d-123">若要啟動指派，選取刀鋒視窗頂端的 [指派]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-123">To start the assignment, select **Assign** at the top of the blade.</span></span>

   ![所有產品、指派授權](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. <span data-ttu-id="aa40d-125">在 [指派授權] 刀鋒視窗中，按一下 [使用者和群組] 以開啟 [使用者和群組] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa40d-125">On the **Assign license** blade, click **Users and groups** to open the **Users and groups** blade.</span></span> <span data-ttu-id="aa40d-126">搜尋群組名稱人力資源部門、選取群組，然後請務必按一下刀鋒視窗底部的 [選取] 來確認。</span><span class="sxs-lookup"><span data-stu-id="aa40d-126">Search for the group name *HR Department*, select the group, and then be sure to confirm by clicking **Select** at the bottom of the blade.</span></span>

   ![選取群組](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. <span data-ttu-id="aa40d-128">在 [指派授權] 刀鋒視窗中，按一下 [指派選項 (選用)]，便會顯示我們先前選取的兩個產品中所包含的所有服務方案。</span><span class="sxs-lookup"><span data-stu-id="aa40d-128">On the **Assign license** blade, click **Assignment options (optional)**, which displays all service plans included in the two products that we selected previously.</span></span> <span data-ttu-id="aa40d-129">尋找 **Yammer Enterprise** 並將它**關閉**，以從產品授權停用該服務。</span><span class="sxs-lookup"><span data-stu-id="aa40d-129">Find **Yammer Enterprise** and turn it **Off** to disable that service from the product license.</span></span> <span data-ttu-id="aa40d-130">按一下 [指派選項] 底部的 [確定] 來確認。</span><span class="sxs-lookup"><span data-stu-id="aa40d-130">Confirm by clicking **OK** at the bottom of **Assignment options**.</span></span>

   ![指派選項](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. <span data-ttu-id="aa40d-132">若要完成指派，在 [指派授權] 刀鋒視窗中，按一下刀鋒視窗底部的 [指派]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-132">To complete the assignment, on the **Assign license** blade, click **Assign** at the bottom of the blade.</span></span>

8. <span data-ttu-id="aa40d-133">右上角顯示的通知會顯示程序的狀態和結果。</span><span class="sxs-lookup"><span data-stu-id="aa40d-133">A notification is displayed in the upper-right corner that shows the status and outcome of the process.</span></span> <span data-ttu-id="aa40d-134">如果無法完成指派給群組 (例如，因為群組中已存在的授權)，按一下通知以檢視失敗的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aa40d-134">If the assignment to the group couldn't be completed (for example, because of pre-existing licenses in the group), click the notification to view details of the failure.</span></span>

<span data-ttu-id="aa40d-135">我們現在已指定「人力資源部門」群組的授權範本。</span><span class="sxs-lookup"><span data-stu-id="aa40d-135">We've now specified a license template for the HR Department group.</span></span> <span data-ttu-id="aa40d-136">在 Azure AD 中的背景處理已開始處理該群組的所有現有成員。</span><span class="sxs-lookup"><span data-stu-id="aa40d-136">A background process in Azure AD has been started to process all existing members of that group.</span></span> <span data-ttu-id="aa40d-137">此初始作業可能需要一些時間，依群組的目前大小而定。</span><span class="sxs-lookup"><span data-stu-id="aa40d-137">This initial operation might take some time, depending on the current size of the group.</span></span> <span data-ttu-id="aa40d-138">在下一個步驟中，我們將說明如何確認處理程序已完成，並且決定是否需要進一步注意以解決問題。</span><span class="sxs-lookup"><span data-stu-id="aa40d-138">In the next step, we'll describe how to verify that the process has finished and determine if further attention is required to resolve problems.</span></span>

> [!NOTE]
> <span data-ttu-id="aa40d-139">您可以從 Azure AD 中的其他位置︰**使用者和群組**啟動相同的指派。</span><span class="sxs-lookup"><span data-stu-id="aa40d-139">You can start the same assignment from an alternative location: **Users and groups** in Azure AD.</span></span> <span data-ttu-id="aa40d-140">移至 [Azure Active Directory] > [使用者和群組] > [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-140">Go to **Azure Active Directory** > **Users and groups** > **All groups**.</span></span> <span data-ttu-id="aa40d-141">然後尋找群組並加以選取，而後移至 [授權] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aa40d-141">Then find the group, select it, and go to the **Licenses** tab.</span></span> <span data-ttu-id="aa40d-142">刀鋒視窗頂端的 [指派] 按鈕會開啟授權指派刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa40d-142">The **Assign** button on top of the blade opens the license assignment blade.</span></span>

## <a name="step-2-verify-that-the-initial-assignment-has-finished"></a><span data-ttu-id="aa40d-143">步驟 2︰確認已完成初始指派</span><span class="sxs-lookup"><span data-stu-id="aa40d-143">Step 2: Verify that the initial assignment has finished</span></span>

1. <span data-ttu-id="aa40d-144">移至 [Azure Active Directory] > [使用者和群組] > [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-144">Go to **Azure Active Directory** > **Users and groups** > **All groups**.</span></span> <span data-ttu-id="aa40d-145">然後尋找獲得授權指派的「人力資源部門」 群組。</span><span class="sxs-lookup"><span data-stu-id="aa40d-145">Then find the **HR Department** group that licenses were assigned to.</span></span>

2. <span data-ttu-id="aa40d-146">在 [人力資源部門] 群組刀鋒視窗中，選取 [授權]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-146">On the **HR Department** group blade, select **Licenses**.</span></span> <span data-ttu-id="aa40d-147">可讓您快速確認授權是否已完全指派給使用者，以及是否有任何錯誤需要探究。</span><span class="sxs-lookup"><span data-stu-id="aa40d-147">This lets you quickly confirm if licenses have been fully assigned to users and if there are any errors that you need to look into.</span></span> <span data-ttu-id="aa40d-148">可用資訊如下：</span><span class="sxs-lookup"><span data-stu-id="aa40d-148">The following information is available:</span></span>

   - <span data-ttu-id="aa40d-149">目前指派給群組的產品授權清單。</span><span class="sxs-lookup"><span data-stu-id="aa40d-149">List of product licenses that are currently assigned to the group.</span></span> <span data-ttu-id="aa40d-150">選取項目來顯示已啟用且要進行變更的特定服務。</span><span class="sxs-lookup"><span data-stu-id="aa40d-150">Select an entry to show the specific services that have been enabled and to make changes.</span></span>

   - <span data-ttu-id="aa40d-151">對群組進行的最新授權變更狀態 (變更是否正在處理，或是否已完成所有使用者成員的處理)。</span><span class="sxs-lookup"><span data-stu-id="aa40d-151">Status of the latest license changes that were made to the group (if the changes are being processed or if processing has finished for all user members).</span></span>

   - <span data-ttu-id="aa40d-152">因為無法獲得授權指派而處於錯誤狀態的使用者相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aa40d-152">Information about users who are in an error state because licenses couldn't be assigned to them.</span></span>

   ![指派選項](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. <span data-ttu-id="aa40d-154">如需授權處理的詳細資訊，請參閱 [Azure Active Directory] > [使用者和群組] > 群組名稱 > [稽核記錄]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-154">See more detailed information about license processing under **Azure Active Directory** > **Users and groups** > *group name* > **Audit logs**.</span></span> <span data-ttu-id="aa40d-155">請注意下列活動：</span><span class="sxs-lookup"><span data-stu-id="aa40d-155">Note the following activities:</span></span>

   - <span data-ttu-id="aa40d-156">活動︰**開始將群組型授權套用至使用者**。</span><span class="sxs-lookup"><span data-stu-id="aa40d-156">Activity: **Start applying group based license to users**.</span></span> <span data-ttu-id="aa40d-157">當我們的系統拾取群組的授權指派變更，並開始將其套用到所有使用者成員時，就會進行記錄。</span><span class="sxs-lookup"><span data-stu-id="aa40d-157">This is logged when the system picks up the license-assignment change on the group and starts applying it to all user members.</span></span> <span data-ttu-id="aa40d-158">它包含已進行之變更的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aa40d-158">It contains information about the change that was made.</span></span>

   - <span data-ttu-id="aa40d-159">活動︰**完成將群組型授權套用至使用者**。</span><span class="sxs-lookup"><span data-stu-id="aa40d-159">Activity: **Finish applying group based license to users**.</span></span> <span data-ttu-id="aa40d-160">當系統完成處理群組中的所有使用者時，就會進行記錄。</span><span class="sxs-lookup"><span data-stu-id="aa40d-160">This is logged when the system finishes processing all users in the group.</span></span> <span data-ttu-id="aa40d-161">它包含已成功處理的使用者人數和無法獲得群組授權指派的使用者人數之摘要。</span><span class="sxs-lookup"><span data-stu-id="aa40d-161">It contains a summary of how many users were successfully processed and how many users couldn't be assigned group licenses.</span></span>

   <span data-ttu-id="aa40d-162">[閱讀本節](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity)以深入了解如何使用稽核記錄，以分析群組型授權所做的變更。</span><span class="sxs-lookup"><span data-stu-id="aa40d-162">[Read this section](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) to learn more about how audit logs can be used to analyze changes made by group-based licensing.</span></span>

## <a name="step-3-check-for-license-problems-and-resolve-them"></a><span data-ttu-id="aa40d-163">步驟 3︰檢查授權問題及解決這些問題</span><span class="sxs-lookup"><span data-stu-id="aa40d-163">Step 3: Check for license problems and resolve them</span></span>

1. <span data-ttu-id="aa40d-164">移至 [Azure Active Directory] > [使用者和群組] > [所有群組]，然後尋找獲得授權指派的「人力資源部門」群組。</span><span class="sxs-lookup"><span data-stu-id="aa40d-164">Go to **Azure Active Directory** > **Users and groups** > **All groups**, and find the **HR Department** group that licenses were assigned to.</span></span>
2. <span data-ttu-id="aa40d-165">在 [人力資源部門] 群組刀鋒視窗中，選取 [授權]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-165">On the **HR Department** group blade, select **Licenses**.</span></span> <span data-ttu-id="aa40d-166">刀鋒視窗頂端的通知顯示有 10 位使用者無法獲得授權指派。</span><span class="sxs-lookup"><span data-stu-id="aa40d-166">The notification on top of the blade shows that there are 10 users that licenses couldn't be assigned to.</span></span> <span data-ttu-id="aa40d-167">按一下通知，隨即開啟一份此群組為授權錯誤狀態的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="aa40d-167">Clicking it opens a list of all users in a licensing-error state for this group.</span></span>
3. <span data-ttu-id="aa40d-168">[失敗的指派] 資料行告訴我們，兩個產品授權都無法指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="aa40d-168">The **Failed assignments** column tells us that both product licenses couldn't be assigned to the users.</span></span> <span data-ttu-id="aa40d-169">[失敗的前幾大原因] 資料行包含失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="aa40d-169">The **Top reason for failure** column contains the cause of the failure.</span></span> <span data-ttu-id="aa40d-170">在此案例中為 [衝突的服務方案]。</span><span class="sxs-lookup"><span data-stu-id="aa40d-170">In this case, it's **Conflicting service plans**.</span></span>

   ![失敗的指派](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. <span data-ttu-id="aa40d-172">選取使用者以開啟 [授權] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa40d-172">Select a user to open the **Licenses** blade.</span></span> <span data-ttu-id="aa40d-173">此刀鋒視窗會顯示目前指派給此使用者的所有授權。</span><span class="sxs-lookup"><span data-stu-id="aa40d-173">This blade shows all licenses that are currently assigned to the user.</span></span> <span data-ttu-id="aa40d-174">在此範例中，使用者擁有繼承自 **Kiosk 使用者** 群組的 Office 365 Enterprise E1 授權。</span><span class="sxs-lookup"><span data-stu-id="aa40d-174">In this example, the user has the Office 365 Enterprise E1 license that was inherited from the **Kiosk users** group.</span></span> <span data-ttu-id="aa40d-175">這會與系統嘗試從**人力資源部門**群組套用的 E3 授權衝突。</span><span class="sxs-lookup"><span data-stu-id="aa40d-175">This conflicts with the E3 license that the system tried to apply from the **HR Department** group.</span></span> <span data-ttu-id="aa40d-176">如此一來，該群組沒有任何授權會指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="aa40d-176">As a result, none of the licenses from that group has been assigned to the user.</span></span>

   ![檢視使用者的授權](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. <span data-ttu-id="aa40d-178">若要解決這個衝突，從 **Kiosk 使用者**群組移除使用者。</span><span class="sxs-lookup"><span data-stu-id="aa40d-178">To solve this conflict, remove the user from the **Kiosk users** group.</span></span> <span data-ttu-id="aa40d-179">在 Azure AD 處理變更之後，會正確指派**人力資源部門**授權。</span><span class="sxs-lookup"><span data-stu-id="aa40d-179">After Azure AD processes the change, the **HR Department** licenses are correctly assigned.</span></span>

   ![已正確指派的授權](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a><span data-ttu-id="aa40d-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa40d-181">Next steps</span></span>

<span data-ttu-id="aa40d-182">若要深入了解透過群組管理授權的功能集，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="aa40d-182">To learn more about the feature set for license management through groups, see the following articles:</span></span>

* [<span data-ttu-id="aa40d-183">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="aa40d-183">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="aa40d-184">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="aa40d-184">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="aa40d-185">如何將個別的已授權使用者移轉成 Azure Active Directory 中的群組型授權 (英文)</span><span class="sxs-lookup"><span data-stu-id="aa40d-185">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="aa40d-186">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="aa40d-186">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
