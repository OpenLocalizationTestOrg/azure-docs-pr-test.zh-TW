---
title: 在 Azure 中的開發虛擬機器上部署 ElasticSearch
description: 教學課程 - 在 Azure 中的開發 Linux VM 上安裝彈性堆疊
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rloutlaw
manager: justhe
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: tutorial
ms.date: 10/11/2017
ms.author: routlaw
ms.openlocfilehash: 5b0b51504478cc0d501a89760ccd60808a69ccbd
ms.sourcegitcommit: 694e40a193980dea1e2f945471071f11030d5641
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="install-the-elastic-stack-on-an-azure-vm"></a><span data-ttu-id="31526-103">在 Azure VM 上安裝彈性堆疊</span><span class="sxs-lookup"><span data-stu-id="31526-103">Install the Elastic Stack on an Azure VM</span></span>

<span data-ttu-id="31526-104">本文將逐步引導您了解如何在 Azure 中的 Ubuntu VM 上部署 [Elasticsearch](https://www.elastic.co/products/elasticsearch) \(英文\)、[Logstash](https://www.elastic.co/products/logstash) \(英文\) 和 [Kibana](https://www.elastic.co/products/kibana) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="31526-104">This article walks you through how to deploy [Elasticsearch](https://www.elastic.co/products/elasticsearch), [Logstash](https://www.elastic.co/products/logstash), and [Kibana](https://www.elastic.co/products/kibana), on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="31526-105">若要查看運作中的彈性堆疊，您可以選擇性地連接到 Kibana，然後處理一些記錄資料的範例。</span><span class="sxs-lookup"><span data-stu-id="31526-105">To see the Elastic Stack in action, you can optionally connect to Kibana  and work with some sample logging data.</span></span> 

<span data-ttu-id="31526-106">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="31526-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31526-107">在 Azure 資源群組中建立 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="31526-107">Create an Ubuntu VM in an Azure resource group</span></span>
> * <span data-ttu-id="31526-108">在 VM 上安裝 Elasticsearch、Logstash 和 Kibana</span><span class="sxs-lookup"><span data-stu-id="31526-108">Install Elasticsearch, Logstash, and Kibana on the VM</span></span>
> * <span data-ttu-id="31526-109">使用 Logstash 將範例資料傳送至 Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="31526-109">Send sample data to Elasticsearch with Logstash</span></span> 
> * <span data-ttu-id="31526-110">開啟連接埠並處理 Kibana 主控台中的資料</span><span class="sxs-lookup"><span data-stu-id="31526-110">Open ports and work with data in the Kibana console</span></span>


 <span data-ttu-id="31526-111">此部署適用於具有彈性堆疊的基本開發。</span><span class="sxs-lookup"><span data-stu-id="31526-111">This deployment is suitable for basic development with the Elastic Stack.</span></span> <span data-ttu-id="31526-112">如需彈性堆疊的詳細資訊，包括適用於生產環境的建議，請參閱 [Elastic 文件](https://www.elastic.co/guide/index.html) \(英文\) 與 [Azure 架構中心](/azure/architecture/elasticsearch/)。</span><span class="sxs-lookup"><span data-stu-id="31526-112">For more on the Elastic Stack, including recommendations for a production environment, see the [Elastic documentation](https://www.elastic.co/guide/index.html) and the [Azure Architecture Center](/azure/architecture/elasticsearch/).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="31526-113">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="31526-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="31526-114">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="31526-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="31526-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="31526-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="31526-116">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="31526-116">Create a resource group</span></span>

<span data-ttu-id="31526-117">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="31526-117">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="31526-118">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="31526-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="31526-119">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="31526-119">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="31526-120">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="31526-120">Create a virtual machine</span></span>

<span data-ttu-id="31526-121">使用 [az vm create](/cli/azure/vm#create) 命令來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="31526-121">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="31526-122">下列範例會建立名為 myVM 的 VM，並建立 SSH 金鑰 (如果它們不存在於預設金鑰位置)。</span><span class="sxs-lookup"><span data-stu-id="31526-122">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="31526-123">若要使用特定的一组密钥，请使用 `--ssh-key-value` 选项。</span><span class="sxs-lookup"><span data-stu-id="31526-123">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="31526-124">建立 VM 後，Azure CLI 會顯示類似下列範例的資訊。</span><span class="sxs-lookup"><span data-stu-id="31526-124">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="31526-125">記下 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="31526-125">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="31526-126">此位址用來存取 VM。</span><span class="sxs-lookup"><span data-stu-id="31526-126">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="31526-127">透過 SSH 連線到您的 VM</span><span class="sxs-lookup"><span data-stu-id="31526-127">SSH into your VM</span></span>

<span data-ttu-id="31526-128">如果您還不知道您 VM 的公用 IP 位址，請執行 [az network public-ip list](/cli/azure/network/public-ip#list) 命令：</span><span class="sxs-lookup"><span data-stu-id="31526-128">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>

```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="31526-129">使用下列命令，建立與虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="31526-129">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="31526-130">替換為您虛擬機器的正確公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="31526-130">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="31526-131">在此範例中，IP 位址是 *40.68.254.142*。</span><span class="sxs-lookup"><span data-stu-id="31526-131">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

## <a name="install-the-elastic-stack"></a><span data-ttu-id="31526-132">安裝彈性堆疊</span><span class="sxs-lookup"><span data-stu-id="31526-132">Install the Elastic Stack</span></span>

<span data-ttu-id="31526-133">匯入 Elasticsearch 簽署金鑰並更新您的 APT 來源清單，以包含 Elastic 套件存放庫：</span><span class="sxs-lookup"><span data-stu-id="31526-133">Import the Elasticsearch signing key and update your APT sources list to include the Elastic package repository:</span></span>

```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
```

<span data-ttu-id="31526-134">在 VM 上安裝 Java 虛擬機器並設定 JAVA_HOME 變數 - 這是執行彈性堆疊元件所需的變數。</span><span class="sxs-lookup"><span data-stu-id="31526-134">Install the Java Virtual on the VM and configure the JAVA_HOME variable-this is necessary for the Elastic Stack components to run.</span></span>

```bash
sudo apt update && sudo apt install openjdk-8-jre-headless
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```

<span data-ttu-id="31526-135">執行下列命令以更新 Ubuntu 套件來源，並安裝 Elasticsearch、Kibana 和 Logstash。</span><span class="sxs-lookup"><span data-stu-id="31526-135">Run the following commands to update Ubuntu package sources and install Elasticsearch, Kibana, and Logstash.</span></span>

```bash
sudo apt update && sudo apt install elasticsearch kibana logstash   
```

> [!NOTE]
> <span data-ttu-id="31526-136">詳細的安裝指示 (包括目錄配置和初始設定) 保留在 [Elastic 文件](https://www.elastic.co/guide/en/elastic-stack/current/installing-elastic-stack.html) \(英文\) 中</span><span class="sxs-lookup"><span data-stu-id="31526-136">Detailed installation instructions, including directory layouts and initial configuration, are maintained in [Elastic's documentation](https://www.elastic.co/guide/en/elastic-stack/current/installing-elastic-stack.html)</span></span>

## <a name="start-elasticsearch"></a><span data-ttu-id="31526-137">啟動 Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="31526-137">Start Elasticsearch</span></span> 

<span data-ttu-id="31526-138">使用下列命令啟動 VM 上的 Elasticsearch：</span><span class="sxs-lookup"><span data-stu-id="31526-138">Start Elasticsearch on your VM with the following command:</span></span>

```bash
sudo systemctl start elasticsearch.service
```

<span data-ttu-id="31526-139">此命令不會產生任何輸出，因此請使用這個 `curl` 命令，確認 Elasticsearch 正在 VM 上執行：</span><span class="sxs-lookup"><span data-stu-id="31526-139">This command produces no output, so verify that Elasticsearch is running on the VM with this `curl` command:</span></span>

```bash
curl -XGET 'localhost:9200/'
```

<span data-ttu-id="31526-140">如果 Elasticsearch 正在執行，您應該會看到如以下的輸出：</span><span class="sxs-lookup"><span data-stu-id="31526-140">If Elasticsearch is running, you see output like the following:</span></span>

```json
{
  "name" : "w6Z4NwR",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "SDzCajBoSK2EkXmHvJVaDQ",
  "version" : {
    "number" : "5.6.3",
    "build_hash" : "1a2f265",
    "build_date" : "2017-10-06T20:33:39.012Z",
    "build_snapshot" : false,
    "lucene_version" : "6.6.1"
  },
  "tagline" : "You Know, for Search"
}
```

## <a name="start-logstash-and-add-data-to-elasticsearch"></a><span data-ttu-id="31526-141">啟動 Logstash，並將資料新增至 Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="31526-141">Start Logstash and add data to Elasticsearch</span></span>

<span data-ttu-id="31526-142">使用下列命令啟動 Logstash：</span><span class="sxs-lookup"><span data-stu-id="31526-142">Start Logstash with the following command:</span></span>

```bash 
sudo systemctl start logstash.service
```

<span data-ttu-id="31526-143">在互動模式下測試 Logstash ，以確定它正常運作：</span><span class="sxs-lookup"><span data-stu-id="31526-143">Test Logstash in interactive mode to make sure it's working correctly:</span></span>

```bash
sudo /usr/share/logstash/bin/logstash -e 'input { stdin { } } output { stdout {} }'
```

<span data-ttu-id="31526-144">這是基本的 logstash [管線](https://www.elastic.co/guide/en/logstash/5.6/pipeline.html) \(英文\)，可回應標準輸出的標準輸入。</span><span class="sxs-lookup"><span data-stu-id="31526-144">This is a basic logstash [pipeline](https://www.elastic.co/guide/en/logstash/5.6/pipeline.html) that echoes standard input to standard output.</span></span> 

```output
The stdin plugin is now waiting for input:
hello azure
2017-10-11T20:01:08.904Z myVM hello azure
```

<span data-ttu-id="31526-145">設定 Logstash 將核心訊息從這個 VM 轉送至 Elasticsearch。</span><span class="sxs-lookup"><span data-stu-id="31526-145">Set up Logstash to forward the kernel messages from this VM to Elasticsearch.</span></span> <span data-ttu-id="31526-146">在稱為 `vm-syslog-logstash.conf` 的空白目錄中建立新檔案，然後貼在下列 Logstash 設定中：</span><span class="sxs-lookup"><span data-stu-id="31526-146">Create a new file in an empty directory called `vm-syslog-logstash.conf` and paste in the following Logstash configuration:</span></span>

```Logstash
input {
    stdin {
        type => "stdin-type"
    }

    file {
        type => "syslog"
        path => [ "/var/log/*.log", "/var/log/*/*.log", "/var/log/messages", "/var/log/syslog" ]
        start_position => "beginning"
    }
}

output {

    stdout {
        codec => rubydebug
    }
    elasticsearch {
        hosts  => "localhost:9200"
    }
}
```

<span data-ttu-id="31526-147">測試這個設定，並將 syslog 資料傳送至 Elasticsearch：</span><span class="sxs-lookup"><span data-stu-id="31526-147">Test this configuration and send the syslog data to Elasticsearch:</span></span>

```bash
sudo /usr/share/logstash/bin/logstash -f vm-syslog-logstash.conf
```

<span data-ttu-id="31526-148">當終端機中的 syslog 項目傳送至 Elasticsearch 時，您看到回應。</span><span class="sxs-lookup"><span data-stu-id="31526-148">You see the syslog entries in your terminal echoed as they are sent to Elasticsearch.</span></span> <span data-ttu-id="31526-149">一旦您傳送一些資料之後，使用 `CTRL+C` 退出 Logstash。</span><span class="sxs-lookup"><span data-stu-id="31526-149">Use `CTRL+C` to exit out of Logstash once you've sent some data.</span></span>

## <a name="start-kibana-and-visualize-the-data-in-elasticsearch"></a><span data-ttu-id="31526-150">啟動 Kibana，並將 Elasticsearch 中的資料視覺化</span><span class="sxs-lookup"><span data-stu-id="31526-150">Start Kibana and visualize the data in Elasticsearch</span></span>

<span data-ttu-id="31526-151">編輯 `/etc/kibana/kibana.yml` 並變更 Kibana 接聽的 IP 位址，讓您可以從網頁瀏覽器加以存取。</span><span class="sxs-lookup"><span data-stu-id="31526-151">Edit `/etc/kibana/kibana.yml` and change the IP address Kibana listens on so you can access it from your web browser.</span></span>

```bash
server.host:"0.0.0.0"
```

<span data-ttu-id="31526-152">使用下列命令啟動 Kibana：</span><span class="sxs-lookup"><span data-stu-id="31526-152">Start Kibana with the following command:</span></span>

```bash
sudo systemctl start kibana.service
```

<span data-ttu-id="31526-153">從 Azure CLI 開啟連接埠 5601，以允許從遠端存取 Kibana 主控台：</span><span class="sxs-lookup"><span data-stu-id="31526-153">Open port 5601 from the Azure CLI to allow remote access to the Kibana console:</span></span>

```azurecli-interactive
az vm open-port --port 5601 --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="31526-154">開啟 Kibana 主控台，然後選取 [建立]，以便根據您稍早傳送至 Elasticsearch 的 syslog 資料，產生預設索引。</span><span class="sxs-lookup"><span data-stu-id="31526-154">Open up the Kibana console and select **Create** to generate a default index based on the syslog data you sent to Elasticsearch earlier.</span></span> 

![瀏覽 Kibana 中的 Syslog 事件](media/elasticsearch-install/kibana-index.png)

<span data-ttu-id="31526-156">選取 Kibana 主控台上的 [探索]，以搜尋、瀏覽並篩選 syslog 事件。</span><span class="sxs-lookup"><span data-stu-id="31526-156">Select **Discover** on the Kibana console to search, browse, and filter through the syslog events.</span></span>

![瀏覽 Kibana 中的 Syslog 事件](media/elasticsearch-install/kibana-search-filter.png)

## <a name="next-steps"></a><span data-ttu-id="31526-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31526-158">Next steps</span></span>

<span data-ttu-id="31526-159">在本教學課程中，您將彈性堆疊部署到 Azure 中的開發 VM。</span><span class="sxs-lookup"><span data-stu-id="31526-159">In this tutorial, you deployed the Elastic Stack into a development VM in Azure.</span></span> <span data-ttu-id="31526-160">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="31526-160">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31526-161">在 Azure 資源群組中建立 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="31526-161">Create an Ubuntu VM in an Azure resource group</span></span>
> * <span data-ttu-id="31526-162">在 VM 上安裝 Elasticsearch、Logstash 和 Kibana</span><span class="sxs-lookup"><span data-stu-id="31526-162">Install Elasticsearch, Logstash, and Kibana on the VM</span></span>
> * <span data-ttu-id="31526-163">將範例資料從 Logstash 傳送至 Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="31526-163">Send sample data to Elasticsearch from Logstash</span></span> 
> * <span data-ttu-id="31526-164">開啟連接埠並處理 Kibana 主控台中的資料</span><span class="sxs-lookup"><span data-stu-id="31526-164">Open ports and work with data in the Kibana console</span></span>