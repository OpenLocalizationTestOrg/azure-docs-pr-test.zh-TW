---
title: "新使用者 tooAzure aaaAdd Active Directory |Microsoft 文件"
description: "說明如何在 Azure Active Directory tooadd 新使用者。"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>快速入門： 加入新使用者 tooAzure Active Directory
本文說明 tooadd hello Azure Active Directory (Azure AD) 中您組織中的新使用者如何當其中一一次使用 hello Azure 入口網站或同步處理內部部署 Windows Server AD 使用者帳戶資料。 

## <a name="add-cloud-based-users"></a>新增雲端式使用者
1. 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取 [Azure Active Directory]**Azure Active Directory**，然後選取 [使用者和群組]。
3. 在 hello**使用者和群組**刀鋒視窗中，選取**所有使用者**，然後選取**新使用者**。
   ![選取 hello Add 命令](./media/add-users-azure-active-directory/add-user.png)
4. Hello 使用者輸入的詳細資訊，例如**名稱**和**使用者名**。 hello hello 使用者名稱的網域名稱部分必須 hello 初始預設網域名稱"[網域名稱].onmicrosoft.com 」 或已驗證非同盟[自訂網域名稱](add-custom-domain.md)例如"contoso.com"。
5. 複製或其他方式的附註 hello，讓您能夠提供其 toohello 使用者完成此程序之後產生的使用者密碼。
6. （選擇性） 您可以開啟，並填寫 hello 資訊在 hello**設定檔**刀鋒視窗，hello**群組**刀鋒視窗中或使用 hello**目錄角色**hello 使用者 刀鋒視窗。 如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。
7. 在 hello**使用者**刀鋒視窗中，選取**建立**。
8. 安全地散發 hello 產生密碼 toohello 新使用者，讓 hello 使用者可以登入。

> [!TIP]
> 您也可以同步處理內部部署 Windows Server AD 中的使用者帳戶資料。 Microsoft 的身分識別解決方案跨越內部部署和雲端架構的功能，建立單一使用者識別進行驗證和授權 tooall 資源，不論位置為何。 我們稱之為混合式身分識別。 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)可以是您的內部部署目錄與 Azure Active Directory 混合式身分識別案例使用的 toointegrate。 這可讓您 tooprovide 通用識別身分為您的 Office 365、 Azure 和 SaaS 應用程式的使用者與 Azure AD 整合。 

## <a name="delete-users-from-azure-ad"></a>從 Azure AD 刪除使用者
1. 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取 [使用者和群組]。
3. 在 hello**使用者和群組**刀鋒視窗中，選取 hello 使用者 toodelete 從 hello 清單。 
4. 在 hello 選使用者的 hello 刀鋒視窗，選取 **概觀**，然後 hello 命令列中，選取**刪除**。
   ![選取 hello Add 命令](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>詳細資訊 
* [新增外部使用者](active-directory-users-create-external-azure-portal.md)

* [在您的 Azure AD 中指派使用者 tooa 角色](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>後續步驟
本快速入門中，您學到如何新增使用者 tooAzure tooadd AD Premium。 

您可以使用 hello hello Azure 入口網站中的下列 Azure AD 中的連結 toocreate 新的使用者。

> [!div class="nextstepaction"]
> [新增使用者 tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
