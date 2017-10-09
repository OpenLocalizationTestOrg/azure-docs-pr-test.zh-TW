您必須建立 VNet 和閘道子網路，才能進行下列工作的 hello。 請參閱 hello 文章[設定虛擬網路使用 hello 傳統入口網站](../articles/expressroute/expressroute-howto-vnet-portal-classic.md)如需詳細資訊。   

## <a name="add-a-gateway"></a>新增閘道
使用以下 toocreate 閘道 hello 命令。 是確定 toosubstitute 自己所需的任何值。

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>確認已建立 hello 閘道
已建立下列 hello 閘道的 tooverify use hello 命令。 此命令也會擷取 hello 閘道識別碼，您需要進行其他作業。

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>調整閘道器大小
有幾個 [閘道 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)。 您可以使用下列隨時命令 toochange hello 閘道 SKU 的 hello。

> [!IMPORTANT]
> 此命令不適用於 UltraPerformance 閘道。 toochange 閘道 tooan UltraPerformance 閘道，先移除現有的 ExpressRoute 閘道的 hello，然後再建立新的 UltraPerformance 閘道。 toodowngrade UltraPerformance 閘道，從您的閘道先移除 hello UltraPerformance 閘道，然後再建立新的閘道。 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>移除閘道器
使用以下 tooremove 閘道 hello 命令

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>