---
title: "在 Azure Stack 中建立方案 | Microsoft Docs"
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
ms.openlocfilehash: 30759dca746fd7fd02653556cb105f419f5bf854
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="8e18a-103">在 Azure Stack 中建立方案</span><span class="sxs-lookup"><span data-stu-id="8e18a-103">Create a plan in Azure Stack</span></span>

<span data-ttu-id="8e18a-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="8e18a-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="8e18a-105">[方案](azure-stack-key-features.md)結合一或多項服務。</span><span class="sxs-lookup"><span data-stu-id="8e18a-105">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="8e18a-106">身為提供者的您可以為使用者製作方案。</span><span class="sxs-lookup"><span data-stu-id="8e18a-106">As a provider, you can create plans to offer to your users.</span></span> <span data-ttu-id="8e18a-107">使用者接著即可訂閱您的供應項目，以使用其中的方案與服務。</span><span class="sxs-lookup"><span data-stu-id="8e18a-107">In turn, your users subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="8e18a-108">此範例說明如何建立一個包含計算、網路及儲存體資源提供者的方案。</span><span class="sxs-lookup"><span data-stu-id="8e18a-108">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="8e18a-109">此方案可讓訂閱者佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e18a-109">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="8e18a-110">登入 Azure Stack 系統管理員入口網站 (https://adminportal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="8e18a-110">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="8e18a-111">輸入您在[執行 PowerShell 指令碼](azure-stack-run-powershell-script.md)一節步驟 5 中所建立帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="8e18a-111">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="8e18a-112">若要建立使用者可訂閱的方案和供應項目，請按一下 [新增] > [租用戶供應項目 + 方案] > [方案]。</span><span class="sxs-lookup"><span data-stu-id="8e18a-112">To create a plan and offer that users can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="8e18a-113">在 [新的方案] 刀鋒視窗中，填寫 [顯示名稱] 與 [資源名稱]。</span><span class="sxs-lookup"><span data-stu-id="8e18a-113">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="8e18a-114">[顯示名稱] 是使用者看到的方案易記名稱。</span><span class="sxs-lookup"><span data-stu-id="8e18a-114">The Display Name is the plan's friendly name that users see.</span></span> <span data-ttu-id="8e18a-115">只有系統管理員可以看到「資源名稱」。</span><span class="sxs-lookup"><span data-stu-id="8e18a-115">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="8e18a-116">它是系統管理員用來將方案當作 Azure Resource Manager 資源來使用時的名稱。</span><span class="sxs-lookup"><span data-stu-id="8e18a-116">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="8e18a-117">建立新的 [資源群組]或選取現有的資源群組，以作為方案的容器。</span><span class="sxs-lookup"><span data-stu-id="8e18a-117">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="8e18a-118">按一下 服務，選取 Microsoft.Compute、Microsoft.Network 及 Microsoft.Storage，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="8e18a-118">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="8e18a-119">依序按一下 [配額]、[Microsoft.Storage (本機)]，然後選取預設配額，或按一下 [建立新的配額] 來自訂配額。</span><span class="sxs-lookup"><span data-stu-id="8e18a-119">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="8e18a-120">如果您要建立新配額，請輸入配額名稱 > 設定配額值 > 按一下 [確定] > 按一下新配額的名稱。</span><span class="sxs-lookup"><span data-stu-id="8e18a-120">If you're creating a new quota, enter a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="8e18a-121">按一下 [Microsoft.Network (本機)]，然後選取預設配額，或按一下 [建立新的配額] 來自訂配額。</span><span class="sxs-lookup"><span data-stu-id="8e18a-121">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="8e18a-122">如果您要建立新配額，請輸入配額名稱 > 設定配額值 > 按一下 [確定] > 按一下新配額的名稱。</span><span class="sxs-lookup"><span data-stu-id="8e18a-122">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="8e18a-123">按一下 [Microsoft.Compute (本機)]，然後選取預設配額，或按一下 [建立新的配額] 來自訂配額。</span><span class="sxs-lookup"><span data-stu-id="8e18a-123">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="8e18a-124">如果您要建立新配額，請輸入配額名稱 > 設定配額值 > 按一下 [確定] > 按一下新配額的名稱。</span><span class="sxs-lookup"><span data-stu-id="8e18a-124">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="8e18a-125">在 [配額] 刀鋒視窗中，按一下 [確定]，然後在 [新的方案] 刀鋒視窗中，按一下 [建立] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="8e18a-125">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="8e18a-126">若要查看您的新方案，請按一下 [所有資源]，然後搜尋該方案並按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="8e18a-126">To see your new plan, click **All resources**, then search for the plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="8e18a-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e18a-127">Next steps</span></span>
[<span data-ttu-id="8e18a-128">建立優惠</span><span class="sxs-lookup"><span data-stu-id="8e18a-128">Create an offer</span></span>](azure-stack-create-offer.md)
