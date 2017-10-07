---
title: "測試 Azure 堆疊中的 VM aaaCreate |Microsoft 文件"
description: "深入了解如何 tooprovision 測試 Azure 雲端操作員的堆疊中的 VM。"
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
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="2061c-103">在 Azure Stack 中建立測試虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2061c-103">Create a test virtual machine in Azure Stack</span></span>
<span data-ttu-id="2061c-104">雲端操作員，您可以建立測試虛擬機器 toovalidate Azure 堆疊部署。</span><span class="sxs-lookup"><span data-stu-id="2061c-104">As a cloud operator, you can create a test virtual machine toovalidate your Azure Stack deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="2061c-105">您可以佈建虛擬機器之前，您必須[新增 hello Windows Server 2016 Evaluation 映像 toohello Azure 堆疊 marketplace](azure-stack-add-default-image.md)。</span><span class="sxs-lookup"><span data-stu-id="2061c-105">Before you can provision virtual machines, you must [add hello Windows Server 2016 Evaluation image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="2061c-106">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2061c-106">Create a virtual machine</span></span>
1. <span data-ttu-id="2061c-107">Hello Azure 堆疊開發套件在主機上，[登入](azure-stack-connect-azure-stack.md)toohello 管理員入口網站 (`https://adminportal.local.azurestack.external`)，然後按一下**新增** > **計算** > **評估版的 Windows Server 2016 資料中心** > **建立**。</span><span class="sxs-lookup"><span data-stu-id="2061c-107">On hello Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) toohello administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="2061c-108">在 hello**基本概念**刀鋒視窗中，輸入**名稱**，**使用者名稱**，和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="2061c-108">In hello **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="2061c-109">選擇 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="2061c-109">Choose a **Subscription**.</span></span> <span data-ttu-id="2061c-110">建立 資源群組，或選取現有的資源群組，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="2061c-110">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="2061c-111">在 hello**大小選擇 「**刀鋒視窗中，按一下**標準 A1**，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="2061c-111">In hello **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="2061c-112">在 hello**設定**刀鋒視窗中，接受 hello 預設值，並按一下**確定**</span><span class="sxs-lookup"><span data-stu-id="2061c-112">In hello **Settings** blade, accept hello defaults and click **OK**</span></span>
5. <span data-ttu-id="2061c-113">在 hello**摘要**刀鋒視窗中，按一下 **確定**toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2061c-113">In hello **Summary** blade, click **OK** toocreate hello virtual machine.</span></span>  
6. <span data-ttu-id="2061c-114">toosee 新的虛擬機器，按一下 **所有資源**，然後搜尋 hello 虛擬機器，然後按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="2061c-114">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="2061c-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2061c-115">Next steps</span></span>
[<span data-ttu-id="2061c-116">使用 Azure 堆疊中的 hello 系統管理員和使用者入口網站</span><span class="sxs-lookup"><span data-stu-id="2061c-116">Using hello administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
