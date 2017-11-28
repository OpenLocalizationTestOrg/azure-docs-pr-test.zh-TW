---
title: "搭配使用 Office 365 租用戶與 Azure 訂用帳戶 | Microsoft Docs"
description: "了解如何將 Office 365 目錄 (租用戶) 加入至 Azure 訂用帳戶。"
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: 7affb4a83cdb8ababef60e786a3c824e7477ed68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a><span data-ttu-id="f48a6-103">將 Office 365 租用戶與 Azure 訂用帳戶產生關聯</span><span class="sxs-lookup"><span data-stu-id="f48a6-103">Associate an Office 365 tenant to an Azure subscription</span></span>
<span data-ttu-id="f48a6-104">連結個別的 Azure 和 Office 365 訂用帳戶，這樣您就可以從 Azure 訂用帳戶存取 Office 365 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f48a6-104">Link your separate Azure and Office 365 subscriptions so that you can access the Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="f48a6-105">若要連結您的訂用帳戶，請使用 Azure 服務系統管理員帳戶登入 Azure，新增一個目錄，然後將 Office 365 組織帳戶新增到 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f48a6-105">To link your subscriptions, sign in to Azure with the Azure service administrator account, add a directory, and add the Office 365 organizational accounts to the Azure Active Directory tenant.</span></span>

