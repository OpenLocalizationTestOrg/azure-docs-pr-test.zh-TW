---
title: "aaaCreate Azure 堆疊中的計劃 |Microsoft 文件"
description: "身為雲端系統管理員，您可以建立可供訂閱者佈建虛擬機器的方案。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="018cb-103">在 Azure Stack 中建立方案</span><span class="sxs-lookup"><span data-stu-id="018cb-103">Create a plan in Azure Stack</span></span>
<span data-ttu-id="018cb-104">[方案](azure-stack-key-features.md)結合一或多項服務。</span><span class="sxs-lookup"><span data-stu-id="018cb-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="018cb-105">做為提供者，您可以建立計劃 toooffer tooyour 租用戶。</span><span class="sxs-lookup"><span data-stu-id="018cb-105">As a provider, you can create plans toooffer tooyour tenants.</span></span> <span data-ttu-id="018cb-106">接著，您的租用戶訂閱 tooyour 優惠 toouse hello 計劃和它們所包含的服務。</span><span class="sxs-lookup"><span data-stu-id="018cb-106">In turn, your tenants subscribe tooyour offers toouse hello plans and services they include.</span></span> <span data-ttu-id="018cb-107">此範例將示範如何 toocreate 包含計劃 hello 運算、 網路和儲存體資源提供者。</span><span class="sxs-lookup"><span data-stu-id="018cb-107">This example shows you how toocreate a plan that includes hello compute, network, and storage resource providers.</span></span> <span data-ttu-id="018cb-108">這個計劃可讓訂閱者 hello 能力 tooprovision 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="018cb-108">This plan gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="018cb-109">登入 toohello 堆疊 Azure 管理員入口網站 (https://adminportal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="018cb-109">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="018cb-110">輸入您在步驟 5 的 hello 期間建立的 hello 帳戶 hello 認證[執行 hello PowerShell 指令碼](azure-stack-run-powershell-script.md)> 一節。</span><span class="sxs-lookup"><span data-stu-id="018cb-110">Enter hello credentials for hello account that you created during step 5 of hello [Run hello PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="018cb-111">toocreate 計劃和提供租用戶可以訂閱，按一下**新增** > **租用戶提供 + 計劃** > **計劃**。</span><span class="sxs-lookup"><span data-stu-id="018cb-111">toocreate a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="018cb-112">在 hello**新增計劃**刀鋒視窗中，填滿**顯示名稱**和**資源名稱**。</span><span class="sxs-lookup"><span data-stu-id="018cb-112">In hello **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="018cb-113">hello 顯示名稱是租用戶中看到的 hello 計劃的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="018cb-113">hello Display Name is hello plan's friendly name that tenants see.</span></span> <span data-ttu-id="018cb-114">只有 hello 管理員可以看到 hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="018cb-114">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="018cb-115">它的 hello 名稱，系統管理員 」 搭配 toowork hello 計劃做為 Azure 資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="018cb-115">It's hello name that admins use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="018cb-116">建立新**資源群組**，或選取現有的我的最愛，做為 hello 計劃的容器。</span><span class="sxs-lookup"><span data-stu-id="018cb-116">Create a new **Resource Group**, or select an existing one, as a container for hello plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="018cb-117">按一下 服務，選取 Microsoft.Compute、Microsoft.Network 及 Microsoft.Storage，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="018cb-117">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="018cb-118">按一下**配額**，按一下  **Microsoft.Storage （本機）**，並接著任一選取 hello 預設配額，或按一下**建立新的配額**toocustomize hello 配額。</span><span class="sxs-lookup"><span data-stu-id="018cb-118">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="018cb-119">如果您要建立新的配額，請輸入 hello 配額的名稱 > 設定 hello 配額值 > 按**確定**> 按一下 hello hello 新配額名稱。</span><span class="sxs-lookup"><span data-stu-id="018cb-119">If you're creating a new quota, enter a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="018cb-120">按一下**Microsoft.Network （本機）**，並接著任一選取 hello 預設配額，或按一下**建立新的配額**toocustomize hello 配額。</span><span class="sxs-lookup"><span data-stu-id="018cb-120">Click **Microsoft.Network (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="018cb-121">如果您要建立新的配額，請輸入 hello 配額的名稱 > 設定 hello 配額值 > 按**確定**> 按一下 hello hello 新配額名稱。</span><span class="sxs-lookup"><span data-stu-id="018cb-121">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="018cb-122">按一下**Microsoft.Compute （本機）**，並接著任一選取 hello 預設配額，或按一下**建立新的配額**toocustomize hello 配額。</span><span class="sxs-lookup"><span data-stu-id="018cb-122">Click **Microsoft.Compute (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="018cb-123">如果您要建立新的配額，請輸入 hello 配額的名稱 > 設定 hello 配額值 > 按**確定**> 按一下 hello hello 新配額名稱。</span><span class="sxs-lookup"><span data-stu-id="018cb-123">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="018cb-124">在 hello**配額**刀鋒視窗中，按一下**確定**，然後在 hello**新計劃**刀鋒視窗中，按一下**建立**toocreate hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="018cb-124">In hello **Quotas** blade, click **OK**, and then in hello **New Plan** blade, click **Create** toocreate hello plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="018cb-125">toosee 您新的計畫中，按一下 **所有資源**，然後搜尋 hello 計劃，然後按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="018cb-125">toosee your new plan, click **All resources**, then search for hello plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="018cb-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="018cb-126">Next steps</span></span>
[<span data-ttu-id="018cb-127">建立優惠</span><span class="sxs-lookup"><span data-stu-id="018cb-127">Create an offer</span></span>](azure-stack-create-offer.md)
