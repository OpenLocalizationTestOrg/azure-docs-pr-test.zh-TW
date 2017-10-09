---
title: "aaaUse hello Azure Docker VM 擴充功能 |Microsoft 文件"
description: "了解如何 toouse hello Docker VM 擴充功能 tooquickly 安全地部署在 Azure 中使用資源管理員範本 Docker 環境及和 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="1a0e0-103">使用 hello Docker VM 擴充功能在 Azure 中建立 Docker 環境</span><span class="sxs-lookup"><span data-stu-id="1a0e0-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="1a0e0-104">Docker 是常用的容器管理和映像的平台，可讓您在 Linux 上的 tooquickly 工作與容器。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="1a0e0-105">在 Azure 中，有各種方式，您可以部署 Docker 根據 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="1a0e0-106">本文著重在 hello Docker VM 擴充功能和 Azure 資源管理員範本 hello Azure CLI 2.0 使用。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="1a0e0-107">您也可以執行下列步驟以 hello [Azure CLI 1.0](dockerextension-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="1a0e0-108">Azure Docker VM 延伸模組概觀</span><span class="sxs-lookup"><span data-stu-id="1a0e0-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="1a0e0-109">hello Azure Docker VM 擴充功能中安裝和設定 hello Docker 精靈、 Docker 用戶端，和 Docker Compose Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="1a0e0-110">藉由使用 hello Azure Docker VM 擴充功能，您有更多的控制與比只需使用 Docker 機器，或自行建立 hello Docker 主機的功能。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="1a0e0-111">這些其他功能，例如[Docker Compose](https://docs.docker.com/compose/overview/)，建立適用於更穩固的開發人員或實際執行環境的 hello Azure Docker VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="1a0e0-112">如需有關 hello 不同部署方法，包括使用 Docker 機器和 Azure 容器服務，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="1a0e0-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="1a0e0-113">tooquickly 原型應用程式，您可以建立單一的 Docker 主機使用[Docker 機器](docker-machine.md)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="1a0e0-114">toobuild 備妥、 可擴充式環境中提供其他的排程和管理工具，您可以部署[Azure 容器服務上的 Docker Swarm 叢集](../../container-service/dcos-swarm/container-service-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="1a0e0-115">部署具有 hello Azure Docker VM 擴充功能的範本</span><span class="sxs-lookup"><span data-stu-id="1a0e0-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="1a0e0-116">讓我們來使用現有的快速入門範本 toocreate 使用 hello Azure Docker VM 擴充功能 tooinstall Ubuntu VM，並設定 hello Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="1a0e0-117">您可以檢視以下 hello 範本：[簡單 Ubuntu VM 部署使用 Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="1a0e0-118">您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1a0e0-119">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1a0e0-120">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *uswest*位置：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="1a0e0-121">接下來，部署具有 VM [az 群組部署建立](/cli/azure/group/deployment#create)包含 hello Azure Docker VM 擴充功能，從[GitHub 上的此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="1a0e0-122">針對 newStorageAccountName、adminUsername、adminPassword 和 dnsNameForPublicIP 提供您自己的值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="1a0e0-123">花幾分鐘，讓 hello 部署 toofinish。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="1a0e0-124">在 hello 部署完成時，[移動 toonext 步驟](#deploy-your-first-nginx-container)tooSSH tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="1a0e0-125">（選擇性） tooinstead 傳回控制 toohello 提示與 hello 可讓的部署於 hello 背景繼續執行新增 hello `--no-wait` toohello 命令的前面加上旗標。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="1a0e0-126">此程序可讓您 tooperform hello CLI 時在幾分鐘後會繼續進行 hello 部署中的其他工作。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="1a0e0-127">然後，您可以檢視與 hello Docker 主機狀態的詳細[az vm 顯示](/cli/azure/vm#show)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="1a0e0-128">hello 下列範例會檢查 hello 狀態 hello 名為 VM *myDockerVM* （hello hello 範本中的預設名稱-不要變更這個名稱） 在 hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1a0e0-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="1a0e0-129">此命令會傳回當*Succeeded*hello 部署已完成，您可以在 hello 步驟之後的 SSH toohello VM。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="1a0e0-130">部署您的第一個 nginx 容器</span><span class="sxs-lookup"><span data-stu-id="1a0e0-130">Deploy your first nginx container</span></span>
<span data-ttu-id="1a0e0-131">tooview 詳細資料，您的 VM，包括 hello DNS 名稱，使用`az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="1a0e0-132">SSH tooyour 新的 Docker 主機從本機電腦，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="1a0e0-133">登入 toohello Docker 主機之後，我們先執行 nginx 容器：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="1a0e0-134">hello 輸出是下載 hello nginx 映像時，下列範例類似 toohello 和啟動容器：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="1a0e0-135">檢查您的 Docker 主機上執行的如下所示的 hello 容器 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="1a0e0-136">hello 輸出是下列範例類似 toohello，顯示該 hello nginx 容器正在執行且 TCP 連接埠 80 和 443，被轉送：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="1a0e0-137">toosee 您的容器，在動作中，開啟網頁瀏覽器並輸入您的 Docker 主機 hello DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![執行 ngnix 容器](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="1a0e0-139">Azure Docker VM 延伸模組範本參考</span><span class="sxs-lookup"><span data-stu-id="1a0e0-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="1a0e0-140">hello 前一個範例會使用現有的快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="1a0e0-141">您也可以使用您自己的資源管理員範本部署 hello Azure Docker VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="1a0e0-142">toodo，加入下列 tooyour 資源管理員範本，定義 hello hello `vmName` VM 的適當地：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="1a0e0-143">如需更詳細的 Resource Manager 範本使用逐步解說，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a0e0-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a0e0-144">Next steps</span></span>
<span data-ttu-id="1a0e0-145">您可能會希望太[設定 hello Docker daemon TCP 通訊埠](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket)，了解[Docker 安全性](https://docs.docker.com/engine/security/security/)，部署使用的容器或[Docker Compose](https://docs.docker.com/compose/overview/)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="1a0e0-146">如需有關 hello Azure Docker VM 擴充功能本身的詳細資訊，請參閱 hello [GitHub 專案](https://github.com/Azure/azure-docker-extension/)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="1a0e0-147">閱讀有關 hello 其他 Docker 部署 Azure 中的選項的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="1a0e0-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="1a0e0-148">使用 Docker 電腦以 hello Azure 驅動程式</span><span class="sxs-lookup"><span data-stu-id="1a0e0-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="1a0e0-149">[開始使用 Docker 和撰寫 toodefine 和 Azure 虛擬機器上執行多個容器應用程式](docker-compose-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="1a0e0-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="1a0e0-150">部署 Azure 容器服務叢集</span><span class="sxs-lookup"><span data-stu-id="1a0e0-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

