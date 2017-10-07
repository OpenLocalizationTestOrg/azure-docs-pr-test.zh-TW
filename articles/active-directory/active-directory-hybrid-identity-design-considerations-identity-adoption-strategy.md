---
title: "aaaAzure Active Directory 混合式身分識別設計考量-定義混合式身分識別採用策略 |Microsoft 文件"
description: "條件式存取控制與 Azure Active Directory 檢查 hello 您挑選驗證 hello 使用者時，才能允許存取 toohello 應用程式特定的條件。 一旦符合這些條件，hello 使用者已驗證，而且允許存取 toohello 應用程式。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>定義混合式身分識別採用策略
在這項工作，您將為您混合式身分識別解決方案 toomeet hello 的商務需求所討論的定義 hello 混合式身分識別採用策略：

* [判斷商務需求](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [判斷目錄同步處理需求](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [判斷多重要素驗證需求](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>定義商務需求策略
hello 第一項工作會滿足決定 hello 組織商務需求。  這可能非常廣泛，一不小心就會發生範圍蔓延。  Hello 開頭中保持簡單，但一定要記得 tooplan 設計，可容納並促進 hello 未來變更。  無論它是簡單的設計或非常複雜，Azure Active Directory 是支援 Office 365、 Microsoft Online Services 和雲端感知的應用程式的 hello Microsoft 身分識別平台。

## <a name="define-an-integration-strategy"></a>定義整合策略
Microsoft 有三個主要的整合案例，分別為雲端身分識別、同步處理身分識別和同盟身分識別。  您應該規劃採用這些整合策略的其中一個。  hello 的策略有所不同而且 hello 決策選擇其中一個可能包含，何種類型，您選擇要 tooprovide 的使用者體驗，您擁有 hello 現有基礎結構已經就地、 部分，以及什麼是最符合成本效益的 hello。  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

hello 上方圖中所定義的 hello 案例包括：

* **雲端身分識別**： 這些是只存在於 hello 雲端的身分識別。  在 Azure AD 的 hello 案例中，它們會位於特別在 Azure AD 目錄中。
* **同步處理**： 這些是存在於內部部署身分識別和 hello 雲端中。  使用 Azure AD Connect 時，將會以現有的 Azure AD 帳戶建立或聯結這些使用者。  hello 使用者的密碼雜湊同步處理從 hello 在內部部署環境 toohello 雲端中稱為密碼雜湊。  使用同步處理時 hello 一個需要注意的是，如果 hello 在內部部署環境中停用使用者時，就可以在該帳戶狀態 tooshow 的 too3 時數在 Azure AD 中。  這是因為 toohello 同步處理時間間隔。
* **同盟**： 這些身分識別存在於這兩個內部部署和 hello 雲端中。  使用 Azure AD Connect 時，將會以現有的 Azure AD 帳戶建立或聯結這些使用者。  

> [!NOTE]
> 如需有關 hello 同步處理選項讀取[整合內部部署身分識別與 Azure Active Directory](connect/active-directory-aadconnect.md)。
> 
> 

下表中的 hello 有助於決定 hello 優點和缺點的 hello 下列策略：

| 策略 | 優點 | 缺點 |
| --- | --- | --- |
| **雲端身分識別** |更容易為小組織的 toomanage。 <br> Tooinstall 在內部部署沒有額外的硬體所需執行任何動作<br>輕鬆地停用 如果 hello 使用者離開公司 hello |存取 hello 雲端中的工作負載時，使用者將需要 toosign 中 <br> 密碼可能會或可能不是 hello 相同的雲端和內部部署身分識別 |
| **已同步處理** |內部部署密碼會驗證內部部署和雲端目錄  <br>小型、 中型或大型組織更容易 toomanage <br>使用者可以對一些資源進行單一登入 (SSO) <br> Microsoft 對於同步處理的慣用方法 <br> 更容易 toomanage |有些客戶可能不願意 toosynchronize 其目錄以 hello 雲端特定的公司原則到期 |
| **同盟** |使用者可以有單一登入 (SSO)  <br>如果使用者已終止或離開時，可以立即停用 hello 帳戶和撤銷存取權，<br> 支援同步處理所無法解決的進階案例 |更多步驟 toosetup 和設定 <br> 較高的維護 <br> 可能需要額外的硬體 hello STS 基礎結構 <br> 可能需要額外的硬體 tooinstall hello 同盟伺服器。如果使用 AD FS，則需要額外的軟體 <br> 需要大量的設定才能使用 SSO <br> 重大失敗點的 hello 同盟伺服器已關機，使用者將無法再 tooauthenticate |

### <a name="client-experience"></a>用戶端體驗
您使用的 hello 策略會規定 hello 使用者登入體驗。  hello 下表提供您哪些 hello 使用者應預期其登入的相關資訊會遇到 toobe。  請注意，所有同盟識別提供者並非在所有案例中都支援 SSO。

**加入網域和私人網路應用程式**：

|  | 同步處理身分識別 | 同盟身分識別 |
| --- | --- | --- |
| 網頁瀏覽器 |表單型驗證 |單一登入，有時需要 toosupply 組織識別碼 |
| Outlook |提示輸入認證 |提示輸入認證 |
| 商務用 Skype (Lync) |提示輸入認證 |在 Lync 中需要單一登入，在 Exchange 中會提示輸入認證 |
| Skydrive Pro |提示輸入認證 |單一登入 |
| Office Pro Plus 訂用帳戶 |提示輸入認證 |單一登入 |

**外部或未受信任的來源**：

|  | 同步處理身分識別 | 同盟身分識別 |
| --- | --- | --- |
| 網頁瀏覽器 |表單型驗證 |表單型驗證 |
| Outlook、商務用 Skype (Lync)、Skydrive Pro、Office 訂用帳戶 |提示輸入認證 |提示輸入認證 |
| Exchange ActiveSync |提示輸入認證 |在 Lync 中需要單一登入，在 Exchange 中會提示輸入認證 |
| 行動應用程式 |提示輸入認證 |提示輸入認證 |

如果您有根據工作 1 您有合作對象 IdP 或進行 toouse 第 3 tooprovide 同盟與 Azure AD，您需要支援 toobe 留意 hello 下列功能：

* 這可能會與相容 hello SP Lite 設定檔的任何 SAML 2.0 提供者可支援驗證 tooAzure AD 和相關聯的應用程式
* 支援被動驗證，這有助於 auth tooOWA，SPO，等等。
* Exchange Online 用戶端可支援透過 hello SAML 2.0 增強用戶端設定檔 (ECP)

您也必須知道無法使用哪些功能：

* 如果沒有 WS-Trust/同盟支援，其他所有使用中用戶端都會中斷
  * 這表示沒有 Lync 用戶端、 OneDrive 用戶端，Office 訂用帳戶，Office Mobile 先前 tooOffice 2016
* 轉換 Office toopassive 驗證可讓他們 toosupport 純 SAML 2.0 IdPs，但支援仍會在用戶端的用戶端

> [!NOTE]
> Hello 文章 http://aka.ms/ssoproviders 讀取最新的清單。
> 
> 

## <a name="define-synchronization-strategy"></a>定義同步處理策略
在這項工作中，您將定義 hello 工具將會使用的 toosynchronize hello 組織的內部部署資料 toohello 雲端，以及您應該使用的拓撲。  因為大部分的組織使用 Active Directory，某些詳細資料中提供使用上述的 Azure AD Connect tooaddress hello 問題的詳細資訊。  不具有 Active Directory 環境中，沒有使用 FIM 2010 R2 的相關資訊，或 MIM 2016 toohelp 規劃此策略。  不過，Azure AD Connect 的未來版本將支援 LDAP 目錄，因此視您的時間軸，這項資訊可能是無法 tooassist。

### <a name="synchronization-tools"></a>同步處理工具
Hello 年來，有存在數個同步處理工具，並將其用於各種案例中。  目前 Azure AD Connect 是 hello 移 tootool 所有支援的案例所選擇。  AAD 同步和 DirSync 也依然存在，甚至現在就在您的環境中。 

> [!NOTE]
> Hello 最新資訊有關 hello 支援功能的各項工具，請參閱[目錄整合工具比較](active-directory-hybrid-identity-design-considerations-tools-comparison.md)發行項。  
> 
> 

### <a name="supported-topologies"></a>支援的拓撲
定義同步處理策略時，必須決定用 hello 拓撲。 步驟 2，您可以判斷哪些拓樸中發現的資訊是 hello 適當一個 toouse 根據 hello。 hello 單一樹系、 單一 Azure AD 拓撲是最常見的 hello 與單一 Active Directory 樹系和 Azure AD 的單一執行個體所組成。  這會 toobe 大多數的 hello 案例中使用時，則 hello 預期拓撲 hello 圖所示，使用 Azure AD 連接 Express 安裝。

![](./media/hybrid-id-design-considerations/single-forest.png)單一樹系案例是非常普遍的大型且更小型組織 toohave 多個樹系，如圖 5 所示。

> [!NOTE]
> 如需有關 hello 不同內部部署和 Azure AD 與 Azure AD Connect 同步處理的拓樸閱讀 hello 文章[Azure AD Connect 的拓撲](connect/active-directory-aadconnect-topologies.md)。
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

多樹系案例

如果 hello 本例然後 hello 多 forest 單一 Azure AD 拓撲應該考慮，如果 hello 下列項目，則為 true:

* 使用者在所有樹系有只有 1 識別 – 用來唯一識別 [使用者] 區段下方的 hello 更詳細地說明。
* hello 使用者會驗證其身分識別位於 toohello 樹系
* UPN 和來源錨點 (固定 ID) 來自此樹系
* 所有樹系都可以存取 Azure AD connect – 這表示它不需要加入 toobe 網域，而且可以放在 DMZ 中，如果這簡化此作業。
* 使用者只有一個信箱
* 裝載使用者信箱的 hello 樹系有 hello 最佳的資料品質 hello Exchange 全域通訊清單 (GAL) 中可見的屬性
* 如果沒有信箱 hello 使用者，則任何樹系可能會使用的 toocontribute 這些值
* 如果您有連結的信箱，然後另外還有另一個帳戶中使用不同的樹系 toosign 中。

> [!NOTE]
> 存在於這兩個內部部署和 hello 雲端中的物件是 「 連線 」 透過唯一識別碼。 在 hello 內容中的目錄同步作業，這個唯一識別碼是參考的 tooas hello SourceAnchor。 在 hello 內容中的單一登入，這是參考的 tooas hello ImmutableId。 [針對 Azure AD Connect 設計概念](connect/active-directory-aadconnect-design-concepts.md#sourceanchor)的 SourceAnchor 的 hello 使用多個考量。
> 
> 

如果 hello 上述條件都不成立，而且您有多個使用中的帳戶或多個信箱，Azure AD Connect 將挑選其中一個，並忽略其他 hello。  如果您已連結信箱，但沒有任何其他帳戶，這些帳戶將不會匯出的 tooAzure AD，且該使用者將不會是任何群組的成員。  這是不同的方式就是過去的 hello 與 DirSync 和是刻意 toobetter 支援這些多樹系案例。 多樹系案例是以 hello 圖所示。

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**多樹系多個 Azure AD 案例**

建議只進行組織，但是它的 Azure AD 中的單一目錄的 toohave 支援它的 Azure AD Connect 同步處理伺服器與 Azure AD 目錄之間保留 1:1 關聯性。  對於每個 Azure AD 執行個體，您需要安裝 Azure AD Connect。  此外，Azure AD 中，依設計隔離並在一個 Azure AD 的執行個體中的使用者並不會無法 toosee 另一個執行個體的使用者。

它可，而其中一個支援的 tooconnect 內部部署 Active Directory toomultiple Azure AD 目錄中 hello 圖所示的執行個體：

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**單一樹系篩選案例**

順序 toodo 這個 hello 下列必須為真：

* Azure AD Connect 同步作業伺服器必須設定篩選，以各自有一組互斥的物件。  這樣做，比方說，藉由範圍的每個伺服器 tooa 特定網域或 OU。
* DNS 網域只能在單一註冊 Azure AD 目錄，因此 hello hello 中的 hello 使用者的 upn，請在內部部署 AD 必須使用不同的命名空間
* 一個 Azure AD 的執行個體中的使用者才會從其執行個體可以 toosee 使用者。  將不會在 hello 無法 toosee 使用者其他執行個體
* 只有其中一個 hello Azure AD 目錄可以啟用 Exchange 混合式 hello 與內部部署 AD
* 相互專用性也適用於 toowrite 後。  這造成此拓撲不支援部分回寫功能，因為這些功能都假設使用單一內部部署組態。  其中包括：
  * 使用預設組態的群組回寫
  * 裝置寫回

請注意 hello 下列不支援，並且不應該被選為實作：

* 不支援多個 Azure AD Connect 同步伺服器連接 toohello 相同的 Azure AD 目錄，即使它們是互斥的設定的 toosynchronize 物件集的 toohave
* 它不支援 toosync hello 相同使用者 toomultiple Azure AD 目錄。 
* 它也是不支援的 toomake 變更 toomake 使用者在其中一個做為 Azure AD tooappear 連絡另一個 Azure AD 目錄中的設定。 
* 它也是不支援的 toomodify Azure AD Connect 同步處理 tooconnect toomultiple Azure AD 目錄。
* Azure AD 目錄在設計上是隔離的。 是不支援的 toochange hello 組態的其他 Azure AD 目錄中嘗試 toobuild 一般和統一 GAL hello 目錄之間的 Azure AD Connect 同步處理 tooread 資料。 它也是不支援的 tooexport 使用者連絡 tooanother 為在內部部署 AD 中使用 Azure AD Connect 同步處理。

> [!NOTE]
> 如果您的組織會從連接 toohello 網際網路限制網路上的電腦，本文章列出 hello 端點 （Fqdn、 IPv4 和 IPv6 位址範圍），您應該在包含您輸出的允許清單和 Internet Explorer 信任的網站區域的用戶端電腦 tooensure 您的電腦可以成功使用 Office 365。 如需詳細資訊，請參閱 [Office 365 URL 和 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)。
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>定義多重要素驗證策略
在這項工作中，您將定義 hello 多重要素驗證策略 toouse。  Azure Multi-Factor Authentication 有兩個不同的版本。  一個是以雲端為基礎，其他 hello 是在內部部署基礎使用 hello Azure MFA Server。  根據 hello 評估您未在上述您可以判斷哪一種解決方案是 hello 正確的另一個用於您的策略。  使用 hello 表 toodetermine 哪種設計選項最符合您的公司安全性需求：

多重要素設計選項：

| 資產 toosecure | Hello 雲端中的 MFA | MFA 內部部署 |
| --- | --- | --- |
| Microsoft 應用程式 |yes |yes |
| 在 hello 應用程式庫中的 SaaS 應用程式 |yes |yes |
| 透過 Azure AD App Proxy 發佈的 IIS 應用程式 |yes |yes |
| 不透過 hello Azure AD 應用程式 Proxy 發行的 IIS 應用程式 |no |yes |
| VPN、RDG 等遠端存取 |no |yes |

即使您可能已結束某個方案策略，您仍然需要 toouse hello 評估上述上您的使用者位於何處。  這可能會導致 hello 方案 toochange。  您可以決定這項需求使用 hello tooassist 表：

| 使用者位置 | 建議的設計選項 |
| --- | --- |
| Azure Active Directory |多重 Authentication hello 雲端中 |
| Azure AD 和使用 AD FS 同盟的內部部署 AD |兩者 |
| Azure AD 和內部部署 AD，使用 Azure AD Connect，沒有密碼同步處理 |兩者 |
| Azure AD 和內部部署，使用 Azure AD Connect，搭配密碼同步處理 |兩者 |
| 內部部署 AD |Multi-Factor Authentication Server |

> [!NOTE]
> 您也應該確定您選取的 hello 多重要素驗證設計選項支援 hello 功能所需的設計。  如需詳細資訊請參閱[為您選擇 hello multi-factor authentication 的安全性解決方案](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure)。
> 
> 

## <a name="multi-factor-auth-provider"></a>Multi-Factor Auth Provider
依預設，擁有 Azure Active Directory 租用戶的全域管理員可以使用 Multi-Factor Authentication。 不過，如果您想要將多重要素驗證 tooall tooextend 的使用者和/或想 tooyour 全域管理員 toobe 無法 tootake 利用功能 hello 管理入口網站、 自訂問候及報告等，然後您必須購買並設定多因素驗證提供者。

> [!NOTE]
> 您也應該確定您選取的 hello 多重要素驗證設計選項支援 hello 功能所需的設計。 
> 
> 

## <a name="next-steps"></a>後續步驟
[判斷資料保護需求](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

