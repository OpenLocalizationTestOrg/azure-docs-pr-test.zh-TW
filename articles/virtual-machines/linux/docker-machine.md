---
title: "在 Azure 中裝載 aaaUse Docker 機器 toocreate Linux |Microsoft 文件"
description: "描述如何 toouse Docker 機器 toocreate Docker 裝載在 Azure 中。"
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
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a><span data-ttu-id="13b26-103">Toouse Docker 機器 toocreate 如何在 Azure 中裝載</span><span class="sxs-lookup"><span data-stu-id="13b26-103">How toouse Docker Machine toocreate hosts in Azure</span></span>
<span data-ttu-id="13b26-104">此發行項詳細資料時，如何 toouse [Docker 機器](https://docs.docker.com/machine/)toocreate 在 Azure 中的主機。</span><span class="sxs-lookup"><span data-stu-id="13b26-104">This article details how toouse [Docker Machine](https://docs.docker.com/machine/) toocreate hosts in Azure.</span></span> <span data-ttu-id="13b26-105">hello`docker-machine`命令在 Azure 中建立 Linux 虛擬機器 (VM)，然後安裝 Docker。</span><span class="sxs-lookup"><span data-stu-id="13b26-105">hello `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="13b26-106">接著，您可以管理您的 Docker 主機，在 Azure 中使用 hello 相同本機工具和工作流程。</span><span class="sxs-lookup"><span data-stu-id="13b26-106">You can then manage your Docker hosts in Azure using hello same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="13b26-107">使用 Docker 電腦建立 VM</span><span class="sxs-lookup"><span data-stu-id="13b26-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="13b26-108">首先，使用 [az account show](/cli/azure/account#show) 取得您的 Azure 訂用帳戶識別碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13b26-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="13b26-109">您在 Azure 中建立 Docker 主機 Vm`docker-machine create`藉由指定*azure*作為 hello 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="13b26-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as hello driver.</span></span> <span data-ttu-id="13b26-110">如需詳細資訊，請參閱 hello [Docker Azure 驅動程式文件](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="13b26-110">For more information, see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="13b26-111">hello 下列範例會建立名為的 VM *myVM*，建立名為的使用者帳戶*azureuser*，並開啟連接埠*80* hello 上裝載的 VM。</span><span class="sxs-lookup"><span data-stu-id="13b26-111">hello following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on hello host VM.</span></span> <span data-ttu-id="13b26-112">請遵循 tooyour Azure 帳戶中的任何提示 toolog Docker 機器權限 toocreate 授與和管理資源。</span><span class="sxs-lookup"><span data-stu-id="13b26-112">Follow any prompts toolog in tooyour Azure account and grant Docker Machine permissions toocreate and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="13b26-113">hello 輸出看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="13b26-113">hello output looks similar toohello following example:</span></span>

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
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="13b26-114">設定您的 Docker 殼層</span><span class="sxs-lookup"><span data-stu-id="13b26-114">Configure your Docker shell</span></span>
<span data-ttu-id="13b26-115">tooconnect tooyour Docker 主機，在 Azure 中，定義 hello 適當的連線設定。</span><span class="sxs-lookup"><span data-stu-id="13b26-115">tooconnect tooyour Docker host in Azure, define hello appropriate connection settings.</span></span> <span data-ttu-id="13b26-116">如所述在 hello hello 輸出的結尾，檢視 hello Docker 主機的連接資訊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13b26-116">As noted at hello end of hello output, view hello connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="13b26-117">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="13b26-117">hello output is similar toohello following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="13b26-118">可以是執行的 hello toodefine hello 連線設定建議的組態命令 (`eval $(docker-machine env myvmdocker)`)，或您可以手動設定 hello 環境變數。</span><span class="sxs-lookup"><span data-stu-id="13b26-118">toodefine hello connection settings you can either run hello suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set hello environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="13b26-119">執行容器</span><span class="sxs-lookup"><span data-stu-id="13b26-119">Run a container</span></span>
<span data-ttu-id="13b26-120">toosee 的容器中的動作，可讓您執行基本的 NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="13b26-120">toosee a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="13b26-121">使用 `docker run` 建立容器，並且為 Web 流量公開連接埠 80，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13b26-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="13b26-122">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="13b26-122">hello output is similar toohello following example:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="13b26-123">使用 `docker ps` 檢視執行中容器。</span><span class="sxs-lookup"><span data-stu-id="13b26-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="13b26-124">hello 下列的範例輸出顯示 hello NGINX 容器執行使用連接埠 80 公開：</span><span class="sxs-lookup"><span data-stu-id="13b26-124">hello following example output shows hello NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a><span data-ttu-id="13b26-125">測試 hello 容器</span><span class="sxs-lookup"><span data-stu-id="13b26-125">Test hello container</span></span>
<span data-ttu-id="13b26-126">取得 hello 公用 IP 位址的 Docker 主機，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13b26-126">Obtain hello public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="13b26-127">toosee hello 容器在動作中，開啟網頁瀏覽器，並輸入 hello hello hello 前面命令輸出中所述公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="13b26-127">toosee hello container in action, open a web browser and enter hello public IP address noted in hello output of hello preceding command:</span></span>

![執行 ngnix 容器](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="13b26-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13b26-129">Next steps</span></span>
<span data-ttu-id="13b26-130">您也可以建立主控件以 hello [Docker VM 擴充功能](dockerextension.md)。</span><span class="sxs-lookup"><span data-stu-id="13b26-130">You can also create hosts with hello [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="13b26-131">如需使用 Docker Compose 的範例，請參閱[在 Azure 中開始使用 Docker 與 Compose](docker-compose-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="13b26-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
