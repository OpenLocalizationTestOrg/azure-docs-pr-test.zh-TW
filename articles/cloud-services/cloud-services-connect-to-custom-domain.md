---
title: "將雲端服務連接到自訂網域控制站 | Microsoft Docs"
description: "了解如何使用 PowerShell 和 AD 網域延伸將 Web/背景工作角色連接到自訂 AD 網域"
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
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="d25ba-103">將 Azure 雲端服務角色連接到裝載於 Azure 中的自訂 AD 網域控制站</span><span class="sxs-lookup"><span data-stu-id="d25ba-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="d25ba-104">我們會先在 Azure 中設定虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="d25ba-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="d25ba-105">接著再將 Active Directory 網域控制站 (裝載於 Azure 虛擬機器上) 加入 VNet。</span><span class="sxs-lookup"><span data-stu-id="d25ba-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="d25ba-106">下一步是將現有雲端服務角色加入預先建立的 VNet，然後將它們連接到網域控制站。</span><span class="sxs-lookup"><span data-stu-id="d25ba-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="d25ba-107">在開始之前，請將以下幾件事牢記在心：</span><span class="sxs-lookup"><span data-stu-id="d25ba-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="d25ba-108">本教學課程使用 PowerShell，因此請確認您已安裝 Azure PowerShell 且已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="d25ba-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="d25ba-109">如需設定 Azure PowerShell 的說明，請參閱 [如何安裝及設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d25ba-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="d25ba-110">AD 網域控制站和 Web/背景工作角色執行個體必須位在 VNet 中。</span><span class="sxs-lookup"><span data-stu-id="d25ba-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="d25ba-111">請依本逐步指南作業，如果遇到任何問題，請在本文結尾處留言。</span><span class="sxs-lookup"><span data-stu-id="d25ba-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="d25ba-112">我們將會回覆您 (沒錯，我們真的會閱讀留言)。</span><span class="sxs-lookup"><span data-stu-id="d25ba-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="d25ba-113">雲端服務所參考的網路必須是**傳統虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="d25ba-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="d25ba-114">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d25ba-114">Create a Virtual Network</span></span>
<span data-ttu-id="d25ba-115">您可以使用 Azure 入口網站或 PowerShell 在 Azure 中建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d25ba-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="d25ba-116">在本教學課程中，我們將使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d25ba-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="d25ba-117">若要使用 Azure 入口網站建立虛擬網路，請參閱[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="d25ba-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="d25ba-118">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d25ba-118">Create a Virtual Machine</span></span>
<span data-ttu-id="d25ba-119">完成虛擬網路的設定後，您需要建立 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="d25ba-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="d25ba-120">在本教學課程中，我們會在 Azure 虛擬機器上設定 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="d25ba-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="d25ba-121">若要這樣做，請使用下列命令透過 PowerShell 建立虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="d25ba-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

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

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="d25ba-122">將虛擬機器提升為網域控制站</span><span class="sxs-lookup"><span data-stu-id="d25ba-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="d25ba-123">若要將虛擬機器設定為 AD 網域控制站，您需要登入 VM 並進行設定。</span><span class="sxs-lookup"><span data-stu-id="d25ba-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="d25ba-124">若要登入 VM，您可以透過 PowerShell 取得 RDP 檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d25ba-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="d25ba-125">登入 VM 後，請遵循[如何設定客戶的 AD 網域控制站](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx)中的逐步指南，將虛擬機器設為 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="d25ba-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="d25ba-126">將雲端服務加入虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d25ba-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="d25ba-127">接下來，您需要將雲端服務部署新增至新的 VNet。</span><span class="sxs-lookup"><span data-stu-id="d25ba-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="d25ba-128">若要這樣做，請使用 Visual Studio 或選擇的編輯器將相關區段加入 cscfg，藉此修改雲端服務 cscfg。</span><span class="sxs-lookup"><span data-stu-id="d25ba-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

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

<span data-ttu-id="d25ba-129">接下來，請建置雲端服務專案並將它部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="d25ba-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="d25ba-130">如需將雲端服務封裝部署到 Azure 的說明，請參閱「 [如何建立和部署雲端服務](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="d25ba-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="d25ba-131">將 Web/背景工作角色連接到網域</span><span class="sxs-lookup"><span data-stu-id="d25ba-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="d25ba-132">在 Azure 上部署雲端服務專案後，請使用 AD 網域延伸將角色執行個體連接到自訂 AD　網域。</span><span class="sxs-lookup"><span data-stu-id="d25ba-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="d25ba-133">若要將 AD 網域延伸加入現有雲端服務部署及加入自訂網域，請在 PowerShell 中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d25ba-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="d25ba-134">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="d25ba-134">And that's it.</span></span>

<span data-ttu-id="d25ba-135">您的雲端服務應該已加入自訂網域控制站。</span><span class="sxs-lookup"><span data-stu-id="d25ba-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="d25ba-136">如果您想要深入了解設定 AD 網域延伸時可用的其他選項，請使用 PowerShell 說明。</span><span class="sxs-lookup"><span data-stu-id="d25ba-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="d25ba-137">以下是一些範例：</span><span class="sxs-lookup"><span data-stu-id="d25ba-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
