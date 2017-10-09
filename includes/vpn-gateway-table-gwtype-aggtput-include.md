Azure 會提供下列 VPN 閘道 Sku 的 hello:

|**SKU**   | **S2S/VNet-to-VNet<br>通道** | **P2S<br>連線** | **彙總<br>輸送量基準測試** |
|---       | ---                             | ---                    | ---                         |
|**VpnGw1**| 最大 30                         | 最大 128               | 650 Mbps                    |
|**VpnGw2**| 最大 30                         | 最大 128               | 1 Gbps                      |
|**VpnGw3**| 最大 30                         | 最大 128               | 1.25 Gbps                   |
|**基本** | 最大 10                         | 最大 128               | 100 Mbps                    | 
|          |                                 |                        |                             | 

- 「彙總輸送量基準測試」是以透過單一閘道彙總之多個通道的量值為基礎。 不保證的輸送量，因為 tooInternet 流量條件和您的應用程式行為。

- 定價資訊可以在 hello 找到[定價](https://azure.microsoft.com/pricing/details/vpn-gateway)頁面。

- Hello 上可以找到 SLA （服務層級協議） 資訊[SLA](https://azure.microsoft.com/support/legal/sla/vpn-gateway/)頁面。
