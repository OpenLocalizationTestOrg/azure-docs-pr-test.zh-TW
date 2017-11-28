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
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="6898f-103">連接 Azure 雲端服務角色 tooa 自訂在 Azure 中裝載的 AD 網域控制站</span><span class="sxs-lookup"><span data-stu-id="6898f-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="6898f-104">我們會先在 Azure 中設定虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="6898f-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="6898f-105">接著，我們會新增 （裝載在 Azure 虛擬機器上） 的 Active Directory 網域控制站 toohello VNet。</span><span class="sxs-lookup"><span data-stu-id="6898f-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="6898f-106">接下來，我們會將預先建立的 VNet，現有的雲端服務角色 toohello，然後將它們連接 toohello 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="6898f-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="6898f-107">我們開始之前，請記住的事項 tookeep 的幾個：</span><span class="sxs-lookup"><span data-stu-id="6898f-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="6898f-108">本教學課程使用 PowerShell，因此請確定您已安裝 Azure PowerShell，並準備 toogo。</span><span class="sxs-lookup"><span data-stu-id="6898f-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="6898f-109">tooget 說明設定 Azure PowerShell，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6898f-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="6898f-110">您的 AD 網域控制站和 Web/背景工作角色執行個體需要 toobe hello VNet 中。</span><span class="sxs-lookup"><span data-stu-id="6898f-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="6898f-111">請依照本逐步指南，如果您遇到任何問題，請讓我們在 hello hello 文章結尾處的註解。</span><span class="sxs-lookup"><span data-stu-id="6898f-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="6898f-112">其他人將會傳回 tooyou （是，我們沒有讀取註解）。</span><span class="sxs-lookup"><span data-stu-id="6898f-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="6898f-113">hello hello 雲端服務所參考的網路必須位於**傳統虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="6898f-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="6898f-114">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6898f-114">Create a Virtual Network</span></span>
<span data-ttu-id="6898f-115">您可以使用 hello Azure 入口網站或 PowerShell 在 Azure 中建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6898f-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="6898f-116">在本教學課程中，我們將使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6898f-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="6898f-117">虛擬網路使用 toocreate hello Azure 入口網站，請參閱[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="6898f-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="6898f-118">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6898f-118">Create a Virtual Machine</span></span>
<span data-ttu-id="6898f-119">當您完成設定 hello 虛擬網路時，您需要 toocreate AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="6898f-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="6898f-120">在本教學課程中，我們會在 Azure 虛擬機器上設定 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="6898f-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="6898f-121">toodo，建立虛擬機器，透過 PowerShell 中使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6898f-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

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

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="6898f-122">升級您的虛擬機器 tooa 網域控制站</span><span class="sxs-lookup"><span data-stu-id="6898f-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="6898f-123">tooconfigure hello 虛擬機器的 AD 網域控制站，您將需要 toolog toohello VM 中的，並將它設定。</span><span class="sxs-lookup"><span data-stu-id="6898f-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="6898f-124">toolog toohello VM 中的，您可以透過 PowerShell，下列命令使用 hello 取得 hello RDP 檔案：</span><span class="sxs-lookup"><span data-stu-id="6898f-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="6898f-125">一旦您登入 toohello VM，設定您的虛擬機器由下列 hello 逐步指南的 AD 網域控制站上[如何註冊您的客戶 AD 網域控制站 tooset](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6898f-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="6898f-126">加入您的雲端服務 toohello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6898f-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="6898f-127">接下來，您需要 tooadd 您雲端服務部署 toohello 新的 VNet。</span><span class="sxs-lookup"><span data-stu-id="6898f-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="6898f-128">toodo，透過加入使用 Visual Studio hello 相關章節 tooyour cscfg 修改雲端服務 cscfg 或 hello 您選擇的編輯器。</span><span class="sxs-lookup"><span data-stu-id="6898f-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

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

<span data-ttu-id="6898f-129">接下來建置您的雲端服務專案，並將其部署 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6898f-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="6898f-130">tooget 說明部署您雲端服務封裝 tooAzure 」，請參閱[如何 tooCreate 及部署雲端服務](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="6898f-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="6898f-131">連接您的 web/背景工作角色 toohello 網域</span><span class="sxs-lookup"><span data-stu-id="6898f-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="6898f-132">一旦在 Azure 上部署雲端服務專案時，連接使用 hello AD 網域延伸您的角色執行個體 toohello 自訂的 AD 網域。</span><span class="sxs-lookup"><span data-stu-id="6898f-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="6898f-133">tooadd hello AD 網域延伸 tooyour 現有雲端服務部署和聯結 hello 自訂網域，請執行下列命令在 PowerShell 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="6898f-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

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

<span data-ttu-id="6898f-134">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="6898f-134">And that's it.</span></span>

<span data-ttu-id="6898f-135">您的雲端服務應該聯結的 tooyour 自訂的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="6898f-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="6898f-136">如果您想要深入 hello 不同選項可供 toolearn 如何協助 tooconfigure AD 網域延伸模組，使用 hello PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6898f-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="6898f-137">以下是一些範例：</span><span class="sxs-lookup"><span data-stu-id="6898f-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
