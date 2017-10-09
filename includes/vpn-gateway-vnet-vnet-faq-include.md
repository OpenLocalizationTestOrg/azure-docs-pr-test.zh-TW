hello VNet 對 VNet 常見問題集適用於 tooVPN 閘道連線。 如果您要尋找 VNet 對等互連，請參閱[虛擬網路對等互連](../articles/virtual-network/virtual-network-peering-overview.md)

### <a name="does-azure-charge-for-traffic-between-vnets"></a>Azure 會對 VNet 之間的流量收費嗎？

VNet 對 VNet 流量內 hello 相同區域時，兩個方向可以免費使用 VPN 閘道連線。 跨區域 VNet 對 VNet 輸出流量的收費的依據 hello 來源區域的 hello 輸出間 VNet 資料傳輸速率。 請參閱 toohello [VPN 閘道定價頁面](https://azure.microsoft.com/pricing/details/vpn-gateway/)如需詳細資訊。 如果您要連接的 Vnet 使用 VNet 對等互連，而不是 VPN 閘道，請參閱 hello[定價頁面的虛擬網路](https://azure.microsoft.com/pricing/details/virtual-network/)。

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>VNet 對 VNet 流量是否跨網際網路 hello 移動？

否。 VNet 對 VNet 流量會透過 Microsoft Azure backbone hello 網際網路 hello。

### <a name="is-vnet-to-vnet-traffic-secure"></a>VNet 對 VNet 流量是否安全？

是，它是由 IPsec/IKE 加密保護。

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>我需要 VPN 裝置 tooconnect Vnet 一起嗎？

否。 將多個 Azure 虛擬網路連接在一起並不需要 VPN 裝置，除非需要跨單位連線能力。

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>我的 Vnet 是否需要在 hello toobe 相同區域？

否。 hello 虛擬網路可位於 hello 相同或不同 Azure 區域 （位置）。

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>如果不在 hello Vnet hello 相同訂用帳戶，並訂閱 hello 需要 toobe hello 相同 AD 租用戶相關聯？

否。

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>可以使用 VNet 對 VNet 以及多站台連線嗎？

是。 虛擬網路連線能力可以與多站台 VPN 同時使用。

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>一個虛擬網路可以連接多少內部部署網站和虛擬網路？

請參閱[閘道需求](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements)表格。

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>我可以使用 VNet 對 VNet tooconnect Vm 或雲端服務之外 VNet 嗎？

否。 VNet 對 VNet 支援連接虛擬網路。 但是不支援連接不在虛擬網路中的虛擬機器或雲端服務。

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>雲端服務或負載平衡端點是否可以跨越 VNet？

否。 即使虛擬網路連接在一起，雲端服務或負載平衡端點也無法跨虛擬網路。

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>是否可以使用 PolicyBased VPN 類型進行 VNet 對 VNet 或多站台連線？

否。 VNet 對 VNet 和多站台連線需要 VPN 類型為 RouteBased (前稱為動態路由) 的 Azure VPN 閘道。

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>我可以連接 VNet 與 RouteBased VPN 類型 tooanother VNet PolicyBased VPN 類型？

否，這兩個虛擬網路必須使用路由式 (先前稱為動態路由) VPN。

### <a name="do-vpn-tunnels-share-bandwidth"></a>VPN 通道是否共用頻寬？

是。 Hello 虛擬網路的所有 VPN 通道共用 hello hello Azure VPN 閘道上的可用頻寬，並且 hello 相同 azure VPN 閘道執行時間 SLA。

### <a name="are-redundant-tunnels-supported"></a>是否支援備援通道？

當一個虛擬網路閘道設定為主動-主動時，支援成對虛擬網路之間的備援通道。

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>VNet 對 VNet 組態的位址空間是否可以重疊？

否。 您的 IP 位址範圍不能重疊。

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>在連接的虛擬網路和內部部署本機網站之間是否可以有重疊的位址空間？

否。 您的 IP 位址範圍不能重疊。



