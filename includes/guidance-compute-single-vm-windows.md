本文概述了一組經過證實的作法，在 Azure 上執行 Windows 虛擬機器 (VM)、 支付注意 tooscalability、 可用性、 管理性和安全性。

> [!NOTE]
> Azure 有兩個不同的部署模型：[Azure Resource Manager][resource-manager-overview] 和傳統。 本文使用 Microsoft 建議用於新部署的資源管理員。
>
>

我們不建議用使用單一 VM 進行關鍵任務工作負載，因為它會建立單一失敗點。 若要擁有較高的可用性，您必須在[可用性設定組][availability-set]中部署多個 VM。 如需詳細資訊，請參閱[在 Azure 上執行多個 VM][multi-vm]。

## <a name="architecture-diagram"></a>架構圖表

佈建 Azure 中的 VM，牽涉到零件越比只 hello VM 本身。 有計算、網路及儲存體元素。

> 包含此架構圖表的 Visio 文件是否可供下載從 hello [Microsoft 下載中心][visio-download]。 此圖表是 hello 」 計算的單一 VM 」 的頁面。
>
>

![[0]][0]

* **資源群組。** [*資源群組*][resource-manager-overview]是保存相關資源的容器。 為此 VM 建立資源群組 toohold hello 資源。
* **VM**。 您可以佈建 VM，從已發行的映像清單，或從虛擬硬碟 (VHD) 檔案上傳 tooAzure Blob 儲存體。
* **作業系統磁碟。** hello OS 磁碟是儲存在 VHD [Azure 儲存體][azure-storage]。 也就是說，它會保存即使 hello 主機電腦效能降低。
* **暫存磁碟。** hello 建立 VM 時使用的暫存磁碟 (hello `D:` Windows 上的磁碟機)。 這個磁碟儲存在 hello 主機電腦上的實體磁碟機上。 不會  儲存在 Azure 儲存體中，而且可能在重新開機期間和其他 VM 生命週期事件中刪除。 僅將此磁碟使用於暫存資料，例如分頁檔或交換檔。
* **資料磁碟。** [資料磁碟][data-disk]是用於應用程式資料的持續性 VHD。 資料磁碟儲存在 Azure 儲存體，hello OS 磁碟相同。
* **虛擬網路 (VNet) 和子網路。** 在 Azure 中的每個 VM 都會部署到 VNet 中，而虛擬網路會進一步分成數個子網路。
* **公用 IP 位址。** 公用 IP 位址是以 hello VM 需要的 toocommunicate&mdash;例如透過遠端桌面 (RDP)。
* **網路介面 (NIC)**。 hello NIC 可讓您將 VM toocommunicate hello 與 hello 虛擬網路。
* **網路安全性群組 (NSG)**。 hello [NSG] [ nsg]是使用 tooallow/拒絕的網路流量 toohello 子網路。 您可以將 NSG 與獨立的 NIC 或子網路關聯。 如果您將它與子網路，hello NSG 規則適用於 tooall Vm 子網路中。
* **診斷。** 診斷記錄而言十分重要的管理和疑難排解 hello VM。

## <a name="recommendations"></a>建議

在大部分情況下，套用遵循建議的 hello。 除非您有特定的需求會覆寫它們，否則請遵循下列建議。

### <a name="vm-recommendations"></a>VM 建議

Azure 提供許多不同的虛擬機器大小，但我們建議您 hello DS-與 GS 系列，因為這些機器大小支援[高階儲存體][premium-storage]。 選取其中一個機器大小，除非您有高效能運算等特殊工作負載。 如需詳細資訊，請參閱[虛擬機器的大小][virtual-machine-sizes]。

如果您要移動現有的工作負載 tooAzure，開頭是 hello 最接近的相符項目 tooyour 的 hello VM 大小上的內部部署伺服器。 量值與實際工作負載 hello 效能尊重 tooCPU、 記憶體和磁碟輸入/輸出作業每秒 (IOPS)，然後視需要調整 hello 大小。 如果您需要多個 Nic vm，請注意 hello 的 Nic 數目上限是函式的 hello [VM 大小][vm-size-tables]。   

當您佈建 hello VM 和其他資源時，您必須指定區域。 一般而言，最接近 tooyour 內部使用者選擇地區或客戶。 不過，並非所有 VM 大小在所有區域都可供使用。 如需詳細資訊，請參閱[依區域提供的服務][services-by-region]。 toosee hello VM 大小清單提供在給定的區域中，執行下列 Azure 命令列介面 (CLI) 命令的 hello:

```
azure vm sizes --location <location>
```

如需選擇已發佈 VM 映像的相關資訊，請參閱[在 Azure 中使用 Powershell 或 CLI 瀏覽並選取 Windows 虛擬機器映像][select-vm-image]。

### <a name="disk-and-storage-recommendations"></a>磁碟和儲存體建議

為了達到最佳的磁碟 I/O 效能，我們建議使用[進階儲存體][premium-storage]，這會將資料儲存在固態硬碟 (SSD)。 成本根據 hello hello 佈建的磁碟大小。 IOPS 和輸送量也取決於磁碟大小，因此當您佈建磁碟時，請考慮以下三個因素 (容量、IOPS 和輸送量)。

