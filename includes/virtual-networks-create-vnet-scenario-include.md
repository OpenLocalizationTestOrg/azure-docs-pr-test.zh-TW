## <a name="scenario"></a>案例
toobetter 會說明如何 toocreate VNet 和子網路，將會使用這份文件 hello 案例下方。

![VNet 案例](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

在這個案例中，您將建立名為 **TestVNet** 的 VNet，並包含保留的 CIDR 區塊 **192.168.0.0./16**。 您的 VNet 將會包含下列子網路的 hello: 

* **FrontEnd**，使用 **192.168.1.0/24** 作為其 CIDR 區塊。
* **BackEnd**，使用 **192.168.2.0/24** 作為其 CIDR 區塊。

