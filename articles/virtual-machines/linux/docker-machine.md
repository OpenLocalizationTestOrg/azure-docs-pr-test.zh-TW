---
title: "使用 Docker 電腦在 Azure 中建立 Linux 主機 | Microsoft Docs"
description: "說明如何使用 Docker 電腦在 Azure 中建立 Docker 主機。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: a69951ed60edab8ae20374ab3869b468979c4907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-docker-machine-to-create-hosts-in-azure"></a><span data-ttu-id="6f303-103">如何使用 Docker 電腦在 Azure 中建立主機</span><span class="sxs-lookup"><span data-stu-id="6f303-103">How to use Docker Machine to create hosts in Azure</span></span>
<span data-ttu-id="6f303-104">這篇文章說明如何使用 [Docker 電腦](https://docs.docker.com/machine/)在 Azure 中建立主機。</span><span class="sxs-lookup"><span data-stu-id="6f303-104">This article details how to use [Docker Machine](https://docs.docker.com/machine/) to create hosts in Azure.</span></span> <span data-ttu-id="6f303-105">`docker-machine` 命令會在 Azure 中建立 Linux 虛擬機器 (VM)，然後安裝 Docker。</span><span class="sxs-lookup"><span data-stu-id="6f303-105">The `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="6f303-106">接著，您可以使用相同本機工具和工作流程，在 Azure 中管理您的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="6f303-106">You can then manage your Docker hosts in Azure using the same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="6f303-107">使用 Docker 電腦建立 VM</span><span class="sxs-lookup"><span data-stu-id="6f303-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="6f303-108">首先，使用 [az account show](/cli/azure/account#show) 取得您的 Azure 訂用帳戶識別碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f303-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="6f303-109">您使用 `docker-machine create`，將 *azure* 指定為驅動程式，在 Azure 中建立 Docker 主機 VM。</span><span class="sxs-lookup"><span data-stu-id="6f303-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as the driver.</span></span> <span data-ttu-id="6f303-110">如需詳細資訊，請參閱 [Docker Azure 驅動程式文件](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="6f303-110">For more information, see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="6f303-111">下列範例會建立名為 *myVM* 的 VM，建立名為 *azureuser* 的使用者帳戶，並且在主機 VM 上開啟連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="6f303-111">The following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on the host VM.</span></span> <span data-ttu-id="6f303-112">依照任何提示登入您的 Azure 帳戶，並且授與 Docker 電腦權限以建立及管理資源。</span><span class="sxs-lookup"><span data-stu-id="6f303-112">Follow any prompts to log in to your Azure account and grant Docker Machine permissions to create and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="6f303-113">輸出大致如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6f303-113">The output looks similar to the following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="6f303-114">設定您的 Docker 殼層</span><span class="sxs-lookup"><span data-stu-id="6f303-114">Configure your Docker shell</span></span>
<span data-ttu-id="6f303-115">若要連線到 Azure 中的 Docker 主機，請定義適當的連線設定。</span><span class="sxs-lookup"><span data-stu-id="6f303-115">To connect to your Docker host in Azure, define the appropriate connection settings.</span></span> <span data-ttu-id="6f303-116">如輸出結尾所述，檢視 Docker 主機的連線資訊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f303-116">As noted at the end of the output, view the connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="6f303-117">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="6f303-117">The output is similar to the following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command to configure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="6f303-118">若要定義連線設定，您可以執行建議的設定命令 (`eval $(docker-machine env myvmdocker)`)，或手動設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="6f303-118">To define the connection settings you can either run the suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set the environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="6f303-119">執行容器</span><span class="sxs-lookup"><span data-stu-id="6f303-119">Run a container</span></span>
<span data-ttu-id="6f303-120">為了查看作用中的容器，讓我們執行基本 NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="6f303-120">To see a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="6f303-121">使用 `docker run` 建立容器，並且為 Web 流量公開連接埠 80，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f303-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="6f303-122">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="6f303-122">The output is similar to the following example:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="6f303-123">使用 `docker ps` 檢視執行中容器。</span><span class="sxs-lookup"><span data-stu-id="6f303-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="6f303-124">下列範例輸出顯示使用已公開連接埠 80 執行的 NGINX 容器：</span><span class="sxs-lookup"><span data-stu-id="6f303-124">The following example output shows the NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-the-container"></a><span data-ttu-id="6f303-125">測試容器</span><span class="sxs-lookup"><span data-stu-id="6f303-125">Test the container</span></span>
<span data-ttu-id="6f303-126">取得 Docker 主機的公用 IP 位址，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f303-126">Obtain the public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="6f303-127">若要查看作用中的容器，開啟網頁瀏覽器並輸入上述命令輸出中所述的公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="6f303-127">To see the container in action, open a web browser and enter the public IP address noted in the output of the preceding command:</span></span>

![執行 ngnix 容器](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="6f303-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f303-129">Next steps</span></span>
<span data-ttu-id="6f303-130">您也可以使用 [Docker VM 延伸模組](dockerextension.md)建立主機。</span><span class="sxs-lookup"><span data-stu-id="6f303-130">You can also create hosts with the [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="6f303-131">如需使用 Docker Compose 的範例，請參閱[在 Azure 中開始使用 Docker 與 Compose](docker-compose-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="6f303-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
