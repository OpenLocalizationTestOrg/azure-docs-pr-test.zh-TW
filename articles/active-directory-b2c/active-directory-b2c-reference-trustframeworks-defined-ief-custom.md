---
title: "Azure Active Directory B2C：參考 - 信任架構 | Microsoft Docs"
description: "關於 Azure Active Directory B2C 自訂原則與 hello 身分識別體驗架構的主題"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>使用 Azure AD B2C 識別體驗架構定義信任架構

Azure Active Directory B2C (Azure AD B2C) 使用 hello 身分識別體驗架構的自訂原則提供您的組織與集中式服務。 此服務可降低大型社群中的識別身分同盟感興趣的 hello 複雜性。 hello 複雜性會降低的 tooa 單一信任關係和單一中繼資料交換。

Azure AD B2C 自訂原則，以使用 hello 身分識別體驗架構 tooenable 您 tooanswer hello 下列問題：

- 什麼是合法的 hello、 安全性、 隱私權和資料保護原則，必須遵守？
- Hello 連絡人，以及它們變成合格的參與者 hello 程序是誰？
- 誰是 hello accredited 身分識別資訊提供者 （也稱為 「 宣告提供者 」） 以及他們是否提供什麼？
- 誰是 hello accredited 信賴憑證者的合作對象 （及選擇性地執行需要）？
- 什麼是 「 開啟 hello 纜線 」 技術 hello 參與者的互通性需求？
- Hello 交換資訊的數位身分識別必須強制執行的操作"runtime"規則有哪些？

tooanswer 建構所有這些問題，Azure AD B2C 使用 hello 身分識別體驗架構使用 hello 信任架構 (TF) 的自訂原則。 讓我們來看一下這個結構，並想想它能提供什麼。

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>了解 hello 信任架構和同盟管理的基礎

hello 信任架構是寫入的 hello 身分識別、 安全性、 隱私權和資料保護原則的 toowhich 感興趣的社群參與者都必須符合規格。

同盟身分識別可作為基礎，來實現網際網路規模的使用者身分識別保證。 委派給身分識別管理 toothird 合作對象，就可以重複使用單一的數位身分識別的使用者與多個信賴憑證者的合作對象。  

識別保證要求身分識別提供者 (IdPs) 和屬性提供者 (AtPs) 遵守 toospecific 安全性、 隱私權和操作的原則和作法。  如果他們不能執行直接操作，信賴憑證者的合作對象 (Rp) 必須開發與 hello IdPs 和 AtPs 他們選擇 toowork 具有信任關係。  

消費者和提供者的數位身分識別資訊的 hello 數目成長時，它困難 toocontinue 成對管理這些信任關聯性，或甚至 hello 成對交換所需的網路連線的 hello 技術中繼資料.  同盟中樞在解決這些問題上，只有些許成就。

### <a name="what-a-trust-framework-specification-defines"></a>信任架構規格定義的內容
TFs 會 hello linchpins 的 hello 身分開啟 Exchange (OIX) 信任架構模型，其中每個感興趣的社群由特定的 TF 規格。 這類 TF 規範會定義︰

- **hello hello 定義感興趣的 hello 社群的安全性和隱私權度量：**
    - hello 保證層級 (LOA) 所提供/所需的參與者。例如，已排序集合的信心評等的 hello 真實性的數位身分識別資訊。
    - hello 層級的保護 (LOP) 是提供/所需的參與者。例如，hello 保護數位身分識別資訊的感興趣的 hello 社群參與者由信賴等級的已排序集合。

- **hello hello 數位身分識別資訊說明已提供/所需的參與者**。

- **hello 技術原則生產和耗用的數位身分識別資訊，以及因此測量 LOA 和 LOP。這些通常寫入原則包括下列的原則類別目錄的 hello:**
    - 身分識別證明原則，例如︰個人的身分識別資訊受到多嚴格的審查？
    - 安全性原則，例如︰資訊的完整性和機密性受到多嚴格的保護？
    - 隱私權原則，例如︰使用者對於個人識別資訊 (PII) 擁有何種控制權？
    - 生存能力原則，例如︰若提供者停止營業，PII 功能的持續性和保護如何運作？

