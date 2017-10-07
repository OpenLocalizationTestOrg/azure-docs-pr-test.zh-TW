---
title: "對於企業移動 tooAzure aaaBest 作法 |Microsoft 文件"
description: "描述 scaffold，企業可以使用 tooensure 安全且容易管理的環境。"
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Azure 企業 Scaffold - 規定的訂用帳戶治理
企業正逐漸採用 hello 公用雲端中的為其靈活度和彈性。 它們會利用 hello 雲端優點 toogenerate 營收，或最佳化 hello 商務的資源。 Microsoft Azure 提供許多服務，企業可以組合的建置組塊 tooaddress 像廣泛的工作負載和應用程式。 

但是，了解 toobegin 很困難。 之後決定 toouse Azure 時，一些經常遇到問題：

* 「如何符合某些國家/地區中資料主權的法律需求？」
* 「如何確保他人不會不慎變更重要系統？」
* 「如何知道每個資源支援什麼，才能精準地斟酌考量並回收成本？」

空的訂用帳戶與沒有防護滑軌 hello 潛在是鉅的任務。 此空格可能會妨礙您移動 tooAzure。

本文章提供起始點的技術專業人員 tooaddress hello 需要控管，並以 hello 它需要的靈活性來平衡。 它引進引導中實作和管理他們的 Azure 訂用帳戶的組織的企業 scaffold hello 概念。 

## <a name="need-for-governance"></a>治理需求
當您移動 tooAzure，您必須解決控管早期 tooensure hello 成功使用 hello 企業中的 hello 雲端 hello 的主題。 不幸的是，hello 時間和建立完整的管理系統的科層表示某些業務群組連直接 toovendors 不需要企業 IT。 如果沒有妥善管理 hello 資源，這種方式可以保留 hello 企業開啟 toovulnerabilities。 -靈活度、 彈性和耗用量為基準的價格-hello 公用雲端的 hello 特性而言很重要需要 tooquickly toobusiness 群組符合 hello 要求客戶 （內部和外部）。 但是，企業 IT 需要 tooensure 資料和系統有效地保護。

在現實生活中，scaffolding 會是使用的 toocreate hello 基礎的 hello 結構。 hello scaffold 引導 hello 一般外框，並提供更具永久性系統 toobe 掛接錨點。 企業 scaffold 是 hello 相同： 一組彈性化控制項和 Azure 建置的 hello 公用雲端服務提供結構 toohello 環境中，與錨點的功能。 它提供 hello 產生器 (IT 和商務群組) foundation toocreate 並附加新的服務。

hello scaffold 根據我們收集從用戶端的各種大小的許多合作的作法。 這些用戶端的範圍從小型組織 hello 雲端 tooFortune 500 企業和獨立軟體廠商會移轉與開發 hello 雲端中的方案中開發方案。 hello 企業 scaffold 是 「 特殊用途的 「 toobe 彈性 toosupport 傳統的 IT 工作負載和敏捷式軟體開發的工作負載;例如，開發人員建立軟體做為服務 (SaaS) 應用程式為基礎的 Azure 功能。

hello 企業 scaffold 是預定的 toobe hello 基礎，在 Azure 中的每個新訂用帳戶。 可讓系統管理員 tooensure 工作負載符合 hello 最小的控管組織的需求而又商業群組和開發人員可以從快速達到他們自己的目標。

> [!IMPORTANT]
> 控管是 Azure 重要 toohello 成功。 此發行項的目標 hello 企業 scaffold 的技術實作，但只會牽涉到 hello 更廣泛程序和 hello 元件之間的關聯性。 原則控管往下流動 hello 由上至下，而且會決定哪些 hello 的商務想 tooachieve。 當然，hello 建立 Azure 控管模型包含代表從 IT，但是更重要的是應該具有從商務群組和安全和風險管理增強式表示法。 Hello 結束時，在企業 scaffold 是免除商業風險 toofacilitate 組織的任務和目標。
> 
> 

