---
title: "aaaCreate 具有使用 PowerShell 將多個 Nic 的 VM （傳統） |Microsoft 文件"
description: "深入了解如何 toocreate，並設定使用 PowerShell 將多個 Nic Vm。"
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>建立具有多個 NIC 的 VM (傳統)
您可以在 Azure 中建立虛擬機器 (Vm)，並附加多個網路介面 (Nic) tooeach 的 Vm。 多個 NIC 是許多網路虛擬應用裝置的需求，例如應用程式傳遞和 WAN 最佳化解決方案。 多個 NIC 也能隔離 NIC 之間的流量。

![適用於 VM 的多個 NIC](./media/virtual-networks-multiple-nics/IC757773.png)

hello 圖便會顯示具有三個 Nic VM，每個連線 tooa 不同的子網路。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議大部分的新部署使用 Resource Manager。

* Hello 「 預設 」 NIC 上才支援網際網路對向的 VIP （傳統部署） 沒有只有一個 VIP toohello IP 的 hello 預設 nic。
* 執行個體層級公用 IP (LPIP) 位址 (傳統部署) 目前不支援多個 NIC 的 VM。
* hello 的 hello Nic 順序內 hello VM 會隨機的而且也可以變更各個 Azure 基礎結構更新。 不過，hello IP 位址，而且 hello 對應的乙太網路 MAC 位址會保留 hello 相同。 例如，假設**Eth1**具有 IP 位址是 10.1.0.100 和 00-0D-3A-B0-39-0D 的 MAC 位址，則為 Azure 基礎結構更新並重新開機之後, 就無法變更太**Eth2**，但 hello IP 和 MAC 配對會保持 hello 相同。 當客戶啟動重新啟動，NIC 順序 hello 仍 hello 相同。
* hello 每個 VM 上的每個 NIC 的位址必須位於子網路、 在單一上的多個 Nic VM 可以每個指派位址 hello 相同子網路。
* hello VM 大小會決定您可以建立適用於 VM 的 NIC 的 hello 數目。 參考 hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM 大小的發行項 toodetermine 多少 NIC 支援每個 VM 的大小。 

## <a name="network-security-groups-nsgs"></a>網路安全性群組 (NSG)
在資源管理員部署中，VM 上的任何 NIC 可能會關聯至網路安全性群組 (NSG)，包括已啟用多個 NIC 功能的 VM 上的任何 NIC。 如果 NIC 指派其中 hello 子網路是與 NSG 相關聯的子網路內的位址，然後 hello hello 子網路的 NSG 中的規則也適用於 toothat nic。 在與 Nsg 加法 tooassociating 子網路，可以也 NIC 關聯 NSG。

如果子網路是 NSG 和內的 NIC 相關聯的子網路個別與 NSG 相關聯，hello 關聯 NSG 規則會套用**流程順序**根據 toohello hello 流量進入或離開傳遞方向hello NIC:

* **連入流量**其目的地是有問題的 hello NIC 流經先 hello 子網路，觸發 hello 子網路的 NSG 規則，然後再將傳入 hello NIC，然後觸發 hello NIC 的 NSG 規則。
* **連出流量**其來源為 hello 有問題的 NIC 流程從 hello NIC，觸發 hello NIC 的 NSG 規則通過 hello 的子網路，然後觸發 hello 子網路的 NSG 規則之前先出。

深入了解[網路安全性群組](virtual-networks-nsg.md)和套用方式根據關聯 toosubnets、 Vm 和 Nic...

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>如何 tooConfigure 傳統部署在多重 NIC VM
下列的 hello 指示將協助您建立多重 NIC VM 包含 3 個 Nic： 預設 NIC 和兩個其他 Nic。 hello 組態步驟將建立的 VM，將會根據 toohello 服務組態檔片段以下設定：

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


您需要下列必要條件，然後再嘗試 toorun hello hello 範例中的 PowerShell 命令的 hello。

* Azure 訂用帳戶。
* 已設定的虛擬網路。 如需 VNet 的詳細資訊，請參閱 [虛擬網路概觀](virtual-networks-overview.md) 。
* hello 最新版本的 Azure PowerShell 下載及安裝。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

toocreate 具有多個 Nic，完成下列步驟，在單一 PowerShell 工作階段中輸入每個命令的 hello 的 VM:

