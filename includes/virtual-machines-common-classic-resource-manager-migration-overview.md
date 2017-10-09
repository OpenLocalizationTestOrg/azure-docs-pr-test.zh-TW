# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>平台支援移轉從傳統 tooAzure 資源管理員的 IaaS 資源
在本文中，我們將描述我們如何啟用作為 hello 傳統 tooResource 管理員部署模型的服務 (IaaS) 資源的基礎結構。 您可以進一步了解 [Azure Resource Manager 功能和優點](../articles/azure-resource-manager/resource-group-overview.md)。 我們將詳細說明如何 tooconnect 資源從 hello 兩種部署模型，同時存在於訂用帳戶使用虛擬網路站台對站台閘道。

## <a name="goal-for-migration"></a>移轉目標
Resource Manager 除了可讓您透過範本部署複雜的應用程式之外，還可使用 VM 擴充功能來設定虛擬機器，並且納入了存取管理和標記功能。 Azure Resource Manager 還將虛擬機器的可調整、平行部署納入可用性設定組中。 hello 新部署模型也獨立提供運算、 網路和儲存體的生命週期的管理。 最後，有的焦點是根據預設，虛擬機器的虛擬網路中的 hello 強制使用啟用安全性。

Hello 傳統部署模型的幾乎所有 hello 功能都支援計算、 網路和儲存在 Azure 資源管理員。 toobenefit hello 新功能 Azure 資源管理員中，您可以移轉現有的部署從 hello 傳統部署模型。

## <a name="supported-resources-for-migration"></a>支援移轉的資源
移轉期間支援這些傳統 IaaS 資源

* 虛擬機器
* 可用性設定組 (Availability Sets)
* 雲端服務
* 儲存體帳戶
* 虛擬網路
* VPN 閘道
* 快速路由閘道_(hello 在相同訂用帳戶與虛擬網路只)_
* 網路安全性群組 
* 路由表 
* 保留的 IP 

## <a name="supported-scopes-of-migration"></a>支援的移轉範圍
有 4 個不同的方式 toocomplete 移轉運算、 網路和儲存體資源。 它們是： 

* 移轉 (不在虛擬網路中的) 虛擬機器
* 移轉 (虛擬網路中的) 虛擬機器
* 儲存體帳戶移轉
* 未連結的資源 (網路安全性群組、路由表和保留的 IP)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>移轉 (不在虛擬網路中的) 虛擬機器
在 hello Resource Manager 部署模型，安全性會強制執行您的應用程式預設。 所有 Vm 都需要 toobe hello 資源管理員模型中的虛擬網路中。 hello Azure 平台會重新啟動 (`Stop`， `Deallocate`，和`Start`) hello Vm hello 移轉的一部分。 針對 hello hello 虛擬機器的虛擬網路將移轉到，您會有兩個選項：

* 您可以要求 hello 平台 toocreate 新的虛擬網路，並將 hello 虛擬機器移轉到新的虛擬網路 hello。
* 您可以將 hello 虛擬機器移轉到現有的虛擬網路中資源管理員。

> [!NOTE]
> 在此移轉範圍內，同時 hello 管理平面作業，並針對一段時間 hello 移轉期間可能不允許 hello 資料平面作業。
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>移轉 (虛擬網路中的) 虛擬機器
對於大部分的 VM 設定，只有 hello 中繼資料 hello 傳統和資源管理員部署模型之間移轉。 hello hello 基礎 Vm 正在執行相同的硬體，在相同網路，然後與 hello 相同的 hello 儲存體。 針對一段時間 hello 移轉期間可能不允許 hello 管理平面作業。 不過，hello 資料平面會繼續 toowork。 也就是 Vm （傳統） 之上執行的應用程式不會造成停機時間 hello 移轉期間。

目前不支援 hello 的設定。 如果未來的 hello 加入支援，某些 Vm 在此設定可能會產生停機時間 （請透過 [停止]，解除配置，並重新啟動 VM 作業）。

* 您在單一雲端服務中有多個可用性設定組。
* 您在單一雲端服務中有一或多個可用性設定組，以及不在可用性設定組中的 VM。

> [!NOTE]
> 在此移轉範圍內，hello 管理平面可能不允許一段 hello 移轉期間的時間。 針對先前所述的某些組態，將會發生資料平面停機時間。
>
>

### <a name="storage-accounts-migration"></a>儲存體帳戶移轉
tooallow 順暢的移轉，您可以在傳統的儲存體帳戶中部署資源管理員 Vm。 透過這項功能，您就可以移轉計算和網路資源，且應該不受儲存體帳戶限制。 一旦移轉透過您的虛擬機器和虛擬網路，您需要 toomigrate 透過儲存體帳戶 toocomplete hello 遷移程序。

> [!NOTE]
> hello Resource Manager 部署模型沒有 hello 概念傳統映像和磁碟。 Hello 儲存體帳戶是移轉、 傳統映像和磁碟中不會顯示 hello Resource Manager 堆疊但 hello 備份 Vhd 維持不變 hello 儲存體帳戶。
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>未連結的資源 (網路安全性群組、路由表和保留的 IP)
網路安全性群組、 路由表與保留 Ip 未附加的 tooany 虛擬機器和虛擬網路都能單獨移轉。

<br>

## <a name="unsupported-features-and-configurations"></a>不支援的功能和組態
我們目前不支援某些功能和組態。 hello 下列各節說明我們的建議解決它們。

