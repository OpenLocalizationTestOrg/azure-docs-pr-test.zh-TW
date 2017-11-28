---
title: "使用虛擬機器擴充功能將應用程式部署自動化 | Microsoft Docs"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="4bfec-103">使用適用於 Linux VM 的 Azure Resource Manager 範本進行應用程式部署</span><span class="sxs-lookup"><span data-stu-id="4bfec-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="4bfec-104">識別出所有 Azure 基礎結構需求並轉譯成部署範本之後，就必須處理實際的應用程式部署需求。</span><span class="sxs-lookup"><span data-stu-id="4bfec-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="4bfec-105">這裡的應用程式部署係指將實際的應用程式二進位檔安裝到 Azure 資源上。</span><span class="sxs-lookup"><span data-stu-id="4bfec-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="4bfec-106">以「音樂市集」範例來說，必須在每一部虛擬機器上安裝並設定 .Net 核心、NGINX 及監督員。</span><span class="sxs-lookup"><span data-stu-id="4bfec-106">For the Music Store sample, .Net Core, NGINX, and Supervisor need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="4bfec-107">必須將「音樂市集」二進位檔安裝到虛擬機器上，並且必須預先建立「音樂市集」資料庫。</span><span class="sxs-lookup"><span data-stu-id="4bfec-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="4bfec-108">本文件詳細說明「虛擬機器」擴充功能如何將 Azure 虛擬機器的應用程式部署和設定自動化。</span><span class="sxs-lookup"><span data-stu-id="4bfec-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="4bfec-109">所有相依項目和獨特的設定都會以醒目提示的方式標示。</span><span class="sxs-lookup"><span data-stu-id="4bfec-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="4bfec-110">為了獲得最佳體驗，請將一個解決方案執行個體預先部署到您的 Azure 訂用帳戶，然後與 Azure Resource Manager 範本搭配運作。</span><span class="sxs-lookup"><span data-stu-id="4bfec-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="4bfec-111">您可以在下列連結找到完整的範本 – [Ubuntu 上的音樂市集部署](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。</span><span class="sxs-lookup"><span data-stu-id="4bfec-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="4bfec-112">組態指令碼</span><span class="sxs-lookup"><span data-stu-id="4bfec-112">Configuration script</span></span>
<span data-ttu-id="4bfec-113">「虛擬機器」擴充功能是針對虛擬機器執行以提供組態自動化的特製化程式。</span><span class="sxs-lookup"><span data-stu-id="4bfec-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="4bfec-114">針對許多特定用途 (防毒、記錄組態及 Docker 組態) 都有擴充功能可供使用。</span><span class="sxs-lookup"><span data-stu-id="4bfec-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="4bfec-115">自訂指令碼擴充功能可以用來對虛擬機器執行任何指令碼。</span><span class="sxs-lookup"><span data-stu-id="4bfec-115">A custom script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="4bfec-116">在「音樂市集」範例中，需仰賴自訂指令碼擴充功能來設定 Ubuntu 虛擬機器及安裝「音樂市集」應用程式。</span><span class="sxs-lookup"><span data-stu-id="4bfec-116">With the Music Store sample, it is up to the custom script extension to configure the Ubuntu virtual machines and install the Music Store application.</span></span> 

<span data-ttu-id="4bfec-117">在詳細說明如何在 Azure Resource Manager 範本中宣告虛擬機器擴充功能之前，請先檢查所執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="4bfec-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="4bfec-118">此指令碼會設定 Ubuntu 虛擬機器以裝載「音樂市集」應用程式。</span><span class="sxs-lookup"><span data-stu-id="4bfec-118">This script configures the Ubuntu virtual machine to host the Music Store application.</span></span> <span data-ttu-id="4bfec-119">在執行時，指令碼會安裝所有必要的軟體、從原始檔控制安裝「音樂市集」應用程式，以及準備資料庫。</span><span class="sxs-lookup"><span data-stu-id="4bfec-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

<span data-ttu-id="4bfec-120">若要深入了解如何在 Linux 上裝載 .Net 核心應用程式，請參閱 [Publish to a Linux Production Environment (發佈至 Linux 生產環境)](https://docs.asp.net/en/latest/publishing/linuxproduction.html)。</span><span class="sxs-lookup"><span data-stu-id="4bfec-120">To learn more about hosting a .Net Core application on Linux, see [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="4bfec-121">此範例僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="4bfec-121">This sample is for demonstration purposes.</span></span>
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a><span data-ttu-id="4bfec-122">VM 指令碼擴充功能</span><span class="sxs-lookup"><span data-stu-id="4bfec-122">VM Script Extension</span></span>
<span data-ttu-id="4bfec-123">透過將擴充功能資源包含在 Azure Resource Manager 範本中，即可在建置階段對虛擬機器執行「VM 指令碼擴充功能」。</span><span class="sxs-lookup"><span data-stu-id="4bfec-123">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="4bfec-124">您可以使用 Visual Studio 的「加入新資源」精靈或在範本中插入有效的 JSON，來新增擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4bfec-124">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="4bfec-125">「指令碼擴充功能」資源內嵌在「虛擬機器」資源的巢狀結構中；在下列範例中即可看到此情況。</span><span class="sxs-lookup"><span data-stu-id="4bfec-125">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="4bfec-126">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [VM 指令碼擴充功能](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359)。</span><span class="sxs-lookup"><span data-stu-id="4bfec-126">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="4bfec-127">請注意，在下列 JSON 中，指令碼是儲存在 GitHub。</span><span class="sxs-lookup"><span data-stu-id="4bfec-127">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="4bfec-128">此指令碼也可以儲存在 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="4bfec-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="4bfec-129">此外，Azure Resource Manager 範本也允許建構指令碼執行字串，讓範本參數值可被用來當作指令碼執行參數。</span><span class="sxs-lookup"><span data-stu-id="4bfec-129">Also, Azure Resource Manager templates allow the script execution string to constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="4bfec-130">在此案例中，是在部署範本時提供資料，接著在執行指令碼時，就可以使用這些值。</span><span class="sxs-lookup"><span data-stu-id="4bfec-130">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="4bfec-131">如需有關使用自訂指令碼擴充功能的詳細資訊，請參閱 [使用 Resource Manager 範本來自訂指令碼擴充功能](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4bfec-131">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="4bfec-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bfec-132">Next Step</span></span>
<hr>

[<span data-ttu-id="4bfec-133">探索其他 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="4bfec-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

