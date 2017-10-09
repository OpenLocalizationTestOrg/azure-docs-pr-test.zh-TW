---
title: "aaaAzure 容器服務教學課程-管理 DC/OS |Microsoft 文件"
description: "Azure Container Service 教學課程 - 管理 DC/OS"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="1ebe5-104">Azure Container Service 教學課程 - 管理 DC/OS</span><span class="sxs-lookup"><span data-stu-id="1ebe5-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="1ebe5-105">DC/OS 所提供的分散式平台可執行現代及容器化的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="1ebe5-106">透過 Azure Container Service 可簡單又快速地佈建生產環境就緒 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="1ebe5-107">DC/OS 叢集並執行基本的工作負載需要 toodeploy 此快速入門詳細資料的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ebe5-108">建立 ACS DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="1ebe5-109">Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="1ebe5-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="1ebe5-110">安裝 hello DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="1ebe5-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="1ebe5-111">部署應用程式 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="1ebe5-112">調整 hello 叢集上的應用程式</span><span class="sxs-lookup"><span data-stu-id="1ebe5-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="1ebe5-113">調整 hello DC/OS 叢集節點</span><span class="sxs-lookup"><span data-stu-id="1ebe5-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="1ebe5-114">DC/OS 的基本管理</span><span class="sxs-lookup"><span data-stu-id="1ebe5-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="1ebe5-115">刪除 hello DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="1ebe5-116">本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1ebe5-117">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1ebe5-118">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="1ebe5-119">建立 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-119">Create DC/OS cluster</span></span>

<span data-ttu-id="1ebe5-120">首先，建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1ebe5-121">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="1ebe5-122">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westeurope*位置。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="1ebe5-123">接下來，建立 hello DC/OS 叢集[az acs 建立](/cli/azure/acs#create)命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="1ebe5-124">hello 下列範例會建立名為 DC/OS 叢集*myDCOSCluster*並建立 SSH 金鑰，如果它們尚不存在。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="1ebe5-125">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="1ebe5-126">幾分鐘之後，hello 命令完成，且傳回 hello 部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="1ebe5-127">TooDC/OS 叢集連線</span><span class="sxs-lookup"><span data-stu-id="1ebe5-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="1ebe5-128">一旦建立 DC/OS 叢集之後，可透過 SSH 通道加以存取。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="1ebe5-129">執行下列命令 tooreturn hello 公用 IP 位址的 hello DC/OS master hello。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="1ebe5-130">此 IP 位址是儲存在變數中，而且用於 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="1ebe5-131">toocreate hello SSH 通道，執行下列命令的 hello 並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="1ebe5-132">如果連接埠 80 已在使用中，hello 命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="1ebe5-133">更新 hello 通道連接埠 tooone 不在使用中，例如`85:localhost:80`。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="1ebe5-134">安裝 DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="1ebe5-134">Install DC/OS CLI</span></span>

