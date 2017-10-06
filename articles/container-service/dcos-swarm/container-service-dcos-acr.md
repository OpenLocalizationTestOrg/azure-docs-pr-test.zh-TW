---
title: "與 Azure DC/OS 叢集 aaaUsing ACR |Microsoft 文件"
description: "在 Azure Container Service 中搭配使用 Azure Container Registry 與 DC/OS 叢集"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, Containers, Micro-services, Mesos, Azure, FileShare, cifs, 容器, 微服務"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="f985d-104">您的應用程式使用與 DC/OS 叢集 toodeploy ACR</span><span class="sxs-lookup"><span data-stu-id="f985d-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="f985d-105">在本文中，我們探討如何與 DC/OS 叢集 toouse Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="f985d-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="f985d-106">使用 ACR 可讓您 tooprivately 存放區和管理容器映像。</span><span class="sxs-lookup"><span data-stu-id="f985d-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="f985d-107">本教學課程涵蓋 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="f985d-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f985d-108">部署 Azure Container Registry (如有需要)</span><span class="sxs-lookup"><span data-stu-id="f985d-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="f985d-109">在 DC/OS 叢集上設定 ACR 驗證</span><span class="sxs-lookup"><span data-stu-id="f985d-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="f985d-110">上傳映像 toohello Azure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="f985d-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="f985d-111">從 hello Azure 容器登錄中執行的容器映像</span><span class="sxs-lookup"><span data-stu-id="f985d-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="f985d-112">您必須在本教學課程步驟的叢集 toocomplete hello ACS DC/OS。</span><span class="sxs-lookup"><span data-stu-id="f985d-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="f985d-113">如有需要，[此指令碼範例](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)可為您建立一個叢集。</span><span class="sxs-lookup"><span data-stu-id="f985d-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="f985d-114">本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f985d-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f985d-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="f985d-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f985d-116">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f985d-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="f985d-117">部署 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="f985d-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="f985d-118">如有需要建立 Azure 容器登錄以 hello [az acr 建立](/cli/azure/acr#create)命令。</span><span class="sxs-lookup"><span data-stu-id="f985d-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="f985d-119">hello 下列範例會建立登錄中的以隨機產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="f985d-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="f985d-120">hello 登錄也會搭配使用 hello 系統管理員帳戶設定`--admin-enabled`引數。</span><span class="sxs-lookup"><span data-stu-id="f985d-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="f985d-121">一旦建立 hello 登錄之後，hello Azure CLI 輸出類似 toohello 下列資料。</span><span class="sxs-lookup"><span data-stu-id="f985d-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="f985d-122">記下 hello`name`和`loginServer`，會在稍後步驟中使用這些。</span><span class="sxs-lookup"><span data-stu-id="f985d-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="f985d-123">取得使用 hello hello 容器登錄認證[az acr 認證顯示](/cli/azure/acr/credential)命令。</span><span class="sxs-lookup"><span data-stu-id="f985d-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="f985d-124">替代 hello`--name`以 hello 一個 hello 最後一個步驟中所述。</span><span class="sxs-lookup"><span data-stu-id="f985d-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="f985d-125">記下一組密碼，稍後的步驟中會用到此密碼。</span><span class="sxs-lookup"><span data-stu-id="f985d-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="f985d-126">如需有關 Azure 容器登錄中的詳細資訊，請參閱[簡介 tooprivate Docker 容器登錄](../../container-registry/container-registry-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="f985d-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="f985d-127">管理 ACR 驗證</span><span class="sxs-lookup"><span data-stu-id="f985d-127">Manage ACR authentication</span></span>

<span data-ttu-id="f985d-128">hello 傳統方式 toopush 和提取映像從私人登錄 toofirst 向 hello 登錄。</span><span class="sxs-lookup"><span data-stu-id="f985d-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="f985d-129">toodo 因此，您會使用 hello`docker login`命令需要 tooaccess hello 私人登錄任何用戶端上。</span><span class="sxs-lookup"><span data-stu-id="f985d-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="f985d-130">DC/OS 叢集可以包含許多節點，其中需要 toobe 驗證以 hello ACR，因為它是很有幫助 tooautomate 透過此程序的每個節點。</span><span class="sxs-lookup"><span data-stu-id="f985d-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="f985d-131">建立共用儲存體</span><span class="sxs-lookup"><span data-stu-id="f985d-131">Create shared storage</span></span>

<span data-ttu-id="f985d-132">此程序使用的 Azure 檔案共用，已掛接 hello 叢集中的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="f985d-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="f985d-133">如果尚未設定共用儲存體，請參閱[在 DC/OS 叢集內設定檔案共用](container-service-dcos-fileshare.md)。</span><span class="sxs-lookup"><span data-stu-id="f985d-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="f985d-134">設定 ACR 驗證</span><span class="sxs-lookup"><span data-stu-id="f985d-134">Configure ACR authentication</span></span>

