---
title: "aaaKey 功能和 Azure 堆疊中的概念 |Microsoft 文件"
description: "深入了解 hello 重要功能與 Azure 堆疊中的概念。"
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: 09ca32b7-0e81-4a27-a6cc-0ba90441d097
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.openlocfilehash: a9cb3b99dc67a12976ca61b6678f047caab48543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="key-features-and-concepts-in-azure-stack"></a>Azure Stack 的主要功能與概念
如果您是新 tooMicrosoft Azure 堆疊時，這些詞彙和功能描述可能會很有幫助。

## <a name="personas"></a>角色
有兩種使用者的 Microsoft Azure 堆疊，hello 雲端操作員 （提供者） 和 hello 租用戶 （消費者）。

* A**雲端操作員**可以設定 Azure 堆疊，並為其租用戶管理優惠、 計畫、 服務、 配額和定價 tooprovide 資源。  雲端操作員也管理容量，以及回應 tooalerts。  
* A**租用戶**(也參考的 tooas 使用者) 使用 hello 雲端系統管理員提供的服務。 租用戶可以佈建、監視及管理他們所訂閱的服務，例如 Web Apps、儲存體以及虛擬機器。

## <a name="portal"></a>入口網站
hello 與 Microsoft Azure 堆疊互動的主要方法是 hello 管理員入口網站，使用者入口網站和 PowerShell。

每個備份的個別執行個體的 Azure Resource Manager hello Azure 堆疊入口網站。  雲端操作員會使用 hello 系統管理員入口網站 toomanage Azure 堆疊和 toodo 等建立租用戶供應項目。  hello 使用者入口網站 （也參考的 tooas hello 租用戶入口網站） 提供雲端資源，例如虛擬機器、 儲存體帳戶和 Web 應用程式的耗用量自助服務體驗。 如需詳細資訊，請參閱[使用 hello Azure 堆疊系統管理員和使用者入口網站](azure-stack-manage-portals.md)。

## <a name="identity"></a>身分識別 
Azure Stack 使用 Azure Active Directory (AAD) 或 Active Directory 同盟服務 (AD FS) 作為識別提供者。  

### <a name="azure-active-directory"></a>Azure Active Directory
Azure Active Directory 是 Microsoft 的雲端式、多租用識別提供者。  大部分的混合式案例使用 Azure Active Directory 做為 hello 身分識別存放區。

### <a name="active-directory-federation-services"></a>Active Directory Federation Services
您可以選擇 toouse Active Directory Federation Services (AD FS) 已中斷連線 Azure 堆疊的部署。  Azure 堆疊、 資源提供者，以及其他應用程式使用多 hello 相同方式，AD FS 與 Azure Active Directory 所顯示的一樣。 Azure Stack 包含自己的 AD FS 和 Active Directory 執行個體，以及 Active Directory 圖形 API。 Azure 堆疊開發套件支援下列 AD FS 案例 hello:

- 使用 AD FS 登入 toohello 部署。
- 使用金鑰保存庫中的祕密建立虛擬機器
- 建立用於儲存/存取機密資料的保存庫
- 建立訂用帳戶中的自訂 RBAC 角色
- 將使用者指派 tooRBAC 角色資源
- 建立透過 Azure PowerShell 的全系統 RBAC 角色
- 透過 Azure PowerShell 的使用者身分登入
- 建立服務主體中使用這些 toosign tooAzure PowerShell


## <a name="regions-services-plans-offers-and-subscriptions"></a>區域、服務、方案、產品以及訂用帳戶
Azure 堆疊中的服務會傳遞 tootenants 使用區域、 訂閱、 提供項目及計劃。 租用戶可以訂閱 toomultiple 優惠。 優惠可以有一個或多個方案，而方案則可有一或多項服務。

![](media/azure-stack-key-features/image4.png)

範例階層的租用戶的訂用帳戶 toooffers 各有不同的計劃和服務。

