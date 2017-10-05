---
title: "Azure Container Service 教學課程 - 管理 DC/OS | Microsoft Docs"
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
ms.openlocfilehash: e93f782c26c32f97749e817ec59ee3c2ecb7e119
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="d6259-104">Azure Container Service 教學課程 - 管理 DC/OS</span><span class="sxs-lookup"><span data-stu-id="d6259-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="d6259-105">DC/OS 所提供的分散式平台可執行現代及容器化的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6259-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="d6259-106">透過 Azure Container Service 可簡單又快速地佈建生產環境就緒 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="d6259-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="d6259-107">本快速入門將詳細說明部署 DC/OS 叢集和執行基本工作負載所需的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="d6259-107">This quick start details basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d6259-108">建立 ACS DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="d6259-109">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-109">Connect to the cluster</span></span>
> * <span data-ttu-id="d6259-110">安裝 DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="d6259-110">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="d6259-111">將應用程式部署到叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-111">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="d6259-112">調整叢集上的應用程式</span><span class="sxs-lookup"><span data-stu-id="d6259-112">Scale an application on the cluster</span></span>
> * <span data-ttu-id="d6259-113">調整 DC/OS 叢集節點</span><span class="sxs-lookup"><span data-stu-id="d6259-113">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="d6259-114">DC/OS 的基本管理</span><span class="sxs-lookup"><span data-stu-id="d6259-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="d6259-115">刪除 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-115">Delete the DC/OS cluster</span></span>

<span data-ttu-id="d6259-116">本教學課程需要 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d6259-116">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d6259-117">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="d6259-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="d6259-118">如果您需要升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d6259-118">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="d6259-119">建立 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-119">Create DC/OS cluster</span></span>

<span data-ttu-id="d6259-120">首先，使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="d6259-120">First, create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d6259-121">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="d6259-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="d6259-122">下列範例會在 westeurope 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d6259-122">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="d6259-123">接下來，使用 [az acs create](/cli/azure/acs#create) 命令來建立 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="d6259-123">Next, create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="d6259-124">下列範例會建立名為 myDCOSCluster 的 DC/OS 叢集，並建立 SSH 金鑰 (如果它們尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="d6259-124">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="d6259-125">若要使用一組特定金鑰，請使用 `--ssh-key-value` 選項。</span><span class="sxs-lookup"><span data-stu-id="d6259-125">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="d6259-126">幾分鐘之後，此命令就會完成，且會傳回部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d6259-126">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="d6259-127">連線到 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-127">Connect to DC/OS cluster</span></span>

<span data-ttu-id="d6259-128">一旦建立 DC/OS 叢集之後，可透過 SSH 通道加以存取。</span><span class="sxs-lookup"><span data-stu-id="d6259-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="d6259-129">執行下列命令，可傳回 DC/OS 主機的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d6259-129">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="d6259-130">此 IP 位址儲存在變數中，且用於下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d6259-130">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="d6259-131">若要建立 SSH 通道，請執行下列命令，並遵循螢幕上的指示。</span><span class="sxs-lookup"><span data-stu-id="d6259-131">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="d6259-132">如果連接埠 80 已在使用中，命令就會失敗。</span><span class="sxs-lookup"><span data-stu-id="d6259-132">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="d6259-133">將通道連接埠更新為非使用中的連接埠，例如 `85:localhost:80`。</span><span class="sxs-lookup"><span data-stu-id="d6259-133">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="d6259-134">安裝 DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="d6259-134">Install DC/OS CLI</span></span>

