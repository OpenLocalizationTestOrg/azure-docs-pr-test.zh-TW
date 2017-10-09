

Azure 基礎結構服務提供兩種負載平衡層級︰

* **DNS 層級**： 負載平衡流量 toodifferent 雲端服務位於不同的資料中心、 toodifferent Azure 網站位於不同的資料中心或 tooexternal 端點。 這是使用 Azure Traffic Manager 和 hello 循環配置資源負載平衡方法。
* **網路層級**： 負載平衡的連入網際網路流量 toodifferent 虛擬機器的雲端服務或雲端服務或虛擬網路中的虛擬機器之間流量的負載平衡。 這是與 hello Azure 負載平衡器。

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>雲端服務及網站的流量管理員負載平衡
Traffic Manager 可讓您的使用者流量 tooendpoints 可以包括雲端服務、 網站、 外部網站，以及其他流量管理員設定檔的 toocontrol hello 發佈。 流量管理員會藉由套用智慧型原則引擎 tooDomain 名稱系統 (DNS) 查詢的 hello 的網際網路資源的網域名稱。 您的雲端服務或網站可以在不同的資料中心 hello 世界各地執行。

您必須使用 REST 或 Windows PowerShell tooconfigure 外部端點或 Traffic Manager 設定檔作為端點。

Traffic Manager 會使用三種負載平衡方法 toodistribute 流量：

* **容錯移轉**： 使用這個方法，當您想 toouse 主要端點來處理所有流量，但提供備份以防主要 hello 變得無法使用。
* **效能**： 當您在不同的地理位置擁有端點，而且您想要求依據 hello 最低延遲的用戶端 toouse hello 「 最靠近 」 端點時使用這個方法。
* **循環配置資源：**使用這個方法，當您想 toodistribute 負載透過一組雲端服務的 hello 相同資料中心或跨越雲端服務或不同資料中心內的網站。

如需詳細資訊，請參閱[關於流量管理員負載平衡方法](../articles/traffic-manager/traffic-manager-routing-methods.md)。

hello 下列圖表顯示 hello 的不同雲端服務之間的流量分散至循環配置資源負載平衡方法範例。

![負載平衡](./media/virtual-machines-common-load-balance/TMSummary.png)

hello 基本程序是 hello 下列：

1. 網際網路用戶端會查詢網域名稱對應 tooa web 服務。
2. DNS 會轉送 hello 名稱查詢要求 tooTraffic 管理員。
3. Traffic Manager 在 hello 循環配置資源的清單中選擇 hello 下一個雲端服務，並傳送回 hello DNS 名稱。 hello 網際網路用戶端的 DNS 伺服器解析 hello 名稱 tooan IP 位址，並將它傳送 toohello 網際網路用戶端。
4. hello 網際網路用戶端與 hello 選擇由 Traffic Manager 的雲端服務連線。

如需詳細資訊，請參閱 [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md)。

## <a name="azure-load-balancing-for-virtual-machines"></a>虛擬機器的 Azure 負載平衡
中的虛擬機器 hello 相同雲端服務或虛擬網路可以彼此直接使用其私人 IP 位址。 電腦及服務外 hello 雲端服務或虛擬網路只能與虛擬機器中的雲端服務或虛擬網路設定的端點通訊。 端點是對應的公用 IP 位址和連接埠 toothat 私人 IP 位址和連接埠的虛擬機器或 Azure 雲端服務內的 web 角色。

隨機 hello Azure 負載平衡器會將特定類型的連入流量分散到多個虛擬機器或服務設定，稱為 負載平衡的集合中。 例如，您可以 hello 負載分散 web 要求流量的多個 web 伺服器或 web 角色。

hello 下列圖表顯示 hello 公用和私人 TCP 連接埠 80 的三部虛擬機器之間共用的標準 （未加密） 的 web 流量的負載平衡端點。 這三部虛擬機器均位在負載平衡集合中。

![負載平衡](./media/virtual-machines-common-load-balance/LoadBalancing.png)

如需詳細資訊，請參閱 [Azure 負載平衡器](../articles/load-balancer/load-balancer-overview.md)。 Hello 步驟 toocreate 一組負載平衡，請參閱[設定一組負載平衡](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md)。

Azure 也可在雲端服務或虛擬網路中進行負載平衡。 這稱為內部負載平衡，並可用於下列方式 hello:

* 在多層式應用程式 （例如，web 和資料庫層） 之間的不同層級中的伺服器之間的 tooload 達成平衡。
* tooload 平衡的特定業務 (LOB) 應用程式裝載於 Azure，而不需要額外的負載平衡器硬體或軟體。
* tooinclude 內部 hello 的一組電腦的流量進行負載平衡的伺服器。

類似 tooAzure 負載平衡，內部負載平衡是透過實現藉由設定內部負載平衡集。

hello 下列圖表顯示三個虛擬機器之間共用的跨單位虛擬網路中的企業營運 (LOB) 應用程式的內部負載平衡端點的範例。

![負載平衡](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>負載平衡器考量
預設會設定負載平衡器 tootimeout 閒置工作階段在 4 分鐘。 如果您的應用程式負載平衡器後方離開連接閒置超過 4 分鐘，而且沒有保持運作的組態，hello 連線皆會予以捨棄。 您可以變更 hello 負載平衡器行為 tooallow [Azure 負載平衡器的較長逾時設定](../articles/load-balancer/load-balancer-tcp-idle-timeout.md)。

另一個考量是 hello Azure 負載平衡器所支援的通訊模式類型。 您可以設定來源 IP 同質性 (來源 IP、目的地 IP) 或來源 IP 通訊協定 (來源 IP、目的地 IP 及通訊協定)。 如需詳細資訊，請參閱 [Azure 負載平衡器分佈模式 (來源 IP 同質性)](../articles/load-balancer/load-balancer-distribution-mode.md) 。

## <a name="next-steps"></a>後續步驟
Hello 步驟 toocreate 一組負載平衡，請參閱[設定內部負載平衡集](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md)。

如需負載平衡器的詳細資訊，請參閱 [內部負載平衡](../articles/load-balancer/load-balancer-internal-overview.md)。