### <a name="unsupported-features"></a>不支援的功能
目前不支援下列功能的 hello。 您可以選擇性地移除這些設定，移轉 hello Vm，然後再重新啟用 hello Resource Manager 部署模型中的 hello 設定。

| 資源提供者 | 功能 | 建議 |
| --- | --- | --- |
| 計算 |未關聯的虛擬機器磁碟。 | 移轉 hello 儲存體帳戶時，將取得移轉 hello 背後這些磁碟的 VHD blob |
| 計算 |虛擬機器映像。 | 移轉 hello 儲存體帳戶時，將取得移轉 hello 背後這些磁碟的 VHD blob |
| 網路 |端點 ACL。 | 移除端點 ACL，然後重試移轉。 |
| 網路 |具有 ExpressRoute 閘道和 VPN 閘道的虛擬網路  | 在開始移轉之前移除 hello VPN 閘道，然後在移轉完成之後重新建立 hello VPN 閘道。 深入了解 [ExpressRoute 移轉](../articles/expressroute/expressroute-migration-classic-resource-manager.md)。|
| 網路 |具有授權連結的 ExpressRoute  | 移除 hello ExpressRoute 電路 toovirtaul 網路連線在開始移轉之前，並完成移轉之後，再重新建立 hello 連線。 深入了解 [ExpressRoute 移轉](../articles/expressroute/expressroute-migration-classic-resource-manager.md)。 |
| 網路 |應用程式閘道 | 在開始移轉之前移除 hello 應用程式閘道，然後重新建立 hello 應用程式閘道後，移轉即完成。 |
| 網路 |使用 VNet 對等互連的虛擬網路。 | 移轉虛擬網路 tooResource 管理員 中，然後對等。 深入了解 [VNet 對等互連](../articles/virtual-network/virtual-network-peering-overview.md)。 | 

### <a name="unsupported-configurations"></a>不支援的組態
目前不支援 hello 的設定。

| 服務 | 組態 | 建議 |
| --- | --- | --- |
| Resource Manager |傳統資源的「角色型存取控制」(RBAC) |因為在移轉後修改 hello hello 資源的 URI 時，建議您計劃移轉之後需要 toohappen hello RBAC 原則更新。 |
| 計算 |與 VM 關聯的多個子網路 |更新 hello 子網路組態 tooreference 唯一子網路。 |
| 計算 |屬於 tooa 虛擬網路，但沒有指派的明確子網路的虛擬機器 |您可以選擇性地刪除 hello VM。 |
| 計算 |具有警示、自動調整原則的虛擬機器 |hello 移轉閒內通過，並卸除這些設定。 強烈建議您不要 hello 移轉之前，評估您的環境。 或者，您可以重新設定 hello 警示設定後，移轉即完成。 |
| 計算 |XML VM 擴充功能 (BGInfo 1.*、Visual Studio Debugger、Web Deploy 及遠端偵錯) |不支援此做法。 建議您從 hello toocontinue 移轉虛擬機器中移除這些擴充功能，或它們皆會予以捨棄自動 hello 移轉程序期間。 |
| 計算 |使用進階儲存體進行開機診斷 |停用 hello Vm 的開機診斷功能，再繼續進行移轉。 Hello 移轉完成後，您可以重新啟用 hello Resource Manager 堆疊中的開機診斷。 此外，應該將用於快照和序列記錄檔的 Blob 刪除，這樣您就不再需要支付這些 Blob 的費用。 |
| 計算 |包含 Web 角色/背景工作角色的雲端服務 |目前不支援。 |
| 網路 |包含虛擬機器和 Web 角色/背景工作角色的虛擬網路 |目前不支援。 |
| Azure App Service |包含 App Service 環境的虛擬網路 |目前不支援。 |
| Azure HDInsight |包含 HDInsight 服務的虛擬網路 |目前不支援。 |
| Microsoft Dynamics 週期服務 |包含「Dynamics 週期服務」所管理之虛擬機器的虛擬網路 |目前不支援。 |
| Azure AD 網域服務 |包含 Azure AD 網域服務的虛擬網路 |目前不支援。 |
| Azure RemoteApp |包含 Azure RemoteApp 部署的虛擬網路 |目前不支援。 |
| Azure API 管理 |包含 Azure API 管理部署的虛擬網路 |目前不支援。 toomigrate hello IaaS VNET，請變更 hello hello 沒有停機時間作業 API 管理部署的 VNET。 |
| 計算 |與 VNET 搭配使用的「Azure 資訊安全中心」擴充功能，其中該 VNET 具有與內部部署 DNS 伺服器搭配使用的 VPN 閘道傳輸連線或 ExpressRoute 閘道 |Azure 資訊安全中心會自動安裝擴充功能上的虛擬機器 toomonitor 它們的安全性，並引發警示。 這些延伸通常取得自動安裝 hello Azure 資訊安全中心原則啟用 hello 訂用帳戶。 目前不支援 ExpressRoute 閘道移轉，且具有傳輸連線的 VPN 閘道會失去內部部署存取。 刪除 ExpressRoute 閘道或移轉的 VPN 閘道與傳輸連線會導致網際網路存取 tooVM 儲存體帳戶 toobe 繼續進行認可 hello 移轉時遺失。 因為無法填入 hello 客體代理程式狀態的 blob 發生此情況時，將不會繼續 hello 移轉。 建議 toodisable hello 訂用帳戶的 Azure 資訊安全中心原則過去 3 小時內，再繼續移轉。 |

