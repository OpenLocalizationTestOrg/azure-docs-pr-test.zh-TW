---
title: "aaaCreate 具有多個 Nic 的 Azure PowerShell 的 VM （傳統） |Microsoft 文件"
description: "深入了解如何 toocreate 具有使用 PowerShell 將多個 Nic 的 VM （傳統）。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>使用 PowerShell 建立具有多個 NIC 的 VM (傳統)

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

您可以在 Azure 中建立虛擬機器 (Vm)，並附加多個網路介面 (Nic) tooeach 的 Vm。 有多個 NIC 時，可透過各個 NIC 分隔不同的流量類型。 例如，一個 NIC 通訊 hello 網際網路，而另一個不只與內部資源通訊連接 toohello 網際網路。 許多網路虛擬應用裝置，例如應用程式傳遞和 WAN 最佳化解決方案需要 hello 能力 tooseparate 跨多個 Nic 的網路流量。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 深入了解如何 tooperform 這些步驟使用 hello [Resource Manager 部署模型](virtual-network-deploy-multinic-arm-ps.md)。

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。

## <a name="prerequisites"></a>必要條件

您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。 toocreate 這些資源，完成 hello 遵循的步驟。 建立虛擬網路中 hello 的 hello 步驟[建立虛擬網路](virtual-networks-create-vnet-classic-netcfg-ps.md)發行項。

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>後端 Vm 建立 hello
後端 Vm 相依於下列資源的 hello hello 建立 hello:

* **後端子網路**。 hello 資料庫伺服器都屬於不同的子網路，toosegregate 流量。 下列指令碼 hello 預期此子網路 tooexist 中名為 vnet *WTestVnet*。
* **資料磁碟的儲存體帳戶**。 為提升效能，hello hello 資料庫伺服器上的資料磁碟會使用固態硬碟 (SSD) 技術，需要進階儲存體帳戶。 請確定 hello 部署 toosupport 高階儲存體的 Azure 位置。
* **可用性設定組**。 所有資料庫伺服器將會都加入 tooa 一個可用性設定組，其中至少一個 hello Vm tooensure 已啟動並執行在維護期間。

### <a name="step-1---start-your-script"></a>步驟 1：啟動指令碼
您可以下載用 hello 完整 PowerShell 指令碼[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1)。 請遵循下列 toochange hello 指令碼 toowork 您環境中的 hello 步驟。

1. 變更 hello hello 變數值以下根據您現有的資源群組，在上面部署[必要條件](#Prerequisites)。

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. 變更 hello 值 hello 變數的下列根據 hello 值要 toouse 後端部署。

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>步驟 2：為 VM 建立必要的資源
您需要新的雲端服務和儲存體帳戶的所有 vm hello 資料磁碟的 toocreate。 您也需要 toospecify 映像及本機系統管理員帳戶的 hello Vm。 toocreate 這些資源，完成下列步驟 hello:

1. 建立新的雲端服務。

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. 建立新的進階儲存體帳戶。

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. 上面所建立與 hello 目前儲存體帳戶訂用帳戶集 hello 儲存體帳戶。

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. 選取 hello VM 映像。

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. 設定 hello 本機系統管理員帳戶認證。

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>步驟 3：建立 VM
您需要 toouse 迴圈 toocreate 因為許多 Vm，並建立 hello 所需的 Nic 和 Vm hello 迴圈內。 toocreate hello Nic 和 Vm，執行下列步驟的 hello。

1. 啟動`for`迴圈 toorepeat hello 命令 toocreate VM 和兩個 Nic 如有必要，次數根據 hello hello 值`$numberOfVMs`變數。

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. 建立`VMConfig`指定 hello 映像、 大小和可用性設定組 hello VM 的物件。

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. 佈建 hello 做為 Windows VM 的 VM。

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. 設定 hello 預設 NIC，並將其指派靜態 IP 位址。

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. 為每部 VM 加入第二個 NIC。

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. 每個 VM 建立 toodata 磁碟。

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. 建立每個 VM，以及結束 hello 迴圈。

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>步驟 4-執行 hello 指令碼
既然您已下載並變更 hello 指令碼，根據您的需求，runt 他指令碼 toocreate hello 後端資料庫具有多個 Nic Vm。

1. 儲存您的指令碼，並從 hello 執行**PowerShell**命令提示字元，或**PowerShell ISE**。 您會看到 hello 初始輸出，如下所示。

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. 填寫在 hello 認證提示，並按一下所需的 hello 資訊**確定**。 會傳回以下 hello 輸出。

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
