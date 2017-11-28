## <a name="scenario"></a><span data-ttu-id="bf59c-101">案例</span><span class="sxs-lookup"><span data-stu-id="bf59c-101">Scenario</span></span>
<span data-ttu-id="bf59c-102">為了更清楚說明如何建立 VNet 和子網路，本文件會使用下列案例。</span><span class="sxs-lookup"><span data-stu-id="bf59c-102">To better illustrate how to create a VNet and subnets, this document will use the scenario below.</span></span>

![VNet 案例](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="bf59c-104">在這個案例中，您將建立名為 **TestVNet** 的 VNet，並包含保留的 CIDR 區塊 **192.168.0.0./16**。</span><span class="sxs-lookup"><span data-stu-id="bf59c-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="bf59c-105">VNet 會包含下列子網路：</span><span class="sxs-lookup"><span data-stu-id="bf59c-105">Your VNet will contain the following subnets:</span></span> 

* <span data-ttu-id="bf59c-106">**FrontEnd**，使用 **192.168.1.0/24** 作為其 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="bf59c-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="bf59c-107">**BackEnd**，使用 **192.168.2.0/24** 作為其 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="bf59c-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

