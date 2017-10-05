---
title: "設定 Azure AD Privileged Identity Management | Microsoft Docs"
description: "本主題說明何謂 Azure AD Privileged Identity Management，以及如何使用 PIM 改善雲端安全性。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: eb7059368cb80be7dd625f9dc6ad2aab1bad709a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>什麼是 Azure AD Privileged Identity Management？
您可以利用 Azure Active Directory (AD) Privileged Identity Management 來管理、控制和監視組織內的存取行為。 這包括存取 Azure AD 中的資源和其他 Microsoft 線上服務，例如 Office 365 或 Microsoft Intune。  

> [!NOTE]
> 當您將 Azure Active Directory 的 Premium P2 版本授權給系統管理員時，Privileged Identity Management 可供您的整個組織使用。 如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。

組織想要將能夠存取安全資訊或資源的人數降到最低，因為這樣可以降低惡意使用者取得該存取權的機率。 不過，使用者仍然需要在 Azure、Office 365 或 SaaS 應用程式中執行特殊權限作業。 組織可以在 Azure AD 中授與使用者特殊權限，而不需監視這些使用者使用其系統管理權限來執行什麼作業。 Azure AD 特殊權限身分識別管理有助於解決此風險。  

Azure AD Privileged Identity Management 可協助您：  

* 查看哪些使用者是 Azure AD 管理員
* 視需要啟用 Office 365 和 Intune 等 Microsoft Online Services 的 "just-in-time" 系統管理存取權限
* 取得有關系統管理員存取記錄與系統管理員指派變更的報告
* 取得有關特殊權限角色存取的警示
* 需要核准才能啟動 (預覽)

Azure AD Privileged Identity Management 可以管理內建的 Azure AD 組織角色，包括 (但不限於)：  

* 全域管理員
* 計費管理員
* 服務管理員  
* 使用者管理員
* 密碼管理員

## <a name="just-in-time-administrator-access"></a>即時管理員存取權
在過去，您可以透過 Azure 傳統入口網站或 Windows PowerShell 將使用者指派給管理員角色。 因此，該使用者會成為 **永久管理員**，其獲得指派的角色永遠處於作用狀態。 Azure AD Privileged Identity Management 導入了「合格系統管理員」 的概念。 合格系統管理員應該是指偶爾需要特殊存取權限而非每一天都需要此權限的使用者。 在使用者需要存取權之前，角色會處於非作用中狀態，然後使用者須完成啟用程序，才能在一段預定的時間內成為作用中的系統管理員。

## <a name="enable-privileged-identity-management-for-your-directory"></a>啟用目錄的 Privileged Identity Management
您可以在 [Azure 入口網站](https://portal.azure.com/)中開始使用 Azure AD Privileged Identity Management。

> [!NOTE]
> 您必須是具有組織帳戶 (例如 @yourdomain.com) 而非 Microsoft 帳戶 (例如 @outlook.com) 的全域管理員，才能啟用目錄的 Azure AD Privileged Identity Management。

1. 以目錄的全域系統管理員身分登入 [Azure 入口網站](https://portal.azure.com/) 。
2. 如果貴組織有多個目錄，請選取 Azure 入口網站右上角的使用者名稱。 選取您將在其中使用 Azure AD Privileged Identity Management 的目錄。
3. 選取 [更多服務] 並使用 [篩選器] 文字方塊來搜尋 [Azure AD Privileged Identity Management]。
4. 選取 [釘選到儀表板]，然後按一下 [建立]。 Privileged Identity Management 應用程式隨即開啟。

如果您是在目錄中使用 Azure AD Privileged Identity Management 的第一個人，則 [安全性精靈](active-directory-privileged-identity-management-security-wizard.md) 會引導您完成初始指派體驗。 之後，您就會自動成為目錄的第一個「安全性系統管理員」和「特殊權限角色管理員」。

只有特殊權限角色管理員可以管理其他系統管理員的存取權。 您可以 [在 PIM 中為其他使用者提供管理能力](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。

## <a name="privileged-identity-management-admin-dashboard"></a>Privileged Identity Management 管理員儀表板
Azure AD Privileged Identity Manager 有一個管理員儀表板可提供重要資訊，例如：

* 指出有提升安全性機會的警示
* 指派給每個特殊權限角色的使用者數目  
* 合格和永久系統管理員的數目
* 您的目錄中特殊權限角色啟用的圖表

![PIM 儀表板 - 螢幕擷取畫面][2]

## <a name="privileged-role-management"></a>特殊權限角色管理
使用 Azure AD Privileged Identity Management，您便可透過新增或移除每個角色的永久或合格系統管理員來管理這些管理員。

![PIM 新增/移除系統管理員 - 螢幕擷取畫面][3]

## <a name="configure-the-role-activation-settings"></a>設定角色啟用設定
您可以使用 [角色設定](active-directory-privileged-identity-management-how-to-change-default-settings.md) 來設定合格角色啟用屬性，包括：

* 角色啟用期間的持續時間
* 角色啟用通知
* 使用者在角色啟用程序期間所需提供的資訊
* 服務票證或事件數目
* [核准工作流程需求 - 預覽](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM 設定 - 系統管理員啟動 - 螢幕擷取畫面][4]

請注意，此影像中已停用 [Multi-Factor Authentication]  的按鈕。 針對某些高特殊權限的角色，我們會要求使用 MFA 來增強防護。

## <a name="role-activation"></a>角色啟用
為了 [啟用角色](active-directory-privileged-identity-management-how-to-activate-role.md)，合格系統管理員會為角色要求一個有時效性的「啟用」。 使用 Azure AD 特殊權限身分識別管理中的 [ **啟用我的角色** ] 選項，即可要求啟用。

想要啟用角色的管理員必須在 Azure 入口網站中初始化 Azure AD Privileged Identity Management。

角色啟用是可自訂的。 在 [PIM] 設定中，您可以決定啟用的長度，以及管理員必須提供才能啟用角色的資訊。

![PIM 系統管理員要求角色啟用 - 螢幕擷取畫面][5]

## <a name="review-role-activity"></a>檢閱角色活動
有兩種方式可以追蹤您的員工和系統管理員使用特殊權限角色的情況。 第一個選項是使用[目錄角色稽核歷程](active-directory-privileged-identity-management-how-to-use-audit-log.md)。 稽核歷程記錄會追蹤特殊權限角色的指派和角色啟用歷程中的變更。

![PIM 啟動歷程記錄 - 螢幕擷取畫面][6]

第二個選項是設定標準 [存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。 這些存取檢閱可以由指派的檢閱者 (例如團隊經理) 來執行或者員工可以檢閱自己。 如此來監視誰仍需要或不再需要存取是最佳的方式。

## <a name="azure-ad-pim-at-subscription-expiration"></a>訂用帳戶過期時的 Azure AD PIM
在公開上市之前，Azure AD PIM 處於預覽狀態，而且沒有租用戶的授權檢查可預覽 Azure AD PIM。  現在，Azure AD PIM 已公開上市，試用或付費授權必須指派給租用戶的系統管理員，才能繼續使用 PIM。  如果您的組織並未購買 Azure AD Premium P2 或您的試用過期，您的租用戶就無法再使用幾乎所有 Azure AD PIM 功能。  您可以深入了解 [Azure AD PIM 訂用帳戶需求](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
