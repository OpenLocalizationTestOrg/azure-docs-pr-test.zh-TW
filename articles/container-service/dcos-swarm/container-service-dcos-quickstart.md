---
title: "aaaAzure 容器服務快速入門-部署的作業系統 DC/叢集 |Microsoft 文件"
description: "Azure Container Service 快速入門 - 部署 DC/OS 叢集"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="58f6c-104">部署 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="58f6c-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="58f6c-105">DC/OS 所提供的分散式平台可執行現代及容器化的應用程式。</span><span class="sxs-lookup"><span data-stu-id="58f6c-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="58f6c-106">透過 Azure Container Service 可簡單又快速地佈建生產環境就緒 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="58f6c-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="58f6c-107">DC/OS 叢集並執行基本的工作負載需要 toodeploy 此快速入門的詳細資料 hello 基本步驟。</span><span class="sxs-lookup"><span data-stu-id="58f6c-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="58f6c-108">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="58f6c-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="58f6c-109">本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="58f6c-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="58f6c-110">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="58f6c-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="58f6c-111">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="58f6c-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="58f6c-112">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="58f6c-112">Log in tooAzure</span></span> 

<span data-ttu-id="58f6c-113">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="58f6c-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="58f6c-114">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="58f6c-114">Create a resource group</span></span>

<span data-ttu-id="58f6c-115">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="58f6c-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="58f6c-116">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="58f6c-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="58f6c-117">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="58f6c-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="58f6c-118">建立 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="58f6c-118">Create DC/OS cluster</span></span>

<span data-ttu-id="58f6c-119">建立以 hello DC/OS 叢集[az acs 建立](/cli/azure/acs#create)命令。</span><span class="sxs-lookup"><span data-stu-id="58f6c-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="58f6c-120">hello 下列範例會建立名為 DC/OS 叢集*myDCOSCluster*並建立 SSH 金鑰，如果它們尚不存在。</span><span class="sxs-lookup"><span data-stu-id="58f6c-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="58f6c-121">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="58f6c-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="58f6c-122">幾分鐘之後，hello 命令完成，且傳回 hello 部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="58f6c-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="58f6c-123">TooDC/OS 叢集連線</span><span class="sxs-lookup"><span data-stu-id="58f6c-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="58f6c-124">一旦建立 DC/OS 叢集之後，可透過 SSH 通道加以存取。</span><span class="sxs-lookup"><span data-stu-id="58f6c-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="58f6c-125">執行下列命令 tooreturn hello 公用 IP 位址的 hello DC/OS master hello。</span><span class="sxs-lookup"><span data-stu-id="58f6c-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="58f6c-126">此 IP 位址是儲存在變數中，而且用於 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="58f6c-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="58f6c-127">toocreate hello SSH 通道，執行下列命令的 hello 並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="58f6c-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="58f6c-128">如果連接埠 80 已在使用中，hello 命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="58f6c-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="58f6c-129">更新 hello 通道連接埠 tooone 不在使用中，例如`85:localhost:80`。</span><span class="sxs-lookup"><span data-stu-id="58f6c-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="58f6c-130">進行測試 hello SSH 通道，請瀏覽過`http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="58f6c-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="58f6c-131">如果連接埠已使用 80，其他調整 hello 位置 toomatch。</span><span class="sxs-lookup"><span data-stu-id="58f6c-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="58f6c-132">如果已成功建立 hello SSH 通道，則會傳回 hello DC/OS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="58f6c-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![DCOS UI](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="58f6c-134">安裝 DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="58f6c-134">Install DC/OS CLI</span></span>

<span data-ttu-id="58f6c-135">hello DC/OS 命令列介面是使用的 toomanage DC/OS 叢集中，從命令列 hello。</span><span class="sxs-lookup"><span data-stu-id="58f6c-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="58f6c-136">安裝使用 hello hello DC/OS cli [az acs dcos 安裝 cli](/azure/acs/dcos#install-cli)命令。</span><span class="sxs-lookup"><span data-stu-id="58f6c-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="58f6c-137">如果您使用 Azure CloudShell，hello DC/OS CLI 已安裝。</span><span class="sxs-lookup"><span data-stu-id="58f6c-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="58f6c-138">如果您執行 hello Azure CLI macOS 或 Linux 上，您可能需要具有 sudo toorun hello 命令。</span><span class="sxs-lookup"><span data-stu-id="58f6c-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="58f6c-139">之前可使用 CLI 來與 hello 叢集 hello，它必須設定的 toouse hello SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="58f6c-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="58f6c-140">toodo 因此，執行下列命令，如有需要調整 hello 連接埠的 hello。</span><span class="sxs-lookup"><span data-stu-id="58f6c-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="58f6c-141">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="58f6c-141">Run an application</span></span>

<span data-ttu-id="58f6c-142">hello 預設排程 ACS DC/OS 叢集中的機制是馬拉松。</span><span class="sxs-lookup"><span data-stu-id="58f6c-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="58f6c-143">馬拉松是使用的 toostart 的應用程式，並管理 hello hello hello DC/OS 叢集上的應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="58f6c-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="58f6c-144">tooschedule 馬拉松，透過應用程式建立名為*馬拉松 app.json*，並複製 hello 遵循到其中的內容。</span><span class="sxs-lookup"><span data-stu-id="58f6c-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="58f6c-145">執行下列命令 tooschedule hello 應用程式 toorun hello DC/OS 叢集上的 hello。</span><span class="sxs-lookup"><span data-stu-id="58f6c-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="58f6c-146">hello 應用程式中，執行下列命令的 hello toosee hello 部署狀態。</span><span class="sxs-lookup"><span data-stu-id="58f6c-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="58f6c-147">當 hello**等候**資料行值會從切換*True*太*False*，應用程式部署已完成。</span><span class="sxs-lookup"><span data-stu-id="58f6c-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="58f6c-148">收到 hello 公用 IP 位址的 hello DC/OS 叢集代理程式。</span><span class="sxs-lookup"><span data-stu-id="58f6c-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="58f6c-149">瀏覽 toothis 位址傳回 hello 預設 NGINX 站台。</span><span class="sxs-lookup"><span data-stu-id="58f6c-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="58f6c-151">刪除 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="58f6c-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="58f6c-152">當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 DC/OS 叢集，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="58f6c-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="58f6c-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58f6c-153">Next steps</span></span>

<span data-ttu-id="58f6c-154">在這個快速入門中，您已部署的作業系統 DC/叢集，並擁有 hello 叢集上執行簡單的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="58f6c-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="58f6c-155">進一步了解 Azure 容器服務，toolearn 繼續 toohello ACS 教學課程。</span><span class="sxs-lookup"><span data-stu-id="58f6c-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="58f6c-156">管理 ACS DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="58f6c-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)