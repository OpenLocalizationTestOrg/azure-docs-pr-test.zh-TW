Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。 hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。 Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。

您可以設定負載平衡器：

* 負載平衡連入網際網路流量 toovirtual 機器 (Vm)。 我們在此案例中為 tooa 負載平衡器[網際網路對向負載平衡器](../articles/load-balancer/load-balancer-internet-overview.md)。
* 對虛擬網路 (VNet) 中的 VM 之間、雲端服務中的 VM 之間，或內部部署電腦與跨單位虛擬網路中的 VM 之間的流量進行負載平衡。 我們在此案例中為 tooa 負載平衡器[內部負載平衡器 (ILB)](../articles/load-balancer/load-balancer-internal-overview.md)。
* 將外部流量 tooa 特定 VM 執行個體。
