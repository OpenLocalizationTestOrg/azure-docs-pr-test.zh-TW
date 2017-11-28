---
title: "快速入門-aaaAzure 建立 VM CLI |Microsoft 文件"
description: "快速了解以 hello Azure CLI toocreate 虛擬機器。"
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
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="00920-103">建立 Linux 虛擬機器以 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="00920-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="00920-104">hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="00920-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="00920-105">本指南將詳細說明使用 hello Azure CLI toodeploy 執行 Ubuntu server 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="00920-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="00920-106">Hello 伺服器部署之後，建立 SSH 連線，以及 NGINX 網頁伺服器已安裝。</span><span class="sxs-lookup"><span data-stu-id="00920-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="00920-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="00920-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="00920-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="00920-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="00920-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="00920-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="00920-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="00920-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="00920-111">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="00920-111">Create a resource group</span></span>

<span data-ttu-id="00920-112">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="00920-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="00920-113">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="00920-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="00920-114">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="00920-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="00920-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="00920-115">Create virtual machine</span></span>

<span data-ttu-id="00920-116">建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="00920-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="00920-117">hello 下列範例會建立名為的 VM *myVM*並建立 SSH 金鑰，如果它們原本不在預設索引鍵位置。</span><span class="sxs-lookup"><span data-stu-id="00920-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="00920-118">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="00920-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="00920-119">建立 hello VM 後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="00920-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="00920-120">記下 hello `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="00920-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="00920-121">此位址為使用的 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="00920-121">This address is used tooaccess hello VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="00920-122">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="00920-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="00920-123">依預設只能透過 SSH 連線至 Azure 中部署的 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="00920-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="00920-124">如果此 VM 將會 toobe web 伺服器，您需要從網際網路 hello tooopen 連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="00920-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="00920-125">使用 hello [az vm 開啟通訊埠](/cli/azure/vm#open-port)命令 tooopen hello 所需的連接埠。</span><span class="sxs-lookup"><span data-stu-id="00920-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="00920-126">透過 SSH 連線到您的 VM</span><span class="sxs-lookup"><span data-stu-id="00920-126">SSH into your VM</span></span>

<span data-ttu-id="00920-127">使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="00920-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="00920-128">請確定 tooreplace  *<publicIpAddress>*  hello 包含正確的虛擬機器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="00920-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="00920-129">在上面的範例中，我們的 IP 位址是 40.68.254.142。</span><span class="sxs-lookup"><span data-stu-id="00920-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="00920-130">安裝 NGINX</span><span class="sxs-lookup"><span data-stu-id="00920-130">Install NGINX</span></span>

<span data-ttu-id="00920-131">使用 hello 以下撞指令碼 tooupdate 封裝來源，並安裝最新 NGINX 套件 hello。</span><span class="sxs-lookup"><span data-stu-id="00920-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="00920-132">檢視 hello NGINX 歡迎使用 頁面</span><span class="sxs-lookup"><span data-stu-id="00920-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="00920-133">現在從 hello 網際網路-VM 上開啟連接埠 80 與 NGINX 安裝中，您可以使用網頁瀏覽器，您的選擇 tooview hello 預設 NGINX 歡迎頁面。</span><span class="sxs-lookup"><span data-stu-id="00920-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="00920-134">要確定 toouse hello *publicIpAddress*您 toovisit hello 預設頁面上面所記載。</span><span class="sxs-lookup"><span data-stu-id="00920-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="00920-136">清除資源</span><span class="sxs-lookup"><span data-stu-id="00920-136">Clean up resources</span></span>

<span data-ttu-id="00920-137">當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 VM 和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="00920-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="00920-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00920-138">Next steps</span></span>

<span data-ttu-id="00920-139">在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="00920-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="00920-140">進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="00920-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="00920-141">Azure Linux 虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="00920-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
