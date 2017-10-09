---
title: "aaaHow tooload 平衡在 Azure 中的 Linux 虛擬機器 |Microsoft 文件"
description: "了解如何 toouse hello Azure 跨越三個 Linux Vm 的負載平衡器 toocreate 高度可用且安全的應用程式"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>如何 tooload 會平衡 Azure toocreate 中 Linux 虛擬機器的高可用性的應用程式
負載平衡會將傳入要求分散到多部虛擬機器，藉此提供高可用性。 在本教學課程中，您會了解 hello 的不同元件 hello Azure 負載平衡器會將流量，以及提供高可用性。 您會了解如何：

> [!div class="checklist"]
> * 建立 Azure Load Balancer
> * 建立負載平衡器健全狀況探查
> * 建立負載平衡器流量規則
> * 使用雲端 init toocreate 基本 Node.js 應用程式
> * 建立虛擬機器，並附加 tooa 負載平衡器
> * 檢視作用中的負載平衡器
> * 新增和移除虛擬機器的負載平衡器


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="azure-load-balancer-overview"></a>Azure Load Balancer 概觀
Azure Load Balancer 是 Layer-4 (TCP、UDP) 負載平衡器，可將連入流量分散於狀況良好的 VM 來提供高可用性。 負載平衡器健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。

您可定義含有一或多個公用 IP 位址的前端 IP 組態。 此前端 IP 組態可讓您的負載平衡器和應用程式 toobe 存取透過 hello 網際網路。 

虛擬機器連接 tooa 負載平衡器使用他們的虛擬網路介面卡 (NIC)。 toodistribute 流量 toohello Vm 後, 端位址集區包含 hello hello 虛擬 (Nic) 連線的 toohello 負載平衡器的 IP 位址。

toocontrol hello 流量的流量，您會定義特定連接埠和通訊協定對應 tooyour Vm 的負載平衡器規則。

如果您遵循 hello 上一個教學課程太[建立虛擬機器規模集](tutorial-create-vmss.md)，為您建立負載平衡器。 所有這些元件已設定為您 hello 規模集的一部分。


