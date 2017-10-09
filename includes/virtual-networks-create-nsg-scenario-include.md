## <a name="scenario"></a>案例
toobetter 會說明如何 toocreate Nsg 這份文件會使用下面的 hello 案例。

![VNet 案例](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

在此案例中，您將建立 hello 中每個子網路 NSG **TestVNet**虛擬網路，如下所述： 

* **NSG-FrontEnd**。 hello 前端 NSG 會套用的 toohello*前端*子網路，而且包含兩個規則：    
  * **rdp-rule**。 此規則可讓 RDP 流量 toohello*前端*子網路。
  * **web-rule**。 此規則將允許 HTTP 流量 toohello*前端*子網路。
* **NSG-BackEnd**。 hello 後端 NSG 會套用的 toohello*後端*子網路，而且包含兩個規則：    
  * **sql-rule**。 此規則可讓 SQL 流量只會從 hello*前端*子網路。
  * **web-rule**。 此規則，拒絕來自 hello 所有的網際網路繫結的傳輸*後端*子網路。

hello 這些規則的組合建立 DMZ 類似案例，其中 hello 後端子網路只會接收來自 hello 前端子網路，sql 的連入流量，且具有沒有存取 toohello 網際網路時 hello 前端子網路可以與 hello 網際網路通訊，以及收到只連入 HTTP 要求。

