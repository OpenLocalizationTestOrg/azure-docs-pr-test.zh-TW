## <a name="virtual-network"></a>虛擬網路
虛擬網路 (VNET) 和子網路資源有助於定義在 Azure 中執行之工作負載的安全性範圍。 VNET 可由一組位址空間集合所界定 (此集合定義為 CIDR 區塊)。 

> [!NOTE]
> 網路管理員都熟悉 CIDR 標記法。 如果您不熟悉 CIDR，請 [深入了解](http://whatismyipaddress.com/cidr)。
> 
> 

![含有多個子網路的 VNET](./media/resource-groups-networking/Figure4.png)

Vnet 包含下列屬性的 hello。

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **addressSpace** |位址首碼 hello VNet 以 CIDR 標記法所組成的集合 |192.168.0.0/16 |
| **子網路** |組成 hello VNet 的子網路的集合 |請參閱下方的 [子網路](#Subnets) 。 |
| **ipAddress** |Tooobject 指派 IP 位址。 這是唯讀屬性。 |104.42.233.77 |

### <a name="subnets"></a>子網路
子網路是 VNET 的子資源，而且有助於使用 IP 位址首碼來定義 CIDR 區塊內位址空間的區段。 Nic 可以加入 toosubnets，並已連線的 tooVMs，提供各種工作負載的連線。

子網路包含下列屬性的 hello。 

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **addressPrefix** |Hello 子網路，以 CIDR 標記法所組成的單一位址首碼 |192.168.1.0/24 |
| **networkSecurityGroup** |NSG 套用 toohello 子網路 |請參閱 [NSG](#Network-Security-Group) |
| **routeTable** |路由表套用 toohello 子網路 |請參閱 [UDR](#Route-table) |
| **ipConfigurations** |Nic 已連線的 toohello 子網路所使用的 IP 設定物件的集合 |請參閱 [UDR](#Route-table) |

JSON 格式的範例 VNET：

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a>其他資源
* 取得 [VNET](../articles/virtual-network/virtual-networks-overview.md)的詳細資訊。
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163650.aspx)vnet。
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163618.aspx)子網路。

