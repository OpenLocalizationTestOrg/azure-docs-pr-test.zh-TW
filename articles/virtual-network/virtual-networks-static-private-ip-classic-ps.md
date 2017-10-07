---
title: "適用於 Vm （傳統）-Azure PowerShell aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解如何 tooconfigure 私人 IP 位址使用 PowerShell 的虛擬機器 （傳統）。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 60c7b489-46ae-48af-a453-2b429a474afd
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 99546ee9c2c4eb9aa7b67f30721d37ef9b2944f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a>使用 PowerShell 設定虛擬機器 (傳統) 的私人 IP 位址

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello 傳統部署模型。 您也可以[管理 hello Resource Manager 部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-arm-ps.md)。

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

下列的 hello 範例 PowerShell 命令預期簡單的環境中已經建立。 如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 VNet](virtual-networks-create-vnet-classic-netcfg-ps.md)。

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>如何 tooverify 特定的 IP 位址是否可用
如果 hello tooverify IP 位址*192.168.1.101*位於名為 VNet *TestVNet*，執行下列 PowerShell 命令的 hello，並確認 hello 值*IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

預期的輸出：

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>如何 toospecify 靜態私人 IP 位址建立 VM 時
hello 下列 PowerShell 指令碼會建立新的雲端服務，名為*TestService*，然後從 Azure 擷取映像，建立名為 VM *DNS01* hello 新雲端服務中使用 hello 擷取映像，設定hello 名為的子網路的 VM toobe*前端*，並設定*從 192.168.1.7* hello VM 的靜態私人 IP 位址為：

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

預期的輸出：

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊
tooview hello 靜態私人 IP 位址建立 VM 與 hello 指令碼，請執行下列 PowerShell 命令的 hello hello 資訊，並觀察 hello 值*IpAddress*:

    Get-AzureVM -Name DNS01 -ServiceName TestService

預期的輸出：

    DeploymentName              : TestService
    Name                        : DNS01
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 192.168.1.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : DNS01
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>如何 tooremove 靜態私人 IP 位址從 VM
tooremove hello 靜態私人 IP 位址執行下列 PowerShell 命令的 hello 上方的 hello 指令碼中加入 toohello VM:

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

預期的輸出：

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Tooadd 靜態私人 IP 定址 tooan 現有 VM 的方式
tooadd 靜態私人 IP 位址 toohello 下命令使用上述 runt hello 指令碼建立 VM:

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

預期的輸出：

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a>後續步驟
* 深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。
* 深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。
* 請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。

