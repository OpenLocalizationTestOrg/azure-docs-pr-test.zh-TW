## <a name="nic"></a>NIC
網路介面卡 (NIC) 資源會提供網路連線 tooan 現有的子網路中的 VNet 的資源。 雖然您可以建立為獨立物件的 NIC，您需要 tooassociate 它 tooanother 物件 tooactually 提供連線能力。 NIC 可以是使用的 tooconnect，VM tooa 子網路、 公用 IP 位址或在負載平衡器。  

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **virtualMachine** |VM hello NIC 相關聯。 |/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |Hello NIC 的 MAC 位址 |介於 4 到 30 之間的任意值 |
| **networkSecurityGroup** |NSG 相關聯 toohello NIC |/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |Hello NIC 的 DNS 設定 |請參閱 [PIP](#Public-IP-address) |

網路介面卡或 NIC，表示相關聯的 tooa 虛擬機器 (VM) 網路介面。 一個 VM 可以有一或多個 NIC。

![單一 VM 上的 NIC](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>IP 組態
Nic 已命名的子物件**ipConfigurations**包含下列屬性的 hello:

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **subnet** |子網路 hello NIC 是連接到。 |/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1 |
| **privateIPAddress** |Hello 子網路中的 hello NIC 的 IP 位址 |10.0.0.8 |
| **privateIPAllocationMethod** |IP 配置方法 |動態或靜態 |
| **enableIPForwarding** |Hello NIC 是否可以使用的路由 |True 或 False |
| **primary** |Hello NIC 是否 hello 主要的 NIC，供 hello VM |True 或 False |
| **publicIPAddress** |Hello NIC 相關聯的 PIP |請參閱 [DNS 設定](#DNS-settings) |
| **loadBalancerBackendAddressPools** |後端位址集區 hello NIC 是與相關聯 | |
| **loadBalancerInboundNatRules** |輸入 NIC 是與相關聯的負載平衡器 NAT 規則 hello | |

JSON 格式的範例公用 IP 位址：

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>其他資源
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163579.aspx)nic。