建立順序 tooavoid 達到 hello IOPS 限制儲存體帳戶中的每個 VM toohold hello 虛擬硬碟 (Vhd) 的個別 Azure 儲存體帳戶。

新增一或多個資料磁碟。 當您建立新的 VHD 時，它仍未格式化。 登入 hello VM tooformat hello 磁碟。 如果您有大量的資料磁碟，請留意 hello 總 I/O 限制 hello 儲存體帳戶。 如需詳細資訊，請參閱[虛擬機器磁碟限制][vm-disk-limits]。

如果可能的話，安裝應用程式資料的磁碟，而非 hello OS 磁碟上。 不過，有些舊版應用程式可能需要 tooinstall hello c： 磁碟機上的元件。 您可以在此情況下，[調整 hello OS 磁碟][ resize-os-disk]使用 PowerShell。

為了達到最佳效能，請建立個別的儲存體帳戶 toohold 診斷記錄檔。 標準本地備援儲存體 (LRS) 帳戶已足以保存診斷記錄。

### <a name="network-recommendations"></a>網路建議

hello 公用 IP 位址可以是動態或靜態。 hello 預設值為動態。

* 保留[靜態 IP 位址][ static-ip]如果您需要將不會變更的固定的 IP 位址&mdash;比方說，如果您需要 toocreate A 記錄在 DNS 中，或需要 hello IP 位址 toobe 加入的 tooa 安全清單。
* 您也可以建立 hello IP 位址的完整的網域名稱 (FQDN)。 您可以註冊[CNAME 記錄][ cname-record]點 toohello FQDN 的 DNS 中。 如需詳細資訊，請參閱[hello Azure 入口網站中建立的完整的網域名稱][fqdn]。

所有 NSG 都包含一組[預設規則][nsg-default-rules]，包括一個封鎖所有網際網路輸入流量的規則。 無法刪除 hello 預設規則，但其他規則覆寫它們。 tooenable 網際網路流量建立規則以允許輸入的流量 toospecific 連接埠&mdash;，例如 HTTP 連接埠 80。  

tooenable RDP，加入允許輸入的流量 tooTCP 連接埠 3389 的 NSG 規則。

## <a name="scalability-considerations"></a>延展性考量

您可以藉由調整 VM 向上或向下[hello VM 大小變更](../articles/virtual-machines/windows/sizes.md)。 tooscale out 水平，會將兩個或多個 Vm 放入的可用性設定組負載平衡器後方。 如需詳細資訊，請參閱[在 Azure 上執行多個 VM 以獲得延展性和可用性][multi-vm]。

## <a name="availability-considerations"></a>可用性考量

若要擁有較高的可用性，您必須在可用性設定組中部署多個 VM。 這也會提供較高的[服務等級協定][vm-sla] (SLA)。

您的 VM 可能會受到[計劃性維護][planned-maintenance]或[非計劃性維護][manage-vm-availability]影響。 您可以使用[VM 重新啟動記錄][ reboot-logs] toodetermine 是否重新啟動 VM 因計劃性維護。

VHD 是儲存在 [Azure 儲存體][azure-storage]，而系統會複寫 Azure 儲存體來提供持久性和可用性。

tooprotect 資料意外遺失 （例如，由於使用者錯誤） 的正常作業期間，您應該實作使用的時間點備份[blob 快照集][ blob-snapshot]或其他工具。

## <a name="manageability-considerations"></a>管理性考量

**資源群組。** Put 緊密結合的資源的相同生命週期到該共用 hello hello 相同[資源群組][resource-manager-overview]。 資源群組讓您 toodeploy 和監視資源做為群組，以及彙總計費資源群組的成本。 您也可以刪除整組資源，這對於測試部署非常有用。 為資源提供有意義的名稱。 可讓您更輕鬆 toolocate 特定資源，並了解其角色。 請參閱 [Azure 資源的建議命名慣例][naming conventions]。

**VM 診斷。** 啟用監視和診斷，包括基本健全狀況度量、診斷基礎結構記錄檔及[開機診斷][boot-diagnostics]。 如果您的 VM 進入無法開機的狀態，開機診斷能協助您診斷開機失敗。 如需詳細資訊，請參閱[啟用監視和診斷][enable-monitoring]。 使用 hello [Azure 記錄檔收集][ log-collector]延伸 toocollect Azure 平台的記錄，並上傳 tooAzure 儲存體。   

hello 下列 CLI 命令啟用診斷：

```
azure vm enable-diag <resource-group> <vm-name>
```

**停止 VM。** Azure 會區分「已停止」和「已解除配置」狀態。 Hello VM 狀態已停止，但 hello VM 會取消配置時，不會向您收取費用。

使用下列 CLI 命令 toodeallocate VM hello:

```
azure vm deallocate <resource-group> <vm-name>
```

在 hello Azure 入口網站，hello**停止**按鈕取消配置 hello VM。 不過，如果您關閉透過 hello OS 登入時，hello VM 已停止，但*不*取消配置，因此仍將須付費。

