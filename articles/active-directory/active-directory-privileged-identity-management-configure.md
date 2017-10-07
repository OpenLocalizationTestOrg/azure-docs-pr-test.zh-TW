---
title: "Azure AD Privileged Identity Management aaaConfigure |Microsoft 文件"
description: "主題，說明 Azure AD Privileged Identity Management 為何及如何 toouse PIM tooimprove 您雲端的安全性。"
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
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>什麼是 Azure AD Privileged Identity Management？
您可以利用 Azure Active Directory (AD) Privileged Identity Management 來管理、控制和監視組織內的存取行為。 這包括存取 tooresources 在 Azure AD 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。  

> [!NOTE]
> Privileged 的 Identity Management 授權您的系統管理員與 Azure Active Directory Premium P2 hello 版時可用的 tooyour 整個組織。 如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。

組織想 toominimize hello 許多人都擁有存取 toosecure 資訊或資源，因為，可以減少惡意使用者取得存取 hello 機會。 不過，使用者仍然需要 toocarry Azure、 Office 365 或 SaaS 應用程式中的特殊權限作業。 組織可以在 Azure AD 中授與使用者特殊權限，而不需監視這些使用者使用其系統管理權限來執行什麼作業。 Azure AD Privileged Identity Management 可協助 tooresolve 這項風險。  

Azure AD Privileged Identity Management 可協助您：  

* 查看哪些使用者是 Azure AD 管理員
* 視需要啟用，"just-in-time"系統管理存取權 tooMicrosoft 線上服務，如 Office 365 和 Intune
* 取得有關系統管理員存取記錄與系統管理員指派變更的報告
* 取得警示存取 tooa 特殊權限角色
* 需要核准 tooactivate （預覽）

Azure AD Privileged Identity Management 可以管理 hello 內建的 Azure AD 組織角色，包括 （但不是限於）：  

* 全域管理員
* 計費管理員
* 服務管理員  
* 使用者管理員
* 密碼管理員

## <a name="just-in-time-administrator-access"></a>即時管理員存取權
在過去，您可能會指派使用者 tooan 系統管理員角色，透過 hello Azure 傳統入口網站或 Windows PowerShell。 如此一來，該使用者即成為**永久系統管理員**，一律在 hello 指派角色在作用中。 Azure AD Privileged Identity Management 引進 hello 概念**合格的系統管理員**。合格系統管理員應該是指偶爾需要特殊存取權限而非每一天都需要此權限的使用者。 hello 角色未作用中，直到 hello 使用者需要存取時，，然後完成啟動程序，並成為使用中的系統管理員預先決定的一段時間。

## <a name="enable-privileged-identity-management-for-your-directory"></a>啟用目錄的 Privileged Identity Management
您可以開始使用 Azure AD Privileged Identity Management 中 hello [Azure 入口網站](https://portal.azure.com/)。

> [!NOTE]
> 您必須是全域管理員的組織帳戶 (例如， @yourdomain.com)，不是 Microsoft 帳戶 (例如， @outlook.com)，tooenable 目錄的 Azure AD Privileged Identity Management。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)您目錄的全域管理員身分。
2. 如果您的組織具有多個目錄，選取您的使用者名稱 hello 右上角的 hello Azure 入口網站。 選取您將在其中使用 Azure AD Privileged Identity Management hello 目錄。
3. 選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。
4. 請檢查**Pin toodashboard** ，然後按一下**建立**。 hello Privileged Identity Management 的應用程式會開啟。

如果您正在 hello 第一個人 toouse Azure AD Privileged Identity Management 目錄中，然後 hello[安全性精靈](active-directory-privileged-identity-management-security-wizard.md)會引導您完成 hello 初始設定經驗。 之後，您會自動變成 hello 先**安全性系統管理員**和**特殊權限的角色管理員**的 hello 目錄。

只有特殊權限角色管理員可以管理其他系統管理員的存取權。 您可以[PIM 中授與其他使用者 hello 能力 toomanage](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。

## <a name="privileged-identity-management-admin-dashboard"></a>Privileged Identity Management 管理員儀表板
Azure AD Privileged Identity Manager 有一個管理員儀表板可提供重要資訊，例如：

* 指出機會 tooimprove 安全性警示
* hello tooeach 特殊權限的角色所指派的使用者的數目  
* hello 數字的合格和永久系統管理員
* 您的目錄中特殊權限角色啟用的圖表

![PIM 儀表板 - 螢幕擷取畫面][2]

## <a name="privileged-role-management"></a>特殊權限角色管理
使用 Azure AD Privileged Identity Management，您可以透過加入或移除永久或符合資格的系統管理員 tooeach 角色管理 hello 系統管理員。

![PIM 新增/移除系統管理員 - 螢幕擷取畫面][3]

## <a name="configure-hello-role-activation-settings"></a>設定 hello 角色啟動設定
使用 hello[角色設定](active-directory-privileged-identity-management-how-to-change-default-settings.md)您可以設定 hello 符合資格的角色啟動屬性，包括：

* hello 的 hello 角色啟動期間的持續時間
* hello 角色啟用通知
* hello 角色啟動程序期間需要 tooprovide hello 資訊的使用者
* 服務票證或事件數目
* [核准工作流程需求 - 預覽](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM 設定 - 系統管理員啟動 - 螢幕擷取畫面][4]

請注意，在 hello 映像，hello 的按鈕**Multi-factor Authentication**會停用。 針對某些高特殊權限的角色，我們會要求使用 MFA 來增強防護。

## <a name="role-activation"></a>角色啟用
太[啟用角色](active-directory-privileged-identity-management-how-to-activate-role.md)，合格的系統管理員要求時間繫結至的 「 啟用 」 hello 角色。 可以使用 hello 要求 hello 啟用**啟用 我的角色**Azure AD Privileged Identity Management 中的選項。

系統管理員，並想要 tooactivate 角色都需要 tooinitialize hello Azure 入口網站中的 Azure AD Privileged Identity Management。

角色啟用是可自訂的。 在 hello PIM 設定中，您可以判斷 hello 啟用和哪些資訊 hello 系統管理員必須 tooprovide tooactivate hello 角色 hello 長度。

![PIM 系統管理員要求角色啟用 - 螢幕擷取畫面][5]

## <a name="review-role-activity"></a>檢閱角色活動
有兩種方式 tootrack 如何使用您的員工和系統管理員特殊權限的角色。 hello 第一個選項使用[目錄角色稽核歷程](active-directory-privileged-identity-management-how-to-use-audit-log.md)。 hello 稽核歷程記錄中的特殊權限的角色指派及角色啟動歷程記錄的追蹤變更。

![PIM 啟動歷程記錄 - 螢幕擷取畫面][6]

hello 第二個選項是一般向上 tooset[存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。 這些存取檢視可以執行，而指派給檢閱者 （例如小組管理員） 或 hello 員工可以檢閱其本身。 這是 hello 最佳方式 toomonitor 人員仍需要存取，以及人員不會再。

## <a name="azure-ad-pim-at-subscription-expiration"></a>訂用帳戶過期時的 Azure AD PIM
檢查租用戶 toopreview Azure AD PIM 先前 tooreaching 一般可用性 Azure AD PIM 處於預覽，且沒有任何授權。  現在，Azure AD PIM 已達到公開上市，試用或付費的授權，必須指派 toohello hello 租用戶 toocontinue 使用 PIM 系統管理員。  如果您的組織不會購買 Azure AD Premium P2，或您的試用版到期，大部分的所有 hello Azure AD PIM 功能將不再提供您的租用戶。  閱讀更多在 hello [Azure AD PIM 訂用帳戶需求](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
