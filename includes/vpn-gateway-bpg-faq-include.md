### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>所有的 Azure VPN 閘道 SKU 上是否都支援 BGP？
否，在 Azure **標準**和**HighPerformance** VPN 閘道上才支援 BGP。 **基本** SKU。

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>可以使用 BGP 與 Azure Policy-Based VPN 閘道嗎？
否，僅路由 VPN 閘道支援 BGP。

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>可以使用私人 ASN (自發系統編號) 嗎？
是，針對您的內部部署網路和 Azure 虛擬網路，您可以使用您自己的公用 ASN 或私人 ASN。

### <a name="are-there-asns-reserved-by-azure"></a>是否有 Azure 所保留的 ASN 嗎？
是，hello 下列 Asn Azure 會保留內部和外部的對等互連的：

* 公用 ASN：8075、8076、12076
* 私人 ASN：65515、65517、65518、65519、65520

連接 tooAzure VPN 閘道時，您無法在內部部署 VPN 裝置的指定這些 Asn。

### <a name="are-there-any-other-asns-that-i-cant-use"></a>有我不能使用的任何其他 ASN 嗎？
是，下列的 Asn hello 都[由 IANA 保留](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml)且無法在 Azure VPN 閘道上設定：

23456、64496-64511、65535-65551 和 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>我可以使用 hello 相同的 ASN 兩個內部部署 VPN 網路和 Azure Vnet 嗎？
否，如果您要將內部部署網路和 Azure VNet 與 BGP 連接，必須在內部部署網路與 Azure VNet 之間指派不同 ASN。 Azure VPN 閘道已將預設 ASN 指派為 65515 (無論跨單位連線是否啟用 BGP)。 您可以藉由建立 hello VPN 閘道時，指派不同的 ASN 覆寫此預設或建立 hello 閘道之後，變更 hello ASN。 您將需要 tooassign 您在內部部署的 Asn toohello 對應 Azure 本機網路閘道。

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>哪些位址前置詞將 Azure VPN 閘道通告 toome？
Azure VPN 閘道將通告下列路由 tooyour 內部 BGP 裝置 hello:

* 您的 VNet 位址首碼
* 每個本機網路閘道連線的 toohello Azure VPN 閘道的位址首碼
* 從其他 BGP 對等互連工作階段連線的 toohello Azure VPN 閘道，學習的路由**除了預設路由與重疊任何 VNet 前置詞**。

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>我可以公告預設路由 (0.0.0.0/0) tooAzure VPN 閘道嗎？
是。

請注意這會強制所有 VNet 輸出流量接近您在內部部署站台，並會防止 hello VNet Vm 接受來自 hello 網際網路直接管理，這類的 RDP 或 SSH hello 網際網路 toohello Vm 從公用通訊。

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>可以為我的虛擬網路首碼公告 hello 確切的前置詞？

否，廣告 hello 相同的前置詞與虛擬網路的位址前置詞的任何一個將會封鎖，或篩選的 hello Azure 平台。 不過，您可以公告一個前置詞，也就是您在虛擬網路內已有的超集。 

比方說，如果您的虛擬網路使用 hello 位址空間 10.0.0.0/16，您可以公告 10.0.0.0/8。 但您無法公告 10.0.0.0/16 或 10.0.0.0/24。

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>可以與我的 VNet 對 VNet 連線搭配使用 BGP 嗎？
是，您可以針對跨單位連線和 VNet 對 VNet 連線使用 BGP。

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>可以針對我的 Azure VPN 閘道混合使用 BGP 和非 BGP 連線嗎？
是，您可以混合這兩個 BGP，非 BGP 的連線 hello 相同 Azure VPN 閘道。

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>Azure VPN 閘道是否支援 BGP 傳輸路由？
是，BGP 傳輸路由支援，與 Azure VPN 閘道將 hello 例外狀況**不**通告預設路由 tooother BGP 對等體。 tooenable 傳輸路由跨多個 Azure VPN 閘道，您必須啟用 BGP 的所有中繼 VNet 對 VNet 連線。

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>是否可在 Azure VPN 閘道與我的內部部署網路之間擁有多個通道？
是，您可在 Azure VPN 閘道與內部部署網路之間建立多個 S2S VPN 通道。 請注意，所有這些通道將會計算針對 hello 總數的 Azure VPN 閘道的通道，您必須在這兩個通道上啟用 BGP。

例如，如果您有兩個備援通道 Azure VPN 閘道與內部部署網路之間，它們會耗用 hello Azure VPN 閘道 (10 standard) 和高效能的分散式 30 」 總配額超出 2 通道。

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>可以在兩個具有 BGP 的 Azure VNet 之間擁有多個通道嗎？
主動-主動組態中必須是，但至少一個 hello 虛擬網路閘道。

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>我可以在 ExpressRoute/S2S VPN 共存組態中使用適用於 S2S VPN 的 BGP 嗎？
是。 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Azure VPN 閘道會對 BGP 對等互連 IP 使用什麼位址？
hello Azure VPN 閘道將單一 IP 位址配置 hello GatewaySubnet 範圍為 hello 虛擬網路定義。 根據預設，它是 hello 第二個最後一個位址 hello 範圍。 例如，如果您 GatewaySubnet 10.12.255.0/27，範圍從 10.12.255.0 too10.12.255.31，hello hello Azure VPN 閘道的 BGP 對等 IP 位址將會是 10.12.255.30。 當您列出 hello Azure VPN 閘道資訊時，您可以找到這項資訊。

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>VPN 裝置上的 hello BGP 對等 IP 位址的 hello 需求為何？
您在內部部署的 BGP 對等地址**不得**是為 hello 公用 IP 位址的 VPN 裝置 hello 相同。 為 BGP 對等 IP，hello VPN 裝置上使用不同的 IP 位址。 它可以是指派 toohello 回送介面 hello 裝置上的位址。 指定此位址在 hello 對應本機網路閘道代表 hello 位置。

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>功能應該指定為我 hello 本機網路閘道的位址前置詞使用 BGP 時？
Azure 的區域網路閘道 hello 初始位址為指定前置詞 hello 與內部網路。 Bgp，您必須配置 hello 主機首碼 （/ 32 的前置詞） 的 BGP 對等 IP 位址為 hello 在內部部署網路的位址空間。 如果您的 BGP 對等 IP 10.52.255.254，您應該指定 「 10.52.255.254/32"hello localNetworkAddressSpace 為 hello 表示此為內部網路的區域網路閘道。 這是 tooensure 的 hello Azure VPN 閘道建立 hello BGP 工作階段，透過 hello S2S VPN 通道。

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>功能應該加入 toomy 在內部部署 VPN 裝置 hello BGP 對等互連工作階段嗎？
您應該加入 hello Azure BGP 對等 IP 位址的主機路由指向 toohello IPsec S2S VPN 通道 VPN 裝置上。 比方說，如果"10.12.255.30"hello Azure VPN 對等 IP，您應該將"10.12.255.30"hello 相對應的 IPsec 通道 interface 的下一個躍點介面的主機路由 VPN 裝置上。

