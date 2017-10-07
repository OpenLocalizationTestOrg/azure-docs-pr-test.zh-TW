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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>在 Linux 上建立虛擬機器擴展集及部署高可用性應用程式
虛擬機器規模集可讓您 toodeploy 和管理一組完全相同，自動調整的虛擬機器。 您可以手動調整 hello 規模集中的 Vm hello 數目，或定義規則 tooautoscale 根據 CPU 使用量、 記憶體需求或網路流量。 在本教學課程中，您將會在 Azure 部署虛擬機器擴展集。 您會了解如何：

> [!div class="checklist"]
> * 使用雲端 init toocreate 應用程式 tooscale
> * 建立虛擬機器擴展集
> * 增加或減少 hello 規模集中的執行個體數目
> * 檢視擴展集執行個體的連線資訊
> * 在擴展集內使用資料磁碟


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="scale-set-overview"></a>擴展集概觀
虛擬機器規模集可讓您 toodeploy 和管理一組完全相同，自動調整的虛擬機器。 小數位數設定使用 hello 相同元件因為您了解有關在 hello 上一個教學課程中太[建立高可用性 Vm](tutorial-availability-sets.md)。 擴展集中的 VM 會建立於可用性設定組中並分散於邏輯容錯網域和更新網域。

VM 會視需要建立於擴展集中。 您可以定義自動調整規模規則 toocontrol 如何及何時加入或移除從 hello 擴展集 Vm。 您可以根據計量 (例如 CPU 負載、記憶體使用量或網路流量) 觸發這些規則。

小數位數設定總 too1，000 Vm，當您使用 Azure 平台映像的支援。 對於生產工作負載，您可能希望太[建立自訂的 VM 映像](tutorial-custom-images.md)。 您可以建立啟動 too100 Vm 擴展集時使用的自訂映像內。


## <a name="create-an-app-tooscale"></a>建立應用程式 tooscale
用於實際執行環境，您可能希望太[建立自訂的 VM 映像](tutorial-custom-images.md)，其中包含您的應用程式安裝和設定。 本教學課程，可讓自訂的 hello 第一個開機 tooquickly 上的 Vm，請參閱在動作中設定的標尺。

在先前的教學課程中，您學會[如何 toocustomize Linux 虛擬機器第一次開機](tutorial-automate-vm-deployment.md)與雲端 init。 您可以使用 hello 相同的雲端 init 組態檔案 tooinstall NGINX 並執行簡單的 ' Hello World' Node.js 應用程式。 

您目前的殼層中建立名為*雲端 init.txt*和 hello 貼上下列組態。 例如，在 hello 雲端 Shell 不在您本機電腦上建立 hello 檔案。 輸入`sensible-editor cloud-init.txt`toocreate hello 檔案，並查看一份可用的編輯器。 請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：

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


