---
title: "aaaDesign Azure 複雜的解決方案範本 |Microsoft 文件"
description: "顯示為複雜的實例設計 Azure Resource Manager 範本的最佳做法"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>部署複雜的解決方案時，設計 Azure Resource Manager 範本的模式
在 Azure Resource Manager 範本上使用彈性的做法，您可以快速且一致地部署複雜的拓撲。 您可以調整這些部署，輕鬆地為核心發展供應項目或極端值的案例或客戶的 tooaccommodate 變化。

本主題是較大份白皮書的一部分。 tooread hello 完整紙張，下載[世界類別 Azure 資源管理員範本考量和證明作法](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)。

範本會結合 hello hello 基礎 hello 適應性與可讀性的 JavaScript Object Notation (JSON) 的 Azure 資源管理員的優點。 使用範本，您可以：

* 以一致的方式部署拓撲及其工作負載。
* 使用資源群組，一併管理應用程式中的所有資源。
* 適用於角色型存取控制 (RBAC) toogrant 適當的存取權 toousers、 群組和服務。
* 使用標記的關聯 toostreamline 工作，例如計費彙總套件。

本文提供在我們的設計工作階段以及真實世界中與 Azure 客戶諮詢小組 (AzureCAT) 客戶進行範本實作過程中所識別的取用案例、架構及實作模式的詳細資訊。 遠離 academic，這些方法會通過驗證的最佳通知 hello 開發的範本 12 hello 頂端以 Linux 為基礎的 OSS 技術，包括： Apache Kafka Apache Spark、 Cloudera、 Couchbase、 的 Hortonworks HDP、 由 DataStax EnterpriseApache Cassandra、 Elasticsearch、 Jenkins、 MongoDB、 PostgreSQL、 Redis 和 Nagios。 

這篇文章會共用您設計架構世界類別 Azure 資源管理員範本這些經過證實的作法 toohelp。  

透過與客戶合作，我們已在企業、系統整合者和 CSV 之間識別出數個 Resource Manager 範本取用體驗。 hello 下列各節提供常見的案例和模式的高階概觀不同客戶類型。

## <a name="enterprises-and-system-integrators"></a>企業和系統整合者
在大型組織中，我們常看到兩種 Resource Manager 範本取用取用者︰內部軟體開發團隊和公司 IT。 我們找到 hello SIs 的 hello 案例對應 toohello 案例，企業，因此 hello 相同的考量。

### <a name="internal-software-development-teams"></a>內部軟體開發團隊
如果您的小組正在開發軟體 toosupport 業務範本可讓您的輕鬆 tooquickly 部署在特定的商務方案中使用的技術。 您也可以使用範本 toorapidly 建立定型環境可讓小組成員 toogain 所需的技巧。

您可以使用範本做為是或擴充或組合這些 tooaccommodate 您的需求。 在範本內使用標記，您可以利用各種不同的檢視 (例如，團隊、專案、個人及教育) 來提供帳單摘要。

企業通常會想軟體開發小組 toocreate 一致部署解決方案的範本。 hello 範本有助於進行條件約束，因此該環境內的特定項目保持固定，而且無法加以覆寫。 例如，銀行可能需要範本 tooinclude RBAC 好讓程式設計人員無法修改銀行方案 toosend 資料 tooa 個人儲存體帳戶。

### <a name="corporate-it"></a>公司 IT
公司 IT 組織通常會使用範本來傳遞雲端容量和雲端裝載功能。

#### <a name="cloud-capacity"></a>雲端容量
企業 IT 群組 tooprovide 雲端容量的小組常見方法是使用"t 恤大小 」，也就是標準供應項目大小例如小型、 中型和大型。 hello t 恤尺寸供應項目可以混合不同資源類型和數量，同時提供可讓可能 toouse 範本的標準化的層級。 hello 範本提供一致的方式來強制執行公司原則，並使用標記 tooprovide 計費 tooconsuming 組織的容量。

例如，您可能需要 tooprovide 開發、 測試或實際執行環境中的 hello 軟體開發團隊可以部署解決方案。 hello 的環境具有預先定義的網路拓撲，且無法變更 hello 軟體開發團隊的項目，例如存取 toohello 公用網際網路和封包檢查的規則。 您也可能使用不同的存取權限 hello 環境對於這些環境的組織特定角色。