- **hello 生產和耗用的數位身分識別資訊的技術設定檔。這些設定檔包括：**
    - 界定在指定的 LOA 下，數位身分識別資訊所適用的介面。
    - 線上互通性的技術需求。

- **hello 的 hello 描述各種角色 hello 社群的參與得以執行，這些角色 hello 所需要的 toofulfill 限定性條件。**

因此 TF 規格會管理身分識別資訊感興趣的 hello 社群的 hello 參與者之間交換： 信賴憑證者的合作對象、 身分識別和屬性提供者，以及屬性能力檢查器。

TF 規格是做為參考的 hello 控管的原則會規定 hello 判斷提示的感興趣的 hello 社群及 hello 社群內的數位身分識別資訊的耗用量的一或多個文件。 它是一組文件的原則和程序設計 tooestablish 信任用於感興趣的社群成員之間的線上交易的 hello 數位身分識別。  

換句話說，TF 規格定義 hello 規則適用於社群建立可行的同盟識別身分生態系統。

目前沒有廣泛的協議上 hello 權益的這種方法。 沒有一定的 framework 規格促進 hello 開發使用可驗證的安全性，保證和隱私權特性，這表示，就可以重複跨多個群體感興趣的數位身分識別生態系統的信任。

因此，Azure AD B2C 自訂原則，以使用 hello 身分識別體驗架構 hello 規格使用作為其資料表示法 hello 基礎 TF toofacilitate 互通性。  

利用 hello 身分識別體驗架構的 azure AD B2C 自訂原則表示為人性化和可供電腦讀取的資料混合 TF 規格。 此模型 （通常區段所比較導向控管） 的某些小節會以參考 toopublished 安全性和隱私權原則文件，以及 hello 表示相關程序 （如果有的話）。 在 詳細資料 hello 組態中繼資料和執行階段規則，以便操作自動化其他章節。

## <a name="understand-trust-framework-policies"></a>了解信任架構原則

實作，根據 hello TF 規格包含一組原則，可讓您完整控制識別行為和體驗。  Azure AD B2C 自訂原則，以利用 hello 身分識別體驗架構啟用您 tooauthor，並建立您自己 TF 透過這類宣告式的原則，可以定義及設定：

- hello 文件參考或參考，其定義的 hello 社群與相關 toohello TF hello 同盟識別身分生態系統。 它們是連結 toohello TF 文件。 hello （預先定義） 的操作"runtime"規則或 hello 使用者皆可自動化及/或控制 hello exchange 和使用方式的 hello 宣告。 這些使用者旅程會與 LOA (和 LOP) 相關聯。 原則所具備的使用者旅程圖因此會有不同的 LOA (和 LOP)。

- hello 身分識別和屬性提供者或使用 hello 宣告提供者，它們支援以及與相關 toothem hello （的頻外） LOA/LOP 履歷表 hello 社群的技術的利息和 hello 設定檔中。

- hello 與屬性能力檢查器或整合宣告提供者。

- hello hello 社群中的信賴憑證者合作對象 （依推斷）。

- 建立參與者之間的網路通訊的 hello 中繼資料。 交易 tooplumb 期間會使用此中繼資料，hello 設定檔技術，以及 「 開啟 hello 纜線 」 之間的互通性 hello 信賴憑證者的合作對象及其他社群參與者。

- 如果有任何 hello 通訊協定轉換 (例如，SAML、 OAuth2，WS-同盟和 OpenID Connect)。

- hello 驗證需求。

- hello 多因素的協調流程如果有的話。

- 所有可用的 hello 宣告和對應 tooparticipants 感興趣的社群的共用的結構描述。

