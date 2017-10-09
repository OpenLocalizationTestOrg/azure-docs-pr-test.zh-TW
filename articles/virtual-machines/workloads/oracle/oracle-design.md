---
title: "在 Azure 上資料庫 aaaDesign 和實作 Oracle |Microsoft 文件"
description: "在 Azure 環境中設計和實作 Oracle 資料庫。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>在 Azure 中設計和實作 Oracle 資料庫

## <a name="assumptions"></a>假設

- 您計劃 toomigrate 內部 tooAzure 從 Oracle 資料庫。
- 您了解的 hello 各種標準 Oracle AWR 報表中。
- 您已基本了解應用程式效能和平台使用量。

## <a name="goals"></a>目標

- 了解如何 toooptimize Oracle 部署在 Azure 中的。
- 探索 Azure 環境中 Oracle 資料庫的效能調整選項。

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>hello 內部之間的差異和 Azure 的實作 

以下是一些重要事情 tookeep 記住，當您移轉內部部署應用程式 tooAzure。 

其中的一項重要差異是，Azure 實作中的資源 (例如 VM、磁碟和虛擬網路) 會與其他用戶端共用。 此外，資源可以進行節流處理 hello 需求為基礎。 而不是將焦點放在避免發生失敗 (MTBF)，Azure 更專注於存活 hello 失敗 (MTTR)。

hello 下表列出一些在內部部署實作和 Azure 的 Oracle 資料庫實作的 hello 差異。

