## <a name="scenario"></a><span data-ttu-id="d00d1-101">案例</span><span class="sxs-lookup"><span data-stu-id="d00d1-101">Scenario</span></span>
<span data-ttu-id="d00d1-102">toobetter 會說明如何 toocreate VNet 和子網路，將會使用這份文件 hello 案例下方。</span><span class="sxs-lookup"><span data-stu-id="d00d1-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![VNet 案例](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="d00d1-104">在這個案例中，您將建立名為 **TestVNet** 的 VNet，並包含保留的 CIDR 區塊 **192.168.0.0./16**。</span><span class="sxs-lookup"><span data-stu-id="d00d1-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="d00d1-105">您的 VNet 將會包含下列子網路的 hello:</span><span class="sxs-lookup"><span data-stu-id="d00d1-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="d00d1-106">**FrontEnd**，使用 **192.168.1.0/24** 作為其 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="d00d1-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="d00d1-107">**BackEnd**，使用 **192.168.2.0/24** 作為其 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="d00d1-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

