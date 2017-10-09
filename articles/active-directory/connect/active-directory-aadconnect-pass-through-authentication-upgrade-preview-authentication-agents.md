---
title: "Azure AD Connect：傳遞驗證 - 將預覽驗證代理程式升級 | Microsoft Docs"
description: "本文說明如何 tooupgrade 您的 Azure Active Directory (Azure AD) 的傳遞驗證設定。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Azure Active Directory 傳遞驗證：將預覽驗證代理程式升級

## <a name="overview"></a>概觀

本文適用於透過預覽版使用 Azure AD 傳遞驗證的客戶。 我們最近已升級 （並重新命名） hello 驗證代理程式 」 軟體。 您需要 too_manually_ 升級預覽您的內部部署伺服器上安裝代理程式的驗證。 此手動升級只是一次性動作。 所有未來的更新 tooAuthentication 代理程式是自動的。 hello 原因 tooupgrade 如下所示：

- 任何進一步的安全性或 bug 修正，不會收到 hello 預覽版本驗證代理程式。
-   hello 預覽版本驗證代理程式無法安裝在其他伺服器，以進行高可用性。

## <a name="check-versions-of-your-authentication-agents"></a>檢查驗證代理程式的版本

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>步驟 1：檢查驗證代理程式的安裝位置

請遵循這些步驟 toocheck 驗證代理程式的安裝位置：

1. 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 租用戶的全域管理員認證。
2. 選取**Azure Active Directory** hello 左側導覽上。
3. 選取 [Azure AD Connect]。 
4. 選取 [傳遞驗證]。 此刀鋒視窗會列出 hello 伺服器驗證代理程式的安裝位置。

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>步驟 2： 檢查 hello 版本驗證代理程式

toocheck hello 版本驗證代理程式，在 hello 前面步驟中，識別每個伺服器上遵循下列指示：

1. 跳過**控制台]-> [程式]-> [程式和功能**hello 在內部部署伺服器上。
2. 如果沒有的項目 」**Microsoft Azure AD Connect 驗證代理程式**」，您不需要 tootake 這部伺服器上的任何動作。
3. 如果沒有的項目 」**Microsoft Azure AD 應用程式 Proxy 連接器**"，版本 1.5.132.0 或更早版本，您需要 toomanually 升級此伺服器上。

![驗證代理程式的預覽版本](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>最佳作法 toofollow 開始 hello 升級之前

在升級之前，請確定您有下列項目就地 hello:

1. **建立僅限雲端的全域系統管理員帳戶**： 不升級而不需僅限雲端的全域管理員帳戶 toouse 在緊急情況下，您的傳遞驗證代理程式無法正常運作。 了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。 這是確保您不會被租用戶封鎖的關鍵步驟。
2.  **確保高可用性**： 如果先前未完成，安裝的第二個獨立的登入要求，使用這些驗證代理程式 」 tooprovide 高可用性[指示](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)。

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>在您 Azure AD Connect 的伺服器上的升級 hello 驗證代理程式

您必須升級 Azure AD Connect，才能升級 hello 驗證代理程式 」 在 hello 上的相同的伺服器。 在主要伺服器和暫存 Azure AD Connect 伺服器上執行下列步驟：

1. **升級 Azure AD Connect**： 後面要接著[文章](./active-directory-aadconnect-upgrade-previous-version.md)和 toohello 最新的 Azure AD Connect 版本升級。
2. **解除安裝預覽版本，hello hello 驗證代理程式 」**： 下載[這個 PowerShell 指令碼](https://aka.ms/rmpreviewagent)和 hello 伺服器的系統管理員身分執行它。
3. **下載 hello hello 驗證代理程式最新版本 (版本 1.5.193.0 或更新版本)**： 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)與您的租用戶全域管理員認證。 選取 [Azure Active Directory] -> [Azure AD Connect] -> [傳遞驗證] -> [下載代理程式]。 接受服務條款 hello 和下載 hello hello 驗證代理程式最新版本。
4. **Hello 最新版本的 hello 驗證代理程式安裝**： 在步驟 3 中下載的可執行檔執行 hello。 出現提示時，提供您租用戶的全域管理員認證。
5. **確認是否已安裝，hello 最新版**： 如之前所示，跳過**控制台]-> [程式]-> [程式和功能**，並確認的項目 」**Microsoft Azure AD Connect驗證代理程式 」**"。

>[!NOTE]
>如果您核取 hello 傳遞驗證 刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)之後完成 hello 先前步驟後，您會看到兩個驗證代理程式 」 項目，每一部伺服器-顯示 hello 的一個項目驗證代理程式 」 為**Active**和其他為 hello**非作用中**。 這是_預期行為_。 hello **Inactive**幾天後自動卸除項目。

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>升級其他伺服器上的 hello 驗證代理程式

依照這些步驟 tooupgrade 驗證代理程式上的其他伺服器 （Azure AD Connect 但尚未安裝）：

1. **解除安裝預覽版本，hello hello 驗證代理程式 」**： 下載[這個 PowerShell 指令碼](https://aka.ms/rmpreviewagent)和 hello 伺服器的系統管理員身分執行它。
2. **下載 hello hello 驗證代理程式最新版本 (版本 1.5.193.0 或更新版本)**： 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)與您的租用戶全域管理員認證。 選取 [Azure Active Directory] -> [Azure AD Connect] -> [傳遞驗證] -> [下載代理程式]。 接受服務條款 hello 和下載 hello 最新版本。
3. **Hello 最新版本的 hello 驗證代理程式安裝**： 在步驟 2 中的可執行檔執行 hello 下載。 出現提示時，提供您租用戶的全域管理員認證。
4. **確認是否已安裝，hello 最新版**： 如之前所示，跳過**控制台]-> [程式]-> [程式和功能**，並確認呼叫的項目**Microsoft Azure AD Connect驗證代理程式 」**。

>[!NOTE]
>如果您核取 hello 傳遞驗證 刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)之後完成 hello 先前步驟後，您會看到兩個驗證代理程式 」 項目，每一部伺服器-顯示 hello 的一個項目驗證代理程式 」 為**Active**和其他為 hello**非作用中**。 這是_預期行為_。 hello **Inactive**幾天後自動卸除項目。

## <a name="next-steps"></a>後續步驟
- [**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。
