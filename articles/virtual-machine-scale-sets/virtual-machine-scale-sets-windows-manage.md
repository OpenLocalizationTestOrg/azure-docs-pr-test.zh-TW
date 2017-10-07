---
title: "在虛擬機器擴展集 Vm aaaManage |Microsoft 文件"
description: "使用 Azure PowerShell 管理虛擬機器擴展集中的虛擬機器。"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>管理虛擬機器擴展集中的虛擬機器
使用虛擬機器規模集中的此發行項 toomanage 虛擬機器中的 hello 工作。

大部分的包含管理虛擬機器規模集中的 hello 工作需要您知道您想 toomanage hello 機器 hello 執行個體識別碼。 您可以使用[Azure 資源總管](https://resources.azure.com)toofind hello 執行個體識別碼的虛擬機器規模集中的。 您也可以使用資源總管 tooverify hello 狀態的 hello 完成的工作。

請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關安裝 hello 最新版本的 Azure PowerShell 中，選取您的訂閱，並登入 tooyour 帳戶資訊。

## <a name="display-information-about-a-scale-set"></a>顯示擴展集的相關資訊
您可以取得規模集，這也是參考的 tooas hello 執行個體檢視的一般資訊。 或者，您可以取得更具體的資訊，例如 hello hello 規模集中的資源的相關資訊。

取代 hello 名稱或資源群組與設定，然後執行 hello 命令的小數位數的值加上引號的 hello:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

它會傳回類似下列畫面：

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

取代 hello hello 名稱的資源群組和小數位數設定的值加上引號。 取代 *#* 與 hello hello 虛擬機器您要了解 tooget 資訊，，然後執行它的執行個體識別碼：

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

它會傳回類似下列的範例：

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a>啟動擴展集中的虛擬機器
取代 hello hello 名稱的資源群組和小數位數設定的值加上引號。 取代 *#* 與 hello 識別碼 hello 虛擬機器，您想 toostart，，然後執行它：

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

在資源總管 中，我們可以看到 hello hello 執行個體的狀態是**執行**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

您可以在 hello 擴展集不使用 hello-InstanceId 參數來啟動 hello 的所有虛擬機器。

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>停止擴展集中的虛擬機器
取代 hello hello 名稱的資源群組和小數位數設定的值加上引號。 取代 *#* 與 hello 識別碼 hello 虛擬機器，您想 toostop，，然後執行它：

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

在資源總管 中，我們可以看到 hello hello 執行個體的狀態是**取消配置**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

toostop 虛擬機器不取消其配置、 使用 hello-StayProvisioned 參數。 您可以停止 hello 不使用 hello-InstanceId 參數設定中的所有 hello 虛擬機器。

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>重新啟動擴展集中的虛擬機器
取代 hello 與資源群組和 hello 規模集的 hello 名稱的值加上引號。 取代 *#* 與 hello 識別碼 hello 虛擬機器，您想 toorestart，，然後執行它：

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

您可以重新啟動不使用 hello-InstanceId 參數設定的 hello hello 的所有虛擬機器。

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>移除擴展集中的虛擬機器
取代 hello 與資源群組和 hello 規模集的 hello 名稱的值加上引號。 取代 *#* 與 hello 識別碼 hello 虛擬機器，您想 tooremove，，然後執行它：  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

您可以不使用 hello-InstanceId 參數來移除 hello 虛擬機器規模集一次。

## <a name="change-hello-capacity-of-a-scale-set"></a>變更 hello 容量的規模集
您可以新增或藉由變更 hello 容量 hello 集移除虛擬機器。 取得要 toochange，您想要 toobe，然後再更新 hello 新容量 hello 規模調整集合組 hello 容量 toowhat hello 規模集。 在這些命令，來取代 hello 與資源群組和 hello 規模集的 hello 名稱的值加上引號。

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

如果您要從 hello 規模集移除虛擬機器，就會先移除 hello 最高識別碼 hello 虛擬機器。

