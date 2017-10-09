> [!NOTE]
> * 當移轉從舊的 SKU tooa，hello VPN 閘道的公用 IP 位址將會變更新 SKU。
> * 您無法移轉傳統 VPN 閘道 toohello 新 Sku。 傳統 VPN 閘道可以只使用 hello 傳統的 （舊） Sku。
> 

您不可以調整您的 Azure VPN 閘道之間 hello 舊的 Sku 和 hello 新 SKU 系列。 如果您有使用 hello 的 hello Sku 的舊版本的 VPN 閘道 hello Resource Manager 部署模型中，您可以移轉 toohello 新 Sku。 toomigrate，刪除虛擬網路，hello 現有的 VPN 閘道，然後建立一個新。

移轉工作流程：

1. 移除任何連線 toohello 虛擬網路閘道。
2. 刪除 hello 舊的 VPN 閘道。
3. 建立 hello 新的 VPN 閘道。
4. 更新您的內部部署 VPN 裝置 hello 新 VPN 閘道 IP 位址 （適用於站對站連線）。
5. 更新 hello toothis 閘道將會連接任何 VNet 對 VNet 區域網路閘道的閘道 IP 位址值。
6. 下載新的用戶端 VPN 組態封裝 P2S 用戶端透過此 VPN 閘道連線 toohello 虛擬網路。
7. 重新建立 hello 連線 toohello 虛擬網路閘道。
