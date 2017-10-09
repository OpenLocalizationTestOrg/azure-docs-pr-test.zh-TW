當您建立虛擬網路閘道時，您會需要 toospecify hello 閘道 SKU 的 toouse。 選取符合需求的工作負載、 輸送量、 功能和 Sla hello 類型為基礎的 hello Sku。

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>生產與開發測試工作負載

Sla 」 和 「 功能集 toohello 差異，因為我們建議您遵循 Sku 生產環境的 hello*與*開發測試：

| **工作負載**                       | **SKU**               |
| ---                                | ---                    |
| **生產、重要工作負載** | VpnGw1、VpnGw2、VpnGw3 |
| **開發測試或概念證明**   | 基本                  |
|                                    |                        |

如果您使用舊的 hello hello 生產 SKU 建議的 Sku 是標準和高效能的分散式 Sku。 如需 hello 舊 Sku，請參閱[閘道 Sku (舊版 Sku)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md)。

###  <a name="feature"></a>閘道 SKU 功能集

hello 新的閘道 Sku 簡化 hello hello 閘道所提供的功能集：

| **SKU**| **特性**|
| ---    | ---         |
|**基本**   | **路由式 VPN**：10 個通道 (含 P2S)<br><br>**原則式 VPN** (IKEv1)：1 個通道；沒有 P2S|
| **VpnGw1、VpnGw2 和 VpnGw3** | **路由式 VPN**： 向上 too30 通道 （*） P2S、 BGP，主動-主動、 自訂 IPsec/IKE 原則、 ExpressRoute 或 VPN 共存 |
|        |             |

(*)您可以設定 「 PolicyBasedTrafficSelectors"tooconnect 路由式 VPN 閘道 （VpnGw1、 VpnGw2、 VpnGw3） toomultiple 內部以原則為基礎的防火牆裝置。 請參閱太[連接 VPN 閘道 toomultiple 內部以原則為基礎的 VPN 裝置使用 PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md)如需詳細資訊。

###  <a name="resize"></a>調整閘道 SKU 的大小

1. 您可以調整 VpnGw1、VpnGw2 和 VpnGw3 SKU 之間的大小。
2. 當使用 hello 舊閘道 Sku，您可以調整之間 Basic、 Standard 和高效能的分散式 Sku。
2. 您**無法**調整大小，從基本/標準/HighPerformance Sku toohello 新 VpnGw1/VpnGw2/VpnGw3 Sku。 您必須，相反地，[移轉](#migrate)toohello 新 Sku。

###  <a name="migrate"></a>從舊的 Sku toohello 移轉新的 Sku

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
