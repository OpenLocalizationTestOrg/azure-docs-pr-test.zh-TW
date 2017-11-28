---
title: "準備目標 (VMware tooAzure) |Microsoft 文件"
description: "本文說明如何 tooprepare 複寫 VMware 虛擬機器 tooAzure 您 Azure 環境 toostart。"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="d2d02-103">準備目標 (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="d2d02-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2d02-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="d2d02-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="d2d02-105">實體 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d2d02-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="d2d02-106">本文說明如何 tooprepare 複寫 VMware 虛擬機器 tooAzure 您 Azure 環境 toostart。</span><span class="sxs-lookup"><span data-stu-id="d2d02-106">This article describes how tooprepare your Azure environment toostart replicating VMware virtual machines tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2d02-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="d2d02-107">Prerequisites</span></span>

<span data-ttu-id="d2d02-108">hello 文章假設 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d2d02-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="d2d02-109">您已建立復原服務保存庫 tooprotect VMware 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d2d02-109">You have created a Recovery Services Vault tooprotect your VMware virtual machines.</span></span> <span data-ttu-id="d2d02-110">您可以建立復原服務保存庫，從 hello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="d2d02-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="d2d02-111">您有[安裝程式在內部部署環境](./site-recovery-set-up-vmware-to-azure.md)tooreplicate VMware 虛擬機器 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d2d02-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware virtual machines tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="d2d02-112">準備目標</span><span class="sxs-lookup"><span data-stu-id="d2d02-112">Prepare target</span></span>

<span data-ttu-id="d2d02-113">完成 hello 之後**步驟 1:Select 保護目標**和**步驟 2： 準備來源**，會將您導向太**步驟 3： 目標**</span><span class="sxs-lookup"><span data-stu-id="d2d02-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![準備目標](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="d2d02-115">**訂用帳戶：** hello 從下拉式清單選取 hello 您想 tooreplicate 訂用帳戶 功能表，您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d2d02-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your virtual machines to.</span></span>
2. <span data-ttu-id="d2d02-116">**部署模型：**選取 hello 部署模型 （Classic 或資源管理員）</span><span class="sxs-lookup"><span data-stu-id="d2d02-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="d2d02-117">根據 hello 選擇部署模型，會執行驗證，您有至少一個相容的儲存體帳戶和虛擬網路中 hello 目標訂用帳戶 tooreplicate 和容錯移轉虛擬機器以 tooensure。</span><span class="sxs-lookup"><span data-stu-id="d2d02-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your virtual machine to.</span></span>

<span data-ttu-id="d2d02-118">一旦 hello 驗證順利完成，請按一下 [確定] toogo toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d2d02-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="d2d02-119">如果您沒有相容的資源管理員儲存體帳戶或虛擬網路，或想要更多的 tooadd，您可以按一下 hello **+ 儲存體帳戶**或**+ 網路**上 hello hello 頂端的按鈕刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d2d02-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2d02-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2d02-120">Next steps</span></span>
<span data-ttu-id="d2d02-121">[設定複寫設定](./site-recovery-setup-replication-settings-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="d2d02-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
