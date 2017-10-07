---
title: "aaaCreate Docker 裝載於 Azure 的 Docker 機器 |Microsoft 文件"
description: "說明使用 Docker 機器 toocreate docker 主機，在 Azure 中。"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="fbbea-103">使用 Docker-Machine 在 Azure 中建立 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="fbbea-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="fbbea-104">執行[Docker](https://www.docker.com/)容器需要主機 VM 執行 hello docker 精靈。</span><span class="sxs-lookup"><span data-stu-id="fbbea-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="fbbea-105">本主題描述如何 toouse hello [docker 機器](https://docs.docker.com/machine/)toocreate 新 Linux Vm，以設定 hello Docker 精靈，在 Azure 中執行的命令。</span><span class="sxs-lookup"><span data-stu-id="fbbea-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="fbbea-106">**附註：**</span><span class="sxs-lookup"><span data-stu-id="fbbea-106">**Note:**</span></span> 

* <span data-ttu-id="fbbea-107">*本文是依據 docker-machine 0.9.0-rc2 版或更新版本*</span><span class="sxs-lookup"><span data-stu-id="fbbea-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="fbbea-108">*Windows 容器將會支援透過 docker-機器在未來附近 hello*</span><span class="sxs-lookup"><span data-stu-id="fbbea-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="fbbea-109">使用 Docker 電腦建立 VM</span><span class="sxs-lookup"><span data-stu-id="fbbea-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="fbbea-110">Docker 主機 Vm 在 Azure 中建立以 hello`docker-machine create`命令使用 hello`azure`驅動程式。</span><span class="sxs-lookup"><span data-stu-id="fbbea-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="fbbea-111">hello Azure 驅動程式需要您的訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="fbbea-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="fbbea-112">您可以使用 hello [Azure CLI](cli-install-nodejs.md)或 hello [Azure 入口網站](https://portal.azure.com)tooretrieve 您 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fbbea-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="fbbea-113">**使用 hello Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="fbbea-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="fbbea-114">選取**訂閱**hello 左側瀏覽頁面以及複製 hello 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="fbbea-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="fbbea-115">**使用 Azure CLI hello**</span><span class="sxs-lookup"><span data-stu-id="fbbea-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="fbbea-116">型別```azure account list```和複製 hello 訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="fbbea-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="fbbea-117">型別`docker-machine create --driver azure`toosee hello 選項和其預設值。</span><span class="sxs-lookup"><span data-stu-id="fbbea-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="fbbea-118">您也可以查看 hello [Docker Azure 驅動程式文件](https://docs.docker.com/machine/drivers/azure/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fbbea-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="fbbea-119">hello 下列範例會依賴 hello[預設值](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22)，但選擇性地設定這些值：</span><span class="sxs-lookup"><span data-stu-id="fbbea-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="fbbea-120">azure dns hello hello 公用 IP 相關聯的名稱，以及產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="fbbea-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="fbbea-121">這是您的虛擬機器的 hello DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="fbbea-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="fbbea-122">hello VM 可以然後安全地停止，釋放 hello 動態 IP，並提供 hello 能力 tooreconnect 之後 hello vm 重新啟動新的 ip。</span><span class="sxs-lookup"><span data-stu-id="fbbea-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="fbbea-123">hello 名稱前置詞必須是唯一的 UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com 該區域。</span><span class="sxs-lookup"><span data-stu-id="fbbea-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="fbbea-124">開啟通訊埠 80 上 hello VM 為傳出網際網路存取</span><span class="sxs-lookup"><span data-stu-id="fbbea-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="fbbea-125">hello VM tooutilize 快高階儲存體的大小</span><span class="sxs-lookup"><span data-stu-id="fbbea-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="fbbea-126">用於 hello vm 磁碟的進階儲存體</span><span class="sxs-lookup"><span data-stu-id="fbbea-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="fbbea-127">使用 docker-machine 選擇 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="fbbea-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="fbbea-128">一旦您擁有 docker 機器中的項目為您的主機，您可以設定 hello 預設主控件執行 docker 命令時。</span><span class="sxs-lookup"><span data-stu-id="fbbea-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="fbbea-129">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbbea-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="fbbea-130">使用 Bash</span><span class="sxs-lookup"><span data-stu-id="fbbea-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="fbbea-131">您現在可以針對 hello 指定的主機執行 docker 命令</span><span class="sxs-lookup"><span data-stu-id="fbbea-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="fbbea-132">執行容器</span><span class="sxs-lookup"><span data-stu-id="fbbea-132">Run a container</span></span>
<span data-ttu-id="fbbea-133">請使用設定的主機，您現在可以執行簡單的 web 伺服器 tootest 是否已正確設定您的主機。</span><span class="sxs-lookup"><span data-stu-id="fbbea-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="fbbea-134">這裡我們使用的標準 nginx 映像，請指定應接聽連接埠 80，與 hello 主機 VM 重新啟動時，如果 hello 容器會重新啟動也 (`--restart=always`)。</span><span class="sxs-lookup"><span data-stu-id="fbbea-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="fbbea-135">hello 輸出看起來應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="fbbea-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="fbbea-136">測試 hello 容器</span><span class="sxs-lookup"><span data-stu-id="fbbea-136">Test hello container</span></span>
<span data-ttu-id="fbbea-137">使用 `docker ps`檢查執行中容器：</span><span class="sxs-lookup"><span data-stu-id="fbbea-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="fbbea-138">和執行類型的容器，toosee hello `docker-machine ip <VM name>` toofind hello IP 位址 tooenter hello 瀏覽器中：</span><span class="sxs-lookup"><span data-stu-id="fbbea-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![執行 ngnix 容器](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="fbbea-140">摘要</span><span class="sxs-lookup"><span data-stu-id="fbbea-140">Summary</span></span>
<span data-ttu-id="fbbea-141">docker-machine 可讓您在 Azure 中輕鬆地佈建 docker 主機，以進行個別 docker 主機驗證。</span><span class="sxs-lookup"><span data-stu-id="fbbea-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="fbbea-142">生產環境裝載的容器，請參閱 hello [Azure 容器服務](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="fbbea-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="fbbea-143">toodevelop.NET Core 應用程式與 Visual Studio，請參閱[Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="fbbea-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

