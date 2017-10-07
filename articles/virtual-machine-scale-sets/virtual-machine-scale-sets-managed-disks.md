---
title: "aaaUsing 管理磁碟與 Azure 虛擬機器擴展集 |Microsoft 文件"
description: "了解原因和方式 toouse 管理的磁碟與虛擬機器規模集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Azure VM 擴展集與受控磁碟

Azure [虛擬機器擴展集](/azure/virtual-machine-scale-sets/)支援具有受控磁碟的虛擬機器。 搭配使用受控磁碟與擴展集有數個優點，包括：

* 您不再需要 toopre-建立和管理儲存體帳戶 toostore hello OS 磁碟 hello 擴展集 Vm。

* 您可以附加受管理的資料磁碟 toohello 規模集。

* 利用受控磁碟，擴展集所擁有的容量可以高達 1,000 個 VM (如果以平台映像為基礎) 或 100 個 VM (如果以自訂映像為基礎)。

## <a name="get-started"></a>開始使用

簡單的方式 tooget 入門 受管理的磁碟規模集是從 Azure 入口網站 hello toodeploy 其中一個。 如需詳細資訊，請參閱 [本篇文章](./virtual-machine-scale-sets-portal-create.md)。 另一個簡單的方式啟動 tooget 是 toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy 規模調整集合。 hello 下列範例顯示如何 toocreate Ubuntu 基礎具有每個都具有 50 GB 和 100 GB 資料磁碟的 10 部 Vm 擴展集：

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

或者，您無法查看 hello [Azure 快速入門範本 GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates)資料夾包含`vmss`toosee 預先建立的部署規模集的範本的例子。 tootell 哪些範本已經在使用受管理的磁碟，您可以使用參照太[這份清單](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)。

## <a name="next-steps"></a>後續步驟

如需更多有關一般受控磁碟的資訊，請參閱[這篇文章](../virtual-machines/windows/managed-disks-overview.md)。

toosee 如何 tooconvert 資源管理員範本 tooprovision 規模設定具有管理的磁碟，請參閱[本文](./virtual-machine-scale-sets-convert-template-to-md.md)。 hello 相同修改 toohello 資源管理員範本套用 toohello 以及 Azure REST API。

toolearn 進一步了解使用受管理的資料磁碟的小數位數的集合，請參閱[本文](./virtual-machine-scale-sets-attached-disks.md)。

使用大型擴充集 toobegin 參照太[本文](./virtual-machine-scale-sets-placement-groups.md)。


