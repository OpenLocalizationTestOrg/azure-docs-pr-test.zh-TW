---
title: "Azure 快速入門 - 建立 VM CLI | Microsoft Docs"
description: "快速了解如何使用 Azure CLI 建立虛擬機器。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a7cba5b2c43704d92e36d6f808efaa9fc73fdf36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="9df39-103">使用 Azure CLI 建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9df39-103">Create a Linux virtual machine with the Azure CLI</span></span>

<span data-ttu-id="9df39-104">Azure CLI 可用來從命令列或在指令碼中建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="9df39-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="9df39-105">本指南詳細說明如何使用 Azure CLI 來部署執行 Ubuntu 伺服器的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9df39-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="9df39-106">一旦部署伺服器，就會建立 SSH 連線，以及安裝 NGINX Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9df39-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="9df39-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="9df39-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9df39-108">如果您選擇在本機安裝和使用 CLI，本快速入門會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9df39-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9df39-109">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="9df39-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="9df39-110">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="9df39-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="9df39-111">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="9df39-111">Create a resource group</span></span>

<span data-ttu-id="9df39-112">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="9df39-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9df39-113">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="9df39-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="9df39-114">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9df39-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="9df39-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="9df39-115">Create virtual machine</span></span>

<span data-ttu-id="9df39-116">使用 [az vm create](/cli/azure/vm#create) 命令來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="9df39-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="9df39-117">下列範例會建立名為 myVM 的 VM，並建立 SSH 金鑰 (如果它們不存在於預設金鑰位置)。</span><span class="sxs-lookup"><span data-stu-id="9df39-117">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="9df39-118">若要使用一組特定金鑰，請使用 `--ssh-key-value` 選項。</span><span class="sxs-lookup"><span data-stu-id="9df39-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="9df39-119">建立 VM 後，Azure CLI 會顯示類似下列範例的資訊。</span><span class="sxs-lookup"><span data-stu-id="9df39-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="9df39-120">記下 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="9df39-120">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="9df39-121">此位址用來存取 VM。</span><span class="sxs-lookup"><span data-stu-id="9df39-121">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="9df39-122">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="9df39-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="9df39-123">依預設只能透過 SSH 連線至 Azure 中部署的 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9df39-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="9df39-124">如果此 VM 即將成為 Web 伺服器，您需要從網際網路開啟連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="9df39-124">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="9df39-125">使用 [az vm open-port](/cli/azure/vm#open-port) 命令來開啟所需的連接埠。</span><span class="sxs-lookup"><span data-stu-id="9df39-125">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="9df39-126">透過 SSH 連線到您的 VM</span><span class="sxs-lookup"><span data-stu-id="9df39-126">SSH into your VM</span></span>

<span data-ttu-id="9df39-127">使用下列命令，建立與虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9df39-127">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="9df39-128">務必以虛擬機器的正確公用 IP 位址取代 *<publicIpAddress>*。</span><span class="sxs-lookup"><span data-stu-id="9df39-128">Make sure to replace *<publicIpAddress>* with the correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="9df39-129">在上面的範例中，我們的 IP 位址是 40.68.254.142。</span><span class="sxs-lookup"><span data-stu-id="9df39-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="9df39-130">安裝 NGINX</span><span class="sxs-lookup"><span data-stu-id="9df39-130">Install NGINX</span></span>

<span data-ttu-id="9df39-131">使用下列 bash 指令碼來更新套件來源及安裝最新的 NGINX 套件。</span><span class="sxs-lookup"><span data-stu-id="9df39-131">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="9df39-132">檢視 NGINX 歡迎使用頁面</span><span class="sxs-lookup"><span data-stu-id="9df39-132">View the NGINX welcome page</span></span>

<span data-ttu-id="9df39-133">安裝 NGINX 後，現在經由網際網路在您的 VM 上開啟連接埠 80 - 您可以使用所選的網頁瀏覽器來檢視預設 NGINX 歡迎使用畫面。</span><span class="sxs-lookup"><span data-stu-id="9df39-133">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="9df39-134">請務必使用您上面記載的 publicIpAddress 來瀏覽預設網頁。</span><span class="sxs-lookup"><span data-stu-id="9df39-134">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="9df39-136">清除資源</span><span class="sxs-lookup"><span data-stu-id="9df39-136">Clean up resources</span></span>

<span data-ttu-id="9df39-137">若不再需要，您可以使用 [az group delete](/cli/azure/group#delete) 命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="9df39-137">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="9df39-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9df39-138">Next steps</span></span>

<span data-ttu-id="9df39-139">在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9df39-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="9df39-140">若要深入了解 Azure 虛擬機器，請繼續 Linux VM 的教學課程。</span><span class="sxs-lookup"><span data-stu-id="9df39-140">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="9df39-141">Azure Linux 虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="9df39-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
