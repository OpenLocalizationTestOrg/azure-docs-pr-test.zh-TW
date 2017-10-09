# <a name="azure-managed-disks-overview"></a>Azure 受控磁碟概觀

Azure 受管理的磁碟，藉以管理 hello 簡化 Azure IaaS Vm 的磁碟管理[儲存體帳戶](../articles/storage/common/storage-introduction.md)hello VM 磁碟相關聯。 您只需要 toospecify hello 類型 ([Premium](../articles/storage/common/storage-premium-storage.md)或[標準](../articles/storage/common/storage-standard-storage.md)) 和 hello 大小磁碟的需要以及 Azure 會建立，並會為您管理 hello 磁碟。

## <a name="benefits-of-managed-disks"></a>受控磁碟的好處

讓我們看看一些 hello 的優點，您可以使用受管理的磁碟，從這個 Channel 9 影片，[更好的 Azure VM 恢復功能與管理磁碟](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency)。
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>簡單且可調整的 VM 部署

Hello 幕後，為您管理磁碟控點的儲存體。 之前，您必須為您的 Azure Vm toocreate 儲存體帳戶 toohold hello 磁碟 （VHD 檔案）。 當向上擴充，您必須確定您建立額外的儲存體帳戶，因此，您未與任何磁碟超出儲存體的 hello IOPS 限制 toomake。 使用受管理磁碟時處理儲存體，您都不會再受到 hello 儲存體帳戶限制 (例如 20000 IOPS / 帳戶)。 您也不再有 toocopy 您自訂映像 （VHD 檔案） toomultiple 儲存體帳戶。 您可以在中央位置 – 一個儲存體帳戶每個 Azure 區域 – 中管理它們，並用 toocreate 數百個 Vm 的訂用帳戶中。

受管理的磁碟可讓您向上 too10，000 VM toocreate**磁碟**中訂用帳戶，這可讓您的 toocreate 數千**Vm**單一訂用帳戶中。 這項功能也會進一步增加 hello 延展性[虛擬機器規模集 (VMSS)](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)可以讓您啟動 tooa 一千個 Vm toocreate VMSS，使用 Marketplace 映像中。

### <a name="better-reliability-for-availability-sets"></a>可用性設定組有更高的可靠性

受管理的磁碟可用性設定提供更佳的可靠性，方法是確保該 hello 磁碟[可用性設定組中的 Vm](../articles/virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set)完全分開彼此 tooavoid 單一失敗點。 它會自動將 hello 磁碟放在不同的存放裝置延展單位 （戳記）。 如果因為 toohardware 或軟體失敗而失敗的戳記，只有 hello VM 執行個體與這些戳記上的磁碟失敗。 例如，假設您有五個的 Vm 上執行的應用程式和 hello Vm 位於可用性設定組。 hello 這些 Vm 的磁碟將不會全部儲存在 hello 相同的戳記，因此如果一個戳記當機時，hello hello 應用程式的其他執行個體繼續 toorun。

### <a name="highly-durable-and-available"></a>高耐久性及可用性

Azure 磁碟設計成確保可用性達 99.999%。 得知有三個資料複本，因此有高持久性，這可讓您更安心。 如果一個或甚至兩個複本時遇到問題，hello 剩餘複本協助您確保持續性的資料，並容許較故障。 此結構讓 Azure 針對 IaaS 磁碟穩定地展現企業級持久性，提供領先界業的年度零失敗率。 

### <a name="granular-access-control"></a>細微的存取控制

您可以使用[所有存取控制 (RBAC)](../articles/active-directory/role-based-access-control-what-is.md) tooassign 受管理的磁碟 tooone 或更多使用者的特定權限。 管理磁碟會公開各種不同的作業，包括讀取、 寫入 （建立/更新）、 delete 和擷取[共用的存取簽章 (SAS) URI](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md) hello 磁碟。 您可以授與存取 tooonly hello 作業的人需要 tooperform 他的工作。 例如，如果您不想人員 toocopy tooa 受管理的磁碟儲存體帳戶，您可以選擇不 toogrant 存取 toohello 匯出動作的受管理的磁碟。 同樣地，如果您不想人員 toouse SAS URI toocopy 受管理的磁碟，您可以選擇不 toogrant 該權限 toohello 受管理的磁碟。

