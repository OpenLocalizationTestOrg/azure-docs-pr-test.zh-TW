<span data-ttu-id="6f4a4-101">Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-101">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="6f4a4-102">hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-102">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="6f4a4-103">Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-103">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

<span data-ttu-id="6f4a4-104">您可以設定負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="6f4a4-104">You can configure a load balancer to:</span></span>

* <span data-ttu-id="6f4a4-105">負載平衡連入網際網路流量 toovirtual 機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-105">Load balance incoming Internet traffic toovirtual machines (VMs).</span></span> <span data-ttu-id="6f4a4-106">我們在此案例中為 tooa 負載平衡器[網際網路對向負載平衡器](../articles/load-balancer/load-balancer-internet-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-106">We refer tooa load balancer in this scenario as an [Internet-facing load balancer](../articles/load-balancer/load-balancer-internet-overview.md).</span></span>
* <span data-ttu-id="6f4a4-107">對虛擬網路 (VNet) 中的 VM 之間、雲端服務中的 VM 之間，或內部部署電腦與跨單位虛擬網路中的 VM 之間的流量進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-107">Load balance traffic between VMs in a virtual network (VNet), between VMs in cloud services, or between on-premises computers and VMs in a cross-premises virtual network.</span></span> <span data-ttu-id="6f4a4-108">我們在此案例中為 tooa 負載平衡器[內部負載平衡器 (ILB)](../articles/load-balancer/load-balancer-internal-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-108">We refer tooa load balancer in this scenario as an [internal load balancer (ILB)](../articles/load-balancer/load-balancer-internal-overview.md).</span></span>
* <span data-ttu-id="6f4a4-109">將外部流量 tooa 特定 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="6f4a4-109">Forward external traffic tooa specific VM instance.</span></span>