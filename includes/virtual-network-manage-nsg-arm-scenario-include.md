## <a name="sample-scenario"></a>範例案例
toobetter 說明如何 toomanage Nsg 這篇文章使用下方的 hello 案例。

![VNet 案例](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

在此案例中，您將建立 hello 中每個子網路 NSG **TestVNet**虛擬網路，如下所述： 

* **NSG-FrontEnd**。 hello 前端 NSG 會套用的 toohello*前端*子網路，而且包含兩個規則：    
  * **rdp-rule**。 此規則可讓 RDP 流量 toohello*前端*子網路。
  * **web-rule**。 此規則將允許 HTTP 流量 toohello*前端*子網路。
* **NSG-BackEnd**。 hello 後端 NSG 會套用的 toohello*後端*子網路，而且包含兩個規則：    
  * **sql-rule**。 此規則可讓 SQL 流量只會從 hello*前端*子網路。
  * **web-rule**。 此規則，拒絕來自 hello 所有的網際網路繫結的傳輸*後端*子網路。

這些規則的 hello 組合建立 hello 後端子網路只會接收連入流量 SQL 流量從 hello 前端子網路，而且有沒有存取 toohello 網際網路，而 hello 前端子網路可以與 hello 通訊周邊網路類似的案例網際網路，並接收連入 HTTP 要求只。

請遵循上述步驟 toodeploy hello 案例[此連結](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG)，按一下 **部署 tooAzure**、 取代 hello 預設參數值，如有必要，並遵循 hello 入口網站中的 hello 指示。 在下面 hello 範本 hello 範例指示已使用的 toodeploy 資源群組名稱**RG NSG**。 

