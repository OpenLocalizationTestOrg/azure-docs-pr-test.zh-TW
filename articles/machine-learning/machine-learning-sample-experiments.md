---
title: "aaaCopy 機器學習的實驗範例-Azure |Microsoft 文件"
description: "了解如何 toouse 範例機器學習實驗 toocreate 與 Cortana 智慧組件庫 Microsoft Azure 機器學習新的實驗。"
keywords: "機器學習服務範例, 範例實驗, 機器學習服務範例"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 555f05cf9af2040d1703707f7583396d5da9f156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-example-experiments-toocreate-new-machine-learning-experiments"></a><span data-ttu-id="73388-104">複製範例實驗 toocreate 新的機器學習實驗</span><span class="sxs-lookup"><span data-stu-id="73388-104">Copy example experiments toocreate new machine learning experiments</span></span>
<span data-ttu-id="73388-105">了解如何利用範例 toostart 實驗從[Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/)而不是從頭開始建立機器學習實驗。</span><span class="sxs-lookup"><span data-stu-id="73388-105">Learn how toostart with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="73388-106">您可以使用您自己的機器學習解決方案 hello 範例 toobuild。</span><span class="sxs-lookup"><span data-stu-id="73388-106">You can use hello examples toobuild your own machine learning solution.</span></span>

