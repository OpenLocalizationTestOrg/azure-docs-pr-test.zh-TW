---
title: "在 Azure 虛擬機器中新增或移除網路介面 | Microsoft Docs"
description: "了解如何在虛擬機器中新增網路介面或移除網路介面。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/15/2017
ms.author: jdial
ms.openlocfilehash: abe6abb942d206330e809f3aef388b846d7d7c7f
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="add-network-interfaces-to-or-remove-network-interfaces-from-virtual-machines"></a>新增網路介面或從虛擬機器移除網路介面

了解如何在建立 VM 時新增現有的網路介面，或在處於已停止 (已取消配置) 狀態的現有 VM 中新增或移除網路介面。 網路介面可讓 Azure 虛擬機器 (VM) 與網際網路、Azure 以及內部部署資源進行通訊。 一個 VM 可以有一或多個網路介面。 

如果您需要新增、變更或移除網路介面的 IP 位址，請閱讀[管理網路介面 IP 位址](virtual-network-network-interface-addresses.md)一文。 如果您需要建立、變更或刪除網路介面，請閱讀[管理網路介面](virtual-network-network-interface.md)一文。

## <a name="before"></a>開始之前

在完成本文任一節的任何步驟之前，請先完成下列工作︰

- 使用 Azure 帳戶來登入 Azure [入口網站](https://portal.azure.com)、Azure 命令列介面 (CLI) 或 Azure PowerShell。 如果您還沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果您使用 PowerShell 命令來完成本文中的工作，請[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 請確定您已安裝最新版的 Azure PowerShell commandlet。 若要取得 PowerShell 命令的說明 (包含範例)，請輸入 `get-help <command> -full`。 而不是安裝 Azure PowerShell，您可以使用 Azure 雲端殼層。 Azure 雲端殼層是可用的 PowerShell，您可以直接在 Azure 入口網站中執行。 它具有與您的帳戶使用預先安裝和設定的 Azure PowerShell。 若要使用雲端殼層，按一下 雲端殼層**> _**頂端的按鈕[入口網站](https://portal.azure.com)殼層視窗出現時，在左上角，選取 PowerShell。
- 如果您使用 Azure 命令列介面 (CLI) 命令來完成本文中的工作，請[安裝和設定 Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 請確定您已安裝最新版的 Azure CLI。 若要取得 CLI 命令的說明，請輸入 `az <command> --help`。 您可以不安裝 CLI 及其必要條件，而是改用 Azure Cloud Shell。 Azure Cloud Shell 是免費的 Bash Shell，您可以直接在 Azure 入口網站內執行。 它具有預先安裝和設定的 Azure CLI，可與您的帳戶搭配使用。 若要使用雲端殼層，按一下 [雲端殼層**> _**頂端的按鈕[入口網站](https://portal.azure.com)和中的選取 Bash 左上角，殼層] 視窗隨即出現。

## <a name="vm-create"></a>將現有的網路介面新增至新的 VM

當您透過入口網站建立 VM 時，入口網站會以預設設定為您建立網路介面，並將其連接至該 VM。 您無法將現有的網路介面新增至新的 VM，或使用 Azure 入口網站建立具有多個網路介面的 VM。 這兩項作業都可使用 CLI 或 PowerShell 來進行。 之前使用 PowerShell 或 CLI，但是建立與現有的網路介面的 VM，熟悉[條件約束](#constraints)。 如果您具有多個網路介面建立虛擬機器，您也必須設定正確使用它們建立 VM 之後的作業系統。 如需詳細資訊，請參閱 < 設定[Linux](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-guest-os-for-multiple-nics)或[Windows](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-guest-os-for-multiple-nics)多個網路介面。

**命令**之前建立 VM、 建立網路介面使用中的步驟[建立網路介面](virtual-network-network-interface.md#create-a-network-interface)。

|工具|命令|
|---|---|
|CLI|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>將網路介面加入至現有的 VM

1. 登入 Azure 管理入口網站。
2. 在 入口網站頂端的 搜尋 方塊中，搜尋您想要新增網路介面，VM 的名稱，或按一下瀏覽 vm**所有服務**，然後**虛擬機器**。 一旦您找到了 VM，請按一下它。 您想要新增網路介面以的 VM 必須支援您想要新增的網路介面的數目。 若要了解每個 VM 大小所支援的網路介面數目，請閱讀 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 或 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的文章。  
3. 按一下**概觀**下**設定**。 按一下**停止**，並等到**狀態**VM 的變更為*已停止 （取消配置）*。 
4. 按一下**網路**下**設定**。
5. 按一下**附加網路介面**。 從現有的網路介面目前未附加到另一個 VM 的清單中，按一下您想要附加的網路介面。 您選取的網路介面不能有加速網路啟用、 不能有 IPv6 位址指派給它，並做為虛擬網路的網路介面目前連接至 VM 中，必須位於相同虛擬網路。 如果您沒有現有的網路介面，您必須先建立一個。 若要建立網路介面，請按一下**建立網路介面**。 若要了解有關建立網路介面的詳細資訊，請參閱[建立網路介面](virtual-network-network-interface.md#create-a-network-interface)。 若要深入了解其他條件約束加入至虛擬機器的網路介面時，請參閱[條件約束](#constraints)。
6. 按一下 [SERVICEPRINCIPAL] 。
7. 按一下**概觀**下**設定**。 按一下**啟動**啟動虛擬機器。
8. 設定 VM 作業系統如何正確使用多個網路介面。 如需詳細資訊，請參閱 < 設定[Linux](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-guest-os-for-multiple-nics)或[Windows](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-guest-os-for-multiple-nics)多個網路介面。

|工具|命令|
|---|---|
|CLI|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (參考) 或[詳細步驟](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (參考) 或[詳細步驟](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a>檢視 VM 的網路介面

您可以檢視目前連接至 VM 的網路介面，以了解每個網路介面的組態，以及指派給每個網路介面的 IP 位址。 

1. 使用具備您訂用帳戶之擁有者、參與者或網路參與者角色的帳戶登入 [Azure 入口網站](https://portal.azure.com)。 若要深入了解將角色指派給帳戶的詳細資訊，請參閱 [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 Azure 入口網站頂端包含「搜尋資源」文字的方塊中，輸入「虛擬機器」。 當「虛擬機器」出現於搜尋結果時，按一下它。
3. 按一下您想要檢視的網路介面的 VM 名稱。
4. 在**設定**您選取的 vm 區段中，按一下**網路**。 若要了解網路介面設定，以及如何變更它們，請參閱[管理網路介面](virtual-network-network-interface.md)。 若要了解如何新增、變更或移除已指派給網路介面的 IP 位址，請參閱[管理 IP 位址](virtual-network-network-interface-addresses.md)。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a>從 VM 移除網路介面

1. 登入 Azure 管理入口網站。
2. 在 [入口網站頂端的 [搜尋] 方塊中，搜尋您想要移除的 VM 名稱 （中斷） 的網路介面或瀏覽]，依序按一下 vm**所有服務**，然後**虛擬機器**。 一旦您找到了 VM，請按一下它。
3. 按一下**概觀**下**設定**。 按一下**停止**，並等到**狀態**VM 的變更為*已停止 （取消配置）*。 
4. 按一下**網路**下**設定**。
5. 按一下**中斷連結網路介面**。 從目前連接至虛擬機器的網路介面的清單中，按一下您想要中斷連接的網路介面。 如果只有一個網路介面有列出，您無法卸離，因為虛擬機器必須永遠有至少一個網路介面連接到它。
6. 按一下 [SERVICEPRINCIPAL] 。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (參考) 或[詳細步驟](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (參考) 或[詳細步驟](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>後續步驟
若要建立具有多個網路介面或 IP 位址的 VM，請閱讀下列文章：

**命令**

|Task|工具|
|---|---|
|建立具有多個 NIC 的 VM|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|建立具有多個 IPv4 位址的單一 NIC VM|[CLI](virtual-network-multiple-ip-addresses-cli.md)、[PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|建立具有私人 IPv6 位址的單一 NIC VM (在 Azure Load Balancer 後端)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[Azure Resource Manager 範本](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="constraints"></a>條件約束

- VM 必須有至少一個網路介面連接到它。
- VM 只能有許多網路附加到其為 VM 大小支援的介面。 若要進一步了解有關多少的網路介面支援每個 VM 的大小，請參閱[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)和[Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小。 所有大小都支援至少兩個網路介面。
- 您在某個 VM 中新增的網路介面目前無法連接至另一個 VM。 若要了解有關建立網路介面的詳細資訊，請參閱[建立網路介面](virtual-network-network-interface.md#create-a-network-interface)。
- 在過去，網路介面僅可新增至支援多個網路介面且至少以兩個網路介面建立的 VM。 您無法將網路介面新增至使用一個網路介面建立的 VM，即使該 VM 大小支援多個網路介面也一樣。 相反地，由於以至少兩個網路介面所建立的 VM 一定要有至少兩個網路介面，因此您只能從至少具有三個網路介面的 VM 中移除網路介面。 以上這些限制已不再適用。 您現在可以使用任何數目的網路介面卡 （最多支援 VM 大小的數目） 建立 VM。
- 根據預設，第一個連接到 VM 的網路介面定義為*主要*網路介面。 VM 中的所有其他網路介面均為「次要」網路介面。
- 您可以控制哪個網路介面依預設傳送輸出流量，還是從 VM 的所有輸出流量送出指派給主要 IP 設定的主要網路介面的 IP 位址。
- 在過去，相同可用性設定組中的所有 VM 都必須具有單一或多個網路介面。 具有任意多個 (最多可達 VM 大小所支援的數目) 網路介面的 VM 現在可存在於相同的可用性設定組中。 然而，只有在建立 VM 時，才能將 VM 新增到可用性設定組。 若要深入了解可用性設定組，請閱讀[在 Azure 中管理 VM 的可用性](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy)一文。
- 雖然相同 VM 中的網路介面可以連線至 VNet 中不同的子網路，但這些網路介面全都必須連線至相同的 VNet。
- 您可以將任何主要或次要網路介面之任何 IP 組態的任何 IP 位址新增至 Azure Load Balancer 後端集區。 在過去，只能將主要網路介面的主要 IP 位址新增到後端集區。 若要深入了解 IP 位址和組態，請閱讀[新增、變更或移除 IP 位址](virtual-network-network-interface-addresses.md)一文。
- 刪除 VM 並不會刪除與其連接的網路介面。 刪除 VM 時，會中斷網路介面與該 VM 的連接。 您可以將網路介面新增至其他 VM，也可以刪除它們。
- 如果網路介面有私用的 IPv6 位址指派給它，您必須新增 （附加） 以建立 VM 時的 VM。 建立 VM 之後，您無法指派的 IPv6 位址的網路介面加入至 VM。 如果您加入指派私用的 IPv6 位址的網路介面建立虛擬機器時，您可以只加入該網路介面的虛擬機器，不論 VM 大小支援多少個網路介面。 請參閱[網路介面 IP 位址](virtual-network-network-interface-addresses.md)，進一步瞭解指派 IP 位址給網路介面。
- 類似於 IPv6，即無法加速網路建立 VM 之後，啟用與 VM 連接的網路介面。 此外，若要利用加速網路，您也必須完成 VM 作業系統內的步驟。 若要深入了解加速網路功能和其他條件約束使用時，請參閱加速的網路功能[Windows](create-vm-accelerated-networking-powershell.md)或[Linux](create-vm-accelerated-networking-cli.md)虛擬機器。