**刪除 VM。** 如果您刪除 VM，不會刪除 hello Vhd。 這表示您可以安全地刪除 hello VM 而不會遺失資料。 不過，您仍需支付儲存體費用。 toodelete hello VHD，刪除從 hello 檔案[Blob 儲存體][blob-storage]。

tooprevent 被意外刪除，使用[資源鎖定][ resource-lock] toolock hello 整個資源群組或鎖定個別資源，例如 hello VM。

## <a name="security-considerations"></a>安全性考量

使用[Azure 資訊安全中心][ security-center] tooget hello 安全性狀態，您的 Azure 資源的中央檢視。 資訊安全中心監視潛在的安全性問題，並提供全方位的部署的 hello 安全性健全狀況。 資訊安全中心是依每個 Azure 訂用帳戶設定。 按照 [使用資訊安全中心]所述來啟用安全資料收集。 啟用資料收集時，資訊安全性中心就會自動掃描任何該訂用帳戶建立的 VM。

**修補程式管理。** 如果啟用，資訊安全性中心會檢查是否遺失安全性或重要更新。 使用[群組原則設定][ group-policy] hello VM tooenable 自動系統更新。

**反惡意程式碼。** 如果啟用，資訊安全性中心會檢查是已安裝反惡意程式碼軟體。 您也可以使用資訊安全中心 tooinstall 反惡意程式碼軟體從內部 hello Azure 入口網站。

**作業。** 使用[角色型存取控制][ rbac] (RBAC) toocontrol 存取 toohello Azure 部署的資源。 RBAC 可讓您指派授權角色 toomembers DevOps 小組。 例如，hello 讀取器角色可以檢視 Azure 資源，但不是建立、 管理或刪除它們。 有些角色是特定 tooparticular Azure 資源類型。 比方說，hello 虛擬機器參與者角色可以重新啟動或取消配置 VM、 hello 系統管理員密碼重設、 建立新的 VM，等等。 其他對此參考架構可能有用的[內建 RBAC 角色][rbac-roles]包括 [DevTest Lab 使用者][rbac-devtest]和[網路參與者][rbac-network]。 Toomultiple 角色可以指派使用者，而且您可以建立更多更細緻權限的自訂角色。

> [!NOTE]
> RBAC 不會限制 hello 登入 VM 的使用者可以執行的動作。 這些權限取決於 hello hello 客體作業系統上的帳戶類型。   
>
>

tooreset hello 本機系統管理員密碼執行 hello `vm reset-access` Azure CLI 命令。

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

使用[稽核記錄檔][ audit-logs] toosee 佈建設定的動作和其他 VM 的事件。

**資料加密。** 請考慮[Azure 磁碟加密][ disk-encryption]如果您需要 tooencrypt hello OS 和資料磁碟。

## <a name="solution-deployment"></a>解決方案部署

此參考架構的部署可在 [GitHub][github-folder] 上取得。 它包含 VNet、NSG 及單一 VM。 toodeploy hello 架構，請遵循下列步驟：

1. 以滑鼠右鍵按一下下方的 hello 按鈕，然後選取任一個 「 開啟連結新索引標籤 」 或 「 在新視窗中的開啟連結。 」  
   [![部署 tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. 一旦 hello 連結已開啟 hello Azure 入口網站中，您必須針對一些 hello 設定輸入值：

   * hello**資源群組**hello 參數檔案，因此選取中已經定義名稱**新建**輸入`ra-single-vm-rg`hello 文字方塊中。
   * 選取 hello 區域從 hello**位置**下拉式方塊。
   * 請勿編輯 hello**範本根 Uri**或 hello**參數根 Uri**文字方塊。
   * 選取**windows**在 hello **Os 類型**下拉式方塊。
   * 檢閱 hello 條款和條件，然後按一下 hello **toohello 條款和條件前面所述，即表示我同意**核取方塊。
   * 按一下 hello**購買** 按鈕。
3. 等候 hello 部署 toocomplete。
4. hello 參數檔案包含硬式編碼的系統管理員使用者名稱和密碼，並強烈建議您立即變更兩者。 按一下 hello 名為 VM `ra-single-vm0 `hello Azure 入口網站中。 然後按一下 上**重設密碼**在 hello**支援 + 疑難排解**刀鋒視窗。 選取**重設密碼**在 hello**模式**下拉式清單方塊中，然後選取新**使用者名**和**密碼**。 按一下 hello**更新**按鈕 toopersist hello 新的使用者名稱和密碼。

如需其他方式 toodeploy 此參考架構，請參閱 hello 讀我檔案中 hello[指引單一 vm][github-folder]] GitHub 資料夾。

## <a name="customize-hello-deployment"></a>自訂 hello 部署
如果您需要 toochange hello 部署 toomatch 您的需求，請遵循 hello 中的 hello 指示[讀我檔案][github-folder]。

## <a name="next-steps"></a>後續步驟
如需較高的可用性，請在負載平衡器後面部署兩個以上的 VM。 如需詳細資訊，請參閱[在 Azure 上執行多個 VM][multi-vm]。

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[使用資訊安全中心]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Azure 中的單一 Windows VM 架構"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
