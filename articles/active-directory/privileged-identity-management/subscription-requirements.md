---
title: "aaaPrivileged 身分識別管理訂閱]-[Azure |Microsoft 文件"
description: "說明 hello 訂用帳戶和授權管理和租用戶中使用 Azure AD Privileged Identity Management 的需求"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Azure Active Directory Privileged Identity Management 訂用帳戶需求

Azure AD Privileged Identity Management 可做為 Azure AD Premium P2 hello 版本的一部分。 如需有關 hello P2 和 tooPremium P1 的比較的其他功能，請參閱[Azure Active Directory 版本](../active-directory-editions.md)。

>[!NOTE]
Azure Active Directory (Azure AD) Privileged Identity Management 在預覽中時，沒有任何租用戶 tootry hello 服務的授權檢查。  現在，Azure AD Privileged Identity Management 到達的正式運作時，必須存在 hello 在 2016 年 12 月之後使用 Privileged Identity Management 的租用戶 toocontinue 才能試用或付費訂閱。
  

## <a name="confirm-your-trial-or-paid-subscription"></a>確認試用或付費訂用帳戶

如果您不確定您的組織是否有試用或購買訂用帳戶，您可以檢查是否有您的租用戶中的訂閱使用包含在 Azure Active Directory 模組的 Windows PowerShell V1 hello 命令。 
1. 開啟 PowerShell 視窗。
2. 輸入`Connect-MsolService`tooauthenticate 成為您的租用戶中的使用者。
3. 輸入 `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`。

此命令會擷取您的租用戶中的 hello 訂閱清單。 如果沒有傳回任何線條，您將需要 Azure AD Premium P2 tooobtain 試用版，購買的 Azure AD Premium P2 訂閱或 EMS E5 訂用帳戶 toouse Azure AD Privileged Identity Management。  讀取 tooget 試用版和開始使用 Azure AD Privileged Identity Management[開始使用 Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)。

如果此命令會傳回中的資料行的 SkuPartNumber"AAD_PREMIUM_P2"或"EMSPREMIUM 」 和 IsTrial 為"True"，這表示 Azure AD Premium P2 試用版已存在於 hello 租用戶。  如果未啟用 hello 訂閱狀態，而且您不需要 Azure AD Premium P2 或 EMS E5 訂閱購買，然後您必須購買的 Azure AD Premium P2 訂閱或使用 Azure AD Privileged Identity Management EMS E5 訂用帳戶 toocontinue。

Azure AD Premium P2 是可透過[Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx)，hello[開啟的大量授權方案](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)，和 hello[雲端方案提供者程式](https://partner.microsoft.com/en-US/cloud-solution-provider)。 Azure 和 Office 365 訂閱者也可以線上購買 Azure AD Premium P2。  Azure AD Premium 價格和 tooorder 線上方式可以在找到更多資訊[Azure Active Directory 定價](https://azure.microsoft.com/en-us/pricing/details/active-directory/)。

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Azure AD Privileged Identity Management 不適用於租用戶

在下列情況下，Azure AD Privileged Identity Management 無法再適用於租用戶︰
- 您的組織使用預覽狀態的 Azure AD Privileged Identity Management，且未購買 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶。
- 您的組織擁有的 Azure AD Premium P2 或 EMS E5 試用版已過期。
- 您的組織購買的訂用帳戶已過期。

當 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶過期，或使用預覽狀態 Azure AD Privileged Identity Management 的組織未取得 Azure AD Premium P2 或 EMS E5 訂用帳戶時：

- 永久性的角色指派 tooAzure AD 角色不會受到影響。
- hello hello Azure 入口網站中的 Azure AD Privileged Identity Management 延伸模組，以及 hello Graph API cmdlet 和 PowerShell 的 Azure AD Privileged Identity Management 的介面將不再可供使用者 tooactivate 特殊權限角色管理特殊權限存取，或執行存取檢查的權限的角色。
- 符合資格的角色指派的 Azure AD 角色將會移除，因為使用者將不再能夠 tooactivate 特殊權限角色。
- Azure AD 角色的任何進行中存取檢閱將會結束，而且 Azure AD Privileged Identity Management 組態設定將會遭到移除。
- Azure AD Privileged Identity Management 將不再傳送有關角色指派變更的電子郵件。

## <a name="next-steps"></a>後續步驟

- [開始使用 Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)
- [Azure AD Privileged Identity Management 中的角色](../active-directory-privileged-identity-management-roles.md)
