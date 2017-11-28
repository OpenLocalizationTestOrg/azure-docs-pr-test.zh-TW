---
title: "aaaFrequently Azure 堆疊常見問題 |Microsoft 文件"
description: "Azure 堆疊常見問題集。"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a><span data-ttu-id="6cc14-103">Azure 堆疊的常見問題集</span><span class="sxs-lookup"><span data-stu-id="6cc14-103">Frequently asked questions for Azure Stack</span></span>
## <a name="deployment"></a><span data-ttu-id="6cc14-104">部署</span><span class="sxs-lookup"><span data-stu-id="6cc14-104">Deployment</span></span>
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a><span data-ttu-id="6cc14-105">我需要 tooformat 我的資料磁碟之前啟動或重新啟動安裝？</span><span class="sxs-lookup"><span data-stu-id="6cc14-105">Do I need tooformat my data disks before starting or restarting an installation?</span></span>
<span data-ttu-id="6cc14-106">磁碟應該是以原始格式。</span><span class="sxs-lookup"><span data-stu-id="6cc14-106">Disks should be in raw format.</span></span> <span data-ttu-id="6cc14-107">如果您重新安裝 hello 作業系統，您可能需要 toocheck hello 舊的存放集區是否仍然存在，並刪除使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cc14-107">If you reinstall hello operating system, you may need toocheck if hello old storage pool is still present and delete using hello following steps:</span></span>

1. <span data-ttu-id="6cc14-108">開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="6cc14-108">Open Server Manager.</span></span>
2. <span data-ttu-id="6cc14-109">選取存放集區。</span><span class="sxs-lookup"><span data-stu-id="6cc14-109">Select Storage Pools.</span></span>
3. <span data-ttu-id="6cc14-110">查看是否列出存放集區。</span><span class="sxs-lookup"><span data-stu-id="6cc14-110">See if a storage pool is listed.</span></span>
4. <span data-ttu-id="6cc14-111">以滑鼠右鍵按一下**存放集區**如果列出和啟用讀取 / 寫入。</span><span class="sxs-lookup"><span data-stu-id="6cc14-111">Right-click **storage pool** if listed and enable read / write.</span></span>
5. <span data-ttu-id="6cc14-112">以滑鼠右鍵按一下**Virtual Hard Disk** （左下的角），選取 刪除。</span><span class="sxs-lookup"><span data-stu-id="6cc14-112">Right-click **Virtual Hard Disk** (Lower left corner) and select delete.</span></span>
6. <span data-ttu-id="6cc14-113">以滑鼠右鍵按一下**存放集區**並按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="6cc14-113">Right-click **Storage Pool** and click delete.</span></span>
7. <span data-ttu-id="6cc14-114">一次啟動 Azure 堆疊指令碼，並確認 hello 磁碟驗證通過。</span><span class="sxs-lookup"><span data-stu-id="6cc14-114">Launch Azure Stack script again and verify that hello disk verification passes.</span></span>

<span data-ttu-id="6cc14-115">（選擇性） 您可以使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cc14-115">Optionally, hello following script can be used:</span></span>

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a><span data-ttu-id="6cc14-116">可以使用所有的 SSD 磁碟 hello POC 安裝中的 hello 存放集區嗎？</span><span class="sxs-lookup"><span data-stu-id="6cc14-116">Can I use all SSD disks for hello storage pool in hello POC installation?</span></span>
<span data-ttu-id="6cc14-117">如需有關存放裝置設定的詳細資訊，請參閱 hello[需求指南](azure-stack-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="6cc14-117">For more information on storage configurations, see hello [requirements guide](azure-stack-deploy.md).</span></span>

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="6cc14-118">我可以使用 Microsoft Azure 堆疊 POC hello NVMe 資料磁碟嗎？</span><span class="sxs-lookup"><span data-stu-id="6cc14-118">Can I use NVMe data disks for hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="6cc14-119">儲存空間直接存取支援 NVMe 磁碟，而 Azure 堆疊只支援子集 hello 可能是磁碟機類型以及可能的組合 Storage Spaces Direct。</span><span class="sxs-lookup"><span data-stu-id="6cc14-119">While Storage Spaces Direct supports NVMe disks, Azure Stack only supports a subset of hello possible drive types and combinations possible for Storage Spaces Direct.</span></span>  <span data-ttu-id="6cc14-120">請參閱 hello[需求指南](azure-stack-deploy.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6cc14-120">See hello [requirements guide](azure-stack-deploy.md) for more information.</span></span> 

### <a name="how-can-i-reinstall-azure-stack"></a><span data-ttu-id="6cc14-121">如何重新安裝 Azure 堆疊？</span><span class="sxs-lookup"><span data-stu-id="6cc14-121">How can I reinstall Azure Stack?</span></span>
<span data-ttu-id="6cc14-122">您可以依照 hello 步驟在 hello[重新部署指南](azure-stack-redeploy.md)。</span><span class="sxs-lookup"><span data-stu-id="6cc14-122">You can follow hello steps in hello [redeployment guide](azure-stack-redeploy.md).</span></span>  

## <a name="tenant"></a><span data-ttu-id="6cc14-123">租用戶</span><span class="sxs-lookup"><span data-stu-id="6cc14-123">Tenant</span></span>
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a><span data-ttu-id="6cc14-124">可以為租用戶部署我自己的映像嗎？</span><span class="sxs-lookup"><span data-stu-id="6cc14-124">Can I deploy my own images as a tenant?</span></span>
<span data-ttu-id="6cc14-125">[是]，就像在 Azure 中，租用戶可以上傳 Azure 的堆疊中的映像，此外 hello toousing hello 映像服務管理員。</span><span class="sxs-lookup"><span data-stu-id="6cc14-125">Yes, just like in Azure, a tenant can upload images in Azure Stack, in addition toousing hello images from hello service administrator.</span></span> <span data-ttu-id="6cc14-126">如需概觀，請參閱 hello[加入 VM 映像](azure-stack-add-vm-image.md)。</span><span class="sxs-lookup"><span data-stu-id="6cc14-126">For an overview, see hello [Adding a VM Image](azure-stack-add-vm-image.md).</span></span> 

## <a name="testing"></a><span data-ttu-id="6cc14-127">測試</span><span class="sxs-lookup"><span data-stu-id="6cc14-127">Testing</span></span>
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="6cc14-128">可以使用巢狀虛擬化 tootest hello Microsoft Azure 堆疊 POC 嗎？</span><span class="sxs-lookup"><span data-stu-id="6cc14-128">Can I use Nested Virtualization tootest hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="6cc14-129">不支援巢狀虛擬化或 Azure 堆疊 Technical Preview 3 中進行測試。</span><span class="sxs-lookup"><span data-stu-id="6cc14-129">Nested virtualization is not supported or tested with Azure Stack Technical Preview 3.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="6cc14-130">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6cc14-130">Virtual machines</span></span>
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a><span data-ttu-id="6cc14-131">Azure 堆疊支援動態磁碟的虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="6cc14-131">Does Azure Stack support dynamic disks for virtual machines?</span></span>
<span data-ttu-id="6cc14-132">Azure 堆疊不支援動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="6cc14-132">Azure Stack does not support dynamic disks.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6cc14-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cc14-133">Next steps</span></span>
[<span data-ttu-id="6cc14-134">疑難排解</span><span class="sxs-lookup"><span data-stu-id="6cc14-134">Troubleshooting</span></span>](azure-stack-troubleshooting.md)

