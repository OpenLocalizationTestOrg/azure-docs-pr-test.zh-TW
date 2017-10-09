> [!div class="op_single_selector"]
> * [入口網站](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [範本](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

在 Azure 虛擬機器 (VM) 具有一個或多個網路介面 (NIC) 附加 tooit。 任何 NIC 可以有一個或多靜態或動態的公用和私用 IP 位址指派的 tooit。 指派多個 IP 位址 tooa VM 可讓 hello 下列功能：

* 在單一伺服器上，以不同 IP 位址和 SSL 憑證裝載多個網站或服務。
* 做為網路虛擬設備，例如防火牆或負載平衡器。
* hello 能力 tooadd 任何 hello 私人 IP 位址的任何 hello Nic tooan Azure 負載平衡器後端集區。 在過去只 hello hello hello 可能是主要的 NIC 的主要 IP 位址會加入 tooa 後端集區。 深入了解 toolearn tooload 平衡多個 IP 組態，如何讀取 hello[負載平衡多個 IP 組態](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。

每個連結 NIC tooa VM 有一或多個 IP 組態相關聯 tooit。 每個組態會獲派一個靜態或動態私人 IP 位址。 每個組態可能也有一個公用 IP 位址相關聯的資源 tooit。 公用 IP 位址資源都有可能是動態或靜態公用 IP 位址指派 tooit。 在 Azure 中的 toolearn 進一步了解 IP 位址，請閱讀 hello[在 Azure 中的 IP 位址](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md)發行項。 

沒有限制 toohow 許多私人 IP 位址可以指派 tooa nic。 此外，也限制 toohow 許多可用於 Azure 的訂用帳戶的公用 IP 位址。 請參閱 hello [Azure 限制](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)文件以取得詳細資料。
