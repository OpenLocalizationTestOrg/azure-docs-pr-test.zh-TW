---
title: "Multi-Geo 說明文件 | Microsoft Docs"
description: "了解如何在美國中南部 (SCUS) Azure 區域以外的 Azure 區域中建立工作區並發佈 Web 服務。"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="35b9b-103">Multi-Geo 說明文件</span><span class="sxs-lookup"><span data-stu-id="35b9b-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="35b9b-104">本文將說明如何在不同的 Azure 區域中建立工作區及發佈 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="35b9b-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="35b9b-105">[依區域的 Azure 產品頁面](https://azure.microsoft.com/en-us/regions/services/)會列出可以使用 Azure Machine Learning 的區域。</span><span class="sxs-lookup"><span data-stu-id="35b9b-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="35b9b-106">建立工作區</span><span class="sxs-lookup"><span data-stu-id="35b9b-106">Create a workspace</span></span>
1. <span data-ttu-id="35b9b-107">登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="35b9b-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="35b9b-108">按一下 [+ 新增] > [資料服務] > [機器學習服務] > [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="35b9b-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="35b9b-109">在 [位置] 選取另一個區域，例如 [東南亞]。</span><span class="sxs-lookup"><span data-stu-id="35b9b-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="35b9b-110">![Multi-Geo 說明影像 1][1]</span><span class="sxs-lookup"><span data-stu-id="35b9b-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="35b9b-111">選取工作區，然後按一下 [登入 ML Studio] 。</span><span class="sxs-lookup"><span data-stu-id="35b9b-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="35b9b-112">![Multi-Geo 說明影像 2][2]</span><span class="sxs-lookup"><span data-stu-id="35b9b-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="35b9b-113">您現在已於其他地區中建立工作區，您可如同任何其他工作區一樣使用。</span><span class="sxs-lookup"><span data-stu-id="35b9b-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="35b9b-114">若要切換工作區，請查看您螢幕的右上方。</span><span class="sxs-lookup"><span data-stu-id="35b9b-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="35b9b-115">按一下下拉式清單，選取 [區域]，然後選取 [工作區]。</span><span class="sxs-lookup"><span data-stu-id="35b9b-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="35b9b-116">其中每一項都位於該工作區區域。</span><span class="sxs-lookup"><span data-stu-id="35b9b-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="35b9b-117">例如，所有已從工作區建立的 Web 服務會與工作區位於相同區域。</span><span class="sxs-lookup"><span data-stu-id="35b9b-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="35b9b-118">![Multi-Geo 說明影像 3][3]</span><span class="sxs-lookup"><span data-stu-id="35b9b-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="35b9b-119">從 [資源庫] 開啟實驗</span><span class="sxs-lookup"><span data-stu-id="35b9b-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="35b9b-120">如果從 [資源庫] 開啟實驗，您也可以選取要複製實驗的目標區域。</span><span class="sxs-lookup"><span data-stu-id="35b9b-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Multi-Geo 說明影像 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="35b9b-122">Web 服務管理</span><span class="sxs-lookup"><span data-stu-id="35b9b-122">Web service management</span></span>
<span data-ttu-id="35b9b-123">若要以程式設計方式管理 Web 服務，例如重新訓練、使用特定地區的地址：</span><span class="sxs-lookup"><span data-stu-id="35b9b-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="35b9b-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="35b9b-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="35b9b-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="35b9b-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="35b9b-126">注意事項</span><span class="sxs-lookup"><span data-stu-id="35b9b-126">Things to note</span></span>
1. <span data-ttu-id="35b9b-127">您只能以這樣的方式複製屬於相同區域工作區之間的實驗。</span><span class="sxs-lookup"><span data-stu-id="35b9b-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="35b9b-128">如果您需要在不同區域中跨工作區複製實驗，您可以使用 [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) 來完成。</span><span class="sxs-lookup"><span data-stu-id="35b9b-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="35b9b-129">另一個解決方法是使用未列出的模式將實驗發佈至組件庫，然後在其他區域的工作區中開啟。</span><span class="sxs-lookup"><span data-stu-id="35b9b-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="35b9b-130">區域選取器一次只會顯示一個區域的工作區。</span><span class="sxs-lookup"><span data-stu-id="35b9b-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="35b9b-131">免費工作區或 [來賓存取] \(匿名) 工作區會在美國中南部建立並裝載。</span><span class="sxs-lookup"><span data-stu-id="35b9b-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="35b9b-132">從位於東南亞的工作區部署的 Web 服務也會裝載於東南亞。</span><span class="sxs-lookup"><span data-stu-id="35b9b-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="35b9b-133">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="35b9b-133">More information</span></span>
<span data-ttu-id="35b9b-134">您可在 [Azure Machine Learning 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="35b9b-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
