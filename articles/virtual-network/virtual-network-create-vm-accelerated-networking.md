---
title: "Azure 虛擬機器具有加速網路 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate 具有加速網路的虛擬機器。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>使用加速網路來建立虛擬機器

在此教學課程中，您了解如何在 Azure 虛擬機器 (VM) 具有加速網路 toocreate。 加速網路是 GA for Windows，而且針對特定 Linux 發佈則處於公開預覽狀態。 加速的網路啟用單一根目錄 I/O 虛擬化 (SR-IOV) tooa VM，大幅改善網路效能。 這個高效能的路徑會略過 hello 主機減少延遲、 抖動和與 hello 最嚴苛網路上的工作負載支援的 VM 類型搭配使用的 CPU 使用量，hello 資料路徑。 下列圖片顯示通訊兩台虛擬機器 (VM)，不使用加速網路與 hello:

![比較](./media/virtual-network-create-vm-accelerated-networking/image1.png)

不使用加速網路，所有的網路流量進出 hello VM 必須穿過 hello 主機和 hello 虛擬交換器。 hello 虛擬交換器提供所有的原則強制執行，例如網路安全性群組，存取控制清單、 隔離以及其他網路虛擬化服務 toonetwork 流量。 深入了解虛擬交換器，讀取 hello toolearn [HYPER-V 網路虛擬化和虛擬交換器](https://technet.microsoft.com/library/jj945275.aspx)發行項。

使用加速網路，網路流量送達 hello VM 的網路介面 (NIC)，，然後再轉送 toohello VM。 沒有的卸載加速的網路，並將其套用在硬體中，適用於所有 hello 虛擬交換器的網路原則。 套用原則中的硬體啟用 hello NIC tooforward 網路流量直接 toohello VM，同時維護它套用 hello 主應用程式中的所有 hello 原則略過 hello 主機和虛擬交換器 hello。

hello 加速網路功能的優點僅適用於 toohello 啟用的 VM。 Hello 獲得最佳結果，它是理想的 tooenable 這項功能至少兩個 Vm 上的連接 toohello 相同 Azure 虛擬網路 (VNet)。 當跨 Vnet 或連線在內部部署伺服器通訊，這項功能會有影響降到最低 toooverall 延遲。

> [!WARNING]
> 此 Linux 公用預覽不能有相同的層級的可用性和可靠性功能，因為是的 hello 一般可用性釋放。 hello 功能不支援，可能有限制功能，並可能無法使用所有的 Azure 位置。 Hello 上這項功能的可用性與狀態的最新通知，請檢查 hello Azure 虛擬網路更新 頁面。

## <a name="benefits"></a>優點
* **較低延遲高每秒封包 (pps) 秒：**從 hello 資料路徑移除 hello 虛擬交換器移除原則處理的 hello 主機中的 hello 封包所花的時間並增加 hello 可處理 hello VM 內部的封包數目。
* **降低抖動：**虛擬交換器處理取決於 hello 需要 toobe 套用的原則數量和執行 hello 處理的 hello CPU 的 hello 工作負載。 卸載 hello 原則強制 toohello 硬體所傳送的封包，直接 toohello VM，移除 hello 主機 tooVM 通訊和所有軟體插斷和內容切換移除該變化性。
* **降低 CPU 使用率：** hello 主應用程式中的略過 hello 虛擬交換器會導致處理網路流量 tooless CPU 使用率。

## <a name="Limitations"></a>限制
使用這項功能時，就會存在 hello 下列限制：

* **網路介面建立︰**您只能對新的 NIC 啟用加速網路。 無法對現有 NIC 來啟用。
* **建立 VM:**時 hello 會附加的 tooa VM 建立 VM 只能與加速啟用的網路功能的 NIC。 hello NIC 不可以是附加的 tooan 現有 VM。
* **區域︰**大多數 Azure 區域都有提供具有加速網路的 Windows VM。 多個區域都提供具有加速網路的 Linux VM。 展開這項功能可用於 hello 區域。 請 hello Azure 虛擬網路功能更新的部落格下方 hello 最新的資訊，參閱。   
* **支援的作業系統︰**Windows：Microsoft Windows Server 2012 R2 Datacenter 和 Windows Server 2016。 Linux：Ubuntu Server 16.04 LTS (含核心 4.4.0-77 或更高版本)、SLES 12 SP2、RHEL 7.3 和 CentOS 7.3 (由 “Rogue Wave Software” 發佈)。
* **VM 大小︰**一般用途和具有八個以上核心的計算最佳化執行個體大小。 如需詳細資訊，請參閱 hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)和[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的發行項。 hello 的集合支援的 VM 執行個體大小將擴充在未來的 hello。
* **僅限透過 Azure Resource Manager (ARM) 進行部署：**您無法透過 ASM/RDFE 部署加速網路。

變更 toothese 限制上經過宣布透過 hello [Azure 虛擬網路更新](https://azure.microsoft.com/updates/accelerated-networking-in-preview)頁面。

## <a name="create-a-windows-vm"></a>建立 Windows VM
您可以使用 hello Azure 入口網站或 Azure [PowerShell](#windows-powershell) toocreate hello VM。

### <a name="windows-portal"></a>入口網站

1. 從網際網路瀏覽器中，開啟 hello Azure[入口網站](https://portal.azure.com)並以您的 Azure 登入[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。 如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。
2. 在 hello 入口網站中，按一下  **+ 新增** > **計算** > **Windows Server 2016 Datacenter**。 
3. 在 hello **Windows Server 2016 Datacenter**刀鋒視窗中出現，保持*資源管理員*底下選取**選取部署模型**，按一下**建立**.
4. 在 hello**基本概念**刀鋒視窗中，輸入下列值的 hello、 保留其餘的預設選項的 hello 或選取或輸入您自己的值，然後按一下 hello**確定**按鈕：

    |設定|值|
    |---|---|
    |名稱|MyVm|
    |資源群組|讓 [新建] 保持選取狀態，並輸入 MyResourceGroup|
    |位置|美國西部 2|

    如果您是新 tooAzure，深入了解[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)，[訂閱](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)，和[位置](https://azure.microsoft.com/regions)（這也是指 tooas 區域）。
5. 在 hello**大小選擇 「**刀鋒視窗中，輸入*8*在 hello**核心下限**方塊，然後按一下 **檢視所有**。
6. 按一下**DS4_V2 標準**，或任何支援的 VM，然後按一下 [hello**選取**] 按鈕。
7. 在 hello**設定**刀鋒視窗中出現，讓所有設定，-，除了按一下**啟用**下**加速網路**，然後按一下 [hello**確定** ] 按鈕。 **注意：**如果，在先前步驟中，您選取的 VM 大小、 作業系統或位置的值未列出的 hello[限制](#Limitations)本文中，區段**加速網路**看不到。
8. 在 [hello**摘要**刀鋒視窗中，按一下 hello**確定**] 按鈕。 Azure 會開始建立 hello VM。 VM 需要花幾分鐘的時間來建立。
9. tooinstall hello 加速 windows 網路驅動程式、 完成 hello 步驟 hello[設定 Windows](#configure-windows)本文一節。

### <a name="windows-powershell"></a>PowerShell
1. 安裝 Azure PowerShell hello hello 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell 時，讀取 hello [Azure PowerShell 概觀](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。
2. 按一下 hello Windows [開始] 按鈕，啟動 PowerShell 工作階段輸入**powershell**，然後按一下**PowerShell** hello 搜尋結果中。
3. 在 PowerShell 視窗中，輸入 hello`login-azurermaccount`入您的 Azure 命令 toosign[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。 如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。
4. 在瀏覽器中，複製下列指令碼的 hello:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. 在 PowerShell 視窗中，以滑鼠右鍵按一下 toopaste hello 指令碼，並開始執行它。 系統會提示您輸入使用者名稱和密碼。 當連接 tooit hello 下一個步驟中，請使用這些認證 toolog toohello VM 中。 如果 hello 指令碼失敗，而且您執行之前變更 hello 指令碼中的值，確認您所使用的 VM 大小，作業系統的 hello 值和位置會列在 hello[限制](#Limitations)本文一節。
6. tooinstall hello 加速 windows 網路驅動程式、 完成 hello 步驟 hello[設定 Windows](#configure-windows)本文一節。

### <a name="configure-windows"></a>設定 Windows
一旦您在 Azure 中建立 hello VM，您必須安裝 Windows hello 加速網路驅動程式。 在完成之前 hello 下列步驟，您必須建立 Windows VM 使用任一 hello 加速網路[入口網站](#windows-portal)或[PowerShell](#windows-powershell)這篇文章中的步驟。 

1. 從網際網路瀏覽器中，開啟 hello Azure[入口網站](https://portal.azure.com)並以您的 Azure 登入[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。 如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*MyVm*。 當**MyVm**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello **MyVm**刀鋒視窗中，按一下 hello**連接**hello 的左上角 hello 刀鋒視窗中的按鈕。 **注意：**如果**建立**hello 底下看見**連接**按鈕時，Azure 尚未完成建立 hello VM。 按一下**連接**只有您無法再查看之後**建立**下 hello**連接** 按鈕。
4. 允許您的瀏覽器 toodownload hello **MyVm.rdp**檔案。  在下載後，按一下 hello 檔案 tooopen 它。 
5. 按一下 hello**連接**按鈕在 hello**遠端桌面連線**隨即出現，通知您該 hello hello 遠端連線的發行者無法識別的方塊。
6. 在 hello **Windows 安全性**方塊中，按一下**更多選擇**，然後按一下 **使用不同的帳戶**。 輸入 hello 使用者名稱和您在步驟 4 中，輸入的密碼，然後按一下 [hello**確定**] 按鈕。
7. 按一下 hello**是**hello 隨即出現，通知您，無法驗證 hello hello 遠端電腦識別的遠端桌面連線方塊中的按鈕。
8. 以滑鼠右鍵按一下 hello Windows [開始] 按鈕，然後按一下**裝置管理員**。 展開 hello**網路介面卡**節點。 確認該 hello **Mellanox connectx-3 虛擬函式乙太網路介面卡**隨即出現，如 hello 下列圖片所示：
   
    ![裝置管理員](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. 現在已啟用您 VM 的加速網路。

## <a name="create-a-linux-vm"></a>建立 Linux VM
您可以使用 hello Azure 入口網站或 Azure [PowerShell](#linux-powershell) toocreate Ubuntu 或 SLES VM。 RHEL 和 CentOS VM 的工作流程不同。  請參閱下列的 hello 指示。

### <a name="linux-portal"></a>入口網站
1. 完成步驟 1-5 的 hello 網路 Linux preview 加速 hello 註冊[PowerShell 建立 Linux VM-](#linux-powershell)本文一節。  您無法註冊 hello 入口網站中的 hello 預覽。
2. 完成步驟 1-8 中的 hello[建立 Windows VM-入口網站](#windows-portal)本文一節。 在步驟 2 中，按一下 [Ubuntu Server 16.04 LTS] 而不是 [Windows Server 2016 Datacenter]。 此教學課程中，選擇 toouse 密碼，而不是 SSH 金鑰，但實際執行部署，您可以使用。 如果**加速網路**不會出現在您完成步驟 7 的 hello[建立 Windows VM-入口網站](#windows-portal)> 一節的本文中，可能是其中一個 hello 下列原因：
    - 尚未登錄 hello 預覽。 確認您的註冊狀態是**註冊**hello 的步驟 4 中所述， [Powershell 建立 Linux VM-](#linux-powershell)本文一節。 **注意：**如果您已參與 hello 加速網路 Windows Vm preview （它的任何較長的必要 tooregister toouse 加速適用於 Windows Vm 網路），您都不會自動註冊 hello 加速的網路Linux Vm 預覽。 您必須註冊 hello 加速網路的 Linux Vm 預覽 tooparticipate 中。
    - 您尚未選取 VM 大小、 作業系統或所列位置中 hello[限制](#limitations)本文一節。
3. tooinstall hello 加速適用於 Linux 的網路驅動程式、 完成 hello 步驟 hello[設定 Linux](#configure-linux)本文一節。

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>如果您建立 Linux Vm 加速網路中的訂用帳戶，然後嘗試 toocreate hello 加速網路功能與 Windows VM 相同的訂用帳戶，hello 建立 Windows VM 可能會失敗。 在預覽版測時期間，建議您在不同的訂用帳戶中測試具有加速網路功能的 Linux 和 Windows VM。
>

1. 安裝 Azure PowerShell hello hello 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell 時，讀取 hello [Azure PowerShell 概觀](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。
2. 按一下 hello Windows [開始] 按鈕，啟動 PowerShell 工作階段輸入**powershell**，然後按一下**PowerShell** hello 搜尋結果中。
3. 在 PowerShell 視窗中，輸入 hello`login-azurermaccount`入您的 Azure 命令 toosign[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。 如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。
4. Azure 網路加速 hello 註冊預覽，藉由完成下列步驟的 hello:
    - 傳送電子郵件太[axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e)與您的 Azure 訂用帳戶 ID 預定的用途。 請等候來自 Microsoft 有關正在啟用您訂用帳戶的電子郵件確認。
    - 輸入下列命令 tooconfirm hello preview 註冊您的 hello:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        請繼續進行步驟 5，直到**註冊**hello 後輸入 hello 前一個命令輸出中會出現。 您的輸出必須看起來像 hello 以下輸出再繼續進行：
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >如果您已參與 hello 加速網路 Windows Vm preview （它的任何較長的必要 tooregister toouse 加速適用於 Windows Vm 網路），您都不會自動註冊 hello 加速預覽 Linux Vm 的網路功能。 您必須註冊 hello 加速網路的 Linux Vm 預覽 tooparticipate 中。
      >
5. 在瀏覽器中，複製下列指令碼取代為所需的 Ubuntu 或 SLES hello。  同樣地，Redhat 和 CentOS 具有不同的工作流程，如下所述：

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. 在 PowerShell 視窗中，以滑鼠右鍵按一下 toopaste hello 指令碼，並開始執行它。 系統會提示您輸入使用者名稱和密碼。 當連接 tooit hello 下一個步驟中，請使用這些認證 toolog toohello VM 中。 如果 hello 指令碼失敗，請確認：
    - 步驟 4 中所述，您會註冊 hello preview
    - 如果您變更 VM 大小、 作業系統類型或位置值 hello 指令碼中的執行它之前，hello 值會列在 hello[限制](#Limitations)本文一節。
7. tooinstall hello 加速適用於 Linux 的網路驅動程式、 完成 hello 步驟 hello[設定 Linux](#configure-linux)本文一節。

### <a name="configure-linux"></a>設定 Linux

一旦您在 Azure 中建立 hello VM，您必須安裝適用於 Linux 的 hello 加速網路驅動程式。 在完成之前 hello 下列步驟，您必須建立 Linux VM 使用任一 hello 加速網路[入口網站](#linux-portal)或[PowerShell](#linux-powershell)這篇文章中的步驟。 

1. 從網際網路瀏覽器中，開啟 hello Azure[入口網站](https://portal.azure.com)並以您的 Azure 登入[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。 如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。
2. 頂端的 hello 入口網站中，toohello 右邊的 hello hello*搜尋資源*列上，按一下 hello **> _**圖示 toostart Bash 雲端殼層 （預覽）。 hello Bash 雲端殼層窗格會顯示在 hello 下方 hello 入口網站並在幾秒鐘之後, 呈現 **username@Azure:~ $**提示字元。 雖然您可以從您的電腦，而不是 hello 雲端殼層 SSH toohello VM，在此教學課程中的 hello 指示會假設您使用 hello 雲端殼層。
3. 在 hello hello 入口網站頂端，在 [hello] 方塊中，其中包含 hello 文字*搜尋資源*，型別*MyVm*。 當**MyVm**會出現在 hello 搜尋結果中，按一下它。
4. 在 hello **MyVm**刀鋒視窗中，按一下 hello**連接**hello 的左上角 hello 刀鋒視窗中的按鈕。 **注意：**如果**建立**hello 底下看見**連接**按鈕時，Azure 尚未完成建立 hello VM。 按一下**連接**只有您無法再查看之後**建立**下 hello**連接** 按鈕。
5. Azure 會開啟告訴您 tooenter hello 方塊`ssh adminuser@<ipaddress>`。 輸入這個命令在 hello 雲端殼層 （或複製從 hello 方塊出現在步驟 4，並將它貼入 toohello 雲端殼層中），然後按 Enter 鍵。
6. Enter**是**toohello 問題詢問您是否 toocontinue 連接，然後按 Enter 鍵。
7. 輸入 hello 建立 hello VM 時，您所輸入的密碼。 一次成功登入 toohello VM，您會看到adminuser@MyVm:~ $ 提示字元。 您現在會記錄在 toohello VM 透過 hello 雲端殼層工作階段。 **注意︰**Cloud Shell 工作階段會在閒置 10 分鐘後逾時。

此時，hello 指示隨著您正在使用的 hello 發佈。 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. Hello 提示字元之下，輸入`uname -r`並確認 hello 版本：

    * Ubuntu 是 "4.4.0-77-generic" 或更新版本
    * SLES 是 "4.4.59-92.20-default" 或更新版本

2. 由執行 hello 命令，請遵循建立 hello 標準網路 vNIC 與 hello 加速網路 vNIC 之間連結。 網路流量會使用更高版本來執行 hello 證券可確保網路流量沒有被中斷的某些設定變更跨加速網路 vNIC，hello。
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. 執行 hello 指令碼之後, hello VM 會重新啟動之後暫停 60 秒。
4. 一次重新啟動 VM，hello 重新連線 tooit 再次完成步驟 5-7。
5. 執行 hello`ifconfig`命令，並確認結果是 bond0 hello 介面顯示為向上。 
 
 >[!NOTE]
      >使用加速網路功能的應用程式必須透過 hello 通訊*bond0*介面未*eth0*。  加速網路功能正式運作之前，可能會變更 hello 介面名稱。

#### <a name="rhelcentos"></a>RHEL/CentOS

建立 Red Hat Enterprise Linux 或 CentOS 7.3 VM 需要一些額外步驟 tooload hello 最新驅動程式所需的 SR-IOV 與 hello hello 網路卡的虛擬函式 (VF) 驅動程式。 hello 第一階段中的 hello 指示準備映像可能是使用的 toomake 擁有 hello 預先載入的驅動程式的一個或多個虛擬機器。

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>第一個階段：準備 Red Hat Enterprise Linux 或 CentOS 7.3 基礎映像。 

1.  在 Azure 上佈建非 SRIOV CentOS 7.3 VM

2.  安裝 LIS 4.2.2：
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  下載設定檔
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  取消佈建此 VM

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  從 Azure 入口網站停止此 VM。移 tooVM 的 「 磁碟 」，擷取 hello OSDisk VHD URI。 此 URI 包含 hello 基底映像的 VHD 名稱和其儲存體帳戶。 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>第二個階段：在 Azure 上佈建新的 VM

1.  佈建與新增 AzureRMVMConfig 基礎的新 Vm 使用 hello 基底映像使用 AcceleratedNetworking hello vNIC 上啟用第一，階段中所擷取的 VHD:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Vm 開機後，檢查 「 lspci"hello VF 裝置，並檢查 hello Mellanox 項目。 例如，我們應該會看到 hello lspci 輸出的這個項目：
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  執行 hello 聯結指令碼：

    ```bash
    sudo bondvf.sh
    ```

4.  重新啟動 hello 新的 Vm:

    ```bash
    sudo reboot
    ```

hello VM 應該啟動 bond0 設定與 hello 啟用加速網路路徑。  執行`ifconfig`tooconfirm。
