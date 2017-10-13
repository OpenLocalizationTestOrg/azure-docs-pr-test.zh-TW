---
title: "在 Azure Stack 中建立測試 VM | Microsoft Docs"
description: "了解如何在 Azure Stack 中，以雲端操作員的身分佈建測試 VM。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: erikje
ms.openlocfilehash: 233cf4df53af6a49e5fe4c5d51e112d8196a7530
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="b66dc-103">在 Azure Stack 中建立測試虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b66dc-103">Create a test virtual machine in Azure Stack</span></span>

<span data-ttu-id="b66dc-104">適用於：Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="b66dc-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="b66dc-105">身為 Azure Stack 操作員，您可以建立測試虛擬機器來驗證 [Azure Stack](azure-stack-poc.md) 開發人員套件部署。</span><span class="sxs-lookup"><span data-stu-id="b66dc-105">As an Azure Stack operator, you can create a test virtual machine to validate your [Azure Stack](azure-stack-poc.md) Developer Kit deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="b66dc-106">佈建虛擬機器之前，您必須[將 Windows Server 2016 評估版映像新增至 Azure Stack 市集](azure-stack-add-default-image.md)。</span><span class="sxs-lookup"><span data-stu-id="b66dc-106">Before you can provision virtual machines, you must [add the Windows Server 2016 Evaluation image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="b66dc-107">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b66dc-107">Create a virtual machine</span></span>
1. <span data-ttu-id="b66dc-108">在 Azure Stack 開發套件主機上，[登入](azure-stack-connect-azure-stack.md)系統管理員入口網站 (`https://adminportal.local.azurestack.external`)，然後按一下新增 > [計算] > [Windows Server 2016 Datacenter 評估版] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="b66dc-108">On the Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) to the administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="b66dc-109">在 [基本] 刀鋒視窗中，輸入 [名稱]、[使用者名稱] 與 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="b66dc-109">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="b66dc-110">選擇 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="b66dc-110">Choose a **Subscription**.</span></span> <span data-ttu-id="b66dc-111">建立 資源群組，或選取現有的資源群組，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="b66dc-111">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="b66dc-112">在 [選擇大小] 刀鋒視窗中，按一下 [A1 標準]，再按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="b66dc-112">In the **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="b66dc-113">在 [設定] 刀鋒視窗中，接受預設值並按一下 [確定]</span><span class="sxs-lookup"><span data-stu-id="b66dc-113">In the **Settings** blade, accept the defaults and click **OK**</span></span>
5. <span data-ttu-id="b66dc-114">在 [摘要] 刀鋒視窗中，按一下 [確定]，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b66dc-114">In the **Summary** blade, click **OK** to create the virtual machine.</span></span>  
6. <span data-ttu-id="b66dc-115">若要查看您的新虛擬機器，請按一下 [所有資源]，然後搜尋虛擬機器並按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="b66dc-115">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="b66dc-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b66dc-116">Next steps</span></span>
[<span data-ttu-id="b66dc-117">使用 Azure Stack 中系統管理員和使用者的入口網站</span><span class="sxs-lookup"><span data-stu-id="b66dc-117">Using the administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
