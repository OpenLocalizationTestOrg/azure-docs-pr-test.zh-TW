---
title: "使用 Azure Resource Manager 範本部署 Windows 計算資源 | Microsoft Docs"
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
ms.openlocfilehash: 8a8b888195e52ea9669922a6a00a873025f3c375
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="ac729-103">使用適用於 Windows VM 之 Azure Resource Manager 範本的應用程式架構</span><span class="sxs-lookup"><span data-stu-id="ac729-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="ac729-104">開發 Azure Resource Manager 部署時，必須將計算需求與 Azure 資源和服務對應。</span><span class="sxs-lookup"><span data-stu-id="ac729-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="ac729-105">如果應用程式是由數個 http 端點、一個資料庫及一個資料快取服務所組成，就必須將裝載這當中每個元件的 Azure 資源合理化。</span><span class="sxs-lookup"><span data-stu-id="ac729-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="ac729-106">例如，範例「音樂市集」應用程式包含一個裝載於虛擬機器上的 Web 應用程式，以及一個裝載於 Azure SQL Database 中的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ac729-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="ac729-107">本文件詳細說明範例 Azure Resource Manager 範本中如何設定「音樂市集」計算資源。</span><span class="sxs-lookup"><span data-stu-id="ac729-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="ac729-108">所有相依項目和獨特的設定都會以醒目提示的方式標示。</span><span class="sxs-lookup"><span data-stu-id="ac729-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="ac729-109">為了獲得最佳體驗，請將一個解決方案執行個體預先部署到您的 Azure 訂用帳戶，然後與 Azure Resource Manager 範本搭配運作。</span><span class="sxs-lookup"><span data-stu-id="ac729-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="ac729-110">您可以在下列連結找到完整的範本 – [Windows 上的音樂市集部署](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。</span><span class="sxs-lookup"><span data-stu-id="ac729-110">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="ac729-111">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ac729-111">Virtual Machine</span></span>
<span data-ttu-id="ac729-112">「音樂市集」應用程式包含一個可供客戶瀏覽和購買音樂的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac729-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="ac729-113">雖然有好幾個 Azure 服務可以裝載 Web 應用程式，但是這個範例是使用「虛擬機器」。</span><span class="sxs-lookup"><span data-stu-id="ac729-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="ac729-114">使用範例「音樂市集」範本時，會部署虛擬機器、安裝 Web 伺服器，以及安裝並設定「音樂市集」網站。</span><span class="sxs-lookup"><span data-stu-id="ac729-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="ac729-115">針對本文，只會詳細說明虛擬機器部署。</span><span class="sxs-lookup"><span data-stu-id="ac729-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="ac729-116">Web 伺服器和應用程式的組態在稍後的文章中會有詳細說明。</span><span class="sxs-lookup"><span data-stu-id="ac729-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="ac729-117">您可以透過使用 Visual Studio 的「加入新資源」精靈或在部署範本中插入有效的 JSON，將虛擬機器新增至範本。</span><span class="sxs-lookup"><span data-stu-id="ac729-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="ac729-118">部署虛擬機器時，也需要數個相關的資源。</span><span class="sxs-lookup"><span data-stu-id="ac729-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="ac729-119">如果使用 Visual Studio 來建立範本，就會為您建立這些資源。</span><span class="sxs-lookup"><span data-stu-id="ac729-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="ac729-120">如果以手動方式建構範本，則需要插入及設定這些資源。</span><span class="sxs-lookup"><span data-stu-id="ac729-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="ac729-121">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [虛擬機器 JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285)。</span><span class="sxs-lookup"><span data-stu-id="ac729-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

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

<span data-ttu-id="ac729-122">部署之後，就可以在 Azure 入口網站中看到虛擬機器屬性。</span><span class="sxs-lookup"><span data-stu-id="ac729-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![虛擬機器](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="ac729-124">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ac729-124">Storage Account</span></span>
<span data-ttu-id="ac729-125">儲存體帳戶有許多儲存體選項和功能。</span><span class="sxs-lookup"><span data-stu-id="ac729-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="ac729-126">就 Azure 虛擬機器的內容而言，儲存體帳戶會保有虛擬機器和任何其他資料磁碟的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="ac729-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="ac729-127">「音樂市集」範例包含一個儲存體帳戶，其中保有部署中每個虛擬機器的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="ac729-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="ac729-128">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [儲存體帳戶](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98)。</span><span class="sxs-lookup"><span data-stu-id="ac729-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

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

<span data-ttu-id="ac729-129">儲存體帳戶會在虛擬機器的 Resource Manager 範本宣告內與虛擬機器關聯。</span><span class="sxs-lookup"><span data-stu-id="ac729-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="ac729-130">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [虛擬機器與儲存體帳戶關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321)。</span><span class="sxs-lookup"><span data-stu-id="ac729-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

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

<span data-ttu-id="ac729-131">部署之後，即可在 Azure 入口網站中檢視儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac729-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![儲存體帳戶](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="ac729-133">按一下來進入儲存體帳戶 Blob 容器，即可看到以範本部署之每個虛擬機器的虛擬硬碟檔案。</span><span class="sxs-lookup"><span data-stu-id="ac729-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![虛擬硬碟](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="ac729-135">如需有關「Azure 儲存體」的資訊，請參閱 [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="ac729-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="ac729-136">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ac729-136">Virtual Network</span></span>
<span data-ttu-id="ac729-137">如果虛擬機器需要內部網路功能 (例如與其他虛擬機器及 Azure 資源進行通訊的能力)，就需要「Azure 虛擬網路」。</span><span class="sxs-lookup"><span data-stu-id="ac729-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="ac729-138">虛擬網路不會讓虛擬機器變成可透過網際網路存取的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ac729-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="ac729-139">公用連線能力需要公用 IP 位址，本系列稍後會詳細說明。</span><span class="sxs-lookup"><span data-stu-id="ac729-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="ac729-140">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [虛擬網路和子網路](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126)。</span><span class="sxs-lookup"><span data-stu-id="ac729-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

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

<span data-ttu-id="ac729-141">在 Azure 入口網站中，虛擬網路看起來會像下圖。</span><span class="sxs-lookup"><span data-stu-id="ac729-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="ac729-142">請注意，以範本部署的所有虛擬機器會都連接至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ac729-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![虛擬網路](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="ac729-144">網路介面</span><span class="sxs-lookup"><span data-stu-id="ac729-144">Network Interface</span></span>
 <span data-ttu-id="ac729-145">網路介面會將虛擬機器連接到虛擬網路，更具體來說，是連接到虛擬網路中已定義的子網路。</span><span class="sxs-lookup"><span data-stu-id="ac729-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="ac729-146">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [網路介面](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156)。</span><span class="sxs-lookup"><span data-stu-id="ac729-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

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

<span data-ttu-id="ac729-147">每個虛擬機器資源都包含一個網路設定檔。</span><span class="sxs-lookup"><span data-stu-id="ac729-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="ac729-148">網路介面是在此設定檔中與虛擬機器關聯。</span><span class="sxs-lookup"><span data-stu-id="ac729-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="ac729-149">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [虛擬機器網路設定檔](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330)。</span><span class="sxs-lookup"><span data-stu-id="ac729-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="ac729-150">在 Azure 入口網站中，網路介面看起來會像下圖。</span><span class="sxs-lookup"><span data-stu-id="ac729-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="ac729-151">您可以在網路介面資源上看到內部 IP 位址與虛擬機器關聯。</span><span class="sxs-lookup"><span data-stu-id="ac729-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![網路介面](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="ac729-153">如需有關「Azure 虛擬網路」的詳細資訊，請參閱 [Azure 虛擬網路文件](https://azure.microsoft.com/documentation/services/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="ac729-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="ac729-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ac729-154">Azure SQL Database</span></span>
<span data-ttu-id="ac729-155">除了裝載「音樂市集」網站的虛擬機器之外，也會部署 Azure SQL Database 來裝載「音樂市集」資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac729-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="ac729-156">在這裡，使用 Azure SQL Database 的好處在於不需要第二組虛擬機器，且規模和可用性皆已內建於服務中。</span><span class="sxs-lookup"><span data-stu-id="ac729-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="ac729-157">您可以透過使用 Visual Studio 的「加入新資源」精靈或在範本中插入有效的 JSON，來新增 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ac729-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="ac729-158">SQL Server 資源包括已獲授與 SQL 執行個體上系統管理權限的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="ac729-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="ac729-159">此外，也會新增 SQL 防火牆資源。</span><span class="sxs-lookup"><span data-stu-id="ac729-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="ac729-160">裝載在 Azure 中的應用程式預設即能夠與 SQL 執行個體連線。</span><span class="sxs-lookup"><span data-stu-id="ac729-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="ac729-161">若要允許外部應用程式 (例如 SQL Server Management Studio) 連線到 SQL 執行個體，就必須設定防火牆。</span><span class="sxs-lookup"><span data-stu-id="ac729-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="ac729-162">就「音樂市集」示範而言，無須變更預設組態。</span><span class="sxs-lookup"><span data-stu-id="ac729-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="ac729-163">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379)。</span><span class="sxs-lookup"><span data-stu-id="ac729-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

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

<span data-ttu-id="ac729-164">Azure 入口網站中所示的 SQL Server 和 MusicStore 資料庫檢視。</span><span class="sxs-lookup"><span data-stu-id="ac729-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="ac729-166">如需有關部署 Azure SQL Database 的詳細資訊，請參閱 [Azure SQL Database 文件](https://azure.microsoft.com/documentation/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="ac729-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="ac729-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac729-167">Next step</span></span>
<hr>

[<span data-ttu-id="ac729-168">步驟 2 - Azure Resource Manager 範本中的存取和安全性</span><span class="sxs-lookup"><span data-stu-id="ac729-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

