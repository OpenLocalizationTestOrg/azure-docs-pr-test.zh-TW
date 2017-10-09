---
title: "aaaAzure 虛擬網路和 Linux 虛擬機器 |Microsoft 文件"
description: "教學課程-使用 Azure CLI hello 管理 Azure 虛擬網路和 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>使用 Azure CLI hello 管理 Azure 虛擬網路和 Linux 虛擬機器

Azure 虛擬機器會使用 Azure 網路進行內部和外部的網路通訊。 本教學課程會逐步部署兩部虛擬機器 (VM)，並設定這兩部 VM 的 Azure 網路功能。 此教學課程中的 hello 範例假設 hello Vm 都裝載 web 應用程式與資料庫後端，但未在 hello 教學課程中部署應用程式。 在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 部署虛擬網路
> * 在虛擬網路中建立子網路
> * 附加虛擬機器 tooa 子網路
> * 管理虛擬機器的公用 IP 位址
> * 保護傳入的網際網路流量
> * 確保 VM tooVM 流量的安全


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="vm-networking-overview"></a>VM 網路概觀

Azure 虛擬網路啟用安全的網路連線的虛擬機器之間，hello 網際網路及其他 Azure 服務，例如 Azure SQL database。 虛擬網路會被分割成邏輯區段，稱為子網路。 子網路可用 toocontrol 網路流量，及做為安全性界限。 在部署 VM 時，它通常會包含在虛擬網路介面，也就是附加的 tooa 子網路。

## <a name="deploy-virtual-network"></a>部署虛擬網路

在本教學課程中，會建立一個具有兩個子網路的虛擬網路。 一個是裝載 Web 應用程式的前端子網路，一個是裝載資料庫伺服器的後端子網路。