> 
> |  | **內部部署實作** | **Azure 實作** |
> | --- | --- | --- |
> | **網路功能** |LAN/WAN  |SDN (軟體定義網路)|
> | **安全性群組** |IP/連接埠限制工具 |[網路安全性群組 (NSG)](https://azure.microsoft.com/blog/network-security-groups) |
> | **恢復功能** |MTBF (平均失敗時間) |MTTR (時間 toorecovery)|
> | **預定的維修** |修補/升級|[可用性設定組](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (Azure 所管理的修補/升級) |
> | **Resource** |專用  |與其他用戶端共用|
> | **區域** |資料中心 |[區域配對](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **儲存體** |SAN/實體磁碟 |[Azure 受管理儲存體](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **調整** |垂直調整 |水平調整|


### <a name="requirements"></a>需求

- 決定 hello 資料庫大小和成長率。
- 判斷 hello IOPS 需求，您可以根據 Oracle AWR 報表或其他網路監視工具來估計。

## <a name="configuration-options"></a>組態選項

有四個可能的區域，您可以微調 tooimprove Azure 環境中的效能：

- 虛擬機器大小
- 網路輸送量
- 磁碟類型和設定
- 磁碟快取設定

### <a name="generate-an-awr-report"></a>產生 AWR 報表

如果您有現有的 Oracle 資料庫，並計劃 toomigrate tooAzure，您會有數個選項。 您可以執行 hello Oracle AWR 報表 tooget hello 度量 （IOPS、 Mbps、 GiBs，等等）。 然後選擇 的 hello VM 會根據您所收集的 hello 度量。 或連絡您基礎結構小組 tooget 類似的資訊。

您可以考慮在一般和尖峰工作負載期間執行 AWR 報表，以進行比較。 根據這些報表，您可以調整大小的 Vm 依據 hello 平均工作負載或 hello 最大工作負載的 hello。

以下是如何的範例 toogenerate AWR 報表：

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>重要計量

以下是您可以從 hello AWR 報表取得的 hello 度量：

- 核心總數
- CPU 時脈速度
- 記憶體總計 (GB)
- CPU 使用率
- 尖峰資料傳送速率
- I/O 變更率 (讀/寫)
- 重做記錄速率 (MBPs)
- 網路輸送量
- 網路延遲速率 (低/高)
- 資料庫大小 (GB)
- 位元組收到透過 SQL * Net 從 / tooclient

### <a name="virtual-machine-size"></a>虛擬機器大小

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1.估計的 VM 大小根據 CPU、 記憶體和 I/O 使用方式，從 hello AWR 報表

您可能會看到一件事是 hello 前五個定時的前景事件，以指出 hello 系統瓶頸的所在。

比方說，在下列圖表 hello，hello 記錄檔案同步處理是在 hello 最上方。 它會指出等候之前 hello LGWR 寫入 hello 記錄緩衝區 toohello 重做記錄檔所需的 hello 數目。 這些結果代表您需要效能更好的儲存體或磁碟。 此外，hello 圖表也會顯示 hello CPU （核心） 的數目和記憶體的 hello 數量。

![Hello AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/cpu_memory_info.png)

hello 下列圖表顯示 hello 總 I/O 的讀取和寫入。 沒有 59 GB，讀取和寫入 hello hello 報表階段期間的 247.3 GB。

![Hello AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2.選擇 VM

根據您從 hello AWR 報表收集到的 hello 資訊，hello 下一個步驟是大小的 toochoose 類似符合您需求的 VM。 您可以在 hello 文件中找到可用 Vm 的清單[記憶體最佳化](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory)。

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3.使用類似的 VM 系列，根據 hello ACU 微調 hello VM 大小

您選擇 hello VM 之後，請特別注意 toohello ACU hello VM。 您可以選擇不同的 VM 依據 hello ACU 值更符合您的需求。 如需詳細資訊，請參閱 [Azure 計算單位](https://docs.microsoft.com/azure/virtual-machines/windows/acu)。

![Hello ACU 單位頁面的螢幕擷取畫面](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>網路輸送量

下列圖表顯示 hello 關聯性之間的輸送量和 IOPS 的 hello:

![輸送量的螢幕擷取畫面](./media/oracle-design/throughput.png)

hello 整體網路輸送量估計根據 hello 下列資訊：
- SQL*Net 流量
- MBps x 伺服器數目 (輸出串流，例如 Oracle Data Guard)
- 其他因素，例如應用程式複寫

![螢幕擷取畫面的 hello SQL * Net 輸送量](./media/oracle-design/sqlnet_info.png)

根據您的網路頻寬需求，有各種 toochoose 從閘道類型。 這些類型包括基本、VpnGw 和 Azure ExpressRoute。 如需詳細資訊，請參閱 hello [VPN 閘道定價頁面](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h)。

**建議**

- 網路延遲為更高版本的比較的 tooan 內部部署。 減少網路來回行程可以大幅改善效能。
- tooreduce 往返，彙總 hello 有高交易或 「 多對話 」 應用程式的應用程式相同的虛擬機器。

### <a name="disk-types-and-configurations"></a>磁碟類型和設定

- 預設的 OS 磁碟：這些磁碟類型可提供持續性資料和快取。 它們最適合用在啟動時的 OS 存取，但其設計目的並非用於交易式或資料倉儲 (分析) 工作負載。

- *Unmanaged 磁碟*： 您可以使用 [磁碟] 類型，這些管理 hello 儲存 hello 對應 tooyour VM 磁碟的虛擬硬碟 (VHD) 檔案的儲存體帳戶。 VHD 檔案會以分頁 Blob 的形式儲存在 Azure 儲存體帳戶中。

- *管理磁碟*: Azure 管理您使用的 VM 磁碟的 hello 儲存體帳戶。 指定 hello 磁碟類型 （高階或標準） 以及您需要的 hello 磁碟 hello 大小。 Azure 會建立，並會為您管理 hello 磁碟。

- 進階儲存體磁碟：這些磁碟類型最適合生產工作負載使用。 Premium 儲存體支援的 VM 磁碟可以是附加 toospecific 大小系列 Vm，例如 DS、 DSv2、 GS 和 F 系列 Vm。 hello premium 磁碟隨附不同的大小，而且您可以選擇介於 32 GB too4，096 GB 的磁碟。 每個磁碟大小都有自己的效能規格。 根據您的應用程式需求，您可以附加一或多個磁碟 tooyour VM。

當您從 hello 入口網站建立新的受管理的磁碟時，您可以選擇 hello**帳戶類型**想 toouse hello 類型的磁碟。 請記住，並非所有可用的磁碟所示 hello 下拉式選單。 您選擇特定的 VM 大小之後，hello 功能表會顯示 hello 可用的 premium 儲存體為基礎的 VM 大小的 Sku。

![Hello 受管理的磁碟 頁面的螢幕擷取畫面](./media/oracle-design/premium_disk01.png)

如需詳細資訊，請參閱 [VM 高效能進階儲存體與受控磁碟](https://docs.microsoft.com/azure/storage/storage-premium-storage)。

在 VM 上設定您的儲存體之後，您可能想 tooload 測試 hello 磁碟之前建立資料庫。 了解 hello 延遲和輸送量方面的 I/O 速率可協助您判斷如果 hello Vm 支援 hello 預期輸送量，而延遲的目標。

有數種工具可以進行應用程式負載測試，例如 Oracle Orion、Sysbench 和 Fio。

在部署 Oracle 資料庫之後，再次執行 hello 負載測試。 啟動您的規則和尖峰工作負載，而且 hello 結果顯示 hello 環境的基準。

它可能會更重要的 hello IOPS 速率，而不是 hello 儲存體大小為基礎的 toosize hello 存放裝置。 例如，如果 hello 需要 IOPS 為 5000，但是您只需要 200 GB，可能仍可使用 hello P30 類別高階磁碟即使這樣有 200 GB 以上的儲存體。

hello IOPS 速率可以取自 hello AWR 報表。 而是由決定 hello 重做記錄檔、 實體的讀取和寫入的速率。

![Hello AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/awr_report.png)

例如，hello 重做大小為 12,200,000 位元組 / 秒，也就是等於 too11.63 MBPs。
hello IOPS 是 12200000 / 2,358 = 5,174。

清楚地了解的 hello I/O 需求之後，您可以選擇最適合的 toomeet 的磁碟機的組合這些需求。

**建議**

- 針對資料的資料表空間分散 hello I/O 工作負載的磁碟數目使用受管理存放裝置或 Oracle ASM。
- 隨著 hello I/O 區塊大小增加為大量讀取和寫入密集作業，加入更多的資料磁碟。
- 提高大型循序處理程序的 hello 區塊大小。
- 使用資料壓縮 tooreduce I/O （針對資料和索引）。
- 區隔不同資料磁碟上的重做記錄、系統、暫時和重做 TS。
- 不要將任何應用程式檔案放在預設 OS 磁碟 (/dev/sda)。 這些磁碟不適合用於快速 VM 啟動階段，因此可能不會為您的應用程式提供良好的效能。

### <a name="disk-cache-settings"></a>磁碟快取設定

有三個主機快取選項：

- 唯讀：快取所有要求，以供未來讀取。 會保存所有寫入直接 tooAzure Blob 儲存體。

- 讀寫：這是「預先讀取」演算法。 hello 讀取和寫入快取供後續的讀取。 非直接寫入式寫入為先保存 toohello 本機快取。 For SQL Server 寫入為保存的 tooAzure 儲存體，因為它會貫穿式寫入使用。 它也會提供輕的工作負載的最低磁碟延遲 hello。

- *無*（停用）： 使用此選項，您可以略過 hello 快取。 所有 hello 傳送的 toodisk 及資料保存 tooAzure 儲存體。 這個方法提供下列 hello I/O 密集型工作負載的最高的 I/O 速率。 您也需要 tootake 」 交易成本 」 納入考量。

**建議**

toomaximize hello 輸送量，建議您開始使用**無**主機快取。 Premium 儲存體，請記住，您必須停用 hello 「 屏障 」 時掛接 hello 檔案系統與 hello **ReadOnly**或**無**選項。 更新 hello /etc/fstab hello UUID toohello 磁碟檔案。

如需詳細資訊，請參閱[適用於 Linux VM 的進階儲存體](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms)。

![Hello 受管理的磁碟 頁面的螢幕擷取畫面](./media/oracle-design/premium_disk02.png)

- 針對 OS 磁碟，使用預設的 [讀取/寫入] 快取。
- 針對 SYSTEM、TEMP 和 UNDO，對快取功能使用 [無]。
- 針對 DATA，對快取功能使用 [無]。 但是，如果您的資料庫是唯讀或讀取密集，請使用 [唯讀] 快取。

儲存您的資料磁碟的設定之後，您就無法變更 hello 主機快取設定，除非您卸載在 hello 作業系統層級的 hello 磁碟機，並再重新掛接它之後所做變更的 hello。


## <a name="security"></a>安全性

您已安裝並設定 Azure 環境後，hello 下一個步驟是 toosecure 您的網路。 以下是一些建議：

- NSG 原則：可以透過子網路或 NIC 來定義 NSG。 在 hello 子網路層級安全性和強制的路由項目 （例如防火牆） 應用程式的較簡單 toocontrol 存取它。

- *Jumpbox*： 更安全的存取，系統管理員不應直接連接 toohello 應用程式服務或資料庫。 Jumpbox 做為 hello 管理員機器之間的 Azure 資源的媒體。
![Hello Jumpbox 拓樸 頁面的螢幕擷取畫面](./media/oracle-design/jumpbox.png)

    hello 管理員電腦應該提供 IP 限制存取 toohello jumpbox 只。 hello jumpbox 應有存取 toohello 應用程式和資料庫。

- *私人網路*（子網路）： 我們建議，您擁有 hello 應用程式服務和資料庫上不同的子網路，因此 NSG 原則可以設定更好的控制。


## <a name="additional-reading"></a>其他閱讀資料

- [設定 Oracle ASM](configure-oracle-asm.md)
- [設定 Oracle Data Guard](configure-oracle-dataguard.md)
- [設定 Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Oracle 備份和復原](oracle-backup-recovery.md)

## <a name="next-steps"></a>後續步驟

- [教學課程︰建立高可用性 VM](../../linux/create-cli-complete.md)
- [瀏覽 VM 部署 Azure CLI 範例](../../linux/cli-samples.md)
