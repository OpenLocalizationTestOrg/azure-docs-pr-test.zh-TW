---
title: "Azure Active Directory Domain Services：受管理網域中的同步處理 | Microsoft Docs"
description: "了解 Azure Active Directory Domain Services 受管理網域中的同步處理"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Azure AD Domain Services 受管理網域中的同步處理
hello 下列圖表說明同步化的運作方式在 Azure AD 網域服務中受管理的網域。

![Azure AD Domain Services 中的同步處理拓撲](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>從內部部署目錄 tooyour Azure AD 租用戶的同步處理
Azure AD Connect 同步處理是使用的 toosynchronize 使用者帳戶、 群組成員資格，以及認證雜湊 tooyour Azure AD 租用戶。 屬性的使用者帳戶，例如 hello UPN 和在內部部署同步處理的 SID （安全性識別碼）。 如果您使用 Azure AD 網域服務時，NTLM 和 Kerberos 驗證所需的傳統的認證雜湊也會同步處理的 tooyour Azure AD 租用戶。

如果您設定回寫，在您的 Azure AD 目錄中進行的變更會同步處理後 tooyour 內部部署 Active Directory。 例如，如果您變更密碼使用 Azure AD 自助式密碼變更的功能，hello 變更過的密碼會更新您內部 AD 網域。

> [!NOTE]
> 一律使用 hello 最新版本的 Azure AD Connect tooensure 中，您必須針對所有已知的 bug 修正。
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>從您的 Azure AD 租用戶 tooyour 的同步處理受管理網域
從您的 Azure AD 租用戶 tooyour 受管理的 Azure AD 網域服務網域的使用者帳戶、 群組成員資格，以及認證雜湊會同步處理。 此同步處理程序是自動執行的。 您不需要 tooconfigure，監視或管理此同步處理程序。 完成 hello 一次性的初始同步處理目錄之後，它通常約 20 分鐘讓 Azure AD toobe 中所做的變更會反映在受管理的網域。 此同步處理間隔 toopassword 變更套用，或 tooattributes 在 Azure AD 中所做的變更。

hello 同步處理程序也是其中之一-單向/單向的本質。 除了您建立的所有自訂 OU 之外，您的受管理網域大部分都是唯獨的。 因此，您不能變更 toouser 屬性、 使用者密碼或群組成員資格 hello 受管理的網域內。 如此一來，不會反向同步的變更您受管理的網域後 tooyour Azure AD 租用戶。

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>從多樹系內部部署環境同步處理
許多組織有由多個帳戶樹系組成、相當複雜的內部部署身分識別基礎結構。 Azure AD Connect 支援同步處理的使用者、 群組和從多樹系環境 tooyour Azure AD 租用戶的認證雜湊。

相對地，Azure AD 租用戶是一個簡單許多且單層式的命名空間。 tooenable 使用者 tooreliably 存取應用程式受到 Azure AD，解決跨不同樹系中的使用者帳戶的 UPN 衝突。 您的 Azure AD 網域服務受管理的網域引起關閉認定 tooyour Azure AD 租用戶。 因此，您會在受管理網域中看到單層式 OU 結構。 不論 hello 在內部部署網域或樹系從中它們已同步處理中的 hello ' AADDC 使用者 容器中儲存所有使用者和群組。 您可能已在內部部署環境設定一個階層式 OU 結構。 不過，您的受管理網域仍然是具有簡單的單層式 OU 結構。

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>排除項目-什麼不同步 tooyour 受管理的網域
hello 下列物件或屬性不是已同步處理的 tooyour Azure AD 租用戶或 tooyour 受管理的網域：

* **排除的屬性：**可能從同步處理從您使用 Azure AD Connect 的內部部署網域 tooyour Azure AD 租用戶選擇 tooexclude 特定屬性。 這些排除的屬性將無法在您的受管理網域中提供使用。
* **群組原則：**設定內部部署網域中的群組原則不會同步的 tooyour 受管理的網域。
* **SYSVOL 共用：**同樣地，SYSVOL 共用您的內部網域的 hello 的 hello 內容不會同步的 tooyour 受管理的網域。
* **電腦物件：**電腦聯結的 tooyour 在內部部署網域的電腦物件不是已同步處理的 tooyour 受管理的網域。 這些電腦沒有受管理的網域信任關係，並屬於只有 tooyour 在內部部署網域。 在受管理的網域中，您會發現電腦物件，只會針對管理網域的電腦，您必須明確地加入網域的 toohello。
* **使用者和群組的 SidHistory 屬性：** hello 主要的使用者和主要群組在內部部署網域的 Sid 都是已同步處理的 tooyour 受管理的網域。 不過，現有的 SidHistory 屬性的使用者和群組未從您在內部部署網域 tooyour 受管理的網域同步處理。
* **組織單位 (OU) 的結構：**定義在內部部署網域中的組織單位不會同步 tooyour 受管理的網域。 您的受管理網域中有兩個內建的 OU。 根據預設，您的受管理網域會有單層式 OU 結構。 您可以不過選擇太[在受管理的網域中建立自訂的 OU](active-directory-ds-admin-guide-create-ou.md)。

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>特定的屬性時，同步處理的 tooyour 受管理的網域如何
hello 下表列出一些常見的屬性，並描述其同時同步的 tooyour 受管理的網域。

| 受管理網域中的屬性 | 來源 | 注意事項 |
|:--- |:--- |:--- |
| UPN |Azure AD 租用戶中的使用者 UPN 屬性 |因為 tooyour 受管理網域，則會同步處理從 Azure AD 租用戶的 hello UPN 屬性。 因此，hello 最可靠方式 toosign tooyour 受管理的網域中使用您的 UPN。 |
| SAMAccountName |Azure AD 租用戶中或自動產生的使用者 mailNickname 屬性 |hello SAMAccountName 屬性被來自 Azure AD 租用戶中的 hello mailNickname 屬性。 如果多個使用者帳戶都具有相同 mailNickname 屬性，hello SAMAccountName 就會自動產生的 hello。 如果 hello 使用者 mailNickname 或 UPN 前置詞的長度超過 20 個字元，hello SAMAccountName 自動產生 toosatisfy hello 20 字元限制是 SAMAccountName 屬性。 |
| 密碼 |來自 Azure AD 租用戶的使用者密碼 |系統會從您的 Azure AD 租用戶同步 NTLM 或 Kerberos 驗證所需的認證雜湊 (也稱為補充認證)。 如果您的 Azure AD 租用戶是已同步的租用戶，這些認證就會來自您的內部部署網域。 |
| 主要使用者/群組 SID |自動產生 |hello 個使用者/群組帳戶的主要 SID 都是自動產生受管理的網域中。 這個屬性不符合 hello 主要使用者/群組 SID hello 物件在您內部部署的 AD 網域。 不符的情形是因為 hello 受管理的網域具有不同的 SID 命名空間與您在內部部署網域。 |
| 使用者和群組的 SID 歷程記錄 |內部部署主要使用者和群組 SID |中受管理的網域使用者和群組的 hello SidHistory 屬性是設定在內部部署網域 toomatch hello 對應的主要使用者或群組 SID。 此功能可協助讓增益和-移位的內部部署應用程式 toohello 受管理的網域較為簡單，因為您不需要 toore ACL 的資源。 |

> [!NOTE]
> **登入 toohello 受管理的網域，使用 hello UPN 格式：** hello SAMAccountName 屬性可能是自動產生的受管理的網域中的部分使用者帳戶。 如果多個使用者擁有 hello 相同 mailNickname 屬性或使用者有過度長 UPN 前置詞，這些使用者的 SAMAccountName hello 可能是自動產生。 因此，hello SAMAccountName 格式 (例如，' CONTOSO100\joeuser') 不一定可靠的方式 toosign toohello 網域中。 使用者的自動產生 SAMAccountName 可能會與其 UPN 前置詞不同。 使用 hello UPN 格式 (例如，'joeuser@contoso100.com') 中 toohello toosign 可靠地管理網域。
>
>

### <a name="attribute-mapping-for-user-accounts"></a>使用者帳戶的屬性對應
Azure AD 租用戶中的使用者物件的受管理的網域中的同步處理的 toocorresponding 屬性 hello 下表會說明如何特定屬性。

| Azure AD 租用戶中的使用者屬性 | 受管理網域中的使用者屬性 |
|:--- |:--- |
| accountEnabled |userAccountControl （設定或清除 hello ACCOUNT_DISABLED 位元） |
| city |l |
| country |co |
| department |department |
| displayName |displayName |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| jobTitle |title |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (有時可能會自動產生) |
| mobile |mobile |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| passwordPolicies |userAccountControl （設定或清除 hello DONT_EXPIRE_PASSWORD 位元） |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| surname |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>群組的屬性對應
Azure AD 租用戶中的群組物件的受管理的網域中的同步處理的 toocorresponding 屬性 hello 下表會說明如何特定屬性。

| Azure AD 租用戶中的群組屬性 | 受管理網域中的群組屬性 |
|:--- |:--- |
| displayName |displayName |
| displayName |SAMAccountName (有時可能會自動產生) |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>不是物件同步處理受管理的網域從 tooyour Azure AD 租用戶
本文章的上一節所述，沒有從您受管理的網域後 tooyour Azure AD 租用戶的同步處理。 您可能會選擇太[建立自訂組織單位 (OU)](active-directory-ds-admin-guide-create-ou.md)中受管理的網域。 此外，您還可以在這些自訂 OU 內建立其他 OU、使用者、群組或服務帳戶。 沒有任何自訂的 Ou 內建立的 hello 物件會同步處理後 tooyour Azure AD 租用戶。 這些物件僅供在您的受管理網域內使用。 因此，這些物件不是使用 Azure AD PowerShell cmdlet，Azure AD Graph API，或使用 hello Azure AD 管理 UI 可見的。

## <a name="related-content"></a>相關內容
* [功能 - Azure AD 網域服務](active-directory-ds-features.md)
* [部署案例 - Azure AD 網域服務](active-directory-ds-scenarios.md)
* [Azure AD Domain Services 的網路考量](active-directory-ds-networking.md)
* [開始使用 Azure AD Domain Services](active-directory-ds-getting-started.md)