下列映像的 hello 描述 hello scaffold hello 元件。 hello foundation 依賴部門、 帳戶和訂用帳戶的實心計劃。 hello 功能是由資源管理員的原則和強式命名的標準所組成。 hello scaffold hello 其餘來自核心的 Azure 功能，以及功能，讓安全且容易管理的環境。

![scaffold 元件](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure 自 2008 年引進後就急速成長。 這股成長所需 Microsoft 工程小組 toorethink 來管理和部署服務的方法。 hello Azure Resource Manager 模型 2014年中所導入，並取代 hello 傳統部署模型。 資源管理員可讓的組織 toomore 輕鬆地部署、 組織和控制 Azure 資源。 Resource Manager 在建立資源時納入平行處理，以加快部署複雜、互相依存方案的速度。 它也包含細微的存取控制和 hello 能力 tootag 資源的中繼資料。 Microsoft 建議您建立透過 hello 資源管理員模型的所有資源。 hello 企業 scaffold 明確設計 hello 資源管理員的模型。
> 
> 

## <a name="define-your-hierarchy"></a>定義您的階層
hello scaffold hello foundation 是 hello Azure Enterprise 註冊 （與 hello 企業版入口網站）。 hello enterprise 註冊定義 hello 形狀和使用的公司內的 Azure 服務，且 hello 核心控管結構。 Hello 企業協議內的客戶是否能 toofurther 細分成部門、 帳戶和最後，訂閱 hello 環境。 Azure 訂用帳戶是 hello 基本的單位，其中包含所有資源。 它也可在 Azure 中定義數個限制，例如核心、資源等的數目。

![階層](./media/resource-manager-subscription-governance/agreement.png)

每個企業不同，且在 hello 先前的映像中的 hello 階層可讓針對極大彈性的 Azure hello 公司內的組織方式。 實作包含在此文件中的 hello 指引之前, 您應該模型階層，並了解 hello 影響帳單、 資源的存取和複雜性。

hello 三種常見的模式為 Azure 註冊項目是：

* hello**功能**模式
  
    ![函數](./media/resource-manager-subscription-governance/functional.png)
* hello**業務單位**模式 
  
    ![業務](./media/resource-manager-subscription-governance/business.png)
* hello**地理**模式
  
    ![地理](./media/resource-manager-subscription-governance/geographic.png)

您套用 hello scaffold 在 hello 訂用帳戶層級 tooextend hello 控管需求 hello 企業版的 hello 訂用帳戶。

## <a name="naming-standards"></a>命名標準
hello 第一個 pillar 的 hello scaffold 時命名標準。 設計良好的命名標準可以讓您 tooidentify hello 入口網站、 帳單和指令碼中的資源。 最有可能的是，您已經有內部部署基礎結構的命名標準。 當新增 Azure tooyour 環境時，您應該擴充這些命名標準 tooyour Azure 資源。 命名標準促進更有效率的 hello 環境所有層級管理。

> [!TIP]
> 針對命名慣例：
> * 檢閱並採用盡可能 hello[模式和實務方針](../guidance/guidance-naming-conventions.md)。 本指南可協助您決定有意義的命名標準。
> * 將 camelCasing 使用於資源的名稱 (例如 myResourceGroup 和 vnetNetworkName)。 附註： 有某些資源，例如儲存體帳戶，其中 hello 唯一的選項是 toouse 小寫 （和其他特殊字元）。
> * 請考慮使用 Azure 資源管理員 （hello 下一節中所述） 原則 tooenforce 命名標準。
> 
> hello 上述秘訣協助您實作一致的命名慣例。

## <a name="policies-and-auditing"></a>原則和稽核
hello 第二個 pillar 的 hello scaffold 牽涉到建立[Azure 資源管理員原則](resource-manager-policy.md)和[稽核 hello 活動記錄檔](resource-group-audit.md)。 資源管理員原則可讓您在 Azure 中的 hello 能力 toomanage 風險。 您可以定義一些原則，藉由限制、強制執行或稽核特定動作來確保資料主權。 

* 原則是預設**允許**系統。 您藉由定義並指派原則 tooresources 拒絕或稽核動作的資源控制動作。
* 原則定義會以原則定義語言 (if-then 條件) 描述原則。
* 您可使用 JSON (Javascript 物件標記法) 格式的檔案建立原則。 定義原則之後, 您將其指派 tooa 特定範圍： 訂用帳戶、 資源群組或資源。

原則有多個動作可讓更細緻方法 tooyour 案例。 hello 動作包括：

* **拒絕**： 區塊 hello 資源要求
* **稽核**： 可讓 hello 要求而且會加入列 toohello 活動記錄 （這可以是使用的 tooprovide 警示或 tootrigger runbook）
* **附加**： 加入指定的資訊 toohello 資源。 例如，如果資源上沒有 "CostCenter" 標籤，則新增具有預設值的該標籤。

### <a name="common-uses-of-resource-manager-policies"></a>Resource Manager 原則的常見用途
Azure 資源管理員的原則是 hello Azure toolkit 中的強大工具。 它們可讓您 tooavoid 未預期的成本、 tooidentify 成本中心透過標記，以及 tooensure 資源的需求均符合該規範。 當原則組合與 hello 內建稽核功能時，您可以以複雜且靈活的解決方案。 原則可讓公司 tooprovide 控制項之 「 傳統 IT 」 的工作負載及"Agile"工作負載;例如，開發客戶應用程式。 hello 我們看到原則的最常見的模式是：

* **地理-相容性資料 sovereignty** -Azure 提供 hello 世界各地的區域。 企業通常會想 toocontrol 資源 （無論 tooensure 資料 sovereignty tooensure 資源只會建立或關閉 toohello 結束取用者的 hello 資源） 的建立位置。
* **成本管理** - Azure 訂用帳戶可以包含許多類型的資源。 企業也希望 tooensure 該標準訂閱可讓您避免使用過大的資源，可以成本數百個月份或多個 （美元）。
* **預設透過必要的標記的控管**-需要標記是其中一個 hello 最常見和高度所需的功能。 使用 Azure 資源管理員原則企業正無法 tooensure 資源會適當地標記。 hello 最常見的標記是： 部門、 資源擁有者，以及環境類型 （例如生產、 測試、 開發）

**範例**

企業營運應用程式的「傳統 IT」訂用帳戶

* 對所有資源強制使用「部門」和「擁有者」標籤
* 限制資源建立 toohello 北美地區
* 限制 hello 能力 toocreate G 系列 Vm 與 HDInsight 叢集

可供業務單位建立雲端應用程式的「敏捷式」環境

* toomeet 資料 sovereignty 需求，允許資源 hello 建立只在特定地區。
* 對所有資源強制使用「環境」標籤。 如果沒有標籤建立資源，則附加 hello**環境： 未知**標記 toohello 資源。
* 當資源建立於北美地區以外時進行稽核，但不阻止。
* 建立高成本的資源時進行稽核。

> [!TIP]
> hello 跨組織的資源管理員原則的常見用法是 toocontrol*其中*資源可以建立和*什麼*可以建立類型的資源。 Tooproviding 上的控制項，除了*其中*和*什麼*，許多企業使用原則 tooensure 資源有 hello 適當的中繼資料 toobill 回供取用。 我們建議您套用的 hello 訂用帳戶層級的原則：
> 
> * 地區相容性/資料主權
> * 成本管理
> * 必要標籤 (依照業務需求判斷，例如 BillTo、應用程式擁有者)
> 
> 您可以在較低的範圍層級套用其他原則。
> 
> 

### <a name="audit---what-happened"></a>稽核 - 發生什麼情形？
tooview 環境如何運作，您需要 tooaudit 使用者活動。 Azure 中的大多數資源類型都會建立診斷記錄檔，您可以透過記錄檔工具或在 Azure Operations Management Suite 中進行分析。 您可以收集跨多個訂用帳戶 tooprovide 部門的活動記錄檔或企業檢視。 稽核記錄都是重要的診斷工具，而且在 hello Azure 環境中的重要機制 tootrigger 事件。

從資源管理員部署的活動記錄可讓您 toodetermine hello**作業**，花費了備妥並且執行它們的人員。 使用 Log Analytics 等工具可以收集和彙總活動記錄檔。

## <a name="resource-tags"></a>資源標籤
當您組織中的使用者加入資源 toohello 訂用帳戶時，會變得越來越重要 tooassociate 與 hello 適當部門、 客戶及環境的資源。 您可以將附加到中繼資料 tooresources[標記](resource-group-using-tags.md)。 您使用標記 tooprovide hello 資源或資訊 hello 擁有者。 標記 toonot 只彙總與群組資源，以各種方式可讓您，不過基於計費的 hello 使用該資料。 您可以在具有向上 too15 索引鍵： 值配對中的資源標記。 

資源標記有彈性，而且應該附加的 toomost 資源。 常見資源標籤的範例如下︰

* BillTo
* 部門 (或業務單位)
* 環境 (生產、預備、開發)
* 層次 (Web 層、應用程式層)
* 應用程式擁有者
* ProjectName

![標籤](./media/resource-manager-subscription-governance/resource-group-tagging.png)

如需更多標籤範例，請參閱 [Azure 資源的建議命名慣例](../guidance/guidance-naming-conventions.md)。

> [!TIP]
> 請考慮針對下列各項制定可強制標記的原則︰
> 
> * 資源群組
> * 儲存體
> * 虛擬機器
> * 應用程式服務環境/Web 伺服器
> 
> 此標記的策略會識別您的訂用帳戶之間 hello 商務、 財務、 安全性、 風險管理及 hello 環境的整體管理需要哪些中繼資料。 

## <a name="resource-group"></a>資源群組
資源管理員可讓您 tooput 資源成有意義的群組管理、 計費，或自然親和性。 如先前所述，Azure 有兩個部署模型。 先前的傳統模型，hello 的基本管理單位的 hello 訂用帳戶在 hello。 您很難 toobreak 向訂用帳戶，導致 toohello 建立大量的訂用帳戶內的資源。 使用 hello 資源管理員模型時，我們可了解資源群組的 hello 簡介。 資源群組是資源的容器，其中的資源具有共同的生命週期或共用「所有 SQL 伺服器」或「應用程式 A」等屬性。

資源群組不能包含在彼此，資源只可以隸屬 tooone 資源群組。 您可以將某些動作套用於資源群組中的所有資源。 例如，刪除資源群組中移除 hello 資源群組中的所有資源。 一般而言，您將整個應用程式或相關的系統放 hello 相同的資源群組。 例如，Contoso 的 Web 應用程式的三層應用程式會包含 hello 網頁伺服器、 應用程式伺服器和 SQL server 中 hello 相同的資源群組。

> [!TIP]
> 您將資源群組的組織可能會不同 「 傳統 IT 」 的工作負載太 「 敏捷式軟體開發 IT 」 的工作負載：
> 
> * 「 傳統 IT 」 的工作負載最常分組 hello 內的項目相同的生命週期，例如應用程式。 依照應用程式分組，即可進行個別應用程式管理。
> * 「 敏捷式軟體開發 IT 」 的工作負載通常 toofocus 外部客戶面對雲端應用程式上的。 hello 資源群組應該會反映 hello 層面 （例如 Web 層，應用程式層） 的部署和管理。
> 
> 了解您的工作負載可協助您開發資源群組策略。

## <a name="role-based-access-control"></a>角色型存取控制
您可能會問自己 「 誰應該有存取 tooresources 」？ 以及「如何控制此存取權？」 允許或不允許存取 toohello Azure 入口網站，以及控制在 hello 入口網站存取 tooresources 而言十分重要。 

Azure 最初發行時，存取控制項 tooa 訂用帳戶已基本： 系統管理員或共同管理員。 存取 tooa 訂用帳戶中 hello 傳統模型隱含存取 tooall hello 資源 hello 入口網站中。 這種欠缺更細微的控制會造成訂閱 tooprovide 合理的存取控制層級進行 Azure 註冊 toohello 激增。

不再需要此種訂用帳戶激增情況。 以角色為基礎的存取控制，您可以將使用者指派給 toostandard 角色 （例如通用的 「 讀取器 」 和 「 寫入器 」 類型的角色）。 您也可以定義自訂角色。

> [!TIP]
> tooimplement 角色型存取控制：
> * 您公司的身分識別存放區 (最常見 Active Directory) tooAzure Active Directory 使用 hello AD Connect 工具的連接。
> * 控制 hello 管理員/共同管理員的訂用帳戶使用受管理的身分識別。 **不要**指派系統管理員/共同管理員 tooa 新訂用帳戶擁有者。 相反地，使用 RBAC 角色 tooprovide**擁有者**權限 tooa 群組或個人。
> * 新增 Active Directory 中的 Azure 使用者 tooa 群組 （例如，應用程式 X 擁有者）。 使用 hello 同步處理的群組 tooprovide 群組成員 hello 適當的權限 toomanage hello 的資源群組包含 hello 應用程式。
> * 遵循授與 hello 的 hello 原則**最小權限**必要的 toodo hello 預期的工作。 例如：
>   * 部署群組： 僅能 toodeploy 資源的群組。
>   * 虛擬機器管理： A 也就是可以 toorestart Vm 分組 （適用於作業）
> 
> 這些祕訣可協助您跨訂用帳戶管理使用者存取。

## <a name="azure-resource-locks"></a>Azure 資源鎖定
您的組織加入核心服務 toohello 訂用帳戶，變得越來越重要 tooensure 這些服務的可用 tooavoid 業務中斷。 [資源鎖定](resource-group-lock-resources.md)讓您修改或刪除這些裝置會有重大影響您的應用程式或雲端基礎結構上的高價值資源 toorestrict 作業。 您可以套用鎖定 tooa 訂用帳戶、 資源群組或資源。 一般而言，您可以套用鎖定 toofoundational 資源，例如虛擬網路、 閘道和儲存體帳戶。 

資源鎖定目前支援兩個值︰CanNotDelete 和 ReadOnly。 CanNotDelete 表示 （使用 hello 適當的權限） 的使用者仍然可以讀取或修改資源，但不能予以刪除。 ReadOnly 表示經過授權的使用者無法刪除或修改資源。

toocreate 或刪除管理鎖定，您必須能夠存取太`Microsoft.Authorization/*`或`Microsoft.Authorization/locks/*`動作。
Hello 內建角色中，只有擁有者和使用者存取系統管理員會授與這些動作。

> [!TIP]
> 應該以鎖定保護核心網路選項。 意外刪除的站對站 VPN 閘道，請將而言 tooan Azure 訂用帳戶。 Azure 不允許您 toodelete 正在使用中，虛擬網路，但套用更多的限制是很有幫助的預防措施。 
> 
> * 虛擬網路︰CanNotDelete
> * 網路安全性群組︰CanNotDelete
> * 原則︰CanNotDelete
> 
> 原則也是重要的 toohello 維護適當的控制項。 我們建議您套用**CanNotDelete**鎖定 toopolices 正在使用中。

## <a name="core-networking-resources"></a>核心網路資源
存取 tooresources 可以是內部 （在 hello 公司的網路） 或外部 (透過 hello 網際網路)。 它是方便使用者在您的組織 tooinadvertently put 的資源在 hello 錯誤的位置，然後可能會開啟 toomalicious 存取。 如同在內部部署裝置，企業必須將適當的控制項 tooensure Azure 使用者做出 hello 正確的決策。 針對訂用帳戶治理，我們會找出可提供基本存取控制的核心資源。 hello 核心資源所組成：

* **虛擬網路**是子網路的容器物件。 雖然並非絕對必要，通常使用連接的應用程式 toointernal 公司資源時。
* **網路安全性群組**類似 tooa 防火牆，而且透過 hello 網路提供規則的方式資源可以 「 交談 」。 它們提供更精確地控制如何 / 如果 toohello 網際網路或其他子網路中的可以連接的子網路 （或虛擬機器） hello 相同虛擬網路。

![核心網路](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> 針對網路：
> * 建立專用的 tooexternal 向工作負載的虛擬網路和內部網路的工作負載。 這種方式可以減少不小心將適用於外部對向的空間中的內部工作負載的虛擬機器的放置 hello 機會。
> * 設定網路安全性群組 toolimit 存取。 最少封鎖存取 toohello 網際網路從內部虛擬網路以及從外部虛擬網路的區塊存取 toohello 公司網路。
> 
> 這些祕訣可協助您實作安全的網路資源。

### <a name="automation"></a>自動化
個別管理資源相當耗時，而且某些作業可能容易發生錯誤。 Azure 提供了各種自動化功能，包括 Azure 自動化、Logic Apps 和 Azure Functions。 [Azure 自動化](../automation/automation-intro.md)可讓系統管理員 toocreate 和管理資源定義 runbook toohandle 一般工作。 您可以使用 PowerShell 程式碼編輯器或圖形化編輯器來建立 Runbook。 您可以產生複雜的多階段工作流程。 Azure 自動化通常是使用的 toohandle 常見工作，例如正在關閉未使用的資源，或在回應 tooa 特定觸發程序中建立資源，而不需要人為介入。

> [!TIP]
> 針對自動化：
> * 建立 Azure 自動化帳戶，並檢閱 hello 可用之 runbook （圖形化和命令列） 用於 hello [Runbook 庫](../automation/automation-runbook-gallery.md)。
> * 匯入並自訂重要 Runbook，以便自己使用。
> 
> 常見的案例是 hello 能力 tooStart/關機排程上的虛擬機器。 有範例 hello 組件庫中可用的 runbook 同時處理這種情況下，並教導您如何 tooexpand 它。
> 
> 

## <a name="azure-security-center"></a>Azure 資訊安全中心
可能是其中一個最大障礙 toocloud 採用 hello 已 hello 考量安全性。 風險的 IT 管理員和安全性部門需要 tooensure Azure 中的資源的安全性。 

hello [Azure 資訊安全中心](../security-center/security-center-intro.md)提供 hello 安全性狀態的 hello 訂閱中資源的中央檢視，並提供建議，協助防止遭盜用的資源。 它可以啟用更細微的原則 （例如，套用原則 toospecific 資源群組可讓它們可以明智地處理其對 toohello 風險 hello 企業 tootailor）。 最後，Azure 資訊安全中心是開放式平台，可讓 Microsoft 夥伴和獨立軟體廠商 toocreate 軟體連接到 Azure 資訊安全中心 tooenhance 其功能。 

> [!TIP]
> 根據預設，Azure 資訊安全中心會在每個訂用帳戶中啟用。 不過，您必須啟用資料收集虛擬機器 tooallow Azure 資訊安全中心 tooinstall 其代理程式，並開始收集資料。
> 
> ![資料收集](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>後續步驟
* 現在您已經學會有關訂閱控管，它是時間 toosee 實際上這些建議。 請參閱[實作 Azure 訂用帳戶治理的範例](resource-manager-subscription-examples.md)。