1. 從 Azure VM 映像庫中選取 VM 映像 請注意，映像經常變更且可依區域取得。 hello hello 下面範例中所指定的映像可能會變更或可能不會在您的地區，因此請確定您需要 toospecify hello 映像。

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. 建立 VM 組態。

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. 建立 hello 預設系統管理員身分登入。

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. 新增其他 Nic toohello VM 組態。

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. 指定 hello 預設 NIC 的 hello 子網路和 IP 位址

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. 建立虛擬網路中的 hello VM。

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > hello 您在此處指定的 VNet 必須已存在 （如 hello 必要條件中所述）。 下列的 hello 範例會指定虛擬網路，名為**MultiNIC VNet**。
    >

## <a name="limitations"></a>限制
使用多個 Nic 時，會適用下列限制的 hello:

* 具多個 NIC 的 VM 必須建立在 Azure 虛擬網路 (VNet) 中。 非 VNet 的 VM 無法設定為具有多個 NIC。
* 所有 Vm 的可用性中都設定需要 toouse，多個 Nic 或單一 nic。 在可用性設定組內無法混用多個 NIC VM 和單一 NIC VM。 雲端服務中的 VM 適用相同規則。 對於多個 NIC Vm，它們不需要 toohave hello 的 Nic 數目相同，只要它們都各自具有至少兩個。
* 一旦部署 VM 之後，如果沒有刪除後再重新建立，則無法使用多個 NIC 設定包含單一 NIC 的 VM (反之亦然)。

## <a name="secondary-nics-access-tooother-subnets"></a>次要 Nic 存取 tooother 子網路
依預設不會與預設閘道設定次要 Nic，因為 toowhich hello 流量流程在 hello 次要 Nic 會是有限的 toobe hello 內相同的子網路。 如果 hello 使用者想 tooenable 次要 Nic tootalk 自己的子網路之外，他們必須的 tooadd hello 路由表 tooconfigure hello 閘道做為中的項目如下所述。

> [!NOTE]
> 在 2015 年 7 月之前建立的 VM 可能已經為所有 NIC 設定預設閘道。 這些 Vm 生效，不會移除次要 Nic 的 hello 預設閘道。 作業系統中，使用 hello 弱式主機路由模型，例如 Linux、 如果 hello 輸入和輸出流量都使用不同的 Nic，可以中斷網際網路連線。
> 

### <a name="configure-windows-vms"></a>設定 Windows VM
假設您有包含兩個 NIC 的 Windows VM，如下所示：

* 主要 NIC IP 位址：192.168.1.4
* 次要 NIC IP 位址：192.168.2.5

此 VM 的 hello IPv4 路由表看起來會像這樣：

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

請注意該 hello 預設路由 (0.0.0.0) 是可用 toohello 主要 NIC 您將不會外 hello 次要的 hello 子網路的資源，能 tooaccess NIC，如下所示：

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

的預設路由的 tooadd hello 次要 NIC，後續 hello 步驟：

1. 從命令提示字元執行以下 hello tooidentify hello 索引編號的 hello 命令次要 NIC:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. 請注意 hello hello 資料表、 索引為 27 （在此範例中） 中的第二個項目。
3. Hello 命令提示字元中執行 hello**路由新增**命令如下所示。 在此範例中，您要為 hello hello 預設閘道指定 192.168.2.1 次要 NIC:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. tootest 連線返回 toohello 命令提示字元，並再試一次的 tooping 從不同的子網路 hello 次要 NIC 為顯示整數 eh 下面範例：
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. 您也可以檢查您的路由表 toocheck hello 新加入的路由，如下所示：
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>設定 Linux VM
適用於 Linux Vm，因為 hello 預設行為會使用弱式主機路由，我們建議您該 hello 次要 Nic tootraffic 限制流量只在 hello 內相同的子網路。 不過如果某些情況下需要 hello 子網路外部連線，使用者應該啟用原則型路由 tooensure hello 輸入，輸出流量使用 hello 相同的 nic。

## <a name="next-steps"></a>後續步驟
* 部署 [在資源管理員部署中的 2 層應用程式案例之多個 NIC VM](virtual-network-deploy-multinic-arm-template.md)。
* 部署 [在傳統部署中的 2 層應用程式案例之多個 NIC VM](virtual-network-deploy-multinic-classic-ps.md)。

