Azure 虛擬機器 (Vm)，有時可能會針對無明顯原因，而您初始 hello 重新開機作業的辨識項不重新開機。 本文列出 hello 動作和事件，可能會導致 Vm tooreboot 並提供深入了解 tooavoid 非預期重新開機問題或降低 hello 影響這類問題的方式。

## <a name="configure-hello-vms-for-high-availability"></a>設定高可用性的 hello Vm
重新開機的最佳方式 tooprotect hello 對 VM 在 Azure 執行的應用程式停機時間地 tooconfigure hello Vm 的高可用性。

tooprovide 這個層級的備援性 tooyour 應用程式，我們建議您群組的可用性設定組中的兩個或多個 Vm。 此組態可確保任一個計劃或非計劃性維護事件期間，至少一個 VM 仍可使用和符合 hello 99.95% [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/)。

如需可用性設定組的詳細資訊，請參閱下列文章 hello:

- [管理 Vm hello 可用性](../articles/virtual-machines/windows/manage-availability.md)
- [設定 VM 的可用性](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>資源健全狀況資訊 
Azure 資源健全狀況是一種服務，公開 hello 健全狀況的個別 Azure 資源，並提供可採取動作的指導方針來進行疑難排解。 在雲端環境中不可能 toodirectly 存取伺服器或基礎結構項目，hello 目標的資源健全狀況會是您花在疑難排解 tooreduce hello 時間。 特別是，hello 目標是 tooreduce hello 所花的時間決定是否 hello 根 hello 問題的所在 hello 內的事件或 hello 應用程式中 Azure 平台。 如需詳細資訊，請參閱[了解和使用資源健全狀況](../articles/resource-health/resource-health-overview.md)。

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>動作和事件，可能會造成 hello VM tooreboot

### <a name="planned-maintenance"></a>預定的維修
Microsoft Azure 會定期更新跨 hello 地球 tooimprove hello 可靠性、 效能和安全性構成 Vm hello 主機基礎結構的執行。 許多這些更新 (包括記憶體保留的更新) 在執行時並不會對 VM 或雲端服務造成任何影響。

不過，有些更新的確需要重新開機。 在這種情況下，hello Vm 會關閉而我們修補 hello 基礎結構，並再重新啟動 hello Vm。

toounderstand 哪些 Azure 計劃性的維護，且它會如何影響 hello 可用性的 Linux Vm，請參閱此處所列的 hello 文件。 hello 文章提供有關 hello Azure 計劃性的維護程序的背景和 tooschedule 計劃的維護 toofurther 如何減少 hello 的影響。

- [Azure 中 VM 的計劃性維護](../articles/virtual-machines/windows/planned-maintenance.md)
- [Tooschedule Azure Vm 上所規劃的維護](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>記憶體保留的更新   
對於 Microsoft Azure 中的這類更新，使用者覺得其執行中的 VM 不受任何影響。 許多這些更新的 toocomponents 或可以更新，而不干擾 hello 執行執行個體的服務。 有些 hello 主機作業系統上的 hello Vm 重新開機不可以套用的平台基礎結構更新。

這些記憶體保留的更新是透過可進行就地即時移轉的技術來完成。 正在更新，hello VM 會放置於*暫停*狀態。 此狀態會保留在 RAM 中的 hello 記憶體 hello 基礎主機作業系統可接收 hello 必要更新和修補程式。 hello VM 會在暫停的 30 秒內繼續執行。 之後 hello 繼續 VM 時，它的時鐘會自動同步處理。

因為 hello 短暫的延遲期間，將更新部署透過此機制可大幅減少 hello hello Vm 上的影響。 不過，並非所有更新都可以此方式部署。 

多重執行個體更新 (可用性設定組中的 VM) 一次只會套用到一個更新網域。

> [!NOTE]
> 在此更新方法期間，舊核心版本的 Linux 機器會受到核心異常影響。 tooavoid 這個問題，請更新 tookernel 版本 3.10.0-327.10.1 或更新版本。 如需詳細資訊，請參閱[主機節點升級後以 3.10 為基礎的核心異常上的 Azure Linux VM](https://support.microsoft.com/help/3212236)。     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>使用者起始的重新開機或關機動作
 
如果您從 hello Azure 入口網站、 Azure PowerShell、 命令列介面或重設 API 執行重新開機，您可以在 hello 找到 hello 事件[Azure 活動記錄檔](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md)。

如果您執行 hello 動作從 hello VM 的作業系統，您可以在 hello 系統記錄檔中找到 hello 事件。

通常會造成 hello VM tooreboot 其他案例包括多個組態變更動作。 您通常會看到警告訊息，指出執行特定動作將會導致 hello VM 重新開機。 範例包括任何 VM 大小調整作業，變更 hello 密碼 hello 管理帳戶，以及設定靜態 IP 位址。

### <a name="azure-security-center-and-windows-update"></a>Azure 資訊安全中心與 Windows Update
Azure 資訊安全中心每日監視 Windows 和 Linux VM 是否有遺漏的作業系統更新。 資訊安全中心會根據 Windows VM 上設定的服務，從 Windows Update 或 Windows Server Update Services (WSUS) 擷取可用的安全性和重大更新清單。 資訊安全中心也會檢查 hello 最新的 Linux 系統的更新。 如果您的 VM 遺漏系統更新，資訊安全中心建議您套用系統更新。 這些系統更新的 hello 應用程式被由 hello Azure 入口網站中的 hello 資訊安全中心。 套用某些更新後，可能需要 VM 重新開機。 如需詳細資訊，請參閱[在 Azure 資訊安全中心套用系統更新](../articles/security-center/security-center-apply-system-updates.md)。

如同在內部部署伺服器，Azure 不會不推送更新從 Windows Update tooWindows Azure Vm，因為這些機器預定的 toobe 受其使用者。 您，不過，是鼓勵 tooleave hello 自動 Windows Update 設定已啟用。 自動安裝 Windows update 的更新也可能導致重新開機 toooccur 套用 hello 更新之後更新。 如需詳細資訊，請參閱 [ Windows 更新常見問題集](https://support.microsoft.com/help/12373/windows-update-faq)。

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>其他情況下會影響您的 VM hello 可用性
有其他情況下，Azure 可能會主動暫停 hello 使用 VM。 您會收到電子郵件通知之前不會採取這個動作，讓您將有機會 tooresolve hello 基礎問題。 問題會影響 VM 的可用性的範例包括安全性違規和付款方法 hello 到期。

### <a name="host-server-faults"></a>主機伺服器錯誤 
hello VM 被裝載在 Azure 資料中心內執行的實體伺服器上。 hello 實體伺服器執行的代理程式會呼叫 hello 主機代理程式中加入 tooa 幾個其他 Azure 元件。 當這些 hello 實體伺服器上的 Azure 軟體元件都沒有回應時，hello 監視系統會觸發 hello 主機伺服器 tooattempt 復原的重新開機。 hello VM 可通常一次五分鐘內，而且會 toolive hello 相同在如先前所裝載。

伺服器錯誤通常被因硬體失敗，例如硬碟或固態硬碟 hello 失敗。 Azure 持續監視這些項目、 識別 hello 基礎錯誤，以及之後已經實作並測試 hello 緩和中推出的更新。

因為有些主機伺服器錯誤可能是特定 toothat 伺服器，重複的 VM 重新開機情況可能會改善利用手動重新部署 hello VM tooanother 主機伺服器。 這項作業可藉由使用 hello**重新部署**選項 hello hello VM，詳細資料頁面上，或藉由停止再重新啟動 hello VM hello Azure 入口網站中。

### <a name="auto-recovery"></a>自動復原
如果 hello 主機伺服器無法重新啟動，因為任何原因，hello Azure 平台會起始自動復原動作 tootake hello 故障主機伺服器離輪替循環以便進一步調查。 

在該主機上的所有 Vm 都會自動重新配置的 tooa 不同、 狀況良好的主機伺服器。 此程序通常在 15 分鐘內完成。 toolearn 進一步了解 hello 自動復原程序，請參閱[自動復原 Vm](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines)。

### <a name="unplanned-maintenance"></a>非計劃性維護
在少數情況下，hello Azure 作業小組可能需要 tooperform 維護活動 tooensure hello hello Azure 平台的整體健全狀況。 這種行為可能會影響 VM 的可用性，則通常會導致 hello 相同自動復原動作，如先前所述。  

未計劃的 maintenances hello 如下：

- 緊急節點磁碟重組
- 緊急網路交換器更新

### <a name="vm-crashes"></a>VM 損毀
Vm 可能會重新啟動，因為 hello VM 本身內發生問題。 hello 工作負載或 hello VM 執行的角色可能會觸發錯誤檢查 hello 客體作業系統內。 幫助您判斷 hello hello 損毀的原因，hello 系統和應用程式記錄檔檢視適用於 Windows Vm，適用於 Linux Vm hello 序列的記錄檔。

### <a name="storage-related-forced-shutdowns"></a>儲存體相關的強制關機
在 Azure 中的 Vm 依賴作業系統和裝載 hello Azure 儲存體基礎結構的資料存放區的虛擬磁碟。 每當 hello 可用性或 hello VM 和相關聯的 hello 虛擬磁碟之間的連線會影響多個 120 秒，hello Azure 平台執行 hello Vm tooavoid 資料損毀的強制的關閉。 hello Vm 自動供電回復之後儲存體連線已還原。 

hello hello 關機期間可以是五分鐘的時間越短，但可能會大幅延長。 hello 以下是 hello 與儲存體相關的強制關閉相關聯的特定案例的其中一個： 

**超出 IO 限制**

Vm 可能會暫時關閉時 I/O 要求會持續節流，因為 hello 的 I/O 作業每秒 (IOPS) 的磁碟區超過 hello 磁碟的 hello I/O 限制。 (標準磁碟儲存體是有限 too500 IOPS。)toomitigate 這個問題，請使用磁碟條狀配置，或設定 hello hello 客體 VM 中，根據 hello 工作負載內的儲存空間。 如需詳細資訊，請參閱[設定 Azure VM 以達到最佳的儲存體效能](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx)。

使用透過 Azure 高階儲存體與向上 too80，000 IOPS 高 IOPS 限制。 如需詳細資訊，請參閱[高效能進階儲存體](../articles/storage/common/storage-premium-storage.md)。

### <a name="other-incidents"></a>其他事件
在少數情況下，廣泛的問題可能會影響 Azure 資料中心內的多部伺服器。 如果發生這個問題，hello Azure 團隊會傳送電子郵件通知受影響的 toohello 訂用帳戶。 您可以檢查 hello [Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)和 hello Azure 入口網站的 hello 狀態的進行中中斷和過去的事件。
