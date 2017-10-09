---
title: "aaaScenarios 和範例的訂閱控管 |Microsoft 文件"
description: "提供的範例提供 tooimplement 常見案例的 Azure 訂用帳戶控管。"
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>實作 Azure 企業 Scaffold 的範例
本主題提供的企業如何實作 hello 的建議範例[Azure 企業版 scaffold](resource-manager-subscription-governance.md)。 它會使用虛構的公司名稱 Contoso tooillustrate 最佳作法為常見案例。

## <a name="background"></a>背景
Contoso 是提供客戶的所有項目從 「 軟體即服務 」 模型 tooa 封裝模型的供應鏈方案的全球公司部署在內部部署。  它們在具有大量的開發中心印度、 hello 美國和加拿大的 hello 地球開發軟體。

hello 公司 hello ISV 部份分為數個重要的企業中管理產品的獨立的業務單位。 每個業務單位都有自己的開發人員、產品經理和架構設計人員。

hello 企業的技術服務 (ETS) 業務單位提供集中式的 IT 功能，及管理數個業務單位的裝載應用程式的資料中心。 管理 hello 資料中心，以及 hello ETS 組織提供並管理 （例如電子郵件和網站） 的集中式共同作業和網路/電話語音服務。 它們也會為沒有操作人員的較小業務單位管理客戶面向工作負載。

本主題中使用下列角色的 hello:

* Dave 是 hello ETS Azure 系統管理員。
* Alice 就是 Contoso 的主管的 hello 供應鏈商務單位中開發。

Contoso 必須 toobuild 的特定業務應用程式和客戶對向應用程式。 它決定在 Azure 上的 toorun hello 應用程式。 Dave 讀取 hello[精準的訂閱控管](resource-manager-subscription-governance.md)主題，而且現在準備好 tooimplement hello 建議。

## <a name="scenario-1-line-of-business-application"></a>案例 1︰企業營運應用程式
Contoso 公司正在建置 hello 世界各地由開發人員使用來源的程式碼管理系統 (BitBucket) toobe。  hello 應用程式用於基礎結構即服務 (IaaS) 主控，並且包含 web 伺服器和資料庫伺服器。 開發人員存取他們的開發環境中的伺服器，但不需要存取 toohello Azure 中的伺服器。 Contoso ETS 希望 tooallow hello 應用程式擁有者和團隊 toomanage hello 應用程式。 hello 應用程式才可使用 Contoso 公司網路上時。 Dave 需要 tooset hello 訂用帳戶註冊此應用程式。 hello 訂用帳戶也會主控其他開發人員相關軟體在未來的 hello。  

### <a name="naming-standards--resource-groups"></a>命名標準與資源群組
Dave 建立訂用帳戶 toosupport 所有 hello 業務單位之間是通用的開發人員工具。 他需要 toocreate hello 訂用帳戶有意義的名稱與資源群組 （適用於 hello 應用程式和 hello 網路）。 他會建立下列訂用帳戶和資源群組的 hello:

| Item | 名稱 | 說明 |
| --- | --- | --- |
| 訂閱 |Contoso ETS DeveloperTools Production |支援一般開發人員工具 |
| 資源群組 |rgBitBucket |包含 hello 應用程式 web 伺服器和資料庫伺服器 |
| 資源群組 |rgCoreNetworks |包含 hello 虛擬網路和網站對網站閘道連線 |

### <a name="role-based-access-control"></a>角色型存取控制
在建立其訂用帳戶之後, Dave 要 hello 適當小組的 tooensure 及應用程式擁有者可以存取他們的資源。 Dave 認為每個小組有不同的需求。 他會利用 Contoso 的內部部署 Active Directory (AD) tooAzure Active Directory 中，從已同步的 hello 群組，並提供存取 toohello 小組 hello 正確層級。

Dave 指派 hello 遵循 hello 訂用帳戶的角色：