<span data-ttu-id="f985d-135">首先，取得 hello hello 主要 DC/OS，並將它儲存在變數中的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="f985d-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="f985d-136">建立 SSH 連線與 hello 主要 （或 hello 第一個主要） 的 DC/作業系統為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="f985d-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="f985d-137">如果建立 hello 叢集時使用非預設值，請更新 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f985d-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="f985d-138">執行下列命令 toologin toohello Azure 容器登錄中的 hello。</span><span class="sxs-lookup"><span data-stu-id="f985d-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="f985d-139">取代 hello `--username` hello 名稱 hello 容器登錄中，hello`--password`與其中一個 hello 提供密碼。</span><span class="sxs-lookup"><span data-stu-id="f985d-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="f985d-140">取代 hello 最後一個引數*mycontainerregistry.azurecr.io*中的 hello 容器登錄中的 hello 範例與 hello loginServer 名稱。</span><span class="sxs-lookup"><span data-stu-id="f985d-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="f985d-141">此命令會儲存在本機下 hello hello 驗證值`~/.docker`路徑。</span><span class="sxs-lookup"><span data-stu-id="f985d-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="f985d-142">建立壓縮的檔案，其中包含 hello 容器登錄驗證值。</span><span class="sxs-lookup"><span data-stu-id="f985d-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="f985d-143">複製這個檔案 toohello 叢集共用存放裝置。</span><span class="sxs-lookup"><span data-stu-id="f985d-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="f985d-144">此步驟會 hello 檔案 hello DC/OS 叢集的所有節點上使用。</span><span class="sxs-lookup"><span data-stu-id="f985d-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="f985d-145">上傳映像 tooACR</span><span class="sxs-lookup"><span data-stu-id="f985d-145">Upload image tooACR</span></span>

<span data-ttu-id="f985d-146">現在從開發電腦或任何其他系統已安裝 docker，請建立映像，並將它上傳 toohello Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="f985d-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="f985d-147">從 hello Ubuntu 映像建立容器。</span><span class="sxs-lookup"><span data-stu-id="f985d-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="f985d-148">現在擷取到新的映像的 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="f985d-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="f985d-149">hello 映像名稱必須 tooinclude hello`loginServer`名稱格式的 hello 容器 registrywith `loginServer/imageName`。</span><span class="sxs-lookup"><span data-stu-id="f985d-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="f985d-150">登入 hello Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="f985d-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="f985d-151">取代 hello hello loginServer 名稱、 hello-具有 hello 名稱 hello 容器登錄中和 hello-密碼與其中一個 hello 提供密碼的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f985d-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="f985d-152">最後上, 傳 hello 映像 toohello ACR 登錄。</span><span class="sxs-lookup"><span data-stu-id="f985d-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="f985d-153">這個範例會上傳名為 dcos-demo 的映像。</span><span class="sxs-lookup"><span data-stu-id="f985d-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="f985d-154">從 ACR 執行映像</span><span class="sxs-lookup"><span data-stu-id="f985d-154">Run an image from ACR</span></span>

<span data-ttu-id="f985d-155">toouse hello ACR 登錄中，從映像建立的檔案名稱*acrDemo.json*並複製 hello 遵循到其中的文字。</span><span class="sxs-lookup"><span data-stu-id="f985d-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="f985d-156">Hello 映像名稱取代 hello 容器登錄 loginServer 名稱和映像名稱，例如`loginServer/imageName`。</span><span class="sxs-lookup"><span data-stu-id="f985d-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="f985d-157">記下 hello`uris`屬性。</span><span class="sxs-lookup"><span data-stu-id="f985d-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="f985d-158">這個屬性會保留 hello hello 容器登錄驗證檔案位置，在此情況下是裝載在 hello DC/OS 叢集中的每個節點的 hello Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f985d-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="f985d-159">部署以 hello DC/MICROSOFT-WINDOWS-NETFX3-OC-PACKAGE CLI hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f985d-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="f985d-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f985d-160">Next steps</span></span>

<span data-ttu-id="f985d-161">在本教學課程中，您已設定 DC/OS toouse Azure 容器登錄中包括 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="f985d-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f985d-162">部署 Azure Container Registry (如有需要)</span><span class="sxs-lookup"><span data-stu-id="f985d-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="f985d-163">在 DC/OS 叢集上設定 ACR 驗證</span><span class="sxs-lookup"><span data-stu-id="f985d-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="f985d-164">上傳映像 toohello Azure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="f985d-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="f985d-165">從 hello Azure 容器登錄中執行的容器映像</span><span class="sxs-lookup"><span data-stu-id="f985d-165">Run a container image from hello Azure Container Registry</span></span>