#### <a name="cloud-hosted-capabilities"></a>雲端裝載功能
您可以使用範本 toosupport 雲端裝載功能，包括個別軟體套件或提供商務 toointernal 行複合供應項目。 複合供應項目的一個範例是，在預先定義的網路拓撲上，利用最佳化且已連接的組態來提供的「分析即為服務」(分析、視覺化和其他技術)。

雲端託管的功能會受到 hello 安全性與角色建立 hello 供應項目上所建立的雲端容量的考量。 這些功能會依原樣提供，或提供來做為受管理的服務。 Hello 後者，存取限制的角色，才能進行管理的 tooenable 存取到 hello 環境。

## <a name="cloud-service-vendors"></a>雲端服務廠商
之後談話 toomany Csv，找到多個方法，您可以採取 toodeploy 服務向客戶和相關聯的需求。

### <a name="csv-hosted-offering"></a>CSV 裝載的供應項目
如果您在自己的 Azure 訂用帳戶中裝載您供應項目，則有兩種常見的裝載方法：針對每位客戶部署不同的部署，或部署縮放單位來支持針對所有客戶使用的共用基礎結構。

* **針對每位客戶進行不同的部署。** 針對每位客戶進行不同的部署，需要具備不同已知組態的固定拓撲。 這些部署可能會有不同的虛擬機器 (VM) 大小、各種不同的節點數目，以及不同的相關聯儲存體數量。 部署的標記可用來彙總每位客戶的帳單。 RBAC 可能已啟用的 tooallow 客戶存取 tooaspects 其雲端環境。
* **共用多租用戶環境中的縮放單位。** 範本可以代表多租用戶環境的縮放單位。 在此情況下，hello 相同的基礎結構是使用的 toosupport 所有客戶。 hello 部署代表一組提供的容量 hello 裝載供應項目，例如使用者人數和交易數目的層級的資源。 這些縮放單位會隨著需求增加或減少。

### <a name="csv-offering-injected-into-customer-subscription"></a>插入客戶訂用帳戶的 CSV 供應項目
您可以 toodeploy 軟體到擁有一般客戶的訂閱。 您可以使用範本 toodeploy 不同部署到客戶的 Azure 帳戶。

這些部署使用 RBAC，因此您可以更新和管理 hello 客戶的帳戶中的 hello 部署。

### <a name="azure-marketplace"></a>Azure Marketplace
tooadvertise 和賣出透過服務商場，例如 Azure Marketplace 供應項目，您可以開發範本 toodeliver 不同類型的客戶的 Azure 帳戶中執行的部署。 這些不同的部署通常可以用 T 恤尺寸 (小型、中型、大型)、產品/對象類型 (社群、開發人員、企業) 或功能類型 (基本、高可用性) 來描述。  在某些情況下，這些類型可讓您 toospecify hello 部署，例如 VM 類型或磁碟數目的某些屬性。

## <a name="oss-projects"></a>OSS 專案
開放原始碼專案內的資源管理員範本可讓社群 toodeploy 快速使用經過證實的作法的方案。 您可以儲存範本 GitHub 儲存機制中，好讓 hello 社群可以修改它們經過一段時間。 使用者可在自己的 Azure 訂用帳戶中部署這些範本。

hello 下列各節列出您設計您的方案之前需要 tooconsider hello 項目。

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>識別 VM 內部和外部的功能
設計您的範本時，它會是很有幫助 toolook hello 需求方面外部和內部 hello 虛擬機器 (Vm):

* 外部表示 Vm 和其他資源，例如 hello 網路拓樸、 標記，參考 toohello 憑證/機密資料，並且以角色為基礎的存取控制、 以部署的 hello。 這些資源全都是您範本的一部分。
* 內部表示 hello 安裝軟體，以及整體預期狀態設定。 其他機制 (例如 VM 延伸模組或指令碼) 可完整使用或部分使用。 這些機制可能會識別並 hello 範本所執行，但不在其中。

您會執行 「 內部 hello 方塊 」 活動的常見範例包含-  

* 安裝或移除伺服器角色和功能
* 安裝及設定軟體在 hello 節點或叢集層級
* 在 Web 伺服器上部署網站
* 部署資料庫結構描述
* 管理登錄或其他類型的組態設定
* 管理檔案和目錄
* 啟動、停止及管理處理程序和服務
* 管理本機群組和使用者帳戶
* 安裝和管理封裝 (.msi、.exe、yum 等等)
* 管理環境變數
* 執行原生指令碼 (Windows PowerShell、bash 等)