### <a name="azure-backup-service-support"></a>Azure 備份服務支援
使用 Azure 備份服務與管理磁碟 toocreate 以時間為基礎的備份，輕鬆 VM 還原與備份保留原則的備份作業。 受管理的磁碟只支援本機備援儲存體 (LRS) 做為 hello 複寫選項。這表示它會三份 hello 資料保存在單一區域。 針對區域性災害復原，您必須使用 [Azure 備份服務](../articles/backup/backup-introduction-to-azure-backup.md)來備份位於不同區域的 VM 磁碟，並以 GRS 儲存體帳戶作為備份保存庫。 目前 Azure Backup 支援資料磁碟大小 too1TB 向上進行備份。 如需深入了解，請參閱[針對具有受控磁碟的 VM 使用 Azure 備份服務](../articles/backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)。

## <a name="pricing-and-billing"></a>價格和計費

當使用受管理的磁碟，適用於 hello 遵循計費考量：
* 儲存體類型

* 磁碟大小

* 交易數

* 輸出資料傳輸

* 受控磁碟快照集 (完整磁碟複製)

讓我們仔細看看這些資訊。

**儲存體類型︰**受控磁碟提供 2 個效能層級︰[進階](../articles/storage/common/storage-premium-storage.md) (以 SSD 為基礎) 和[標準](../articles/storage/common/storage-standard-storage.md) (以 HDD 為基礎)。 您已選取 hello 磁碟的儲存體的類型取決於 hello 計費的受管理的磁碟。


**磁碟大小**： 的受管理的磁碟計費取決於佈建的 hello hello 磁碟大小。 Azure 對應 hello （無條件進位） 佈建的大小 toohello 最接近的受管理磁碟 hello 表中所指定的選項。 Hello 的每個受管理的磁碟對應 tooone 支援佈建的大小，並據此計費。 例如，如果您建立標準的受管理的磁碟，並指定佈建的大小為 200 GB，您需要付費根據 hello 定價的 hello S20 磁碟類型。

以下是 hello 磁碟大小適用於 premium 的受管理磁碟：

| **進階受控<br>磁碟類型** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| 磁碟大小        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


以下是 hello 磁碟大小適用於標準的受管理磁碟：

| **標準受控<br>磁碟類型** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| 磁碟大小        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**交易數**： 您所要支付 hello 您執行標準的受管理磁碟的交易數目。 進階受控磁碟沒有交易成本。

**輸出資料傳輸**： [輸出資料傳輸](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure 資料中心送出的資料) 會產生頻寬使用量費用。

