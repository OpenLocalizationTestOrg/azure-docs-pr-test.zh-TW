hello 下表顯示 hello 閘道類型和 hello 估計的彙總輸送量閘道 SKU。 此表格適用於 toohello 資源管理員和傳統部署模型。 

閘道 SKU 之間的價格並不相同。 如需詳細資訊，請參閱 [VPN 閘道價格](https://azure.microsoft.com/pricing/details/vpn-gateway)。

請注意該 hello UltraPerformance 閘道 SKU 不會出現在此資料表。 Hello UltraPerformance SKU 的相關資訊，請參閱 hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md)文件。

|  | **VPN 閘道輸送量 (1)** | **VPN 閘道最大 IPsec 通道 (2)** | **ExpressRoute 閘道輸送量** | **VPN 閘道與 ExpressRoute 共存** |
| --- | --- | --- | --- | --- |
| **基本 SKU (3)(5)(6)** |100 Mbps |10 |500 Mbps (6) |否 |
| **標準 SKU (4)(5)** |100 Mbps |10 |1000 Mbps |是 |
| **高效能 SKU (4)** |200 Mbps |30 |2000 Mbps |是 |


（1) hello VPN 輸送量是 hello hello 的 Vnet 之間的度量單位為基礎的概略估計相同 Azure 區域。 不保證的跨單位連線輸送量 hello 網際網路之間。 它是 hello 可能的最大輸送量的測量。

（2) hello 的通道數量，請參閱 tooRouteBased Vpn。 原則式 VPN 只能支援一個站對站 VPN 通道。

（hello Basic SKU 不支援 BGP 3)。

(4) 此 SKU 不支援原則式 VPN。 Hello Basic SKU 僅支援它們。

(5) 此 SKU 不支援主動-主動 S2S VPN 閘道連線。 主動-主動 hello HighPerformance SKU 僅支援。

(6) 基本 SKU 已不再支援與 ExpressRoute 並用。
