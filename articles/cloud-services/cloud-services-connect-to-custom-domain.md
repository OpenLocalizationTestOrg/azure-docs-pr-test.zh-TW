---
title: "雲端服務 tooa aaaConnect 自訂的網域控制站 |Microsoft 文件"
description: "深入了解如何 tooconnect web/背景工作角色 tooa 自訂 AD 網域使用 PowerShell 和 AD 網域延伸"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>連接 Azure 雲端服務角色 tooa 自訂在 Azure 中裝載的 AD 網域控制站
我們會先在 Azure 中設定虛擬網路 (VNet)。 接著，我們會新增 （裝載在 Azure 虛擬機器上） 的 Active Directory 網域控制站 toohello VNet。 接下來，我們會將預先建立的 VNet，現有的雲端服務角色 toohello，然後將它們連接 toohello 網域控制站。

我們開始之前，請記住的事項 tookeep 的幾個：

1. 本教學課程使用 PowerShell，因此請確定您已安裝 Azure PowerShell，並準備 toogo。 tooget 說明設定 Azure PowerShell，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
2. 您的 AD 網域控制站和 Web/背景工作角色執行個體需要 toobe hello VNet 中。

請依照本逐步指南，如果您遇到任何問題，請讓我們在 hello hello 文章結尾處的註解。 其他人將會傳回 tooyou （是，我們沒有讀取註解）。

hello hello 雲端服務所參考的網路必須位於**傳統虛擬網路**。

## <a name="create-a-virtual-network"></a>建立虛擬網路
您可以使用 hello Azure 入口網站或 PowerShell 在 Azure 中建立虛擬網路。 在本教學課程中，我們將使用 PowerShell。 虛擬網路使用 toocreate hello Azure 入口網站，請參閱[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a>建立虛擬機器
當您完成設定 hello 虛擬網路時，您需要 toocreate AD 網域控制站。 在本教學課程中，我們會在 Azure 虛擬機器上設定 AD 網域控制站。

toodo，建立虛擬機器，透過 PowerShell 中使用下列命令的 hello:

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>升級您的虛擬機器 tooa 網域控制站
tooconfigure hello 虛擬機器的 AD 網域控制站，您將需要 toolog toohello VM 中的，並將它設定。

toolog toohello VM 中的，您可以透過 PowerShell，下列命令使用 hello 取得 hello RDP 檔案：

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

一旦您登入 toohello VM，設定您的虛擬機器由下列 hello 逐步指南的 AD 網域控制站上[如何註冊您的客戶 AD 網域控制站 tooset](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx)。

## <a name="add-your-cloud-service-toohello-virtual-network"></a>加入您的雲端服務 toohello 虛擬網路
接下來，您需要 tooadd 您雲端服務部署 toohello 新的 VNet。 toodo，透過加入使用 Visual Studio hello 相關章節 tooyour cscfg 修改雲端服務 cscfg 或 hello 您選擇的編輯器。

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

接下來建置您的雲端服務專案，並將其部署 tooAzure。 tooget 說明部署您雲端服務封裝 tooAzure 」，請參閱[如何 tooCreate 及部署雲端服務](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>連接您的 web/背景工作角色 toohello 網域
一旦在 Azure 上部署雲端服務專案時，連接使用 hello AD 網域延伸您的角色執行個體 toohello 自訂的 AD 網域。 tooadd hello AD 網域延伸 tooyour 現有雲端服務部署和聯結 hello 自訂網域，請執行下列命令在 PowerShell 中的 hello:

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

就這麼簡單。

您的雲端服務應該聯結的 tooyour 自訂的網域控制站。 如果您想要深入 hello 不同選項可供 toolearn 如何協助 tooconfigure AD 網域延伸模組，使用 hello PowerShell。 以下是一些範例：

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
