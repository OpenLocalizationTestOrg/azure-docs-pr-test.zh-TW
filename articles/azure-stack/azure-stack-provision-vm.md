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
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 4e3f90fe35b7fb2509db0eb7a467305f4c4167ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="9da59-103">在 Azure Stack 中建立測試虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9da59-103">Create a test virtual machine in Azure Stack</span></span>
<span data-ttu-id="9da59-104">身為雲端操作員，您可以建立測試虛擬機器來驗證 Azure Stack 部署。</span><span class="sxs-lookup"><span data-stu-id="9da59-104">As a cloud operator, you can create a test virtual machine to validate your Azure Stack deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="9da59-105">佈建虛擬機器之前，您必須[將 Windows Server 2016 評估版映像新增至 Azure Stack 市集](azure-stack-add-default-image.md)。</span><span class="sxs-lookup"><span data-stu-id="9da59-105">Before you can provision virtual machines, you must [add the Windows Server 2016 Evaluation image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="9da59-106">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9da59-106">Create a virtual machine</span></span>
1. <span data-ttu-id="9da59-107">在 Azure Stack 開發套件主機上，[登入](azure-stack-connect-azure-stack.md)系統管理員入口網站 (`https://adminportal.local.azurestack.external`)，然後按一下 [新增] > [計算] > [Windows Server 2016 Datacenter 評估版] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="9da59-107">On the Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) to the administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="9da59-108">在 [基本] 刀鋒視窗中，輸入 [名稱]、[使用者名稱] 與 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="9da59-108">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="9da59-109">選擇 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="9da59-109">Choose a **Subscription**.</span></span> <span data-ttu-id="9da59-110">建立 [資源群組]，或選取現有的資源群組，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9da59-110">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="9da59-111">在 [選擇大小] 刀鋒視窗中，按一下 [A1 標準]，再按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="9da59-111">In the **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="9da59-112">在 [設定] 刀鋒視窗中，接受預設值並按一下 [確定]</span><span class="sxs-lookup"><span data-stu-id="9da59-112">In the **Settings** blade, accept the defaults and click **OK**</span></span>
5. <span data-ttu-id="9da59-113">在 [摘要] 刀鋒視窗中，按一下 [確定]，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9da59-113">In the **Summary** blade, click **OK** to create the virtual machine.</span></span>  
6. <span data-ttu-id="9da59-114">若要查看您的新虛擬機器，請按一下 [所有資源]，然後搜尋虛擬機器並按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="9da59-114">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="9da59-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9da59-115">Next steps</span></span>
[<span data-ttu-id="9da59-116">使用 Azure Stack 中系統管理員和使用者的入口網站</span><span class="sxs-lookup"><span data-stu-id="9da59-116">Using the administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
