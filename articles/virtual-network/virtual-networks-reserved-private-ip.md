---
title: "aaaStatic 內部私用 IP-Azure VM-傳統"
description: "了解靜態內部 Ip (Dip) 以及 toomanage 它們"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Tooset 靜態內部私用 IP 位址使用 PowerShell （傳統）
在大部分情況下，您不需要 toospecify 靜態內部 IP 位址的虛擬機器。 虛擬網路中的 VM 會從您指定的範圍自動接收內部 IP 位址。 但在某些情況下，針對特定 VM 指定靜態 IP 位址是合理的。 例如，如果您的 VM 進行 toorun DNS 或將網域控制站。 即使歷經停止/解除佈建狀態 hello VM 會保持靜態內部 IP 位址。 

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議的最新的部署使用 hello [Resource Manager 部署模型](virtual-networks-static-private-ip-arm-ps.md)。
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>如何 tooverify 特定的 IP 位址是否可用
如果 hello tooverify IP 位址*10.0.0.7*位於名為 vnet *TestVnet*，執行下列 PowerShell 命令的 hello，並確認 hello 值*IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> 如果您想 tootest hello 上述命令會在安全的環境中請依照下列中的 hello 指導方針[建立虛擬網路 （傳統）](virtual-networks-create-vnet-classic-pportal.md) toocreate 名為 vnet *TestVnet* ，並確保它會使用 hello *10.0.0.0/8*位址空間。
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>如何 toospecify 靜態內部 IP 建立 VM 時
hello 下列 PowerShell 指令碼會建立新的雲端服務，名為*TestService*，然後從 Azure 擷取映像，然後建立名為 VM *TestVM* hello 使用 hello 擷取映像，新雲端服務中設定 hello 名為的子網路的 VM toobe *subnet-1*，並設定*10.0.0.7* hello VM 的靜態內部 ip 位址為：

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>如何 tooretrieve 靜態內部 IP 資訊適用於 VM
執行下列 PowerShell 命令的 hello tooview hello 靜態內部 IP 資訊 hello 與 hello 指令碼，請在建立 VM，並觀察 hello 值*IpAddress*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
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

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>如何 tooremove 從 VM 的靜態內部 IP
tooremove hello 的靜態內部 IP 加入 toohello VM 在 hello 指令碼，請執行下列 PowerShell 命令的 hello:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>如何 tooadd 靜態內部 IP tooan 現有的 VM
tooadd 靜態的內部 IP toohello 下命令使用上述 runt hello 指令碼建立 VM:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>後續步驟
[保留的 IP](virtual-networks-reserved-public-ip.md)

[執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md)

[保留的 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)

