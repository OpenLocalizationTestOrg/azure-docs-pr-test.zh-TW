---
title: "Azure 執行個體層級公用 IP (傳統) 位址 | Microsoft Docs"
description: "了解執行個體層級公用 IP (ILPIP) 位址，以及使用 PowerShell 來管理它們的方式。"
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
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="02f73-103">執行個體層級公用 IP (Classic) 概觀</span><span class="sxs-lookup"><span data-stu-id="02f73-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="02f73-104">執行個體層級公用 IP (ILPIP) 是您可以直接指派至 VM 或雲端服務角色執行個體的公用 IP 位址，而不是指派至 VM 或角色執行個體所在的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="02f73-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="02f73-105">ILPIP 不會取代指派給雲端服務的虛擬 IP (VIP)。</span><span class="sxs-lookup"><span data-stu-id="02f73-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="02f73-106">應該說是您可以用來直接連接到 VM 或角色執行個體的其他 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="02f73-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02f73-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="02f73-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="02f73-108">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="02f73-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="02f73-109">Microsoft 建議您透過 Resource Manager 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="02f73-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="02f73-110">請確定您了解 [IP 位址](virtual-network-ip-addresses-overview-classic.md) 在 Azure 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="02f73-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![ILPIP 和 VIP 之間的差異](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="02f73-112">如圖 1 所示，儘管通常是使用 VIP:&lt;連接埠號碼&gt; 來存取個別 VM，但還是會使用 VIP 來存取雲端服務。</span><span class="sxs-lookup"><span data-stu-id="02f73-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="02f73-113">將 ILPIP 指派給特定的 VM，就能直接使用該 IP 位址來存取 VM。</span><span class="sxs-lookup"><span data-stu-id="02f73-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="02f73-114">當您在 Azure 中建立雲端服務時，對應的 DNS A 記錄即會自動建立，以允許透過完整格式的網域名稱 (FQDN) 存取服務，而不需使用實際的 VIP。</span><span class="sxs-lookup"><span data-stu-id="02f73-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="02f73-115">相同程序也適用於 ILPIP，但可改為透過 FQDN 而不是 ILPIP 來允許存取 VM 或角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="02f73-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="02f73-116">例如，若您建立名為 *contosoadservice* 的雲端服務，並設定名為 *contosoweb* 且具有兩個執行個體的 Web 角色，Azure 將會為那些執行個體登錄下列 A 記錄：</span><span class="sxs-lookup"><span data-stu-id="02f73-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="02f73-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="02f73-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="02f73-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="02f73-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="02f73-119">您只能針對每個 VM 或角色執行個體指派一個 ILPIP。</span><span class="sxs-lookup"><span data-stu-id="02f73-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="02f73-120">您可以針對每個訂用帳戶最多使用 5 個 ILPIP。</span><span class="sxs-lookup"><span data-stu-id="02f73-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="02f73-121">ILPIP 不支援多個 NIC VM。</span><span class="sxs-lookup"><span data-stu-id="02f73-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="02f73-122">為什麼我要要求 ILPIP？</span><span class="sxs-lookup"><span data-stu-id="02f73-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="02f73-123">如果想要透過直接指派 IP 位址的方式連接到 VM 或角色執行個體，而不是使用雲端服務 VIP:&lt;連接埠號碼&gt;，請為 VM 或角色執行個體要求 ILPIP。</span><span class="sxs-lookup"><span data-stu-id="02f73-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="02f73-124">**主動式 FTP**：透過將 ILPIP 指派給 VM，VM 就可以在所有的連接埠上接收流量。</span><span class="sxs-lookup"><span data-stu-id="02f73-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="02f73-125">VM 不需要端點就可以接收流量。</span><span class="sxs-lookup"><span data-stu-id="02f73-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="02f73-126">請參閱 (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP 通訊協定概觀 (英文)] 以取得 FTP 通訊協定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02f73-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="02f73-127">**輸出 IP**：源自 VM 的輸出流量會對應至 ILPIP，因為來源與 ILPIP 可向外部實體唯一識別 VM。</span><span class="sxs-lookup"><span data-stu-id="02f73-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="02f73-128">ILPIP 過去被稱為公用 IP (PIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="02f73-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="02f73-129">管理 VM 的 ILPIP</span><span class="sxs-lookup"><span data-stu-id="02f73-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="02f73-130">下列工作可讓您建立、指派和移除 VM 的 ILPIP：</span><span class="sxs-lookup"><span data-stu-id="02f73-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="02f73-131">如何在建立 VM 期間使用 PowerShell 要求 ILPIP</span><span class="sxs-lookup"><span data-stu-id="02f73-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="02f73-132">下列 PowerShell 指令碼會建立名為 *FTPService* 的雲端服務、從 Azure 擷取映像、使用擷取的映像建立名為 *FTPInstance* 的 VM、設定要使用 ILPIP 的 VM，以及將 VM 加入新服務：</span><span class="sxs-lookup"><span data-stu-id="02f73-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="02f73-133">如何擷取 VM 的 ILPIP 資訊</span><span class="sxs-lookup"><span data-stu-id="02f73-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="02f73-134">若要檢視使用上述指令碼所建立 VM 的 ILPIP 資訊，請執行下列 PowerShell 命令，並觀察 *PublicIPAddress* 和 *PublicIPName* 的值：</span><span class="sxs-lookup"><span data-stu-id="02f73-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="02f73-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="02f73-135">Expected output:</span></span>
 
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

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="02f73-136">如何從 VM 移除 ILPIP</span><span class="sxs-lookup"><span data-stu-id="02f73-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="02f73-137">若要移除在上述指令碼中加入 VM 的 ILPIP，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="02f73-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="02f73-138">如何將 ILPIP 加入現有的 VM</span><span class="sxs-lookup"><span data-stu-id="02f73-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="02f73-139">若要將 ILPIP 加入至使用上述指令碼建立的 VM，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="02f73-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="02f73-140">管理雲端服務角色執行個體的 ILPIP</span><span class="sxs-lookup"><span data-stu-id="02f73-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="02f73-141">若要將 ILPIP 加入至雲端服務角色執行個體，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="02f73-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="02f73-142">完成[如何設定雲端服務](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg)文章中的步驟，以下載雲端服務的 .cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="02f73-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="02f73-143">加入 `InstanceAddress` 元素來更新 .cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="02f73-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="02f73-144">下列範例會加入一個名稱為 *MyPublicIP* 的 ILPIP 到名稱為 *WebRole1* 的角色執行個體：</span><span class="sxs-lookup"><span data-stu-id="02f73-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="02f73-145">完成[如何設定雲端服務](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg)文章中的步驟，以上傳雲端服務的 .cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="02f73-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02f73-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02f73-146">Next steps</span></span>
* <span data-ttu-id="02f73-147">了解 [IP 位址](virtual-network-ip-addresses-overview-classic.md) 在傳統部署模型中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="02f73-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="02f73-148">深入了解 [保留的 IP](virtual-networks-reserved-public-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="02f73-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
