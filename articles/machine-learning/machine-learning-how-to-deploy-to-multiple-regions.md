---
title: "aaaHow toodeploy Web 服務 toomultiple 區域 |Microsoft 文件"
description: "步驟 toodeploy （複製） 新的 Web 服務 tooother 區域。"
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
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="1ea5a-103">如何 toodeploy Web 服務 toomultiple 區域</span><span class="sxs-lookup"><span data-stu-id="1ea5a-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="1ea5a-104">hello 新 Azure Web 服務可讓您 tooeasily 部署 web 服務 toomultiple 區域，而不需要多個訂用帳戶或工作區。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="1ea5a-105">定價是區域特定，因此您必須定義每個區域中，您將部署 hello web 服務的計費方案。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="1ea5a-106">toocreate 另一個區域中的計畫</span><span class="sxs-lookup"><span data-stu-id="1ea5a-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="1ea5a-107">登入 [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="1ea5a-108">按一下 hello**計劃**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="1ea5a-109">在 hello 計劃，透過檢視頁面上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="1ea5a-110">從 hello**訂用帳戶**下拉式清單中，選取 hello 訂用帳戶中的 hello 將位於新的計劃。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="1ea5a-111">從 hello**區域**下拉式清單中，選取 hello 新計劃的區域。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="1ea5a-112">hello 所選區域的 hello 計畫] 選項會顯示在 [hello**計劃選項**hello 頁面區段。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="1ea5a-113">從 hello**資源群組**下拉式清單中，選取資源群組 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="1ea5a-114">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="1ea5a-115">在**計劃名稱**類型 hello hello 計劃名稱。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="1ea5a-116">在下**計劃選項**，按一下 hello hello 新方案的計費層級。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="1ea5a-117">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="1ea5a-118">部署的 hello web 服務 tooanother 區域</span><span class="sxs-lookup"><span data-stu-id="1ea5a-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="1ea5a-119">按一下 hello **Web 服務**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="1ea5a-120">選取您要部署 tooa 新區域的 Web 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="1ea5a-121">按一下 [複製] 。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-121">Click **Copy**.</span></span>
4. <span data-ttu-id="1ea5a-122">在**Web 服務名稱**，輸入 hello web 服務的新名稱。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="1ea5a-123">在**Web 服務描述**，輸入 hello web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="1ea5a-124">從 hello**訂用帳戶**下拉式清單中，選取 hello 訂用帳戶中的 hello 將位於新的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="1ea5a-125">從 hello**資源群組**下拉式清單中，選取資源群組 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="1ea5a-126">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="1ea5a-127">從 hello**區域**下拉式清單中，選取 hello 哪些 toodeploy hello web 服務中的區域。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="1ea5a-128">從 hello**儲存體帳戶**下拉式清單中，選取儲存體帳戶中哪些 toostore hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="1ea5a-129">從 hello**價格計劃**下拉式清單中，選取您選取在步驟 8 中的 hello 區域中的計劃。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="1ea5a-130">按一下 [複製] 。</span><span class="sxs-lookup"><span data-stu-id="1ea5a-130">Click **Copy**.</span></span>

