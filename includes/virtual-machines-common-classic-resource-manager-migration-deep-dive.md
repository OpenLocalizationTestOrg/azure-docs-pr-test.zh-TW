## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>移轉的 IaaS 資源從 hello 傳統部署模型 tooResource 管理員的意義
我們向下鑽研至 hello 詳細資料之前，讓我們看看 hello hello IaaS 資源上的資料平面和管理平面作業間的差異。

* *管理/控制平面*描述 hello 呼叫 hello management/控制平面或 hello API 修改資源的因素。 例如，如建立 VM、 重新啟動 VM，及更新虛擬網路與新的子網路的作業管理 hello 執行資源。 它們不會直接影響連線 toohello 執行個體。
* *資料平面*描述 hello 的 hello 應用程式本身的執行階段 （應用程式），並與互動，並不會通過 hello Azure 應用程式開發介面的執行個體。 不論是存取您的網站，還是從執行中的 SQL Server 或 MongoDB 伺服器提取資料，皆會被視為是資料平面或應用程式互動。 從儲存體帳戶複製 blob 和存取的公用 IP 位址 tooRDP 或 SSH hello 虛擬機器也是資料平面。 這些作業會保留運算、 網路和儲存體跨執行 hello 應用程式。

Hello 幕後 hello 資料平面是 hello hello 傳統部署模型和 Resource Manager 堆疊之間的相同。 在移轉過程中，我們將轉譯 hello hello 傳統部署模型 toothat hello Resource Manager 堆疊中的 hello 資源表示法。 如此一來，您將需要 toouse 新工具、 Sdk toomanage 的 Api，您在 hello Resource Manager 堆疊中的資源。

