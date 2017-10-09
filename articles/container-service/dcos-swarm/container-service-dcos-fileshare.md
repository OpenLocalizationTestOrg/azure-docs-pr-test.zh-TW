---
title: "aaaFile 共用 Azure DC/OS 叢集 |Microsoft 文件"
description: "建立並掛接檔案共用 tooa DC/OS 中的叢集 Azure 容器服務"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, Containers, Micro-services, Mesos, Azure, FileShare, cifs, 容器, 微服務"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="d8482-104">建立並掛接檔案共用 tooa DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d8482-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="d8482-105">本教學課程會詳細說明如何 toocreate 檔案共用在 Azure 中，並將其裝載每個代理程式與主機 hello DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8482-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="d8482-106">設定檔案共用可讓您更輕鬆 tooshare 檔案跨例如設定、 存取、 記錄檔，以及多個叢集。</span><span class="sxs-lookup"><span data-stu-id="d8482-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="d8482-107">在此教學課程中，會完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="d8482-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d8482-108">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d8482-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="d8482-109">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="d8482-109">Create a file share</span></span>
> * <span data-ttu-id="d8482-110">掛接 hello hello DC/OS 叢集中的共用</span><span class="sxs-lookup"><span data-stu-id="d8482-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="d8482-111">您必須在本教學課程步驟的叢集 toocomplete hello ACS DC/OS。</span><span class="sxs-lookup"><span data-stu-id="d8482-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="d8482-112">如有需要，[此指令碼範例](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)可為您建立一個叢集。</span><span class="sxs-lookup"><span data-stu-id="d8482-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="d8482-113">本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d8482-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d8482-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="d8482-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d8482-115">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d8482-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="d8482-116">在 Microsoft Azure 上建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="d8482-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="d8482-117">之前使用 Azure 檔案共用與 DC/OS ACS 叢集，您必須建立 hello 儲存體帳戶和檔案共用。</span><span class="sxs-lookup"><span data-stu-id="d8482-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="d8482-118">執行下列指令碼 toocreate hello 存放區和檔案共用的 hello。</span><span class="sxs-lookup"><span data-stu-id="d8482-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="d8482-119">更新從您的環境 thoes hello 參數。</span><span class="sxs-lookup"><span data-stu-id="d8482-119">Update hello parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="d8482-120">裝載在叢集中的 hello 共用</span><span class="sxs-lookup"><span data-stu-id="d8482-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="d8482-121">接下來，hello 檔案共用需要 toobe 裝載在叢集內每個虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="d8482-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="d8482-122">這項工作已完成使用 hello cifs 工具/通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d8482-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="d8482-123">hello 掛上操作可以手動方式完成，或針對 hello 叢集中的每個節點執行的指令碼的 hello 叢集中，每個節點上。</span><span class="sxs-lookup"><span data-stu-id="d8482-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="d8482-124">在此範例中，執行兩個指令碼、 一 toomount hello Azure 檔案共用，以及第二個 toorun 此指令碼 hello DC/OS 叢集的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="d8482-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="d8482-125">首先，需要 hello Azure 儲存體帳戶名稱和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d8482-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="d8482-126">執行下列命令 tooget hello 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="d8482-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="d8482-127">請將每一個記下，稍後步驟中將會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="d8482-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="d8482-128">儲存體帳戶名稱︰</span><span class="sxs-lookup"><span data-stu-id="d8482-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="d8482-129">儲存體帳戶存取金鑰︰</span><span class="sxs-lookup"><span data-stu-id="d8482-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="d8482-130">接下來，取得 hello hello 主要 DC/OS，並將它儲存在變數中的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d8482-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="d8482-131">複製您的私用金鑰 toohello 主要節點。</span><span class="sxs-lookup"><span data-stu-id="d8482-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="d8482-132">此索引鍵是所需的 toocreate ssh 連線與 hello 叢集中的所有節點。</span><span class="sxs-lookup"><span data-stu-id="d8482-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="d8482-133">如果建立 hello 叢集時使用非預設值，請更新 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d8482-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="d8482-134">建立 SSH 連線與 hello 主要 （或 hello 第一個主要） 的 DC/作業系統為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="d8482-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="d8482-135">如果建立 hello 叢集時使用非預設值，請更新 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d8482-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="d8482-136">建立名為**cifsMount.sh**，並複製 hello 遵循到其中的內容。</span><span class="sxs-lookup"><span data-stu-id="d8482-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="d8482-137">此指令碼是使用的 toomount hello Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="d8482-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="d8482-138">更新 hello`STORAGE_ACCT_NAME`和`ACCESS_KEY`稍早收集到的 hello 資訊的變數。</span><span class="sxs-lookup"><span data-stu-id="d8482-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="d8482-139">建立第二個名為**getNodesRunScript.sh**並複製 hello 遵循到 hello 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="d8482-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="d8482-140">此指令碼會探索所有叢集節點，然後再執行 hello **cifsMount.sh**上每個指令碼 toomount hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="d8482-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="d8482-141">Hello 叢集的所有節點上執行 hello 指令碼 toomount hello Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="d8482-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="d8482-142">hello 檔案共用現在是可存取`/mnt/share/dcosshare`hello 叢集的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="d8482-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8482-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8482-143">Next steps</span></span>

<span data-ttu-id="d8482-144">在本教學課程 Azure 檔案共用已提出可用 tooa DC/OS 叢集使用 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="d8482-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d8482-145">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d8482-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="d8482-146">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="d8482-146">Create a file share</span></span>
> * <span data-ttu-id="d8482-147">掛接 hello hello DC/OS 叢集中的共用</span><span class="sxs-lookup"><span data-stu-id="d8482-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="d8482-148">前進 toohello 下一個教學課程的 toolearn 有關在 Azure 中的 DC/OS 與整合 Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="d8482-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8482-149">負載平衡應用程式</span><span class="sxs-lookup"><span data-stu-id="d8482-149">Load balance applications</span></span>](container-service-dcos-acr.md)