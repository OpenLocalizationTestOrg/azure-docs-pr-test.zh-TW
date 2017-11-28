---
title: "aaaStorage Azure 堆疊中的帳戶 |Microsoft 文件"
description: "了解如何 toocreate Azure 堆疊儲存體帳戶。"
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
ms.openlocfilehash: 5b1f84b15597245cc5ed7e49494dd3abf8d827a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storage-accounts-in-azure-stack"></a><span data-ttu-id="ff775-103">Azure Stack 中的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ff775-103">Storage accounts in Azure Stack</span></span>
<span data-ttu-id="ff775-104">儲存體帳戶包含 Blob 和表格服務和 hello 存放資料物件的唯一命名空間。</span><span class="sxs-lookup"><span data-stu-id="ff775-104">Storage accounts include Blob and Table services, and hello unique namespace for your storage data objects.</span></span> <span data-ttu-id="ff775-105">根據預設，您的帳戶中的 hello 資料會是可用的唯一 tooyou，hello 儲存體帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="ff775-105">By default, hello data in your account is available only tooyou, hello storage account owner.</span></span>

1. <span data-ttu-id="ff775-106">Hello Azure 堆疊 POC 在電腦上，登入太`https://adminportal.local.azurestack.external`為[管理員](azure-stack-connect-azure-stack.md)，然後按一下**新增** > **資料 + 儲存體** >  **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ff775-106">On hello Azure Stack POC computer, log in too`https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span></span>

   ![](media/azure-stack-provision-storage-account/image01.png)
2. <span data-ttu-id="ff775-107">在 hello**建立儲存體帳戶**刀鋒視窗中，輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="ff775-107">In hello **Create storage account** blade, type a name for your storage account.</span></span> <span data-ttu-id="ff775-108">建立新**資源群組**，或選取現有的圖示，然後按一下 **建立**toocreate hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff775-108">Create a new **Resource Group**, or select an existing one, then click **Create** toocreate hello storage account.</span></span>

   ![](media/azure-stack-provision-storage-account/image02.png)
3. <span data-ttu-id="ff775-109">toosee 新的儲存體帳戶，按一下 **所有資源**，然後搜尋 hello 儲存體帳戶，然後按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="ff775-109">toosee your new storage account, click **All resources**, then search for hello storage account and click its name.</span></span>

    ![](media/azure-stack-provision-storage-account/image03.png)

### <a name="next-steps"></a><span data-ttu-id="ff775-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff775-110">Next steps</span></span>
[<span data-ttu-id="ff775-111">使用 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="ff775-111">Use Azure Resource Manager templates</span></span>](azure-stack-arm-templates.md)

[<span data-ttu-id="ff775-112">深入了解 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ff775-112">Learn about Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)

[<span data-ttu-id="ff775-113">下載 hello Azure 堆疊 Azure 一致的存放裝置驗證指南</span><span class="sxs-lookup"><span data-stu-id="ff775-113">Download hello Azure Stack Azure-consistent Storage Validation Guide</span></span>](http://aka.ms/azurestacktp1doc)
