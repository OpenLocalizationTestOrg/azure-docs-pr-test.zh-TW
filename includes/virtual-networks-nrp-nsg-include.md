## <a name="network-security-group"></a>網路安全性群組
NSG 資源可 hello 建立安全性界限的工作負載，藉由實作允許和拒絕規則。 這類規則可能會套用 tooa VM、 NIC 或子網路。

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **子網路** |子網路識別碼 hello NSG 會套用至清單。 |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd |
| **securityRules** |Hello NSG 構成安全性規則的清單 |請參閱下方的 [安全性規則](#Security-rule) |
| **defaultSecurityRules** |出現在每個 NSG 中的預設安全性規則的清單 |請參閱下方的 [預設安全性規則](#Default-security-rules) |

* **安全性規則** - NSG 可以定義多個安全性規則。 每個規則都可以允許或拒絕不同類型的流量。

### <a name="security-rule"></a>安全性規則
安全性規則是 NSG 包含 hello 屬性下方的子資源。

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **description** |Hello 規則描述 |在子網路 X 中允許所有 VM 的輸入流量 |
| **protocol** |通訊協定 toomatch hello 規則 |TCP、UDP 或 * |
| **sourcePortRange** |來源連接埠範圍 toomatch hello 規則 |80, 100-200, * |
| **destinationPortRange** |目的地連接埠範圍 toomatch hello 規則 |80, 100-200, * |
| **sourceAddressPrefix** |來源位址前置詞 toomatch hello 規則 |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |目的地位址前置詞 toomatch hello 規則 |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **direction** |Hello 規則的流量 toomatch 的方向 |inbound (輸入) 或 outbound (輸出) |
| **優先順序** |Hello 規則的優先順序。 系統會依照規則優先順序檢查規則，一旦套用規則，就不會再測試規則是否符合。 |10, 100, 65000 |
| **access** |存取 tooapply 如果 hello 規則符合的型別 |allow (允許) 或 deny (拒絕) |

JSON 格式的範例 NSG：

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>預設安全性規則

預設安全性規則具有 hello 安全性規則中相同的屬性。 其存在 tooprovide 所套用的 Nsg toothem 資源之間的基本連線能力。 請確定您知道哪些[預設安全性規則](../articles/virtual-network/virtual-networks-nsg.md#default-rules)存在。

### <a name="additional-resources"></a>其他資源
* 取得 [NSG](../articles/virtual-network/virtual-networks-nsg.md)的詳細資訊。
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163615.aspx)的 Nsg。
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163580.aspx)安全性規則。