- 所有的 hello 宣告轉換，以及在此內容、 toosustain hello exchange 和使用方式的 hello 宣告 hello 資料可能最小化。

- hello 繫結和加密。

- hello 宣告的儲存體。

### <a name="understand-claims"></a>了解宣告

> [!NOTE]
> 我們共同參照 tooall hello 可能的類型可能會交換做為 「 宣告 」 的身分識別資訊： 個人識別使用者的驗證認證、 身分識別檢查、 通訊裝置、 實體位置，關於宣告屬性，依此類推。  
>
> 我們使用 hello 詞彙 「 宣告 」-而不是屬性 」-因為線上交易，這些資料成品不可以直接驗證信賴憑證者合作對象的 hello 的事實。 而是它們判斷提示或宣告的 hello 信賴憑證者的合作對象必須開發足夠信心 toogrant hello 終端使用者的要求的交易的事實相關。  
>
> 我們也會使用 「 宣告 」 因為使用 hello 身分識別體驗架構的自訂原則對於 Azure AD B2C 設計 toosimplify hello exchange 的所有類型的數位身分識別資訊以一致的方式，不論是否 hello 基礎 hello 詞彙通訊協定被定義使用者驗證或屬性擷取。  同樣地，我們使用 「 宣告提供者 」 toocollectively 時，請參考 tooidentity 提供者、 屬性提供者，以及屬性的能力檢查器我們不想讓其特定函式之間 toodistinguish hello 詞彙。   

因此，這些原則會控管如何在信賴憑證者、識別提供者和屬性提供者以及屬性驗證者之間交換身分識別資訊。 這些原則會控制信賴憑證者的驗證工作需要使用哪一個識別提供者和屬性提供者。 您應將這些原則視為特定領域語言 (DSL)，也就是特定應用程式定義域專用的電腦語言，並具有繼承、*if* 陳述式、多型。

這些原則會構成 hello hello TF 建構運用 hello 身分識別體驗架構的 Azure AD B2C 自訂原則中的電腦可讀取的部分。 其中包括所有 hello 操作詳細資料，包括宣告提供者的中繼資料和技術的設定檔、 宣告的結構描述定義、 宣告轉換函式，以及填滿的使用者皆 toofacilitate 操作的協調流程中，提供自動化功能。  

則會被認為 toobe*生動的文件*因為關於 hello 作用中的參與者，宣告 hello 原則中的時間而改變其內容的機會。 另外還有 hello 潛在 hello 條款和條件的參與者可能會變更。  

同盟的設定和維護大幅簡化了防護信賴憑證者的合作對象從進行中的信任和連線重新設定為不同的宣告提供者/能力檢查器加入或離開 （hello 社群所代表） hello 的一組原則。

互通性是另一項重大挑戰。 其他宣告提供者/能力檢查器都必須整合，因為信賴憑證者的合作對象是不太可能 toosupport 所有 hello 必要通訊協定。 Azure AD B2C 自訂原則來解決這個問題支援業界標準通訊協定，藉由套用特定的使用者皆 tootranspose 要求當信賴憑證者的合作對象和屬性提供者不支援 hello 相同的通訊協定。  

使用者皆包含通訊協定設定檔和中繼資料所使用的 tooplumb 」 上 hello 纜線 」 之間的互通性 hello 信賴憑證者的合作對象與其他參與者。 也有一些作業的執行階段規則只套用的 tooidentity 資訊交換要求/回應訊息的強制執行 hello TF 規格的一部分已發佈的原則相容性。 使用者皆 hello 概念是索引鍵 toohello 自訂 hello 客戶經驗。 它也看出 hello 系統 hello 通訊協定層級的運作方式。

基礎，信賴憑證者的合作對象應用程式和入口網站可以根據其內容，叫用 Azure AD B2C 自訂原則運用 hello 身分識別體驗架構傳遞 hello 的特定原則的名稱，和取得精確 hello 行為和資訊沒有任何 muss、 複雜，或可能會想要的交換。