建立虛擬網路前，請先使用 [az group create](/cli/azure/group#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myRGNetwork* hello eastus 位置中。

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>建立虛擬網路

我們 hello [az 網路 vnet 建立](/cli/azure/network/vnet#create)命令 toocreate 虛擬網路。 在此範例中，名為 hello 網路*mvVnet*和指定的位址首碼*10.0.0.0/16*。 也會建立名為 mySubnetFrontEnd 且首碼為 10.0.1.0/24 的子網路。 稍後在本教學課程前端 VM 是已連線的 toothis 子網路。 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>建立子網路

新的子網路加入 toohello 虛擬網路使用 hello [az vnet 子網路建立](/cli/azure/network/vnet/subnet#create)命令。 在此範例中，名為 hello 子網路*mySubnetBackEnd*和指定的位址首碼*10.0.2.0/24*。 所有的後端服務都會使用此子網路。

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

此時，已建立一個網路並分割成兩個子網路，一個用於前端的服務，另一個用於後端服務。 在 hello 下一步 區段中，虛擬機器建立和連線 toothese 子網路。

## <a name="understand-public-ip-address"></a>認識公用 IP 位址

公用 IP 位址允許存取的 Azure 資源 toobe hello 網際網路。 在本節中的 hello 教學課程中，VM 會建立的 toodemonstrate toowork 與公用 IP 位址的方式。

### <a name="allocation-method"></a>配置方法

公用 IP 位址可以動態或靜態配置。 預設是以動態方式配置公用 IP 位址。 VM 解除配置時，就會釋放動態 IP 位址。 這個行為會包含 VM 解除配置的任何作業期間造成 hello IP 位址 toochange。

hello 配置方法可以設定 toostatic，後者可確保 hello IP 位址的保留期間，指派給 tooa VM，即使解除配置的狀態。 使用靜態配置的 IP 位址，無法指定本身 hello IP 位址。 而是從可用位址集區配置一個給它。

### <a name="dynamic-allocation"></a>動態配置

Hello 與建立 VM 時[az vm 建立](/cli/azure/vm#create)命令時，是動態的 hello 預設公用 IP 位址配置方法。 在下列範例的 hello，VM 會建立具有動態的 IP 位址。 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>靜態配置

當建立虛擬機器使用 hello [az vm 建立](/cli/azure/vm#create)命令，包括 hello`--public-ip-address-allocation static`引數 tooassign 靜態公用 IP 位址。 這項作業不會示範在本教學課程中，不過 hello 下一節的動態配置的 IP 位址已變更的 tooa 靜態配置的位址。 

### <a name="change-allocation-method"></a>變更配置方法

可以使用 hello 變更 hello IP 位址配置方法[az 網路公用 ip 更新](/cli/azure/network/public-ip#update)命令。 在此範例中，hello 的 hello 變更前端 VM 的 IP 位址配置方法 toostatic。

首先，取消配置 hello VM。

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

使用 hello [az 網路公用 ip 更新](/cli/azure/network/public-ip#update)命令 tooupdate hello 配置方法。 在此情況下，hello`--allocation-method`太設定*靜態*。

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

啟動 hello VM。

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>無公用 IP 位址

通常，VM 不需要 toobe 可以透過 hello 網際網路。 toocreate VM 不含公用 IP 位址，使用 hello`--public-ip-address ""`引數以雙引號括住的空集合。 此組態稍後會在本教學課程中示範。

## <a name="secure-network-traffic"></a>保護網路流量

網路安全性群組 (NSG) 包含可允許或拒絕網路流量 tooresources 連接 tooAzure 虛擬網路 (VNet) 安全性規則的清單。 Nsg 可以是相關聯的 toosubnets 或個別的網路介面。 NSG 相關聯的網路介面時，它將適用於僅 hello 相關聯的 VM。 當 NSG 相關聯的 tooa 子網路，hello 規則適用於 tooall 資源連線的 toohello 子網路。 

### <a name="network-security-group-rules"></a>網路安全性群組規則

NSG 規則定義允許或拒絕流量的網路連接埠。 hello 規則可以包含來源和目的地 IP 位址範圍，以便控制特定的系統或子網路之間流量。 NSG 規則也包含優先順序 (介於 1 和 4096)。 會評估 hello 依優先順序的規則。 優先順序 100 的規則會比優先順序 200 的規則優先評估。

所有 NSG 都包含一組預設規則。 無法刪除 hello 預設規則，但它們指派 hello 最低優先權，因為它們會覆寫由您所建立的 hello 規則。

- **虛擬網路** - 虛擬網路中的流量起始和結束同時允許輸入和輸出方向。
- **網際網路** - 允許輸出流量，但會封鎖輸入流量。
- **負載平衡器**-允許 Azure 負載平衡器 tooprobe hello 和健康狀態的 Vm 角色執行個體。 如果您不使用負載平衡的集合，則可以覆寫此規則。

### <a name="create-network-security-groups"></a>建立網路安全性群組

網路安全性群組可以在建立 hello 相同時間當作 VM 使用 hello [az vm 建立](/cli/azure/vm#create)命令。 這樣一來，當 hello NSG 關聯的 hello Vm 網路介面，NSG 規則是連接埠上的自動建立 tooallow 流量*22*從任何來源。 稍早在本教學課程中，前端 NSG 已使用自動建立的 hello hello 前端 VM。 也會自動建立連接埠 22 的 NSG 規則。 

在某些情況下，可能會很有幫助 toopre-建立 NSG，例如當應該不會建立預設 SSH 規則，或當 hello NSG 應該附加的 tooa 子網路。 

使用 hello [az 網路 nsg 建立](/cli/azure/network/nsg#create)命令 toocreate 網路安全性群組。

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

而不是建立 hello NSG tooa 網路介面的關聯，它是子網路相關聯。 在此組態中，任何附加的 toohello 子網路的 VM 會繼承 hello NSG 規則。

更新 hello 現有子網路，名為*mySubnetBackEnd*與 hello 新的 NSG。

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

現在建立虛擬機器，也就是附加的 toohello *mySubnetBackEnd*。 請注意該 hello`--nsg`引數的值為空的雙引號。 NSG 不需要建立以 hello VM toobe。 hello VM 是附加的 toohello 後端子，是使用預先建立後端 NSG hello 保護。 此 NSG 會套用 toohello VM。 另外而且請注意這裡該 hello`--public-ip-address`引數的值為空的雙引號。 此組態會建立無公用 IP 位址的 VM。 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>保護傳入的流量

Hello 前端 VM 建立時，NSG 規則 tooallow 連入流量上建立通訊埠 22。 此規則可讓 SSH 連線 toohello VM。 在此範例中，應該也允許連接埠 80 上的流量。 此設定可讓 web 應用程式 toobe hello VM 上的存取。

使用 hello [az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)命令 toocreate 規則; 連接埠*80*。

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

hello 前端 VM 現在只有為連接埠上*22*和連接埠*80*。 其他所有的連入流量會在網路安全性群組 hello 遭到封鎖。 它可能會很有幫助 toovisualize hello NSG 規則設定。 傳回 hello NSG 規則設定，以 hello [az 網路規則清單](/cli/azure/network/nsg/rule#list)命令。 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

輸出：

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>確保 VM tooVM 流量的安全

網路安全性群組規則也可以套用在 VM 之間。 針對此範例中，前端 VM 需要 toocommunicate 與 hello hello 連接埠上的後端 VM *22*和*3306*。 此設定可讓來自 SSH 連線 hello 前端 VM，而且也允許 hello 前端 VM toocommunicate 與後端 MySQL 資料庫上的 應用程式。 Hello 前端和後端的虛擬機器之間，應予封鎖所有其他流量。

使用 hello [az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)命令 toocreate 規則; 連接埠 22。 請注意該 hello`--source-address-prefix`引數指定的值*10.0.1.0/24*。 此組態可確保只有 hello 前端子網路的流量，允許透過 hello NSG。

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

現在新增連接埠 3306 上 MySQL 流量的規則。

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

最後，因為 Nsg 預設規則允許所有流量 hello 的 Vm 之間相同的 VNet，規則可以建立 hello 後端 Nsg tooblock 所有流量。 在這裡看到該 hello`--priority`給定的值*300*，這是較低兩者 hello NSG 和 MySQL 的規則。 此組態可確保透過 hello NSG，仍允許 SSH 和 MySQL 的流量。

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

hello 後端 VM 現在只有為連接埠上*22*和連接埠*3306*從 hello 前端子網路。 其他所有的連入流量會在網路安全性群組 hello 遭到封鎖。 它可能會很有幫助 toovisualize hello NSG 規則設定。 傳回 hello NSG 規則設定，以 hello [az 網路規則清單](/cli/azure/network/nsg/rule#list)命令。 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

輸出：

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以建立並保護做為相關的 toovirtual 機器的 Azure 網路。 您已了解如何︰

> [!div class="checklist"]
> * 部署虛擬網路
> * 在虛擬網路中建立子網路
> * 附加虛擬機器 tooa 子網路
> * 管理虛擬機器的公用 IP 位址
> * 保護傳入的網際網路流量
> * 確保 VM tooVM 流量的安全

前進 toohello 下一個教學課程的 toolearn 有關使用 Azure 備份的虛擬機器上的資料。 

> [!div class="nextstepaction"]
> [備份 Azure 中的 Linux 虛擬機器](./tutorial-backup-vms.md)
