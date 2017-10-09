---
title: "aaaMulti 地理說明 」 文件 |Microsoft 文件"
description: "深入了解如何 toocreate 工作區和 hello 南中央 United States (SCUS) 與不同 Azure 區域中發佈 web 服務的 Azure 區域。"
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="c443c-103">Multi-Geo 說明文件</span><span class="sxs-lookup"><span data-stu-id="c443c-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="c443c-104">本文將說明如何在不同的 Azure 區域中建立工作區及發佈 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c443c-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="c443c-105">hello[逐頁地區的 Azure 產品](https://azure.microsoft.com/en-us/regions/services/)列出 Azure Machine Learning 使用的地區。</span><span class="sxs-lookup"><span data-stu-id="c443c-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="c443c-106">建立工作區</span><span class="sxs-lookup"><span data-stu-id="c443c-106">Create a workspace</span></span>
1. <span data-ttu-id="c443c-107">登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="c443c-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="c443c-108">按一下 [+ 新增] > [資料服務] > [機器學習服務] > [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="c443c-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="c443c-109">在 [位置] 選取另一個區域，例如 [東南亞]。</span><span class="sxs-lookup"><span data-stu-id="c443c-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="c443c-110">![Multi-Geo 說明影像 1][1]</span><span class="sxs-lookup"><span data-stu-id="c443c-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="c443c-111">選取 [hello] 工作區，然後再按一下**登入 tooML Studio**。</span><span class="sxs-lookup"><span data-stu-id="c443c-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="c443c-112">![Multi-Geo 說明影像 2][2]</span><span class="sxs-lookup"><span data-stu-id="c443c-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="c443c-113">您現在已於其他地區中建立工作區，您可如同任何其他工作區一樣使用。</span><span class="sxs-lookup"><span data-stu-id="c443c-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="c443c-114">tooswitch 之間工作區中，尋找 toohello 右上角螢幕。</span><span class="sxs-lookup"><span data-stu-id="c443c-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="c443c-115">按一下 hello 下拉式清單中，選取 hello 區域，然後選取 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="c443c-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="c443c-116">所有項目是本機 toohello 工作區的區域。</span><span class="sxs-lookup"><span data-stu-id="c443c-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="c443c-117">例如，所有從工作區中建立 web 服務會的 hello 位於相同的區域 hello 工作區中。</span><span class="sxs-lookup"><span data-stu-id="c443c-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="c443c-118">![Multi-Geo 說明影像 3][3]</span><span class="sxs-lookup"><span data-stu-id="c443c-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="c443c-119">從 [資源庫] 開啟實驗</span><span class="sxs-lookup"><span data-stu-id="c443c-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="c443c-120">如果您從組件庫開啟實驗，您也可以選取您想要的 toocopy hello 實驗的區域。</span><span class="sxs-lookup"><span data-stu-id="c443c-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Multi-Geo 說明影像 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="c443c-122">Web 服務管理</span><span class="sxs-lookup"><span data-stu-id="c443c-122">Web service management</span></span>
<span data-ttu-id="c443c-123">tooprogrammatically 會管理 web 服務，例如重新定型使用 hello 特定地區的地址：</span><span class="sxs-lookup"><span data-stu-id="c443c-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="c443c-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="c443c-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="c443c-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="c443c-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="c443c-126">項目 toonote</span><span class="sxs-lookup"><span data-stu-id="c443c-126">Things toonote</span></span>
1. <span data-ttu-id="c443c-127">您僅能複製實驗工作區屬於 toohello 之間相同區域這種方式。</span><span class="sxs-lookup"><span data-stu-id="c443c-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="c443c-128">如果您需要 toocopy 實驗跨越不同地區中的工作區，您可以使用 hello [PowerShell](http://aka.ms/amlps) commandlet [*複製 AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish 的。</span><span class="sxs-lookup"><span data-stu-id="c443c-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="c443c-129">另一個解決方法是至圖庫 toopublish hello 實驗未列出的模式，然後開啟它 hello 工作區中 hello 從其他區域。</span><span class="sxs-lookup"><span data-stu-id="c443c-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="c443c-130">hello 區域選取器只會顯示一個區域的工作區，一次。</span><span class="sxs-lookup"><span data-stu-id="c443c-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="c443c-131">免費工作區或 [來賓存取] \(匿名) 工作區會在美國中南部建立並裝載。</span><span class="sxs-lookup"><span data-stu-id="c443c-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="c443c-132">從位於東南亞的工作區部署的 Web 服務也會裝載於東南亞。</span><span class="sxs-lookup"><span data-stu-id="c443c-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="c443c-133">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c443c-133">More information</span></span>
<span data-ttu-id="c443c-134">提出 hello [Azure Machine Learning 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning)。</span><span class="sxs-lookup"><span data-stu-id="c443c-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
