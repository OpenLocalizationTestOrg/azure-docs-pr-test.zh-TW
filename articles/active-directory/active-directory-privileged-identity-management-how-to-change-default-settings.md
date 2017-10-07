---
title: "aaaHow toomanage 角色啟用設定 |Microsoft 文件"
description: "了解如何 toochange hello 以 hello Azure Active Directory Privileged Identity Management 延伸模組的預設設定為特殊權限的身分識別。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>如何在 Azure AD Privileged Identity Management toomanage 角色啟用設定
特殊權限的角色系統管理員可以自訂 Azure AD Privileged Identity Management (PIM) 在其組織中，其中包括變更 hello 啟用中的合格的角色指派的使用者體驗。

## <a name="manage-hello-role-activation-settings"></a>管理 hello 角色啟用設定
1. 移 toohello [Azure 入口網站](https://portal.azure.com)和選取 hello **Azure AD Privileged Identity Management** hello 儀表板中的應用程式。
2. 選取 [管理特殊權限角色] > [設定] > [特殊權限角色]。
3. 選擇 hello 角色其設定您想要 toomanage。

在 hello [設定] 頁面上，針對每個角色，有一些您可以設定的設定。 這些設定只會影響身為合格系統管理員 (而不是永久系統管理員) 的使用者。

**啟用**: hello 的時間，以小時為單位的角色在過期前維持作用中。 此時間可介於 1 到 72 小時。

**通知**： 您可以選擇是否 hello 系統會傳送電子郵件 tooadmins 確認他們已啟用的角色。 這對偵測未經授權或不合法的啟用而言相當有用。

**事件/要求票證**： 您可以選擇啟用其角色時，不論是否編號 toorequire 合格 admins tooinclude 票證。 當您執行角色存取稽核時，這會相當有用。

**Multi-factor Authentication**： 您可以選擇是否 toorequire 使用者 tooverify mfa，才能啟用其角色其身分識別。 它們只能有 tooverify 每個工作階段，每次在啟用角色不一次。 當您啟用 MFA 記住有兩個秘訣 tookeep:

* 具有 Microsoft 帳戶的電子郵件地址的使用者 (通常@outlook.com，但並非一定) 無法為 Azure MFA 進行註冊。 如果您想 tooassign 角色 toousers 與 Microsoft 帳戶，您應該讓它們永久的系統管理員或停用 MFA，該角色。
* 您無法將 Azure AD 和 Office365 中高特殊權限角色的 MFA 停用。 這是一項安全功能，因為這些角色應該嚴密地受到保護：  
  
  * 應用程式管理員
  * 應用程式 Proxy 伺服器管理員
  * 計費管理員  
  * 規範管理員  
  * CRM 服務管理員
  * 客戶 LockBox 存取核准者
  * 目錄寫入器  
  * Exchange 系統管理員  
  * 全域管理員
  * Intune 服務管理員
  * 信箱管理員  
  * 合作夥伴第 1 層支援  
  * 合作夥伴第 2 層支援  
  * 特殊權限角色管理員   
  * 安全性系統管理員  
  * SharePoint 管理員  
  * 商務用 Skype 的管理員  
  * 使用者帳戶管理員  

如需使用 MFA PIM 的詳細資訊，請參閱[如何 tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md)。

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

