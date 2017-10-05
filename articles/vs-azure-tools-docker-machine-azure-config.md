---
title: "用 Docker 電腦在 Azure 中建立 Docker 主機 | Microsoft Docs"
description: "說明如何使用 Docker 電腦在 Azure 中建立 Docker 主機。"
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
ms.openlocfilehash: 766d327a87ed13e04166d71c3d9ae0a1e7a66d19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="5cb76-103">使用 Docker-Machine 在 Azure 中建立 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="5cb76-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="5cb76-104">執行 [Docker](https://www.docker.com/) 容器時需要執行 Docker 精靈的主機 VM。</span><span class="sxs-lookup"><span data-stu-id="5cb76-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="5cb76-105">本主題說明如何使用 [docker-machine](https://docs.docker.com/machine/) 命令，來建立在 Azure 中執行並使用 Docker 精靈所設定的新 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="5cb76-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="5cb76-106">**附註：**</span><span class="sxs-lookup"><span data-stu-id="5cb76-106">**Note:**</span></span> 

* <span data-ttu-id="5cb76-107">*本文是依據 docker-machine 0.9.0-rc2 版或更新版本*</span><span class="sxs-lookup"><span data-stu-id="5cb76-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="5cb76-108">*在不久的未來，將透過 docker-machine 支援 Windows Containers*</span><span class="sxs-lookup"><span data-stu-id="5cb76-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="5cb76-109">使用 Docker 電腦建立 VM</span><span class="sxs-lookup"><span data-stu-id="5cb76-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="5cb76-110">搭配使用 `docker-machine create` 命令與 `azure` 驅動程式，在 Azure 中建立 Docker 主機 VM。</span><span class="sxs-lookup"><span data-stu-id="5cb76-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="5cb76-111">Azure 驅動程式需要您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="5cb76-111">The Azure driver requires your subscription ID.</span></span> <span data-ttu-id="5cb76-112">您可以使用 [Azure CLI](cli-install-nodejs.md) 或 [Azure 入口網站](https://portal.azure.com)來擷取您的「Azure 訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="5cb76-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="5cb76-113">**使用 Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="5cb76-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="5cb76-114">從左導覽頁面中選取 [訂用帳戶]，並複製訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="5cb76-114">Select **Subscriptions** from the left navigation page and copy the subscription id.</span></span>

<span data-ttu-id="5cb76-115">**使用 Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="5cb76-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="5cb76-116">輸入 ```azure account list``` ，並複製訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="5cb76-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="5cb76-117">輸入 `docker-machine create --driver azure` 以查看選項和其預設值。</span><span class="sxs-lookup"><span data-stu-id="5cb76-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="5cb76-118">您也可以查看 [Docker Azure 驅動程式文件](https://docs.docker.com/machine/drivers/azure/) ，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5cb76-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="5cb76-119">下列範例採用[預設值](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22)，但會視需要設定下列值：</span><span class="sxs-lookup"><span data-stu-id="5cb76-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="5cb76-120">與所產生的公用 IP 位址和憑證關聯之名稱的 azure-dns。</span><span class="sxs-lookup"><span data-stu-id="5cb76-120">azure-dns for the name associated with the public IP and certificates generated.</span></span> <span data-ttu-id="5cb76-121">這是虛擬機器的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="5cb76-121">This is the DNS name of your virtual machine.</span></span> <span data-ttu-id="5cb76-122">接著，VM 就可以安全地停止、釋出動態 IP，還能夠在 VM 以新的 IP 重新啟動之後重新連線。</span><span class="sxs-lookup"><span data-stu-id="5cb76-122">The VM can then safely stop, release the dynamic IP, and provide the ability to reconnect after the vm starts again with a new IP.</span></span> <span data-ttu-id="5cb76-123">該區域必須有唯一的名稱前置詞 UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="5cb76-123">The name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="5cb76-124">VM 上用以進行對外網際網路存取的開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="5cb76-124">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="5cb76-125">用以使用更快速進階儲存體的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="5cb76-125">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="5cb76-126">用來作為 VM 磁碟的進階儲存體</span><span class="sxs-lookup"><span data-stu-id="5cb76-126">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="5cb76-127">使用 docker-machine 選擇 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="5cb76-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="5cb76-128">docker-machine 中有您主機的項目之後，即可在執行 docker 命令時設定預設主機。</span><span class="sxs-lookup"><span data-stu-id="5cb76-128">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="5cb76-129">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cb76-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="5cb76-130">使用 Bash</span><span class="sxs-lookup"><span data-stu-id="5cb76-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="5cb76-131">您現在可以對指定的主機執行 docker 命令</span><span class="sxs-lookup"><span data-stu-id="5cb76-131">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="5cb76-132">執行容器</span><span class="sxs-lookup"><span data-stu-id="5cb76-132">Run a container</span></span>
<span data-ttu-id="5cb76-133">設定主機之後，您現在可以執行簡單的 Web 伺服器，來測試是否已正確設定主機。</span><span class="sxs-lookup"><span data-stu-id="5cb76-133">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="5cb76-134">我們在此使用標準 nginx 映像，指定它應該接聽連接埠 80，而且如果主機 VM 重新啟動，則容器也會重新啟動 (`--restart=always`)。</span><span class="sxs-lookup"><span data-stu-id="5cb76-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="5cb76-135">輸出應該類似下面這樣：</span><span class="sxs-lookup"><span data-stu-id="5cb76-135">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="5cb76-136">測試容器</span><span class="sxs-lookup"><span data-stu-id="5cb76-136">Test the container</span></span>
<span data-ttu-id="5cb76-137">使用 `docker ps`檢查執行中容器：</span><span class="sxs-lookup"><span data-stu-id="5cb76-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="5cb76-138">若要查看執行中的容器，請輸入 `docker-machine ip <VM name>`，找出要在瀏覽器中輸入的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="5cb76-138">And, to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![執行 ngnix 容器](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="5cb76-140">摘要</span><span class="sxs-lookup"><span data-stu-id="5cb76-140">Summary</span></span>
<span data-ttu-id="5cb76-141">docker-machine 可讓您在 Azure 中輕鬆地佈建 docker 主機，以進行個別 docker 主機驗證。</span><span class="sxs-lookup"><span data-stu-id="5cb76-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="5cb76-142">如需實際執行裝載容器，請參閱 [Azure Container Service](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="5cb76-142">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="5cb76-143">若要使用 Visual Studio 開發 .NET Core 應用程式，請參閱 [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="5cb76-143">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

