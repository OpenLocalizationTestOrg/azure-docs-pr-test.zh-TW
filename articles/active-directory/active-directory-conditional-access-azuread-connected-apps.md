---
title: "aaaAzure SaaS 應用程式的條件式存取 |Microsoft 文件"
description: "在 Azure AD 中的條件式存取可讓您您 tooconfigure 每個應用程式多因素驗證存取規則和 hello 能力 tooblock 存取不受信任的網路上的使用者。 "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>開始使用 Azure Active Directory 條件式存取
[SaaS](https://azure.microsoft.com/overview/what-is-saas/) 應用程式及 Azure AD 連線應用程式的「Azure Active Directory 條件式存取」可讓您根據群組、位置和應用程式敏感性來設定條件式存取。 

使用以應用程式敏感性為基礎的條件式存取時，您可以設定每一應用程式的多重要素驗證 (MFA) 存取規則。 每個應用程式的 MFA 提供 hello 能力 tooblock 存取不受信任的網路上的使用者。 您可以套用 MFA 規則 tooall 使用者被指派 toohello 應用程式，或只適用於使用者在指定的安全性群組。  如果它們從 hello 組織的網路內的 IP 位址存取 hello 應用程式，使用者可能會排除從 hello MFA 需求。

這些功能將會使用 toocustomers 購買 Azure Active Directory Premium 授權。

## <a name="scenario-prerequisites"></a>案例必要條件
* Azure Active Directory Premium 的授權
* 同盟或受管理的 Azure Active Directory 租用戶
* 同盟租用戶需要啟用多重要素驗證。

## <a name="configure-per-application-access-rules"></a>設定每個應用程式的存取規則
本章節描述如何 tooconfigure 針對應用程式的存取規則。

1. 登入 toohello 使用 Azure ad 中為全域管理員帳戶的 Azure 傳統入口網站。
2. 在 hello 左窗格中，選取  **Active Directory**。
3. Hello 目錄索引標籤上，選取您的目錄。
4. 選取 hello**應用程式** 索引標籤。
5. 選取 hello hello 規則的應用程式將會針對設定。
6. 選取 hello**設定** 索引標籤。
7. 捲動 toohello 存取規則區段。 選取 hello 所需的存取規則。
8. 指定 hello hello 規則將套用到的使用者。
9. 選取以啟用 hello 原則**上啟用 toobe**。

## <a name="understanding-access-rules"></a>了解存取規則
本節提供支援 hello 條件式應用程式存取 Azure 中的 hello 存取規則的詳細的描述。

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>指定 hello 使用者 hello 的存取規則會套用到
根據預設 hello 原則會套用 tooall 使用者具有存取 toohello 應用程式。 不過，您也可以限制 hello 原則 toousers 成員 hello 指定的安全性群組。 hello**加入群組**按鈕是使用的 tooselect 其中一個，或從 hello 群組選取項目對話方塊 hello 存取規則的多個群組會套用至。 此對話方塊也可以使用的 tooremove 選取群組。 選取的 tooapply tooGroups hello 規則時，hello 存取將只會強制執行規則的使用者屬於 tooone hello 指定的安全性群組。

安全性群組可以也被明確排除 hello 原則選取 hello**除了**選項並指定一個或多個群組。 使用者已在 hello 群組的成員**除了**清單不會主旨 toohello 多因素驗證要求，即使它們是群組的成員，hello 套用存取規則。
存取 hello 應用程式時，如下所示的 hello 存取規則將會需要 hello 管理員群組 toouse 多重要素驗證中的所有使用者。

![使用 MFA 設定條件式存取規則](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>條件式存取規則和 MFA
如果使用者已設定並使用 hello 每位使用者的多重要素驗證功能，這項設定在 hello 使用者會結合 hello 的 hello 應用程式的多因素驗證規則。 這表示已針對每個使用者的 multi-factor authentication 的使用者會需要的 tooperform 多重要素驗證，即使它們有 hello 應用程式多因素驗證規則的豁免。 深入了解多重要素驗證和每個使用者設定。

### <a name="access-rule-options"></a>存取規則選項
支援下列選項的 hello:

* **需要多重要素驗證**: hello 使用者 toowhom hello 套用存取規則，都需要的 toocomplete 多重要素驗證，才能存取 hello hello 原則的應用程式適用於。
* **需要多重要素驗證，不在工作時**： 來自受信任的 IP 位址的使用者不會需要的 tooperform 多重要素驗證。 hello 受信任的 IP 位址範圍可以設定 hello 多因素驗證設定 頁面上。
* **不工作時封鎖存取**：將會封鎖不是來自受信任 IP 位址的使用者。 hello 受信任的 IP 位址範圍可以設定 hello 多因素驗證設定 頁面上。

### <a name="setting-rule-status"></a>設定規則狀態
存取規則狀態可讓您開啟或關閉 hello 規則。 當 hello 關閉存取規則時，不會強制執行 hello 多因素驗證要求。

### <a name="access-rule-evaluation"></a>存取規則評估
當使用者存取使用 OAuth 2.0、OpenID Connect、SAML 或 WS-同盟的同盟應用程式時，就會評估存取規則。 此外，當 hello OAuth 2.0 和 OpenID Connect 使用重新整理語彙基元 tooacquire 存取權杖時，會評估存取規則。 如果原則評估失敗時可使用重新整理語彙基元，hello 錯誤**invalid_grant**便會傳回，這表示 hello 使用者需要 toore-toohello 用戶端進行驗證。

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>設定同盟服務 tooprovide 多因素驗證
同盟租用戶，MFA 可能由 Azure Active Directory 或執行 hello 在內部部署 AD FS 伺服器。

根據預設，MFA 會發生在 Azure Active Directory 所裝載的頁面上。 tooconfigure MFA 內部，hello **– SupportsMFA**屬性必須設定太**true** Azure Active Directory，適用於 Windows PowerShell 使用 hello Azure AD 模組中。

hello 下列範例示範如何 tooenable 內部部署 MFA 使用 hello [Set-msoldomainfederationsettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) hello contoso.com 租用戶上：

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

在加法 toosetting 此旗標，hello 同盟租用戶 AD FS 執行個體必須設定 tooperform multi-factor authentication。 請依照指示 hello [Azure Multi-factor Authentication Server 在內部部署](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)。

## <a name="related-articles"></a>相關文章
* [保護存取 tooOffice 365 和其他應用程式連接 tooAzure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

