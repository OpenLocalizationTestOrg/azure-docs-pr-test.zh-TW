## <a name="route-tables"></a>路由表
路由表資源包含路由使用的 toodefine 流量 Azure 基礎結構中流動的方式。 您可以使用使用者定義的路由 (UDR) toosend 從給定的子網路 tooa 虛擬應用裝置，例如防火牆或入侵偵測系統 (ID) 的所有流量。 您可以將路由表 toosubnets 產生關聯。 

路由表包含下列屬性的 hello。

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **routes** |使用者的集合 hello 路由表中定義的路由 |請參閱 [使用者定義的路由](#User-defined-routes) |
| **子網路** |集合的子網路 hello 路由表太套用|請參閱 [子網路](#Subnets) |

### <a name="user-defined-routes"></a>使用者定義的路由
您可以建立 UDRs toospecify 應流量傳送到，根據其目的地位址。 您可以視為路由的 hello 預設閘道定義根據 hello 網路封包的目的地位址。

UDRs 包含下列屬性的 hello。 

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **addressPrefix** |位址首碼或完整 hello 目的地 IP 位址 |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |將太傳送裝置 hello 流量類型|VirtualAppliance, VPN Gateway, Internet |
| **nextHopIpAddress** |Hello 下一個躍點 IP 位址 |192.168.1.4 |

JSON 格式的範例路由表：

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>其他資源
* 取得 [UDR](../articles/virtual-network/virtual-networks-udr-overview.md)的詳細資訊。
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt502549.aspx)的路由表。
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt502539.aspx)對於使用者定義的路由 (UDRs)。

