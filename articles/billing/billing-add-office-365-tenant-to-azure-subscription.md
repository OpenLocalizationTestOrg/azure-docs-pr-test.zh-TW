---
title: "aaaUse Office 365 租用戶與 Azure 訂用帳戶 |Microsoft 文件"
description: "深入了解如何 tooadd Office 365 目錄 （租用戶） tooan Azure 訂用帳戶。"
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
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="bac40-103">將 Office 365 租用戶 tooan Azure 訂用帳戶產生關聯</span><span class="sxs-lookup"><span data-stu-id="bac40-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="bac40-104">連結個別 Azure 和 Office 365 訂用帳戶，讓您可以從您的 Azure 訂用帳戶存取 hello Office 365 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="bac40-105">toolink 訂用帳戶，登入 tooAzure 以 hello Azure 服務系統管理員帳戶，新增一個目錄，並將 hello Office 365 組織帳戶 toohello Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="bac40-106">如果您要讓 Azure Active Directory 執行個體中的使用者擁有 Office 365 訂用帳戶，或您有 Office 365 帳戶但沒有 Azure 帳戶，請參閱[使用 Office 365 帳戶註冊 Azure](billing-use-existing-office-365-account-azure-subscription.md)。</span><span class="sxs-lookup"><span data-stu-id="bac40-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="bac40-107">開始之前</span><span class="sxs-lookup"><span data-stu-id="bac40-107">Before you begin</span></span>
* <span data-ttu-id="bac40-108">您必須擁有 hello hello Azure 訂用帳戶服務系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="bac40-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="bac40-109">共同系統管理員帳戶不能執行某些 hello 本文中的步驟。</span><span class="sxs-lookup"><span data-stu-id="bac40-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="bac40-110">toochange 您的服務系統管理員，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription)。</span><span class="sxs-lookup"><span data-stu-id="bac40-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="bac40-111">您必須擁有 hello hello Office 365 租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="bac40-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="bac40-112">hello hello 服務系統管理員的電子郵件地址不能在 hello Office 365 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="bac40-113">hello hello 服務系統管理員的電子郵件地址必須不符合任何 hello Office 365 租用戶的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="bac40-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="bac40-114">如果您使用 Microsoft 帳戶和組織帳戶是電子郵件地址，暫時變更 hello 服務管理員 Azure 訂用帳戶 toouse 的另一個 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="bac40-115">您可以在 hello 建立 Microsoft 帳戶[Microsoft 帳戶註冊頁面](https://signup.live.com/)。</span><span class="sxs-lookup"><span data-stu-id="bac40-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="bac40-116">連結 Office 365 租用戶 tooAzure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bac40-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="bac40-117">tooassociate hello Office 365 租用戶 toohello Azure 訂用帳戶，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bac40-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="bac40-118">步驟 1： 加入 Office 365 租用戶 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bac40-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="bac40-119">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)與 hello 服務系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="bac40-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Azure 登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="bac40-121">Hello 左窗格中，選取**ACTIVE DIRECTORY**。</span><span class="sxs-lookup"><span data-stu-id="bac40-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="bac40-122">您不應該看到 hello Office 365 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="bac40-123">如果您看到它，請跳過[步驟 2: hello Azure 訂用帳戶相關聯的變更 hello 目錄](#Step2)。</span><span class="sxs-lookup"><span data-stu-id="bac40-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Active Directory 項目的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="bac40-125">選取 新增 > 目錄 > 自訂建立。</span><span class="sxs-lookup"><span data-stu-id="bac40-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Azure Active Directory 自訂建立的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="bac40-127">在 hello**加入目錄**頁面的 **目錄**，選取**使用現有目錄**。</span><span class="sxs-lookup"><span data-stu-id="bac40-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="bac40-128">然後選取**我已準備好立即登出的 toobe**，然後選取**完成**![完成圖示](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="bac40-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![[使用現有的目錄] 螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="bac40-130">您登出之後，使用 Office 365 租用戶的 hello 全域管理員的認證登入。</span><span class="sxs-lookup"><span data-stu-id="bac40-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Office 365 全域系統管理員登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="bac40-132">選取 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="bac40-132">Select **Continue**.</span></span>
   
    ![驗證的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="bac40-134">按一下 [立即登出]。</span><span class="sxs-lookup"><span data-stu-id="bac40-134">Select **Sign out now**.</span></span>
   
    ![登出的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="bac40-136">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)與 hello 服務系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="bac40-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Azure 登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="bac40-138">您應該會看到您的 Office 365 租用戶 hello 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="bac40-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![儀表板的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="bac40-140"><a name="Step2"></a>步驟 2： 變更與 hello Azure 訂用帳戶相關聯的 hello 目錄</span><span class="sxs-lookup"><span data-stu-id="bac40-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="bac40-141">選取 [Settings] \(設定) 。</span><span class="sxs-lookup"><span data-stu-id="bac40-141">Select **Settings**.</span></span>
   
    ![Azure 傳統入口網站設定圖示的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="bac40-143">選取您的 Azure 訂用帳戶，然後 [編輯目錄]。</span><span class="sxs-lookup"><span data-stu-id="bac40-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Azure 訂用帳戶編輯目錄的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="bac40-145">選取 [下一步] ![下一步圖示](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="bac40-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![「 變更 hello 相關聯的目錄"螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="bac40-147">檢閱受影響的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-147">Review hello affected accounts.</span></span> <span data-ttu-id="bac40-148">所有的共同管理員及[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)移除具有 hello 現有的資源群組中的指派存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="bac40-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="bac40-149">您會收到 hello 警告只會提及 hello 移除共同管理員。</span><span class="sxs-lookup"><span data-stu-id="bac40-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![如果螢幕擷取畫面顯示 hello toobe 移除共同管理員帳戶。](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![螢幕擷取畫面，顯示範例使用者帳戶 toobe 移除。](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="bac40-152">選取 [完成] ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="bac40-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="bac40-153">步驟 3： 將您的 Office 365 組織帳戶新增為共同管理員 toohello Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="bac40-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="bac40-154">選取 hello**管理員**索引標籤，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="bac40-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Azure 傳統入口網站設定系統管理員索引標籤的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="bac40-156">輸入您的 Office 365 租用戶的組織帳戶選取 hello Azure 的訂用帳戶，然後選取**完成**![完成圖示](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。</span><span class="sxs-lookup"><span data-stu-id="bac40-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Azure 新增共同管理員對話方塊的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="bac40-158">返回 toohello**管理員** 索引標籤。您應該會看到顯示為共同管理員的 hello 組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![系統管理員索引標籤的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="bac40-160">測試存取 tooAzure 與 hello 共同系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="bac40-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="bac40-161">a.</span><span class="sxs-lookup"><span data-stu-id="bac40-161">a.</span></span> <span data-ttu-id="bac40-162">Azure 傳統入口網站登出 hello。</span><span class="sxs-lookup"><span data-stu-id="bac40-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="bac40-163">b.</span><span class="sxs-lookup"><span data-stu-id="bac40-163">b.</span></span> <span data-ttu-id="bac40-164">開啟 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="bac40-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="bac40-165">c.</span><span class="sxs-lookup"><span data-stu-id="bac40-165">c.</span></span> <span data-ttu-id="bac40-166">輸入 hello hello 共同系統管理員認證，然後選取**登入**。</span><span class="sxs-lookup"><span data-stu-id="bac40-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Azure 登入頁面的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="bac40-168">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="bac40-168">Need help?</span></span> <span data-ttu-id="bac40-169">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="bac40-169">Contact support.</span></span>
<span data-ttu-id="bac40-170">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="bac40-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