### <a name="desired-state-configuration-dsc"></a>期望狀態組態 (DSC)
思考 hello 的超過部署 Vm 的內部狀態，您會想 toomake 確定此部署不"漂移"從 hello 組態，定義並簽入原始檔控制。 這個方法可確保您的開發人員或操作人員不進行臨機操作變更 tooan 環境不驗證、 測試，或在原始檔控制記錄。 此控制項是很重要，因為 hello 手動變更原始檔控制中。 它們並非也 hello 標準部署的一部分，將會影響未來自動化的 hello 軟體部署。

從安全性觀點來看，除了您的內部員工，期望狀態組態也很重要。 駭客會定期嘗試 toocompromise，並利用軟體系統。 成功時，它是常見的 tooinstall 檔案，並變更 hello 遭入侵的系統狀態。 您可以使用預期的狀態設定，來識別 hello 預期和實際狀態之間的差異和還原已知的組態項目。

有個 hello 最受歡迎的機制 DSC-PowerShell DSC、 Chef 和 Puppet 資源擴充功能。 每個延伸模組可以部署 VM 的 hello 初始狀態，而且也會使用的 toomake 確定 hello 需要維護狀態。

## <a name="common-template-scopes"></a>通用範本範圍
在我們的經驗中，我們看到了範圍所浮現的三個主要解決方案範本。 Hello 下列各節說明這些 – 容量、 功能，以及端對端方案 – 的三個範圍。

### <a name="capacity-scope"></a>容量範圍
容量範圍提供一組標準的預先設定符合規定及原則 toobe 拓撲中的資源。 hello 最常見的範例部署中的企業 IT 或 si 亦然案例的標準的開發環境。

### <a name="capability-scope"></a>功能範圍
功能範圍著重於部署和設定特定技術的拓撲。 常見案例包括像是 SQL Server、Cassandra、Hadoop 等技術。

### <a name="end-to-end-solution-scope"></a>端對端解決方案範圍
端對端解決方案範圍目標超過單一的功能，並改為著重在提供多個功能所組成的結束 tooend 解決方案。  

已設定解決方案範圍的範本範圍會將其本身顯示為一組具有一或多個已設定功能範圍的範本，其中含有解決方案特定的資源、邏輯和期望狀態。 方案範圍範本的範例是結束 tooend 資料管線解決方案範本。 hello 範本可能會混合解決方案專用拓撲和狀態，例如 Kafka、 風暴，以及 Hadoop 的多個功能範圍方案範本。

## <a name="choosing-free-form-vs-known-configurations"></a>選擇自由格式與已知的組態
您一開始可能會認為範本應該授與取用者 hello 具有彈性，但許多考量影響 hello 選擇是否 toouse 自由格式設定與已知的組態。 本章節識別 hello 主要客戶需求和技術形狀共用此文件中的 hello 方法的考量。

### <a name="free-form-configurations"></a>自由格式組態
Hello 介面上的聲音理想自由形式的組態。 它們 tooselect VM 類型可讓您和提供任意的節點數目，並且附加這些節點的磁碟，這樣做為參數 tooa 範本和。 不過，這個做法不適用於某些案例。

