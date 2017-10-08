---
title: "aaaPlanning 在 Azure 中的您 VM 備份基礎結構 |Microsoft 文件"
description: "規劃 tooback 註冊在 Azure 虛擬機器時的重要考量"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份 VM, 備份虛擬機器"
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>在 Azure 中規劃 VM 備份基礎結構
本文章提供效能和資源建議 toohelp 規劃 VM 備份基礎結構。 它也會定義 hello 備份服務的重要層面，含有這些層面可能很重要決定您的架構，容量規劃，和排程。 如果您已經[備妥您的環境](backup-azure-vms-prepare.md)，規劃是 hello 下一個步驟，在您開始前[啟動 Vm tooback](backup-azure-vms.md)。 如果您需要 Azure 虛擬機器的詳細資訊，請參閱 hello[虛擬機器文件](https://azure.microsoft.com/documentation/services/virtual-machines/)。

## <a name="how-does-azure-back-up-virtual-machines"></a>Azure 如何備份虛擬機器？
當 hello Azure 備份服務會啟動備份作業在 hello 排定的時間時，它就會觸發 hello 備用分機號碼 tootake 時間點快照集。 hello Azure 備份服務會使用 hello _VMSnapshot_延伸模組中 Windows 和 hello _VMSnapshotLinux_ Linux 中的擴充功能。 在第一個 VM 備份 hello 安裝 hello 擴充功能。 tooinstall hello 延伸模組，必須執行 hello VM。 如果 hello 未執行 VM，hello Backup service 的快照 hello 基礎儲存體 （因為 VM 已停止的 hello 時，會不發生任何應用程式寫入）。

建立 Windows Vm 快照，hello 備份服務協調一致的快照集的 hello 虛擬機器的磁碟與 hello 磁碟區陰影複製服務 (VSS) tooget。 如果您正在備份 Linux Vm，您可以撰寫您自己的自訂指令碼 tooensure 一致性時取得 VM 快照集。 本文稍後會提供叫用這些指令碼的詳細資料。

一旦 hello Azure 備份服務會擷取 hello 快照，hello 資料就是傳送的 toohello 保存庫。 toomaximize 效率 hello 服務識別，以及傳輸只 hello 的 hello 上一次備份之後變更資料的區塊。

![Azure 虛擬機器備份架構](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Hello 資料傳輸完成時，會移除 hello 快照集，並建立復原點。

> [!NOTE]
> 1. 在 hello 備份過程中，Azure 備份不包含 hello 附加的暫存磁碟 toohello 虛擬機器。 如需詳細資訊，請參閱 hello 部落格上[暫存](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)。
> 2. 因為 Azure Backup 採用儲存層級的快照集和快照集 toovault 的傳輸，請勿變更 hello 儲存體帳戶金鑰，直到 hello 備份工作完成。
> 3. 對於 premium 的 Vm，我們要複製 hello 快照集 toostorage 帳戶。 這是確定 Azure 備份服務取得足夠的 IOPS，傳送資料 toovault toomake。 此儲存體另一份負責根據 hello 已配置大小的 VM。 
>

### <a name="data-consistency"></a>資料一致性
備份和還原業務關鍵資料更為複雜，必須備份企業重要資料產生資料執行中的 hello 的 hello 應用程式時 hello 事實。 tooaddress Windows 和 Linux Vm，Azure Backup 支援應用程式一致備份
#### <a name="windows-vm"></a>Windows VM
Azure 備份會在 Windows VM 上執行 VSS 完整備份 (深入了解 [VSS 完整備份](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx))。 tooenable VSS 複製備份，遵循 hello VM 上的登錄金鑰需求 toobe 集中 hello。

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Linux VM
Azure 備份提供指令碼架構。 tooensure 應用程式一致性 Linux Vm，在備份時建立自訂的前指令碼，以及控制 hello 備份工作流程和環境的後置指令碼。 Azure 備份會 hello 前指令碼叫用之前取得 hello VM 快照集和 hello VM 快照集作業完成之後，會叫用 hello 後指令碼。 如需詳細資訊，請參閱 [Azure Linux VM 的應用程式一致備份 (預覽)](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)。
> [!NOTE]
> Azure 備份只會叫用的客戶所撰寫的 hello 前置和後置指令碼。 如果 hello 前指令碼和後置指令碼執行成功，Azure 備份將標示 hello 復原點為應用程式一致。 不過，hello 客戶而且主要負責 hello 應用程式一致性時使用自訂指令碼。
>


下表說明 hello 它們發生在 Azure VM 的備份和還原程序的一致性與 hello 條件類型。

| 一致性 | 以 VSS 基礎 | 說明和詳細資料 |
| --- | --- | --- |
| 應用程式一致性 |是 - 適用於 Windows|對於工作負載而言，最理想的情況是應用程式一致性，因為它確保：<ol><li> hello VM*開機*。 <li>不會毀損。 <li>不會遺失資料。<li> hello 資料是備份的使用 hello 資料涉及 hello 次-使用 VSS 或備份前/備份後指令碼的 hello 應用程式的一致 toohello 應用程式。</ol> <li>*Windows Vm*-最 Microsoft 工作負載具有執行工作負載的特定動作相關的 toodata 一致性的 VSS 寫入器。 例如，Microsoft SQL Server 具有 VSS 寫入器，以確保正確完成 hello 寫入 toohello 交易記錄檔和 hello 資料庫。 對於 Azure Windows VM 備份，toocreate 應用程式一致復原點，hello 備用分機號碼必須叫用 hello VSS 工作流程，並先完成它再取得 hello VM 快照集。 Hello Azure VM 的快照集 toobe 精確，必須也完成 hello VSS 寫入器的 Azure VM 的所有應用程式。 (深入了解 hello [VSS 的基本概念](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx)深入探討的 hello 詳細資料和[它的運作方式](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx))。 </li> <li> *Linux Vm*位客戶可以執行[自訂前指令碼和後置指令碼 tooensure 應用程式一致性](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)。 </li> |
| 檔案系統一致性 |是 - 適用於 Windows 電腦 |有兩種案例其中 hello 復原點可以是*檔案系統一致*:<ul><li>Azure 中 Linux VM 的備份，沒有前指令碼/後指令碼，或是前指令碼/後指令碼失敗。 <li>在 Azure 中備份 Windows VM 期間發生的 VSS 失敗。</li></ul> 這兩個這種情況，hello 最佳因應是 tooensure 的： <ol><li> hello VM*開機*。 <li>不會毀損。<li>不會遺失資料。</ol> 應用程式需要 tooimplement 自己"v-table 修正"hello 還原資料的機制。 |
| 損毀一致性 |否 |這種情況下都是相等 tooa 遇到 「 當機 」 的虛擬機器 （透過彈性或固定，重設）。 Hello Azure 虛擬機器關機時備份的 hello 時，通常會發生損毀一致性。 當機一致復原點提供 hello 儲存媒體-從的 hello 作業系統或 hello 應用程式的觀點來看 hello hello 資料一致性的 hello 周圍的任何保證。 只有 hello 磁碟已經有 hello 備份時的 hello 資料擷取及備份。 <br/> <br/> 雖然通常不會有任何的保證，hello 作業系統開機時，後面接著檢查磁碟的程序，例如 chkdsk toofix 任何損毀錯誤。 任何記憶體中的資料或有尚未傳送的 toohello 磁碟的寫入都會遺失。 當資料復原需要完成的 toobe hello 應用程式通常遵循與它自己的驗證機制。 <br><br>例如，如果 hello 交易記錄檔具有不存在 hello 資料庫中的項目然後 hello 資料庫軟體會執行回復直到 hello 資料是一致的。 時資料則會分散到多個虛擬磁碟，（例如跨距磁碟區），當機一致復原點會提供任何保證的 hello 正確性的 hello 資料。 |

## <a name="performance-and-resource-utilization"></a>效能與資源使用率
和內部部署的備份軟體一樣，在 Azure 中備份 VM 時也應該規劃容量和資源使用率需求。 hello [Azure 儲存體限制](../azure-subscription-service-limits.md#storage-limits)定義 toostructure VM 部署 tooget 最大效能最少對 toorunning 工作負載的影響。

請特別注意 toohello 規劃備份效能時，會限制下列 Azure 儲存體：

* 每一儲存體帳戶的輸出上限
* 每一儲存體帳戶的總要求率

### <a name="storage-account-limits"></a>儲存體帳戶限制
備份資料複製從儲存體帳戶、 加入 toohello 輸入/輸出作業 (iops) 與輸出 （或輸送量） hello 儲存體帳戶的度量。 在 hello 相同 IOPS 及輸送量，也會耗用時間、 虛擬機器。 hello 目標是 tooensure 備份，且虛擬機器流量不要超過您的儲存體帳戶限制。

### <a name="number-of-disks"></a>磁碟數量
hello 備份程序會盡快嘗試 toocomplete 備份工作。 過程中，它會竭盡所能地取用資源。 不過，所有的 I/O 作業都受到 hello*單一 Blob 的目標輸送量*，其中包含每秒 60 MB 的限制。 在嘗試 toomaximize 速度，hello 備份程序會嘗試在每個 hello VM 磁碟 tooback*平行*。 如果 VM 有四個磁碟，hello 服務會嘗試 tooback 平行中的所有四個磁碟上。 hello**的磁碟數目**進行備份，是決定儲存體帳戶的備份資料傳輸 hello 最重要因素。

### <a name="backup-schedule"></a>備份排程
另一個因素會影響效能是 hello**備份排程**。 如果您設定 hello 原則讓所有 Vm 都備份是在 hello 相同時間，您已排定流量夾紙。 hello 備份程序會嘗試 tooback 平行中的所有磁碟上。 tooreduce hello 備份資料傳輸從儲存體帳戶，在不同時間 hello，無重疊的不同 Vm 備份。

## <a name="capacity-planning"></a>容量規劃
您將 hello 先前因素拼湊在一起，需要 tooplan hello 儲存體帳戶的使用量需求。 下載 hello [VM 備份容量規劃 Excel 試算表](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33)toosee hello 影響您的磁碟和備份排程選項。

### <a name="backup-throughput"></a>備份輸送量
每個磁碟備份，Azure Backup 讀取 hello 磁碟上的 hello 區塊並儲存區僅 hello 變更的資料 （增量備份）。 hello 下表顯示 hello 平均備份服務處理量值。 使用下列資料的 hello，您可以估計 hello 一段時間所需 tooback 設定大小的磁碟。

| 備份作業 | 最佳輸送量 |
| --- | --- |
| 初始備份 |160 Mbps |
| 增量備份 (DR) |640 Mbps  <br><br> 輸送量卸除大幅如果 hello 變更 （需要 toobe 備份） 的資料會散佈在 hello 磁碟。|

## <a name="total-vm-backup-time"></a>VM 備份時間總計
雖然讀取和複製資料，會花費大部分的 hello 備份時間，其他作業提供 toohello 所需的總時間 tooback 將 vm:

* 太所需時間[安裝或更新 hello 備用分機號碼](backup-azure-vms.md)。
* 快照集時間，也就是 hello 所花費時間 tootrigger 快照集。 快照集是觸發排程的關閉 toohello 備份時間。
* 佇列等候時間。 因為 hello 備份服務正在處理來自多個客戶的備份，備份資料複製快照集 toohello 備份或復原服務保存庫可能會立即啟動。 在尖峰負載的時間，hello 等候可以延伸 tooeight 到期的備份正在處理的 toohello 數的時數。 不過，hello VM 備份時間總計會是小於 24 小時內的每日備份原則。
* 資料傳輸時間，備份所需時間服務從先前的備份 toocompute hello 累加式變更和傳輸這些變更 toovault 儲存體。

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>為何我看到的備份時間比較長 (大於 12 小時)？
備份包含兩個階段： 建立快照集，以及傳送 hello 快照 toohello 保存庫。 對儲存體進行最佳化 hello 備份服務。 當傳送嗨快照集資料 tooa 保存庫，hello 服務只將累加變更從 hello 上一個快照。  toodetermine hello 累加變更，hello 服務計算 hello 區塊 hello 總和檢查的碼。 如果變更的區塊，hello 區塊會被視為區塊 toobe 傳送 toohello 保存庫。 然後 hello 服務向下切入進一步到每一個 hello 識別機會 toominimize hello 資料 tootransfer 尋找的區塊。 在評估所有已變更的區塊之後, hello 服務聯合 hello 變更，並將它們傳送 toohello 保存庫。 對部分舊版應用程式來說，小型的分散式寫入並非最適合用於儲存體。 如果 hello 快照集包含許多小型的分散寫入，hello 服務會花更多時間處理 hello hello 應用程式所寫入的資料。 hello 建議 hello VM 內執行的應用程式從 Azure 應用程式寫入區塊是最少為 8 KB。 如果您的應用程式使用小於 8 KB 的區塊，則備份效能會受到影響。 透過調整應用程式 tooimprove 備份效能的說明，請參閱[調整應用程式以獲得最佳效能與 Azure 儲存體](../storage/common/storage-premium-storage-performance.md)。 雖然 hello 備份效能上的發行項使用 Premium 儲存體的範例，但是 hello 指引是適用於標準儲存體磁碟。

## <a name="total-restore-time"></a>總計還原時間
還原作業是由兩個主要子工作所組成： 將資料複製回從 hello 保存庫選擇 toohello 客戶儲存體帳戶，以及建立 hello 虛擬機器。 複製回 hello 保存庫中的資料取決於 hello 備份儲存在內部在 Azure 中，以及 hello 客戶儲存體帳戶的儲存位置。 時間 toocopy 資料而定：
* 佇列會等待時間-因為 hello 服務處理程序從多個客戶在 hello 還原作業相同的時間還原要求會放在佇列中。
* 資料複製時間-從 hello 保存庫 toohello 客戶儲存體帳戶複製資料。 還原時間取決於 IOPS 及輸送量 Azure 備份服務取得 hello 選取客戶儲存體帳戶上。 tooreduce hello 複製 hello 還原程序期間，請選取未使用其他應用程式寫入與讀取載入儲存體帳戶。

## <a name="best-practices"></a>最佳作法
在設定虛擬機器的備份時，建議您遵循下列做法：

* 不要排程超過 10 個傳統的 Vm 從 hello 相同雲端服務 tooback hello 在相同的時間。 如果您想 tooback 啟動相同的雲端服務從多個 Vm，錯開 hello 備份開始時間一小時。
* 不要排程在 hello 向上 40 個以上的 Vm tooback 相同的時間。
* 安排 VM 備份在非尖峰時段進行。 此方式 hello 備份服務會使用 IOPS 從 hello 客戶儲存體帳戶 toohello 保存庫傳輸資料。
* 確定有原則套用至橫跨不同儲存體帳戶的 VM。 我們建議您不能超過 20 來自單一儲存體帳戶的總磁碟受 hello 相同的備份排程。 如果您有大於 20 磁碟儲存體帳戶中，散佈跨多個原則 tooget 這些 Vm 會 hello hello 傳輸程序階段 hello 備份所需的 IOPS。
* 請勿還原 Premium 儲存體 toosame 儲存體帳戶上執行的 VM。 如果 hello 還原作業的程序會伴隨 hello 備份作業，它會減少 hello 可用備份的 IOPS。
* 若要進行進階 VM 備份，請確定裝載進階磁碟的儲存體帳戶至少有 50% 的可用空間可供暫存快照集，以便能順利完成備份。 
* 請確定為了進行備份而在 Linux VM 上啟用的 python 版本為 2.7

## <a name="data-encryption"></a>資料加密
Azure Backup 不會加密資料 hello 備份程序的一部分。 不過，您可以在 hello VM 內的資料加密和備份 hello 受保護的資料緊密 (深入了解[加密資料的備份](backup-azure-vms-encryption.md))。

## <a name="calculating-hello-cost-of-protected-instances"></a>受保護的執行個體的計算 hello 成本
透過 Azure Backup 備份的 azure 虛擬機器也都是主體[Azure 備份定價](https://azure.microsoft.com/pricing/details/backup/)。 hello 受保護的執行個體計算根據 hello*實際*hello 虛擬機器，也就是 hello 總和的 hello 虛擬機器 – 排除 hello 「 資源磁碟 」 中的所有 hello 資料的大小

定價備份 Vm*不*根據 hello 最大支援為每個資料磁碟附加的 toohello 虛擬機器的大小。 定價會根據 hello hello 資料磁碟中所儲存的實際資料。 同樣地，hello 備份儲存體帳單根據 hello 會儲存在 Azure 備份，這是 hello 總和的每個復原點中的 hello 實際資料的資料量。

例如，A2 標準大小的虛擬機器擁有兩個額外資料磁碟，每個大小上限為 1 TB。 hello 下表提供每個這些磁碟上儲存的 hello 實際資料：

| 磁碟類型 | 大小上限 | 實際儲存的資料 |
| --- | --- | --- |
| 作業系統磁碟 |1023 GB |17 GB |
| 本機磁碟/資源磁碟 |135 GB |5 GB (未包含備份) |
| 資料磁碟 1 |1023 GB |30 GB |
| 資料磁碟 2 |1023 GB |0 GB |

hello*實際*hello 虛擬機器的大小，在此情況下為 17 GB + 30 GB + 0 GB = 47 GB。 此受保護執行個體大小 (47 GB) 會變成 hello 基礎 hello 每月帳單。 為 hello hello 虛擬機器中的資料量增加時，據此計費的變更所使用的 hello 受保護執行個體大小。

計費 hello 的第一個成功備份作業完成之前無法啟動。 此時，開始 hello 計費儲存體及受保護的執行個體。 計費仍會繼續，因為沒有*任何備份保存庫中儲存資料*hello 虛擬機器。 如果您停止 hello 的虛擬機器的保護，但有保存庫中的虛擬機器備份資料，計費仍會繼續。

針對指定的虛擬機器停止才停止 hello 保護計費*和*刪除所有備份的資料。 當停止保護並沒有作用中的備份作業、 的 hello 上次成功 VM 備份的 hello 大小變得 hello hello 每月帳單所使用的受保護執行個體大小。

## <a name="questions"></a>有疑問嗎？
如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。

## <a name="next-steps"></a>後續步驟
* [備份虛擬機器](backup-azure-vms.md)
* [管理虛擬機器備份](backup-azure-manage-vms.md)
* [還原虛擬機器](backup-azure-restore-vms.md)
* [疑難排解 VM 備份問題](backup-azure-vms-troubleshoot.md)
