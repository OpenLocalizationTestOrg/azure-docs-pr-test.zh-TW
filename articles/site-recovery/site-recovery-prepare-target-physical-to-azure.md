---
title: "準備目標 (實體至 Azure) | Microsoft Docs"
description: "本文將說明如何準備您的 Azure 環境，以便開始將執行 Windows 或 Linux 的實體伺服器複寫至 Azure。"
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
ms.openlocfilehash: aa7a32ace8354f615a8b8cc137f6bdf48fbadf48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="4c44a-103">準備目標 (VMware 至 Azure)</span><span class="sxs-lookup"><span data-stu-id="4c44a-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c44a-104">VMware 至 Azure</span><span class="sxs-lookup"><span data-stu-id="4c44a-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="4c44a-105">實體至 Azure</span><span class="sxs-lookup"><span data-stu-id="4c44a-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="4c44a-106">本文將說明如何準備您的 Azure 環境，以便開始將執行 Windows 或 Linux 的實體伺服器 (x64) 複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4c44a-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c44a-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="4c44a-107">Prerequisites</span></span>

<span data-ttu-id="4c44a-108">本文的假設如下：</span><span class="sxs-lookup"><span data-stu-id="4c44a-108">The article assumes the following:</span></span>
- <span data-ttu-id="4c44a-109">您已建立復原服務保存庫，用以保護實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="4c44a-109">You have created a Recovery Services Vault to protect your physical servers.</span></span> <span data-ttu-id="4c44a-110">您可以從 [Azure 入口網站] (http://portal.azure.com "Azure 入口網站")建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="4c44a-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="4c44a-111">您已[設定內部部署環境](./site-recovery-set-up-physical-to-azure.md)以將實體伺服器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4c44a-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="4c44a-112">準備目標</span><span class="sxs-lookup"><span data-stu-id="4c44a-112">Prepare target</span></span>

<span data-ttu-id="4c44a-113">完成**步驟 1：選取保護目標**和**步驟 2︰準備來源**之後，即會進入**步驟 3︰目標**</span><span class="sxs-lookup"><span data-stu-id="4c44a-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![準備目標](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="4c44a-115">**訂用帳戶︰**從下拉式功能表中選取您想要的訂用帳戶，以將實體伺服器複寫至該訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c44a-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span></span>
2. <span data-ttu-id="4c44a-116">**部署模型︰**選取部署模型 (傳統或資源管理員)</span><span class="sxs-lookup"><span data-stu-id="4c44a-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="4c44a-117">根據所選的部署模型，系統會執行驗證以確保您的目標訂用帳戶中有至少一個相容的儲存體帳戶和虛擬網路，以便將您的實體伺服器複寫和容錯移轉至其中。</span><span class="sxs-lookup"><span data-stu-id="4c44a-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span></span>

<span data-ttu-id="4c44a-118">驗證成功完成後，按一下 [確定] 以移至下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="4c44a-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="4c44a-119">如果您沒有相容的 Resource Manager 儲存體帳戶或虛擬網路，或想要新增更多，只要按一下刀鋒視窗頂端的 **+ 儲存體帳戶**或 **+ 網路**按鈕即可。</span><span class="sxs-lookup"><span data-stu-id="4c44a-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c44a-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c44a-120">Next steps</span></span>
<span data-ttu-id="4c44a-121">[設定複寫設定](./site-recovery-setup-replication-settings-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="4c44a-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
