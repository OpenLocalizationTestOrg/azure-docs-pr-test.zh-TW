---
title: "使用 Azure Docker VM 延伸模組 | Microsoft Docs"
description: "了解如何使用 Resource Manager 範本和 Azure CLI 2.0，在 Azure 中使用 Docker VM 延伸模組快速而安全地部署 Docker 環境"
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
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="1e511-103">使用 Docker VM 延伸模組在 Azure 中建立 Docker 環境</span><span class="sxs-lookup"><span data-stu-id="1e511-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="1e511-104">Docker 是常用的容器管理和映像處理平台，它能讓您在 Linux 上快速地操作容器。</span><span class="sxs-lookup"><span data-stu-id="1e511-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="1e511-105">在 Azure 中，您可以根據您的需求使用幾個方式來部署 Docker。</span><span class="sxs-lookup"><span data-stu-id="1e511-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="1e511-106">本文著重於搭配 Azure CLI 2.0 使用 Docker VM 延伸模組與 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="1e511-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="1e511-107">您也可以使用 [Azure CLI 1.0](dockerextension-nodejs.md) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="1e511-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="1e511-108">Azure Docker VM 延伸模組概觀</span><span class="sxs-lookup"><span data-stu-id="1e511-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="1e511-109">Azure Docker VM 擴充功能會在您的 Linux 虛擬機器 (VM) 中安裝並設定 Docker 精靈、Docker 用戶端和 Docker Compose。</span><span class="sxs-lookup"><span data-stu-id="1e511-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="1e511-110">相較於只使用 Docker 電腦或自行建立 Docker 主機，您使用 Azure Docker VM 延伸模組會有更多控制權和功能。</span><span class="sxs-lookup"><span data-stu-id="1e511-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="1e511-111">這些額外功能，例如 [Docker Compose](https://docs.docker.com/compose/overview/)，讓 Azure Docker VM 延伸模組適用於更穩固的開發人員或生產環境。</span><span class="sxs-lookup"><span data-stu-id="1e511-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="1e511-112">如需不同部署方法的詳細資訊，包括使用 Docker 電腦和 Azure Container Service，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="1e511-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="1e511-113">如需快速應用程式原型，您可以使用 [Docker 電腦](docker-machine.md)建立單一 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="1e511-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="1e511-114">如需建置提供其他排程和管理工具的生產就緒、可調整環境，您可以[在 Azure Container Service 上部署 Docker Swarm 叢集](../../container-service/dcos-swarm/container-service-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="1e511-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="1e511-115">使用 Azure Docker VM 擴充功能部署範本</span><span class="sxs-lookup"><span data-stu-id="1e511-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="1e511-116">使用現有的快速入門範本建立使用 Azure Docker VM 延伸模組的 Ubuntu VM，以安裝及設定 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="1e511-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="1e511-117">您可以在這裡檢視範本︰ [使用 Docker 簡易部署 Ubuntu VM](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。</span><span class="sxs-lookup"><span data-stu-id="1e511-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="1e511-118">您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e511-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1e511-119">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1e511-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1e511-120">下列範例會在 westus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="1e511-120">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="1e511-121">接下來，使用 [az group deployment create](/cli/azure/group/deployment#create) 來部署 VM，其中包含來自 [GitHub 上此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)的 Azure Docker VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="1e511-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="1e511-122">針對 newStorageAccountName、adminUsername、adminPassword 和 dnsNameForPublicIP 提供您自己的值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e511-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="1e511-123">需要幾分鐘的時間才能完成部署。</span><span class="sxs-lookup"><span data-stu-id="1e511-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="1e511-124">部署完成後，[移至下一個步驟](#deploy-your-first-nginx-container)以透過 SSH 連接到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="1e511-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="1e511-125">(選擇性) 若要將控制權交回給提示字元，並且讓部署繼續在背景中執行，請將 `--no-wait` 旗標新增至上述命令。</span><span class="sxs-lookup"><span data-stu-id="1e511-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="1e511-126">此程序可讓您在部署繼續執行數分鐘時，在 CLI 中執行其他工作。</span><span class="sxs-lookup"><span data-stu-id="1e511-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> 

<span data-ttu-id="1e511-127">您可以接著使用 [az vm show](/cli/azure/vm#show)，檢視有關 Docker 主機狀態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1e511-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="1e511-128">下列範例會在名為 myResourceGroup 的資源群組中檢查名為 myDockerVM 的 VM 狀態 (範本的預設名稱 - 請勿變更這個名稱)：</span><span class="sxs-lookup"><span data-stu-id="1e511-128">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="1e511-129">當此命令傳回 Succeeded 時，即表示部署已完成，您可以在下列步驟中透過 SSH 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="1e511-129">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="1e511-130">部署您的第一個 nginx 容器</span><span class="sxs-lookup"><span data-stu-id="1e511-130">Deploy your first nginx container</span></span>
<span data-ttu-id="1e511-131">若要檢視 VM 的詳細資料，包括 DNS 名稱，請使用 `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`。</span><span class="sxs-lookup"><span data-stu-id="1e511-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="1e511-132">SSH 會從本機電腦連線到新的 Docker 主機，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="1e511-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="1e511-133">一旦登入 Docker 主機後，請執行 nginx 容器︰</span><span class="sxs-lookup"><span data-stu-id="1e511-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="1e511-134">下載 nginx 影像和啟動容器時，輸出類似下列的範例︰</span><span class="sxs-lookup"><span data-stu-id="1e511-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="1e511-135">檢查您的 Docker 主機上執行的容器狀態，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="1e511-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="1e511-136">輸出類似下列的範例，會顯示 nginx 容器正在執行，且正在轉送 TCP 連接埠 80 和 443︰</span><span class="sxs-lookup"><span data-stu-id="1e511-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="1e511-137">若要查看容器實際運作的情況，請開啟網頁瀏覽器，然後輸入 Docker 主機的 DNS 名稱︰</span><span class="sxs-lookup"><span data-stu-id="1e511-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![執行 ngnix 容器](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="1e511-139">Azure Docker VM 延伸模組範本參考</span><span class="sxs-lookup"><span data-stu-id="1e511-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="1e511-140">前一個範例使用現有的快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="1e511-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="1e511-141">您也可以使用您自己的 Resource Manager 範本來部署 Azure Docker VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="1e511-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="1e511-142">若要這樣做，請將下列項目新增至 Resource Manager 範本，適當地定義 VM 的 `vmName`︰</span><span class="sxs-lookup"><span data-stu-id="1e511-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="1e511-143">如需更詳細的 Resource Manager 範本使用逐步解說，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1e511-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e511-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e511-144">Next steps</span></span>
<span data-ttu-id="1e511-145">您可能會想要使用 [Docker Compose](https://docs.docker.com/compose/overview/) 來[設定 Docker 精靈 TCP 連接埠](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket)、了解[Docker 安全性](https://docs.docker.com/engine/security/security/)或部署容器。</span><span class="sxs-lookup"><span data-stu-id="1e511-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="1e511-146">如需有關 Azure Docker VM 延伸模組本身的詳細資訊，請參閱 [GitHub 專案](https://github.com/Azure/azure-docker-extension/)。</span><span class="sxs-lookup"><span data-stu-id="1e511-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="1e511-147">閱讀有關 Azure 中其他 Docker 部署選項的詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="1e511-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="1e511-148">使用 Docker 電腦搭配 Azure 驅動程式</span><span class="sxs-lookup"><span data-stu-id="1e511-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="1e511-149">[在 Azure 虛擬機器上開始使用 Docker 和 Compose 定義並執行多容器應用程式](docker-compose-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="1e511-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="1e511-150">部署 Azure 容器服務叢集</span><span class="sxs-lookup"><span data-stu-id="1e511-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

