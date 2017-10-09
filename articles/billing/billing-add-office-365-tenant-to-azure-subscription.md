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
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>將 Office 365 租用戶 tooan Azure 訂用帳戶產生關聯
連結個別 Azure 和 Office 365 訂用帳戶，讓您可以從您的 Azure 訂用帳戶存取 hello Office 365 租用戶。 toolink 訂用帳戶，登入 tooAzure 以 hello Azure 服務系統管理員帳戶，新增一個目錄，並將 hello Office 365 組織帳戶 toohello Azure Active Directory 租用戶。

如果您要讓 Azure Active Directory 執行個體中的使用者擁有 Office 365 訂用帳戶，或您有 Office 365 帳戶但沒有 Azure 帳戶，請參閱[使用 Office 365 帳戶註冊 Azure](billing-use-existing-office-365-account-azure-subscription.md)。 

## <a name="before-you-begin"></a>開始之前
* 您必須擁有 hello hello Azure 訂用帳戶服務系統管理員認證。 共同系統管理員帳戶不能執行某些 hello 本文中的步驟。 toochange 您的服務系統管理員，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription)。
* 您必須擁有 hello hello Office 365 租用戶的全域管理員認證。
* hello hello 服務系統管理員的電子郵件地址不能在 hello Office 365 租用戶。
* hello hello 服務系統管理員的電子郵件地址必須不符合任何 hello Office 365 租用戶的全域管理員。
* 如果您使用 Microsoft 帳戶和組織帳戶是電子郵件地址，暫時變更 hello 服務管理員 Azure 訂用帳戶 toouse 的另一個 Microsoft 帳戶。 您可以在 hello 建立 Microsoft 帳戶[Microsoft 帳戶註冊頁面](https://signup.live.com/)。

## <a name="link-office-365-tenant-tooazure-subscription"></a>連結 Office 365 租用戶 tooAzure 訂用帳戶
tooassociate hello Office 365 租用戶 toohello Azure 訂用帳戶，請遵循下列步驟：

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>步驟 1： 加入 Office 365 租用戶 tooyour Azure 訂用帳戶

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)與 hello 服務系統管理員認證。

    ![Azure 登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Hello 左窗格中，選取**ACTIVE DIRECTORY**。 您不應該看到 hello Office 365 租用戶。 如果您看到它，請跳過[步驟 2: hello Azure 訂用帳戶相關聯的變更 hello 目錄](#Step2)。
   
   ![Active Directory 項目的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. 選取 新增 > 目錄 > 自訂建立。
   
    ![Azure Active Directory 自訂建立的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. 在 hello**加入目錄**頁面的 **目錄**，選取**使用現有目錄**。 然後選取**我已準備好立即登出的 toobe**，然後選取**完成**![完成圖示](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。
   
    ![[使用現有的目錄] 螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. 您登出之後，使用 Office 365 租用戶的 hello 全域管理員的認證登入。
   
    ![Office 365 全域系統管理員登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. 選取 [繼續]。
   
    ![驗證的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. 按一下 [立即登出]。
   
    ![登出的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)與 hello 服務系統管理員認證。
   
    ![Azure 登入的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. 您應該會看到您的 Office 365 租用戶 hello 儀表板中。
   
    ![儀表板的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>步驟 2： 變更與 hello Azure 訂用帳戶相關聯的 hello 目錄
   
1. 選取 [Settings] \(設定) 。
   
    ![Azure 傳統入口網站設定圖示的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. 選取您的 Azure 訂用帳戶，然後 [編輯目錄]。

    ![Azure 訂用帳戶編輯目錄的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. 選取 [下一步] ![下一步圖示](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png)。
   
    ![「 變更 hello 相關聯的目錄"螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. 檢閱受影響的 hello 帳戶。 所有的共同管理員及[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)移除具有 hello 現有的資源群組中的指派存取權的使用者。 您會收到 hello 警告只會提及 hello 移除共同管理員。
      
    ![如果螢幕擷取畫面顯示 hello toobe 移除共同管理員帳戶。](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![螢幕擷取畫面，顯示範例使用者帳戶 toobe 移除。](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. 選取 [完成] ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>步驟 3： 將您的 Office 365 組織帳戶新增為共同管理員 toohello Azure Active Directory 租用戶
   
1. 選取 hello**管理員**索引標籤，然後選取**新增**。
   
    ![Azure 傳統入口網站設定系統管理員索引標籤的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. 輸入您的 Office 365 租用戶的組織帳戶選取 hello Azure 的訂用帳戶，然後選取**完成**![完成圖示](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)。
   
    ![Azure 新增共同管理員對話方塊的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. 返回 toohello**管理員** 索引標籤。您應該會看到顯示為共同管理員的 hello 組織帳戶。
   
    ![系統管理員索引標籤的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  測試存取 tooAzure 與 hello 共同系統管理員帳戶。
   
    a. Azure 傳統入口網站登出 hello。
   
    b. 開啟 hello [Azure 入口網站](https://portal.azure.com/)。
   
    c. 輸入 hello hello 共同系統管理員認證，然後選取**登入**。
   
    ![Azure 登入頁面的螢幕擷取畫面](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。


