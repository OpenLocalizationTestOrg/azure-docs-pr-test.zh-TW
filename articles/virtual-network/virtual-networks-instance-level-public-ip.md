---
title: "aaaAzure 執行個體層級 （傳統） 的公用 IP 位址 |Microsoft 文件"
description: "了解執行個體層級公用 IP (ILPIP) 位址及如何 toomanage 它們使用 PowerShell。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="f0b36-103">執行個體層級公用 IP (Classic) 概觀</span><span class="sxs-lookup"><span data-stu-id="f0b36-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="f0b36-104">執行個體層級公用 IP (ILPIP) 是您在 tooa VM 或雲端服務角色執行個體，而不是 VM 或角色執行個體位於 toohello 雲端服務可以直接指派的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0b36-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="f0b36-105">ILPIP 不接受 hello 取代 hello 虛擬 IP (VIP) 指派 tooyour 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f0b36-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="f0b36-106">而是其他 IP 位址，您可以使用 tooconnect 直接 tooyour VM 或角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="f0b36-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0b36-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f0b36-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f0b36-108">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f0b36-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="f0b36-109">Microsoft 建議您透過 Resource Manager 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="f0b36-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="f0b36-110">請確定您了解 [IP 位址](virtual-network-ip-addresses-overview-classic.md) 在 Azure 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f0b36-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![ILPIP 和 VIP 之間的差異](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="f0b36-112">圖 1 所示，使用 VIP 存取 hello 雲端服務、 hello 時個別 Vm 通常會使用存取 VIP:&lt;連接埠號碼&gt;。</span><span class="sxs-lookup"><span data-stu-id="f0b36-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="f0b36-113">藉由指派 ILPIP tooa 特定 VM，VM 可以存取直接使用該 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0b36-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="f0b36-114">當您在 Azure 中建立雲端服務時，對應的 DNS A 記錄會自動建立 tooallow 存取 toohello 服務透過完整的網域名稱 (FQDN)，而不是使用 hello 實際 VIP。</span><span class="sxs-lookup"><span data-stu-id="f0b36-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="f0b36-115">相同的程序會針對 ILPIP，讓存取 toohello VM 或角色執行個體的 FQDN 而不是 hello ILPIP hello。</span><span class="sxs-lookup"><span data-stu-id="f0b36-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="f0b36-116">比方說，如果您建立名為雲端服務*contosoadservice*，並設定名為 web 角色*contosoweb*與兩個執行個體，Azure 的暫存器 hello 遵循 A 記錄 hello 執行個體：</span><span class="sxs-lookup"><span data-stu-id="f0b36-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="f0b36-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f0b36-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="f0b36-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f0b36-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="f0b36-119">您只能針對每個 VM 或角色執行個體指派一個 ILPIP。</span><span class="sxs-lookup"><span data-stu-id="f0b36-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="f0b36-120">您可以使用向上 too5 ILPIPs 每個訂閱。</span><span class="sxs-lookup"><span data-stu-id="f0b36-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="f0b36-121">ILPIP 不支援多個 NIC VM。</span><span class="sxs-lookup"><span data-stu-id="f0b36-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="f0b36-122">為什麼我要要求 ILPIP？</span><span class="sxs-lookup"><span data-stu-id="f0b36-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="f0b36-123">如果您想要 toobe 無法 tooconnect tooyour VM 或角色執行個體使用 IP 位址直接指派 tooit，而不是使用 hello 雲端服務 VIP:&lt;連接埠號碼&gt;，要求 ILPIP VM 或角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="f0b36-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="f0b36-124">**作用中 FTP** -指派 ILPIP tooa VM 後，它可以接收任何連接埠的流量。</span><span class="sxs-lookup"><span data-stu-id="f0b36-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="f0b36-125">端點不需要 hello VM tooreceive 流量。</span><span class="sxs-lookup"><span data-stu-id="f0b36-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="f0b36-126">如需 hello FTP 通訊協定的詳細資訊，請參閱 (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [FTP 通訊協定概觀]。</span><span class="sxs-lookup"><span data-stu-id="f0b36-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="f0b36-127">**輸出 IP** -源自的 hello VM 是輸出流量對應 toohello ILPIP 為 hello 來源和 hello ILPIP 唯一識別 hello VM tooexternal 實體。</span><span class="sxs-lookup"><span data-stu-id="f0b36-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="f0b36-128">在過去 hello ILPIP 位址會是參照的 tooas 公用 IP (PIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="f0b36-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="f0b36-129">管理 VM 的 ILPIP</span><span class="sxs-lookup"><span data-stu-id="f0b36-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="f0b36-130">toocreate、 指派及移除的 Vm 所傳來的 ILPIPs hello 下列工作可讓您：</span><span class="sxs-lookup"><span data-stu-id="f0b36-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="f0b36-131">如何 toorequest ILPIP 期間使用 PowerShell 建立的 VM</span><span class="sxs-lookup"><span data-stu-id="f0b36-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="f0b36-132">hello 下列 PowerShell 指令碼會建立名為雲端服務*FTPService*，從 Azure 擷取映像，建立名為 VM *FTPInstance*使用 hello 擷取映像、 設定 hello VM toouse ILPIP，並將 hello VM toohello 新服務：</span><span class="sxs-lookup"><span data-stu-id="f0b36-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="f0b36-133">如何為 vm tooretrieve ILPIP 資訊</span><span class="sxs-lookup"><span data-stu-id="f0b36-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="f0b36-134">執行下列 PowerShell 命令的 hello tooview hello hello 與 hello 至上一個指令碼，在建立 VM 的 ILPIP 資訊，並觀察 hello 值*PublicIPAddress*和*PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="f0b36-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="f0b36-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f0b36-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="f0b36-136">如何從 VM ILPIP tooremove</span><span class="sxs-lookup"><span data-stu-id="f0b36-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="f0b36-137">tooremove hello ILPIP 加入 hello 至上一個指令碼，執行下列 PowerShell 命令的 hello toohello VM:</span><span class="sxs-lookup"><span data-stu-id="f0b36-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="f0b36-138">如何 tooadd ILPIP tooan 現有的 VM</span><span class="sxs-lookup"><span data-stu-id="f0b36-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="f0b36-139">tooadd ILPIP toohello VM 建立使用 hello 指令碼之前，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f0b36-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="f0b36-140">管理雲端服務角色執行個體的 ILPIP</span><span class="sxs-lookup"><span data-stu-id="f0b36-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="f0b36-141">tooadd ILPIP tooa 雲端服務角色執行個體，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f0b36-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="f0b36-142">下載 hello.cscfg 檔案中 hello 步驟 hello 雲端服務，藉由完成 hello [tooConfigure 雲端服務如何](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg)發行項。</span><span class="sxs-lookup"><span data-stu-id="f0b36-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="f0b36-143">更新 hello.cscfg 檔案加 hello`InstanceAddress`項目。</span><span class="sxs-lookup"><span data-stu-id="f0b36-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="f0b36-144">hello 下列範例會加入名為 ILPIP *MyPublicIP* tooa 角色執行個體名為*WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="f0b36-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="f0b36-145">上傳 hello.cscfg 檔案中 hello 步驟 hello 雲端服務，藉由完成 hello [tooConfigure 雲端服務如何](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg)發行項。</span><span class="sxs-lookup"><span data-stu-id="f0b36-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0b36-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0b36-146">Next steps</span></span>
* <span data-ttu-id="f0b36-147">了解如何[IP 定址](virtual-network-ip-addresses-overview-classic.md)hello 傳統部署模型中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f0b36-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="f0b36-148">深入了解 [保留的 IP](virtual-networks-reserved-public-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="f0b36-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