### <a name="regions"></a>區域
Azure Stack 區域是級別和管理的基本元素。 組織可能會有多重區域，而每個區域皆有可用資源。 區域可能也會有不同服務的產品可供使用。 在 Azure Stack 開發套件中，只支援單一區域且會自動命名為「local」。

### <a name="services"></a>服務
Microsoft Azure 堆疊可讓提供者 toodeliver 各種不同的服務和應用程式，例如虛擬機器、 SQL Server 資料庫、 SharePoint、 Exchange、 等等。

### <a name="plans"></a>方案
方案結合一或多項服務。 做為提供者，您建立計劃 toooffer tooyour 租用戶。 接著，您的租用戶訂閱 tooyour 優惠 toouse hello 計劃和它們所包含的服務。

每個服務加入您可以設定 tooa 計劃配額設定 toohelp 與您管理您的雲端容量。 配額可內含限制，像是 VM、RAM 與 CPU 的限制，且會以每位使用者的訂用帳戶為單位加以套用。 配額可能會依位置而有所不同。 例如，包含來自區域 A 的計算服務之方案，可能會有兩部虛擬機器、4 GB RAM 與 10 個 CPU 核心的配額。

Hello 服務系統管理員在建立時提供項目時，可以包含**基本方案**。 當租用戶訂閱 toothat 優惠時，預設會包含這些基底的計劃。 當使用者訂閱 （建立 hello 訂閱），hello 使用者具有存取 tooall hello 資源提供者指定的基底的計劃 （與 hello 對應的配額）。

hello 服務系統管理員也可以包含**附加元件計劃** 的項目。 附加元件計劃不會包含的 hello 訂用帳戶中的預設值。 其他的計劃 （配額） 可用的訂用帳戶擁有者可以加入 tootheir 訂用帳戶 的項目是附加元件計劃。

### <a name="offers"></a>優惠
提供項目是群組的一個或多個計劃存在 tootenants toobuy 該提供者 （訂閱）。 例如，產品 Alpha 可以包含方案 A (包含一組計算服務) 與方案 B (包含一組儲存體與網路服務)。

提供隨附一組基底的計劃和服務系統管理員可以建立租用戶可以加入 tootheir 訂用帳戶的附加元件計劃。

### <a name="subscriptions"></a>訂用帳戶
訂用帳戶是租用戶購買優惠的方式。 訂用帳戶是租用戶與優惠的組合。 租用戶可以訂閱 toomultiple 優惠。 每個訂用帳戶適用於 tooonly 一個供應項目。 租用戶的訂用帳戶會決定他們可以存取哪些方案/服務。

訂用帳戶能協助提供者整理和存取雲端資源與服務。

Hello 系統管理員，在部署期間建立預設提供者訂閱。 此訂用帳戶可以是使用的 toomanage Azure 堆疊、 部署進一步的資源提供者，及建立租用戶計劃和優惠。 它不能使用的 toorun 客戶工作負載和應用程式。 

## <a name="azure-resource-manager"></a>Azure Resource Manager
透過使用 Azure Resource Manager，您能夠以範本為基礎、宣告式模型來使用基礎結構資源。   它提供單一介面，您可以使用 toodeploy 和管理您方案的元件。 完整的資訊和指引，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。

### <a name="resource-groups"></a>資源群組
資源群組是資源、服務與應用程式的集合，而且每個資源各有類型，例如虛擬機器、虛擬網路、公用 IP、儲存體帳戶與網站。 每個資源都必須位於資源群組中，而資源群組有助於整理本機資源，例如依工作負載或位置。  在 Microsoft Azure Stack，像是方案與優惠等資源，也會於資源群組中進行管理。
 
### <a name="azure-resource-manager-templates"></a>Azure 資源管理員範本
利用 Azure Resource Manager，您可以建立可定義應用程式之部署和設定的範本 (以 JSON 格式)。 此範本稱為 Azure 資源管理員範本，並提供宣告式方式 toodefine 部署。 藉由使用範本，您可以重複部署整個 hello 應用程式生命週期的應用程式，並確保一致的狀態以部署您的資源。