![說明管理/控制平面與資料平面之間差異的螢幕擷取畫面](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> 在某些移轉案例，hello Azure 平台停止、 取消配置，並重新啟動您的虛擬機器。 這會造成短暫的資料平面停機時間。
>

## <a name="hello-migration-experience"></a>hello 移轉體驗
開始 hello 移轉體驗之前，建議使用 hello 下列：

* 請確定您想 toomigrate hello 資源不使用任何不支援的功能或組態。 通常 hello 平台偵測到這些問題，並會產生錯誤。
* 如果您有不在虛擬網路的 Vm 時，會停止，會為 hello 一部分準備作業已取消配置。 如果您不想 toolose hello 公用 IP 位址，查看觸發 hello 之前保留 hello IP 位址會準備作業。 不過，如果 hello Vm 虛擬網路中，它們沒有停止並取消配置。
* 規劃移轉期間，在移轉期間可能會發生任何非預期失敗的非上班時間 tooaccommodate。
* 使用 PowerShell、 命令列介面 (CLI) 命令或 REST Api toomake 輕鬆 hello 準備步驟後的驗證已完成下載 hello 目前 Vm 的設定。
* 開始 hello 移轉前，請更新自動化/實施指令碼 toohandle hello 資源管理員部署模型。 您可以選擇性地執行備妥狀態 hello hello 資源時，GET 作業。
* 評估 hello RBAC 原則設定於 hello 傳統的 IaaS 資源，並規劃 hello 移轉完成後。

如下所示為 hello 移轉工作流程

![顯示 hello 移轉工作流程的螢幕擷取畫面](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Hello 下列各節中所述的所有 hello 作業都是等冪。 如果您有不支援的功能或設定錯誤以外的問題，建議您重試 hello 準備、 中止或認可作業。 hello Azure 平台會嘗試一次 hello 動作。
>
>

### <a name="validate"></a>驗證
hello 驗證作業是 hello hello 移轉程序中的第一個步驟。 這個步驟的 hello 目標是您想 toomigrate hello 傳統部署模型中，並傳回成功/失敗，如果 hello 資源可移轉的 hello 資源 tooanalyze hello 狀態。

您選取 hello 虛擬網路或雲端服務 （如果它不是虛擬網路中），您想 toovalidate 進行移轉。

* 如果 hello 資源不支援的移轉，hello Azure 平台會列出所有 hello 原因為何不支援進行移轉。

#### <a name="checks-not-done-in-validate"></a>不在驗證中完成的檢查

驗證作業只會分析 hello hello 傳統部署模型中的 hello 資源狀態。 它可以檢查所有的失敗和不支援的案例，因為 toovarious hello 傳統部署模型中的設定。 不可能 toocheck hello Azure Resource Manager 堆疊在移轉期間，可能會在 hello 資源的所有問題。 Hello 資源進行的移轉，也就是準備 hello 下一個步驟中的轉換時，才會檢查這些問題。 hello 下表列出所有未簽入驗證的 hello 問題。


|不在驗證中的網路功能檢查|
|-|
|同時具有 ER 和 VPN 閘道的虛擬網路|
|處於中斷連線狀態的虛擬網路閘道連線|
|ER 的所有電路都已預先移轉的 tooAzure Resource Manager 堆疊|
|網路資源 (也就是靜態公用 IP、動態公用 IP、負載平衡器、網路安全性群組、路由表、網路介面) 的 Azure Resource Manager 配額檢查 |
| 檢查所有負載平衡器規則是否在整個部署/VNET 中有效 |
| 檢查是否有在 hello 的停止取消配置 Vm 之間的衝突私人 Ip 相同的 VNET |

### <a name="prepare"></a>準備
hello 準備作業是 hello hello 移轉程序中的第二個步驟。 這個步驟的 hello 目標 hello toosimulate hello 轉換傳統部署模型 tooResource Manager 資源的 IaaS 資源，而且具有這並排顯示為您 toovisualize。

> [!NOTE] 
> 傳統資源不會在此步驟期間進行修改。 因此，安全步驟 toorun 如果您想要移轉出。 

您選取 hello 虛擬網路或 hello 雲端服務 （如果它不是虛擬網路） 的 tooprepare 進行移轉。

* 如果 hello 資源不支援的移轉，hello Azure 平台就會停止 hello 移轉程序，並列出 hello 原因 hello 準備作業失敗的原因。
* Hello 資源是否能夠移轉，hello Azure 平台先鎖定 hello 管理平面 hello 資源移轉作業。 例如，您不能 tooadd 移轉資料磁碟 tooa VM。

hello Azure 平台然後 hello 移轉的中繼資料是從開始 hello 移轉資源的傳統部署模型 tooResource 管理員。

Hello 備妥後作業已完成，您可以在 hello 選擇視覺化傳統部署模型和資源管理員中的 hello 資源。 Hello 傳統部署模型中每個雲端服務，hello Azure 平台會建立資源群組名稱擁有 hello 模式`cloud-service-name>-Migrated`。

> [!NOTE]
> 不可能 tooselect hello 針對移轉的資源建立的資源群組名稱 (也就是"-移轉 」)，但完成移轉之後，您可以使用 Azure Resource Manager 移動功能 toomove 資源 tooany 您想要的資源群組。 深入了解此查看 tooread[移動資源 toonew 資源群組或訂用帳戶](../articles/resource-group-move-resources.md)

以下是在 「 準備 」 作業成功之後顯示 hello 結果的兩個畫面。 第一個畫面會顯示包含 hello 原始的雲端服務的資源群組。 第二個螢幕會顯示 hello 新"-移轉 」 包含 hello 對等的 Azure 資源管理員資源的資源群組。

![顯示入口網站傳統雲端服務的螢幕擷取畫面](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![顯示入口網站 Azure Resource Manager 資源處於準備狀態的螢幕擷取畫面](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Hello 準備階段完成之後，以下是幕後看看您的資源。 請注意，hello 資源 hello 資料平面是 hello 相同。 它被代表 hello 管理平面 （傳統部署模型） 和 hello 控制平面 （資源管理員） 中。

![準備階段中的 hello 背景](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> 在這個移轉階段中，不在傳統虛擬網路中的虛擬機器會停止並解除配置。
>

### <a name="check-manual-or-scripted"></a>檢查 (手動或透過指令碼)
在 hello 檢查步驟中，您可以選擇性地使用您下載先前 toovalidate hello 移轉看起來正確 hello 組態。 或者，您可以登入 toohello 入口網站，並特別檢查 hello 內容和資源 toovalidate 中繼資料移轉看起來不錯。

如果您移轉的是虛擬網路，則虛擬機器的大部分組態都不會重新啟動。 對於在那些 Vm 上的應用程式，您可以驗證 hello 應用程式仍會啟動並執行。

您可以測試您的自動化監控和操作指令碼 toosee 如果 hello Vm 正在如預期般，而且如果您更新的指令碼正常運作。 Hello 資源位於 hello 備妥狀態，即支援 GET 作業。

沒有任何設定時間間隔之前，您需要 toocommit hello 移轉。 您可以在此狀態停留任何長度的時間。 不過，hello 管理平面會鎖定這些資源，直到您中止或認可。

如果您發現任何問題，您就可以永遠中止 hello 移轉，並返回 toohello 傳統部署模型。 您移回之後，hello Azure 平台即會開啟 hello hello 資源管理平面作業，以便您可以繼續在 hello 傳統部署模型中的那些 Vm 上正常運作。

### <a name="abort"></a>中止
中止，則為選擇性步驟，您可以使用 toorevert 變更 toohello 傳統部署模型，並停止 hello 移轉。 此操作會刪除 hello hello 先前的準備步驟中所建立的資源的資源管理員中繼資料。 

![在 「 中止 」 階段中的 hello 背景](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> 有觸發 hello 認可作業後，無法執行這項作業。     
>

### <a name="commit"></a>認可
完成 hello 驗證之後，您就可以認可 hello 移轉。 資源不在傳統部署模型中不再顯示，且都只在 hello Resource Manager 部署模型。 hello 移轉的資源可以只 hello 新入口網站進行管理。

> [!NOTE]
> 這是一種等冪作業。 如果失敗，建議您重試 hello 作業。 如果持續 toofail，建立支援票證，或建立論壇文章 ClassicIaaSMigration 標記上我們[VM 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows)。
>
>

![在認可階段 hello 幕後](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>其中 toobegin 移轉嗎？

以下是在流程圖中會顯示如何 tooproceed 移轉

![螢幕擷取畫面顯示 hello 移轉步驟](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>傳統部署模型 tooAzure 資源管理員資源的轉譯
您可以在 hello 下表中找到 hello 傳統部署模型和資源管理員的表示法 hello 資源。 目前不支援其他功能和資源。

| 傳統表示法 | Resource Manager 表示法 | 詳細資訊 |
| --- | --- | --- |
| 雲端服務名稱 |DNS 名稱 |在移轉期間，建立一個新的資源群組的每個雲端服務與 hello 命名模式`<cloudservicename>-migrated`。 此資源群組包含您的所有資源。 hello 雲端服務名稱會變成 hello 公用 IP 位址相關聯的 DNS 名稱。 |
| 虛擬機器 |虛擬機器 |VM 特定屬性會原封不動地移轉過去。 特定的 osProfile 資訊，例如電腦名稱，不會儲存在 hello 傳統部署模型，並在移轉之後會保持空白。 |
| 磁碟資源附加 tooVM |隱含連接的磁碟 tooVM |磁碟不會模型化為 hello Resource Manager 部署模型中的最上層資源。 它們會隨著隱含 hello VM 磁碟進行移轉。 磁碟附加的 tooa 目前支援的 VM。 資源管理員 Vm 現在可以使用傳統的儲存體帳戶，可讓 hello 磁碟 toobe 簡易地移轉沒有更新。 |
| VM 擴充功能 |VM 擴充功能 |所有的 hello 資源擴充功能，除了 XML 延伸模組，會移轉從 hello 傳統部署模型。 |
| 虛擬機器憑證 |Azure 金鑰保存庫中的憑證 |如果雲端服務包含新 Azure 金鑰保存庫每個雲端服務的服務憑證，並將 hello 憑證移至 hello 金鑰保存庫。 hello Vm 是憑證更新的 tooreference hello hello 金鑰保存庫中。 <br><br> **注意：**請勿刪除 hello keyvault 因為它可能造成 hello VM toogo 進入失敗狀態。 我們正努力改善 hello 後端中的項目，如此可以安全地刪除或移動 VM tooa 新訂閱 hello 與金鑰保存庫。 |
| WinRM 組態 |osProfile 下的 WinRM 組態 |Windows 遠端管理組態會移 hello 移轉過程不變。 |
| 可用性設定組屬性 |可用性設定組資源 | 可用性設定組規格已 hello 傳統部署模型中的 hello VM 上的屬性。 可用性設定組會做為 hello 移轉一部分的最上層資源。 hello 下列不支援組態： 多個可用性設定每個雲端服務或一或多個可用性設定組以及不在任何可用性設定組中的雲端服務中的 Vm。 |
| VM 上的網路組態 |主要網路介面 |移轉之後，在 VM 上的網路組態被以 hello 主要網路介面資源。 Hello 內部 IP 位址不在虛擬網路的 Vm，在移轉期間變更。 |
| VM 上的多個網路介面 |網路介面 |如果 VM 有多個與其相關聯的網路介面，每個網路介面會變成位於最上層資源 hello Resource Manager 部署模型，以及所有 hello 屬性中的 hello 移轉的一部分。 |
| 負載平衡的端點集 |負載平衡器 |Hello 傳統部署模型，在 hello 平台會指派每個雲端服務使用隱含的負載平衡器。 移轉期間，會建立新的負載平衡器資源，而 hello 負載平衡端點集變得負載平衡器規則。 |
| 傳入的 NAT 規則 |傳入的 NAT 規則 |Hello VM 上定義的輸入的端點 hello 移轉期間，會轉換的 tooinbound hello 負載平衡器下網路位址轉譯規則。 |
| VIP 位址 |具 DNS 名稱的公用 IP 位址 |hello 虛擬 IP 位址會變成公用 IP 位址，而且與 hello 負載平衡器相關聯。 如果沒有指派 tooit 的輸入的端點只可移轉的虛擬 IP。 |
| 虛擬網路 |虛擬網路 |移轉 hello 虛擬網路，與所有內容，toohello Resource Manager 部署模型。 使用 hello 名稱建立新的資源群組`-migrated`。 |
| 保留的 IP |搭配靜態配置方法的公用 IP 位址 |Hello 負載平衡器相關聯的保留的 Ip 會移轉，以及 hello hello 雲端服務或 hello 虛擬機器的移轉。 目前不支援移轉未關聯的保留 IP。 |
| 每一個 VM 的公用 IP 位址 |搭配動態配置方法的公用 IP 位址 |hello VM 會轉換為公用的 IP 位址資源，與 hello 配置方法設定 toostatic hello 與相關聯的公用 IP 位址。 |
| NSG |NSG |子網路相關聯的網路安全性群組會複製 hello 移轉 toohello Resource Manager 部署模型的一部分。 hello 移轉期間，不會移除 hello 傳統部署模型中的 hello NSG。 不過，當 hello 移轉正在進行中時，會封鎖 hello 管理平面作業 hello NSG。 |
| DNS 伺服器 |DNS 伺服器 |DNS 伺服器相關聯的虛擬網路或 hello VM 會移轉為 hello 對應資源移轉，以及所有 hello 屬性的一部分。 |
| UDR |UDR |子網路相關聯的使用者定義路由會複製 hello 移轉 toohello Resource Manager 部署模型的一部分。 hello 移轉期間，不會移除 hello UDR hello 傳統部署模型中。 hello 移轉正在進行中時，會封鎖 hello UDR 的 hello 管理平面作業。 |
| VM 網路組態上的 IP 轉送屬性 |IP 轉送 hello NIC 上的屬性 |在 VM 上的 hello IP 轉送屬性是 hello 移轉期間的轉換的 tooa hello 網路介面上的屬性。 |
| 具有多個 IP 的負載平衡器 |具有多個公用 IP 資源的負載平衡器 |Hello 負載平衡器相關聯的每個公用 IP 是轉換的 tooa 公用 IP 資源，並在移轉之後，與 hello 負載平衡器相關聯。 |
| 在 hello VM 上的內部 DNS 名稱 |在 hello NIC 上的內部 DNS 名稱 |在移轉期間，用於 hello Vm hello 內部 DNS 尾碼 hello NIC 上名為"InternalDomainNameSuffix 」 移轉的 tooa 唯讀屬性 移轉之後 hello 尾碼維持不變，且 VM 解析應該繼續 toowork 和以前一樣。 |
| 虛擬網路閘道 |虛擬網路閘道 |不變更虛擬網路閘道內容下進行移轉。 hello 與 hello 閘道相關聯的 VIP 不會變更。 |
| 區域網路網站 |區域網路閘道 |區域網路網站的內容會呼叫本機網路閘道的不變的已移轉的 tooa 新資源。 這表示內部部署位址首碼與遠端閘道的 IP。 |
| 連線參考 |連線 |閘道和網路組態中的區域網路網站之間的連線參考在移轉之後會以資源管理員中稱為連線的新建立資源代表。 網路組態檔中的連線能力參考的所有屬性都為複製的不變的 toohello 新建立的連接資源。 在傳統的 VNet tooVNet 連線達成 toolocal 網路站台代表 hello Vnet 建立兩個 IPsec 通道。 這是轉換後的 tooVnet2Vnet 連線而不需要本機網路閘道的資源管理員模型中的型別。 |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>變更 tooyour 自動化和移轉之後的工具
移轉您的資源從 hello 傳統部署模型 toohello Resource Manager 部署模型的一部分，您會有 tooupdate 您現有的自動化或工具 tooensure 仍 toowork hello 移轉之後。