<span data-ttu-id="73388-107">hello 組件庫的範例實驗 hello Microsoft Azure Machine Learning 小組與 hello Machine Learning 社群所共用的範例。</span><span class="sxs-lookup"><span data-stu-id="73388-107">hello gallery has example experiments by hello Microsoft Azure Machine Learning team as well as examples shared by hello Machine Learning community.</span></span> <span data-ttu-id="73388-108">您也可以提出有關實驗的問題或張貼意見。</span><span class="sxs-lookup"><span data-stu-id="73388-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="73388-109">toosee toouse hello 圖庫、 如何監看 hello 3 分鐘的影片[複製其他人工作 toodo 資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md)hello 系列[為初學者所設計的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)。</span><span class="sxs-lookup"><span data-stu-id="73388-109">toosee how toouse hello gallery, watch hello 3-minute video [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from hello series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-toocopy-in-cortana-intelligence-gallery"></a><span data-ttu-id="73388-110">在 Cortana 智慧組件庫中尋找實驗 toocopy</span><span class="sxs-lookup"><span data-stu-id="73388-110">Find an experiment toocopy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="73388-111">toosee 哪些實驗都可用，請移 toohello[圖庫](https://gallery.cortanaintelligence.com/)按一下**實驗**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="73388-111">toosee what experiments are available, go toohello [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at hello top of hello page.</span></span>

### <a name="find-hello-newest-or-most-popular-experiments"></a><span data-ttu-id="73388-112">Hello 尋找最新或最受歡迎的實驗</span><span class="sxs-lookup"><span data-stu-id="73388-112">Find hello newest or most popular experiments</span></span>
<span data-ttu-id="73388-113">這個頁面上，您可以看到**最近新增**實驗或在 toolook 捲動**什麼是最受歡迎**或最新 hello**熱門 Microsoft 實驗**。</span><span class="sxs-lookup"><span data-stu-id="73388-113">On this page, you can see **Recently added** experiments, or scroll down toolook at **What's popular** or hello latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="73388-114">尋找符合特定需求的實驗</span><span class="sxs-lookup"><span data-stu-id="73388-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="73388-115">所有 toobrowse 都實驗：</span><span class="sxs-lookup"><span data-stu-id="73388-115">toobrowse all experiments:</span></span>

1. <span data-ttu-id="73388-116">按一下**全部瀏覽**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="73388-116">Click **Browse all** at hello top of hello page.</span></span>
2. <span data-ttu-id="73388-117">左側 hello，底下**微調**在 hello**類別**區段中，選取**實驗**toosee 所有 hello 中的實驗 hello 組件庫。</span><span class="sxs-lookup"><span data-stu-id="73388-117">On hello left-hand side, under **Refine by** in hello **Categories** section, select **Experiment** toosee all hello experiments in hello Gallery.</span></span>
3. <span data-ttu-id="73388-118">有幾種不同方式可以找到符合您需求的實驗︰</span><span class="sxs-lookup"><span data-stu-id="73388-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="73388-119">**選取左側 hello 的篩選條件。**</span><span class="sxs-lookup"><span data-stu-id="73388-119">**Select filters on hello left.**</span></span> <span data-ttu-id="73388-120">比方說，使用以 PCA 為基礎的異常偵測演算法 toobrowse 實驗： 與**實驗**底下選取**類別**，按一下 **全部顯示**。</span><span class="sxs-lookup"><span data-stu-id="73388-120">For example, toobrowse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="73388-121">然後，在 [使用的演算法] 之下，選擇 [以 PCA 為基礎的異常偵測]。</span><span class="sxs-lookup"><span data-stu-id="73388-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="73388-122">
     ![選取篩選器](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="73388-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="73388-123">**使用 hello [搜尋] 方塊。**</span><span class="sxs-lookup"><span data-stu-id="73388-123">**Use hello search box.**</span></span> <span data-ttu-id="73388-124">比方說，toofind 實驗造成相關的 microsoft toodigit 辨識使用 二級支援向量機器演算法，hello 搜尋 方塊中輸入 「 數字辨識 」。</span><span class="sxs-lookup"><span data-stu-id="73388-124">For example, toofind experiments contributed by Microsoft related toodigit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in hello search box.</span></span> <span data-ttu-id="73388-125">然後，選取 hello 篩選**實驗**， **Microsoft 內容只**，和**二級支援向量機器**:</span><span class="sxs-lookup"><span data-stu-id="73388-125">Then, select hello filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="73388-126">
     ![使用 hello [搜尋] 方塊](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="73388-126">
![Use hello search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="73388-127">按一下 詳細資訊，請參閱實驗 toolearn。</span><span class="sxs-lookup"><span data-stu-id="73388-127">Click an experiment toolearn more about it.</span></span>
5. <span data-ttu-id="73388-128">toorun 及/或修改 hello 實驗，請按一下**在 Studio 中開啟**hello 實驗頁面上。</span><span class="sxs-lookup"><span data-stu-id="73388-128">toorun and/or modify hello experiment, click **Open in Studio** on hello experiment's page.</span></span> <br></br>

    ![範例實驗](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="73388-130">當您開啟實驗 Machine Learning Studio 中的 hello 第一次時，您可以免費試用或購買 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="73388-130">When you open an experiment in Machine Learning Studio for hello first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="73388-131">深入了解 hello Machine Learning Studio 免費試用與付費服務</span><span class="sxs-lookup"><span data-stu-id="73388-131">Learn about hello Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="73388-132">使用範例作為範本來建立新實驗</span><span class="sxs-lookup"><span data-stu-id="73388-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="73388-133">您也可以使用資源庫範例作為範本，在 Machine Learning Studio 中建立新實驗。</span><span class="sxs-lookup"><span data-stu-id="73388-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="73388-134">登入您的 Microsoft 帳戶認證 toohello [Studio](https://studio.azureml.net)，然後按一下**新增**toocreate 實驗。</span><span class="sxs-lookup"><span data-stu-id="73388-134">Sign in with your Microsoft account credentials toohello [Studio](https://studio.azureml.net), and then click **New** toocreate an experiment.</span></span>
2. <span data-ttu-id="73388-135">瀏覽 hello 範例內容，並按一下其中一個。</span><span class="sxs-lookup"><span data-stu-id="73388-135">Browse through hello example content and click one.</span></span>

<span data-ttu-id="73388-136">建立新的實驗使用 hello 範例實驗，做為範本 Machine Learning Studio 工作區中。</span><span class="sxs-lookup"><span data-stu-id="73388-136">A new experiment is created in your Machine Learning Studio workspace using hello example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73388-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73388-137">Next steps</span></span>
* [<span data-ttu-id="73388-138">從各種資源匯入資料</span><span class="sxs-lookup"><span data-stu-id="73388-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="73388-139">Machine Learning 中的 hello R 語言的快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="73388-139">Quickstart tutorial for hello R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="73388-140">部署 Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="73388-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
