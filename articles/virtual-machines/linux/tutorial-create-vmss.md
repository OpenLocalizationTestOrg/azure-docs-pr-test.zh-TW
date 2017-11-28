---
title: "在 Azure 中 linux 虛擬機器擴展集 aaaCreate |Microsoft 文件"
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
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="9a5ce-103">在 Linux 上建立虛擬機器擴展集及部署高可用性應用程式</span><span class="sxs-lookup"><span data-stu-id="9a5ce-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="9a5ce-104">虛擬機器規模集可讓您 toodeploy 和管理一組完全相同，自動調整的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="9a5ce-105">您可以手動調整 hello 規模集中的 Vm hello 數目，或定義規則 tooautoscale 根據 CPU 使用量、 記憶體需求或網路流量。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="9a5ce-106">在本教學課程中，您將會在 Azure 部署虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="9a5ce-107">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a5ce-108">使用雲端 init toocreate 應用程式 tooscale</span><span class="sxs-lookup"><span data-stu-id="9a5ce-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="9a5ce-109">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="9a5ce-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9a5ce-110">增加或減少 hello 規模集中的執行個體數目</span><span class="sxs-lookup"><span data-stu-id="9a5ce-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="9a5ce-111">檢視擴展集執行個體的連線資訊</span><span class="sxs-lookup"><span data-stu-id="9a5ce-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="9a5ce-112">在擴展集內使用資料磁碟</span><span class="sxs-lookup"><span data-stu-id="9a5ce-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9a5ce-113">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9a5ce-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9a5ce-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="9a5ce-116">擴展集概觀</span><span class="sxs-lookup"><span data-stu-id="9a5ce-116">Scale Set overview</span></span>
<span data-ttu-id="9a5ce-117">虛擬機器規模集可讓您 toodeploy 和管理一組完全相同，自動調整的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="9a5ce-118">小數位數設定使用 hello 相同元件因為您了解有關在 hello 上一個教學課程中太[建立高可用性 Vm](tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="9a5ce-119">擴展集中的 VM 會建立於可用性設定組中並分散於邏輯容錯網域和更新網域。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="9a5ce-120">VM 會視需要建立於擴展集中。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="9a5ce-121">您可以定義自動調整規模規則 toocontrol 如何及何時加入或移除從 hello 擴展集 Vm。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="9a5ce-122">您可以根據計量 (例如 CPU 負載、記憶體使用量或網路流量) 觸發這些規則。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="9a5ce-123">小數位數設定總 too1，000 Vm，當您使用 Azure 平台映像的支援。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="9a5ce-124">對於生產工作負載，您可能希望太[建立自訂的 VM 映像](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="9a5ce-125">您可以建立啟動 too100 Vm 擴展集時使用的自訂映像內。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="9a5ce-126">建立應用程式 tooscale</span><span class="sxs-lookup"><span data-stu-id="9a5ce-126">Create an app tooscale</span></span>
<span data-ttu-id="9a5ce-127">用於實際執行環境，您可能希望太[建立自訂的 VM 映像](tutorial-custom-images.md)，其中包含您的應用程式安裝和設定。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="9a5ce-128">本教學課程，可讓自訂的 hello 第一個開機 tooquickly 上的 Vm，請參閱在動作中設定的標尺。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="9a5ce-129">在先前的教學課程中，您學會[如何 toocustomize Linux 虛擬機器第一次開機](tutorial-automate-vm-deployment.md)與雲端 init。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="9a5ce-130">您可以使用 hello 相同的雲端 init 組態檔案 tooinstall NGINX 並執行簡單的 ' Hello World' Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="9a5ce-131">您目前的殼層中建立名為*雲端 init.txt*和 hello 貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="9a5ce-132">例如，在 hello 雲端 Shell 不在您本機電腦上建立 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="9a5ce-133">輸入`sensible-editor cloud-init.txt`toocreate hello 檔案，並查看一份可用的編輯器。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="9a5ce-134">請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="9a5ce-135">建立擴展集</span><span class="sxs-lookup"><span data-stu-id="9a5ce-135">Create a scale set</span></span>
<span data-ttu-id="9a5ce-136">請先使用 [az group create](/cli/azure/group#create) 建立資源群組，才可以建立擴展集。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9a5ce-137">hello 下列範例會建立名為的資源群組*myResourceGroupScaleSet*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="9a5ce-138">現在使用 [az vmss create](/cli/azure/vmss#create) 建立虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="9a5ce-139">hello 下列範例會建立名為小數位數*myScaleSet*會使用 hello 雲端 init 檔案 toocustomize hello VM，並產生 SSH 金鑰，如果它們尚不存在：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="9a5ce-140">它會採用幾分鐘的時間 toocreate 並設定所有 hello 小數位數設定的資源和 Vm。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="9a5ce-141">有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="9a5ce-142">它可能是另一個數分鐘才能存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="9a5ce-143">允許 Web 流量</span><span class="sxs-lookup"><span data-stu-id="9a5ce-143">Allow web traffic</span></span>
<span data-ttu-id="9a5ce-144">Hello 虛擬機器規模集的過程中自動建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="9a5ce-145">hello 負載平衡器會將流量分散到一組定義的 Vm 使用負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="9a5ce-146">您可以進一步了解負載平衡器的概念和 hello 下一個教學課程中的組態[tooload 如何平衡在 Azure 虛擬機器](tutorial-load-balancer.md)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="9a5ce-147">tooallow 流量 tooreach hello web 應用程式，建立與規則[az 網路 lb 規則建立](/cli/azure/network/lb/rule#create)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="9a5ce-148">hello 下列範例會建立名為的規則*myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="9a5ce-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="9a5ce-149">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="9a5ce-149">Test your app</span></span>
<span data-ttu-id="9a5ce-150">toosee hello web 上的 Node.js 應用程式取得您的負載平衡器的 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="9a5ce-151">hello 下列範例會取得 IP 位址 hello *myScaleSetLBPublicIP*建立 hello 規模集的一部分：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="9a5ce-152">Tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="9a5ce-153">會顯示 hello 應用程式，包括 hello 的 hello VM 該 hello 負載平衡器分散流量的主機名稱：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![執行 Node.js 應用程式](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="9a5ce-155">在動作中設定 toosee hello 標尺，您可以強制重新整理 web 瀏覽器 toosee hello 負載平衡器會將流量分散到所有的 hello Vm 執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="9a5ce-156">管理工作</span><span class="sxs-lookup"><span data-stu-id="9a5ce-156">Management tasks</span></span>
<span data-ttu-id="9a5ce-157">整個 hello 規模集的 hello 生命週期，您可能需要 toorun 一或多個管理工作。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="9a5ce-158">此外，您可能想將不同的生命週期工作自動化的 toocreate 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="9a5ce-159">hello Azure CLI 2.0 提供快速的方式 toodo 這些工作。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="9a5ce-160">以下是一些常見工作。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="9a5ce-161">檢視擴展集中的 VM</span><span class="sxs-lookup"><span data-stu-id="9a5ce-161">View VMs in a scale set</span></span>
<span data-ttu-id="9a5ce-162">tooview 一份您的標尺中執行的 Vm 設定，請使用[az vmss 清單執行個體](/cli/azure/vmss#list-instances)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="9a5ce-163">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="9a5ce-164">增加或減少 VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="9a5ce-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="9a5ce-165">執行個體 toosee hello 數目您目前有小數位數中設定，請使用[az vmss 顯示](/cli/azure/vmss#show)及查詢上*sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="9a5ce-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="9a5ce-166">您可以再以手動方式增加或減少 hello 擴展集內的虛擬機器的 hello 數目[az vmss 標尺](/cli/azure/vmss#scale)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="9a5ce-167">hello 下列範例會設定 hello Vm 數目在您設定過的標尺*5*:</span><span class="sxs-lookup"><span data-stu-id="9a5ce-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="9a5ce-168">自動調整規模規則可讓您定義在例如 CPU 使用率或網路流量的回應 toodemand tooscale 向上或向下 hello Vm 數目在您的標尺的設定方式。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="9a5ce-169">目前，無法在 Azure CLI 2.0 中設定這些規則。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="9a5ce-170">使用 hello [Azure 入口網站](https://portal.azure.com)tooconfigure 自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="9a5ce-171">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="9a5ce-171">Get connection info</span></span>
<span data-ttu-id="9a5ce-172">tooobtain 連接資訊 hello Vm 規模集中，使用[az vmss 清單執行個體的連接-資訊](/cli/azure/vmss#list-instance-connection-info)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="9a5ce-173">此命令會輸出每個 VM，可讓您透過 SSH tooconnect hello 公用 IP 位址和連接埠：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="9a5ce-174">使用資料磁碟搭配擴展集</span><span class="sxs-lookup"><span data-stu-id="9a5ce-174">Use data disks with scale sets</span></span>
<span data-ttu-id="9a5ce-175">您可以建立及使用資料磁碟搭配擴展集。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="9a5ce-176">在先前的教學課程中，您學會如何太[管理 Azure 磁碟](tutorial-manage-disks.md)外框 hello 最佳作法和資料磁碟，而不是 hello OS 磁碟上建置應用程式的效能改進。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="9a5ce-177">使用資料磁碟建立擴展集</span><span class="sxs-lookup"><span data-stu-id="9a5ce-177">Create scale set with data disks</span></span>
<span data-ttu-id="9a5ce-178">toocreate 設定小數位數，並連接資料磁碟加入 hello`--data-disk-sizes-gb`參數 toohello [az vmss 建立](/cli/azure/vmss#create)命令。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="9a5ce-179">hello 下列範例會建立與設定的比例*50*Gb 資料磁碟附加 tooeach 執行個體：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

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

<span data-ttu-id="9a5ce-180">當執行個體從擴展集移除時，所有連結的資料磁碟也會一併移除。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="9a5ce-181">新增資料磁碟</span><span class="sxs-lookup"><span data-stu-id="9a5ce-181">Add data disks</span></span>
<span data-ttu-id="9a5ce-182">tooadd 在您的標尺資料磁碟 tooinstances 設定，請使用[az vmss 磁碟附加](/cli/azure/vmss/disk#attach)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="9a5ce-183">hello 下列範例會將*50*Gb 磁碟 tooeach 執行個體：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="9a5ce-184">卸離資料磁碟</span><span class="sxs-lookup"><span data-stu-id="9a5ce-184">Detach data disks</span></span>
<span data-ttu-id="9a5ce-185">tooremove 在您的標尺資料磁碟 tooinstances 設定，請使用[az vmss 磁碟卸離](/cli/azure/vmss/disk#detach)。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="9a5ce-186">hello 下列範例會移除 hello 資料磁碟的 LUN *2*從每個執行個體：</span><span class="sxs-lookup"><span data-stu-id="9a5ce-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="9a5ce-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a5ce-187">Next steps</span></span>
<span data-ttu-id="9a5ce-188">在本教學課程中，您已建立虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="9a5ce-189">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="9a5ce-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a5ce-190">使用雲端 init toocreate 應用程式 tooscale</span><span class="sxs-lookup"><span data-stu-id="9a5ce-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="9a5ce-191">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="9a5ce-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9a5ce-192">增加或減少 hello 規模集中的執行個體數目</span><span class="sxs-lookup"><span data-stu-id="9a5ce-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="9a5ce-193">檢視擴展集執行個體的連線資訊</span><span class="sxs-lookup"><span data-stu-id="9a5ce-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="9a5ce-194">在擴展集內使用資料磁碟</span><span class="sxs-lookup"><span data-stu-id="9a5ce-194">Use data disks in a scale set</span></span>

<span data-ttu-id="9a5ce-195">前進 toohello 下一個教學課程 toolearn 有關負載平衡的虛擬機器概念的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9a5ce-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a5ce-196">平衡虛擬機器的負載</span><span class="sxs-lookup"><span data-stu-id="9a5ce-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)