## <a name="create-a-scale-set"></a>建立擴展集
請先使用 [az group create](/cli/azure/group#create) 建立資源群組，才可以建立擴展集。 hello 下列範例會建立名為的資源群組*myResourceGroupScaleSet*在 hello *eastus*位置：

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

現在使用 [az vmss create](/cli/azure/vmss#create) 建立虛擬機器擴展集。 hello 下列範例會建立名為小數位數*myScaleSet*會使用 hello 雲端 init 檔案 toocustomize hello VM，並產生 SSH 金鑰，如果它們尚不存在：

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

它會採用幾分鐘的時間 toocreate 並設定所有 hello 小數位數設定的資源和 Vm。 有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。 它可能是另一個數分鐘才能存取 hello 應用程式。


## <a name="allow-web-traffic"></a>允許 Web 流量
Hello 虛擬機器規模集的過程中自動建立負載平衡器。 hello 負載平衡器會將流量分散到一組定義的 Vm 使用負載平衡器規則。 您可以進一步了解負載平衡器的概念和 hello 下一個教學課程中的組態[tooload 如何平衡在 Azure 虛擬機器](tutorial-load-balancer.md)。

tooallow 流量 tooreach hello web 應用程式，建立與規則[az 網路 lb 規則建立](/cli/azure/network/lb/rule#create)。 hello 下列範例會建立名為的規則*myLoadBalancerRuleWeb*:

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

## <a name="test-your-app"></a>測試應用程式
toosee hello web 上的 Node.js 應用程式取得您的負載平衡器的 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show)。 hello 下列範例會取得 IP 位址 hello *myScaleSetLBPublicIP*建立 hello 規模集的一部分：

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。 會顯示 hello 應用程式，包括 hello 的 hello VM 該 hello 負載平衡器分散流量的主機名稱：

![執行 Node.js 應用程式](./media/tutorial-create-vmss/running-nodejs-app.png)

在動作中設定 toosee hello 標尺，您可以強制重新整理 web 瀏覽器 toosee hello 負載平衡器會將流量分散到所有的 hello Vm 執行您的應用程式。


## <a name="management-tasks"></a>管理工作
整個 hello 規模集的 hello 生命週期，您可能需要 toorun 一或多個管理工作。 此外，您可能想將不同的生命週期工作自動化的 toocreate 指令碼。 hello Azure CLI 2.0 提供快速的方式 toodo 這些工作。 以下是一些常見工作。

### <a name="view-vms-in-a-scale-set"></a>檢視擴展集中的 VM
tooview 一份您的標尺中執行的 Vm 設定，請使用[az vmss 清單執行個體](/cli/azure/vmss#list-instances)，如下所示：

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

hello 輸出是 toohello 類似下列範例程式碼：

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>增加或減少 VM 執行個體
執行個體 toosee hello 數目您目前有小數位數中設定，請使用[az vmss 顯示](/cli/azure/vmss#show)及查詢上*sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

您可以再以手動方式增加或減少 hello 擴展集內的虛擬機器的 hello 數目[az vmss 標尺](/cli/azure/vmss#scale)。 hello 下列範例會設定 hello Vm 數目在您設定過的標尺*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

自動調整規模規則可讓您定義在例如 CPU 使用率或網路流量的回應 toodemand tooscale 向上或向下 hello Vm 數目在您的標尺的設定方式。 目前，無法在 Azure CLI 2.0 中設定這些規則。 使用 hello [Azure 入口網站](https://portal.azure.com)tooconfigure 自動調整規模。

### <a name="get-connection-info"></a>取得連線資訊
tooobtain 連接資訊 hello Vm 規模集中，使用[az vmss 清單執行個體的連接-資訊](/cli/azure/vmss#list-instance-connection-info)。 此命令會輸出每個 VM，可讓您透過 SSH tooconnect hello 公用 IP 位址和連接埠：

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>使用資料磁碟搭配擴展集
您可以建立及使用資料磁碟搭配擴展集。 在先前的教學課程中，您學會如何太[管理 Azure 磁碟](tutorial-manage-disks.md)外框 hello 最佳作法和資料磁碟，而不是 hello OS 磁碟上建置應用程式的效能改進。

### <a name="create-scale-set-with-data-disks"></a>使用資料磁碟建立擴展集
toocreate 設定小數位數，並連接資料磁碟加入 hello`--data-disk-sizes-gb`參數 toohello [az vmss 建立](/cli/azure/vmss#create)命令。 hello 下列範例會建立與設定的比例*50*Gb 資料磁碟附加 tooeach 執行個體：

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

當執行個體從擴展集移除時，所有連結的資料磁碟也會一併移除。

### <a name="add-data-disks"></a>新增資料磁碟
tooadd 在您的標尺資料磁碟 tooinstances 設定，請使用[az vmss 磁碟附加](/cli/azure/vmss/disk#attach)。 hello 下列範例會將*50*Gb 磁碟 tooeach 執行個體：

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>卸離資料磁碟
tooremove 在您的標尺資料磁碟 tooinstances 設定，請使用[az vmss 磁碟卸離](/cli/azure/vmss/disk#detach)。 hello 下列範例會移除 hello 資料磁碟的 LUN *2*從每個執行個體：

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>後續步驟
在本教學課程中，您已建立虛擬機器擴展集。 您已了解如何︰

> [!div class="checklist"]
> * 使用雲端 init toocreate 應用程式 tooscale
> * 建立虛擬機器擴展集
> * 增加或減少 hello 規模集中的執行個體數目
> * 檢視擴展集執行個體的連線資訊
> * 在擴展集內使用資料磁碟

前進 toohello 下一個教學課程 toolearn 有關負載平衡的虛擬機器概念的詳細資訊。

> [!div class="nextstepaction"]
> [平衡虛擬機器的負載](tutorial-load-balancer.md)