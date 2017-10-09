# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>在傳統 tooAzure 資源管理員移轉期間的常見錯誤
此文件類別目錄會從 Azure 傳統部署模型 toohello Azure Resource Manager 堆疊的 IaaS 資源 hello 移轉期間 hello 最常見的錯誤和防護功能。

## <a name="list-of-errors"></a>錯誤清單
| 錯誤字串 | 緩和 |
| --- | --- |
| 內部伺服器錯誤 |在某些情況下，這是隨著重試消失的暫時性錯誤。 如果持續 toopersist，[連絡 Azure 支援](../articles/azure-supportability/how-to-create-azure-support-request.md)依其需要調查平台的記錄檔。 <br><br> **注意：**修訂 hello 事件是由 hello 支援小組，請不要嘗試任何自我補救這可能會有您的環境中預期的結果。 |
| 移轉不支援 HostedService {hosted-service-name} 中的部署 {deployment-name}，因為它是 PaaS 部署 (Web/背景工作角色)。 |這會在部署包含 Web/背景工作角色時發生。 因為僅支援虛擬機器的移轉，請移除 hello 部署的 hello web/背景工作角色，然後再試一次移轉。 |
| 範本 {template-name} 部署失敗。 相互關聯識別碼 = {guid} |在 hello 後端中的 移轉服務，我們可以使用 Azure Resource Manager 範本 toocreate 資源 hello Azure Resource Manager 堆疊中。 範本是具有等冪性，因為通常您可以安全地重試一次 hello 移轉作業 tooget 忽略錯誤。 如果此錯誤持續 toopersist，請[連絡 Azure 支援](../articles/azure-supportability/how-to-create-azure-support-request.md)授與他們 hello 的相互關聯識別碼。 <br><br> **注意：**修訂 hello 事件是由 hello 支援小組，請不要嘗試任何自我補救這可能會有您的環境中預期的結果。 |
| hello 虛擬網路 {虛擬-網路-名稱} 不存在。 |如果您在 hello 新版 Azure 入口網站中建立 hello 虛擬網路，也可能會發生。 hello 實際虛擬網路名稱遵循 hello 模式 」 群組 * <VNET name>" |
| HostedService {hosted-service-name} 中的 VM {vm-name} 包含擴充 {extension-name}，在 Azure Resource Manager 中不支援。 建議 toouninstall 從 hello VM，再繼續進行移轉。 |XML 擴充，例如 BGInfo 1.*，在 Azure Resource Manager 中不支援。 因此，這些擴充功能不能移轉。 如果這些擴充功能左邊的已安裝在 hello 虛擬機器，它們會自動解除安裝之前完成 hello 移轉。 |
| HostedService {hosted-service-name} 中的 VM {vm-name} 包含擴充 VMSnapshot/VMSnapshotLinux，目前不支援移轉。 從 hello VM 解除安裝，並將它傳回 hello 移轉已完成之後，使用 Azure 資源管理員 |這是 hello 案例 hello 虛擬機器設定 Azure 備份的位置。 由於這是目前不支援的案例，請遵循在 https://aka.ms/vmbackupmigration hello 因應措施 |
| VM {vm-名稱} {裝載-服務-名稱} 託管服務中的包含其狀態不從 hello VM 所報告的副檔名 {擴充功能-名稱}。 因此，無法移轉此 VM。 請確定該 hello 延伸模組狀態報告或從 hello VM 解除安裝 hello 延伸模組，然後重試移轉。 <br><br> HostedService {hosted-service-name} 中的 VM {vm-name} 包含擴充 {extension-name}，報告處理常式狀態：{handler-status}。 因此，無法移轉 hello VM。 請確認 hello 延伸模組處理常式狀態報告 {處理常式 status} 或從 hello VM 解除安裝然後重試移轉。 <br><br> VM {vm-名稱} {裝載-服務-名稱} 託管服務中的 VM 代理程式回報 hello 整體的代理程式狀態為未就緒。 因此，hello VM 可能不會移轉，是否可移轉的延伸模組。 請確定該 hello VM 代理程式報告為已備妥代理程式的整體狀態。 請參閱 toohttps://aka.ms/classiciaasmigrationfaqs。 |Azure 客體代理程式和 VM 延伸模組需要傳出網際網路存取 toohello VM 儲存體帳戶 toopopulate 及其狀態。 狀態失敗的常見原因包括 <li> 網路安全性群組會封鎖 toohello 對外存取網際網路 <li> 如果 hello VNET 具有內部 DNS 伺服器及 DNS 連線已遺失 <br><br> 如果您繼續 toosee 不支援的狀態，您可以解除安裝 hello 延伸 tooskip 這項檢查，然後繼續進行移轉。 |
| 移轉不支援 HostedService {hosted-service-name} 中的部署 {deployment-name}，因為它有多個可用性設定組。 |目前，只能移轉具有 1 或更少可用性設定組的託管服務。 toowork 解決這個問題，請將移 hello 其他可用性設定組和虛擬機器在不同的可用性集 tooa 託管服務。 |
| 不支援移轉託管服務中的部署 {部署-名稱} {裝載的服務名稱因為它有不屬於可用性設定組的 hello，即使 hello 託管服務包含一個 Vm。 |此案例中的 hello 因應措施是 tooeither 移動到單一可用性所有 hello 虛擬機器設定，或移除的 hello hello 託管服務中的可用性設定組中的所有虛擬機器。 |
| 儲存體帳戶/託管服務/虛擬網路 {虛擬-網路-名稱} 處於 hello 進行移轉，因此無法變更 |Hello 資源 hello 「 準備 」 移轉作業已完成，而使得變更 toohello 資源的作業觸發時，會發生這個錯誤。 「 準備 」 作業之後的 hello 管理平面 hello 鎖定，因為任何變更 toohello 資源會遭到封鎖。 toounlock hello 管理平面，您可以執行 hello 「 認可 」 移轉作業 toocomplete 移轉或 hello 「 中止 」 移轉作業 tooroll 回 hello 「 準備 」 作業。 |
| HostedService {hosted-service-name} 不允許移轉，因為它有 VM {vm-name} 處於下列「狀態」：RoleStateUnknown。 只有當 hello VM 處於 hello 下列其中一種狀態-執行、 已停止的停止取消配置允許移轉。 |hello VM 可能會開始進行透過狀態轉換，這通常發生在 hello 託管服務，例如重新啟動電腦上的更新作業期間，擴充功能安裝等等。建議的 hello 更新作業 toocomplete hello 託管服務上才會嘗試移轉。 |
| 部署託管服務 {裝載-服務-名稱} {部署-名稱} {vm-名稱} VM 包含了其實體 blob 的大小 {size-of-the-vhd-blob-backing-the-data-disk} 位元組與 hello VM 資料磁碟的邏輯大小 {不相符的資料磁碟 {資料-磁碟-名稱}size-of-the-data-disk-specified-in-the-vm-api} 個位元組。 移轉會繼續執行，而不指定 hello hello Azure 資源管理員 VM 的資料磁碟的大小。 | 如果您不更新 hello VM API 模型中的 hello 大小調整 hello VHD blob，則會發生這個錯誤。 詳細的緩和步驟說明[如下](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes)。|
| 驗證具有雲端服務 {Cloud Service name} 中 VM {VM name} 之媒體連結 {data disk Uri} 的資料磁碟 {data disk name} 時發生儲存體例外狀況。 請確定該 hello VHD 媒體連結可存取此虛擬機器 | 如果 hello hello 磁碟 VM 已被刪除或不再可存取，可能會發生這個錯誤。 請先確定 hello 磁碟 hello VM 存在。|
| HostedService {cloud-service-name} 中的 VM {vm-name} 包含 Disk with MediaLink {vhd-uri}，其具有 Azure Resource Manager 不支援的 blob 名稱 {vhd-blob-name}。 | "/"中不支援的計算資源提供者目前 hello hello blob 名稱時，就會發生此錯誤。 |
| 移轉不會允許部署託管服務 {雲端-服務-名稱} {部署-名稱}，因為它不是處於 hello 區域範圍內。 請參閱 toohttp://aka.ms/regionalscope 移動這個部署 tooregional 範圍。 | 在 2014 中，Azure 宣布的網路功能資源會從叢集層級範圍 tooregional 範圍移動。 請參閱 [http://aka.ms/regionalscope] 以取得詳細資訊 (http://aka.ms/regionalscope)。 Hello 部署移轉何時未於更新作業，會自動移 tooa 區域範圍內，就會發生此錯誤。 最佳的解決方法是 tooeither 新增端點 tooa VM，或資料磁碟 toohello VM，然後重試移轉。 <br> 請參閱[如何 Azure 中的傳統 Windows 虛擬機器上的端點上 tooset](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint)或[附加資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>詳細的緩和措施

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>與資料磁碟之實體 blob 的大小位元組的 VM 不符合 hello VM 資料磁碟的邏輯大小位元組。

這會 hello 資料磁碟的邏輯大小可以取得 hello 實際的 VHD blob 大小與同步處理。 可以輕鬆地驗證使用 hello 下列命令：

#### <a name="verifying-hello-issue"></a>正在驗證 hello 問題

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>緩和 hello 問題

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>移動 VM tooa 不同訂用帳戶完成移轉之後

Hello 移轉程序完成之後，您可能想 toomove hello VM tooanother 訂用帳戶。 不過，如果您有密碼/憑證參考的金鑰保存庫資源，hello 的 VM 移的 hello 目前不支援。 下面的指示 hello 可讓您 tooworkaround hello 問題。 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Azure CLI 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
