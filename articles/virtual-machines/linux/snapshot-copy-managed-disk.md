---
title: "複製 Azure 受控磁碟作為備份 | Microsoft Docs"
description: "了解如何建立 Azure 受控磁碟的複本作為備份，或用於針對磁碟問題進行疑難排解。"
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
ms.openlocfilehash: c91367ef11c9d531bebac7c069d2df586607ec29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="5305d-103">使用受控快照集建立 VHD 的複本並儲存為 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="5305d-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="5305d-104">建立受控磁碟的快照集作為備份，或從快照集建立受控磁碟並將它附加至測試虛擬機器進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5305d-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="5305d-105">受控快照集是 VM 受控磁碟的完整時間點複本。</span><span class="sxs-lookup"><span data-stu-id="5305d-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="5305d-106">它會建立 VHD 的唯讀複本，而且根據預設儲存為標準受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="5305d-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="5305d-107">如需價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/managed-disks/)。</span><span class="sxs-lookup"><span data-stu-id="5305d-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link to topic or blog post that explains managed disks. -->

<span data-ttu-id="5305d-108">使用 Azure 入口網站或 Azure CLI 2.0 製作受控磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="5305d-108">Use either the Azure portal or the Azure CLI 2.0 to take a snapshot of the Managed Disk.</span></span>

## <a name="use-azure-cli-20-to-take-a-snapshot"></a><span data-ttu-id="5305d-109">使用 Azure CLI 2.0 製作快照集</span><span class="sxs-lookup"><span data-stu-id="5305d-109">Use Azure CLI 2.0 to take a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="5305d-110">下列範例需要安裝 Azure CLI 2.0 並登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5305d-110">The following example requires the Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="5305d-111">下列步驟說明如何使用 `az snapshot create` 命令搭配 `--source-disk` 參數，取得及製作受控 OS 磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="5305d-111">The following steps show how to obtain and take a snapshot of a managed OS disk using the `az snapshot create` command with the `--source-disk` parameter.</span></span> <span data-ttu-id="5305d-112">下列範例假設有一個名為 `myVM` 的 VM，該 VM 是使用 `myResourceGroup` 資源群組中的受控 OS 磁碟加以建立。</span><span class="sxs-lookup"><span data-stu-id="5305d-112">The following example assumes that there is a VM called `myVM` created with a managed OS disk in the `myResourceGroup` resource group.</span></span>

```azure-cli
# take the disk id with which to create a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="5305d-113">輸出應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5305d-113">The output should look something like:</span></span>

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

## <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="5305d-114">使用 Azure 入口網站建立快照集</span><span class="sxs-lookup"><span data-stu-id="5305d-114">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="5305d-115">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5305d-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5305d-116">從左上方開始，按一下 [新增]並搜尋**快照集**。</span><span class="sxs-lookup"><span data-stu-id="5305d-116">Starting in the upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="5305d-117">在 [快照集] 刀鋒視窗中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5305d-117">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="5305d-118">輸入快照集的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="5305d-118">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="5305d-119">選取現有的[資源群組](../../azure-resource-manager/resource-group-overview.md#resource-groups)，或輸入新群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="5305d-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="5305d-120">選取 Azure 資料中心的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="5305d-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="5305d-121">在 [來源磁碟] 中，選取要建立快照集的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="5305d-121">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="5305d-122">選取用來儲存快照集的 [帳戶類型]。</span><span class="sxs-lookup"><span data-stu-id="5305d-122">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="5305d-123">除非需要儲存在高效能磁碟上，否則建議選取 **Standard_LRS**。</span><span class="sxs-lookup"><span data-stu-id="5305d-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="5305d-124">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5305d-124">Click **Create**.</span></span>

<span data-ttu-id="5305d-125">如果您打算使用快照集來建立受控磁碟，並將它附加至必須是高效能的 VM，請使用 `--sku Premium_LRS` 參數搭配 `az snapshot create` 命令。</span><span class="sxs-lookup"><span data-stu-id="5305d-125">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `--sku Premium_LRS` with the `az snapshot create` command.</span></span> <span data-ttu-id="5305d-126">這麼做建立的快照集會儲存為進階受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="5305d-126">This creates the snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="5305d-127">進階受控磁碟的效能比較好，因為它們是固態硬碟 (SSD)，但成本高於標準磁碟 (HDD)。</span><span class="sxs-lookup"><span data-stu-id="5305d-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


