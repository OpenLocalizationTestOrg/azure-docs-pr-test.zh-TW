---
title: "Windows Azure 資源管理員範本與計算資源 aaaDeploying |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="7cbb5-103">使用適用於 Windows VM 之 Azure Resource Manager 範本的應用程式架構</span><span class="sxs-lookup"><span data-stu-id="7cbb5-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="7cbb5-104">在開發 Azure Resource Manager 部署時，計算需求需要對應的 toobe tooAzure 資源和服務。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="7cbb5-105">如果應用程式是由數個 http 端點、 資料庫和資料快取服務所組成，hello 裝載每個元件的 Azure 資源需要 toobe 合理化。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="7cbb5-106">比方說，hello 範例 Music Store 應用程式包含虛擬機器裝載的 web 應用程式和 SQL 資料庫中，裝載於 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="7cbb5-107">本文件詳述 hello Music Store 計算資源 hello 範例 Azure Resource Manager 範本中設定的方式。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="7cbb5-108">所有相依項目和獨特的設定都會以醒目提示的方式標示。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="7cbb5-109">Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="7cbb5-110">hello 完成範本可以在這裡 – 找到[音樂存放部署在 Windows 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-110">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="7cbb5-111">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7cbb5-111">Virtual Machine</span></span>
<span data-ttu-id="7cbb5-112">hello Music Store 應用程式包含 web 應用程式，其中客戶可以瀏覽及購買音樂。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="7cbb5-113">雖然有好幾個 Azure 服務可以裝載 Web 應用程式，但是這個範例是使用「虛擬機器」。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="7cbb5-114">使用 hello 範例 Music Store 範本，在部署虛擬機器、 web 伺服器安裝及 hello Music Store 網站安裝及設定。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="7cbb5-115">為了本文章的 hello 起見，hello 虛擬機器部署會詳細說明。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="7cbb5-116">hello 設定 hello web 伺服器與 hello 應用程式的更新版本的文件會詳細說明。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="7cbb5-117">虛擬機器可以加入 tooa 範本使用 hello Visual Studio 加入新資源精靈，或有效的 JSON 插入 hello 部署範本。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="7cbb5-118">部署虛擬機器時，也需要數個相關的資源。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="7cbb5-119">如果使用 Visual Studio toocreate hello 範本，則會為您建立這些資源。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="7cbb5-120">若以手動方式建構 hello 範本，這些資源需要 toobe 插入並設定。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="7cbb5-121">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器 JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

<span data-ttu-id="7cbb5-122">一旦部署之後，hello Azure 入口網站中可以看到 hello 虛擬機器內容。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![虛擬機器](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="7cbb5-124">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7cbb5-124">Storage Account</span></span>
<span data-ttu-id="7cbb5-125">儲存體帳戶有許多儲存體選項和功能。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="7cbb5-126">Hello 的 Azure 虛擬機器的內容，儲存體帳戶會保留 hello 虛擬硬碟的 hello 虛擬機器與其他所有資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="7cbb5-127">hello Music Store 範例 hello 部署中包含一個儲存體帳戶 toohold hello 虛擬硬碟的每個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="7cbb5-128">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[儲存體帳戶](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="7cbb5-129">儲存體帳戶是內 hello 資源管理員範本宣告 hello 虛擬機器的虛擬機器相關聯。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="7cbb5-130">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器與儲存體帳戶的關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="7cbb5-131">部署之後，可以在 hello Azure 入口網站中檢視 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![儲存體帳戶](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="7cbb5-133">按一下至 hello 儲存體帳戶 blob 容器中，可以看到每個虛擬機器使用 hello 範本部署的 hello 虛擬硬碟檔案。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![虛擬硬碟](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="7cbb5-135">如需有關「Azure 儲存體」的資訊，請參閱 [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="7cbb5-136">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7cbb5-136">Virtual Network</span></span>
<span data-ttu-id="7cbb5-137">如果虛擬機器需要內部網路，例如 hello 能力 toocommunicate 與其他虛擬機器和 Azure 資源，Azure 虛擬網路是必要的。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="7cbb5-138">虛擬網路不會進行 hello 虛擬機器可以透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="7cbb5-139">公用連線能力需要公用 IP 位址，本系列稍後會詳細說明。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="7cbb5-140">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬網路和子網路](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="7cbb5-141">Hello Azure 入口網站，從 hello 虛擬網路看起來像下列映像的 hello。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="7cbb5-142">請注意，使用 hello 範本部署的所有虛擬機器附加的 toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![虛擬網路](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="7cbb5-144">網路介面</span><span class="sxs-lookup"><span data-stu-id="7cbb5-144">Network Interface</span></span>
 <span data-ttu-id="7cbb5-145">網路介面正在連線的虛擬機器 tooa 虛擬網路、 更明確地說 hello 虛擬網路中已定義 tooa 子網路。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="7cbb5-146">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[網路介面](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="7cbb5-147">每個虛擬機器資源都包含一個網路設定檔。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="7cbb5-148">hello 網路介面是 hello 這個設定檔中的虛擬機器相關聯。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="7cbb5-149">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器的網路設定檔](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="7cbb5-150">Hello Azure 入口網站，從 hello 網路介面看起來像下列映像的 hello。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="7cbb5-151">hello 內部 IP 位址和 hello 虛擬機器關聯可以看見 hello 網路介面資源上。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![網路介面](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="7cbb5-153">如需有關「Azure 虛擬網路」的詳細資訊，請參閱 [Azure 虛擬網路文件](https://azure.microsoft.com/documentation/services/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="7cbb5-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7cbb5-154">Azure SQL Database</span></span>
<span data-ttu-id="7cbb5-155">此外 tooa 裝載 hello 音樂商店的網站，Azure SQL Database 的虛擬機器是部署的 toohost hello Music Store 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="7cbb5-156">這裡使用 Azure SQL Database 的 hello 優點是不是必要項目，第二組的虛擬機器，hello 服務內建延展性和可用性。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="7cbb5-157">可以使用 Visual Studio 加入新資源精靈，或藉由插入範本中的有效的 JSON hello 加入 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="7cbb5-158">hello SQL Server 資源包含使用者名稱和密碼會授與 hello SQL 執行個體上的系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="7cbb5-159">此外，也會新增 SQL 防火牆資源。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="7cbb5-160">根據預設，在 Azure 中裝載的應用程式會無法 tooconnect 與 hello SQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="7cbb5-161">tooallow 外部應用程式這類的 SQL Server Management studio tooconnect toohello SQL 執行個體，需要設定 toobe hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="7cbb5-162">Hello Music Store 示範的 hello 起見，hello 預設組態是正常的。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="7cbb5-163">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="7cbb5-164">Hello SQL server 和 MusicStore 資料庫 hello Azure 入口網站中所見的檢視。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="7cbb5-166">如需有關部署 Azure SQL Database 的詳細資訊，請參閱 [Azure SQL Database 文件](https://azure.microsoft.com/documentation/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="7cbb5-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="7cbb5-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7cbb5-167">Next step</span></span>
<hr>

[<span data-ttu-id="7cbb5-168">步驟 2 - Azure Resource Manager 範本中的存取和安全性</span><span class="sxs-lookup"><span data-stu-id="7cbb5-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

