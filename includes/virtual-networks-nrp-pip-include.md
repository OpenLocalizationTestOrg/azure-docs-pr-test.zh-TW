## <a name="public-ip-address"></a>公用 IP 位址
公用 IP 位址資源提供保留或動態的網際網路的 IP 位址。 雖然您可以建立為獨立物件的公用 IP 位址，您需要 tooassociate 它 tooanother 物件 tooactually 使用 hello 位址。 您可以將公用 IP 位址 tooa 負載平衡器、 應用程式閘道或 NIC tooprovide 網際網路存取 toothose 資源建立關聯。  

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **publicIPAllocationMethod** |定義 hello IP 位址是否*靜態*或*動態*。 |static、dynamic |
| **idleTimeoutInMinutes** |定義 hello 閒置逾時，預設值為 4 分鐘。 如果沒有指定工作階段的多個封包這段時間內收到，hello 工作階段已終止。 |介於 4 到 30 之間的任意值 |
| **ipAddress** |Tooobject 指派 IP 位址。 這是唯讀屬性。 |104.42.233.77 |

### <a name="dns-settings"></a>DNS 設定
公用 IP 位址具有名為的子物件**dnsSettings**包含下列屬性的 hello:

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **domainNameLabel** |用於名稱解析的主機名稱。 |www、ftp、vm1 |
| **fqdn** |Hello 公用 ip 的完整限定的名稱。 |www.westus.cloudapp.azure.com |
| **reverseFqdn** |Toohello IP 位址解析，且會註冊在 DNS PTR 記錄的完整的網域名稱。 |www.contoso.com。 |

JSON 格式的範例公用 IP 位址：

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>其他資源
* 取得 [公用 IP 位址](../articles/virtual-network/virtual-networks-reserved-public-ip.md)的詳細資訊。
* 了解 [執行個體層級公用 IP 位址](../articles/virtual-network/virtual-networks-instance-level-public-ip.md)。
* 讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163638.aspx)公用 ip 位址。

