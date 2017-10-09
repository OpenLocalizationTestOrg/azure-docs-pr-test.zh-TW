>[!NOTE]
> 您可以在此頁面上，或透過 [Azure 意見反應](https://feedback.azure.com/forums/216843-virtual-machines) 並利用 #azerrormessage 標記，發表對於錯誤訊息的意見反應。

## <a name="error-response-format"></a>錯誤回應的格式 
Azure Vm 中使用下列 JSON 格式的錯誤回應 hello:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

錯誤回應永遠包含狀態碼和錯誤物件。 每個錯誤物件永遠包含錯誤碼和訊息。 如果 hello 建立 VM 範本，hello 錯誤物件也會包含詳細資料 區段包含的錯誤碼和訊息內部層級。 一般來說，hello 大部分內部層級的錯誤訊息為 hello 根失敗。


## <a name="common-virtual-machine-management-errors"></a>常見的虛擬機器管理錯誤

此區段會列出 hello 管理 Vm 時，可能會遇到常見錯誤訊息：

|  錯誤碼  |  錯誤訊息  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  建立磁碟 '{0}' 使用 blob URI {1} 時無法 tooacquire 租用。 Blob 已在使用中。  |  
|  AllocationFailed  |  配置失敗。 請嘗試減少 hello VM 大小或 Vm 數目、 稍後重試，或嘗試部署 tooa 其他可用性設定組或其他 Azure 位置。  |  
|  AllocationFailed  |  hello VM 配置失敗，因為 tooan 內部錯誤。 請稍後再重試，或嘗試部署 tooa 不同的位置。  |
|  ArtifactNotFound  |  在位置 '{2}' 中找不到 hello 發行者 '{0}' 和型別 '{1}' VM 擴充功能。  |
|  ArtifactNotFound  |  發行者 '{0}'，輸入 '{1}'，與 hello 延伸模組儲存機制中找不到類型處理常式版本 '{2}'。  |
|  ArtifactVersionNotFound  |  沒有找到符合 hello hello 成品儲存機制中的版本要求版本 '{0}'。  |
|  ArtifactVersionNotFound  |  沒有找到符合 hello hello 成品儲存機制中的版本要求發行者 '{1}' 與類型 '{2}' 版本 '{0}' 的 VM 延伸模組。  |
|  AttachDiskWhileBeingDetached  |  無法附加資料磁碟 '{0}' tooVM '{1}'，因為目前正在卸離 hello 磁碟。 請等候 hello 磁碟完全中斷連結，並再試一次。  |
|  BadRequest  |  此區域尚不支援「對齊」可用性設定組。  |
|  BadRequest  |  新增具有 toonon 管理可用性設定組或新增具有基礎 blob 磁碟 toomanaged 可用性設定組的 VM 不支援受管理的磁碟的 VM。 請建立可用性設定組 'managed' 屬性設定順序 tooadd 在具有受管理的磁碟 tooit 的 VM。  |
|  BadRequest  |  此區域不支援受控磁碟。  |
|  BadRequest  |  作業系統類型 '{0}' 不支援每個處理常式有多個 VMExtensions。 已新增或在輸入中已指定處理常式為 '{2}' 的 VMExtension '{1}'。  |
|  BadRequest  |  具有受控磁碟的資源 '{1}' 不支援作業 '{0}'。  |
|  CertificateImproperlyFormatted  |  hello 從 {0} 擷取密碼的 JSON 表示有一個資料欄位不是正確格式的 PFX 檔案，或提供的 hello 密碼未正確解碼 hello PFX 檔案。  |
|  CertificateImproperlyFormatted  |  無法還原序列化為 JSON hello {0} 從擷取的資料。  |
|  衝突  |  只有在建立 VM 時或 hello VM 解除配置時，被允許調整磁碟大小。  |
|  ConflictingUserInput  |  無法附加磁碟 '{0}'，因為 vm '{1}' 已擁有 hello 磁碟。  |
|  ConflictingUserInput  |  來源與目的地資源群組是 hello 相同。  |
|  ConflictingUserInput  |  磁碟 {0} 的來源和目的地儲存體帳戶不同。  |
|  ContainerAlreadyOnLease  |  Hello 儲存體容器保留 uri 為 {0} hello blob 上已有租用。  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  hello 移動資源要求包含一個或多個 {0} s hello 要求中所參考的 KeyVault 資源。 跨訂用帳戶移動目前不支援此功能。 請檢查 hello hello KeyVault 資源識別碼的錯誤詳細資料。  |
|  DiagnosticsOperationInternalError  |  處理 VM {0} 的診斷設定檔時發生內部錯誤。  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  Blob {0} 已經由另一個磁碟 tooVM '{1}' 使用中。 您可以檢查 hello hello 磁碟參考資訊的 blob 中繼資料。  |
|  DiskBlobNotFound  |  無法 toofind VHD blob URI {0} 磁碟 '{1}'。  |
|  DiskBlobNotFound  |  無法 toofind VHD blob uri 為 {0}。  |
|  DiskEncryptionKeySecretMissingTags  |  {0} 密碼不需要 hello {1} 標記。 請更新 hello 密碼版本，新增所需的 hello 標籤，然後重試。  |
|  DiskEncryptionKeySecretUnwrapFailed  |  使用金鑰 {1} 解除密碼 {0} 值的密封失敗。  |
|  DiskImageNotReady  |  磁碟映像 {0} 處於 {1} 狀態。 映像備妥時，請重試。  |
|  DiskPreparationError  |  準備 VM 磁碟時發生一或多個錯誤。 如需詳細資訊，請參閱磁碟執行個體檢視。  |
|  DiskProcessingError  |  磁碟處理停止，因為 hello VM 失敗的磁碟中有其他磁碟。  |
|  ImageBlobNotFound  |  無法 toofind VHD blob URI {0} 磁碟 '{1}'。  |
|  ImageBlobNotFound  |  無法 toofind VHD blob uri 為 {0}。  |
|  IncorrectDiskBlobType  |  磁碟 blob 只可是分頁 blob 類型。 磁碟 '{1}' 的 blob {0} 為區塊 blob 類型。  |
|  IncorrectDiskBlobType  |  磁碟 blob 只可是分頁 blob 類型。 Blob {0} 是 '{1}' 類型。  |
|  IncorrectImageBlobType  |  磁碟 blob 只可是分頁 blob 類型。 磁碟 '{1}' 的 blob {0} 為區塊 blob 類型。  |
|  IncorrectImageBlobType  |  磁碟 blob 只可是分頁 blob 類型。 Blob {0} 是 '{1}' 類型。  |
|  InternalOperationError  |  無法解析儲存體帳戶 {0}。 請確定它已透過 hello 儲存體資源提供者中建立 hello 相同 hello 與位置計算資源。  |
|  InternalOperationError  |  {0} 目標搜尋工作失敗。  |
|  InternalOperationError  |  驗證 VM '{0}' 的 hello 網路設定檔時發生錯誤。  |
|  InvalidAccountType  |  hello AccountType {0} 無效。  |
|  InvalidParameter  |  參數 {0} hello 值無效。  |
|  InvalidParameter  |  不允許指定 hello 系統管理員密碼。  |
|  InvalidParameter  |  "hello 提供密碼必須介於 {0}-\ {1 \} 個字元長，且至少必須符合 {2} 的 hello 下列密碼複雜性需求： <ol><li> 包含大寫字元</li><li>包含小寫字元</li><li>包含數字</li><li>包含特殊字元。</li></ol>  |
|  InvalidParameter  |  不允許 hello 指定管理員使用者名稱。  |
|  InvalidParameter  |  無法附加現有的作業系統磁碟，如果 hello 建立 VM 時從平台或使用者映像。  |
|  InvalidParameter  |  容器名稱 {0} 無效。 容器名稱長度必須是 3-63 個字元，而且只能包含小寫英數字元和連字號。 連字號前後都必須緊接英數字元。  |
|  InvalidParameter  |  URL {1} 中的容器名稱 {0} 無效。 容器名稱長度必須是 3-63 個字元，而且只能包含小寫英數字元和連字號。 連字號前後都必須緊接英數字元。  |
|  InvalidParameter  |  在 URL {0} hello blob 名稱包含斜線。 磁碟目前不支援這種作法。  |
|  InvalidParameter  |  hello URI {0} 看起來並無 toobe 正確的 blob URI。  |
|  InvalidParameter  |  磁碟名稱為 '{0}' 已經使用 hello 相同的 LUN: {1}。  |
|  InvalidParameter  |  名為 '{0}' 的磁碟已經存在。  |
|  InvalidParameter  |  無法指定使用者映像覆寫已經在指定的 hello 中定義為磁碟映像參考。  |
|  InvalidParameter  |  磁碟名稱為 '{0}' 已經使用 hello 相同的 VHD URL {1}。  |
|  InvalidParameter  |  hello 指定的錯誤網域計數 {0} 必須落在 hello 範圍 {1} too\ {2 \}。  |
|  InvalidParameter  |  hello 授權類型 {0} 無效。 有效授權類型為: Windows_Client 或 Windows_Server (區分大小寫)。  |
|  InvalidParameter  |  Linux 主機名稱不能超過 {0} 個字元的長度，或包含下列字元的 hello: {1}。  |
|  InvalidParameter  |  Ssh 公開金鑰的目的地路徑是目前限制的 tooits 預設值 {0} 到期 tooa 已知 Linux 佈建代理程式中的問題。  |
|  InvalidParameter  |  已有磁碟的 LUN 為 {0}。  |
|  InvalidParameter  |  Hello 要求的訂用帳戶 {0} 必須符合包含在 hello 受管理的磁碟識別碼 hello 訂用帳戶 {1}。  |
|  InvalidParameter  |  OSProfile 中的自訂資料必須以 Base64 編碼，而且長度上限為 {0} 個字元。  |
|  InvalidParameter  |  URL {0} 中的 blob 名稱必須以 '{1}' 副檔名結尾。  |
|  InvalidParameter  |  '{0}' 不是有效擷取的 VHD blob 名稱前置詞。 有效的前置詞符合 regex '{1}'。  |
|  InvalidParameter  |  如果尚未佈建 hello VM 代理程式，憑證無法加入 tooyour VM。  |
|  InvalidParameter  |  已有磁碟的 LUN 為 {0}。  |
|  InvalidParameter  |  無法 toocreate hello VM hello 要求大小 {0}，因此不適用於 hello 叢集 hello 可用性設定組目前配置的位置。 hello 可用大小： {1}。 請前往 https://aka.ms/azure-resizevm，深入了解 VM 的大小調整策略。  |
|  InvalidParameter  |  hello VM 大小 {0} 無法取得要求 hello 目前區域中。 hello hello 目前區域中可用的大小為： {1}。 Https://aka.ms/azure-regions 在每個區域中，以找出需 hello 可用的 VM 大小的詳細資訊。  |
|  InvalidParameter  |  hello VM 大小 {0} 無法取得要求 hello 目前區域中。 Https://aka.ms/azure-regions 在每個區域中，以找出需 hello 可用的 VM 大小的詳細資訊。  |
|  InvalidParameter  |  Windows 系統管理員使用者名稱不能超過 {0} 個字元長、 結尾句號 （.），或包含下列字元的 hello: {1}。  |
|  InvalidParameter  |  Windows 電腦名稱不能超過 {0} 個字元長、 不得完全為數字，或包含下列字元的 hello: {1}。  |
|  MissingMoveDependentResources  |  hello 移動資源要求不包含所有 hello 相依資源。 請查看遺漏資源識別碼的錯誤詳細資料。  |
|  MoveResourcesHaveInvalidState  |  hello 移動資源要求包含無效的儲存體帳戶相關聯的 Vm。 請查看這些資源識別碼和參考的儲存體帳戶名稱的詳細資料。  |
|  MoveResourcesHavePendingOperations  |  hello 移動資源要求包含的資源的作業正在擱置中。 請查看這些資源識別碼的詳細資料。 Hello 暫止作業完成之後請重試操作。  |
|  MoveResourcesNotFound  |  hello 移動的資源要求包含找不到的資源。 請查看這些資源識別碼的詳細資料。  |
|  NetworkingInternalOperationError  |  不明的網路配置錯誤。  |
|  NetworkingInternalOperationError  |  不明的網路配置錯誤  |
|  NetworkingInternalOperationError  |  在處理 hello VM 的網路設定檔時發生內部錯誤。  |
|  NotFound  |  找不到 hello 可用性設定組 {0}。  |
|  NotFound  |  來源虛擬機器 '{0}' hello 要求中指定不存在於此 Azure 位置。  |
|  NotFound  |  找不到 id 為 {0} 的租用戶。  |
|  NotFound  |  找不到 hello 映像 {0}。  |
|  NotSupported  |  hello 授權類型為 {0}，但 hello 映像 blob {1} 並非來自內部部署。  |
|  OperationNotAllowed  |  無法刪除可用性設定組 {0}。 在刪除可用性設定組之前，請確定它未包含任何 VM。  |
|  OperationNotAllowed  |  變更可用性集 SKU 從 'Aligned' too'Classic' 不允許。  |
|  OperationNotAllowed  |  Hello VM 未執行時，無法修改 hello VM 中的延伸模組。  |
|  OperationNotAllowed  |  在具有 blob 磁碟之虛擬機器上才支援 hello 擷取動作。 請使用 hello 「 影像 」 資源應用程式開發介面 toocreate 從受管理的虛擬機器映像。  |
|  OperationNotAllowed  |  無法從映像 {1} 建立 hello 資源 {0}，直到成功建立映像。  |
|  OperationNotAllowed  |  已配置 VM，請重試後 VM 解除配置時，不允許更新 tooencryptionSettings  |
|  OperationNotAllowed  |  不支援新增 blob 磁碟的受管理的磁碟 tooa VM。  |
|  OperationNotAllowed  |  附加 toobe tooa 此大小的 VM 是 {0} 允許 hello 的資料磁碟數目上限。  |
|  OperationNotAllowed  |  不支援新增 blob 磁碟 tooVM 與受管理的磁碟。  |
|  OperationNotAllowed  |  在映像 '{1}' hello 映像標示為刪除自不允許作業 '{0}'。 您可以只重試 hello 刪除作業 （或等候進行中的一個 toocomplete）。  |
|  OperationNotAllowed  |  Vm '{1}' hello VM 一般化自不允許作業 '{0}'。  |
|  OperationNotAllowed  |  因為還原點集合 '{1}' 已標示為要刪除，不允許作業 '{0}'。  |
|  OperationNotAllowed  |  因為 VM 擴充 '{1}' 已標示為要刪除，不允許對它執行作業 '{0}'。 您可以只重試 hello 刪除作業 （或等候進行中的一個 toocomplete）。  |
|  OperationNotAllowed  |  不允許作業 '{0}'，因為 hello 虛擬機器 '{1}' 正在佈建使用 hello 映像 '{2}'。  |
|  OperationNotAllowed  |  不允許作業 '{0}'，因為虛擬機器 ScaleSet '{1}' hello 正在使用映像 '{2}' hello。  |
|  OperationNotAllowed  |  Vm '{1}' hello VM 已標示為刪除自不允許作業 '{0}'。 您可以只重試 hello 刪除作業 （或等候進行中的一個 toocomplete）。  |
|  OperationNotAllowed  |  因為 hello VM 是已解除配置或標示 toobe 解除配置 VM '{1}' 不被允許作業 '{0}'。  |
|  OperationNotAllowed  |  Vm '{1}' hello VM 正在執行，因為不允許作業 '{0}'。 請關閉電源明確萬一您關閉 hello 從 VM hello 客體作業系統內。  |
|  OperationNotAllowed  |  Vm '{1}' hello VM 不會取消配置自不允許作業 '{0}'。  |
|  OperationNotAllowed  |  因為 VM '{1}' 的擴充 '{2}' 處於失敗狀態，不允許對此 VM 執行作業 '{0}'。  |
|  OperationNotAllowed  |  VM '{1}' 上不允許作業 '{0}'，因為有其他作業正在進行。  |
|  OperationNotAllowed  |  hello 作業 '{0}' 需要 hello 虛擬機器 '{1}' toobe 一般。  |
|  OperationNotAllowed  |  hello 作業需要執行的 hello VM toobe （或設定 toorun）。  |
|  OperationNotAllowed  |  磁碟大小 {0} GB，這是較 hello 大小 {1}GB 的相對應的磁碟映像中，不允許。  |
|  OperationNotAllowed  |  只能在 hello 虛擬機器擴展集建立時，可以加入處理常式 '{0}' 的虛擬機器擴展集延伸模組。  |
|  OperationNotAllowed  |  只能在虛擬機器擴展集已刪除的 hello 階段，您可以刪除處理常式 '{0}' 的虛擬機器擴展集延伸模組。  |
|  OperationNotAllowed  |  VM '{0}' 已在使用受控磁碟。  |
|  OperationNotAllowed  |  VM '{0}' 所屬 too'Classic' 可用性設定組 '{1}'。 請更新 hello 可用性設定 toouse 'Aligned' SKU，然後再重試 hello 轉換。  |
|  OperationNotAllowed  |  從映像建立的 VM 不能有 blob 磁碟。 所有磁碟都有 toobe 管理磁碟。  |
|  OperationNotAllowed  |  擷取無法完成作業，因為 hello VM 不被一般化。  |
|  OperationNotAllowed  |  因為 VM 磁碟經過轉換的 toomanaged 磁碟，不允許 VM '{0}' 上的管理作業。  |
|  OperationNotAllowed  |  進行中作業正在變更虛擬機器 {0} too\ {1 \} 的電源狀態。 請於稍後再執行作業 {2}。  |
|  OperationNotAllowed  |  無法 tooadd 或更新 hello VM。 hello 要求的 VM 大小 {0} 可能無法使用 hello 現有配置單位中。 請前往 https://aka.ms/azure-resizevm，深入了解 VM 的大小調整策略。  |
|  OperationNotAllowed  |  無法 tooresize hello VM hello 要求大小 {0}，因此不適用於 hello 叢集 hello 可用性設定組目前配置的位置。 hello 可用大小： {1}。 請前往 https://aka.ms/azure-resizevm，深入了解 VM 的大小調整策略。  |
|  OperationNotAllowed  |  無法 tooresize hello VM hello 要求大小 {0}，因此不適用於 hello 叢集 hello VM 目前配置位置。 請解除配置您 VM too\ {1 \} 的 tooresize （這是停止作業在 hello Azure 入口網站中的），然後再試一次 hello 的調整大小作業。 請前往 https://aka.ms/azure-resizevm，深入了解 VM 的大小調整策略。  |
|  OSProvisioningClientError  |  作業系統佈建的 VM '{0}' 失敗，因為目前正在佈建 hello 客體作業系統。  |
|  OSProvisioningClientError  |  VM '{0}' 的 OS 佈建失敗。 錯誤詳細資料： {1} 請確定 hello 映像已備妥 （一般化）。 <ul><li>適用於 Windows 的指示: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  產生 SSH 主機金鑰失敗。 錯誤詳細資料: {0}。 tooresolve 此問題，確認是否 Linux 代理程式已正確設定。 <ul><li>您可以檢查 hello 指示： https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  指定使用者名稱的 hello VM 不適用於此 Linux 散發套件。 錯誤詳細資料: {0}。  |
|  OSProvisioningInternalError  |  作業系統佈建 VM '{0}' 的失敗因為 tooan 內部錯誤。  |
|  OSProvisioningTimedOut  |  作業系統佈建 vm '{0}' 未在完成 hello 分配的時間。 hello VM 仍可能會完成佈建成功。 請稍後再查看佈建狀態。  |
|  OSProvisioningTimedOut  |  作業系統佈建 vm '{0}' 未在完成 hello 分配的時間。 hello VM 仍可能會完成佈建成功。 請稍後再查看佈建狀態。 此外，請確定已正確地準備 hello 映像 （一般化）。   <ul><li>適用於 Windows 的指示: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> 適用於 Linux 的指示: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  作業系統佈建 vm '{0}' 未在完成 hello 分配的時間。 不過，hello VM 客體代理程式已偵測到執行。 這暗示 hello 客體 OS 已正確地準備 toobe 做為 VM 映像 （CreateOption = FromImage）。 tooresolve 這個問題，請使用 hello VHD 現況 CreateOption = 附加或正確地準備進行用作映像：   <ul><li>適用於 Windows 的指示: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> 適用於 Linux 的指示: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  hello 所需的 VM 大小目前不提供在 hello 選取位置。  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  由於 tooongoing 平台更新，此時無法更新資源。 請稍後再試一次。  |
|  StorageAccountLimitation  |  儲存體帳戶 '{0}' 不支援分頁 blob，也就是必要的 toocreate 磁碟。  |
|  StorageAccountLimitation  |  儲存體帳戶 '{0}' 超過其配置的配額。  |
|  StorageAccountLocationMismatch  |  無法解析儲存體帳戶 {0}。 請確定它已透過 hello 儲存體資源提供者中建立 hello 相同 hello 與位置計算資源。  |
|  StorageAccountNotFound  |  找不到儲存體帳戶 {0}。 確保不會刪除儲存體帳戶，且所屬 toohello hello VM 相同的 Azure 位置。  |
|  StorageAccountNotRecognized  |  請使用由儲存體資源提供者管理的儲存體帳戶。 不支援使用 {0}。  |
|  StorageAccountOperationInternalError  |  存取儲存體帳戶 {0} 時發生內部錯誤。  |
|  StorageAccountSubscriptionMismatch  |  儲存體帳戶 {0} 不屬於 toosubscription {1}。  |
|  StorageAccountTooBusy  |  儲存體帳戶 '{0}' 目前太忙碌。 請考慮使用另一個帳戶。  |
|  StorageAccountTypeNotSupported  |  磁碟 {0} 使用的 {1} 是 Blob 儲存體帳戶。 請建立「一般用途」的儲存體帳戶。  |
|  StorageAccountTypeNotSupported  |  儲存體帳戶 {0} 為 {1} 類型。 開機診斷支援 {2} 儲存體帳戶類型。  |
|  SubscriptionNotAuthorizedForImage  |  hello 訂用帳戶未獲授權。  |
|  TargetDiskBlobAlreadyExists  |  Blob {0} 已經存在。 請提供其他 blob URI toocreate 新的空白資料磁碟 '{1}'。  |
|  TargetDiskBlobAlreadyExists  |  擷取作業無法繼續，因為目標映像 blob {0} 已經存在而且未設定 hello 旗標 toooverwrite VHD blob。 請刪除 hello blob 或 toooverwrite VHD blob 設定 hello 旗標，然後重試。  |
|  TargetDiskBlobAlreadyExists  |  因為目標映像 blob {0} 有作用中的租用，所以擷取作業無法繼續。   |
|  TargetDiskBlobAlreadyExists  |  Blob {0} 已經存在。 請提供其他 blob URI 做為磁碟 '{1}' 的目標。  |
|  TooManyVMRedeploymentRequests  |  VM '{0}' 已收到過多部署要求中的 hello Vm hello 與此 VM 的同一個可用性設定組內。 請稍後重試。  |
|  VHDSizeInvalid  |  所指定的 hello {0} '{1}' blob {2} 磁碟的磁碟大小值無效。 磁碟大小必須介於 {3} 和 {4} 之間。  |
|  VMAgentStatusCommunicationError  |  VM '{0}' 未回報 VM 代理程式或擴充的狀態。 請確認 hello VM 已執行的 VM 代理程式，並可建立輸出連線 tooAzure 儲存體。  |
|  VMArtifactRepositoryInternalError  |  Hello 成品儲存機制 tooretrieve VM 成品詳細資料與通訊時發生錯誤。  |
|  VMArtifactRepositoryInternalError  |  從 hello 成品儲存機制擷取 hello VM 構件資料時發生內部錯誤。  |
|  VMExtensionHandlerNonTransientError  |  處理常式 '{0}' 回報 VM 擴充 '{1}' 失敗，終端機錯誤碼為 '{2}'，錯誤訊息: '{3}  |
|  VMExtensionManagementInternalError  |  處理 VM 擴充 '{0}' 時發生內部錯誤。  |
|  VMExtensionManagementInternalError  |  準備 hello VM 擴充功能時，發生多個錯誤。 如需詳細資訊，請參閱 VM 擴充執行個體檢視。  |
|  VMExtensionProvisioningError  |  VM 回報在處理擴充 '{0}' 時失敗。 錯誤訊息: "{1}"。  |
|  VMExtensionProvisioningError  |  多個 VM 擴充功能無法 toobe hello VM 上佈建。 請 hello VM 延伸模組執行個體檢視的詳細資訊，參閱。  |
|  VMExtensionProvisioningTimeout  |  VM 擴充 '{0}' 的佈建已逾時。擴充安裝可能花太長的時間，或無法取得擴充狀態。  |
|  VMMarketplaceInvalidInput  |  從非 Marketplace 映像建立虛擬機器並不需要方案資訊，請移除 hello 要求中的 hello 計劃資訊。 作業系統磁碟名稱是 {0}。  |
|  VMMarketplaceInvalidInput  |  hello 購買資訊不符。 無法從 hello Marketplace 映像 toodeploy。 作業系統磁碟名稱是 {0}。  |
|  VMMarketplaceInvalidInput  |  從 Marketplace 映像建立虛擬機器需要 hello 要求中的計劃資訊。 作業系統磁碟名稱是 {0}。  |
|  VMNotFound  |  hello VM '{0}' 找不到。  |
|  VMRedeploymentFailed  |  VM '{0}' 重新部署失敗，因為 tooan 內部錯誤。 請稍後重試。  |
|  VMRedeploymentTimedOut  |  重新部署的 VM '{0}' 未在 hello 分配時間內完成的。 可能在後來某個時候成功完成。 否則，您可以重試 hello 要求。  |
|  VMStartTimedOut  |  VM '{0}' 未在 hello 分配時間內啟動。 hello VM 可能仍可順利啟動。 請稍後再查看 hello 電源狀態。  |


## <a name="next-steps"></a>後續步驟
如果您需要更多協助，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。
