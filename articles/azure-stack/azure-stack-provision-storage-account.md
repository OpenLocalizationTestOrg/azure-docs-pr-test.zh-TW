---
title: "Azure Stack 中的儲存體帳戶 | Microsoft Docs"
description: "了解如何建立 Azure Stack 儲存體帳戶。"
services: azure-stack
documentationcenter: 
author: vhorne
manager: byronr
editor: 
ms.assetid: e1152110-b756-4c1a-9fa2-73fe3ab0ad8e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: victorh
ms.openlocfilehash: de32c0ce79e8357274cc19cd1ea4ec23b85b918f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="storage-accounts-in-azure-stack"></a><span data-ttu-id="8b5ee-103">Azure Stack 中的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8b5ee-103">Storage accounts in Azure Stack</span></span>
<span data-ttu-id="8b5ee-104">儲存體帳戶包含 Blob 與資料表服務，且儲存體資料物件的命名空間不得重複。</span><span class="sxs-lookup"><span data-stu-id="8b5ee-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span></span> <span data-ttu-id="8b5ee-105">根據預設，您帳戶中的資料只有身為儲存體帳戶擁有者的您可以使用。</span><span class="sxs-lookup"><span data-stu-id="8b5ee-105">By default, the data in your account is available only to you, the storage account owner.</span></span>

1. <span data-ttu-id="8b5ee-106">在 Azure Stack POC 電腦上，以[系統管理員](azure-stack-connect-azure-stack.md)身分登入 `https://adminportal.local.azurestack.external`，然後按一下 [新增] > [資料 + 儲存體] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="8b5ee-106">On the Azure Stack POC computer, log in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span></span>

   ![](media/azure-stack-provision-storage-account/image01.png)
2. <span data-ttu-id="8b5ee-107">在 [建立儲存體帳戶] 刀鋒視窗中，輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="8b5ee-107">In the **Create storage account** blade, type a name for your storage account.</span></span> <span data-ttu-id="8b5ee-108">建立新的 [資源群組]，或選取現有的資源群組，然後按一下 [建立]，以建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8b5ee-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span></span>

   ![](media/azure-stack-provision-storage-account/image02.png)
3. <span data-ttu-id="8b5ee-109">若要查看您的新儲存體帳戶，請按一下 [所有資源]，然後搜尋儲存體帳戶並按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="8b5ee-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span></span>

    ![](media/azure-stack-provision-storage-account/image03.png)

### <a name="next-steps"></a><span data-ttu-id="8b5ee-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b5ee-110">Next steps</span></span>
[<span data-ttu-id="8b5ee-111">使用 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="8b5ee-111">Use Azure Resource Manager templates</span></span>](azure-stack-arm-templates.md)

[<span data-ttu-id="8b5ee-112">深入了解 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8b5ee-112">Learn about Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)

<span data-ttu-id="8b5ee-113">[下載 Azure Stack 與 Azure 一致的儲存體驗證指南](http://aka.ms/azurestacktp1doc) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="8b5ee-113">[Download the Azure Stack Azure-consistent Storage Validation Guide](http://aka.ms/azurestacktp1doc)</span></span>