<span data-ttu-id="f48a6-106">如果您要讓 Azure Active Directory 執行個體中的使用者擁有 Office 365 訂用帳戶，或您有 Office 365 帳戶但沒有 Azure 帳戶，請參閱[使用 Office 365 帳戶註冊 Azure](billing-use-existing-office-365-account-azure-subscription.md)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f48a6-107">開始之前</span><span class="sxs-lookup"><span data-stu-id="f48a6-107">Before you begin</span></span>
* <span data-ttu-id="f48a6-108">您必須有 Azure 訂用帳戶服務的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f48a6-108">You must have the credentials of the Azure subscription service administrator.</span></span> <span data-ttu-id="f48a6-109">共同管理員無法執行本文中某些步驟。</span><span class="sxs-lookup"><span data-stu-id="f48a6-109">Co-administrator accounts can't do some of the steps in this article.</span></span> <span data-ttu-id="f48a6-110">若要變更服務管理員，請參閱[如何新增或變更 Azure 管理員角色](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-110">To change your service administrator, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="f48a6-111">您必須有 Office 365 租用戶的全域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f48a6-111">You must have the credentials of a global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="f48a6-112">服務管理員的電子郵件地址不得位於 Office 365 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="f48a6-112">The email address of the service administrator must not be in the Office 365 tenant.</span></span>
* <span data-ttu-id="f48a6-113">服務管理員的電子郵件地址不得符合 Office 365 租用戶的任何全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="f48a6-113">The email address of the service administrator must not match that of any global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="f48a6-114">如果您使用的電子郵件地址同時為 Microsoft 帳戶和組織帳戶，請暫時將 Azure 訂用帳戶的服務管理員變更成使用另一個 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f48a6-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change the service administrator of your Azure subscription to use another Microsoft account.</span></span> <span data-ttu-id="f48a6-115">您可以在 [Microsoft 帳戶註冊頁面](https://signup.live.com/)建立新的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f48a6-115">You can create a Microsoft account at the [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-to-azure-subscription"></a><span data-ttu-id="f48a6-116">將 Office 365 租用戶連結到 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f48a6-116">Link Office 365 tenant to Azure subscription</span></span>
<span data-ttu-id="f48a6-117">若要將 Office 365 租用戶與 Azure 訂用帳戶產生關聯，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="f48a6-117">To associate the Office 365 tenant to the Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a><span data-ttu-id="f48a6-118">步驟 1：將 Office 365 租用戶加入至 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f48a6-118">Step 1: Add Office 365 tenant to your Azure subscription</span></span>

1. <span data-ttu-id="f48a6-119">使用服務管理員認證登入 [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-119">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>

    ![Azure 登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="f48a6-121">在左窗格中選取 [ACTIVE DIRECTORY]。</span><span class="sxs-lookup"><span data-stu-id="f48a6-121">In the left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="f48a6-122">您應該不會看見 Office 365 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f48a6-122">You shouldn't see the Office 365 tenant.</span></span> <span data-ttu-id="f48a6-123">如果有看見租用戶，請跳至[步驟 2：變更與 Azure 訂用帳戶相關聯的目錄](#Step2)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-123">If you see it, skip to [Step 2: Change the directory associated with the Azure subscription](#Step2).</span></span>
   
   ![Active Directory 項目的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="f48a6-125">選取 新增 > 目錄 > 自訂建立。</span><span class="sxs-lookup"><span data-stu-id="f48a6-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Azure Active Directory 自訂建立的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="f48a6-127">在 [新增目錄] 頁面中，於 [目錄] 下方選取 [使用現有的目錄]。</span><span class="sxs-lookup"><span data-stu-id="f48a6-127">On the **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="f48a6-128">接著選取 [我現在已經可以登出]，然後選取 [完成] ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-128">Then select **I am ready to be signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![[使用現有的目錄] 螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="f48a6-130">在您登出之後，使用 Office 365 租用戶的全域系統管理員認證登入。</span><span class="sxs-lookup"><span data-stu-id="f48a6-130">After you are signed out, sign in with the global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Office 365 全域系統管理員登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="f48a6-132">選取 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="f48a6-132">Select **Continue**.</span></span>
   
    ![驗證的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="f48a6-134">按一下 [立即登出]。</span><span class="sxs-lookup"><span data-stu-id="f48a6-134">Select **Sign out now**.</span></span>
   
    ![登出的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="f48a6-136">使用服務管理員認證登入 [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>
   
    ![Azure 登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="f48a6-138">您應該會在儀表板中看到 Office 365 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f48a6-138">You should see your Office 365 tenant in the dashboard.</span></span>
   
    ![儀表板的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="f48a6-140"><a name="Step2"></a>步驟 2：變更與 Azure 訂用帳戶相關聯的目錄</span><span class="sxs-lookup"><span data-stu-id="f48a6-140"><a name="Step2"></a>Step 2: Change the directory associated with the Azure subscription</span></span>
   
1. <span data-ttu-id="f48a6-141">選取 [Settings] \(設定) 。</span><span class="sxs-lookup"><span data-stu-id="f48a6-141">Select **Settings**.</span></span>
   
    ![Azure 傳統入口網站設定圖示的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="f48a6-143">選取您的 Azure 訂用帳戶，然後 [編輯目錄]。</span><span class="sxs-lookup"><span data-stu-id="f48a6-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Azure 訂用帳戶編輯目錄的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="f48a6-145">選取 [下一步] ![下一步圖示](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![[變更相關聯的目錄] 螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="f48a6-147">檢閱受影響的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f48a6-147">Review the affected accounts.</span></span> <span data-ttu-id="f48a6-148">現有資源群組中所有具有指派存取權的共同管理員和[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)使用者也會一併移除。</span><span class="sxs-lookup"><span data-stu-id="f48a6-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in the existing resource groups are removed.</span></span> <span data-ttu-id="f48a6-149">您收到的警告只會提及共同管理員的移除。</span><span class="sxs-lookup"><span data-stu-id="f48a6-149">The warning you receive only mentions the removal of co-administrators.</span></span>
      
    ![顯示將移除之共同管理員帳戶的螢幕擷取畫面。](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![顯示將移除之範例使用者帳戶的螢幕擷取畫面。](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="f48a6-152">選取 [完成] ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a><span data-ttu-id="f48a6-153">步驟 3：將您的 Office 365 組織帳戶新增為 Azure Active Directory 租用戶的共同管理員</span><span class="sxs-lookup"><span data-stu-id="f48a6-153">Step 3: Add your Office 365 organizational accounts as co-administrators to the Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="f48a6-154">選取 [系統管理員] 索引標籤，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f48a6-154">Select the **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Azure 傳統入口網站設定系統管理員索引標籤的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="f48a6-156">輸入您的 Office 365 租用戶組織帳戶，選取 Azure 訂用帳戶，然後選取 [完成] ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-156">Enter an organizational account of your Office 365 tenant, select the Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Azure 新增共同管理員對話方塊的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="f48a6-158">返回 [系統管理員] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f48a6-158">Go back to the **ADMINISTRATORS** tab.</span></span> <span data-ttu-id="f48a6-159">您應該會看到組織帳戶顯示為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="f48a6-159">You should see the organizational account displayed as co-administrator.</span></span>
   
    ![系統管理員索引標籤的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="f48a6-161">測試使用共同管理員帳戶存取 Azure。</span><span class="sxs-lookup"><span data-stu-id="f48a6-161">Test access to Azure with the co-administrator account.</span></span>
   
    <span data-ttu-id="f48a6-162">a.</span><span class="sxs-lookup"><span data-stu-id="f48a6-162">a.</span></span> <span data-ttu-id="f48a6-163">登出 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="f48a6-163">Sign out of the Azure classic portal.</span></span>
   
    <span data-ttu-id="f48a6-164">b.</span><span class="sxs-lookup"><span data-stu-id="f48a6-164">b.</span></span> <span data-ttu-id="f48a6-165">開啟 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="f48a6-165">Open the [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="f48a6-166">c.</span><span class="sxs-lookup"><span data-stu-id="f48a6-166">c.</span></span> <span data-ttu-id="f48a6-167">輸入共同管理員的認證，然後選取 [登入] 。</span><span class="sxs-lookup"><span data-stu-id="f48a6-167">Enter the credentials of the co-administrator, and then select **Sign in**.</span></span>
   
    ![Azure 登入頁面的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="f48a6-169">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="f48a6-169">Need help?</span></span> <span data-ttu-id="f48a6-170">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="f48a6-170">Contact support.</span></span>
<span data-ttu-id="f48a6-171">如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="f48a6-171">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


