## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>了解 VM 重新開機 - 維護與停機時間
有三種情況，可能導致 toovirtual 機器發生在 Azure 中受到影響： 未規劃的硬體維護、 未預期的停機時間和規劃的維護。

* **未規劃的硬體維護事件**發生於 hello Azure 平台來預測該 hello 硬體或任何平台元件相關聯的 tooa 實體電腦，是關於 toofail。 Hello 平台預測失敗，它就會發出非計劃的硬體維護事件 tooreduce hello 影響 toohello 上裝載虛擬機器的硬體。 Azure 會使用即時移轉技術 toomigrate hello hello 失敗硬體 tooa 狀況良好的實體機器的虛擬機器。 即時移轉會保留作業只能暫停 hello 虛擬機器，短時間的 VM。 系統會維護記憶體中，開啟的檔案，與網路連線，但前及/或 hello 事件之後，可能會降低效能。 無法使用即時移轉的情況下，hello VM 將會遇到非預期的停機時間，如下所述。


* **非預期的停機時間**hello 硬體或 hello 基礎虛擬機器的實體基礎結構發生某種錯誤，很少時發生。 這可能包含本機網路錯誤、本機磁碟錯誤，或其他機架層級的錯誤。 偵測到這類失敗時，hello Azure 平台會自動移轉 （治療） 虛擬機器 tooa 狀況良好實體電腦。 Hello 修復程序，在虛擬機器停機 （重新開機） 和 hello 暫存磁碟機的部分情況下遺失。 hello 附加 OS 和資料磁碟一定會被保留。 

* **已規劃的維護事件**會定期更新由 Microsoft toohello 基礎 Azure 平台 tooimprove 整體的可靠性、 效能和安全性的虛擬機器執行的 hello 平台基礎結構。 這些更新大多數都會在不影響虛擬機器或雲端服務的情況下執行 (請參閱 [VM 保留維護](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance))。 雖然 hello Azure 平台嘗試 toouse VM 保留維護在所有可能的情況下，有極少數的執行個體時這些更新需要重新開機，您的虛擬機器 tooapply hello 必要的更新 toohello 基礎結構。 在此情況下，您也可以初始化為其 Vm hello 適合時間視窗中的 hello 維護，以執行 Azure 規劃的維護與維護重新部署作業。 如需詳細資訊，請參閱[虛擬機器的規劃維護](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/)。


tooreduce hello 停機 tooone 或多個事件的影響，我們建議您遵守您的虛擬機器的高可用性最佳作法的 hello:

* [針對備援在可用性設定組中設定多部虛擬機器]
* [將受控磁碟使用於可用性設定組中的 VM]
* [使用排程的事件 tooproactively 回應 tooVM 影響事件](https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [將每個應用程式層設定至不同的可用性設定組中]
* [將負載平衡器與可用性設定組結合]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>針對備援在可用性設定組中設定多部虛擬機器
tooprovide 備援 tooyour 應用程式中，我們建議您群組的可用性設定組中的兩個或多個虛擬機器。 此組態可確保任一個計劃或非計劃性維護事件期間，至少一部虛擬機器可變更，同時符合 hello 99.95%Azure SLA。 如需詳細資訊，請參閱 hello[虛擬機器的 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)。

> [!IMPORTANT]
> 避免一個可用性設定組中只有一部執行個體虛擬機器。 此組態中的 VM 不符合 SLA 的保證，而且會在 Azure 規劃的維護事件期間發生停機狀況，除非單一 VM 是使用 [Azure 進階儲存體](../articles/storage/common/storage-premium-storage.md)。 對於使用進階儲存體的單一 Vm，適用於 Azure SLA hello。

在您的可用性設定組中每個虛擬機器指派了**更新網域**和**容錯網域**由 hello 基礎 Azure 平台。 若為給定的可用性集合時，五個使用者設定的更新網域會指派預設 （資源管理員部署則是增加的 tooprovide 向上 too20 更新網域） 的虛擬機器及基礎實體硬體 tooindicate 群組可以在 hello 重新啟動相同的時間。 五個以上的虛擬機器設定一個可用性設定組內，hello 第六個虛擬機器會放入相同更新網域做為第一個虛擬機器 hello，hello 第七個中的相同更新網域 hello 第二個虛擬機器，以及讓 hello hello上。 正在重新啟動可能不會繼續循序計劃性的維護期間的更新網域，但只能有一個更新網域的 hello 順序已重新啟動一次。 重新啟動的更新網域有 30 分鐘 toorecover 維護會在不同更新網域上起始之前。

容錯網域定義 hello 群組共用通用的電力來源和網路交換器的虛擬機器。 根據預設，設定您的可用性設定組中的 hello 虛擬機器之間隔開 toothree 容錯網域 （兩個故障網域的傳統） 資源管理員部署設定。 將您的虛擬機器放置到可用性設定組不會從作業系統或特定應用程式失敗保護您的應用程式，而它在限制 hello 潛在的實體硬體故障、 網路中斷或電源中斷的影響。

<!--Image reference-->
   ![Hello 更新網域和故障網域組態的概念圖](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>將受控磁碟使用於可用性設定組中的 VM
如果您目前使用的 Vm 具有未受管理的磁碟，我們強烈建議您使用[轉換中可用性設定組 toouse 管理磁碟 Vm](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md)。

[管理磁碟](../articles/virtual-machines/windows/managed-disks-overview.md)彼此隔離可用性設定組確保 hello 磁碟的可用性設定組的 Vm 夠 tooavoid 單一失敗點提供較佳的可靠性。 它會自動將 hello 磁碟放在不同的存放裝置叢集。 如果因為 toohardware 或軟體失敗而失敗的儲存體叢集，則只有 hello VM 執行個體與這些戳記上的磁碟失敗。

![受控磁碟 FD](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> hello 受管理的可用性設定組的容錯網域數目會因區域-兩個或三個每個區域。 hello 下表顯示 hello 數目每個區域

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

如果您計劃的 Vm toouse [unmanaged 磁碟](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks)，以下是虛擬硬碟 (Vhd) 的 Vm 會儲存為儲存體帳戶的最佳作法[分頁 blob](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs)。

1. **保留所有的磁碟 （OS 和資料） 相關聯的 VM 中 hello 相同儲存體帳戶**
2. **檢閱 hello[限制](../articles/storage/common/storage-scalability-targets.md)上未受管理的磁碟儲存體帳戶中的 hello 數目**之前新增多個 Vhd tooa 儲存體帳戶
3. **針對可用性設定組中的每個 VM 使用個別的儲存體帳戶。** 不會共用儲存體帳戶與多個 Vm 在 hello 相同可用性設定組。 它是可接受的 Vm 不同的可用性設定組 tooshare 儲存體帳戶間如果遵循上述最佳作法

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>將每個應用程式層設定至不同的可用性設定組中
如果您的虛擬機器是所有幾乎完全相同，而且做 hello 相同用途的應用程式時，我們建議您設定的可用性設定組的應用程式的每一層。  如果您將兩個不同層中 hello 相同可用性設定組的 hello 可以一次重新啟動相同的應用程式層中所有虛擬機器。 您可以藉由在可用性設定組中為每個層設定至少兩部虛擬機器，確保每個層中至少有一部虛擬機器可供使用。

例如，您無法將 hello 的所有虛擬機器都放在 hello 前端上執行 IIS、 Apache Nginx 一個可用性設定組中的應用程式。 請確定，只有前端的虛擬機器會放置在 hello 相同可用性設定組。 同樣地，也要確認資料層的虛擬機器僅會放在它們自己的可用性設定組中，如同複寫的 SQL Server 虛擬機器或 MySQL 虛擬機器。

<!--Image reference-->
   ![應用程式層](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>將負載平衡器與可用性設定組結合
結合 hello [Azure 負載平衡器](../articles/load-balancer/load-balancer-overview.md)可用性設定 tooget hello 大部分的應用程式恢復功能。 hello Azure 負載平衡器將分散多部虛擬機器之間的流量。 針對我們的標準層虛擬機器，會包含 hello Azure 負載平衡器。 並非所有的虛擬機器層包含 hello Azure 負載平衡器。 如需關於負載平衡虛擬機器的詳細資訊，請參閱 [負載平衡虛擬機器](../articles/virtual-machines/virtual-machines-linux-load-balance.md)。

如果不是 hello 負載平衡器設定 toobalance 流量跨多個虛擬機器，計劃性的維護的任何事件影響 hello 只有流量服務的虛擬機器，造成中斷 tooyour 應用程式層。 相同層下 hello 相同負載平衡器和持續由至少一個執行個體的可用性集可讓流量 toobe 放置 hello 的多個虛擬機器。


<!-- Link references -->
[針對備援在可用性設定組中設定多部虛擬機器]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[將每個應用程式層設定至不同的可用性設定組中]: #configure-each-application-tier-into-separate-availability-sets
[將負載平衡器與可用性設定組結合]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[將受控磁碟使用於可用性設定組中的 VM]: #use-managed-disks-for-vms-in-an-availability-set
