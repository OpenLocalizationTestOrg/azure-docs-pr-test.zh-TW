

<span data-ttu-id="23bc7-101">「自訂」虛擬機器單指您使用從 **Marketplace** 取得的**熱門應用程式**所建立的虛擬機器，因為它為您做了大部分的工作。</span><span class="sxs-lookup"><span data-stu-id="23bc7-101">A *custom* virtual machine simply means a virtual machine that you create using a **Featured app** from the **Marketplace** because it does much of the work for you.</span></span> <span data-ttu-id="23bc7-102">但是，您仍然可以在組態選項中包括下列項目：</span><span class="sxs-lookup"><span data-stu-id="23bc7-102">Yet, you can still make configuration choices that include the following items:</span></span>

* <span data-ttu-id="23bc7-103">將虛擬機器連線至虛擬網路</span><span class="sxs-lookup"><span data-stu-id="23bc7-103">Connecting the virtual machine to a virtual network.</span></span>
* <span data-ttu-id="23bc7-104">安裝 Azure 虛擬機器代理程式和 Azure 虛擬機器擴充程式，例如用於反惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="23bc7-104">Installing the Azure Virtual Machine Agent and Azure Virtual Machine Extensions, such as for antimalware.</span></span>
* <span data-ttu-id="23bc7-105">將虛擬機器加入至現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="23bc7-105">Adding the virtual machine to existing cloud services.</span></span>
* <span data-ttu-id="23bc7-106">將虛擬機器加入現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="23bc7-106">Adding the virtual machine to an existing Storage account.</span></span>
* <span data-ttu-id="23bc7-107">將虛擬機器加入至可用性集合。</span><span class="sxs-lookup"><span data-stu-id="23bc7-107">Adding the virtual machine to an availability set.</span></span>

<!--
> [!IMPORTANT]
> If you want your virtual machine to use a virtual network so you can connect to it directly by host name or set up cross-premises connections, make sure that you specify the virtual network when you create the virtual machine. A virtual machine can be configured to join a virtual network only when you create the virtual machine. For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).
>
>
 -->

> [!IMPORTANT]
> <span data-ttu-id="23bc7-108">如果您想要讓虛擬機器使用虛擬網路，請務必在建立虛擬機器時指定虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23bc7-108">If you want your virtual machine to use a virtual network, make sure that you specify the virtual network when you create the virtual machine.</span></span>

> * <span data-ttu-id="23bc7-109">使用虛擬網路的兩個優點是直接連接到虛擬機器，以及設定跨單位連線。</span><span class="sxs-lookup"><span data-stu-id="23bc7-109">Two benefits of using a virtual network are connecting directly to the virtual machine and to set up cross-premises connections.</span></span>

> * <span data-ttu-id="23bc7-110">只有在建立虛擬機器時，才能將虛擬機器設定為加入虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23bc7-110">A virtual machine can be configured to join a virtual network only when you create the virtual machine.</span></span> <span data-ttu-id="23bc7-111">如需虛擬網路的詳細資訊，請參閱 [Azure 虛擬網路概觀](../articles/virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="23bc7-111">For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).</span></span>
>
>

## <a name="to-create-the-virtual-machine"></a><span data-ttu-id="23bc7-112">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="23bc7-112">To create the virtual machine</span></span>
