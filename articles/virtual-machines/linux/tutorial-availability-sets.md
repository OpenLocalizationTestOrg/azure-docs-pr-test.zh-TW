---
title: "aaaAvailability 適用於 Linux Vm 在 Azure 中設定教學課程 |Microsoft 文件"
description: "適用於 Linux Vm 在 Azure 中，以了解 hello 可用性設定組。"
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>如何 toouse 可用性設定組


在本教學課程中，您將學習如何 tooincrease hello 可用性和可靠性的虛擬機器上使用此功能的 Azure 方案的呼叫可用性設定組。 可用性設定組，請確定您在 Azure 上部署的 Vm 會分散到多個隔離的硬體叢集該 hello。 如此一來，可確保如果在 Azure 中的硬體或軟體失敗，會影響您的 Vm 子組可用且正常運作，從您的客戶使用它的 hello 觀點來看，將會保留您的整體解決方案。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立可用性設定組
> * 在可用性設定組中建立 VM
> * 檢查可用的 VM 大小


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="availability-set-overview"></a>可用性設定組概觀

可用性設定組中您在其中放置 hello VM 資源時，都是彼此隔離的 Azure 資料中心內部署的 Azure tooensure 是一種邏輯群組功能，您可以使用。 Azure 可確保該 hello 您放置多個實體伺服器上執行可用性設定組內的 Vm、 計算機架、 儲存體單位及網路交換器。 這樣可以確保在 hello 事件中的硬體或 Azure 軟體失敗，會影響 Vm 的子集，整體應用程式將保持為設定並繼續 toobe 可用 tooyour 客戶。 使用可用性設定組時，重要的功能 tooleverage 想 toobuild 可靠的雲端解決方案。

請想想典型的 VM 架構解決方案，在此解決方案中，您可能有 4 個前端 Web 伺服器，並使用 2 個後端 VM 來裝載資料庫。 有了 Azure，您會想 toodefine 兩個可用性設定組才能部署您的 Vm: hello"web"層和一個可用性設定 hello 「 資料庫 」 層的一個可用性設定組。 當您建立新的 VM，您可以接著指定 hello 可用性設定組參數 toohello az vm 建立命令，以及 Azure 會自動確保該 hello hello 可用中所建立的 Vm 組會隔離跨多個實體硬體資源。 這表示如果 hello 實體硬體上執行您的 Web 伺服器或資料庫伺服器 Vm 的其中一個發生問題，您知道該 hello 網頁伺服器及資料庫 Vm 的其他執行個體將會繼續執行正常因為它們是在不同硬體上。

當您想 toodeploy 可靠 VM 為基礎的解決方案在 Azure 中，您應該一律使用可用性設定組。


## <a name="create-an-availability-set"></a>建立可用性設定組

您可以使用 [az vm availability-set create](/cli/azure/vm/availability-set#create) 來建立可用性設定組。 在此範例中，我們設定兩個 hello 的更新和容錯網域數目在*2* hello 可用性名為*myAvailabilitySet*在 hello *myResourceGroupAvailability*資源群組。

建立資源群組。

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

可用性設定組可讓您 tooisolate 資源跨 「 故障網域 」 和 「 更新網域 」。 **容錯網域**代表以隔離方式集合在一起的伺服器、網路和儲存體資源。 在上述範例中的 hello，我們表示我們想要我們可用性設定組 toobe 我們 Vm 部署時，分散在至少兩個容錯網域。 我們也表示我們想要讓可用性設定組分散到兩個**更新網域**。  兩個更新網域確保 Azure 會執行軟體更新 VM 資源都會隔離，導致無法更新在 hello 我們 VM 執行的所有 hello 軟體相同的時間。

## <a name="configure-virtual-network"></a>設定虛擬網路
您將一些 Vm 部署，並可以測試您平衡器之前，先建立 hello 支援的虛擬網路資源。 如需有關虛擬網路的詳細資訊，請參閱 hello[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。

### <a name="create-network-resources"></a>建立網路資源
使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。 hello 下列範例會建立虛擬網路，名為*myVnet*與子網路，名為*mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
使用 [az network nic create](/cli/azure/network/nic#create) 建立虛擬 NIC。 hello 下列範例會建立三個虛擬 Nic。 （每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）。 您可以隨時建立其他虛擬 Nic 和 Vm，並將它們加入 toohello 負載平衡器：

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>建立位於可用性設定組內的 VM

Vm 必須確定正確分散 hello 硬體的 hello 可用性集 toomake 內建立。 您無法加入現有 VM tooan 可用性設定組建立之後。 

當您建立 VM 使用[az vm 建立](/cli/azure/vm#create)指定 hello 可用性設定組使用 hello`--availability-set`參數 toospecify hello 名稱 hello 可用性設定組。

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

現在，我們新建立的可用性設定組內有兩部虛擬機器。 因為它們是在 hello 相同可用性設定組，Azure 可確保該 hello Vm 及其所有資源 （包括資料磁碟） 會分散到隔離的實體硬體。 這樣的分佈方式有助於確保 VM 解決方案整體有更高的可用性。

當您新增 Vm 可能會遇到的一件事是特定的 VM 大小已不再可用 toouse 可用性集內。 如果不再有足夠的容量 tooadd 它同時保留 hello 隔離規則 hello 可用性設定組會強制執行，可能會發生此問題。 您可以檢查 toosee 哪些 VM 大小是使用中的現有的可用性設定組使用 hello toouse`--availability-set list-sizes`參數。

## <a name="check-for-available-vm-sizes"></a>檢查可用的 VM 大小 

您可以加入更多的 Vm toohello 可用性設定組更新版本中，但您需要一個 tooknow hello 硬體上可用哪些 VM 大小。 使用[az vm 可用性設定組清單大小](/cli/azure/availability-set#list-sizes)toolist hello 硬體上的 hello 可用大小叢集以 hello 可用性設定組。

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 建立可用性設定組
> * 在可用性設定組中建立 VM
> * 檢查可用的 VM 大小

前進 toohello 下一個教學課程的 toolearn 有關虛擬機器規模集。

> [!div class="nextstepaction"]
> [建立 VM 擴展集](tutorial-create-vmss.md)

