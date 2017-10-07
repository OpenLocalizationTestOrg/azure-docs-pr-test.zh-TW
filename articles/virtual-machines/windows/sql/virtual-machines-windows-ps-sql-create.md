---
title: "在 Azure PowerShell （資源管理員） 中的 SQL Server 虛擬機器 aaaCreate |Microsoft 文件"
description: "提供使用 SQL Server 虛擬機器資源庫映像建立 Azure VM 的步驟和 PowerShell 指令碼。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>使用 Azure PowerShell 佈建 SQL Server 虛擬機器 (Resource Manager)
> [!div class="op_single_selector"]
> * [入口網站](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>概觀
本教學課程告訴您如何 toocreate 單一 Azure 虛擬機器使用 hello **Azure Resource Manager**部署模型，使用 Azure PowerShell cmdlet。 在此教學課程中，我們將建立單一的虛擬機器在 hello SQL 組件庫中使用單一磁碟機從映像。 我們將建立新的提供者的 hello 儲存體、 網路和 hello 虛擬機器將使用的計算資源。 如果上述任何資源有現有的提供者，您可以改用這些提供者。

如果您需要 hello 傳統本主題的版本，請參閱[佈建 SQL Server 虛擬機器使用 Azure PowerShell 傳統](../classic/ps-sql-create.md)。

## <a name="prerequisites"></a>必要條件
本教學課程中，您將需要：

* 在開始之前，您需要有 Azure 帳戶和訂用帳戶。 如果您沒有帳戶，請註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* [Azure PowerShell)](/powershell/azure/overview)，最低版本 1.4.0 或更新版本 (本教學課程是以 1.5.0 版撰寫)。
  * tooretrieve 程式版本中，輸入**Azure Get-module-ListAvailable**。

## <a name="configure-your-subscription"></a>設定您的訂用帳戶
開啟 Windows PowerShell 並執行下列 cmdlet 的 hello 建立存取 tooyour Azure 帳戶。 您會有登入畫面 tooenter 您的認證。 使用 hello 相同電子郵件和密碼，您會使用 toosign toohello Azure 入口網站中。

    Add-AzureRmAccount

已成功登入之後您會看到一些資訊，其中包含您登入的 hello SubscriptionId 螢幕上。 這是 hello 訂用帳戶中的 hello 本教學課程會建立資源除非您變更 tooa 不同訂用帳戶。 如果您有多個訂用帳戶，執行下列 cmdlet tooreturn hello 所有您訂用帳戶的清單：

    Get-AzureRmSubscription

執行下列 cmdlet 與您想要的訂用帳戶 Id 的 hello toochange tooanother SubscriptionID、。

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>定義映像變數
toosimplify 可用性與了解從本教學課程中的 hello 完成指令碼，我們一開始會定義變數的數目。 當您，但修改提供的 hello 值時，請注意命名的限制相關的 tooname 長度和特殊字元，請變更 hello 參數值。

### <a name="location-and-resource-group"></a>位置和資源群組
使用兩個變數 toodefine hello 資料區域和 hello 資源群組到其中您將建立 hello hello 虛擬機器的其他資源。

請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>儲存體屬性
使用下列變數 toodefine hello 儲存體帳戶和 hello 型別 hello 虛擬機器所使用的儲存體 toobe hello。

請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。 請注意，在此範例中，我們使用 [進階儲存體](../../../storage/common/storage-premium-storage.md)，這是針對生產環境工作負載建議使用的儲存體。 如需有關本指南及其他建議的詳細資料，請參閱 [Azure 虛擬機器中的 SQL Server 效能最佳做法](virtual-machines-windows-sql-performance.md)。

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>網路屬性
使用下列變數 toodefine hello 網路介面、 hello TCP/IP 配置方法，hello 虛擬網路名稱、 hello 虛擬子網路名稱、 hello 虛擬網路的 hello 範圍的 IP 位址、 hello 的 IP 位址範圍的 hello 子網路和 hello hello公用網域名稱標籤 toobe hello 虛擬機器中的 hello 網路所使用。

請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>虛擬機器屬性
使用下列變數 toodefine hello 虛擬機器名稱、 hello 電腦名稱、 hello 虛擬機器大小和 hello hello 虛擬機器的作業系統磁碟名稱的 hello。

請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>映像屬性
使用下列變數 toodefine hello hello 虛擬機器的映像 toouse hello。 在此範例中，會使用 hello SQL Server 2016 Enterprise 映像。

