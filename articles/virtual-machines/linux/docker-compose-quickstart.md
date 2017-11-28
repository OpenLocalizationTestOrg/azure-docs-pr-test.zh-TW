---
title: "在 Azure 中的 Linux VM 上的 Docker Compose aaaUse |Microsoft 文件"
description: "Toouse Docker 和 Linux 的虛擬機器上撰寫 hello Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="bdb20-103">取得開始使用 Docker 和撰寫 toodefine 並在 Azure 中執行多個容器應用程式</span><span class="sxs-lookup"><span data-stu-id="bdb20-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="bdb20-104">與[撰寫](http://github.com/docker/compose)，您可以使用簡單的文字檔案 toodefine 組成的多個 Docker 容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdb20-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="bdb20-105">然後加速您的應用程式中的單一命令的一切 toodeploy 您定義的環境。</span><span class="sxs-lookup"><span data-stu-id="bdb20-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="bdb20-106">例如，本文章將示範如何 tooquickly WordPress 部落格與後端 MariaDB SQL 資料庫上設定 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="bdb20-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="bdb20-107">您也可以使用撰寫 tooset 組成更複雜的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdb20-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="bdb20-108">設定 Linux VM 做為 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="bdb20-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="bdb20-109">您可以在 hello Azure Marketplace toocreate Linux VM 中使用各種 Azure 的程序和可用的映像或資源管理員範本，並將它設定為 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="bdb20-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="bdb20-110">例如，請參閱[使用您環境的 hello Docker VM 擴充功能 toodeploy](dockerextension.md) tooquickly Ubuntu VM 以 hello Azure Docker VM 延伸模組建立使用[快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="bdb20-111">當您使用 hello Docker VM 擴充功能時，您的 VM 會自動設定為 Docker 主機，且已安裝撰寫。</span><span class="sxs-lookup"><span data-stu-id="bdb20-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="bdb20-112">使用 Azure CLI 2.0 建立 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="bdb20-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="bdb20-113">最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="bdb20-114">首先，使用 [az group create](/cli/azure/group#create) 建立 Docker 環境的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bdb20-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bdb20-115">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *uswest*位置：</span><span class="sxs-lookup"><span data-stu-id="bdb20-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="bdb20-116">接下來，部署具有 VM [az 群組部署建立](/cli/azure/group/deployment#create)包含 hello Azure Docker VM 擴充功能，從[GitHub 上的此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="bdb20-117">針對 newStorageAccountName、adminUsername、adminPassword 和 dnsNameForPublicIP 提供您自己的值：</span><span class="sxs-lookup"><span data-stu-id="bdb20-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="bdb20-118">花幾分鐘，讓 hello 部署 toofinish。</span><span class="sxs-lookup"><span data-stu-id="bdb20-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="bdb20-119">在 hello 部署完成時，[移動 toonext 步驟](#verify-that-compose-is-installed)tooSSH tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="bdb20-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="bdb20-120">（選擇性） tooinstead 傳回控制 toohello 提示與 hello 可讓的部署於 hello 背景繼續執行新增 hello `--no-wait` toohello 命令的前面加上旗標。</span><span class="sxs-lookup"><span data-stu-id="bdb20-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="bdb20-121">此程序可讓您 tooperform hello CLI 時在幾分鐘後會繼續進行 hello 部署中的其他工作。</span><span class="sxs-lookup"><span data-stu-id="bdb20-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="bdb20-122">然後，您可以檢視與 hello Docker 主機狀態的詳細[az vm 顯示](/cli/azure/vm#show)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="bdb20-123">hello 下列範例會檢查 hello 狀態 hello 名為 VM *myDockerVM* （hello hello 範本中的預設名稱-不要變更這個名稱） 在 hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="bdb20-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="bdb20-124">此命令會傳回當*Succeeded*hello 部署已完成，您可以在 hello 步驟之後的 SSH toohello VM。</span><span class="sxs-lookup"><span data-stu-id="bdb20-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="bdb20-125">確認已安裝 Compose</span><span class="sxs-lookup"><span data-stu-id="bdb20-125">Verify that Compose is installed</span></span>
<span data-ttu-id="bdb20-126">在 hello 部署完成時，SSH tooyour 新 Docker 主機使用 hello DNS 名稱提供您在部署期間。</span><span class="sxs-lookup"><span data-stu-id="bdb20-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="bdb20-127">您可以使用`az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`tooview 詳細資料，您的 VM，包括 hello DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="bdb20-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="bdb20-128">撰寫的 toocheck 被安裝在 hello VM，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="bdb20-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="bdb20-129">您會看到類似的輸出太*docker 撰寫 1.6.2、 組建 4d 72027*。</span><span class="sxs-lookup"><span data-stu-id="bdb20-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="bdb20-130">如果您使用另一個方法 toocreate Docker 主機，而需要的 tooinstall 撰寫您自己，請參閱 hello[撰寫文件](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="bdb20-131">建立 docker-compose.yml 組態檔</span><span class="sxs-lookup"><span data-stu-id="bdb20-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="bdb20-132">接下來您建立`docker-compose.yml`不只是文字組態檔，toodefine hello Docker 容器 toorun hello VM 上的檔案。</span><span class="sxs-lookup"><span data-stu-id="bdb20-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="bdb20-133">hello 檔案指定 hello 映像 toorun 上每個容器 （或可能是來自 Dockerfile），必要的環境變數和相依性、 連接埠和 hello 容器之間的連結。</span><span class="sxs-lookup"><span data-stu-id="bdb20-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="bdb20-134">如需有關 yml 檔案語法的詳細資料，請參閱 [Compose file reference (Compose 檔案參考)](https://docs.docker.com/compose/compose-file/)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="bdb20-135">建立 hello *docker compose.yml*檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bdb20-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="bdb20-136">使用您慣用的文字編輯器 tooadd toohello 的一些資料檔案。</span><span class="sxs-lookup"><span data-stu-id="bdb20-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="bdb20-137">hello 下列範例會使用 hello *vi*編輯器：</span><span class="sxs-lookup"><span data-stu-id="bdb20-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="bdb20-138">下列範例文字檔案到貼上 hello。</span><span class="sxs-lookup"><span data-stu-id="bdb20-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="bdb20-139">這種設定使用映像從 hello [DockerHub 登錄](https://registry.hub.docker.com/_/wordpress/)tooinstall WordPress （hello 開放原始碼部落格和內容管理系統） 和連結的後端 MariaDB SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="bdb20-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="bdb20-140">輸入您自已的 MYSQL_ROOT_PASSWORD，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bdb20-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="bdb20-141">Hello 容器開頭撰寫</span><span class="sxs-lookup"><span data-stu-id="bdb20-141">Start hello containers with Compose</span></span>
<span data-ttu-id="bdb20-142">在 hello 相同目錄做為您*docker compose.yml*檔案中，執行下列命令的 hello (根據您的環境，您可能需要 toorun`docker-compose`使用`sudo`):</span><span class="sxs-lookup"><span data-stu-id="bdb20-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="bdb20-143">此命令會啟動 hello Docker 容器中指定*docker compose.yml*。</span><span class="sxs-lookup"><span data-stu-id="bdb20-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="bdb20-144">花一分鐘，或兩個進行此步驟 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="bdb20-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="bdb20-145">您會看到下列範例的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="bdb20-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="bdb20-146">要確定 toouse hello **-d**啟動選項，使 hello 容器連續執行 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="bdb20-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="bdb20-147">hello 容器已啟動的 tooverify 類型`docker-compose ps`。</span><span class="sxs-lookup"><span data-stu-id="bdb20-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="bdb20-148">您應該會看到如下的內容：</span><span class="sxs-lookup"><span data-stu-id="bdb20-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="bdb20-149">您現在可以連接 tooWordPress 直接在 hello 連接埠 80 上的 VM 上。</span><span class="sxs-lookup"><span data-stu-id="bdb20-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="bdb20-150">開啟網頁瀏覽器並輸入您 VM hello DNS 名稱 (例如`http://mypublicdns.westus.cloudapp.azure.com`)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="bdb20-151">您現在應該會看到的 hello WordPress 開始畫面上，您會完成 hello 安裝，並開始使用 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdb20-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![WordPress 起始畫面][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="bdb20-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bdb20-153">Next steps</span></span>
* <span data-ttu-id="bdb20-154">移 toohello [Docker VM 延伸模組使用者指南](https://github.com/Azure/azure-docker-extension/blob/master/README.md)更多選項 tooconfigure Docker 和 Docker VM 中的撰寫。</span><span class="sxs-lookup"><span data-stu-id="bdb20-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="bdb20-155">例如，其中一個選項是 tooput hello 撰寫 yml 檔案 (轉換後 tooJSON) 直接在 hello hello Docker VM 擴充功能組態。</span><span class="sxs-lookup"><span data-stu-id="bdb20-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="bdb20-156">簽出 hello[撰寫命令列參照](http://docs.docker.com/compose/reference/)和[使用者指南](http://docs.docker.com/compose/)建置及部署多個容器應用程式的相關範例。</span><span class="sxs-lookup"><span data-stu-id="bdb20-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="bdb20-157">使用 Azure 資源管理員範本，或是您自己或其中一個由 hello[社群](https://azure.microsoft.com/documentation/templates/)，toodeploy Docker 和應用程式與 Azure VM 與撰寫設定。</span><span class="sxs-lookup"><span data-stu-id="bdb20-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="bdb20-158">例如，hello[部署使用 Docker WordPress 部落格](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql)範本使用 Docker，並撰寫 tooquickly 使用 MySQL 後端 Ubuntu 虛擬機器上部署 WordPress。</span><span class="sxs-lookup"><span data-stu-id="bdb20-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="bdb20-159">嘗試整合 Docker Compose 與 Docker Swarm 叢集。</span><span class="sxs-lookup"><span data-stu-id="bdb20-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="bdb20-160">如需案例，請參閱[搭配使用 Compose 與 Swarm (英文)](https://docs.docker.com/compose/swarm/)。</span><span class="sxs-lookup"><span data-stu-id="bdb20-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
