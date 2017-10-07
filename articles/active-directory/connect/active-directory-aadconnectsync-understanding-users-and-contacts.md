---
title: "Azure AD Connect 同步：了解使用者和連絡人 | Microsoft Docs"
description: "說明 Azure AD Connect 同步處理中的使用者和連絡人。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Azure AD Connect 同步處理：了解使用者和連絡人
您可能有幾種不同的原因，而擁有多個 Active Directory 樹系並且具有幾種不同的部署拓撲。 常見的模型包括合併與收購之後的帳戶-資源部署與 GAL 同步處理的樹系。 雖然有單純的模型，但混合模型也同樣常見。 Azure AD Connect 同步處理中的 hello 預設組態不採用任何特定的模型，但取決於如何比對使用者已選取 hello 安裝指南中，可以觀察到不同的行為。

本主題中，我們將探討 hello 預設組態在特定拓撲中的運作方式。 我們將探討 hello 組態和 hello 同步處理規則編輯器可以是使用的 toolook 在 hello 組態。

有幾個 hello 設定會假設的一般規則：

* 不論順序我們從 hello 來源 Active Directory 匯入，hello 最終結果應一律是 hello 相同。
* 使用中的帳戶一律會提供登入資訊，包括 **userPrincipalName** 和 **sourceAnchor**。
* 停用的帳戶會提供 userPrincipalName 和 sourceAnchor，除非它是連結的信箱，如果不沒有找到任何使用中的帳戶 toobe。
* 具有連結信箱的帳戶永遠不會用於 userPrincipalName 和 sourceAnchor。 它假設稍後就會找到使用中的帳戶。
* 連絡人物件可能佈建的 tooAzure AD 作為連絡人或使用者。 一直要到處理了所有來源 Active Directory 樹系之後，您才會知道物件成為何者。

## <a name="contacts"></a>連絡人
在合併與收購時使用 GALSync 解決方案橋接兩個或多個 Exchange 樹系之後，常會有多個連絡人代表不同樹系中的某個使用者。 hello 連絡人物件一律要加入從 hello 連接器空間 toohello metaverse 使用 hello mail 屬性。 如果已經有相同的連絡人物件或使用者物件以 hello 郵件地址，hello 物件聯結在一起。 這設定在 hello 規則**中 from AD – Contact Join**。 另外還有名為的規則**中 from AD – Contact Common**屬性流程 toohello metaverse 屬性與**sourceObjectType**與 hello 常數**連絡人**。 此規則的優先順序非常低，如果任何使用者物件聯結的 toohello 相同的 metaverse 物件，然後 hello 規則**中 from AD – User Common**會導致 hello value 使用者 toothis 屬性。 與這項規則，此屬性必須 hello 值，如果沒有使用者已經加入，請連絡 hello 使用者的值，如果至少一個使用者發現。

佈建物件 tooAzure AD，hello 輸出規則**出 tooAAD – Contact Join**會建立連絡人物件，如果 hello metaverse 屬性**sourceObjectType**設定得**連絡**. 如果此屬性設定太**使用者**，然後 hello 規則**出 tooAAD – User Join**改為建立使用者物件。
很可能更多來源 Active Directory 會匯入和同步處理時，會從 Contact tooUser 升級物件。

比方說，在 GALSync 拓撲中我們會發現連絡人物件的每個人都 hello 第二個樹系中當我們匯入 hello 第一個樹系。 這將暫存 hello AAD 連接器中新的連絡人物件。 當我們稍後匯入和同步處理 hello 第二個樹系時，我們會尋找 hello 真正的使用者，並將其聯結 toohello 現有的 metaverse 物件。 然後我們將刪除 AAD 中的 hello 連絡人物件，並改為建立新的使用者物件。

如果您有的拓撲，其中使用者會顯示為連絡人，請確定您選取 toomatch hello mail 屬性上的使用者 hello 安裝指南中。 如果您選取另一個選項，則您的組態就會與順序有關。 Hello mail 屬性上一律聯結連絡人物件，但使用者物件上聯結 hello mail 屬性如果 hello 安裝指南中已選取此選項。 您可以再得到 hello 與 hello metaverse 中的兩個不同物件具有相同 mail 屬性如果 hello 連絡人物件已匯入之前 hello 使用者物件。 在匯出 tooAzure AD，將會擲回錯誤。 此行為是設計所致，表示不正確的資料，或在 hello 安裝期間未正確識別該 hello 拓撲。

## <a name="disabled-accounts"></a>停用的帳戶
停用的帳戶也會同步 tooAzure AD。 停用的帳戶是交換，例如會議室中的常見 toorepresent 資源。 hello 例外狀況是使用者具有連結信箱。如先前所述，這些將會永遠不會提供帳戶 tooAzure AD。

hello 假設是，如果找到停用的使用者帳戶，則稍後我們會不到另一個使用中的帳戶，而且 hello 物件是佈建的 tooAzure AD 與找到 hello userPrincipalName 和 sourceAnchor。 在案例中另一個使用中的帳戶將會加入的 toohello 將使用相同的 metaverse 物件，然後將其 userPrincipalName 和 sourceAnchor。

## <a name="changing-sourceanchor"></a>變更 sourceAnchor
當物件已匯出 tooAzure AD，則不允許的 toochange hello sourceAnchor 不再。 當 hello 物件已匯出的 hello metaverse 屬性**cloudSourceAnchor**設定以 hello **sourceAnchor** Azure AD 所接受的值。 如果**sourceAnchor**的變更，並不符合**cloudSourceAnchor**，hello 規則**出 tooAAD – User Join**會擲回 hello 錯誤**sourceAnchor 屬性已變更**。 在此情況下，hello 組態或資料必須更正錯誤，因此 hello 相同 sourceAnchor 存在於試 hello metaverse 中才可以再次同步處理 hello 物件。

## <a name="additional-resources"></a>其他資源
* [Azure AD Connect 同步處理：自訂同步處理選項](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

