## <a name="scenario"></a>案例
toobetter 會說明如何 toocreate UDRs 這份文件會使用下面的 hello 案例。

![影像說明](./media/virtual-network-create-udr-scenario-include/figure1.png)

在此案例中，您將建立一個 UDR hello*前端結束子網路*和另一個 UDR hello*後結束子網路*，如下所述： 

* **UDR-FrontEnd**。 hello 前端 UDR 會套用的 toohello*前端*子網路，而且包含一個路由：    
  * **RouteToBackend**。 此路由會傳送所有流量 toohello 後端子網路 toohello **FW1**虛擬機器。
* **UDR-BackEnd**。 hello 後端 UDR 將會套用的 toohello*後端*子網路，而且包含一個路由：    
  * **RouteToFrontend**。 此路由會傳送所有流量 toohello 前端子網路 toohello **FW1**虛擬機器。

hello 組合這些路由可確保從一個子網路 tooanother 為目標的所有流量將都會路由的 toohello **FW1**虛擬機器，當作虛擬應用裝置。 您也需要該 vm 上 IP 轉送 tooturn，它可以接收流量 tooensure 目的地 tooother Vm。

