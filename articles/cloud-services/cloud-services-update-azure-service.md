---
title: "aaaHow tooupdate 雲端服務 |Microsoft 文件"
description: "了解 tooupdate 雲端服務在 Azure 中的方式。 了解如何更新雲端服務上的繼續 tooensure 可用性。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>如何 tooupdate 雲端服務

更新雲端服務 (包括其角色和客體 OS) 是一個包含三步驟的程序。 首先，hello 二進位檔和組態檔 hello 新雲端服務，或必須上傳的作業系統版本。 接下來，Azure 會保留運算和網路資源 hello hello hello 新雲端服務版本需求為基礎的雲端服務。 最後，Azure 會執行輪流升級 tooincrementally 更新 hello 租用戶 toohello 新版本或客體作業系統，同時保留您的可用性。 本文討論最後一個步驟-hello 輪流升級的 hello 詳細的資料。

## <a name="update-an-azure-service"></a>更新 Azure 服務
Azure 會將您的角色執行個體組織成名為升級網域 (UD) 的邏輯群組。 升級網域 (UD) 是角色執行個體的邏輯集合，會以群組方式進行更新。  Azure 雲端的更新一次，可讓執行個體中其他處理流量的 Ud toocontinue 服務一個 UD。

升級網域的 hello 預設數目為 5。 您可以指定不同數目的升級網域包括 hello 服務定義檔 (.csdef) 中的 hello upgradeDomainCount 屬性。 如需 hello upgradeDomainCount 屬性的詳細資訊，請參閱[WebRole 結構描述](https://msdn.microsoft.com/library/azure/gg557553.aspx)或[WorkerRole 結構描述](https://msdn.microsoft.com/library/azure/gg557552.aspx)。

當您在您的服務執行的一個或多個角色的就地更新時，Azure 會更新依據 toohello 升級網域 toowhich 所隸屬的角色執行個體的集合。 Azure hello 中所有執行個體指定的升級網域 – 加以停止、 更新，將它們放回線上的更新，然後移到 hello 下一個網域。 透過停止目前的 hello 中執行的唯一 hello 執行個體的升級網域時，Azure 可確保進行更新時 hello 執行服務最低可能影響 toohello。 如需詳細資訊，請參閱[hello 更新，如何繼續](#howanupgradeproceeds)本文稍後。

> [!NOTE]
> 雖然 hello 條款**更新**和**升級**hello 內容 Azure 中有稍微不同的意義，但它們可以交替 hello 程序和本文件中的 hello 功能的描述。
>
>

您的服務必須定義至少兩個該角色更新 toobe 就地而無需停機的角色執行個體。 如果 hello 服務包含一個角色只有一個執行個體，您的服務將無法使用，直到 hello 就地更新已完成。

本主題涵蓋下列 Azure 更新的相關資訊的 hello:

* [在更新期間允許的服務變更](#AllowedChanges)
* [如何繼續進行升級](#howanupgradeproceeds)
* [復原更新](#RollbackofanUpdate)
* [在進行中的部署上起始多項變更作業](#multiplemutatingoperations)
* [將角色散發於升級網域](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>在更新期間允許的服務變更
hello 下表顯示 hello 允許變更 tooa 服務更新期間：

| 允許 toohosting、 服務和角色變更 | 就地更新 | 預備 (VIP 交換) | 刪除並重新部署 |
| --- | --- | --- | --- |
| 作業系統版本 |是 |是 |是 |
| .NET 信任等級 |是 |是 |是 |
| 虛擬機器大小<sup>1</sup> |是<sup>2</sup> |是 |是 |
| 本機儲存體設定 |只會增加<sup>2</sup> |是 |是 |
| 在服務中新增或移除角色 |是 |是 |是 |
| 特定角色的執行個體數目 |是 |是 |是 |
| 服務端點的數目或類型 |是<sup>2</sup> |否 |是 |
| 組態設定的名稱和值 |是 |是 |是 |
| 組態設定的值 (而不是名稱) |是 |是 |是 |
| 加入新憑證 |是 |是 |是 |
| 變更現有的憑證 |是 |是 |是 |
| 部署新程式碼 |是 |是 |是 |

<sup>1</sup>大小變更限制 toohello 子集可用 hello 雲端服務的大小。

<sup>2</sup> 需要 Azure SDK 1.5 或更新版本。

> [!WARNING]
> 變更 hello 虛擬機器大小，將會損毀本機資料。
>
>

更新期間，不支援下列項目 hello:

* 變更 hello 角色的名稱。 移除，然後再加入 hello 與 hello 新名稱的角色。
* 變更 hello 升級網域計數。
* 遞減 hello hello 本機資源大小。

如果您要進行其他更新 tooyour 服務定義，例如減少本機資源大小 hello 必須改為執行 VIP 交換更新。 如需詳細資訊，請參閱 [交換部署](https://msdn.microsoft.com/library/azure/ee460814.aspx)。

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>如何繼續進行升級
您可以決定是否要讓 tooupdate 所有服務中的 hello 角色或 hello 服務中的單一角色。 在任一情況下，每個角色，正在升級而且屬於 toohello 第一個升級網域的所有執行個體是停止、 升級，並回到線上。 它們都回到線上之後，hello hello 第二個升級網域中的執行個體已停止、 升級，而資料庫恢復上線。 雲端服務一次最多可有一個作用中的升級。 hello 升級會自動執行對 hello hello 雲端服務的最新版本。

hello 下列圖表說明如果您要升級所有 hello 服務中的 hello 角色 hello 升級，如何繼續：

![升級服務](media/cloud-services-update-azure-service/IC345879.png "升級服務")

下圖說明如果您要升級單一角色，hello 更新如何繼續：

![升級角色](media/cloud-services-update-azure-service/IC345880.png "升級角色")  

自動更新期間 hello Azure 網狀架構控制器定期評估 hello 雲端服務 toodetermine hello 健全狀況時的安全 toowalk hello UD 下一步。 此健全狀況評估執行每個角色為基礎，並將只執行個體視為 hello 最新版本 （也就是從執行個體已逐步的 Ud） 中。 它會確認每個角色的最少角色執行個體是否已達到令人滿意的終止狀態。

### <a name="role-instance-start-timeout"></a>角色執行個體啟動逾時
hello 網狀架構控制器會等待 30 分鐘每個角色執行個體 tooreach 已啟動 」 狀態的時間。 如果已超過 hello 逾時持續期間，hello 網狀架構控制器會繼續查核 toohello 下一個角色執行個體。

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>在雲端服務升級期間影響 toodrive 資料

從您的服務將會關閉 hello 升級由於 Azure 升級服務 toohello 方法執行期間的單一執行個體 toomultiple 執行個體的服務升級。 hello 服務等級協定保證服務可用性僅適用於與多個執行個體一起部署的 tooservices。 hello 下列清單描述每個 Azure 服務升級案例如何影響每個磁碟機上的 hello 資料：

|案例|C 磁碟機|D 磁碟機|E 磁碟機|
|--------|-------|-------|-------|
|VM 重新啟動|保留|保留|保留|
|入口網站重新啟動|保留|保留|終結|
|入口網站重新安裝映像|保留|終結|終結|
|就地升級|保留|保留|終結|
|節點移轉|終結|終結|終結|

請注意，在清單上方的 hello，hello e： 磁碟機代表 hello 角色的根磁碟機，而不應該是硬式編碼。 請改用 hello **%roleroot%**環境變數 toorepresent hello 磁碟機。

toominimize hello 停機時間時升級單一執行個體服務，部署新多重執行個體服務 toohello 臨時伺服器，並執行 VIP 交換。

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>復原更新
Azure 提供有彈性地管理服務更新期間，讓您之後 hello Azure 網狀架構控制器接受 hello 初始更新要求起始服務的其他作業。 更新 （組態變更） 時，可以只執行回復，或升級處於 hello**正在**hello 部署狀態。 更新或升級，只要至少一個執行個體尚未更新的 toohello 新版 hello 服務被視為 toobe 進行中。 tootest 是否允許回復，檢查 hello hello RollbackAllowed 旗標的值，傳回[取得部署](https://msdn.microsoft.com/library/azure/ee460804.aspx)和[取得雲端服務屬性](https://msdn.microsoft.com/library/azure/ee460806.aspx)作業，會設定 tootrue。

> [!NOTE]
> 它只會在意義上 toocall 復原**就地**更新或升級，因為 VIP 交換升級牽涉到取代另一個整個執行執行個體的服務。
>
>

回復進行中更新具有下列效果 hello 部署的 hello:

* 尚未尚未更新或升級 toohello 新版本的任何角色執行個體不會更新或升級，因為這些執行個體已經在執行 hello 服務 hello 目標版本。
* 任何角色執行個體，其具有已更新或升級的 toohello 新版 hello 服務封裝 (\*.cspkg) 檔案或 hello 服務組態 (\*.cscfg) 檔案 （或這兩個檔案） 是還原的 toohello 升級前版本這些檔案。

此功能是由提供 hello 下列功能：

* hello[回復更新或升級](https://msdn.microsoft.com/library/azure/hh403977.aspx)作業，可針對組態更新 (藉由呼叫觸發[變更部署組態](https://msdn.microsoft.com/library/azure/ee460809.aspx)) 或升級 (藉由呼叫觸發[升級部署](https://msdn.microsoft.com/library/azure/ee460793.aspx))，只要 hello 服務中沒有至少一個執行個體的尚未更新 toohello 新版本。
* hello 鎖定元素和 hello RollbackAllowed 元素，都以 hello 回應 hello 主體的一部分傳回[取得部署](https://msdn.microsoft.com/library/azure/ee460804.aspx)和[取得雲端服務屬性](https://msdn.microsoft.com/library/azure/ee460806.aspx)作業：

  1. hello 鎖定項目可讓您 toodetect 時可以針對給定部署叫用變更作業。
  2. hello RollbackAllowed 元素可讓您 toodetect 時 hello[復原更新或升級](https://msdn.microsoft.com/library/azure/hh403977.aspx)可以針對給定的部署呼叫作業。

  在訂單 tooperform 復原，您沒有 toocheck hello 鎖定和 hello RollbackAllowed 元素。 這樣便已足夠 tooconfirm RollbackAllowed 設定 tootrue。 這些項目才會傳回這些方法會叫用使用 hello 要求標頭設定得 「 x ms 版本： 2011年-10-01"或更新版本。 如需標頭版本控制的詳細資訊，請參閱 [服務管理版本控制](https://msdn.microsoft.com/library/azure/gg592580.aspx)。

有某些情況下，不支援復原更新或升級，如下所示：

* 減少本機資源-如果 hello 更新增加 hello 本機資源角色 hello Azure 平台不允許回復。
* 配額限制-如果 hello 更新已減少作業，您可能不會再有足夠計算配額 toocomplete hello （rollback） 作業。 每個 Azure 訂用帳戶已指定 hello 最大數目可供所有的託管服務屬於 toothat 訂用帳戶核心配額與它相關聯。 如果執行指定之更新的復原會讓您的訂用帳戶超出配額，則不會啟用復原。
* 競爭情形-如果 hello 初始更新已完成，不可能復原。

更新 hello 回復時可能會很有用的範例是，如果您使用 hello[升級部署](https://msdn.microsoft.com/library/azure/ee460793.aspx)作業在手動模式 toocontrol hello 速率的主要就地升級 tooyour Azure 託管服務中推出。

在您呼叫 hello 升級的 hello 首展期間[升級部署](https://msdn.microsoft.com/library/azure/ee460793.aspx)在手動模式中，並開始 toowalk 升級網域。 如果在某個時間點，當您監視 hello 升級，您會注意 hello 第一個升級網域中檢查某些角色執行個體變得沒有回應，您可以呼叫 hello[復原更新或升級](https://msdn.microsoft.com/library/azure/hh403977.aspx)hello 部署作業的會保留不變的 hello 有尚未升級的執行個體，這便是復原執行個體升級 toohello 先前的服務封裝和組態。

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>在進行中的部署上起始多項變更作業
在某些情況下您可能想 tooinitiate 持續進行的部署上的多個同時變更作業。 例如，您可能會執行服務更新，在該更新透過您的服務復原，您想 toomake 某些變更，tooroll 例如 hello 回更新、 套用不同的更新，或甚至刪除 hello 部署。 這可能是必要的情況是如果服務升級包含下列程式碼中造成升級的角色執行個體 toorepeatedly 損毀。 在此情況下，hello Azure 網狀架構控制器不會在套用升級，因為 hello 升級網域中執行個體數目不足的狀況良好的能 toomake 進度。 此狀態是參照的 tooas*停滯部署*。 您可助您脫離停滯 hello 部署回復 hello update 或透過頂端的其中一個失敗的 hello 套用新的更新。

一旦 hello 初始要求 tooupdate 或升級 hello 服務已收到 hello Azure 網狀架構控制器，就可以開始後續變更作業。 也就是您沒有針對 hello 初始作業 toocomplete toowait 才能開始另一個變更作業。

Hello 第一次更新正在進行中時，起始第二個更新作業將會執行類似 toohello 復原作業。 如果 hello 第二個更新，以自動模式 hello 的第一個升級網域將會立即升級，這樣可能會導致 tooinstances 多個升級網域已在 hello 離線相同時間點。

hello 變更作業如下：[變更部署組態](https://msdn.microsoft.com/library/azure/ee460809.aspx)，[升級部署](https://msdn.microsoft.com/library/azure/ee460793.aspx)，[更新部署狀態](https://msdn.microsoft.com/library/azure/ee460808.aspx)，[刪除部署](https://msdn.microsoft.com/library/azure/ee460815.aspx)，和[回復更新或升級](https://msdn.microsoft.com/library/azure/hh403977.aspx)。

兩個作業，[取得部署](https://msdn.microsoft.com/library/azure/ee460804.aspx)和[取得雲端服務屬性](https://msdn.microsoft.com/library/azure/ee460806.aspx)，傳回是否可以針對給定部署叫用變更作業可以是檢查的 toodetermine hello 鎖定旗標。

順序 toocall hello 版本的這些方法會傳回 hello 鎖定旗標，您必須設定要求標頭太"x ms 版本： 2011年-10-01"或更新的版本。 如需標頭版本控制的詳細資訊，請參閱 [服務管理版本控制](https://msdn.microsoft.com/library/azure/gg592580.aspx)。

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>將角色散發於升級網域
Azure 平均將角色執行個體分散到固定數目的升級網域，可以設定為 hello 服務定義 (.csdef) 檔案的一部分。 hello 升級網域數目上限為 20，hello 預設值為 5。 如需有關如何 toomodify hello 服務定義檔的詳細資訊，請參閱[Azure 服務定義結構描述 (.csdef 檔)](cloud-services-model-and-package.md#csdef)。

例如，如果您的角色有 10 個執行個體，依預設每個升級網域包含 2 個執行個體。 如果您的角色有 14 個執行個體，則四個 hello 升級網域包含三個執行個體，和第五個網域包含兩個。

升級網域會使用以零為起始的索引加以識別： hello 的第一個升級網域的 ID 為 0，個 hello 第二個升級網域的識別碼為 1，依此類推。

hello 下列圖表說明 hello 服務定義兩個升級網域時，如何散發包含兩個角色服務。 hello 服務正在執行的 hello web 角色的八個執行個體並 hello 背景工作角色的九個執行個體。

![升級網域的分配](media/cloud-services-update-azure-service/IC345533.png "升級網域的分配")

> [!NOTE]
> 請注意，Azure 會控制執行個體配置於升級網域的方式。 不可能 toospecify 哪一個執行個體配置 toowhich 網域。
>
>

## <a name="next-steps"></a>後續步驟
[如何 tooManage 雲端服務](cloud-services-how-to-manage.md)  
[如何 tooMonitor 雲端服務](cloud-services-how-to-monitor.md)  
[如何 tooConfigure 雲端服務](cloud-services-how-to-configure.md)  