## <a name="resource-providers-rps"></a>資源提供者 (RP)
資源提供者是 web 服務形式 hello 基礎所有以 Azure 為基礎的 IaaS 和 paas 整合服務。 Azure 資源管理員都依賴不同 RPs tooprovide 存取 tooservices。

有四個基本的資源提供者：網路、儲存體、計算和 KeyVault。 每個這些資源提供者，皆可協助您設定及控制其各自的資源。 服務管理員也可以加入新的自訂資源提供者。

### <a name="compute-rp"></a>計算 RP
hello 計算資源提供者 (CRP) 可讓 Azure 堆疊租用戶 toocreate 他們自己的虛擬機器。 hello CRP 包括 hello 能力 toocreate 虛擬機器以及虛擬機器擴充功能。 hello 虛擬機器擴充功能服務可協助您針對 Windows 和 Linux 虛擬機器提供 IaaS 功能。  例如，您可以使用 hello CRP tooprovision Linux 虛擬機器，並部署 tooconfigure hello VM 期間執行 Bash 指令碼。

### <a name="network-rp"></a>網路 RP
hello 網路資源提供者 (NRP) 提供一系列的 hello 私人雲端的軟體定義網路功能 (SDN) 和網路函式虛擬化 (NFV) 功能。  您可以使用 hello NRP toocreate 資源，例如軟體負載平衡器、 公用 Ip 時，網路安全性群組，虛擬網路。

### <a name="storage-rp"></a>儲存體 RP
儲存體 RP hello 傳遞四個 Azure 一致的儲存體服務： blob、 資料表、 佇列和帳戶管理。 它也提供儲存體雲端管理服務 toofacilitate 服務提供者管理的 Azure 一致的儲存體服務。 Azure 儲存體提供 hello 彈性 toostore 和擷取大量非結構化資料，例如文件和媒體檔案，使用 Azure Blob，以及結構化的 NoSQL 資料與 Azure 資料表。 如需有關 Azure 儲存體的詳細資訊，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)。

#### <a name="blob-storage"></a>Blob 儲存體
Blob 儲存體可儲存任何檔案集。 Blob 可以是任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 資料表儲存體可儲存結構化的資料集。 資料表儲存體是 NoSQL 索引鍵屬性的資料存放區，可快速開發和快速存取 toolarge 數量的資料。 佇列儲存體針對工作流程處理及雲端服務元件間的通訊，提供可靠的訊息服務。

每個 Blob 會在容器下形成組織。 容器也會提供實用的方式 tooassign 安全性原則 toogroups 的物件。 儲存體帳戶可以包含任何數目的容器，以及容器可以包含任何數目的 blob，向上 toohello 500 TB 容量限制的 hello 儲存體帳戶。 Blob 儲存體提供三種類型的 Blob，包括區塊 Blob、附加 Blob 及分頁 Blob (磁碟)。 區塊 Blob 已針對串流和儲存雲端物件進行最佳化，是儲存文件、媒體檔案、備份等的不錯選擇。附加 blob 類似 tooblock blob，但適合用於附加作業。 附加 blob 可以只是藉由加入新的區塊 toohello 結尾更新。 附加 blob 是不錯的選擇，例如記錄、 需要新的資料寫入只 toohello 結尾 hello blob toobe 案例。 分頁 blob 適用於代表 IaaS 磁碟，支援隨機寫入，以及可能是 up too1 TB。 Azure 虛擬機器網路連結的 IaaS 磁碟是以頁面 Blob 方式儲存的 VHD。

