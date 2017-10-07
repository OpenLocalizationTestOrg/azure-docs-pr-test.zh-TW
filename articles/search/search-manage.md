---
title: "Azure 搜尋中 hello Azure 入口網站的 aaaService 管理"
description: "管理 Azure 搜尋中，使用 hello Azure 入口網站的 Microsoft Azure 上託管的雲端搜尋服務。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Azure 搜尋 hello Azure 入口網站中的服務管理
> [!div class="op_single_selector"]
> * [入口網站](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python (英文)](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Azure 搜尋服務是完全受管理、以雲端為基礎的搜尋服務，用來在自訂應用程式內建置豐富的搜尋經驗。 本文章涵蓋 hello*服務管理*工作，您可以在 hello 執行[Azure 入口網站](https://portal.azure.com)您已經佈建搜尋服務。 *服務管理*是根據設計，下列工作的有限 toohello 輕量：

* 管理及保護存取 toohello *api 金鑰*用於讀取或寫入存取 tooyour 服務。
* 變更 hello 配置的資料分割和複本，以調整服務的容量。
* 監視資源使用量，您的服務層的相對 toomaximum 限制。

**不在範圍中** 

*內容管理*（或索引管理） 是指 toooperations 分析搜尋流量 toounderstand 查詢磁碟區，例如探索的詞彙搜尋，以及如何成功的搜尋結果是以引導客戶 toospecific 的人員您的索引中的文件。 如需此區域的說明，請參閱 [Azure 搜尋服務的搜尋流量分析](search-traffic-analytics.md)。

*查詢效能*也已超出本文 hello 範圍。 如需詳細資訊，請參閱[監視使用量和查詢度量](search-monitor-usage.md)和[效能和最佳化](search-performance-optimization.md)。

「升級」不是管理工作。 佈建 hello 服務時，會配置資源，因為移動的 tooa 不同的階層會需要新的服務。 如需詳細資料，請參閱[建立 Azure 搜尋服務](search-create-service-portal.md)。

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>系統管理員權限
佈建或解除委任 hello 服務本身即可做到的 Azure 訂用帳戶系統管理員或共同管理員。

在服務內，任何人存取 toohello 服務 url 和管理 api 金鑰都有讀寫存取 toohello 服務。 讀寫存取提供 hello 能力 tooadd、 刪除或修改伺服器物件，包括應用程式開發介面索引鍵、 索引、 索引子、 資料來源、 排程和角色指派，如透過實作[RBAC 定義角色](#rbac)。

使用 Azure 搜尋的所有使用者互動都置於其中一個模式： 讀寫存取 toohello 服務 （系統管理員權限） 或唯讀存取 toohello 服務 （查詢權限）。 如需詳細資訊，請參閱[管理 hello api 金鑰](#manage-keys)。

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>設定系統管理存取權的 RBAC 角色
Azure 提供[全域以角色為基礎的授權模型](../active-directory/role-based-access-control-configure.md)透過 hello 入口網站或資源管理員 Api 管理的所有服務。 擁有者、 參與者和讀取器角色判斷服務管理的 Active Directory 使用者、 群組和安全性主體指派的 tooeach 角色 hello 層級。 

Azure 搜尋 RBAC 權限會決定下列系統管理工作的 hello:

| 角色 | 工作 |
| --- | --- |
| 擁有者 |建立或刪除 hello 服務或 hello 服務，包括 api 金鑰、 索引、 索引子、 索引子資料來源，以及索引子排程上的任何物件。<p>檢視服務狀態，包括計數和儲存體大小。<p>新增或刪除角色成員資格 (只有「擁有者」可以管理角色成員資格)。<p>訂用帳戶管理員和服務擁有者具有自動成員資格 hello 擁有者角色中。 |
| 參與者 |與「擁有者」相同層級的存取權，減去 RBAC 角色管理。 例如，參與者可以檢視和重新產生 `api-key`，但不能修改角色成員資格。 |
| 讀取者 |檢視服務狀態及查詢金鑰。 這個角色的成員無法變更服務組態，也無法檢視管理金鑰。 |

角色不會授與存取權限 toohello 服務端點。 搜尋服務作業 (例如索引管理、索引母體擴展，以及搜尋資料查詢) 可透過 api-key 而非角色來控制。 如需詳細資訊，請參閱[什麼是角色存取控制](../active-directory/role-based-access-control-what-is.md)中的「管理授權與資料作業」。

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>記錄與系統資訊
Azure 搜尋不會公開透過 hello 入口網站或程式設計介面的個別服務的記錄檔。 Hello 基本層和更新版本中，Microsoft 會監視所有的 Azure 搜尋服務的每個服務等級協定 (SLA) 的 99.9%可用性。 如果 hello 服務很慢，或要求輸送量低於 SLA 臨界值，支援小組會檢閱 hello 記錄檔可用 toothem 和地址 hello 問題。

根據您的服務的一般資訊，您可以取得 hello 下列方式中的資訊：

* 在 hello 入口網站，hello 服務儀表板上，透過通知、 屬性和狀態訊息。
* 使用[PowerShell](search-manage-powershell.md)或 hello[管理 REST API](https://docs.microsoft.com/rest/api/searchmanagement/)太[取得服務屬性](https://docs.microsoft.com/rest/api/searchmanagement/services)，或在索引資源使用狀況的狀態。
* 如先前所述，透過[搜尋流量分析](search-traffic-analytics.md)。

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>管理 API 金鑰
Tooa 搜尋服務需要特別為您的服務所產生的 api 金鑰的所有要求。 此 api 金鑰是 hello 驗證存取 tooyour 搜尋服務端點的唯一機制。 

API 金鑰是由隨機產生的數字和字母所組成的字串。 透過[RBAC 權限](#rbac)，您可以刪除或讀取 hello 機碼，但您無法以使用者定義的密碼取代金鑰。 

兩種類型的索引鍵是使用的 tooaccess 搜尋服務：

* 系統管理員 （適用於 hello 服務的任何讀取寫入作業）
* 查詢 (適用於唯讀作業，例如針對索引的查詢)

佈建 hello 服務時，會建立系統管理 api 金鑰。 有兩個的系統管理金鑰指定為*主要*和*次要*tookeep 它們直接，但事實上它們是可互換的。 每個服務有兩個系統管理金鑰，因此您可以換一而不會遺失存取 tooyour 服務。 您可以重新產生任一管理金鑰，但您無法加入 toohello 總管理索引鍵計數。 每個搜尋服務最多有 2 個管理員金鑰。

查詢金鑰是專為直接呼叫搜尋的用戶端應用程式所設計。 您可以建立 too50 查詢索引鍵。 在應用程式碼中，您可以指定 hello 搜尋 URL 和查詢 api 金鑰 tooallow 唯讀存取 toohello 服務。 應用程式程式碼也會指定應用程式所使用的 hello 索引。 在一起，hello 端點，api 金鑰的唯讀存取和目標索引定義用戶端應用程式中的 hello 連接 hello 領域和存取層的級。

tooget 或重新產生 api 金鑰，開啟 hello 服務儀表板。 按一下**金鑰**tooslide 開啟 hello 金鑰管理頁面。 重新產生或建立機碼的命令是在 hello hello 頁面最上方。 依預設，只會建立管理員金鑰。 查詢 API 金鑰必須以手動方式建立。

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>保護 API 金鑰
藉由限制存取透過 hello 入口網站或資源管理員介面 （PowerShell 或命令列介面），會確保重要的安全性。 如前所述，訂用帳戶系統管理員可以檢視及重新產生所有的 API 金鑰。 做為預防起見，檢視角色指派 toounderstand 擁有存取 toohello 系統管理金鑰。

1. 在 hello 服務儀表板 hello 存取圖示 tooslide 開啟 hello 使用者刀鋒視窗。
   ![][7]
2. 在 [使用者] 中，檢閱現有的角色指派。 如預期般，訂用帳戶系統管理員已透過 hello 擁有者角色的完整存取 toohello 服務。
3. 此外，toodrill 按一下**訂用帳戶系統管理員 」**然後展開 hello 角色指派清單 toosee 上搜尋服務具有共同的系統管理權限。

另一個方式 tooview 存取權限是 tooclick**角色**hello 使用者 刀鋒視窗上。 這麼做會顯示可用的角色和使用者或群組指派的 tooeach 角色的 hello 數目。

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>監視資源使用量
在 hello 儀表板，資源監視是有限的 toohello hello 服務儀表板，您可以透過查詢 hello 服務取得的幾個度量所示的資訊。 Hello 服務儀表板上，在 hello 使用量區段中，您可以快速判斷是否適合您的應用程式磁碟分割資源層級。

您可以使用 hello 搜尋服務 API，來取得文件和索引上的資料計數。 有這些 hello 定價層為依據的計數相關聯的固定限制。 如需詳細資訊，請參閱[搜尋服務限制](search-limits-quotas-capacity.md)。 

* [取得索引統計資料](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [文件計數](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> 快取行為可暫時放寬限制。 例如，使用共用的 hello 服務時，您可能會看到文件計數超過 hello 10000 的文件的硬限制。 hello overstatement 是暫時的系統會偵測到下一步限制強制檢查 hello 上。 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>災害復原和服務中斷

雖然我們可以先搶救資料，Azure 搜尋不提供立即的容錯移轉的 hello 服務層級 hello 叢集或資料中心中斷時。 如果在 hello 資料中心失敗的叢集，hello 作業小組會偵測並工作 toorestore 服務。 您會在服務還原期間經歷停機。 您可以要求每個 hello 服務無法使用的服務參與名單 toocompensate[服務等級協定 (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。 

如果持續服務需要的重大錯誤，Microsoft 的控制之外的 hello 事件中，您可以[佈建其他服務以](search-create-service-portal.md)以不同的地區和實作地理複寫策略 tooensure 索引是完全重複的所有服務。

使用客戶[索引子](search-indexer-overview.md)toopopulate 和重新整理的索引，可以處理透過運用 hello 地理特定索引子的災害復原相同的資料來源。 在不同區域中，每個執行索引子的兩個服務無法索引 hello 從相同資料來源 tooachieve 異地備援。 如果從同為異地備援的資料來源建立索引，請留意，Azure 搜尋服務索引子只能在主要複本執行遞增索引。 在容錯移轉事件中，必須確定 toore 點 hello 索引子 toohello 新主要複本。 

如果您不使用索引子，您會以平行方式來使用應用程式程式碼 toopush 物件和資料 toodifferent 搜尋服務。 如需詳細資訊，請參閱 [Azure 搜尋服務中的效能和最佳化](search-performance-optimization.md)。

## <a name="backup-and-restore"></a>備份與還原

因為 Azure 搜尋服務不是主要的資料儲存體解決方案，所以我們不提供自助備份及還原的正式機制。 您的應用程式程式碼，用來建立及填入索引是 hello 既定的還原選項，如果您不小心刪除索引。 

toorebuild 索引，您會刪除它 （假設存在的話）、 重新建立 hello 服務中的 hello 索引並重新載入從您的主要資料存放區中擷取資料。 或者，您可能會達到太[客戶支援]()toosalvage 編製索引，如果沒有地區中斷。


<a id="scale"></a>

## <a name="scale-up-or-down"></a>擴大或縮小規模
每個搜尋服務都會以一個複本和一個資料分割的最小值開始執行。 如果您註冊[層提供專用的資源](search-limits-quotas-capacity.md)，按一下 hello**標尺**hello 服務儀表板 tooadjust 資源使用量磚。

當您將透過資源的容量時，hello 服務它們會自動使用。 組件上不需要任何進一步的動作，但 hello hello 新資源的影響，才能實現之前，會稍微延遲。 可能需要 15 分鐘或更多 tooprovision 其他資源。

 ![][10]

### <a name="add-replicas"></a>新增複本
系統會藉由新增複本來增加每秒查詢 (QPS) 數量或達到高可用性。 每個複本有一份索引，因此會加入一個詳細複本轉譯 tooone 多個索引，做為處理服務查詢要求。 高可用性至少需要 3 個複本 (如需詳細資訊，請參閱[容量規劃](search-capacity-planning.md) )。

有許多複本的搜尋服務可透過大量索引來達到查詢要求的負載平衡。 獲得查詢磁碟區的層級，查詢輸送量即將 toobe 更快更多份 hello 索引可用 tooservice hello 要求時。 如果您遇到查詢延遲，您可以預期正面的影響效能一旦 hello 其他複本都在線上。

雖然查詢輸送量提高當您新增複本，它就不會不精確按兩下，或三倍，當您新增複本 tooyour 服務。 所有的搜尋應用程式都可以 impinge 對查詢效能的主旨 tooexternal 因素。 複雜的查詢與網路延遲是兩個因素構成 toovariations 查詢回應時間。

### <a name="add-partitions"></a>新增資料分割
大部分的服務應用程式內建需要多個複本，而非資料分割。 如果您註冊的是標準服務，對於需要新增文件計數的案例，可以新增資料分割。 基本層沒有提供額外的資料分割。

在 hello 標準層，分割區區加入的 12 倍 (具體而言，1、 2、 3、 4、 6 或 12)。 這是分區化的構件。 索引會建立在 12 個分區中，並且可以全部儲存在 1 個資料分割中，或平均分配在 2、3、4、6 或 12 個資料分割中 (每個資料分割分配一個分區)。

### <a name="remove-replicas"></a>移除複本
高查詢量期間過後，在搜尋的查詢負載量回到標準時 (例如，假日銷售結束後)，您可以減少複本。

toodo 這個，移動 hello 複本滑桿後 tooa 較低數字。 無須再執行其他步驟。 降低 hello 複本計數讓出 hello 資料中心中的虛擬機器。 相較於先前的情況，現在會在較少的 VM 上執行您的查詢和資料擷取作業。 hello 最小限制為一個複本。

### <a name="remove-partitions"></a>移除資料分割
相較於移除複本，這需要您採取任何額外心力，您可能不需要某些工作 toodo，如果您使用更多儲存空間，比可以降低。 例如，如果您的解決方案使用三個資料分割，裁員 tooone 或兩個資料分割，將會產生錯誤如果 hello 新儲存空間是早於所需。 如您所料，您的選擇 toodelete 索引或文件內的關聯的索引 toofree 佔用空間，或保留 hello 的目前設定。

沒有任何偵測方法可告訴您哪個索引分區儲存在哪個特定資料分割中。 每個資料分割提供大約 25 GB 的儲存體，因此您需要 tooreduce 儲存體 tooa 大小可以容納由您所擁有的分割 hello 數。 如果您想 toorevert tooone 資料分割時，所有的 12 個分區必須 toofit。

toohelp 與未來的規劃，您可能會想 toocheck 儲存體 (使用[取得索引統計資料](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee 多少您實際使用。 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>調整和部署的最佳作法
在這段 30 分鐘的影片中，會檢閱進階部署案例的最佳作法，包括地理位置分散工作負載。 您也可以查看[效能和最佳化 Azure 搜尋中的](search-performance-optimization.md)相同點之說明頁面的封面 hello。

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>後續步驟
一旦您了解 hello 服務管理的概念，請考慮使用[PowerShell](search-manage-powershell.md) tooautomate 工作。

我們也建議您檢閱 hello[效能與最佳化的發行項](search-performance-optimization.md)。

另一個建議是 toowatch hello 視訊 hello 上一節所述。 它提供更深入的涵蓋範圍的這一節所述的 hello 技術。

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



