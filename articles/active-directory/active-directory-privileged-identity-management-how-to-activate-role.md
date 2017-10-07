---
title: "aaaHow tooactivate 或停用角色 |Microsoft 文件"
description: "了解如何 tooactivate 角色的特殊權限身分識別與 hello Azure Privileged Identity Management 的應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>如何 tooactivate 或停用 Azure AD Privileged Identity Management 中的角色
Azure Active Directory (AD) 的權限身分管理可簡化企業如何管理 Azure AD 中的特殊權限的存取 tooresources 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。  

如果您已經進行了適合管理的角色，這表示當您需要特殊權限的 tooperform 動作時，您可以啟用該角色。 例如，如果您偶爾會管理 Office 365 功能，則貴組織的特殊權限角色管理員可能不會讓您成為永久全域管理員，因為該角色也會影響其他服務。 他們反而會讓您符合 Azure AD 角色 (例如「Exchange Online 管理員」) 的資格。 您可以 tooactivate 該角色而且時，要求您需要其權限，然後您就有預定的時間期間的系統管理控制權。

本文適用於需要 tooactivate 系統管理員在 Azure AD Privileged Identity Management (PIM) 中的角色。 它會引導您透過 hello 步驟 tooactivate 角色當您需要 hello 權限，而且當您完成時，停用 hello 角色。 此外，特殊權限的角色系統管理員可以要求核准 tooactivate （預覽） 的角色。 在這裡深入了解 [PIM 核准工作流程](./privileged-identity-management/azure-ad-pim-approval-workflow.md)。

## <a name="add-hello-privileged-identity-management-application"></a>新增 hello Privileged Identity Management 的應用程式
Hello Azure AD Privileged Identity Management 的應用程式用於 hello [Azure 入口網站](https://portal.azure.com/)toorequest 啟用角色，即使您將 toooperate 中另一個入口網站或 PowerShell。 如果您的 Azure 入口網站上沒有 hello Azure AD Privileged Identity Management 的應用程式，請遵循啟動這些步驟 tooget。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取您在 hello 右上角的 hello Azure 入口網站，與您將您的選取 hello 目錄中的使用者名稱進行操作。
3. 選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。
4. 請檢查**Pin toodashboard** ，然後按一下**建立**。 hello Privileged Identity Management 的應用程式會開啟。

## <a name="activate-a-role"></a>啟用角色
當您需要 tootake 角色上的時，您可以藉由選取 hello 要求啟用**我角色**hello Azure AD Privileged Identity Management 的應用程式中的導覽選項的左瀏覽資料行。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello Azure AD Privileged Identity Management 磚。
2. 選取 [我的角色]。 指派的合格角色的清單會出現在 hello hello 頁面頂端的 hello 分組。
3. 選取角色 tooactivate。
4. 選取 [ **啟用**]。 hello**要求角色啟用**刀鋒視窗隨即出現。
5. 某些角色需要多重要素驗證 (MFA)，才能啟動 hello 角色。 您只需要 tooauthenticate 一次每個工作階段。
   
    ![在啟用角色之前先以 MFA 驗證 - 螢幕擷取畫面][2]
6. Hello 文字欄位中輸入 hello hello 啟用要求的原因。  某些角色需要 toosupply 疑難票證號碼。
7. 選取 [確定] 。  如果 hello 角色不需要核准，它現在已啟用，而且 hello 角色出現在 hello （正下方 hello 符合資格的角色指派清單） 的使用中角色清單。 如果 hello[角色需要核准](./privileged-identity-management/azure-ad-pim-approval-workflow.md)tooactivate，快顯通知會短暫出現 hello 右上角的瀏覽器 hello 要求正在等待核准的通知。

    ![要求擱置通知 - 螢幕擷取畫面][3]

## <a name="deactivate-a-role"></a>停用角色
角色一經啟用，就會在達到時間限制 (合格的持續時間) 時自動停用。

如果您提早完成管理工作，您也可以停用手動中 hello Azure AD Privileged Identity Management 的應用程式的角色。  選取**我角色**，選擇您完成時的 hello 角色使用從 hello**作用中的角色指派**群組，然後選取**停用**。  

## <a name="cancel-a-pending-request"></a>取消擱置要求
不需要啟用需要核准之角色的 hello 事件中，您可以隨時取消暫止要求。 只需選取 hello**我角色**hello Azure AD Privileged Identity Management 的應用程式中的導覽選項的左瀏覽資料行。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello Azure AD Privileged Identity Management 磚。
2. 選取 [我的角色]。 指派的合格角色的清單會出現在 hello hello 頁面頂端的 hello 分組。
3. 選取角色。
4. 選取 hello**啟用正在等待核准**橫幅 hello 角色啟用詳細資料 刀鋒視窗上。
5. 選取**取消**頂端的 hello hello**等待核准**刀鋒視窗。

   ![取消擱置要求螢幕擷取畫面][4]

## <a name="next-steps"></a>後續步驟
如果您想要了解更多關於 Azure AD Privileged Identity Management，hello 下列連結有更多的資訊。

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