| 角色 | 指派太| 說明 |
| --- | --- | --- |
| [擁有者](../active-directory/role-based-access-built-in-roles.md#owner) |Contoso AD 提供的受管理識別碼 |此識別碼會透過 Contoso 的身分識別管理工具進行即時 (JIT) 存取控制，可確保完整稽核訂用帳戶擁有者存取權。 |
| [安全性管理員](../active-directory/role-based-access-built-in-roles.md#security-manager) |安全性和風險管理部門 |此角色可讓使用者在 hello Azure 資訊安全中心的 toolook 和 hello hello 資源狀態。 |
| [網路參與者](../active-directory/role-based-access-built-in-roles.md#network-contributor) |網路小組 |此角色可讓 Contoso 網路小組 toomanage hello 網站 tooSite VPN，而且 hello 虛擬網路。 |
| *自訂角色* |應用程式擁有者 |Dave 建立角色，授與 hello 的資源群組中的 hello 能力 toomodify 資源。 如需詳細資訊，請參閱 [Azure RBAC 中的自訂角色](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>原則
Dave 具有下列需求來管理資源 hello 訂用帳戶中的 hello:

* Hello 開發工具支援 hello 世界各地的開發人員，因為他不希望 tooblock 使用者建立的任何區域中的資源。 不過，他需要的 tooknow 會建立資源。
* 他很關心成本問題。 因此，他想 tooprevent 應用程式擁有者建立不必要地高度耗費資源的虛擬機器。  
* 因為此應用程式提供許多業務單位中的開發人員，他想 tootag 每個資源與 hello 業務單位和應用程式擁有者。 藉由使用這些標記，ETS 就可以結帳 hello 適當小組。

他要建立 hello 下列[資源管理員原則](resource-manager-policy.md):

| 欄位 | 效果 | 說明 |
| --- | --- | --- |
| location |稽核 |稽核 hello 建立的任何區域中的 hello 資源 |
| 類型 |deny |拒絕建立 G 系列虛擬機器 |
| 標籤 |deny |需要應用程式擁有者標籤 |
| 標籤 |deny |需要成本中心標籤 |
| 標籤 |附加 |標記名稱附加**BusinessUnit**及標記值**ETS** tooall 資源 |

### <a name="resource-tags"></a>資源標籤
Dave 了解他需要 hello BitBucket 實作 toohave hello bill tooidentify hello 成本中心上的特定資訊。 此外，Dave 想的 tooknow 所有 hello ETS 擁有的資源。

他將新增 hello 下列[標記](resource-group-using-tags.md)toohello 資源群組和資源。

| 標籤名稱 | 標籤值 |
| --- | --- |
| ApplicationOwner |hello hello 人員負責管理此應用程式名稱。 |
| CostCenter |hello 支付 hello Azure 耗用量的 hello 群組的成本中心。 |
| BusinessUnit |**ETS** （hello 訂用帳戶相關聯 hello 業務單位） |

### <a name="core-network"></a>核心網路
資訊安全和風險管理小組會檢閱 Dave 建議的 Contoso ETS hello 規劃 toomove hello 應用程式 tooAzure。 他們想 tooensure hello 應用程式不會公開 toohello 網際網路。  Dave 也有在 hello 未來將會移動的 tooAzure 開發人員應用程式。 這些應用程式都需要公用介面。  toomeet 這些需求，他提供內部和外部虛擬網路和網路安全性群組 toorestrict 存取權。

他會建立 hello 下列資源：

| 資源類型 | 名稱 | 說明 |
| --- | --- | --- |
| 虛擬網路 |vnInternal |Hello BitBucket 應用程式搭配使用，且已透過 ExpressRoute tooContoso 公司網路連線。  特定的 IP 位址空間的 hello 應用程式提供子網路 (sbBitBucket)。 |
| 虛擬網路 |vnExternal |適用於未來需要公開端點的應用程式。 |
| 網路安全性群組 |nsgBitBucket |可確保該 hello 此工作負載的受攻擊面降至最低由允許只在連接埠 443 hello 子網路的 hello 應用程式所在 (sbBitBucket) 上的連線。 |

### <a name="resource-locks"></a>資源鎖定
Dave 會辨識 hello 連線從 Contoso 公司網路 toohello 內部虛擬網路必須受到保護從任何不定的指令碼或意外刪除。

他要建立 hello 下列[資源鎖定](resource-group-lock-resources.md):

| 鎖定類型 | 資源 | 說明 |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |防止使用者刪除 hello 虛擬網路或子網路，但不會防止 hello 加入新的子網路。 |

### <a name="azure-automation"></a>Azure 自動化
Dave 沒有 tooautomate 此應用程式。 雖然他建立了 Azure 自動化帳戶，但他一開始不會使用它。

### <a name="azure-security-center"></a>Azure 資訊安全中心
Contoso IT 服務管理需要 tooquickly 識別和處理潛在威脅。 也會想要 toounderstand 哪些問題可能存在。  

toofulfill 這些需求、 Dave 啟用 hello [Azure 資訊安全中心](../security-center/security-center-intro.md)，並提供存取 toohello 安全性管理員角色。

## <a name="scenario-2-customer-facing-app"></a>案例 2︰客戶面向應用程式
由各種機會 tooincrease engagement 與 Contoso 的客戶使用忠誠度卡 hello 商務領導 hello 供應鏈商務單位中。 Alice 的小組必須建立此應用程式，並決定 Azure 會增加其功能 toomeet hello 的商務需求。 Alice 搭配 Dave ETS tooconfigure 兩個訂用帳戶來開發及操作此應用程式。

### <a name="azure-subscriptions"></a>Azure 訂用帳戶
Dave 登入 toohello Azure 企業版入口網站，並會看見 hello 供應鏈部門已經存在。  但是，因為這個專案是針對在 Azure 中的 hello 供應鏈小組 hello 第一個開發專案，Dave 辨認 hello 需要 Alice 的開發小組的新帳戶。  他會建立 hello"r&d 」 帳號她的小組，並指派存取 tooAlice。 Alice 透過 hello Azure 入口網站登入，並建立兩個訂閱： 一個 toohold hello 程式開發伺服器和一個 toohold hello 實際執行伺服器。  建立 hello 下列訂用帳戶時，她會遵循 hello 先前建立的命名標準：

| 訂用帳戶用途 | 名稱 |
| --- | --- |
| 開發 |SupplyChain ResearchDevelopment LoyaltyCard Development |
| Production |SupplyChain Operations LoyaltyCard Production |

### <a name="policies"></a>原則
Dave 和 Alice 討論 hello 應用程式，並識別此應用程式只提供在 hello 北美地區的客戶。  Alice 和她的小組計劃 toouse Azure 應用程式服務環境和 Azure SQL toocreate hello 應用程式。 在開發期間，他們可能需要 toocreate 虛擬機器。  Alice 想 tooensure 她的開發人員必須 hello 資源必要 tooexplore 且不含納入 ETS 檢查問題。

Hello**開發訂用帳戶**，他們建立 hello 下列原則：

| 欄位 | 效果 | 說明 |
| --- | --- | --- |
| location |稽核 |稽核 hello 建立的任何區域中的 hello 資源。 |

不會限制使用者可以在開發中，建立的 sku hello 類型，而且不需要的任何資源群組或資源標記。

Hello**生產訂用帳戶**，他們建立 hello 下列原則：

| 欄位 | 效果 | 說明 |
| --- | --- | --- |
| location |deny |拒絕 hello 建立 hello 美式資料中心以外的任何資源。 |
| tags |deny |需要應用程式擁有者標籤 |
| 標籤 |deny |需要部門標籤。 |
| 標籤 |附加 |附加表示實際執行環境的標記 tooeach 資源群組。 |

它們不會限制使用者可以在生產環境中建立的 sku hello 型別。

### <a name="resource-tags"></a>資源標籤
Dave 了解他帳單及擁有權必須 toohave 特定資訊 tooidentify hello 正確的商務群組。 他會針對資源群組和資源定義資源標籤。

| 標籤名稱 | 標籤值 |
| --- | --- |
| ApplicationOwner |hello hello 人員負責管理此應用程式名稱。 |
| department |hello 支付 hello Azure 耗用量的 hello 群組的成本中心。 |
| EnvironmentType |**生產**(即使 hello 訂用帳戶包含**生產**hello 名稱中包含此標記，可讓您輕鬆識別查看 hello 入口網站中，或在 hello 帳單上的資源時。) |

### <a name="core-networks"></a>核心網路
資訊安全和風險管理小組會檢閱 Dave 建議的 Contoso ETS hello 規劃 toomove hello 應用程式 tooAzure。 他們想 hello 忠誠度卡應用程式的 tooensure 正確地隔離並 DMZ 網路中受保護。  toofulfill 這項需求，Dave 和 Alice 建立外部虛擬網路和網路安全性群組 tooisolate hello 忠誠度卡應用程式從 hello Contoso 公司網路。  

Hello**開發訂用帳戶**，他們建立：

| 資源類型 | 名稱 | 說明 |
| --- | --- | --- |
| 虛擬網路 |vnInternal |做 hello Contoso 忠誠度卡開發環境，並透過 ExpressRoute tooContoso 公司網路連接。 |

Hello**生產訂用帳戶**，他們建立：

| 資源類型 | 名稱 | 說明 |
| --- | --- | --- |
| 虛擬網路 |vnExternal |裝載 hello 忠誠度卡應用程式，而且未直接 tooContoso 的 ExpressRoute 連線。 程式碼會透過其原始碼系統推入直接 toohello PaaS 服務。 |
| 網路安全性群組 |nsgBitBucket |可確保該 hello 此工作負載的受攻擊面降至最低只允許 TCP 443 上的 繫結的通訊。  Contoso 也正在調查如何使用 Web 應用程式防火牆提供額外的保護。 |

### <a name="resource-locks"></a>資源鎖定
Dave Alice 授與和決定 tooadd 某些錯誤的程式碼推送的 hello 環境 tooprevent 被意外刪除中的 hello 關鍵資源上的資源鎖定。

他們建立 hello 下列鎖定：

| 鎖定類型 | 資源 | 說明 |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |tooprevent 刪除 hello 虛擬網路或子網路的人員。 hello 鎖定無法防止 hello 加入新的子網路。 |

### <a name="azure-automation"></a>Azure 自動化
Alice 和開發團隊有大量的 runbook toomanage hello 環境為此應用程式。 hello runbook 允許 hello 新增/刪除 hello 應用程式的節點和其他 DevOps 工作。

toouse 它們可讓這些 runbook，[自動化](../automation/automation-intro.md)。

### <a name="azure-security-center"></a>Azure 資訊安全中心
Contoso IT 服務管理需要 tooquickly 識別和處理潛在威脅。 也會想要 toounderstand 哪些問題可能存在。  

toofulfill 這些需求，Dave 啟用 Azure 資訊安全中心。 他可確保 hello Azure 資訊安全中心監視 hello 資源，並提供存取 toohello DevOps 與安全性小組。

## <a name="next-steps"></a>後續步驟
* toolearn 有關建立資源管理員範本，請參閱[最佳作法來建立 Azure 資源管理員範本](resource-manager-template-best-practices.md)。

