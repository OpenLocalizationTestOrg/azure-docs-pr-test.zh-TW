---
title: "在 Azure 中建立 Linux 的虛擬機器擴展集 | Microsoft Docs"
description: "在 Linux VM 上使用虛擬機器擴展集，建立及部署高可用性應用程式。"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="6ff19-103">在 Linux 上建立虛擬機器擴展集及部署高可用性應用程式</span><span class="sxs-lookup"><span data-stu-id="6ff19-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="6ff19-104">虛擬機器擴展集可讓您部署和管理一組相同、自動調整的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6ff19-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="6ff19-105">您可以手動調整擴展集中的 VM 數目，或定義規則以根據 CPU 使用量、記憶體需求或網路流量自動調整。</span><span class="sxs-lookup"><span data-stu-id="6ff19-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="6ff19-106">在本教學課程中，您將會在 Azure 部署虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="6ff19-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="6ff19-107">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="6ff19-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6ff19-108">使用 Cloud-init 來建立要調整的應用程式</span><span class="sxs-lookup"><span data-stu-id="6ff19-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="6ff19-109">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="6ff19-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="6ff19-110">增加或減少擴展集內的執行個體數目</span><span class="sxs-lookup"><span data-stu-id="6ff19-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="6ff19-111">檢視擴展集執行個體的連線資訊</span><span class="sxs-lookup"><span data-stu-id="6ff19-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="6ff19-112">在擴展集內使用資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6ff19-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6ff19-113">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6ff19-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6ff19-114">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="6ff19-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="6ff19-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6ff19-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="6ff19-116">擴展集概觀</span><span class="sxs-lookup"><span data-stu-id="6ff19-116">Scale Set overview</span></span>
<span data-ttu-id="6ff19-117">虛擬機器擴展集可讓您部署和管理一組相同、自動調整的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6ff19-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="6ff19-118">擴展集使用的元件，與您在[建立高可用性 VM](tutorial-availability-sets.md) 的先前教學課程中所學習到的元件相同。</span><span class="sxs-lookup"><span data-stu-id="6ff19-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="6ff19-119">擴展集中的 VM 會建立於可用性設定組中並分散於邏輯容錯網域和更新網域。</span><span class="sxs-lookup"><span data-stu-id="6ff19-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="6ff19-120">VM 會視需要建立於擴展集中。</span><span class="sxs-lookup"><span data-stu-id="6ff19-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="6ff19-121">您將定義自動調整規則，以控制如何及何時新增或移除擴展集中的 VM。</span><span class="sxs-lookup"><span data-stu-id="6ff19-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="6ff19-122">您可以根據計量 (例如 CPU 負載、記憶體使用量或網路流量) 觸發這些規則。</span><span class="sxs-lookup"><span data-stu-id="6ff19-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="6ff19-123">當您使用 Azure 平台映像時，擴展集可支援多達 1,000 部 VM。</span><span class="sxs-lookup"><span data-stu-id="6ff19-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="6ff19-124">對於生產工作負載，您可以[建立自訂 VM 映像](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="6ff19-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="6ff19-125">使用自訂映像時，您可以在擴展集中建立多達 100 部 VM。</span><span class="sxs-lookup"><span data-stu-id="6ff19-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="6ff19-126">建立要調整的應用程式</span><span class="sxs-lookup"><span data-stu-id="6ff19-126">Create an app to scale</span></span>
<span data-ttu-id="6ff19-127">為了提供生產環境使用，您可以[建立自訂 VM 映像](tutorial-custom-images.md)，其中包含已安裝和設定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ff19-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="6ff19-128">在本教學課程中，我們會在首次開機時自訂 VM，以便快速查看作用中擴展集。</span><span class="sxs-lookup"><span data-stu-id="6ff19-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="6ff19-129">在先前的教學課程中，您已了解使用 cloud-init [如何在首次開機時自訂 Linux 虛擬機器](tutorial-automate-vm-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="6ff19-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="6ff19-130">您可以使用相同的 cloud-init 組態檔來安裝 NGINX 和執行簡單的 'Hello World' Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ff19-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="6ff19-131">您目前的殼層中，建立名為 cloud-init.txt 的檔案，並貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="6ff19-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="6ff19-132">例如，在 Cloud Shell 中建立不在本機電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="6ff19-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="6ff19-133">輸入 `sensible-editor cloud-init.txt` 可建立檔案，並查看可用的編輯器清單。</span><span class="sxs-lookup"><span data-stu-id="6ff19-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="6ff19-134">請確定已正確複製整個 cloud-init 檔案，特別是第一行：</span><span class="sxs-lookup"><span data-stu-id="6ff19-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="6ff19-135">建立擴展集</span><span class="sxs-lookup"><span data-stu-id="6ff19-135">Create a scale set</span></span>
<span data-ttu-id="6ff19-136">請先使用 [az group create](/cli/azure/group#create) 建立資源群組，才可以建立擴展集。</span><span class="sxs-lookup"><span data-stu-id="6ff19-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6ff19-137">下列範例會在 eastus 位置建立名為 myResourceGroupScaleSet 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="6ff19-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="6ff19-138">現在使用 [az vmss create](/cli/azure/vmss#create) 建立虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="6ff19-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="6ff19-139">下列範例會建立名為 myScaleSet 的擴展集，使用 cloud-int 檔案來自訂 VM，以及產生 SSH 金鑰 (如果不存在)︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="6ff19-140">建立及設定所有擴展集資源和 VM 需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="6ff19-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="6ff19-141">在 Azure CLI 將您返回提示字元之後，背景工作會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="6ff19-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="6ff19-142">可能需要再等候幾分鐘，才能存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ff19-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="6ff19-143">允許 Web 流量</span><span class="sxs-lookup"><span data-stu-id="6ff19-143">Allow web traffic</span></span>
<span data-ttu-id="6ff19-144">負載平衡器會自動建立，作為虛擬機器擴展集的一部分。</span><span class="sxs-lookup"><span data-stu-id="6ff19-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="6ff19-145">負載平衡器會使用負載平衡器規則，將流量分散於一組定義的 VM。</span><span class="sxs-lookup"><span data-stu-id="6ff19-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="6ff19-146">您可以在下一個教學課程[如何平衡 Azure 中虛擬機器的負載](tutorial-load-balancer.md)中，深入了解負載平衡器的概念和設定。</span><span class="sxs-lookup"><span data-stu-id="6ff19-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="6ff19-147">若要允許流量觸達 Web 應用程式，請使用 [az network lb rule create](/cli/azure/network/lb/rule#create) 建立規則。</span><span class="sxs-lookup"><span data-stu-id="6ff19-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="6ff19-148">下列範例會建立名為 myLoadBalancerRuleWeb 的規則：</span><span class="sxs-lookup"><span data-stu-id="6ff19-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="6ff19-149">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="6ff19-149">Test your app</span></span>
<span data-ttu-id="6ff19-150">若要查看 Web 上的 Node.js 應用程式，請使用 [az network public-ip show](/cli/azure/network/public-ip#show) 取得負載平衡器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ff19-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="6ff19-151">下列範例會取得建立作為擴展集一部分的 myScaleSetLBPublicIP IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="6ff19-152">在 Web 瀏覽器中輸入公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ff19-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="6ff19-153">應用程式隨即顯示，包括負載平衡器分散流量之 VM 的主機名稱︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![執行 Node.js 應用程式](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="6ff19-155">若要查看作用中的擴展集，請強制重新整理您的 Web 瀏覽器，以查看負載平衡器如何將流量分散於執行應用程式的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="6ff19-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="6ff19-156">管理工作</span><span class="sxs-lookup"><span data-stu-id="6ff19-156">Management tasks</span></span>
<span data-ttu-id="6ff19-157">在擴展集生命週期中，您可能需要執行一或多個管理工作。</span><span class="sxs-lookup"><span data-stu-id="6ff19-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="6ff19-158">此外，您可以建立指令碼來自動化各種生命週期工作。</span><span class="sxs-lookup"><span data-stu-id="6ff19-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="6ff19-159">Azure CLI 2.0 提供快速的方式來執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="6ff19-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="6ff19-160">以下是一些常見工作。</span><span class="sxs-lookup"><span data-stu-id="6ff19-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="6ff19-161">檢視擴展集中的 VM</span><span class="sxs-lookup"><span data-stu-id="6ff19-161">View VMs in a scale set</span></span>
<span data-ttu-id="6ff19-162">若要檢視在擴展集中執行的 VM 清單，請使用 [az vmss list-instances](/cli/azure/vmss#list-instances)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="6ff19-163">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="6ff19-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="6ff19-164">增加或減少 VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="6ff19-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="6ff19-165">若要查看擴展集中目前擁有的執行個體數目，請使用 [az vmss show](/cli/azure/vmss#show)並查詢 sku.capacity：</span><span class="sxs-lookup"><span data-stu-id="6ff19-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="6ff19-166">然後，您可以使用 [az vmss scale](/cli/azure/vmss#scale)，手動增加或減少擴展集中的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="6ff19-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="6ff19-167">下列範例會將擴展集中的 VM 數目設定為 5：</span><span class="sxs-lookup"><span data-stu-id="6ff19-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="6ff19-168">自動調整規則可讓您定義如何在擴展集中相應增加或相應減少 VM 的數目，以回應例如網路流量或 CPU 使用率的需求。</span><span class="sxs-lookup"><span data-stu-id="6ff19-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="6ff19-169">目前，無法在 Azure CLI 2.0 中設定這些規則。</span><span class="sxs-lookup"><span data-stu-id="6ff19-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="6ff19-170">使用 [Azure 入口網站](https://portal.azure.com)以設定自動調整。</span><span class="sxs-lookup"><span data-stu-id="6ff19-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="6ff19-171">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="6ff19-171">Get connection info</span></span>
<span data-ttu-id="6ff19-172">若要取得擴展集中 VM 的相關連線資訊，請使用 [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info)。</span><span class="sxs-lookup"><span data-stu-id="6ff19-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="6ff19-173">此命令會輸出每部 VM 的公用 IP 位址和連接埠，可讓您與 SSH 連線︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="6ff19-174">使用資料磁碟搭配擴展集</span><span class="sxs-lookup"><span data-stu-id="6ff19-174">Use data disks with scale sets</span></span>
<span data-ttu-id="6ff19-175">您可以建立及使用資料磁碟搭配擴展集。</span><span class="sxs-lookup"><span data-stu-id="6ff19-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="6ff19-176">在先前的教學課程中，您已了解如何[管理 Azure 磁碟](tutorial-manage-disks.md)，其中概述了在資料磁碟上 (不是在 OS 磁碟上) 建置應用程式的最佳做法和效能改進。</span><span class="sxs-lookup"><span data-stu-id="6ff19-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="6ff19-177">使用資料磁碟建立擴展集</span><span class="sxs-lookup"><span data-stu-id="6ff19-177">Create scale set with data disks</span></span>
<span data-ttu-id="6ff19-178">若要建立擴展集並連結資料磁碟，可將 `--data-disk-sizes-gb` 參數新增到 [az vmss create](/cli/azure/vmss#create)命令。</span><span class="sxs-lookup"><span data-stu-id="6ff19-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="6ff19-179">下列範例會建立有 50GB 資料磁碟且連結到每個執行個體的擴展集︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="6ff19-180">當執行個體從擴展集移除時，所有連結的資料磁碟也會一併移除。</span><span class="sxs-lookup"><span data-stu-id="6ff19-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="6ff19-181">新增資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6ff19-181">Add data disks</span></span>
<span data-ttu-id="6ff19-182">若要將資料磁碟新增到擴展集中的執行個體，請使用 [az vmss disk attach](/cli/azure/vmss/disk#attach)。</span><span class="sxs-lookup"><span data-stu-id="6ff19-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="6ff19-183">下列範例會將 50GB 的磁碟新增到每個執行個體：</span><span class="sxs-lookup"><span data-stu-id="6ff19-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="6ff19-184">卸離資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6ff19-184">Detach data disks</span></span>
<span data-ttu-id="6ff19-185">若要將資料磁碟從擴展集中的執行個體上移除，請使用 [az vmss disk detach](/cli/azure/vmss/disk#detach)。</span><span class="sxs-lookup"><span data-stu-id="6ff19-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="6ff19-186">下列範例會從每個執行個體移除在 LUN 2 的資料磁碟︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="6ff19-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ff19-187">Next steps</span></span>
<span data-ttu-id="6ff19-188">在本教學課程中，您已建立虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="6ff19-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="6ff19-189">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="6ff19-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6ff19-190">使用 Cloud-init 來建立要調整的應用程式</span><span class="sxs-lookup"><span data-stu-id="6ff19-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="6ff19-191">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="6ff19-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="6ff19-192">增加或減少擴展集內的執行個體數目</span><span class="sxs-lookup"><span data-stu-id="6ff19-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="6ff19-193">檢視擴展集執行個體的連線資訊</span><span class="sxs-lookup"><span data-stu-id="6ff19-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="6ff19-194">在擴展集內使用資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6ff19-194">Use data disks in a scale set</span></span>

<span data-ttu-id="6ff19-195">請前進到下一個教學課程，以深入了解虛擬機器的負載平衡概念。</span><span class="sxs-lookup"><span data-stu-id="6ff19-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ff19-196">平衡虛擬機器的負載</span><span class="sxs-lookup"><span data-stu-id="6ff19-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)