<span data-ttu-id="d6259-135">使用 [az acs dcos install-cli](/azure/acs/dcos#install-cli) 命令來安裝 DC/OS CLI。</span><span class="sxs-lookup"><span data-stu-id="d6259-135">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="d6259-136">如果您是使用 Azure CloudShell，就已安裝 DC/OS CLI。</span><span class="sxs-lookup"><span data-stu-id="d6259-136">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> <span data-ttu-id="d6259-137">如果您是在 Mac OS 或 Lunix 上執行 Azure CLI，可能需要搭配 sudo 來執行命令。</span><span class="sxs-lookup"><span data-stu-id="d6259-137">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="d6259-138">在 CLI 可與叢集搭配使用之前，它必須先設定為使用 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="d6259-138">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="d6259-139">若要這樣做，請執行下列命令，並視需要調整連接埠。</span><span class="sxs-lookup"><span data-stu-id="d6259-139">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="d6259-140">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d6259-140">Run an application</span></span>

<span data-ttu-id="d6259-141">ACS DC/OS 叢集的預設排程機制為 Marathon。</span><span class="sxs-lookup"><span data-stu-id="d6259-141">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="d6259-142">Marathon 可用來啟動應用程式及管理 DC/OS 叢集上的應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="d6259-142">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="d6259-143">若要透過 Marathon 排程應用程式，請建立名為 **marathon-app.json** 的檔案，並將下列內容複製到其中。</span><span class="sxs-lookup"><span data-stu-id="d6259-143">To schedule an application through Marathon, create a file named **marathon-app.json**, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="d6259-144">執行下列命令可排程要在 DC/OS 叢集上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6259-144">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="d6259-145">若要查看應用程式的部署狀態，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d6259-145">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="d6259-146">當 **TASKS** 資料行值從 0/1 切換為 1/1 時，應用程式部署就已完成。</span><span class="sxs-lookup"><span data-stu-id="d6259-146">When the **TASKS** column value switches from *0/1* to *1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="d6259-147">調整 Marathon 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6259-147">Scale Marathon application</span></span>

<span data-ttu-id="d6259-148">在上述範例中，已建立單一執行個體應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6259-148">In the previous example, a single instance application was created.</span></span> <span data-ttu-id="d6259-149">若要更新此部署，以便讓應用程式的三個執行個體可供使用，請開啟 **marathon-app.json** 檔案，並將執行個體屬性更新為 3。</span><span class="sxs-lookup"><span data-stu-id="d6259-149">To update this deployment so that three instances of the application are available, open up the **marathon-app.json** file, and update the instance property to 3.</span></span>

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

<span data-ttu-id="d6259-150">使用 `dcos marathon app update` 命令更新應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6259-150">Update the application using the `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="d6259-151">若要查看應用程式的部署狀態，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d6259-151">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="d6259-152">當 **TASKS** 資料行值從 1/3 切換為 3/1 時，應用程式部署就已完成。</span><span class="sxs-lookup"><span data-stu-id="d6259-152">When the **TASKS** column value switches from *1/3* to *3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="d6259-153">執行網際網路可存取應用程式</span><span class="sxs-lookup"><span data-stu-id="d6259-153">Run internet accessible app</span></span>

<span data-ttu-id="d6259-154">ACS DC/OS 叢集包含兩個節點集合，一個是可在網際網路上存取的公用節點集合，以及一個不可在網際網路上存取的私人節點集合。</span><span class="sxs-lookup"><span data-stu-id="d6259-154">The ACS DC/OS cluster consists of two node sets, one public which is accessible on the internet, and one private which is not accessible on the internet.</span></span> <span data-ttu-id="d6259-155">預設設定是私人節點，會在最後一個範例中使用。</span><span class="sxs-lookup"><span data-stu-id="d6259-155">The default set is the private nodes, which was used in the last example.</span></span>

<span data-ttu-id="d6259-156">若要讓應用程式可在網際網路上存取，請將其部署至公用節點集合。</span><span class="sxs-lookup"><span data-stu-id="d6259-156">To make an application accessible on the internet, deploy them to the public node set.</span></span> <span data-ttu-id="d6259-157">若要這樣做，請為 `acceptedResourceRoles` 物件提供 `slave_public` 的值。</span><span class="sxs-lookup"><span data-stu-id="d6259-157">To do so, give the `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="d6259-158">建立名為 **nginx-public.json** 的檔案，並將下列內容複製到其中。</span><span class="sxs-lookup"><span data-stu-id="d6259-158">Create a file named **nginx-public.json** and copy the following contents into it.</span></span>

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

<span data-ttu-id="d6259-159">執行下列命令可排程要在 DC/OS 叢集上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6259-159">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="d6259-160">取得 DC/OS 公用叢集代理程式的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d6259-160">Get the public IP address of the DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="d6259-161">瀏覽到這個地址會傳回預設的 NGINX 站台。</span><span class="sxs-lookup"><span data-stu-id="d6259-161">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="d6259-163">調整 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="d6259-164">在上一個範例中，應用程式會調整為多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6259-164">In the previous examples, an application was scaled to multiple instance.</span></span> <span data-ttu-id="d6259-165">也可以調整 DC/OS 基礎結構以提供較多或較少的計算容量。</span><span class="sxs-lookup"><span data-stu-id="d6259-165">The DC/OS infrastructure can also be scaled to provide more or less compute capacity.</span></span> <span data-ttu-id="d6259-166">方法是使用 [az acs scale]() 命令。</span><span class="sxs-lookup"><span data-stu-id="d6259-166">This is done with the [az acs scale]() command.</span></span> 

<span data-ttu-id="d6259-167">若要查看目前 DC/OS 代理程式的計數，請使用 [az acs show](/cli/azure/acs#show) 命令。</span><span class="sxs-lookup"><span data-stu-id="d6259-167">To see the current count of DC/OS agents, use the [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="d6259-168">若要將計數增加至 5，請使用 [az acs scale](/cli/azure/acs#scale) 命令。</span><span class="sxs-lookup"><span data-stu-id="d6259-168">To increase the count to 5, use the [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="d6259-169">刪除 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="d6259-170">若不再需要，您可以使用 [az group delete](/cli/azure/group#delete) 命令將資源群組、DC/OS 叢集和所有相關資源移除。</span><span class="sxs-lookup"><span data-stu-id="d6259-170">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="d6259-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6259-171">Next steps</span></span>

<span data-ttu-id="d6259-172">在本教學課程中，您已了解有關基本的 DC/OS 管理工作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d6259-172">In this tutorial, you have learned about basic DC/OS management task including the following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d6259-173">建立 ACS DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="d6259-174">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-174">Connect to the cluster</span></span>
> * <span data-ttu-id="d6259-175">安裝 DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="d6259-175">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="d6259-176">將應用程式部署到叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-176">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="d6259-177">調整叢集上的應用程式</span><span class="sxs-lookup"><span data-stu-id="d6259-177">Scale an application on the cluster</span></span>
> * <span data-ttu-id="d6259-178">調整 DC/OS 叢集節點</span><span class="sxs-lookup"><span data-stu-id="d6259-178">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="d6259-179">刪除 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="d6259-179">Delete the DC/OS cluster</span></span>

<span data-ttu-id="d6259-180">前往下一個教學課程，可了解在 Azure 上 DC/OS 中的負載平衡應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6259-180">Advance to the next tutorial to learn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6259-181">負載平衡應用程式</span><span class="sxs-lookup"><span data-stu-id="d6259-181">Load balance applications</span></span>](container-service-load-balancing.md)