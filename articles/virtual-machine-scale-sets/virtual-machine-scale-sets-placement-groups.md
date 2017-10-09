---
title: "使用大型的 Azure 虛擬機器擴展集 aaaWorking |Microsoft 文件"
description: "您的需要 tooknow toouse 大型 Azure 虛擬機器擴充集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>使用大型的虛擬機器擴展集
您現在可以建立 Azure[虛擬機器擴展集](/azure/virtual-machine-scale-sets/)too1，000 Vm 上的容量。 本文件_大型虛擬機器規模集_定義為在擴展集能夠調整 toogreater 超過 100 的 Vm。 此容量是由擴展集屬性 (_singlePlacementGroup=False_) 所設定。 

大規模的特定部分設定，例如負載平衡和容錯網域有不同的行為 tooa 標準規模集。 本文件說明的中的大規模 hello 特性，並說明哪些需要 tooknow toosuccessfully 中使用這些應用程式。 

常見的方法進行部署大的規模的雲端基礎結構是 toocreate 一組_延展單位_，例如藉由建立多個 Vm 跨多個 Vnet 和儲存體帳戶中調整設定。 這種方法讓您更輕鬆管理比較 toosingle Vm，而且多個擴充單元可用於許多應用程式，尤其是需要其他可堆疊的元件，例如多個虛擬網路和端點。 如果您的應用程式需要單一大型叢集但，它可以是單一的小數位數的設定 too1，000 Vm 更直接 toodeploy。 範例案例包括集中式的巨量資料部署，或是需要可簡單管理大型背景工作節點集區的計算方格。 與 VM 規模調整集合結合[附加資料磁碟](virtual-machine-scale-sets-attached-disks.md)，大規模集可讓您 toodeploy 可擴充的基礎結構，包含數千個核心和 pb 計的儲存體，以單一作業。

## <a name="placement-groups"></a>放置群組 
構成_大型_設定特殊的小數位數不 hello 的 Vm，但如果 hello 數目_放置群組_其中的內容。 放置群組是建構類似 tooan Azure 可用性設定組，與它自己的容錯網域和升級網域。 根據預設，擴展集包含一個大小上限為 100 個 VM 的位置群組。 如果小數位數設定的屬性稱為_singlePlacementGroup_設定 too_false_，hello 規模集可能會組成多個位置群組，而有 0-1000 的範圍 Vm。 當設定 toohello 預設值是_true_，小數位數是由單一的位置 群組中，以及範圍為 0-100 Vm。

## <a name="checklist-for-using-large-scale-sets"></a>使用大型擴展集的檢查清單
toodecide 是否可大規模集合的有效地使用您的應用程式。 請考慮下列需求的 hello:

- 大型擴展集需要 Azure 受控磁碟。 所建立的擴展集若非使用受控磁碟，則需要多個儲存體帳戶 (每 20 個 VM 一個)。 設計的 toowork 獨佔方式使用受管理磁碟 tooreduce 儲存體管理額外負荷，以及 tooavoid hello 的風險執行訂用帳戶限制的儲存體帳戶中的大規模集合。 如果您未使用受管理的磁碟，小數位數組是有限的 too100 Vm。
- 從 Azure Marketplace 映像建立的規模集就能相應 too1，000 Vm。
- 擴展集所建立的自訂映像 （VM 映像您建立及上傳您自己） 目前可以 too100 Vm 向上延展。
- 第 4 層負載平衡及 hello Azure 負載平衡器尚未支援多個位置群組所組成的小數位數組。 如果您需要 toouse hello Azure 負載平衡器進行確定 hello 擴展集是設定的 toouse 單一位置群組，也就是 hello 預設設定。
- 支援所有的小數位數組 7 層負載平衡及 hello Azure 應用程式閘道。
- 擴展集以單一子網路定義-請確定您的子網路具有位址空間夠大，您需要的所有 hello vm。 根據預設小數位數設定 overprovisions （建立額外的 Vm，在部署時，或向外延展，則不需收費的） tooimprove 部署可靠性和效能。 允許的位址空間 20%大於 hello 您計劃要 tooscale 中 Vm 的數目。
- 如果您計劃 toodeploy 許多 Vm，您的運算核心配額限制可能需要增加 toobe。
- 容錯網域和升級網域只會在放置群組內保持一致。 這個架構不會變更 hello 整體標尺的可用性設定，因為 Vm 平均分散於不同的實體硬體，但也不會表示，如果您需要的 tooguarantee 兩個 Vm 位於不同的硬體，請確定這些主機位於不同的錯誤中的網域 hello 相同位置 群組。 容錯網域和放置群組的識別碼會顯示在 hello_執行個體檢視_的小數位數設定的 VM。 您可以檢視 hello 擴展集 VM 執行個體檢視中 hello [Azure 資源總管](https://resources.azure.com/)。


## <a name="creating-a-large-scale-set"></a>建立大型擴展集
當您建立 hello Azure 入口網站中設定的標尺時，您可以允許它 tooscale toomultiple 放置群組設定 hello_限制 tooa 單一位置群組_在 hello 選項 too_False__基本概念_刀鋒視窗。 使用此選項設定 too_False_，您可以指定_執行個體計數_too1，000 的值。

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

您可以建立使用 hello 設定大型 VM 規模調整[Azure CLI](https://github.com/Azure/azure-cli) _az vmss 建立_命令。 此命令會設定智慧型預設值，例如子網路大小根據 hello_執行個體計數_引數：

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
請注意該 hello _vmss 建立_命令預設某些設定值，如果您未指定。 toosee hello 可用的選項，您可以覆寫，請再試一次：
```bash
az vmss create --help
```

如果您要建立大規模撰寫 Azure Resource Manager 範本設定，請確定 hello 範本建立 Azure 受管理磁碟為基礎的小數位數集。 您可以設定 hello _singlePlacementGroup_在 hello 屬性 too_false__屬性_區段 hello _Microsoft.Compute/virtualMAchineScaleSets_資源。 hello 下列 JSON 片段顯示的小數位數組範本，包括 hello 1000 的 VM 容量和 hello 的 hello 開頭_"singlePlacementGroup": false_設定：
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
如需完整的範例，若要大規模的設定範本，請參閱太[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json)。

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>轉換現有的小數位數設定多個位置群組 toospan
toomake 現有的 VM 規模調整集合能夠調整 toomore 超過 100 的 Vm，您需要 toochange hello _singplePlacementGroup_屬性 too_false_ hello 規模設定的模型。 您可以測試變更這個屬性與 hello [Azure 資源總管](https://resources.azure.com/)。 尋找現有的小數位數集合，選取_編輯_並變更 hello _singlePlacementGroup_屬性。 如果看不到此屬性，您可能會檢視 hello 與較舊版本的 hello Microsoft.Compute 應用程式開發介面所設定的小數位數。

>[!NOTE] 
您可以變更設定從支援唯一 （hello 預設行為） tooa 支援多個位置群組，單一放置群組的比例，但您無法將轉換 hello 反過來。 因此請確定您了解的大型集合，然後再將轉換的 hello 屬性。 特別是，請確定您不需要第 4 層負載平衡及 hello Azure 負載平衡器。