如需受控磁碟價格的詳細資訊，請參閱[受控磁碟價格](https://azure.microsoft.com/pricing/details/managed-disks)。


## <a name="managed-disk-snapshots"></a>受控磁碟快照集

受控快照集是受控磁碟的完整唯讀複本，預設會儲存為標準受控磁碟。 快照集可讓您在任何時間點備份受控磁碟。 這些快照集存在與 hello 來源磁碟無關而且可以使用的 toocreate 新受管理的磁碟。 所支付的費用使用 hello 大小為基礎。 比方說，如果您建立 64 GB 的佈建的容量與實際使用的資料大小的 10 GB 的受管理磁碟的快照集，快照集將僅針對使用 hello 資料大小的 10 GB 計費。  

[增量快照](../articles/virtual-machines/windows/incremental-snapshots.md)目前不支援受管理的磁碟，但將在未來的 hello 支援。

toolearn 深入了解如何 toocreate 快照集，與受管理的磁碟，請簽出這些資源：

* [在 Windows 中建立 VHD 複本並儲存為受控磁碟](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [在 Linux 中建立 VHD 複本並儲存為受控磁碟](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)


## <a name="images"></a>映像

受控磁碟也支援建立受管理的自訂映像。 您可以從儲存體帳戶中的自訂 VHD 或直接從一般化 (系統預備的) VM 建立映像。 這會擷取所有受管理磁碟 VM，包括 hello OS 和資料磁碟相關聯的單一映像。 建立數百個 Vm 使用自訂映像沒有 hello 這個控制項可讓需要 toocopy 或管理任何儲存體帳戶。

如需建立映像的資訊，請查看下列發行項的 hello:
* [如何 toocapture 一般化 vm 在 Azure 中的受管理的映像](../articles/virtual-machines/windows/capture-image-resource.md)
* [Toogeneralize 和 Linux 虛擬機器使用的擷取 hello Azure CLI 2.0](../articles/virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>映像與快照集的比較

您通常看 hello 這個字 「 映像 」 的 Vm，搭配使用，現在您會看到以及的 「 快照集 」。 它是重要的 toounderstand hello 差異這些。 受控磁碟可讓您為已解除配置的一般化 VM 建立映像。 此映像會包含所有 hello 連接磁碟 toohello VM。 您可以使用此映像 toocreate 新的 VM，以及它將會包含所有的 hello 磁碟。

快照是磁碟的一份在 hello 點，它磁碟的所花的時間。 僅適用於 tooone 磁碟。 如果您有只有一個磁碟 (hello OS) 的 VM，您可以使用快照集或它的映像，並從 hello 快照集或 hello 映像建立 VM。

如果 VM 有五個磁碟，且都已等量分配，情形又如何？ 所採取的每個 hello 磁碟，快照集，但是無法得知內 hello hello hello 磁碟 – hello 快照集狀態的 VM 只是知道該一個磁碟。 在此情況下，hello 快照需要 toobe 相互協調，目前不支援。

## <a name="managed-disks-and-encryption"></a>受控磁碟與加密

有兩種加密 toodiscuss 參考 toomanaged 磁碟中。 hello 第一次是儲存體服務加密 (SSE) 中，這會由 hello 儲存體服務執行。 hello 第二個是 Azure 磁碟加密，您可以為您的 Vm hello OS 和資料磁碟啟用。

### <a name="storage-service-encryption-sse"></a>儲存體服務加密 (SSE)

[Azure 儲存體服務加密](../articles/storage/common/storage-service-encryption.md)提供靜態加密和保護資料 toomeet 您組織的安全性與相容性承諾。 預設會啟用 SSE 所有受管理的磁碟，快照集和受管理的磁碟可使用的所有 hello 區域中的映像。 啟動 2017 年 6 月 10 日，所有新的受管理的映像的磁碟/快照集和新資料寫入 tooexisting 管理磁碟可自動加密靜止由 Microsoft 管理的索引鍵。  請瀏覽 hello[管理磁碟常見問題集頁面](../articles/virtual-machines/windows/faq-for-disks.md#managed-disks-and-storage-service-encryption)如需詳細資訊。


### <a name="azure-disk-encryption-ade"></a>Azure 磁碟加密 (ADE)

Azure 磁碟加密可讓您 tooencrypt hello OS 和 IaaS 虛擬機器使用的資料磁碟。 這包括受控磁碟。 適用於 Windows、 hello 磁碟會使用業界標準的 BitLocker 加密技術來加密。 適用於 Linux，hello 磁碟會使用 hello DM Crypt 技術來加密。 這是與整合 Azure 金鑰保存庫 tooallow 您 toocontrol 和管理 hello 磁碟加密金鑰。 如需詳細資訊，請參閱 [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](../articles/security/azure-security-disk-encryption.md)。

## <a name="next-steps"></a>後續步驟

如需有關管理磁碟的詳細資訊，請參閱下列文章 toohello。

### <a name="get-started-with-managed-disks"></a>開始使用受管理的磁碟

* [使用 Resource Manager 和 PowerShell 建立 VM](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md)

* [建立 Linux VM，使用 Azure CLI 2.0 hello](../articles/virtual-machines/linux/quick-create-cli.md)

* [附加的受管理的資料磁碟 tooa Windows VM 使用 PowerShell](../articles/virtual-machines/windows/attach-disk-ps.md)

* [新增受管理的磁碟 tooa Linux VM](../articles/virtual-machines/linux/add-disk.md)

* [受控磁碟的 PowerShell 範例指令碼](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [在 Azure Resource Manager 範本中使用受控磁碟](../articles/virtual-machines/windows/using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>比較受控磁碟儲存體選項

* [進階儲存體和磁碟](../articles/storage/common/storage-premium-storage.md)

* [標準儲存體和磁碟](../articles/storage/common/storage-standard-storage.md)

### <a name="operational-guidance"></a>作業指引

* [從 AWS 和其他平台 tooManaged 磁碟在 Azure 中的移轉](../articles/virtual-machines/windows/on-prem-to-azure.md)

* [在 Azure 中的 Azure Vm toomanaged 磁碟轉換](../articles/virtual-machines/windows/migrate-to-managed-disks.md)