在[虛擬機器的大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，識別出 hello 不同 VM 類型和可用的大小，和持久的 hello 數的每個磁碟 （2、 4、 8、 16 個 / 32），可以附加。 每個連接的磁碟可提供 500 個 IOPS，而您可以利用這個 IOPS 數目做為乘數來共用這些磁碟數目的倍數。 例如，16 個磁碟可以是共用的 tooprovide 8000 的 IOPS。 集區會透過 hello 作業系統，在 Linux 中使用 Microsoft Windows 儲存空間或獨立磁碟 (RAID) 的備援陣列中的組態來完成。

自由格式的組態可讓 hello 選取數個 VM 執行個體，不同 VM 類型，且這些執行個體，如 hello VM 類型的各種磁碟大小，和一或多個指令碼 tooconfigure hello VM 內容。

通常，部署可能會有多種類型的節點 (例如主要和資料節點)，因此，經常會針對每個節點類型提供此彈性。

當您開始的任何重要性 toodeploy 叢集，您會開始 toowork 處理這些複雜的案例。 如果您已部署 Hadoop 叢集，例如，8 主要節點和 200 資料節點，以及每個主要節點上的 4 連接的磁碟管理的集區和每個資料節點的集區連接 16 個磁碟具有您必須 208 Vm 和 3,232 磁碟 toomanage。

儲存體帳戶，將節流處理的要求上述其識別的 20000 交易/秒限制，所以您應該查看資料分割的儲存體帳戶，並使用計算 toodetermine hello 適當數目的儲存體帳戶 tooaccommodate 此拓撲。 指定 hello 許多 hello 自由格式的方法，動態計算所支援的組合是必要的 toodetermine hello 適當的資料分割。 hello Azure 資源管理員範本語言不目前提供數學函式，所以您必須執行這些計算程式碼中，產生唯一的硬式編碼的範本與 hello 適當的詳細資料。

在企業 IT 和 SI 案例中，某人必須維護 hello 範本，以及支援一或多個組織部署的 hello 拓撲。 這個額外負擔 (每位客戶都有不同的組態和範本) 並不盡理想。

您可以使用這些範本 toodeploy 環境中客戶的 Azure 訂用帳戶，但同時公司的 IT 團隊和 Csv 通常將它們部署到他們自己的訂用帳戶，使用計費函式 toobill 他們的客戶。 在這些情況下，hello 目標中是用於多位客戶 toodeploy 容量的訂用帳戶和保持部署密集的方式擴展到 hello 訂閱 toominimize 訂用帳戶蔓延到集區，也就是多個訂用帳戶 toomanage。 真正動態部署大小，以達到這種類型的密度需要仔細規劃和其他開發來代表 hello 組織 scaffolding 工作。

此外，您無法建立訂用帳戶，透過 API 呼叫，但必須透過 hello 入口網站手動執行。 任何產生的訂用帳戶蔓延到 hello 訂用帳戶數目增加時，需要人為介入，就無法利用其自動化。 很多，所以部署的 hello 大小可以有變化，您必須 toopre 佈建訂用帳戶數目手動 tooensure 訂用帳戶可用。

考慮這所有因素，真正的自由格式組態乍看之下比較不具吸引力。

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>已知的組態 — hello t 恤調整大小方法
而是提供範本，提供總彈性和無數的變化，我們的經驗中常見的模式是 tooprovide hello 能力 tooselect 已知的組態 — 標準 t 恤作用中，例如沙箱小型、 中型和大型調整大小。 T 恤尺寸的其他範例包括產品供應項目，例如社群版本或企業版本。  在其他情況下，這可能是某種技術的工作負載特定組態，例如，對應減少或沒有 SQL。

許多企業 IT 組織、OSS 廠商和 SI 目前都能在內部部署且虛擬化的環境 (企業) 中或做為「軟體即為服務」(SaaS) 供應項目 (CSV 和 OSV)，使用這種方式來使他們的供應項目可供使用。

這種方法可針對預先為客戶設定好的各種大小提供良好且已知的組態。 沒有已知的設定，客戶必須判斷在自己的叢集大小調整，納入平台資源條件約束，並執行數學 tooidentify hello 產生分割的儲存體帳戶和其他資源 （因為 toocluster 大小和資源條件約束）。 已知的組態可讓客戶 tooeasily 選取 hello 右 t 恤尺寸 — 也就是給定的部署。 此外 toomaking hello 客戶更好的體驗，少數的已知設定更容易 toosupport 並可協助您提供更高的密度。

著重於 T 恤尺寸的已知組態方法在某個尺寸內可能也會擁有各種節點數目。 例如，小型 T 恤尺寸可能介於 3 到 10 個節點之間。  hello t 恤尺寸會設計的 tooaccommodate too10 節點上，提供 hello 消費者 hello 能力 toomake 自由格式選取項目向上 toohello 識別的最大大小。  

根據工作負載類型 t 恤尺寸可能更多的自由格式在本質上就可以部署，但是會有工作負載的不同節點大小和 hello 軟體的組態 hello 節點上的節點的 hello 數目而言。

根據提供的產品，例如 community 或企業，可能會有不同的資源類型和可部署的節點數目上限的 t 恤大小通常與 toolicensing 考量或功能可用性跨 hello 不同供應項目。

您也可以配合客戶具有使用 hello JSON 為基礎的範本的唯一變數。 當處理極端值，您可以合併 hello 適當規劃和開發、 支援和成本的考量。

根據 hello 客戶範本耗用情形，以及識別這個文件的 hello 開頭的需求，我們所識別的範本分解的模式。

## <a name="capacity-and-capability-scoped-solution-templates"></a>已設定容量和功能範圍的解決方案範本
分解提供支援重複使用擴充性測試，和工具的模組化方法 tootemplate 開發。 本章節會詳細說明如何分解方法可以套用的 tootemplates 具有容量或功能領域。

這種方法，主要範本會從範本取用者接收參數值，然後下游連結 tooseveral 類型的範本和指令碼，如下所示。 參數、 靜態變數，並產生的變數是使用的 tooprovide 值出 hello 連結的範本。

![範本參數](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**參數會傳遞 tooa 主要範本則 toolinked 範本**

下列各節焦點 hello 類型的範本和單一範本就會分解成的指令碼的 hello。 hello 章節將用來傳遞各 hello 範本的狀態資訊的方法。 每個範本和 hello 指令碼中的型別 hello 映像描述以及範例。 如需內容相關範例，請參閱本文件稍後的＜整合在一起：範例實作＞。

### <a name="template-metadata"></a>範本中繼資料
範本中繼資料 （hello metadata.json 檔案） 包含描述的範本，在 JSON 中，可讓人了和軟體系統讀取的索引鍵/值組。

![範本中繼資料](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**範本中繼資料描述 hello metadata.json 檔案中**

軟體代理程式可以擷取 hello metadata.json 檔案，並將 hello 資訊和連結 toohello 範本發行網頁或目錄中。 項目包括 itemDisplayName、description、summary、githubUsername 及 dateUpdated。

以下顯示完整的範例檔案。

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>主要的範本
hello 主要範本從使用者接收參數，會使用該資訊 toopopulate 複雜物件變數，並執行 hello 連結的範本。

![主要的範本](./media/best-practices-resource-manager-design-templates/main-template.png)

**hello 主要範本會從使用者接收參數**

提供一個參數是已知的組態類型也稱為 hello t 恤大小參數，因為其標準化的值，例如小型、 中型或大型。 實際上，您可以用多種方式使用此參數。 如需詳細資訊，請參閱本文件稍後的＜已知組態資源範本＞。

不論 hello 已知使用者參數所指定的設定部署一些資源。 這些資源都會使用單一的共用的資源範本佈建和共用的其他範本，以便先執行 hello 共用的資源的範本。

某些資源會選擇性地部署，不論 hello 指定已知的組態。

### <a name="shared-resources-template"></a>共用的資源範本
此範本會提供所有已知組態上通用的資源。 它包含 hello 虛擬網路，可用性設定組，以及不論已部署的 hello 已知的組態範本都需要具備其他資源。

![範本資源](./media/best-practices-resource-manager-design-templates/template-resources.png)

**共用的資源範本**

資源名稱，例如 hello 虛擬網路名稱，以 hello 主要範本為基礎。 您可以將其指定為該範本內的變數，或接收這些 hello 使用者，視需要由您的組織與參數。

### <a name="optional-resources-template"></a>選擇性資源範本
hello 選擇性資源範本包含以程式設計方式部署 hello 的參數或變數的值為基礎的資源。

![選擇性資源](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**選擇性資源範本**

例如，您可以使用選擇性資源範本 tooconfigure 讓間接存取 tooa 部署環境的 hello jumpbox 公用網際網路。 您可以使用參數或變數 tooidentify，是否應該啟用 hello jumpbox 和 hello *concat*函式 toobuild hello 目標 hello 範本名稱，例如*jumpbox_enabled.json*。 連結的範本會使用產生變數 tooinstall hello jumpbox hello。

您可以連結 hello 選擇性資源範本，從多個位置：

* 當適用 tooevery 部署從 hello 共用的資源範本建立的參數驅動的連結。
* 當適用 tooselect 已知的組態 — 比方說，只會在大型部署上安裝，建立從 hello 已知的組態範本參數具或變數急迫連結。

選擇性指定的資源是否可能不重點的 hello 範本的取用者而 hello 範本提供者。 例如，您可能需要 toosatisfy 特定產品需求或產品附加元件 （一般 csv） 或 tooenforce 原則 (一般為 SIs 與企業 IT 群組)。 在這些情況下，您可以使用變數 tooidentify 是否應該部署的 hello 資源。

### <a name="known-configuration-resources-template"></a>已知組態資源範本
在 hello 主要範本中，參數可以是公開的 tooallow hello 範本的取用者 toospecify 所需的已知的設定 toodeploy。 通常，這個已知組態會使用具有一組固定組態大小 (例如，沙箱、小型、中型和大型) 的 T 恤尺寸方法。

![已知組態資源](./media/best-practices-resource-manager-design-templates/known-config.png)

**已知組態資源範本**

hello t 恤大小方法常用，但 hello 參數可代表任何已知的組態集。 例如，您可以為企業應用程式指定一組環境，例如，開發、測試和產品。 您可以使用不同雲端服務 toorepresent 或縮放單位、 產品版本或產品的組態，例如 Community、 Developer 或 Enterprise。

如同 hello 共用的資源的範本，變數會從傳遞 toohello 已知的組態範本：

* 畷樾簅 — 也就是 hello 參數傳送 toohello 主要範本。
* 組織 — 也就是 hello 代表內部的需求或原則 hello 主要範本中的變數。

### <a name="member-resources-template"></a>成員資源範本
在已知組態中，通常會包含一或多個成員節點類型。 例如，使用 Hadoop，您會有主要節點和資料節點。 如果正在安裝 MongoDB，則會有資料節點和仲裁程式。 如果正在部署 DataStax，就必須擁有資料節點，以及已安裝 OpsCenter 的 VM。

![成員資源](./media/best-practices-resource-manager-design-templates/member-resources.png)

**成員資源範本**

每種類型的節點可以有不同的 Vm，連接的磁碟，指令碼 tooinstall 的數字的大小，並設定 hello 節點、 連接埠組態的 hello Vm、 執行個體數目和其他詳細資料。 因此每個節點類型會取得自己成員資源範本，其中包含 hello 和詳細資料部署和設定基礎結構，以及執行指令碼 toodeploy 設定 hello VM 內的軟體。

針對 VM，通常會使用兩種類型的指令碼：廣泛可重複使用和自訂的指令碼。

### <a name="widely-reusable-scripts"></a>廣泛可重複使用的指令碼
廣泛可重複使用的指令碼可以在多種類型的範本上使用。 其中一個 hello 更好的範例，這些廣泛的可重複使用的指令碼設定 RAID Linux toopool 磁碟上，並取得更多的 IOPS。 不論 hello hello VM 中安裝的軟體，此指令碼提供經過證實的作法重複使用常見的案例。

![可重複使用的指令碼](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**成員資源範本能夠呼叫廣泛可重複使用的指令碼**

### <a name="custom-scripts"></a>自訂指令碼
範本通常會呼叫一或多個指令碼，在 VM 內安裝和設定軟體。 常見的模式會出現在大型拓撲中，其中部署了一或多個成員類型的多個執行個體。 安裝指令碼會針對每個可平行執行的 VM 加以啟動，後面接著要在部署所有 VM (或指定成員類型的所有 VM) 之後呼叫的安裝指令碼。

![自訂指令碼](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**成員資源範本可基於特定目的呼叫指定碼，例如 VM 組態**

## <a name="capability-scoped-solution-template-example---redis"></a>已設定功能範圍的解決方案範本範例 - Redis
tooshow 如何實作可能會運作，讓我們看看建置範本，可促進 hello 部署和設定 Redis 以標準 t 恤尺寸的實際範例。  

Hello 部署有一組共用的資源 （虛擬網路、 儲存體帳戶，可用性設定組） 和選擇性的資源 (jumpbox)。 有多個以 T 恤尺寸 (小型、中型、大型) 來表示的已知組態，但每一個都具有單一節點類型。 此外，還有兩個具備特定目的的指令碼 (安裝、組態)。

### <a name="creating-hello-template-files"></a>建立 hello 範本檔案
您會建立名為 azuredeploy.json 的主要範本。

您會建立名為 shared-resources.json 的共用資源範本

建立名為 jumpbox_enabled.json 的 jumpbox 選擇性資源範本 tooenable hello 部署

Redis 只會使用單一節點類型，因此您將建立名為 node-resources.json 的單一成員資源範本。

使用 Redis，您會想 tooinstall 每個個別的節點，然後再將 hello 叢集。  您有指令碼 tooaccommodate hello 安裝並設定，為叢集 redis install.sh 和 redis-叢集-setup.sh。

### <a name="linking-hello-templates"></a>連結 hello 範本
使用範本的連結，連結 toohello 共用的資源範本會建立 hello 虛擬網路外 hello 主要範本。

是否應該部署 jumpbox hello 主要範本 tooenable 取用者的 hello 範本 toospecify 內加入邏輯。 *啟用*值 hello *EnableJumpbox*參數會指出該 hello 客戶想 toodeploy jumpbox。 Hello 範本時提供此值，串連*_enabled*作為 hello jumpbox 功能的後置詞 tooa 基底範本名稱。

hello 主要範本適用於 hello*大型*參數值 t 恤大小，然後使用的尾碼 tooa 基底範本名稱為 out 範本連結中的值太*technology_on_os_large.json*。

hello 拓撲會看起來像下圖。

![Redis 範本](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Redis 範本的範本結構**

### <a name="configuring-state"></a>設定狀態
Hello hello 叢集中的節點，有兩個步驟 tooconfiguring hello 狀態，表示由特定用途的指令碼。  「 redis 叢集-為 install.sh 」 安裝 Redis 並"redis-叢集 setup.sh 的 「 設定 hello 叢集。

### <a name="supporting-different-size-deployments"></a>支援不同大小的部署
內部變數，hello t 恤大小範本指定的每個型別的節點的 hello 數目 hello toodeploy 指定的大小 (*大型*)。 然後將部署此數目的 VM 執行個體使用資源迴圈，將節點名稱附加數字序號，從含有提供唯一的名稱 tooresources *copyIndex()*。 它會依照對於這兩個作用中且暖區域的 Vm，hello t 恤名稱範本中所定義

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>分解和已設定端對端解決方案範圍的範本
具有端對端解決方案範圍的解決方案範本會將重點放在提供端對端解決方案。  這個做法通常是多個已設定功能範圍的範本以及其他資源、邏輯和狀態的組合。

Hello 圖中反白顯示，hello 功能範圍範本所使用的相同模型已擴充與端對端方案領域的範本。

共用資源範本和選擇性資源範本做的 hello hello 容量和功能的功能相同範圍範本方法，但 hello 結束 tooend 解決方案的範圍。

當端點 tooend 解決方案範圍範本也通常有 t 恤大小，hello 已知設定資源範本反映所需的 hello 解決方案指定的已知設定內容。

hello 已知設定資源範本連結 tooone 或更多的功能範圍是相關 toohello tooend 解決方案也 hello 成員資源範本所需的 hello tooend 解決方案的解決方案範本。

Hello t 恤尺寸的 hello 方案可能會與 hello 個別功能範圍範本不同，hello 已知設定資源範本內的變數是使用的 tooprovide hello 適當的值範圍的下游功能方案範本 toodeploy hello 適當 t 恤尺寸。

![端對端](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**hello 模型用於容量或範圍的功能解決方案範本可以輕易地延伸結束 tooend 方案範本範圍**

## <a name="preparing-templates-for-hello-marketplace"></a>準備 hello Marketplace 中的範本
hello 上述方法，輕易地配合企業、 SIs 和 Csv 想 tooeither 部署 hello 範本本身的位置，或啟用其自己的客戶 toodeploy 的案例。

另一個所需的案例將透過 hello marketplace 範本部署。  這個分解方法適用於 hello marketplace，一些微幅變更。

如先前所述，範本可以使用的 toooffer hello 市場中銷售的不同部署類型。 不同的部署類型可能是 T 恤尺寸 (小型、中型、大型)、產品/對象類型 (社群、開發人員、企業) 或功能類型 (基本、高可用性)。

為現有的結束 tooend 如下所示，hello 方案或功能已設定領域的範本可以輕易地利用 toolist hello 不同已知的組態 hello marketplace 中。

hello 參數 toohello 主要範本第一次修改 tooremove hello 名為 tshirtSize 的輸入的參數。

Hello 不同部署類型會對應 toohello 已知設定資源範本，他們也需要 hello 通用資源與組態中找到 hello 共用資源範本，而可能選擇性資源範本。

如果您想 toopublish 您範本 toohello marketplace，您會建立主要範本，以取代的 hello 先前可用的輸入的參數 tshirtSize tooa 變數的內嵌 hello 範本內的不同複本。

![Marketplace](./media/best-practices-resource-manager-design-templates/marketplace.png)

**改寫方案範圍 hello marketplace 的範本**

## <a name="next-steps"></a>後續步驟
* toolearn 有關共用狀態，進出範本，請參閱[共用 Azure Resource Manager 範本中的狀態](best-practices-resource-manager-state.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

