## <a name="traffic-manager-profile"></a>流量管理員設定檔
Traffic manager，且其子 endpoint 資源可讓在 Azure 和 Azure 外部 DNS 路由 tooendpoints。 這類流量分配是由路由原則方法所管理。 Traffic manager 也可讓您監視端點健全狀況 toobe，並被導向適當的流量會根據 hello 健全狀況的端點。 

| 屬性 | 說明 |
| --- | --- |
| **trafficRoutingMethod** |可能的值為 *Performance*、*Weighted* 和 *Priority* |
| **dnsConfig** |Hello 設定檔的 FQDN |
| **通訊協定** |監視通訊協定，可能的值為 *HTTP* 和 *HTTPS* |
| **連接埠** |監視連接埠 |
| **路徑** |監視路徑 |
| **Endpoints** |端點資源的容器 |

### <a name="endpoint"></a>端點
端點是流量管理員設定檔的子資源。 它代表服務或 web 端點 toowhich 使用者流量分散根據 hello Traffic Manager 設定檔的資源中的 hello 設定原則。 

| 屬性 | 說明 |
| --- | --- |
| **類型** |hello 類型可能的值為 hello 端點的*Azure 結束點*，*外部端點*，和*巢狀的端點* |
| **targetResourceId** |服務或 Web 端點的公用 IP 位址。 這可以是 Azure 或外部端點。 |
| **重量** |用於流量管理的端點加權。 |
| **優先順序** |hello 端點，使用 toodefine 容錯移轉動作的優先順序 |

JSON 格式的流量管理員範例： 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>其他資源
如需詳細資訊，請閱讀 [流量管理員的 REST API 文件](https://msdn.microsoft.com/library/azure/mt163664.aspx) 。