#### <a name="table-storage"></a>表格儲存體
表格儲存體屬於 Microsoft 的 NoSQL 索引鍵/屬性存放區，其設計成沒有結構描述，使其有別於傳統的關聯式資料庫。 因為資料存放區缺少結構描述，所以資料做為 hello 需要的應用程式 evolve 輕鬆 tooadapt。 資料表儲存體是簡單 toouse，因此開發人員可以快速建立應用程式。 表格儲存體屬於索引鍵屬性儲存，代表資料表中的每個值會與具型別的屬性名稱一起儲存。 hello 屬性名稱可以用於篩選和指定選取準則。 一組屬性及其值就構成一個實體。 因為資料表儲存體缺少結構描述中的兩個實體 hello 相同資料表可以包含不同集合的屬性，而這些屬性可以屬於不同的類型。 您可以使用資料表儲存體 toostore 彈性的資料集，例如 web 應用程式、 通訊錄，裝置資訊和任何其他類型的中繼資料服務所需的使用者資料。 您可以將任意數目的實體儲存在資料表中，而且儲存體帳戶包含任何數量的資料表，向上 toohello hello 儲存體帳戶的容量限制。

#### <a name="queue-storage"></a>佇列儲存體
Azure 佇列儲存體可提供應用程式元件之間的雲端傳訊。 設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。 佇列儲存體提供非同步傳訊應用程式元件之間的通訊是否在 hello 雲端中，在 hello 桌面上、 在內部部署伺服器上，或行動裝置上執行。 佇列儲存體也支援管理非同步工作並建置處理工作流程。

### <a name="keyvault"></a>KeyVault
hello KeyVault RP 提供的管理和稽核的機密資料，例如密碼和憑證。 例如，可以使用租用戶 VM 部署期間 hello KeyVault RP tooprovide 系統管理員密碼或金鑰。

## <a name="role-based-access-control-rbac"></a>角色型存取控制 (RBAC)
您可以在訂用帳戶、 資源群組或個別的資源層級角色指派，來使用 RBAC toogrant 系統存取 tooauthorized 使用者、 群組和服務。 每個角色定義使用者、 群組或服務的 Microsoft Azure 堆疊資源高於 hello 存取層級。

Azure RBAC 已套用 tooall 資源類型的三個基本角色： 擁有者、 參與者和讀取器。 擁有者具有完整存取 tooall 資源包括 hello 右 toodelegate 存取 tooothers。 參與者可以建立和管理所有類型的 Azure 資源，但無法授與存取 tooothers。 讀者只能檢視現有的 Azure 資源。 hello RBAC 角色在 Azure 中的 hello rest 允許特定的 Azure 資源管理。 比方說，hello 角色允許建立及管理的虛擬機器，但不該 hello 虛擬機器允許管理 hello 虛擬網路或 hello 子網路的虛擬機器參與者會連接到。

## <a name="usage-data"></a>使用狀況資料
Microsoft Azure 堆疊會收集和彙總使用方式資料跨所有資源提供者，並傳輸它 tooAzure 處理由 Azure 商務。 您可以透過 REST API 檢視 hello 使用量資料收集 Azure 堆疊上。 有跨所有租用戶訂用帳戶是 Azure 一致的租用戶 API，以及提供者和委派的提供者 Api tooget 使用量資料。 此資料可以使用的 toointegrate 與外部工具或收費或計費服務。 一旦已由 Azure 商務處理使用方式，就可以在 hello Azure 計費入口網站中檢視它。

## <a name="in-development-build-of-azure-stack-development-kit"></a>正在開發的 Azure Stack 開發套件組建
在開發組建讓早期採用者評估 hello hello Azure 堆疊開發套件最新版本。 Hello 最新的主要版本為基礎累加建置它們。 主要版本將會繼續 toobe 發行每幾個月、 hello 中開發組建時，將會發行間歇之間主要的 hello 釋放。

在開發組建會提供下列優點的 hello:
- 錯誤修正
- 新功能
- 其他改進功能

## <a name="next-steps"></a>後續步驟
[部署 Azure Stack 開發套件](azure-stack-deploy.md)