## <a name="create-azure-load-balancer"></a>建立 Azure Load Balancer
本節將詳細說明如何建立及設定 hello 負載平衡器的每個元件。 請先使用 [az group create](/cli/azure/group#create) 建立資源群組，才可建立負載平衡器。 hello 下列範例會建立名為的資源群組*myResourceGroupLoadBalancer*在 hello *eastus*位置：

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>建立公用 IP 位址
tooaccess 上的應用程式 hello 網際網路，您就需要公用 IP 位址 hello 負載平衡器。 使用 [az network public-ip create](/cli/azure/network/public-ip#create) 建立公用 IP 位址。 hello 下列範例會建立名為的公用 IP 位址*myPublicIP*在 hello *myResourceGroupLoadBalancer*資源群組：

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>建立負載平衡器
使用 [az network lb create](/cli/azure/network/lb#create) 建立負載平衡器。 hello 下列範例會建立名為負載平衡器*myLoadBalancer*和指派 hello *myPublicIP*位址 toohello 前端 IP 組態：

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>建立健康狀態探查
tooallow hello 負載平衡器 toomonitor hello 狀態的應用程式，您可以使用健全狀況探查。 hello 健全狀況探查以動態方式加入或移除 hello 負載平衡器輪替根據其回應 toohealth 檢查 Vm。 根據預設，VM 會移除從 15 秒的間隔的兩個連續多次失敗後的 hello 負載平衡器發佈。 您可根據通訊協定或您應用程式的特定健康狀態檢查頁面，建立健康狀態探查。 

hello 下列範例會建立 TCP 探查。 您也可以建立自訂 HTTP 探查，以進行更精細的健康狀態檢查。 時使用自訂的 HTTP 探查，您必須建立 hello 健康情況檢查 頁面上，例如*healthcheck.js*。 必須傳回 hello 探查**HTTP 200 「 確定**回應 hello 負載平衡器 tookeep hello 中主機的旋轉。

您使用 toocreate TCP 健全狀況探查， [az 網路 lb 探查建立](/cli/azure/network/lb/probe#create)。 hello 下列範例會建立名為健全狀況探查*myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>建立負載平衡器規則
負載平衡器規則是使用的 toodefine 流量的分散式的 toohello Vm 的方式。 您定義 hello 連入流量和 hello 後端 IP 集區 tooreceive hello 流量，以及 hello 必要的來源和目的地連接埠 hello 前端 IP 組態。 toomake 確定只有狀況良好的 Vm 接收流量，您也定義 hello 健全狀況探查 toouse。

使用 [az network lb rule create](/cli/azure/network/lb/rule#create) 建立負載平衡器規則。 hello 下列範例會建立名為的規則*myLoadBalancerRule*，使用 hello *myHealthProbe*健全狀況探查和連接埠上的餘額流量*80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>設定虛擬網路
您將一些 Vm 部署，並可以測試您平衡器之前，先建立 hello 支援的虛擬網路資源。 如需有關虛擬網路的詳細資訊，請參閱 hello[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。

### <a name="create-network-resources"></a>建立網路資源
使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。 hello 下列範例會建立虛擬網路，名為*myVnet*與子網路，名為*mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

您使用 tooadd 網路安全性群組， [az 網路 nsg 建立](/cli/azure/network/nsg#create)。 hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 建立網路安全性群組規則。 hello 下列範例會建立網路安全性群組規則命名為*myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

使用 [az network nic create](/cli/azure/network/nic#create) 建立虛擬 NIC。 hello 下列範例會建立三個虛擬 Nic。 （每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）。 您可以隨時建立其他虛擬 Nic 和 Vm，並將它們加入 toohello 負載平衡器：

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>建立虛擬機器

### <a name="create-cloud-init-config"></a>建立 Cloud-init 組態
在上一個教學課程中[如何 toocustomize Linux 虛擬機器第一次開機](tutorial-automate-vm-deployment.md)，您學到如何使用雲端 init tooautomate VM 自訂。 您可以使用 hello 相同的雲端 init 組態檔案 tooinstall NGINX 並執行簡單的 ' Hello World' Node.js 應用程式。

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

### <a name="create-virtual-machines"></a>建立虛擬機器
tooimprove hello 高可用性的應用程式會將您的 Vm 放在可用性設定組。 如需可用性設定組的詳細資訊，請參閱先前的 hello[如何 toocreate 高可用性虛擬機器](tutorial-availability-sets.md)教學課程。

使用 [az vm availability-set create](/cli/azure/vm/availability-set#create) 建立可用性設定組。 hello 下列範例會建立可用性設定組具名*myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

現在您可以建立與 hello Vm [az vm 建立](/cli/azure/vm#create)。 hello 下列範例會建立三個 Vm，如果它們尚不存在，會產生 SSH 金鑰：

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。 hello`--no-wait`參數不會等到所有 hello 工作 toocomplete。 它可能是另一個數分鐘才能存取 hello 應用程式。 hello 負載平衡器健全狀況探查會自動偵測 hello 應用程式在每個 VM 上執行。 一旦 hello 應用程式正在執行，hello 負載平衡器規則會啟動 toodistribute 流量。


## <a name="test-load-balancer"></a>測試負載平衡器
取得您的負載平衡器的 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show)。 hello 下列範例會取得 IP 位址 hello *myPublicIP*稍早建立：

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

然後，您就可以 tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。 請記住，-花幾分鐘的時間 hello hello Vm toobe 準備 hello 負載平衡器開始 toodistribute 流量 toothem 之前。 hello 應用程式會顯示，包括 hello hello VM 主機名稱的 hello 負載平衡器分散流量 tooas hello 下列範例中：

![執行 Node.js 應用程式](./media/tutorial-load-balancer/running-nodejs-app.png)

toosee hello 負載平衡器會將流量分散到執行您的應用程式的所有三個 Vm，您可以強制重新整理您的 web 瀏覽器。


## <a name="add-and-remove-vms"></a>新增和移除 VM
您可能需要 tooperform hello 執行您的應用程式，例如安裝作業系統更新的 Vm 上的維護。 toodeal 使用增加的流量 tooyour 應用程式，您可能需要 tooadd 其他 Vm。 這個區段會顯示如何 tooremove 或加入 VM 從 hello 負載平衡器。

### <a name="remove-a-vm-from-hello-load-balancer"></a>從 hello 負載平衡器移除 VM
您可以從 hello 與後端位址集區移除 VM [az 網路 nic ip 設定的位址集區移除](/cli/azure/network/nic/ip-config/address-pool#remove)。 下列範例中移除的 hello hello 虛擬 NIC，供**myVM2**從*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

toosee hello 負載平衡器會將流量分散到 hello 剩餘的兩個 Vm 執行您的應用程式您可以強制重新整理您的 web 瀏覽器。 您現在可以在 hello VM，如安裝作業系統更新，或執行 VM 重新啟動電腦上執行維護。

### <a name="add-a-vm-toohello-load-balancer"></a>新增 VM toohello 負載平衡器
之後執行 VM 維護，或者如果您需要 tooexpand 容量時，您可以加入 VM toohello 後端位址集區與[az 網路 nic ip 設定的位址集區新增](/cli/azure/network/nic/ip-config/address-pool#add)。 hello 下列範例會將 hello 虛擬 NIC，供**myVM2**太*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>後續步驟
在本教學課程中，您可以建立負載平衡器，並附加 Vm tooit。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Azure Load Balancer
> * 建立負載平衡器健全狀況探查
> * 建立負載平衡器流量規則
> * 使用雲端 init toocreate 基本 Node.js 應用程式
> * 建立虛擬機器，並附加 tooa 負載平衡器
> * 檢視作用中的負載平衡器
> * 新增和移除虛擬機器的負載平衡器

前進 toohello 下一個教學課程 toolearn 有關 Azure 虛擬網路元件的詳細資訊。

> [!div class="nextstepaction"]
> [管理 VM 和虛擬網路](tutorial-virtual-network.md)
