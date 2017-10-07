---
title: "Azure AD Connect：支援的拓撲 | Microsoft Docs"
description: "本主題詳細說明 Azure AD Connect 的受支援和不受支援拓撲"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Azure AD Connect 的拓撲
本文說明各種內部部署與使用 Azure AD Connect 同步處理為 hello 重要的整合方案的 Azure Active Directory (Azure AD) 拓撲。 本文包含受支援和不受支援的組態。

以下是圖片 hello 文件中的 hello 圖例：

| 說明 | 符號 |
| --- | --- |
| 內部部署 Active Directory 樹系 |![內部部署 Active Directory 樹系](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| 內含篩選匯入的內部部署 Active Directory |![內含篩選匯入的 Active Directory](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Azure AD Connect 同步處理伺服器 |![Azure AD Connect 同步處理伺服器](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| Azure AD Connect 同步處理伺服器「預備模式」 |![Azure AD Connect 同步處理伺服器「預備模式」](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync 與 Forefront Identity Manager (FIM) 2010 或 Microsoft Identity Manager (MIM) 2016 |![GALSync 與 FIM 2010 或 MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Azure AD Connect 同步處理伺服器，詳細說明 |![Azure AD Connect 同步處理伺服器，詳細說明](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| 不受支援的案例 |![不受支援的案例](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>單一樹系、單一 Azure AD 租用戶
![單一樹系和單一租用戶的拓撲](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

hello 最常見的拓撲是單一內部部署樹系，其中包含一個或多個網域，與單一的 Azure AD 租用戶。 對於 Azure AD 驗證，會使用密碼同步處理。 Azure AD connect 的 hello 快速安裝支援這種拓撲。

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>單一樹系、 多個同步伺服器 tooone Azure AD 租用戶
![不受支援、已篩選的單一樹系拓撲](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

多個 Azure AD Connect 同步處理伺服器不支援連接的 toohello 相同的 Azure AD 租用戶，除了[暫存伺服器](#staging-server)。 它具有不支援，即使這些伺服器是設定的 toosynchronize 與一組互斥物件。 可能會視為此拓撲設定如果無法連線到單一伺服器，從 hello 樹系中的所有網域，或如果您想 toodistribute 負載到數部伺服器。

## <a name="multiple-forests-single-azure-ad-tenant"></a>多個樹系、單一 Azure AD 租用戶
![多個樹系和單一租用戶的拓撲](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

許多組織都有包含多個內部部署 Active Directory 樹系的環境。 擁有多個內部部署 Active Directory 的原因有很多。 典型的範例包括帳戶-資源樹系與 hello 結果合併或收購的設計。

當您擁有多個樹系，所有樹系必須可由單一 Azure AD Connect 同步處理伺服器連線。 您不需要 toojoin hello 伺服器 tooa 網域。 如果必要 tooreach 所有樹系中，您可以 hello 將伺服器放在周邊網路 （也稱為 DMZ、 非軍事區域和屏障式子網路）。

hello Azure AD Connect 的安裝精靈會提供數個選項 tooconsolidate 使用者在多個樹系中表示。 hello 目標是使用者一次呈現在 Azure AD。 有一些您可以設定在 hello 安裝精靈中的 hello 自訂安裝路徑中的常見拓撲。 在 [hello**用來唯一識別您的使用者**頁面上，選取 hello 對應的選項，表示您的拓撲。 hello 彙總設定僅適用於使用者。 重複的群組不會合併與 hello 預設組態。

常見的拓樸 hello 章節中討論關於[分割拓撲](#multiple-forests-separate-topologies)，[完整網狀](#multiple-forests-full-mesh-with-optional-galsync)，和[hello 帳戶-資源拓撲](#multiple-forests-account-resource-forest)。

Azure AD Connect 同步處理中的 hello 預設設定會假設：

* 每個使用者都只能有一個已啟用的帳戶，而且此帳戶所在的 hello 樹系是使用的 tooauthenticate hello 使用者。 此假設適用於密碼同步處理和同盟。 UserPrincipalName 和 sourceAnchor/immutableID 來自此樹系
* 每個使用者只有一個信箱。
* 裝載使用者 hello 信箱的 hello 樹系有 hello 最佳的資料品質 hello Exchange 全域通訊清單 (GAL) 中可見的屬性。 如果沒有 hello 使用者沒有信箱，任何樹系可以是使用的 toocontribute 這些屬性的值。
* 如果您有連結的信箱，則不同的樹系中還有帳戶用來登入。

如果您的環境不符合這些假設，hello 會發生下列情況：

* 如果您有多個使用中的帳戶或多個信箱，hello 同步處理引擎會挑選其中一個，並忽略其他 hello。
* 沒有其他作用中的帳戶具有連結的信箱不匯出的 tooAzure AD。 hello 使用者帳戶不會出現在任何群組成員身分。 DirSync 中已連結的信箱一律會顯示為一般信箱。 這項變更是刻意不同的行為 toobetter 支援多個樹系案例。

您可以找到更多詳細資料中的[了解 hello 預設組態](active-directory-aadconnectsync-understanding-default-configuration.md)。

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>多個樹系、 多個同步伺服器 tooone Azure AD 租用戶
![多個樹系和多個同步處理伺服器的不受支援拓撲](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

不支援具有單一 Azure AD 租用戶一個以上的 Azure AD Connect 同步處理連接伺服器 tooa。 hello 例外狀況是 hello 使用[暫存伺服器](#staging-server)。

### <a name="multiple-forests-separate-topologies"></a>多個樹系，個別拓撲
![跨所有目錄僅顯示使用者一次的選項](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![多個樹系和個別拓撲的描述](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

在此環境中，所有內部部署樹系會被視為個別的實體。 使用者不會顯示在其他樹系中。 每個樹系有它自己的 Exchange 組織，且 hello 樹系之間沒有 GALSync。 此拓撲可能 hello 情況合併/併購之後，或在組織中每個業務單位獨立運作的位置。 這些樹系 hello 相同組織在 Azure AD 中的，並且有統一 GAL 位於。 Hello 前面圖片，在會顯示一次 hello metaverse 中每個樹系中每個物件，並將其 hello 目標 Azure AD 租用戶中彙總中。

### <a name="multiple-forests-match-users"></a>多個樹系：比對使用者
常見的 tooall 這些案例是該發佈，安全性群組可包含混合的使用者、 連絡人及外部安全性主體 (Fsp)。 Fsp Active Directory 網域服務 (AD DS) toorepresent 成員從安全性群組中的其他樹系中使用。 所有 Fsp 會都是在 Azure AD 中解析的 toohello 實際物件。

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>多個樹系：內含選擇性 GALSync 的完整網狀
![比對使用者的身分存在跨多個目錄時使用 hello mail 屬性的選項](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![多個樹系的完整網狀拓撲](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

完整網狀拓撲可讓使用者和資源 toobe 任何樹系中。 通常，hello 樹系之間有雙向信任關係。

如果 Exchange 出現在一個以上的樹系中，有可能是選擇性的內部部署 GALSync 解決方案。 然後每個使用者可以顯示為所有其他樹系中的連絡人。 GALSync 通常會透過 FIM 2010 或 MIM 2016 實作。 Azure AD Connect 無法用於內部部署 GALSync。

在此案例中，身分識別物件的聯結透過 hello mail 屬性。 在樹系中具有信箱的使用者與 hello 中的 hello 連絡人聯結其他樹系。

### <a name="multiple-forests-account-resource-forest"></a>多個樹系：帳戶資源樹系
![比對識別身分存在於跨多個目錄時使用 hello ObjectSID 和 msExchMasterAccountSID 屬性的選項](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![多個樹系的帳戶資源樹系拓撲](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

在帳戶資源樹系拓撲中，您會有一個以上的*帳戶*樹系內含作用中的使用者帳戶。 您也會有一或多個*資源*樹系具有停用的帳戶。

在此案例中，一個 (或多個) 資源樹系信任所有帳戶樹系。 hello 資源樹系通常會有與 Exchange 和 Lync 擴充的 Active Directory 架構。 所有的 Exchange 和 Lync 服務以及其他共用的服務都位於此樹系。 使用者擁有這個樹系中，停用的使用者帳戶，並且連結 hello 信箱 toohello 帳戶樹系。

## <a name="office-365-and-topology-considerations"></a>Office 365 和拓撲考量
有些 Office 365 工作負載對受支援的拓撲有某些限制：

| 工作負載 | 限制 |
--------- | ---------
| Exchange Online | 如果有多個內部部署 Exchange 組織 （也就是 Exchange 已部署的 toomore 比一個樹系），您必須使用 Exchange 2013 SP1 或更新版本。 如需詳細資訊，請參閱[內含多個 Active Directory 樹系的混合式部署](https://technet.microsoft.com/library/jj873754.aspx)。 |
| 商務用 Skype | 當您使用多個內部部署樹系時，就會支援只有 hello 帳戶資源樹系拓撲。 如需詳細資訊，請參閱[商務用 Skype Server 2015 的環境需求](https://technet.microsoft.com/library/dn933910.aspx)。 |


## <a name="staging-server"></a>預備伺服器
![在拓撲中的預備伺服器](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect 支援以「預備模式」安裝第二部伺服器。 在此模式中的伺服器從所有連接的目錄中讀取資料，但不會寫入任何項目 tooconnected 目錄。 它會使用 hello 正常的同步處理循環，因此具有 [hello 識別資料的更新的複本。

其中 hello 主要伺服器失敗，發生災害，您可以容錯移轉 toohello 臨時伺服器。 您在 hello Azure AD Connect 精靈進行。 這個第二部伺服器可以位於不同資料中心，因為沒有基礎結構共用與 hello 主要伺服器。 您必須手動複製 hello 主要伺服器 toohello 第二部伺服器上進行任何組態變更。

您可以使用暫存伺服器 tootest 新自訂組態和 hello 效果它對您的資料。 您可以預覽 hello 做的變更，並調整 hello 設定。 Hello 新設定感到滿意時，您可以設 hello 暫存伺服器 hello 作用中的伺服器，並設定 hello 舊的使用中伺服器 toostaging 模式。

您也可以使用此方法 tooreplace hello 作用中的同步伺服器。 準備 hello 新伺服器，並將它設定 toostaging 模式。 請確定它是否處於良好狀態，停用預備模式 （讓它成為使用中），並關閉 hello 目前作用中的伺服器。

它是可能 toohave 多個臨時伺服器時想 toohave 不同資料中心內的多個備份。

## <a name="multiple-azure-ad-tenants"></a>多個 Azure AD 租用戶
我們建議一個組織在 Azure AD 中有單一租用戶。
您計劃 toouse 多個 Azure AD 租用戶之前，請參閱 hello 文章[Azure AD 中的系統管理單元管理](../active-directory-administrative-units-management.md)。 它涵蓋了常見的案例，您可以使用單一租用戶。

![多個樹系和多個租用戶的拓撲](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Azure AD Connect 同步處理伺服器和 Azure AD 租用戶之間有 1:1 的關聯性。 在每個 Azure AD 租用戶中，您將需要一個 Azure AD Connect 同步處理伺服器安裝。 設計會隔離 hello Azure AD 租用戶執行個體。 也就是說，一個租用戶中的使用者看 hello 中的使用者其他租用戶。 如果您想要這樣的分隔方式，這是支援的組態。 否則，您應該使用 hello 單一 Azure AD 租用戶模型。

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>每個物件只在 Azure AD 租用戶運作一次
![已篩選的單一樹系拓撲](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

在此拓撲中，一個 Azure AD Connect 同步伺服器是連線的 tooeach Azure AD 租用戶。 hello Azure AD Connect 同步伺服器必須設定篩選，如此每一個具有物件 toooperate 互斥集合。 您可以比方說，為範圍的每個伺服器 tooa 特定網域或組織單位。

DNS 網域只能在單一 Azure AD 租用戶中註冊。 hello hello 在內部部署 Active Directory 執行個體中的 hello 使用者的 Upn 也必須使用不同的命名空間。 例如，hello 前面圖片，在三個不同的 UPN 尾碼都登錄在 hello 在內部部署 Active Directory 執行個體： contoso.com、 fabrikam.com 和 wingtiptoys.com。每個內部部署 Active Directory 網域中的 hello 使用者使用不同的命名空間。

Hello Azure AD 租用戶執行個體之間沒有 GALSync。 只有在使用者 hello 同一個租用戶 hello 通訊錄在 Exchange Online 及 Skype 商務顯示。

此拓撲具有下列 hello 限制否則支援的案例：

* 只有其中一個 hello Azure AD 租用戶可以啟用 Exchange 混合式與 hello 在內部部署 Active Directory 執行個體。
* Windows 10 裝置只能與一個 Azure AD 租用戶相關聯。
* hello 單一登入 (SSO) 選項來驗證的密碼同步處理和傳遞可以搭配只有一個 Azure AD 租用戶。

一組互斥物件的 hello 需求也適用於 toowriteback。 此拓撲不支援部分寫回功能，因為這些功能假設單一內部部署組態。 這些功能包括：

* 使用預設組態的群組回寫。
* 裝置回寫。

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>每個物件在 Azure AD 租用戶運作多次
![單一樹系與多個租用戶的不受支援拓撲](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![單一樹系與多個連接器的不受支援拓撲](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

下列工作不受支援：

* 同步處理 hello 相同使用者 toomultiple Azure AD 租用戶。
* 進行組態變更，讓一個 Azure AD 中的使用者顯示為另一個 Azure AD 租用戶中的連絡人。
* 修改 Azure AD Connect 同步處理 tooconnect toomultiple Azure AD 租用戶。

### <a name="galsync-by-using-writeback"></a>使用回寫 GALSync
![多個樹系和多個目錄的不受支援拓撲，具有將焦點放在 Azure AD 的 GALSync](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![多個樹系和多個目錄的不受支援拓撲，具有將焦點放在內部部署 Azure AD 的 GALSync](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Azure AD 租用戶在設計上是隔離的。 下列工作不受支援：

* 從另一個 Azure AD 租用戶中變更資料的 Azure AD Connect 同步 tooread hello 組態。
* 匯出使用者與連絡人 tooanother 在內部部署 Active Directory 執行個體，使用 Azure AD Connect 同步處理。

### <a name="galsync-with-on-premises-sync-server"></a>具備內部部署同步處理伺服器的 GALSync
![多個樹系和多個目錄拓撲中的 GALSync](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

您可以使用 FIM 2010 或 MIM 2016 內部 toosync 使用者 （透過 GALSync) 兩個 Exchange 組織之間。 一個組織中的 hello 使用者顯示為外部使用者/連絡人中 hello 另一個組織。 這些不同的內部部署 Active Directory 執行個體可同步處理至它們自己的 Azure AD 租用戶。

## <a name="next-steps"></a>後續步驟
如何針對這些案例，Azure AD Connect tooinstall 參閱的 toolearn[的 Azure AD Connect 自訂安裝](active-directory-aadconnect-get-started-custom.md)。

深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解[將內部部署身分識別與 Azure Active Directory 整合](active-directory-aadconnect.md)。
