---
title: "Azure 受管理備份磁碟上的 aaaCopy |Microsoft 文件"
description: "了解如何 toocreate 回最新或疑難排解磁碟 Azure 受管理磁碟 toouse 一份問題。"
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="b7ca7-103">使用受控快照集建立 VHD 的複本並儲存為 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="b7ca7-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="b7ca7-104">取得備份的受管理磁碟的快照或從 hello 快照集建立受管理磁碟並將它附加 tooa 測試虛擬機器 tootroubleshoot。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="b7ca7-105">受控快照集是 VM 受控磁碟的完整時間點複本。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="b7ca7-106">它會建立 VHD 的唯讀複本，而且根據預設儲存為標準受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="b7ca7-107">如需價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/managed-disks/)。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="b7ca7-108">使用 Azure 入口網站或 hello Azure CLI 2.0 tootake 任一 hello hello 受管理磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="b7ca7-109">使用 Azure CLI 2.0 tootake 快照集</span><span class="sxs-lookup"><span data-stu-id="b7ca7-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="b7ca7-110">hello 下列範例要求 hello Azure CLI 2.0 安裝並登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="b7ca7-111">hello 下列步驟顯示如何 tooobtain 並採取快照集的受管理的作業系統磁碟使用 hello`az snapshot create`命令與 hello`--source-disk`參數。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="b7ca7-112">hello 下列範例假設有呼叫 VM`myVM`建立的受管理的作業系統磁碟在 hello`myResourceGroup`資源群組。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="b7ca7-113">hello 輸出應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="b7ca7-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="b7ca7-114">使用 Azure 入口網站 tootake 快照集</span><span class="sxs-lookup"><span data-stu-id="b7ca7-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="b7ca7-115">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b7ca7-116">從開始 hello 左上方，按一下**新增**並搜尋**快照**。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="b7ca7-117">在 hello 快照刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="b7ca7-118">輸入**名稱**hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="b7ca7-119">選取現有[資源群組](../../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="b7ca7-120">選取 Azure 資料中心的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="b7ca7-121">如**來源磁碟**，選取 hello toosnapshot 管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="b7ca7-122">選取 hello**帳戶類型**toouse toostore hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="b7ca7-123">除非需要儲存在高效能磁碟上，否則建議選取 **Standard_LRS**。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="b7ca7-124">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-124">Click **Create**.</span></span>

<span data-ttu-id="b7ca7-125">如果您規劃 toouse hello 快照 toocreate 受管理的磁碟，並將它附加 toobe 高執行所需的 VM，使用 hello 參數`--sku Premium_LRS`以 hello`az snapshot create`命令。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="b7ca7-126">這會建立 hello 快照集，使它儲存為 Premium 管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="b7ca7-127">進階受控磁碟的效能比較好，因為它們是固態硬碟 (SSD)，但成本高於標準磁碟 (HDD)。</span><span class="sxs-lookup"><span data-stu-id="b7ca7-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


