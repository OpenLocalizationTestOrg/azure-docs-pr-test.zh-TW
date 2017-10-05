---
title: "如何將 Web 服務部署到多個區域 | Microsoft Docs"
description: "將新的 Web 服務部署 (複製) 到其他區域的步驟。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="401d7-103">如何將 Web 服務部署到多個區域</span><span class="sxs-lookup"><span data-stu-id="401d7-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="401d7-104">新式 Azure Web 服務可讓您輕鬆地將 Web 服務部署到多個區域，而不需要多個訂用帳戶或工作區。</span><span class="sxs-lookup"><span data-stu-id="401d7-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="401d7-105">價格依照區域而有所不同，因此您必須為您要部署 Web 服務的每個區域定義計費方案。</span><span class="sxs-lookup"><span data-stu-id="401d7-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="401d7-106">在其他區域中建立方案</span><span class="sxs-lookup"><span data-stu-id="401d7-106">To create a plan in another region</span></span>
1. <span data-ttu-id="401d7-107">登入 [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="401d7-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="401d7-108">按一下 [方案]  功能表選項。</span><span class="sxs-lookup"><span data-stu-id="401d7-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="401d7-109">在方案概觀頁面上，按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="401d7-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="401d7-110">從 [訂用帳戶]  下拉式清單中，選取新方案所在的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="401d7-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="401d7-111">從 [區域]  下拉式清單中，選取新方案的區域。</span><span class="sxs-lookup"><span data-stu-id="401d7-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="401d7-112">所選區域的「方案選項」會顯示在頁面的 [方案選項]  區段中。</span><span class="sxs-lookup"><span data-stu-id="401d7-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="401d7-113">從 [資源群組]  下拉式清單中，選取方案的資源群組。</span><span class="sxs-lookup"><span data-stu-id="401d7-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="401d7-114">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="401d7-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="401d7-115">在 [方案名稱]  中，輸入方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="401d7-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="401d7-116">在 [方案選項] 下，按一下新方案的計費層級。</span><span class="sxs-lookup"><span data-stu-id="401d7-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="401d7-117">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="401d7-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="401d7-118">將 Web 服務部署到另一個區域</span><span class="sxs-lookup"><span data-stu-id="401d7-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="401d7-119">按一下 [Web 服務]  功能表選項。</span><span class="sxs-lookup"><span data-stu-id="401d7-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="401d7-120">選取您要部署到新區域的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="401d7-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="401d7-121">按一下 [複製] 。</span><span class="sxs-lookup"><span data-stu-id="401d7-121">Click **Copy**.</span></span>
4. <span data-ttu-id="401d7-122">在 [Web 服務名稱] 中，輸入 Web 服務的新名稱。</span><span class="sxs-lookup"><span data-stu-id="401d7-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="401d7-123">在 [Web 服務描述] 中，輸入 Web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="401d7-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="401d7-124">從 [訂用帳戶]  下拉式清單中，選取新 Web 服務所在的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="401d7-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="401d7-125">從 [資源群組]  下拉式清單中，選取 Web 服務的資源群組。</span><span class="sxs-lookup"><span data-stu-id="401d7-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="401d7-126">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="401d7-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="401d7-127">從 [區域]  下拉式清單中，選取要部署 Web 服務的區域。</span><span class="sxs-lookup"><span data-stu-id="401d7-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="401d7-128">從 [儲存體帳戶]  下拉式清單中，選取要儲存 Web 服務的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="401d7-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="401d7-129">從 [價格方案]  下拉式清單中，在您在步驟 8 選取的區域中選取方案。</span><span class="sxs-lookup"><span data-stu-id="401d7-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="401d7-130">按一下 [複製] 。</span><span class="sxs-lookup"><span data-stu-id="401d7-130">Click **Copy**.</span></span>

