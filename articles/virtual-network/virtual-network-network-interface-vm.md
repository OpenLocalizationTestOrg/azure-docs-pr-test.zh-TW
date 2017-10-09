---
title: "從 Azure 虛擬機器移除 aaaAdd 網路介面 tooor |Microsoft 文件"
description: "了解 tooadd 網路介面 tooor 如何從虛擬機器移除網路介面。"
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
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>新增 tooor 移除虛擬機器的網路介面

了解現有的網路介面建立 VM 時新增或移除網路介面從現有的 VM 中 hello tooadd 如何停止 （取消配置） 的狀態。 網路介面可讓您的 Azure 虛擬機器 (VM) toocommunicate 與網際網路、 Azure 和內部部署資源。 一個 VM 可以有一或多個網路介面。 

如果您需要 tooadd，變更或移除網路介面的 IP 位址讀取 hello[管理網路介面的 IP 位址](virtual-network-network-interface-addresses.md)發行項。 如果您需要 toocreate，變更或刪除網路介面，讀取 hello[管理網路介面](virtual-network-network-interface.md)發行項。

## <a name="before"></a>開始之前

這份文件的任何部分中的步驟完成 hello 之前完成任何下列工作：

- 瞭解每個 Linux 和 Windows VM 的大小支援藉由檢閱 hello 多少的網路介面的相關[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的發行項。
- 登入 toohello Azure[入口網站](https://portal.azure.com)，Azure 命令列介面 (CLI) 或 Azure PowerShell 的 Azure 帳戶。 如果您還沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果使用 PowerShell 命令在本文中 toocomplete 工作[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure PowerShell 指令程式，安裝最新版本。 tooget 說明的 PowerShell 命令，與範例中，輸入`get-help <command> -full`。
- 如果使用 Azure 命令列介面 (CLI) 命令 toocomplete 工作，在本文中[安裝及設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure CLI 安裝最新版本。 CLI 命令的 tooget 說明輸入`az <command> --help`。 而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層**> _**按鈕上方的 hello hello[入口網站](https://portal.azure.com)。

## <a name="about"></a>關於網路介面和 VM

您可以加入 （附加） 現有的網路介面 tooa VM，當您建立 VM，hello hello 網路介面目前不提供附加 tooanother VM。 您可以將網路介面，加入或移除 （中斷） 網路介面 toofrom 現有的 VM，提供 hello VM 在 hello 停止 （取消配置） 的狀態。 如果您建立使用 hello Azure 入口網站的 VM，hello 入口網站的網路介面為您建立使用預設設定。 hello 入口網站不允許您：

- 建立 hello VM 時指定現有的網路介面 tooadd
- 建立具有多個網路介面的 VM
- 指定 hello 網路介面的名稱 （hello 入口網站會以預設名稱建立 hello 網路介面）

您可以使用 Azure PowerShell 或 hello CLI toocreate 網路介面或 VM 與所有 hello 先前的屬性不能使用 hello 入口網站。 在完成之前 hello 下列各節中的 hello 工作，請考慮 hello 下列條件約束和行為：

- 所有 VM 大小至少都會支援兩個網路介面，但某些 VM 大小可支援兩個以上的網路介面。 在過去，某些 VM hello 大小只支援一個網路介面。 toolearn 多少個網路介面支援每個 VM 的大小，讀取 hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的發行項。 
- 在過去的 hello，網路介面可能只是加入的 tooVMs 支援多個網路介面，而且建立具有兩個以上的網路介面。 您無法將一個網路介面，以建立 VM 網路介面 tooa 即使 hello VM 大小支援多個網路介面。 相反地，您只可以從 VM 具有至少三個網路介面移除網路介面，因為 Vm 一律使用至少兩個網路介面建立 toohave 至少兩個網路介面。 以上這些限制已不再適用。 您可以現在建立具有任意數目的網路介面 （向上 toohello hello VM 大小所支援的數字） 的 VM 和加入或移除任何數目的網路介面 （從 Vm 在 hello 停止 （取消配置） 的狀態），只要 hello VM 永遠有至少一個網路介面。
- 根據預設，在 VM 中的 hello 第一個網路介面定義為 hello*主要*網路介面。 Hello VM 中的所有其他的網路介面*次要*網路介面。
- 主要的網路介面由 hello Azure DHCP 伺服器指派預設閘道，但不是次要網路介面。 由於系統未對次要網路介面指派預設閘道，因此根據預設，它們無法與其子網路外的資源進行通訊。 在使用它們的子網路之外的資源 Windows VM toocommunicate tooenable 次要網路介面新增路由 toohello 作業系統使用 hello`route add`從 Windows 命令列命令。 適用於 Linux Vm，因為 hello 預設行為會使用弱式主機路由，我們會建議限制次要網路介面 tooa 單一子網路的流量。 如果您需要連線 hello 子網路之外，次要網路介面，啟用以原則為基礎來路由 tooensure 該輸入和輸出流量使用 hello 相同的網路介面。
- 根據預設，所有輸出流量 hello VM 送出 hello IP 位址指派 hello 主要網路介面的 toohello 主要 IP 設定。 您可以控制在 hello VM 的作業系統，輸出流量會使用的 IP 位址，但根據預設，它是透過 hello 主要網路介面。
- 在過去 hello 內的所有 Vm 的 hello 相同可用性設定組提供了必要的 toohave 單一或多個網路介面。 具有任意數目的網路介面現在可以存在於 Vm hello 相同可用性設定組，toohello hello VM 大小所支援的數字。 您只能新增 VM tooan 可用性，但建立時設定。 深入了解可用性設定組，讀取 hello toolearn[管理的 Vm 在 Azure 中的 hello 可用性](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy)發行項。
- 雖然網路中的介面 hello 相同 VM 可能會與連接的 toodifferent VNet 中的子網路，hello 網路介面都必須連接的 toohello 相同的 VNet。
- 您可以新增任何主要或次要網路介面 tooan Azure 負載平衡器後端集區的任何 IP 組態的任何 IP 位址。 在過去的 hello，只有 hello 主要 IP 位址 hello 主要網路介面無法新增 tooa 後端集區。 深入了解 IP 位址和設定，讀取 hello toolearn[新增、 變更或移除 IP 位址](virtual-network-network-interface-addresses.md)發行項。
- 刪除 VM 不會刪除所附加的 tooit hello 網路介面。 刪除 VM 時，會中斷連接 hello VM hello 網路介面。 您可以新增 hello 網路介面 toodifferent Vm，或刪除它們。
- 如果網路介面具有私用的 IPv6 位址指派 tooit，您可以將它附加 tooa VM 建立 hello VM 時。 建立 hello VM 之後，您無法附加指定的 IPv6 位址 tooa VM 的網路介面。 如果您附加指派私用的 IPv6 位址的網路介面建立虛擬機器時，您只能再附加該網路介面 toohello 虛擬機器，不論多少 hello VM 大小所支援的網路介面。 請參閱[網路介面的 IP 位址](virtual-network-network-interface-addresses.md)toolearn 進一步了解指派的 IP 位址 toonetwork 介面。

## <a name="vm-create"></a>加入現有的網路介面 tooa 新的 VM

當您建立 VM，以透過 hello 入口網站時，hello 入口網站會使用預設設定建立網路介面，並將其為您附加 toohello VM。 您無法加入現有的網路介面 tooa 新的 VM，或具有多個網路介面使用 hello Azure 入口網站建立 VM。 您可以執行使用 hello CLI 或 PowerShell。 您可以將許多網路介面 tooa VM 為 hello 您要建立支援的 VM 大小。 深入了解多少網路 toolearn 介面讀取 hello 每個 VM 大小支援[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的發行項。 hello 新增 tooa VM 的網路介面目前無法在附加的 tooanother VM。 深入了解建立網路介面，讀取 hello toolearn[管理網路介面](virtual-network-network-interface.md#create-a-network-interface)發行項。

> [!WARNING]
> 如果網路介面具有指派 tooit 私用的 IPv6 位址，您只可以在建立 hello 虛擬機器時加入 hello 網路介面 toohello 虛擬機器。 您無法附加多個網路介面 toohello 虛擬機器時建立 hello 虛擬機器，或 hello 虛擬機器建立之後，只要將 IPv6 位址指派 tooa 網路介面附加 tooa 虛擬機器。 請參閱[網路介面的 IP 位址](virtual-network-network-interface-addresses.md)toolearn 進一步了解指派的 IP 位址 toonetwork 介面。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>加入現有的 VM 現有網路介面 tooan

您可以將許多網路介面 tooa VM 為 hello 您想要新增網路介面 toosupports 的 VM 大小。 toolearn 多少個網路介面支援每個 VM 的大小，讀取 hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的發行項。 hello VM 想的 tooadd 網路介面 toomust 支援您想 tooadd，而且必須在 hello 停止的網路介面的 hello 數目 （取消配置） 狀態。 您想要 tooadd hello 網路介面目前無法在附加的 tooanother VM。 您無法加入現有的 VM 使用 hello Azure 入口網站的網路介面 tooan。 tooadd 網路介面 tooan 現有 VM，您必須使用 hello CLI 或 PowerShell。 

> [!WARNING]
> 如果網路介面具有私用的 IPv6 位址指派 tooit，無法將它新增 tooan 現有的虛擬機器。 當您建立虛擬機器時，您只能新增指派私人 IPv6 位址 tooa 虛擬機器的網路介面。 請參閱[網路介面的 IP 位址](virtual-network-network-interface-addresses.md)toolearn 進一步了解指派的 IP 位址 toonetwork 介面。

|工具|命令|
|---|---|
|CLI|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (參考) 或[詳細步驟](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (參考) 或[詳細步驟](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a>檢視 VM 的網路介面

您可以檢視 hello 網路介面目前已連接的 tooa VM toolearn 有關每個網路介面的組態和 hello IP 位址指派 tooeach 網路介面。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 訂用帳戶的擁有者、 參與者或網路參與者角色指派的帳戶。 請參閱詳細資料指派角色 tooaccounts toolearn [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*虛擬機器*。 當**虛擬機器**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**虛擬機器**刀鋒視窗中，按一下 hello hello 想 tooview 的網路介面的 VM 名稱。
4. 在 hello**設定**區段的 hello 虛擬機器刀鋒視窗，其中會顯示 hello VM 已選取，按一下**網路介面**。 網路介面設定的相關 toolearn 以及如何 toochange 它們，請讀取的 hello[管理網路介面](virtual-network-network-interface.md)發行項。 關於新增 toolearn，變更或移除 IP 位址指派 tooa 網路介面，請參閱[管理 IP 位址](virtual-network-network-interface-addresses.md)。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a>從 VM 移除網路介面

hello VM，您想 tooremove （或卸離） 從網路介面必須在 hello 停止 （取消配置） 的狀態，而且必須目前有兩個以上的網路介面連結 tooit。 您可以移除任何網路介面，但 hello VM 必須永遠有至少一個網路介面附加 tooit。 如果您移除主要網路介面時，Azure 將指派 hello 主要屬性 toohello 網路介面已附加的 toohello VM hello 最長。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 訂用帳戶的擁有者、 參與者或網路參與者角色指派的帳戶。 請參閱詳細資料指派角色 tooaccounts toolearn [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*虛擬機器*。 當**虛擬機器**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**虛擬機器**刀鋒視窗中，按一下 hello hello 想 tooremove 的網路介面的 VM 名稱。
4. 在 hello**設定**區段的 hello 虛擬機器刀鋒視窗，其中會顯示 hello VM 已選取，按一下**網路介面**。 網路介面設定的相關 toolearn 以及如何 toochange 它們，請讀取的 hello[管理網路介面](virtual-network-network-interface.md)發行項。 關於新增 toolearn，變更或移除 IP 位址指派 tooa 網路介面，請參閱[管理 IP 位址](virtual-network-network-interface-addresses.md)。
5. 在 hello 網路介面刀鋒視窗中顯示，按一下 hello **...** toohello 右側的 toodetach hello 網路介面。
6. 按一下 [中斷連結]。 如果只有一個網路介面附加 toohello 虛擬機器，hello**卸離**選項無法使用。 按一下**是**在 hello 確認方塊中出現。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (參考) 或[詳細步驟](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (參考) 或[詳細步驟](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>接續步驟
toocreate 具有多個網路介面的 VM 或 IP 位址，請閱讀下列發行項的 hello:

**命令**

|Task|工具|
|---|---|
|建立具有多個 NIC 的 VM|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|建立具有多個 IPv4 位址的單一 NIC VM|[CLI](virtual-network-multiple-ip-addresses-cli.md)、[PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|建立具有私人 IPv6 位址的單一 NIC VM (在 Azure Load Balancer 後端)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[Azure Resource Manager 範本](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