請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

請注意，您可以取得 SQL Server 映像供應項目與 hello Get AzureRmVMImageOffer 命令的完整清單：

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

而且您可以看見 hello Sku 供 hello Get AzureRmVMImageSku 命令的供應項目。 hello 下列命令會顯示所有 Sku 供 hello **SQL2014SP1 WS2012R2**提供。

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>建立資源群組
Hello Resource Manager 部署模型，與 hello 您所建立的第一個物件是 hello 資源群組。 我們將使用 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate Azure 資源群組和其資源與 hello 資源群組名稱與先前初始化的 hello 變數所定義的位置。

執行下列 cmdlet toocreate hello 您新資源群組。

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>建立儲存體帳戶
hello 虛擬機器需要存放裝置資源 hello 作業系統磁碟和 hello SQL Server 資料和記錄檔。 為了簡單起見，我們將針對兩者建立單一磁碟。 您可以附加額外的磁碟，稍後再使用 hello[新增 Azure 磁碟](/powershell/module/azure/add-azuredisk)中的 cmdlet 順序 tooplace SQL Server 資料和專用磁碟上記錄檔。 我們將使用 hello[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate 標準儲存體帳戶中新的資源群組和 hello 儲存體帳戶名稱、 儲存體 Sku 名稱，與使用 hello 變數定義的位置，您先前初始化。

執行下列 cmdlet toocreate hello 新的儲存體帳戶。

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>建立網路資源
hello 虛擬機器需要的網路連線的網路資源數目。

* 每部虛擬機器都需要虛擬網路。
* 虛擬網路必須定義至少一個子網路。
* 網路介面必須以公用或私人 IP 位址定義。

### <a name="create-a-virtual-network-subnet-configuration"></a>建立虛擬網路子網路組態
我們首先會建立虛擬網路的子網路組態。 教學課程中，我們將建立預設子網路使用 hello[新增 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet。 我們將建立虛擬網路子網路組態設定與 hello 子網路名稱和位址定義的前置詞使用您先前初始化的 hello 變數。

> [!NOTE]
> 您可以定義使用這個指令程式，hello 虛擬網路子網路組態的其他屬性，但這超出本教學課程的 hello 範圍。
>
>

執行下列 cmdlet toocreate hello 虛擬子網路組態。

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>建立虛擬網路
接下來，我們將建立虛擬網路使用 hello[新增 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet。 新資源群組，以 hello 名稱、 位置和位址定義的前置詞使用 hello 先前初始化的變數，以及使用 hello 在 hello 上一個步驟中所定義的子網路組態中，我們將建立虛擬網路。

執行下列 cmdlet toocreate hello 虛擬網路。

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>建立 hello 公用 IP 位址
現在我們有虛擬網路定義，我們需要 tooconfigure IP 位址連線 toohello 虛擬機器。 此教學課程中，我們將建立使用動態 IP 位址 toosupport 網際網路連線的公用 IP 位址。 我們將使用 hello[新增 AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello 公用 IP 位址以 hello 資源群組建立先前和 hello 名稱、 位置、 配置方法，以及使用 hello 定義 DNS 網域名稱標籤您先前初始化的變數。

> [!NOTE]
> 您可以定義 hello 使用這個指令程式，公用 IP 位址的其他屬性，但這超出本教學課程中初始 hello 範圍。 您也可以建立私用位址，且具有靜態位址，但其同時也是本教學課程的 hello 範圍之外。
>
>

執行下列 cmdlet toocreate hello 公用 IP 位址。

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>建立 hello 網路介面
我們現在是我們的虛擬機器將使用的準備 toocreate hello 網路介面。 我們將使用 hello[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate 先前定義我們稍早建立的 hello 資源群組，並使用 hello 名稱、 位置、 子網路和公用 IP 位址的網路介面。

執行下列 cmdlet toocreate hello 您的網路介面。

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>設定 VM 物件
現在，我們已經定義的儲存體和網路資源，我們會準備 toodefine hello 虛擬機器計算資源。 教學課程中，我們會指定 hello 虛擬機器大小和各種作業系統屬性指定 hello 先前建立的網路介面，定義 blob 儲存體，，然後指定 hello 作業系統磁碟。

### <a name="create-hello-vm-object"></a>建立 hello VM 物件
我們一開始會指定 hello 虛擬機器大小。 在本教學課程諸ㄥ，我們會指定 DS13。 我們將使用 hello[新增 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate hello 名稱與使用您先前初始化的 hello 變數定義的大小可設定的虛擬機器物件。

執行下列 cmdlet toocreate hello 虛擬機器物件的 hello。

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>建立認證物件 toohold hello 名稱與 hello 本機系統管理員認證的密碼
我們可以設定 hello hello 虛擬機器的作業系統內容之前，我們需要 toosupply hello 認證 hello 本機系統管理員帳戶為安全字串。 tooaccomplish，我們將使用 hello [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet。

執行下列 cmdlet 的 hello 和 hello Windows PowerShell 認證要求在視窗中，輸入 hello hello hello Windows 虛擬機器中的本機系統管理員帳戶的名稱和密碼 toouse。

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>設定 hello hello 虛擬機器的作業系統屬性
現在我們已經準備好 tooset hello 虛擬機器的作業系統內容。 我們將使用 hello[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem)作業系統為 Windows，cmdlet tooset hello 類型需要 hello[虛擬機器代理程式](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)toobe 安裝，可讓您指定 hello 指令程式可讓自動更新並設定 hello 虛擬機器名稱、 hello 電腦名稱及使用您先前初始化的 hello 變數 hello 認證。

執行下列 cmdlet tooset hello 作業系統屬性為您的虛擬機器的 hello。

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>新增 hello 網路介面 toohello 虛擬機器
接下來，我們將加入 hello 我們先前建立 toohello 虛擬機器的網路介面。 我們將使用 hello[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello 網路介面使用您先前定義的 hello 網路介面變數。

執行下列 cmdlet tooset hello 之虛擬機器的網路介面的 hello。

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>設定 hello hello 磁碟 toobe hello 虛擬機器所使用的 blob 儲存體位置
接下來，我們會設定為使用您先前定義的 hello 變數 hello 虛擬機器所使用的 hello 磁碟 toobe hello blob 儲存體位置。

執行下列 cmdlet tooset hello blob 儲存體位置的 hello。

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>設定 hello 作業系統 hello 虛擬機器的磁碟內容
接下來，我們會設定 hello 作業系統磁碟屬性 hello 虛擬機器。 我們將使用 hello[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify hello hello 虛擬機器的作業系統，將來自映像時，快取只 tooread tooset (因為 hello 上安裝 SQL Server 相同的磁碟)，並定義hello 虛擬機器名稱和 hello 作業系統磁碟使用 hello 我們先前定義的變數定義。

執行下列 cmdlet tooset hello 作業系統磁碟屬性為您的虛擬機器的 hello。

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>指定 hello hello 虛擬機器的平台映像
我們最後的組態步驟是我們的虛擬機器的 toospecify hello 平台映像。 教學課程中，我們使用 hello 最新的 SQL Server 2016 CTP 映像。 我們將使用 hello[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse 先前定義的 hello 變數所定義，此映像。

執行下列 cmdlet toospecify hello 平台映像的虛擬機器的 hello。

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>建立 hello SQL VM
現在完成 hello 組態步驟後，您就準備好 toocreate hello 虛擬機器。 我們將使用 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello 虛擬機器使用，我們已定義的 hello 變數。

執行下列 cmdlet toocreate hello 您的虛擬機器。

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

建立 hello 虛擬機器。 請注意，標準儲存體帳戶已建立的開機診斷，因為 hello 指定 hello 虛擬機器的磁碟儲存體帳戶是進階儲存體帳戶。

您現在可以檢視此機器在 hello Azure 入口網站 toosee[公用 IP 位址和其完整的網域名稱](virtual-machines-windows-portal-sql-server-provision.md)。

## <a name="example-script"></a>範例指令碼
hello 下列指令碼包含 hello 完整的 PowerShell 指令碼在此教學課程。 它會假設您已經安裝 hello Azure 訂用帳戶 toouse 以 hello**新增 AzureRmAccount**和**選取 AzureRmSubscription**命令。

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>後續步驟
建立 hello 虛擬機器之後，您就準備好 tooconnect toohello 虛擬機器使用 RDP 和安裝程式的連線能力。 如需詳細資訊，請參閱[連接 tooa Azure （資源管理員） 上的 SQL Server 虛擬機器](virtual-machines-windows-sql-connect.md)。

