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
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="b3807-103">Azure VM 擴展集與受控磁碟</span><span class="sxs-lookup"><span data-stu-id="b3807-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="b3807-104">Azure [虛擬機器擴展集](/azure/virtual-machine-scale-sets/)支援具有受控磁碟的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3807-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="b3807-105">搭配使用受控磁碟與擴展集有數個優點，包括：</span><span class="sxs-lookup"><span data-stu-id="b3807-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="b3807-106">您不再需要 toopre-建立和管理儲存體帳戶 toostore hello OS 磁碟 hello 擴展集 Vm。</span><span class="sxs-lookup"><span data-stu-id="b3807-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="b3807-107">您可以附加受管理的資料磁碟 toohello 規模集。</span><span class="sxs-lookup"><span data-stu-id="b3807-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="b3807-108">利用受控磁碟，擴展集所擁有的容量可以高達 1,000 個 VM (如果以平台映像為基礎) 或 100 個 VM (如果以自訂映像為基礎)。</span><span class="sxs-lookup"><span data-stu-id="b3807-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="b3807-109">開始使用</span><span class="sxs-lookup"><span data-stu-id="b3807-109">Get started</span></span>

<span data-ttu-id="b3807-110">簡單的方式 tooget 入門 受管理的磁碟規模集是從 Azure 入口網站 hello toodeploy 其中一個。</span><span class="sxs-lookup"><span data-stu-id="b3807-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="b3807-111">如需詳細資訊，請參閱 [本篇文章](./virtual-machine-scale-sets-portal-create.md)。</span><span class="sxs-lookup"><span data-stu-id="b3807-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="b3807-112">另一個簡單的方式啟動 tooget 是 toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy 規模調整集合。</span><span class="sxs-lookup"><span data-stu-id="b3807-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="b3807-113">hello 下列範例顯示如何 toocreate Ubuntu 基礎具有每個都具有 50 GB 和 100 GB 資料磁碟的 10 部 Vm 擴展集：</span><span class="sxs-lookup"><span data-stu-id="b3807-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="b3807-114">或者，您無法查看 hello [Azure 快速入門範本 GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates)資料夾包含`vmss`toosee 預先建立的部署規模集的範本的例子。</span><span class="sxs-lookup"><span data-stu-id="b3807-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="b3807-115">tootell 哪些範本已經在使用受管理的磁碟，您可以使用參照太[這份清單](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)。</span><span class="sxs-lookup"><span data-stu-id="b3807-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3807-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3807-116">Next steps</span></span>

<span data-ttu-id="b3807-117">如需更多有關一般受控磁碟的資訊，請參閱[這篇文章](../virtual-machines/windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b3807-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="b3807-118">toosee 如何 tooconvert 資源管理員範本 tooprovision 規模設定具有管理的磁碟，請參閱[本文](./virtual-machine-scale-sets-convert-template-to-md.md)。</span><span class="sxs-lookup"><span data-stu-id="b3807-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="b3807-119">hello 相同修改 toohello 資源管理員範本套用 toohello 以及 Azure REST API。</span><span class="sxs-lookup"><span data-stu-id="b3807-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="b3807-120">toolearn 進一步了解使用受管理的資料磁碟的小數位數的集合，請參閱[本文](./virtual-machine-scale-sets-attached-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="b3807-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="b3807-121">使用大型擴充集 toobegin 參照太[本文](./virtual-machine-scale-sets-placement-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="b3807-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


