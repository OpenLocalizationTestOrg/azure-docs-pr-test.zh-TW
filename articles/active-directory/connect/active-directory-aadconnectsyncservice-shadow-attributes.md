---
title: "aaaAzure AD Connect 同步處理服務陰影屬性 |Microsoft 文件"
description: "描述陰影屬性如何在 Azure AD Connect 同步處理服務中運作。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Azure AD Connect 同步處理服務陰影屬性
大部分屬性都表示相同 hello 在 Azure AD 和它們在您的內部部署 Active Directory 中。 但某些屬性有一些特殊的處理和在 Azure AD 中的 hello 屬性值可能不同於 Azure AD Connect 同步處理。

## <a name="introducing-shadow-attributes"></a>簡介陰影屬性
某些屬性在 Azure AD 中有兩種表示法。 Hello 內部值和導出的值會儲存。 這些額外的屬性稱為陰影屬性。 hello 兩個最常見屬性，您會看到這種行為是**userPrincipalName**和**proxyAddress**。 這些屬性代表非已驗證網域中的值時，就會發生 hello 變更屬性值中。 但在連接中的 hello 同步處理引擎讀取 hello 值 hello 陰影屬性中的，從其觀點來看，hello 屬性已確認 Azure AD。

您無法看到 hello 陰影屬性使用 hello Azure 入口網站或 PowerShell。 但是了解 hello 概念可幫助您 tootroubleshoot 某些情況下 hello 屬性有不同的值在內部部署和雲端 hello。

toobetter 了解 hello 行為，看看這個範例來自 Fabrikam:  
![網域](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
它們在其內部部署 Active Directory 中有多個 UPN 尾碼，但是它們只驗證其中一個。

### <a name="userprincipalname"></a>userPrincipalName
使用者具有下列屬性值，在非驗證的網域中的 hello:

| 屬性 | 值 |
| --- | --- |
| 內部部署 userPrincipalName | lee.sperry@fabrikam.com |
| Azure AD shadowUserPrincipalName | lee.sperry@fabrikam.com |
| Azure AD userPrincipalName | lee.sperry@fabrikam.onmicrosoft.com |

hello userPrincipalName 屬性是使用 PowerShell 時，您所看到的 hello 值。

因為 hello 實際在內部部署的屬性值會儲存在 Azure AD 中，當您驗證 hello fabrikam.com 網域，Azure AD 會更新與 hello shadowUserPrincipalName hello 值 hello userPrincipalName 屬性。 您沒有 toosynchronize 來自 Azure AD Connect 的更新這些值 toobe 的任何變更。

### <a name="proxyaddresses"></a>proxyAddresses
hello proxyAddresses，不過多了某些額外邏輯，也會發生相同的程序，只包含已驗證的網域。 已驗證網域的 hello 檢查只會發生的信箱的使用者。 擁有郵件功能的使用者或連絡人代表另一個 Exchange 組織中的使用者，並在 proxyAddresses toothese 物件，您可以加入任何值。

對於信箱使用者，內部部署或 Exchange Online，只會顯示已驗證網域的值。 它看起來如下所示：

| 屬性 | 值 |
| --- | --- |
| 內部部署 proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| Exchange Online proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

在此情況下，**smtp:abbie.spencer@fabrikam.com ** 已移除，因為該網域尚未驗證。 但是 Exchange 也會新增 **SIP:abbie.spencer@fabrikamonline.com **。Fabrikam 不曾使用 Lync/Skype 內部部署，但是 Azure AD 和 Exchange Online 為它進行準備。

此邏輯 proxyAddresses 是參照的 tooas **ProxyCalc**。 ProxyCalc 在使用者每次變更時叫用，其時機為︰

- hello 使用者已被指派包含 Exchange Online，即使 hello 使用者未獲得授權，適用於 Exchange 服務方案。 比方說，如果 hello 使用者被指派 hello Office E3 SKU，但只被指派 SharePoint Online。 即使您的信箱仍然是內部部署，也是如此。
- hello 屬性 msExchRecipientTypeDetails 的值。
- 您進行變更 tooproxyAddresses 或 userPrincipalName。

ProxyCalc 花一些時間 tooprocess 變更使用者，而且不同步與 hello Azure AD Connect 匯出程序。

> [!NOTE]
> hello ProxyCalc 邏輯都有某些進階案例中未記載於本主題的其他行為。 本主題會提供您 toounderstand hello 行為和不文件內部的所有邏輯。

### <a name="quarantined-attribute-values"></a>隔離的屬性值
有重複的屬性值時，也會使用陰影屬性。 如需詳細資訊，請參閱[重複屬性恢復功能](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)。

## <a name="see-also"></a>另請參閱
* [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