<span data-ttu-id="1ebe5-135">安裝使用 hello hello DC/OS cli [az acs dcos 安裝 cli](/azure/acs/dcos#install-cli)命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="1ebe5-136">如果您使用 Azure CloudShell，hello DC/OS CLI 已安裝。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="1ebe5-137">如果您執行 hello Azure CLI macOS 或 Linux 上，您可能需要具有 sudo toorun hello 命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="1ebe5-138">之前可使用 CLI 來與 hello 叢集 hello，它必須設定的 toouse hello SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="1ebe5-139">toodo 因此，執行下列命令，如有需要調整 hello 連接埠的 hello。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="1ebe5-140">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="1ebe5-140">Run an application</span></span>

<span data-ttu-id="1ebe5-141">hello 預設排程 ACS DC/OS 叢集中的機制是馬拉松。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="1ebe5-142">馬拉松是使用的 toostart 的應用程式，並管理 hello hello hello DC/OS 叢集上的應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="1ebe5-143">tooschedule 馬拉松，透過應用程式建立名為**馬拉松 app.json**，並複製 hello 遵循到其中的內容。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
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
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="1ebe5-144">執行下列命令 tooschedule hello 應用程式 toorun hello DC/OS 叢集上的 hello。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="1ebe5-145">hello 應用程式中，執行下列命令的 hello toosee hello 部署狀態。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="1ebe5-146">當 hello**工作**資料行值會從切換*0/1*太*1/1*，應用程式部署已完成。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="1ebe5-147">調整 Marathon 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ebe5-147">Scale Marathon application</span></span>

<span data-ttu-id="1ebe5-148">在 hello 前一個範例中，建立單一執行個體的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="1ebe5-149">此部署，以便 hello 應用程式的三個執行個體可用，開啟 hello tooupdate**馬拉松 app.json**檔案，並更新 hello 執行個體屬性 too3。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="1ebe5-150">更新 hello 應用程式使用 hello`dcos marathon app update`命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="1ebe5-151">hello 應用程式中，執行下列命令的 hello toosee hello 部署狀態。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="1ebe5-152">當 hello**工作**資料行值會從切換*1/3*太*3/1*，應用程式部署已完成。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="1ebe5-153">執行網際網路可存取應用程式</span><span class="sxs-lookup"><span data-stu-id="1ebe5-153">Run internet accessible app</span></span>

<span data-ttu-id="1ebe5-154">hello ACS DC/OS 叢集包含兩個節點集合，可存取在上一個公用 hello 網際網路，並不能存取在其中一個私用 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="1ebe5-155">hello 預設集是 hello 私用的節點，這使用於 hello 最後一個範例。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="1ebe5-156">應用程式存取 toomake hello 網際網路，將其部署 toohello 公用節點集。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="1ebe5-157">toodo，授與 hello`acceptedResourceRoles`物件的值`slave_public`。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="1ebe5-158">建立名為**nginx public.json**並複製 hello 遵循到其中的內容。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

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

<span data-ttu-id="1ebe5-159">執行下列命令 tooschedule hello 應用程式 toorun hello DC/OS 叢集上的 hello。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="1ebe5-160">收到 hello 公用 IP 位址的 hello DC/OS 公用叢集代理程式。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="1ebe5-161">瀏覽 toothis 位址傳回 hello 預設 NGINX 站台。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="1ebe5-163">調整 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="1ebe5-164">在 hello 上述範例中，應用程式會是縮放的 toomultiple 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="1ebe5-165">hello DC/OS 基礎結構也可以縮放的 tooprovide 更多或更少計算容量。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="1ebe5-166">這是以 hello [az acs 調整]()命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="1ebe5-167">toosee hello 目前計數的 DC/OS 代理程式，使用 hello [az acs 顯示](/cli/azure/acs#show)命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="1ebe5-168">tooincrease hello 計數 too5，請使用 hello [az acs 調整](/cli/azure/acs#scale)命令。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="1ebe5-169">刪除 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="1ebe5-170">當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 DC/OS 叢集，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="1ebe5-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ebe5-171">Next steps</span></span>

<span data-ttu-id="1ebe5-172">在本教學課程中，您已經學會基本的 DC/OS 管理工作，包括 hello 下列有關。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="1ebe5-173">建立 ACS DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="1ebe5-174">Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="1ebe5-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="1ebe5-175">安裝 hello DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="1ebe5-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="1ebe5-176">部署應用程式 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="1ebe5-177">調整 hello 叢集上的應用程式</span><span class="sxs-lookup"><span data-stu-id="1ebe5-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="1ebe5-178">調整 hello DC/OS 叢集節點</span><span class="sxs-lookup"><span data-stu-id="1ebe5-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="1ebe5-179">刪除 hello DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="1ebe5-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="1ebe5-180">進階 toohello 下一個教學課程 toolearn 有關負載平衡的應用程式在 Azure 上的 DC/OS。</span><span class="sxs-lookup"><span data-stu-id="1ebe5-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ebe5-181">負載平衡應用程式</span><span class="sxs-lookup"><span data-stu-id="1ebe5-181">Load balance applications</span></span>](container-service-load-balancing.md)