---
title: "管理虛擬機器擴展集中的 VM | Microsoft Docs"
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
ms.openlocfilehash: d09a020b903e5f43afe03b86c675bcc1eb536cbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="56fa0-103">管理虛擬機器擴展集中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56fa0-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="56fa0-104">您可以使用本文中的工作來管理虛擬機器擴展集中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="56fa0-104">Use the tasks in this article to manage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="56fa0-105">大部分涉及管理擴展集中虛擬機器的工作，都需要您知道要管理的電腦執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="56fa0-105">Most of the tasks that involve managing a virtual machine in a scale set require that you know the instance ID of the machine that you want to manage.</span></span> <span data-ttu-id="56fa0-106">您可以使用 [Azure 資源總管](https://resources.azure.com) 尋找擴展集中虛擬機器的執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="56fa0-106">You can use [Azure Resource Explorer](https://resources.azure.com) to find the instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="56fa0-107">您也可以使用資源總管來確認您所完成的工作狀態。</span><span class="sxs-lookup"><span data-stu-id="56fa0-107">You also use Resource Explorer to verify the status of the tasks that you finish.</span></span>

<span data-ttu-id="56fa0-108">如需如何安裝最新版 Azure PowerShell、選取訂用帳戶，以及登入帳戶的相關資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="56fa0-108">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="56fa0-109">顯示擴展集的相關資訊</span><span class="sxs-lookup"><span data-stu-id="56fa0-109">Display information about a scale set</span></span>
<span data-ttu-id="56fa0-110">您可以取得擴展集，也稱為執行個體檢視的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="56fa0-110">You can get general information about a scale set, which is also referred to as the instance view.</span></span> <span data-ttu-id="56fa0-111">或者，您可以取得更特定的資訊，如擴展集中的資源資訊。</span><span class="sxs-lookup"><span data-stu-id="56fa0-111">Or, you can get more specific information, such as information about the resources in the scale set.</span></span>

<span data-ttu-id="56fa0-112">將引號值取代為名稱或您的資源群組和擴展集，然後執行命令︰</span><span class="sxs-lookup"><span data-stu-id="56fa0-112">Replace the quoted values with the name or your resource group and scale set and then run the command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="56fa0-113">它會傳回類似下列畫面：</span><span class="sxs-lookup"><span data-stu-id="56fa0-113">It returns something like this:</span></span>

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

<span data-ttu-id="56fa0-114">將引號值取代為名稱或您的資源群組和擴展集。</span><span class="sxs-lookup"><span data-stu-id="56fa0-114">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="56fa0-115">將 *#* 取代為您想要取得相關資訊的虛擬機器執行個體識別碼，然後加以執行︰</span><span class="sxs-lookup"><span data-stu-id="56fa0-115">Replace *#* with the instance identifier of the virtual machine that you want to get information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56fa0-116">它會傳回類似下列的範例：</span><span class="sxs-lookup"><span data-stu-id="56fa0-116">It returns something like this example:</span></span>

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="56fa0-117">啟動擴展集中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56fa0-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="56fa0-118">將引號值取代為名稱或您的資源群組和擴展集。</span><span class="sxs-lookup"><span data-stu-id="56fa0-118">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="56fa0-119">將 *#* 取代為您想要啟動的虛擬機器識別碼，然後加以執行：</span><span class="sxs-lookup"><span data-stu-id="56fa0-119">Replace *#* with the identifier of the virtual machine that you want to start and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56fa0-120">在資源總管中，我們可以看到執行個體的狀態是 **執行中**：</span><span class="sxs-lookup"><span data-stu-id="56fa0-120">In Resource Explorer, we can see that the status of the instance is **running**:</span></span>

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

<span data-ttu-id="56fa0-121">您可以啟動擴展集中的所有虛擬機器，只要不使用 -InstanceId 參數即可。</span><span class="sxs-lookup"><span data-stu-id="56fa0-121">You can start all the virtual machines in the scale set by not using the -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="56fa0-122">停止擴展集中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56fa0-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="56fa0-123">將引號值取代為名稱或您的資源群組和擴展集。</span><span class="sxs-lookup"><span data-stu-id="56fa0-123">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="56fa0-124">將 *#* 取代為您想要停止的虛擬機器識別碼，然後加以執行：</span><span class="sxs-lookup"><span data-stu-id="56fa0-124">Replace *#* with the identifier of the virtual machine that you want to stop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56fa0-125">在資源總管中，我們可以看到執行個體的狀態是 **解除配置**：</span><span class="sxs-lookup"><span data-stu-id="56fa0-125">In Resource Explorer, we can see that the status of the instance is **deallocated**:</span></span>

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

<span data-ttu-id="56fa0-126">若要停止虛擬機器但不解除配置，請使用 -StayProvisioned 參數。</span><span class="sxs-lookup"><span data-stu-id="56fa0-126">To stop a virtual machine and not deallocate it, use the -StayProvisioned parameter.</span></span> <span data-ttu-id="56fa0-127">您可以停止集合中的所有虛擬機器，只要不使用 -InstanceId 參數即可。</span><span class="sxs-lookup"><span data-stu-id="56fa0-127">You can stop all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="56fa0-128">重新啟動擴展集中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56fa0-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="56fa0-129">將引號值取代為名稱或您的資源群組和擴展集。</span><span class="sxs-lookup"><span data-stu-id="56fa0-129">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="56fa0-130">將 *#* 取代為您想要重新啟動的虛擬機器識別碼，然後加以執行：</span><span class="sxs-lookup"><span data-stu-id="56fa0-130">Replace *#* with the identifier of the virtual machine that you want to restart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56fa0-131">您可以重新啟動集合中的所有虛擬機器，只要不使用 -InstanceId 參數即可。</span><span class="sxs-lookup"><span data-stu-id="56fa0-131">You can restart all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="56fa0-132">移除擴展集中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56fa0-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="56fa0-133">將引號值取代為名稱或您的資源群組和擴展集。</span><span class="sxs-lookup"><span data-stu-id="56fa0-133">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="56fa0-134">將 *#* 取代為您想要移除的虛擬機器識別碼，然後加以執行：</span><span class="sxs-lookup"><span data-stu-id="56fa0-134">Replace *#* with the identifier of the virtual machine that you want to remove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56fa0-135">您可以一次移除虛擬機器擴展集，只要不使用 -InstanceId 參數即可。</span><span class="sxs-lookup"><span data-stu-id="56fa0-135">You can remove the virtual machine scale set all at once by not using the -InstanceId parameter.</span></span>

## <a name="change-the-capacity-of-a-scale-set"></a><span data-ttu-id="56fa0-136">變更擴展集的容量</span><span class="sxs-lookup"><span data-stu-id="56fa0-136">Change the capacity of a scale set</span></span>
<span data-ttu-id="56fa0-137">您可以新增或移除虛擬機器，方法是變更集合的容量。</span><span class="sxs-lookup"><span data-stu-id="56fa0-137">You can add or remove virtual machines by changing the capacity of the set.</span></span> <span data-ttu-id="56fa0-138">取得您想要變更的擴展集，設定您想要的容量，然後使用新的容量更新擴展集。</span><span class="sxs-lookup"><span data-stu-id="56fa0-138">Get the scale set that you want to change, set the capacity to what you want it to be, and then update the scale set with the new capacity.</span></span> <span data-ttu-id="56fa0-139">在這些命令中，將引號值取代為名稱或您的資源群組和擴展集。</span><span class="sxs-lookup"><span data-stu-id="56fa0-139">In these commands, replace the quoted values with the name of your resource group and the scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="56fa0-140">如果您要從擴展集移除虛擬機器，會先移除具有最高識別碼的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="56fa0-140">If you are removing virtual machines from the scale set, the virtual machines with the highest ids are removed first.</span></span>

