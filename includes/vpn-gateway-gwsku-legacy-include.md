hello 舊版 （舊） VPN 閘道 Sku 為：

* 基本
* 標準
* 高效能

VPN 閘道不使用 hello UltraPerformance 閘道 SKU。 Hello UltraPerformance SKU 的相關資訊，請參閱 hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md)文件。

當使用 hello 舊版 Sku，請考慮下列 hello:

* 如果您想 toouse PolicyBased VPN 類型時，您必須使用 hello Basic SKU。 其他所有 SKU 均不支援原則式 VPN (先前稱為靜態路由)。
* 在 hello Basic SKU 上不支援 BGP。
* ExpressRoute VPN 閘道共存 hello Basic SKU 上不支援組態。
* 只有 hello HighPerformance SKU 上可以設定主動-主動 S2S VPN 閘道連線。
