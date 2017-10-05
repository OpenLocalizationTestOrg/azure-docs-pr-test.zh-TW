---
title: "在 Azure 中使用 Docker Compose 連接至 Linux VM | Microsoft Docs"
description: "如何透過 Azure CLI 在 Linux 虛擬機器上使用 Docker 和 Compose"
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
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="84432-103">在 Azure 中開始使用 Docker 和 Compose 定義並執行多容器應用程式</span><span class="sxs-lookup"><span data-stu-id="84432-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="84432-104">藉由 [Compose](http://github.com/docker/compose)，您將可以使用簡單的文字檔來定義由多個 Docker 容器所組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="84432-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="84432-105">接著，您可以透過單一命令來啟動應用程式，此命令會執行所需的一切準備工作，以部署您的已定義環境。</span><span class="sxs-lookup"><span data-stu-id="84432-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="84432-106">舉例來說，本文將說明如何藉由 Ubuntu VM 上的後端 MariaDB SQL 資料庫來快速設定 WordPress 部落格。</span><span class="sxs-lookup"><span data-stu-id="84432-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="84432-107">您也可以使用 Compose 來設定更複雜的應用程式。</span><span class="sxs-lookup"><span data-stu-id="84432-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="84432-108">設定 Linux VM 做為 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="84432-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="84432-109">您可以使用 Azure Marketplace 中的各種 Azure 程序和可用映像或 Resource Manager 範本來建立 Linux VM，並將其設定為 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="84432-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="84432-110">例如，請參閱[使用 Docker VM 擴充功能來部署您的環境](dockerextension.md)，以使用[快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)藉由 Azure Docker VM 擴充功能建立 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="84432-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="84432-111">當您使用 Docker VM 擴充功能時，您的 VM 會自動設為 Docker 主機，並已安裝 Compose。</span><span class="sxs-lookup"><span data-stu-id="84432-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="84432-112">使用 Azure CLI 2.0 建立 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="84432-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="84432-113">請安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="84432-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="84432-114">首先，使用 [az group create](/cli/azure/group#create) 建立 Docker 環境的資源群組。</span><span class="sxs-lookup"><span data-stu-id="84432-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="84432-115">下列範例會在 westus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="84432-115">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="84432-116">接下來，使用 [az group deployment create](/cli/azure/group/deployment#create) 來部署 VM，其中包含來自 [GitHub 上此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)的 Azure Docker VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="84432-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="84432-117">針對 newStorageAccountName、adminUsername、adminPassword 和 dnsNameForPublicIP 提供您自己的值：</span><span class="sxs-lookup"><span data-stu-id="84432-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="84432-118">需要幾分鐘的時間才能完成部署。</span><span class="sxs-lookup"><span data-stu-id="84432-118">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="84432-119">部署完成後，[移至下一個步驟](#verify-that-compose-is-installed)以透過 SSH 連接到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="84432-119">Once the deployment is finished, [move to next step](#verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="84432-120">(選擇性) 若要將控制權交回給提示字元，並且讓部署繼續在背景中執行，請將 `--no-wait` 旗標新增至上述命令。</span><span class="sxs-lookup"><span data-stu-id="84432-120">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="84432-121">此程序可讓您在部署繼續執行數分鐘時，在 CLI 中執行其他工作。</span><span class="sxs-lookup"><span data-stu-id="84432-121">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="84432-122">您可以接著使用 [az vm show](/cli/azure/vm#show)，檢視有關 Docker 主機狀態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="84432-122">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="84432-123">下列範例會在名為 myResourceGroup 的資源群組中檢查名為 myDockerVM 的 VM 狀態 (範本的預設名稱 - 請勿變更這個名稱)：</span><span class="sxs-lookup"><span data-stu-id="84432-123">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="84432-124">當此命令傳回 Succeeded 時，即表示部署已完成，您可以在下列步驟中透過 SSH 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="84432-124">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="84432-125">確認已安裝 Compose</span><span class="sxs-lookup"><span data-stu-id="84432-125">Verify that Compose is installed</span></span>
<span data-ttu-id="84432-126">部署完成之後，請使用您在部署期間提供的 DNS 名稱，透過 SSH 連接到新的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="84432-126">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="84432-127">您可以使用 `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` 檢視您 VM 的詳細資料，包括 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="84432-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` to view details of your VM, including the DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="84432-128">若要檢查 Compose 是否已安裝在 VM 上，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="84432-128">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="84432-129">您會看見類型「docker-compose 1.6.2, build 4d72027」的輸出結果。</span><span class="sxs-lookup"><span data-stu-id="84432-129">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="84432-130">如果您使用另一種方法來建立 Docker 主機而需要自行安裝 Compose，請參閱 [Compose 文件](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md)。</span><span class="sxs-lookup"><span data-stu-id="84432-130">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="84432-131">建立 docker-compose.yml 組態檔</span><span class="sxs-lookup"><span data-stu-id="84432-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="84432-132">接下來，您需建立 `docker-compose.yml` 檔案，這只是一個文字組態檔，用來定義要在 VM 上執行的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="84432-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="84432-133">此檔案會指定要在每個容器上執行的映像 (或可能是來自 Dockerfile 的組建)、必要的環境變數和相依性、連接埠，以及容器之間的連結。</span><span class="sxs-lookup"><span data-stu-id="84432-133">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="84432-134">如需有關 yml 檔案語法的詳細資料，請參閱 [Compose file reference (Compose 檔案參考)](https://docs.docker.com/compose/compose-file/)。</span><span class="sxs-lookup"><span data-stu-id="84432-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="84432-135">建立 docker-compose.yml 檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="84432-135">Create the *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="84432-136">使用慣用的文字編輯器將一些資料新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="84432-136">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="84432-137">下列範例使用 vi 編輯器：</span><span class="sxs-lookup"><span data-stu-id="84432-137">The following example uses the *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="84432-138">將下列範例貼入文字檔案。</span><span class="sxs-lookup"><span data-stu-id="84432-138">Paste the following example into your text file.</span></span> <span data-ttu-id="84432-139">此組態會使用來自 [DockerHub 登錄](https://registry.hub.docker.com/_/wordpress/) 的映像，安裝 WordPress (開放原始碼部落格和內容管理系統) 和連結的後端 MariaDB SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="84432-139">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="84432-140">輸入您自已的 MYSQL_ROOT_PASSWORD，如下所示：</span><span class="sxs-lookup"><span data-stu-id="84432-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

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

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="84432-141">以 Compose 啟動容器</span><span class="sxs-lookup"><span data-stu-id="84432-141">Start the containers with Compose</span></span>
<span data-ttu-id="84432-142">在與您 docker-compose.yml 檔案相同的目錄中，執行下列命令 (根據您的環境，您可能需要使用 `sudo` 執行 `docker-compose`)：</span><span class="sxs-lookup"><span data-stu-id="84432-142">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="84432-143">這個命令會啟動 docker-compose.yml 中指定的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="84432-143">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="84432-144">此步驟需要幾分鐘的時間來完成。</span><span class="sxs-lookup"><span data-stu-id="84432-144">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="84432-145">您會看到類似以下範例的輸出：</span><span class="sxs-lookup"><span data-stu-id="84432-145">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="84432-146">請務必在啟動時使用 **-d** 選項，讓容器在背景持續執行。</span><span class="sxs-lookup"><span data-stu-id="84432-146">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="84432-147">若要確認容器是否已啟動，請輸入 `docker-compose ps`。</span><span class="sxs-lookup"><span data-stu-id="84432-147">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="84432-148">您應該會看到如下的內容：</span><span class="sxs-lookup"><span data-stu-id="84432-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="84432-149">您現在可以在 VM 的連接埠 80 上直接連線到 WordPress。</span><span class="sxs-lookup"><span data-stu-id="84432-149">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="84432-150">開啟網頁瀏覽器並輸入您 VM 的 DNS 名稱 (例如 `http://mypublicdns.westus.cloudapp.azure.com`)。</span><span class="sxs-lookup"><span data-stu-id="84432-150">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="84432-151">您現在應該會看到 WordPress 起始畫面，您可以在其中完成安裝，然後開始使用此應用程式。</span><span class="sxs-lookup"><span data-stu-id="84432-151">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![WordPress 起始畫面][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="84432-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84432-153">Next steps</span></span>
* <span data-ttu-id="84432-154">如需了解在 Docker VM 中設定 Docker 和 Compose 的更多選項，請移至 [Docker VM 擴充功能使用者指南](https://github.com/Azure/azure-docker-extension/blob/master/README.md) 。</span><span class="sxs-lookup"><span data-stu-id="84432-154">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="84432-155">例如，其中一個選項是將 Compose yml 檔案 (轉換為 JSON) 直接置於 Docker VM 延伸模組的組態中。</span><span class="sxs-lookup"><span data-stu-id="84432-155">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="84432-156">如需更多建置和部署多容器應用程式的範例，請參閱 [Compose command-line reference (Compose 命令列參考)](http://docs.docker.com/compose/reference/) 和[使用者指南](http://docs.docker.com/compose/)。</span><span class="sxs-lookup"><span data-stu-id="84432-156">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="84432-157">使用 Azure 資源管理員範本 (您自己的範本或 [社群](https://azure.microsoft.com/documentation/templates/)提供的範本) 部署包含 Docker 的 Azure VM，以及使用 Compose 設定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="84432-157">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="84432-158">例如， [以 Docker 部署 WordPress 部落格](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) 範本使用 Docker 和 Compose，藉由 Ubuntu VM 上的 MySQL 後端快速部署 WordPress。</span><span class="sxs-lookup"><span data-stu-id="84432-158">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="84432-159">嘗試整合 Docker Compose 與 Docker Swarm 叢集。</span><span class="sxs-lookup"><span data-stu-id="84432-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="84432-160">如需案例，請參閱[搭配使用 Compose 與 Swarm (英文)](https://docs.docker.com/compose/swarm/)。</span><span class="sxs-lookup"><span data-stu-id="84432-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
