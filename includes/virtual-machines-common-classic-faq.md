


本文中的使用者詢問有關 Azure 虛擬機器建立 hello 傳統部署模型的一些常見問題的解答。

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>可以移轉我的 VM hello 傳統部署模型 toohello 新模型中建立資源管理員嗎？
是。 如需有關指示 toomigrate，請參閱：

* [從傳統 tooAzure 使用 Azure PowerShell 的資源管理員移轉](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md)。
* [從傳統 tooAzure 資源管理員使用 Azure CLI 移轉](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)。

## <a name="what-can-i-run-on-an-azure-vm"></a>我可以在 Azure VM 上執行什麼？
所有的訂閱者都可以在 Azure 虛擬機器上執行伺服器軟體。 您可以執行最新版本的 Windows Server，以及各種 Linux 散發套件。 如需支援的詳細資料，請參閱：

• 針對 Windows VM -- [Azure 虛擬機器的 Microsoft 伺服器軟體支援](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• 針對 Linux VM -- [Azure 背書之散發套件上的 Linux](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Windows 用戶端映像，Windows 7 和 Windows 8.1 的特定版本的可用 tooMSDN Azure 權益訂閱者和 MSDN 開發和測試隨用隨付 」 訂閱者開發和測試工作。 如需詳細資訊 (包括指示和限制)，請參閱 [MSDN 訂閱者的 Windows 用戶端映像](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/)。

## <a name="why-are-affinity-groups-being-deprecated"></a>為何同質群組遭到取代？
同質群組是舊的概念，可依地理位置將 Azure 內的客戶雲端服務部署和儲存體帳戶進行分組。 它們原本提供了在 hello 早期的 Azure 網路設計 tooimprove VM 的 VM 網路的效能。 它們也支援 hello 初始版本的虛擬網路 (Vnet)，這是 tooa 有限的一組小型區域中的硬體。

hello 目前 Azure 的網路區域內的設計，因此不再需要同質群組。 虛擬網路也在區域範圍內，因此使用虛擬網路時不再需要同質群組。 Toothese 增強功能，因為我們不再建議客戶使用同質群組，因為它們可以限制在某些情況下。 使用同質群組不必要地之間建立關聯，以限制 hello 選擇是使用 tooyou 的 VM 大小的 Vm toospecific 硬體。 當您嘗試的 tooadd 新的 Vm 與 hello 同質群組相關聯的 hello 特定的硬體是否接近容量時，它也可能會導致 toocapacity 相關的錯誤。

同質群組是已過時的功能在於 hello Azure Resource Manager 部署模型和 hello Azure 入口網站。 Hello 傳統的 Azure 入口網站中，我們正在淘汰建立同質群組，並建立已釘選的 tooan 同質群組的儲存體資源的支援。 您不需要 toomodify 的現有雲端服務使用同質群組。 不過，除非 Azure 支援專家建議使用同質群組，否則您不應該使用新雲端服務的同質群組。

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>我可以使用多少的儲存體搭配虛擬機器？
每個資料磁碟可以是 up too1 TB。 您可以使用的資料磁碟的 hello 數目取決於 hello hello 虛擬機器大小。 如需詳細資訊，請參閱 [虛擬機器的大小](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

Azure 儲存體帳戶提供 hello 作業系統磁碟和任何資料磁碟的儲存體。 每個磁碟是以分頁 Blob 方式儲存的 .vhd 檔案。 如需定價的詳細資料，請參閱 [儲存體定價詳細資料](http://go.microsoft.com/fwlink/p/?LinkId=396819)。

## <a name="which-virtual-hard-disk-types-can-i-use"></a>可以使用哪些虛擬硬碟類型？
Azure 僅支援固定的 VHD 格式虛擬硬碟。 如果您有想要在 Azure 中的 toouse VHDX 時，您需要 toofirst 轉換使用 HYPER-V 管理員或 hello [CONVERT-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet。 這麼做之後，使用[Add-azurevhd](https://msdn.microsoft.com/library/azure/dn495173.aspx)指令程式 （在服務管理模式） tooupload hello VHD tooa 儲存體帳戶，所以您可以使用虛擬機器的 Azure 中。

* 如需 Linux 指示，請參閱[建立及上傳的虛擬硬碟包含 hello Linux Operating System](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。
* 如需 Windows 指示，請參閱[建立並上傳 Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>是這些虛擬機器 hello 與 HYPER-V 虛擬機器相同嗎？
在許多方面它們是類似的太 「 第 1 代 」 HYPER-V Vm，但它們是不完全 hello 相同。 這兩種類型提供虛擬的硬體，而 hello VHD 格式虛擬硬碟相容。 這表示您可以在 Hyper-V 和 Azure 之間移動它們。 有時讓 Hyper-V 使用者感到驚訝的三個主要差異為：

* Azure 不提供主控台存取 tooa 虛擬機器。 沒有任何方式 tooaccess VM 直到它完成開機。
* 多數[大小](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)的 Azure VM 僅有 1 個虛擬網路介面卡，這表示它們也可能會有 1 個外部 IP 位址。 （hello A8 和 A9 大小使用第二個網路介面卡進行有限的案例中的執行個體之間的應用程式通訊）。
* Azure VM 不支援第 2 代 Hyper-V VM 功能。 如需這些功能的詳細資料，請參閱[Hyper-V 的虛擬機器規格](http://technet.microsoft.com/library/dn592184.aspx)以及[第 2 代虛擬機器概觀](https://technet.microsoft.com/library/dn282285.aspx)。

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>這些虛擬機器可以使用我現有的內部部署網路基礎結構嗎？
Hello 傳統部署模型中建立的虛擬機器，您可以使用 Azure 虛擬網路 tooextend 現有基礎結構。 hello 方法就像是設定分公司。 您可以佈建在 Azure 中管理虛擬私人網路 (Vpn) 以及安全地將它們連接 tooon 內部部署 IT 基礎結構。 如需詳細資訊，請參閱 [虛擬網路概觀](../articles/virtual-network/virtual-networks-overview.md)。

您必須要 hello 建立 hello 虛擬機器的虛擬機器 toobelong toowhen 的 toospecify hello 網路。 您無法加入現有的虛擬機器 tooa 虛擬網路。 不過，您可以卸離 hello 虛擬硬碟 (VHD) 從現有虛擬機器 hello，暫時解決這個問題，然後使用它 toocreate 新的虛擬機器與您想要的 hello 網路設定。

## <a name="how-can-i-access--my-virtual-machine"></a>如何存取我的虛擬機器？
您需要 tooestablish toohello 虛擬機器上的遠端連線 toolog 透過遠端桌面連線的 Windows VM 或安全殼層 (SSH)，針對 Linux VM。 如需相關指示，請參閱：

* [如何 tooa 執行 Windows Server 的虛擬機器上的 tooLog](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 支援最多 2 個並行連接，除非 hello 伺服器設定為遠端桌面服務工作階段主機。  
* [如何在 tooa 執行 Linux 虛擬機器上的 tooLog](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 根據預設，SSH 允許最多 10 個並行連線。 您可以增加這個數字藉由編輯 hello 設定檔。

如果您有遠端桌面或 SSH 的問題，安裝並使用 hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)延伸 toohelp 修正 hello 問題。

對於 Windows VM，其他選項包括：

* 在 hello Azure 傳統入口網站，找出 hello VM，然後按一下 **重設遠端存取**hello 命令列。
* 檢閱[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 使用 Windows PowerShell 遠端執行功能 tooconnect toohello VM，或建立其他資源 tooconnect toohello VM 的其他端點。 如需詳細資訊，請參閱[如何 tooSet 端點 tooa 虛擬機器](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

如果您熟悉 HYPER-V，您可能會尋找工具類似 tooVMConnect。 Azure 不提供類似的工具，因為不支援主控台存取 tooa 虛擬機器。

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>可以使用 hello 暫存磁碟 (hello 適用於 Windows 的 d： 磁碟機或 /dev/sdb1 適用於 Linux) toostore 資料嗎？
您不應該使用 hello 暫存磁碟 (d： 磁碟機預設適用於 Windows 或 linux /dev/sdb1 hello) toostore 資料。 它們僅提供暫存空間，因此您會有遺失資料且無法復原的風險。 發生這個問題 hello 虛擬機器會移動 tooa 不同的主機。 調整虛擬機器的大小，更新 hello 主機或硬體失敗 hello 主機上的是一些虛擬機器可能移動的 hello 原因。

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>如何變更 hello hello 暫存磁碟的磁碟機代號？
Windows 虛擬機器，您可以變更 hello 所移動的 hello 分頁檔的磁碟機代號和重新指派磁碟機代號，但您將需要 toomake 確定您執行 hello 以特定順序的步驟。 如需指示，請參閱[hello Windows 暫存磁碟的變更 hello 磁碟機代號](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>如何 hello 客體作業系統升級？
hello 詞彙升級通常是指移動 tooa 多個最新版的作業系統，但 hello 仍使用相同的硬體。 Azure Vm 的 hello 程序來移動 tooa 較新版本的 Linux 和 Windows 有所不同：

* 適用於 Linux Vm 使用 hello 封裝管理工具和程序適用於 hello 發佈。
* Windows 虛擬機器，您必須使用 「 類似 Windows Server 移轉工具 hello toomigrate hello 伺服器。 位於 Azure 時，不要嘗試 tooupgrade hello 客體作業系統。 它不是因為 hello 風險遺失存取 toohello 虛擬機器的支援。 如果在 hello 升級期間發生問題，您可能會失去 hello 能力 toostart 遠端桌面工作階段並不是能 tootroubleshoot hello 問題。

如需 hello 工具和程序移轉 Windows Server 的一般詳細資訊，請參閱[角色和功能移轉 tooWindows 伺服器](http://go.microsoft.com/fwlink/p/?LinkId=396940)。

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>什麼是 hello 預設使用者名稱和 hello 虛擬機器上的密碼？
hello Azure 所提供的映像沒有預先設定的使用者名稱和密碼。 當您建立使用其中一個這些映像的虛擬機器時，您將需要 tooprovide 使用者名稱和密碼，您將使用 toolog toohello 虛擬機器上的。

如果您忘記 hello 使用者名稱或密碼，並已安裝 hello VM 代理程式，您可以安裝並使用 hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)延伸 toofix hello 問題。

其他詳細資料：

* Hello Linux 映像，如果您使用 hello Azure 傳統入口網站，'azureuser' 指定為預設的使用者名稱，但您可以變更這個選項做為 hello 方式 toocreate hello 虛擬機器使用 「 從組件庫 ' 而不是 [快速建立]。 使用 ' 位於 從組件庫 」 也可讓您決定是否 toouse 密碼、 SSH 金鑰或這兩個 toolog 中。 hello 使用者帳戶是具有 'sudo' 存取權的非特殊權限使用者 toorun 特殊權限的命令。 hello 'root' 帳戶已停用。
* 針對 Windows 映像，您將需要 tooprovide 使用者名稱和密碼建立 hello VM。 hello 帳戶會新增 toohello Administrators 群組。

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>Azure 可以在我的虛擬機器上執行防毒軟體嗎？
Azure 提供針對防毒解決方案的幾個選項，但它已啟動 tooyou toomanage 它。 例如，您可能需要不同的訂用帳戶的反惡意程式碼軟體，且 toorun 掃描並安裝更新時，您將需要 toodecide。 當您建立 Windows 虛擬機器或在稍後的時間點，可以使用適用於 Microsoft Antimalware、Symantec Endpoint Protection，或 TrendMicro Deep Security 代理程式的 VM 延伸模組，新增防毒軟體支援。 hello Symantec 和 TrendMicro 延伸模組可讓您使用免費的限時試用訂閱或現有的企業訂閱。 Microsoft Antimalware 則是免費的。 如需詳細資訊，請參閱：

* [如何 tooinstall 及設定 Azure VM 上的 Symantec Endpoint Protection](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [如何 tooinstall 和設定 Trend Micro Deep Security 作為 Azure VM 上的服務](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [在 Azure 虛擬機器上部署反惡意程式碼解決方案](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>備份和復原有哪些選擇？
Azure 備份在特定地區以預覽版提供。 如需詳細資訊，請參閱 [備份 Azure 虛擬機器](../articles/backup/backup-azure-vms.md)。 來自認證合作夥伴的其他解決方案也可供使用。 toofind 解目前可用，搜尋 hello Azure Marketplace。

其他選項為 blob 儲存體 toouse hello 快照集功能。 toodo，您將需要 tooshut hello VM blob 快照集所依賴的任何作業之前關閉。 這會儲存擱置資料寫入，並置於一致的狀態中的 hello 檔案系統。

## <a name="how-does-azure-charge-for-my-vm"></a>Azure 如何對我的 VM 收費？
Azure 計費根據 hello VM 的大小和作業系統以每小時價格。 部分的時數，Azure 只費用使用 hello 分鐘。 如果您建立 hello VM 的 VM 映像包含某些預先安裝的軟體，可能會套用額外的每小時軟體費用。 Azure 的 hello VM 的作業系統和資料磁碟的儲存體分別費用。 暫存磁碟儲存體是免費的。

您需要付費 hello VM 狀態為執行中或已停止，而停止 hello VM 狀態時，不會向時 （取消配置）。 tooput hello 中的 VM 已停止 （取消配置） 」 狀態，請執行 hello 下列其中一項：

* 關閉或刪除 hello Azure 傳統入口網站中的 hello VM。
* 使用 hello Stop-azurevm cmdlet，用於 hello Azure PowerShell 模組。
* 在 hello 服務管理 REST API 中使用 hello 將角色關機作業和 hello PostShutdownAction 元素指定為 StoppedDeallocated。

如需更多詳細資料，請參閱 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)。

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>Azure 會因為維護重新啟動我的 VM 嗎？
Azure 有時候中重新啟動 VM 的定期、 計劃性的維護更新 hello Azure 資料中心。

當 Azure 偵測到嚴重的硬體問題可能會影響您的 VM 時，會發生非計劃性維護事件。 對於非計劃的事件，Azure 會自動移轉 hello VM tooa 狀況良好的主機與 hello VM 重新啟動。

針對任何獨立 VM （表示 hello VM 不屬於可用性設定組），Azure 會告知 hello 訂用帳戶的服務系統管理員透過電子郵件計劃性維護的前至少一週因為 hello Vm hello 更新期間可能會重新啟動。 Hello Vm 上執行的應用程式可能會導致停機時間。

由於 tooplanned 維護發生 hello 重新開機時，您也可以使用 hello Azure 傳統入口網站或 Azure PowerShell tooview hello 重新開機記錄。 如需詳細資訊，請參閱 [檢視 VM 重新啟動記錄檔](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/)。

tooprovide 備援性，將兩個或更同樣 hello 中設定 Vm 相同可用性設定組。 這有助於確保在計劃性或非計劃性的維護期間，至少有一個 VM 仍可使用。 Azure 保證此組態的 VM 可用性特定層級。 如需詳細資訊，請參閱[管理虛擬機器可用性 hello](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="additional-resources"></a>其他資源
[關於 Azure 虛擬機器](../articles/virtual-machines/virtual-machines-linux-about.md)

[建立和管理 Linux Vm 與 hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[使用 Azure PowerShell 建立和管理 Windows VM](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

