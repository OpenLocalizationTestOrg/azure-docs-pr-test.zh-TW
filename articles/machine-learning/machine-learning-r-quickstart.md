---
title: "機器學習的 R 語言 aaaQuickstart 教學課程 |Microsoft 文件"
description: "使用此 R 程式設計教學課程 tooget 啟動快速地使用 Azure Machine Learning Studio toocreate 預測的方案中的 hello R 語言。"
keywords: "快速入門,r 語言,r 程式設計語言,r 程式設計教學課程"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="7cf69-104">Azure Machine Learning 的 hello R 程式設計語言的快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="7cf69-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="7cf69-105">簡介</span><span class="sxs-lookup"><span data-stu-id="7cf69-105">Introduction</span></span>
<span data-ttu-id="7cf69-106">本快速入門教學課程可協助您快速開始使用 hello R 程式設計語言擴充 Azure 機器學習。</span><span class="sxs-lookup"><span data-stu-id="7cf69-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="7cf69-107">請遵循此 R 程式設計教學課程 toocreate、 測試及執行 Azure Machine Learning 中的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="7cf69-108">當您完成教學課程，您將使用 Azure Machine Learning 中的 hello R 語言來建立預測的完整解決方案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="7cf69-109">Microsoft Azure Machine Learning 包含許多功能強大的機器學習和資料操作模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="7cf69-110">hello 功能強大的 R 語言被描述為 hello 通用語言分析。</span><span class="sxs-lookup"><span data-stu-id="7cf69-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="7cf69-111">幸好，擴充 Azure Machine Learning 中的分析和資料操作，使用。這種組合提供 hello 延展性及容易部署的 Azure Machine Learning 的 hello 彈性和更深層的分析是。</span><span class="sxs-lookup"><span data-stu-id="7cf69-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="7cf69-112">預測和 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="7cf69-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="7cf69-113">預測是一個獲得廣泛採用且相當實用的分析方法。</span><span class="sxs-lookup"><span data-stu-id="7cf69-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="7cf69-114">常見用法預測銷售量的季節性的項目，決定最佳的存貨層級，toopredicting macroeconomic 變數範圍的內。</span><span class="sxs-lookup"><span data-stu-id="7cf69-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="7cf69-115">進行預測時通常是搭配時間序列模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="7cf69-116">時間序列資料是在其中 hello 值有時間索引的資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="7cf69-117">hello 時間索引可以是規則，例如每月或每隔一分鐘，或異常。</span><span class="sxs-lookup"><span data-stu-id="7cf69-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="7cf69-118">時間序列模型會根據時間序列資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-118">A time series model is based on time series data.</span></span> <span data-ttu-id="7cf69-119">hello R 程式設計語言包含彈性架構，時間序列資料的大量分析。</span><span class="sxs-lookup"><span data-stu-id="7cf69-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="7cf69-120">在本快速入門指南中，我們將使用加州乳製品產量和訂價資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="7cf69-121">此資料包括每月的數個日常用品 hello 生產和牛奶 fat、 基準商用 hello 價格的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="7cf69-122">使用 R 指令碼，以及此篇文章中的 hello 資料可以是[這裡下載][download]。</span><span class="sxs-lookup"><span data-stu-id="7cf69-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="7cf69-123">此資料已原本合成 hello 大學的威斯康辛 http://future.aae.wisc.edu/tab/production.html 在提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="7cf69-124">組織</span><span class="sxs-lookup"><span data-stu-id="7cf69-124">Organization</span></span>
<span data-ttu-id="7cf69-125">由於您學習如何 toocreate，測試並執行 hello Azure Machine Learning 環境中分析和資料操作 R 程式碼，我們會介紹幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="7cf69-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="7cf69-126">首先，我們將探討 hello hello Azure Machine Learning Studio 環境中使用 hello R 語言的基本概念。</span><span class="sxs-lookup"><span data-stu-id="7cf69-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="7cf69-127">然後我們會進行 toodiscussing 資料、 R 程式碼和 hello Azure Machine Learning 環境中的圖形 I/O 的各個層面。</span><span class="sxs-lookup"><span data-stu-id="7cf69-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="7cf69-128">然後將藉由建立針對資料清理和轉換程式碼建構 hello 我們的預測解決方案的第一個部分。</span><span class="sxs-lookup"><span data-stu-id="7cf69-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="7cf69-129">我們的資料準備，我們將會執行數個 hello 變數，在我們的資料集之間的 hello 相互關聯的分析。</span><span class="sxs-lookup"><span data-stu-id="7cf69-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="7cf69-130">最後，我們將針對牛奶產量建立季節性的時間序列預測模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="7cf69-131"><a id="mlstudio"></a>與 Machine Learning Studio 中的 R 語言互動</span><span class="sxs-lookup"><span data-stu-id="7cf69-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="7cf69-132">本節會帶領您完成與 hello Machine Learning Studio 環境中的 hello R 程式設計語言互動的一些基本概念。</span><span class="sxs-lookup"><span data-stu-id="7cf69-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="7cf69-133">hello R 語言提供功能強大的工具 toocreate 自訂分析和資料操作模組 hello Azure Machine Learning 環境中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="7cf69-134">我將使用 RStudio toodevelop、 測試和偵錯的 R 程式碼小的標尺上。</span><span class="sxs-lookup"><span data-stu-id="7cf69-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="7cf69-135">此程式碼是然後剪下和貼上到[執行 R 指令碼][ execute-r-script] Machine Learning Studio 準備 toorun 中的模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="7cf69-136">hello 執行 R 指令碼模組</span><span class="sxs-lookup"><span data-stu-id="7cf69-136">hello Execute R Script module</span></span>
<span data-ttu-id="7cf69-137">Machine Learning Studio 中，在 R 指令碼執行內 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-138">舉例來說，hello[執行 R 指令碼][ execute-r-script] Machine Learning Studio 中的模組以圖 1 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![R 程式設計語言： 選取 Machine Learning Studio 中的 hello 執行 R 指令碼模組][1]

<span data-ttu-id="7cf69-140">*圖 1。顯示選取的 hello 執行 R 指令碼模組 hello Machine Learning Studio 環境。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="7cf69-141">參照 tooFigure 1，讓我們看看一些使用 hello hello Machine Learning Studio 環境的 hello 關鍵部分[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="7cf69-142">hello 實驗中的 hello 模組會顯示 hello 中間窗格內。</span><span class="sxs-lookup"><span data-stu-id="7cf69-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="7cf69-143">包含視窗 tooview hello hello 右邊窗格上半部，並編輯您的 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="7cf69-144">hello 的右窗格的下半部顯示 hello 的某些屬性[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="7cf69-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="7cf69-145">按一下此窗格的 hello 適當點，您可以檢視 hello 錯誤和輸出記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cf69-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="7cf69-146">我們將當然，討論 hello[執行 R 指令碼][ execute-r-script]更詳細地在 hello 這份文件其餘部分。</span><span class="sxs-lookup"><span data-stu-id="7cf69-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="7cf69-147">使用複雜的 R 函式時，建議您在 RStudio 中進行編輯、測試及偵錯。</span><span class="sxs-lookup"><span data-stu-id="7cf69-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="7cf69-148">與進行任何軟體開發相同，請以累加方式擴充您的程式碼，並在小型的簡單測試案例上進行測試。</span><span class="sxs-lookup"><span data-stu-id="7cf69-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="7cf69-149">然後剪下並貼到 hello R 指令碼視窗中的 hello 的函式[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-150">這種方法可讓您 tooharness hello RStudio 整合式的開發環境 (IDE) 和 hello Azure Machine Learning 的電源。</span><span class="sxs-lookup"><span data-stu-id="7cf69-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="7cf69-151">執行 R 程式碼</span><span class="sxs-lookup"><span data-stu-id="7cf69-151">Execute R code</span></span>
<span data-ttu-id="7cf69-152">任何 R 中的程式碼 hello[執行 R 指令碼][ execute-r-script]當您按一下 hello 以執行 hello 實驗，就會執行模組**執行**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf69-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="7cf69-153">核取記號完成執行之後，會出現在 hello[執行 R 指令碼][ execute-r-script]圖示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="7cf69-154">Azure Machine Learning 的防禦型 R 編碼</span><span class="sxs-lookup"><span data-stu-id="7cf69-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="7cf69-155">如果您正在使用 Azure Machine Learning 為 Web 服務開發 R 程式碼，您應該明確地規劃程式碼將如何處理非預期的資料輸入和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7cf69-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="7cf69-156">toomaintain 求清楚明瞭，並未包含許多 hello 方式檢查或例外狀況處理中的大部分 hello 程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="7cf69-157">不過，隨著我們繼續進行，我將會提供您幾個使用 R 例外狀況處理功能的函式範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="7cf69-158">如果您需要更完整的處理方式的 R 例外狀況處理時，建議您閱讀 hello hello 活頁簿中所列的 Wickham 所適用的章節[附錄 B-進一步閱讀](#appendixb)。</span><span class="sxs-lookup"><span data-stu-id="7cf69-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="7cf69-159">在 Machine Learning Studio 中進行 R 程式碼偵錯和測試</span><span class="sxs-lookup"><span data-stu-id="7cf69-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="7cf69-160">tooreiterate，建議您測試和偵錯小型 RStudio 在標尺上的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="7cf69-161">不過，一些情況下，您必須在 hello 的 R 程式碼問題 tootrack[執行 R 指令碼][ execute-r-script]本身。</span><span class="sxs-lookup"><span data-stu-id="7cf69-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="7cf69-162">此外，它是很好的作法 toocheck 在 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="7cf69-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="7cf69-163">主要的 output.log 找到 hello 執行 R 程式碼並且在 hello Azure Machine Learning 平台上的輸出。</span><span class="sxs-lookup"><span data-stu-id="7cf69-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="7cf69-164">有些其他資訊會顯示在 error.log 中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="7cf69-165">如果發生錯誤 Machine Learning Studio 中執行 R 程式碼時，您的第一個採取的動作應該在 error.log toolook。</span><span class="sxs-lookup"><span data-stu-id="7cf69-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="7cf69-166">這個檔案可以包含有用的錯誤訊息 toohelp 您了解並修正錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7cf69-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="7cf69-167">tooview error.log，請按一下 [**檢視錯誤記錄檔**上 hello**屬性] 窗格**hello[執行 R 指令碼][ execute-r-script]包含 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="7cf69-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="7cf69-168">例如，執行下列 R 程式碼中的使用未定義變數 y 中的 hello[執行 R 指令碼][ execute-r-script]模組：</span><span class="sxs-lookup"><span data-stu-id="7cf69-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="7cf69-169">此程式碼無法 tooexecute，導致錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="7cf69-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="7cf69-170">按一下**檢視錯誤記錄檔**上 hello**屬性 窗格**產生 hello 顯示圖 2 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![錯誤訊息快顯][2]

<span data-ttu-id="7cf69-172">*圖 2.錯誤訊息快顯。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="7cf69-173">它看起來我們需要 toolook output.log toosee hello R 錯誤訊息中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="7cf69-174">按一下 hello[執行 R 指令碼][ execute-r-script] ，然後按一下hello**檢視 output.log** hello 上的項目**屬性] 窗格**toohello 權限。</span><span class="sxs-lookup"><span data-stu-id="7cf69-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="7cf69-175">新的瀏覽器視窗隨即開啟，並看 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="7cf69-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="7cf69-176">這則錯誤訊息包含意外狀況，並清楚地識別 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="7cf69-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="7cf69-177">tooinspect hello R 中的任何物件值，您可以列印這些值 toohello output.log 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="7cf69-178">hello 規則檢查物件的值基本上為 hello 相同如同互動式的 R 工作階段。</span><span class="sxs-lookup"><span data-stu-id="7cf69-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="7cf69-179">例如，如果您的一行輸入變數的名稱，hello 物件 hello 值會列印的 toohello output.log 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="7cf69-180">Machine Learning Studio 中的封裝</span><span class="sxs-lookup"><span data-stu-id="7cf69-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="7cf69-181">Azure Machine Learning 附有超過 350 個預先安裝的 R 語言封裝。</span><span class="sxs-lookup"><span data-stu-id="7cf69-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="7cf69-182">您可以使用下列程式碼中 hello hello[執行 R 指令碼][ execute-r-script]模組 tooretrieve hello 一份預先安裝套件。</span><span class="sxs-lookup"><span data-stu-id="7cf69-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="7cf69-183">如果您不要在 hello 時刻，以了解 hello 這段程式碼的最後一行，閱讀。</span><span class="sxs-lookup"><span data-stu-id="7cf69-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="7cf69-184">在這份文件其餘部分 hello 廣泛我們將討論在 hello Azure Machine Learning 環境中使用 R。</span><span class="sxs-lookup"><span data-stu-id="7cf69-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="7cf69-185">簡介 tooRStudio</span><span class="sxs-lookup"><span data-stu-id="7cf69-185">Introduction tooRStudio</span></span>
<span data-ttu-id="7cf69-186">RStudio 是廣泛使用的 IDE，如。我將使用 RStudio 編輯、 測試和偵錯的一些本快速入門指南中使用的 hello R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="7cf69-187">R 程式碼測試並準備好後，您只需剪下，並從 hello RStudio 編輯器貼入 Machine Learning Studio[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="7cf69-188">如果您沒有在桌面的電腦上安裝的 hello R 程式設計語言，建議您請立刻。</span><span class="sxs-lookup"><span data-stu-id="7cf69-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="7cf69-189">開放原始碼 R 語言的免費下載位於 hello 完整 R 封存網路 (CRAN) 在[http://www.r-project.org/](http://www.r-project.org/)。</span><span class="sxs-lookup"><span data-stu-id="7cf69-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="7cf69-190">有提供適用於 Windows、MacOS 及 Linux/UNIX 的下載項目。</span><span class="sxs-lookup"><span data-stu-id="7cf69-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="7cf69-191">選擇附近的鏡像，並依照 hello 下載指示進行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="7cf69-192">此外，CRAN 也包含大量實用的分析和資料操作封裝。</span><span class="sxs-lookup"><span data-stu-id="7cf69-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="7cf69-193">如果您是新 tooRStudio，您應該下載並安裝 hello 桌面版本。</span><span class="sxs-lookup"><span data-stu-id="7cf69-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="7cf69-194">您可以找到 RStudio Windows、 Mac OS 和 Linux/UNIX 會在下載 http://www.rstudio.com/products/RStudio/ hello。</span><span class="sxs-lookup"><span data-stu-id="7cf69-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="7cf69-195">請依照 hello tooinstall RStudio 提供您桌面的電腦上的指示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="7cf69-196">教學課程簡介 tooRStudio 位於 https://support.rstudio.com/hc/sections/200107586-Using-RStudio。</span><span class="sxs-lookup"><span data-stu-id="7cf69-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="7cf69-197">我在[附錄 A][appendixa] 中提供了一些使用 RStudio 的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="7cf69-198"><a id="scriptmodule"></a>取得資料移轉入和 hello 執行 R 指令碼模組</span><span class="sxs-lookup"><span data-stu-id="7cf69-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="7cf69-199">本節中，我們將討論如何您將資料傳入及傳出 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-200">我們將復 toohandle 各種資料型別讀取方式 hello 進出[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="7cf69-201">本節 hello 完整程式碼是您之前下載的 hello zip 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="7cf69-202">在 Machine Learning Studio 中載入和檢查資料</span><span class="sxs-lookup"><span data-stu-id="7cf69-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="7cf69-203"><a id="loading"></a>載入 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="7cf69-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="7cf69-204">我們一開始會載入 hello **csdairydata.csv** Azure Machine Learning Studio 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="7cf69-205">啟動 Azure Machine Learning Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="7cf69-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="7cf69-206">按一下**+ 新增**hello 在較低的螢幕，然後選取左**資料集**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="7cf69-207">選取**從本機檔案**，然後**瀏覽**tooselect hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="7cf69-208">請確定您已選取**一般 CSV 檔案具有標頭 (.csv)** hello hello 資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="7cf69-209">按一下 hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="7cf69-209">Click hello check mark.</span></span>
* <span data-ttu-id="7cf69-210">已上傳 hello 資料集之後，您應該看到 hello 新的資料集即可 hello**資料集** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7cf69-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="7cf69-211">建立實驗</span><span class="sxs-lookup"><span data-stu-id="7cf69-211">Create an experiment</span></span>
<span data-ttu-id="7cf69-212">現在我們有一些資料 Machine Learning Studio 中，我們需要 toocreate 實驗 toodo hello 分析。</span><span class="sxs-lookup"><span data-stu-id="7cf69-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="7cf69-213">按一下**+ 新增**在 hello 左下並選取**實驗**，然後**空白實驗**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="7cf69-214">您可以藉由選取，命名您的經驗，並修改 hello**上建立的實驗...** hello hello 頁頂端的標題。</span><span class="sxs-lookup"><span data-stu-id="7cf69-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="7cf69-215">例如，變更太**CA 香蕉分析**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="7cf69-216">Hello hello 實驗頁面的左側展開**儲存的資料集**，然後**我的資料集**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="7cf69-217">您應該會看見 hello **cadairydata.csv**您先前上傳。</span><span class="sxs-lookup"><span data-stu-id="7cf69-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="7cf69-218">拖放 hello **csdairydata.csv 資料集**到 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="7cf69-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="7cf69-219">在 hello**搜尋實驗項目**hello 頂端 hello 左窗格中，型別上的方塊[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="7cf69-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="7cf69-220">您會看到顯示 hello 搜尋清單中的 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="7cf69-221">拖放 hello[執行 R 指令碼][ execute-r-script]到您棧板上的模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="7cf69-222">Hello hello 輸出連接**csdairydata.csv 資料集**toohello 最左邊的輸入 (**Dataset1**) 的 hello[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="7cf69-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="7cf69-223">**別忘了 [儲存] tooclick ！**</span><span class="sxs-lookup"><span data-stu-id="7cf69-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="7cf69-224">此時，您的實驗應該會看起來像圖 3。</span><span class="sxs-lookup"><span data-stu-id="7cf69-224">At this point your experiment should look something like Figure 3.</span></span>

![hello CA 香蕉分析試驗資料集和執行 R 指令碼模組][3]

<span data-ttu-id="7cf69-226">*圖 3。hello CA 香蕉分析試驗資料集和執行 R 指令碼模組。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="7cf69-227">檢查 hello 資料</span><span class="sxs-lookup"><span data-stu-id="7cf69-227">Check on hello data</span></span>
<span data-ttu-id="7cf69-228">讓我們看看我們已載入至我們實驗 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="7cf69-229">在 hello 實驗中，按一下 hello hello 輸出**cadairydata.csv 資料集**選取**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="7cf69-230">您應該會看到類似圖 4 的內容。</span><span class="sxs-lookup"><span data-stu-id="7cf69-230">You should see something like Figure 4.</span></span>  

![Hello cadairydata.csv 資料集的摘要][4]

<span data-ttu-id="7cf69-232">*圖 4：Hello cadairydata.csv 資料集的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="7cf69-233">在這個檢視中，我們會看到許多有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="7cf69-234">我們可以看到 hello 該資料集的前幾個資料列。</span><span class="sxs-lookup"><span data-stu-id="7cf69-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="7cf69-235">如果我們選取資料行，hello 統計資料 區段會顯示 hello 資料行的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="7cf69-236">例如，hello 功能類型的資料列顯示我們哪些 Azure Machine Learning Studio 指派 toohello 資料行的資料型別。</span><span class="sxs-lookup"><span data-stu-id="7cf69-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="7cf69-237">擁有快速的看起來像這樣是很好的例行性檢查，我們開始 toodo 任何嚴重的工作之前。</span><span class="sxs-lookup"><span data-stu-id="7cf69-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="7cf69-238">第一個 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="7cf69-238">First R script</span></span>
<span data-ttu-id="7cf69-239">讓我們來建立簡單的第一個 R 指令碼 tooexperiment 與 Azure Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="7cf69-240">已建立並測試下列指令碼中 RStudio hello。</span><span class="sxs-lookup"><span data-stu-id="7cf69-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="7cf69-241">現在我需要 tootransfer 此指令碼 tooAzure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="7cf69-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="7cf69-242">我可以只利用剪下並貼上。</span><span class="sxs-lookup"><span data-stu-id="7cf69-242">I could simply cut and paste.</span></span> <span data-ttu-id="7cf69-243">不過，在此案例中，我將透過 Zip 檔案轉移我的 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="7cf69-244">資料輸入的 toohello 執行 R 指令碼模組</span><span class="sxs-lookup"><span data-stu-id="7cf69-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="7cf69-245">讓我們看一下 hello 輸入 toohello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-246">在此範例中我們將 hello 加州日常的資料讀入 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="7cf69-247">有三個可能的輸入 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-248">視您的應用方式而定，您可以使用這當中的任何一個或所有輸入。</span><span class="sxs-lookup"><span data-stu-id="7cf69-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="7cf69-249">它也是非常合理 toouse R 指令碼完全接受任何輸入。</span><span class="sxs-lookup"><span data-stu-id="7cf69-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="7cf69-250">讓我們看看每個這些輸入，從左 tooright。</span><span class="sxs-lookup"><span data-stu-id="7cf69-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="7cf69-251">您可以藉由將游標放在 hello 輸入上方及閱讀 hello 工具提示中看到每個 hello 輸入 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7cf69-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="7cf69-252">指令碼組合</span><span class="sxs-lookup"><span data-stu-id="7cf69-252">Script Bundle</span></span>
<span data-ttu-id="7cf69-253">hello 指令碼組合輸入可讓您將 zip 檔案 toopass hello 內容[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-254">您可以使用其中一個 hello 遵循 hello zip 檔案的命令 tooread hello 內容到您的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="7cf69-255">Azure Machine Learning 會處理 hello zip 檔案，就好像它們是在 hello src / 目錄，因此您需要的 tooprefix 您的檔案名稱具有這個目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="7cf69-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="7cf69-256">例如，如果 hello zip 包含 hello 檔案`yourfile.R`和`yourData.rdata`hello 在根目錄中的 hello zip，您會解決這些問題，做為`src/yourfile.R`和`src/yourData.rdata`時使用`source`和`load`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="7cf69-257">我們已經討論過載入中的資料集[載入 hello 資料集](#loading)。</span><span class="sxs-lookup"><span data-stu-id="7cf69-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="7cf69-258">一旦您建立並測試顯示 hello 前一節中的 hello R 指令碼，不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7cf69-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="7cf69-259">儲存成 hello R 指令碼。R 的檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="7cf69-260">我將我的指令碼檔案稱為 "simpleplot.R"。</span><span class="sxs-lookup"><span data-stu-id="7cf69-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="7cf69-261">以下是 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="7cf69-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="7cf69-262">建立一個 Zip 檔案，然後將您的指令碼複製到此 Zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="7cf69-263">在 Windows 中，您可以在 hello 檔案上按一下滑鼠右鍵並選取**傳送給**，然後**壓縮的資料夾**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="7cf69-264">這會建立新的 zip 檔案包含 hello"simpleplot。R"檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="7cf69-265">新增檔案 toohello**資料集**在 Machine Learning Studio 中，指定與 hello 類型**zip**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="7cf69-266">您現在應該會在您資料集中看到 hello zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="7cf69-267">拖放 hello zip 檔案從**資料集**到 hello **ML Studio 畫布**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="7cf69-268">Hello hello 輸出連接**zip 資料**圖示 toohello**指令碼組合**輸入的 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="7cf69-269">型別 hello `source()` hello 到 hello 程式碼視窗您 zip 檔案名稱的函式[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-270">在我的案例中，我鍵入了 `source("src/simpleplot.R")`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="7cf69-271">確定按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="7cf69-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="7cf69-272">完成這些步驟之後，hello[執行 R 指令碼][ execute-r-script]模組會執行 hello R 指令碼 hello zip 檔案中執行 hello 實驗時。</span><span class="sxs-lookup"><span data-stu-id="7cf69-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="7cf69-273">此時，您的實驗應該會看起來像圖 5。</span><span class="sxs-lookup"><span data-stu-id="7cf69-273">At this point your experiment should look something like Figure 5.</span></span>

![使用已壓縮之 R 指令碼的實驗][6]

<span data-ttu-id="7cf69-275">*圖 5.使用已壓縮之 R 指令碼的實驗。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="7cf69-276">資料集1</span><span class="sxs-lookup"><span data-stu-id="7cf69-276">Dataset1</span></span>
<span data-ttu-id="7cf69-277">您可以使用的 hello Dataset1 輸入傳遞矩形資料 tooyour R 程式碼的資料表。</span><span class="sxs-lookup"><span data-stu-id="7cf69-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="7cf69-278">在我們的簡單的指令碼 hello`maml.mapInputPort(1)`函式會從連接埠 1 讀取 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="7cf69-279">這項資料接著會指派 tooa 資料框架變數名稱在程式碼中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="7cf69-280">在簡單的指令碼 hello 第一行程式碼會執行 hello 分派。</span><span class="sxs-lookup"><span data-stu-id="7cf69-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="7cf69-281">Hello 上按一下來執行實驗**執行** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf69-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="7cf69-282">Hello 執行完成時，按一下 hello[執行 R 指令碼][ execute-r-script]模組，然後按一下**檢視輸出記錄檔**hello 屬性] 窗格。</span><span class="sxs-lookup"><span data-stu-id="7cf69-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="7cf69-283">新的頁面應該會出現在瀏覽器中顯示 hello hello output.log 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="7cf69-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="7cf69-284">當您向下捲動時您應該會看到類似下列 hello。</span><span class="sxs-lookup"><span data-stu-id="7cf69-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="7cf69-285">遠 hello 關閉頁面是 hello 的資料行，看起來像 hello 以下更詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="7cf69-286">這些結果是大部分如預期般，使用 228 觀察和 9 hello 資料框架中的資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="7cf69-287">我們可以看到 hello 資料行名稱、 hello R 資料類型以及每個資料行的範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="7cf69-288">這個相同的列印的輸出會很方便提供 hello R 裝置 hello 輸出[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-289">我們將討論的 hello hello 輸出[執行 R 指令碼][ execute-r-script] hello 下一節中的模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="7cf69-290">資料集2</span><span class="sxs-lookup"><span data-stu-id="7cf69-290">Dataset2</span></span>
<span data-ttu-id="7cf69-291">hello hello Dataset2 輸入行為是相同的 Dataset1 toothat。</span><span class="sxs-lookup"><span data-stu-id="7cf69-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="7cf69-292">您可以使用此輸入將第二個矩形資料表傳遞給您的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="7cf69-293">hello 函式`maml.mapInputPort(2)`，hello 引數 2，是使用的 toopass 這項資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="7cf69-294">執行 R 指令碼輸出</span><span class="sxs-lookup"><span data-stu-id="7cf69-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="7cf69-295">輸出資料框架</span><span class="sxs-lookup"><span data-stu-id="7cf69-295">Output a dataframe</span></span>
<span data-ttu-id="7cf69-296">您也可以使用 hello 為矩形資料表透過 hello 結果 Dataset1 連接埠輸出的 R 資料框架的 hello 內容`maml.mapOutputPort()`函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="7cf69-297">在簡單的 R 指令碼會執行由 hello 行下。</span><span class="sxs-lookup"><span data-stu-id="7cf69-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="7cf69-298">之後執行 hello 實驗中，按一下 hello 結果 Dataset1 輸出連接埠，然後按一下**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="7cf69-299">您應該會看到類似圖 6 的內容。</span><span class="sxs-lookup"><span data-stu-id="7cf69-299">You should see something like Figure 6.</span></span>

![hello 視覺效果的 hello hello 加州日常資料輸出][7]

<span data-ttu-id="7cf69-301">*圖 6。hello hello 加州日常資料輸出的 hello 視覺效果。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="7cf69-302">完全依照我們所預期，此輸出看起來相同 toohello 輸入。</span><span class="sxs-lookup"><span data-stu-id="7cf69-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="7cf69-303">R 裝置輸出</span><span class="sxs-lookup"><span data-stu-id="7cf69-303">R Device output</span></span>
<span data-ttu-id="7cf69-304">hello 裝置 hello 輸出[執行 R 指令碼][ execute-r-script]模組包含訊息和圖形輸出。</span><span class="sxs-lookup"><span data-stu-id="7cf69-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="7cf69-305">從 R 這兩個標準輸出和標準錯誤訊息會傳送 toohello R 裝置輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="7cf69-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="7cf69-306">tooview hello R 裝置輸出，按一下 hello 連接埠，然後在**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="7cf69-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="7cf69-307">我們看到 hello 標準輸出和圖 7 中的 hello R 指令碼從標準錯誤。</span><span class="sxs-lookup"><span data-stu-id="7cf69-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![標準輸出和標準錯誤從 hello R 裝置連接埠][8]

<span data-ttu-id="7cf69-309">*圖 7.標準輸出和標準誤差從 hello R 裝置連接埠。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="7cf69-310">我們向下捲動，請參閱我們的 R 指令碼，圖 8 中的 hello 圖形輸出。</span><span class="sxs-lookup"><span data-stu-id="7cf69-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![從 hello R 裝置連接埠圖形輸出][9]

<span data-ttu-id="7cf69-312">*圖 8.來自 hello R 裝置連接埠的輸出圖形。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="7cf69-313"><a id="filtering"></a>資料篩選和轉換</span><span class="sxs-lookup"><span data-stu-id="7cf69-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="7cf69-314">本節中，我們將會執行一些基本的資料篩選和 hello 加州日常資料轉換作業。</span><span class="sxs-lookup"><span data-stu-id="7cf69-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="7cf69-315">本節結尾 hello 我們會具有適合用來建立分析模型的格式資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="7cf69-316">更具體來說，在本節中，我們將會執行數個常見的資料清除和轉換工作：類型轉換、依據資料框架進行篩選、新增新的計算資料行，以及值轉換。</span><span class="sxs-lookup"><span data-stu-id="7cf69-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="7cf69-317">這個背景應可協助您處理 hello 許多實際問題中發生的變化。</span><span class="sxs-lookup"><span data-stu-id="7cf69-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="7cf69-318">hello 完整的 R 程式碼對此區段可前往您剛才下載的 hello zip 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="7cf69-319">類型轉換</span><span class="sxs-lookup"><span data-stu-id="7cf69-319">Type transformations</span></span>
<span data-ttu-id="7cf69-320">現在，我們可以讀入 hello 中的 hello R 程式碼中的 hello 加州日常資料[執行 R 指令碼][ execute-r-script]模組中，我們需要 tooensure hello 資料行中的 hello 資料有適合的 hello 類型與格式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="7cf69-321">R 是動態類型的語言，這表示資料型別會從所需的一個 tooanother 強制。</span><span class="sxs-lookup"><span data-stu-id="7cf69-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="7cf69-322">在 R 中的 hello 不可部分完成的資料類型包括數值、 邏輯和字元。</span><span class="sxs-lookup"><span data-stu-id="7cf69-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="7cf69-323">hello 因素型別是使用的 toocompactly 存放區中的類別資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="7cf69-324">您可以在 hello 參考中找到更多有關資料型別的[附錄 B-進一步閱讀](#appendixb)。</span><span class="sxs-lookup"><span data-stu-id="7cf69-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="7cf69-325">表格式資料到 R 從外部來源讀取時，永遠是個不錯的主意 toocheck hello 產生 hello 資料行中的型別。</span><span class="sxs-lookup"><span data-stu-id="7cf69-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="7cf69-326">您可能想要字元類型的資料行，但在許多情況下這會顯示為因素類型，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="7cf69-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="7cf69-327">在其他情況下，則是會以字元資料代表您認為應該是數值的資料行，例如 '1.23' 而非浮點數形式的 1.23。</span><span class="sxs-lookup"><span data-stu-id="7cf69-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="7cf69-328">幸運的是，它是一個型別 tooanother 輕鬆 tooconvert，只要對應可能。</span><span class="sxs-lookup"><span data-stu-id="7cf69-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="7cf69-329">例如，您無法將 'Nevada' 轉換成數值，但您可以將它轉換 tooa 因素 （類別變數）。</span><span class="sxs-lookup"><span data-stu-id="7cf69-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="7cf69-330">另舉一例，您可以將數值 1 轉換成字元 '1' 或因素。</span><span class="sxs-lookup"><span data-stu-id="7cf69-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="7cf69-331">針對任何這些轉換 hello 語法很簡單： `as.datatype()`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="7cf69-332">這些類型轉換函式 hello 如下。</span><span class="sxs-lookup"><span data-stu-id="7cf69-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="7cf69-333">查看 hello 我們輸入 hello 前一節中的 hello 資料行資料類型： 所有資料行都是數字，除了 hello 資料行標示為 'Month'，也就是型別字元的類型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="7cf69-334">讓我們來轉換這個 tooa 因素，並測試 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7cf69-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="7cf69-335">我已刪除 hello 列建立 hello scatterplot 矩陣並加入轉換 hello 'Month' 資料行 tooa 因素一條線。</span><span class="sxs-lookup"><span data-stu-id="7cf69-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="7cf69-336">在我的實驗中我將只剪下並 hello R 程式碼貼入程式碼視窗中 hello hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="7cf69-337">您也可以更新 hello zip 檔案，並將它上傳 tooAzure Machine Learning Studio 中，但這需要一些步驟。</span><span class="sxs-lookup"><span data-stu-id="7cf69-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="7cf69-338">讓我們來執行這個程式碼，並查看 hello hello R 指令碼的輸出記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cf69-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="7cf69-339">圖 9 顯示 hello hello 記錄檔中的相關資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-339">hello relevant data from hello log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="7cf69-340">*圖 9.Hello 與因數變數的資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="7cf69-341">現在應顯示月份的 hello 型別 '**具有 14 個層級的因素**'。</span><span class="sxs-lookup"><span data-stu-id="7cf69-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="7cf69-342">因為 hello 年只 12 個月，這會是問題。</span><span class="sxs-lookup"><span data-stu-id="7cf69-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="7cf69-343">您也可以檢查 hello 類型的 toosee 中**視覺化**hello 結果資料集中的連接埠是 '**類別**'。</span><span class="sxs-lookup"><span data-stu-id="7cf69-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="7cf69-344">hello 問題為該 hello 'Month' 資料行未有系統地編碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="7cf69-345">在某些情況下，某個月份稱為 April ，在其他情況下則會縮寫成 Apr。我們可以修剪 hello 字串 too3 字元來解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="7cf69-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="7cf69-346">hello 一行程式碼現在看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7cf69-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="7cf69-347">重新執行 hello 實驗，並檢視 hello 輸出記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cf69-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="7cf69-348">hello 預期的結果會顯示在圖 10。</span><span class="sxs-lookup"><span data-stu-id="7cf69-348">hello expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="7cf69-349">*圖 10.Hello 與因素層級的正確數目的資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="7cf69-350">我們因數變數現在具有所需的 hello 12 個層級。</span><span class="sxs-lookup"><span data-stu-id="7cf69-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="7cf69-351">基本資料框架篩選</span><span class="sxs-lookup"><span data-stu-id="7cf69-351">Basic data frame filtering</span></span>
<span data-ttu-id="7cf69-352">R 資料框架支援強大的篩選功能。</span><span class="sxs-lookup"><span data-stu-id="7cf69-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="7cf69-353">藉由在資料列或資料行使用邏輯篩選，可將資料集再細分成子集。</span><span class="sxs-lookup"><span data-stu-id="7cf69-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="7cf69-354">在許多情況下，將會需要複雜的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7cf69-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="7cf69-355">參考中的 hello[附錄 B-進一步閱讀](#appendixb)包含廣泛的篩選資料框架的範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="7cf69-356">有一些篩選是我們應該在資料集上執行的。</span><span class="sxs-lookup"><span data-stu-id="7cf69-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="7cf69-357">如果您看一下 hello hello cadairydata 資料框架中的資料行，您會看到兩個不必要的資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="7cf69-358">hello 第一個資料行只會保存資料列數字，不是很有用。</span><span class="sxs-lookup"><span data-stu-id="7cf69-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="7cf69-359">hello 第二個資料行，Year.Month，包含重複的資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="7cf69-360">我們可以使用下列 R 程式碼的 hello，輕鬆地排除這些資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="7cf69-361">從現在在本節中，我將只顯示您的 hello 我 hello 中加入額外的程式碼[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="7cf69-362">將每一個新行**之前**hello`str()`函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="7cf69-363">我使用這個函式 tooverify 我結果 Azure Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="7cf69-364">加入下列行 toomy R 程式碼中 hello hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="7cf69-365">在您實驗中執行此程式碼並查看 hello 輸出記錄檔中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7cf69-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="7cf69-366">這些結果如圖 11 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="7cf69-367">*圖 11.Hello 與移除的兩個資料行的資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="7cf69-368">好消息！</span><span class="sxs-lookup"><span data-stu-id="7cf69-368">Good news!</span></span> <span data-ttu-id="7cf69-369">我們取得 hello 預期結果。</span><span class="sxs-lookup"><span data-stu-id="7cf69-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="7cf69-370">加入新的資料行</span><span class="sxs-lookup"><span data-stu-id="7cf69-370">Add a new column</span></span>
<span data-ttu-id="7cf69-371">toocreate 時間序列模型會很方便 toohave 資料行包含 hello hello hello 時間序列的開頭之後的月份。</span><span class="sxs-lookup"><span data-stu-id="7cf69-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="7cf69-372">我們將會建立新資料行 'Month.Count'。</span><span class="sxs-lookup"><span data-stu-id="7cf69-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="7cf69-373">toohelp 組織 hello 程式碼，我們將建立簡單我們第一個函式， `num.month()`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="7cf69-374">然後，我們會套用此函式 toocreate hello 資料框架中的新資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="7cf69-375">hello 新的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="7cf69-376">現在，執行更新的 hello 實驗並使用 hello 輸出記錄檔 tooview hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7cf69-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="7cf69-377">這些結果如圖 12 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="7cf69-378">*圖 12.Hello 與 hello 額外的資料行的資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="7cf69-379">看來一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="7cf69-379">It looks like everything is working.</span></span> <span data-ttu-id="7cf69-380">我們在我們的資料框架中有 hello hello 預期的值與新資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="7cf69-381">值轉換</span><span class="sxs-lookup"><span data-stu-id="7cf69-381">Value transformations</span></span>
<span data-ttu-id="7cf69-382">這一節我們將的部分我們的資料框架的 hello 欄中的 hello 值上執行一些簡單的轉換。</span><span class="sxs-lookup"><span data-stu-id="7cf69-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="7cf69-383">hello R 語言支援幾乎任意值轉換。</span><span class="sxs-lookup"><span data-stu-id="7cf69-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="7cf69-384">參考中的 hello[附錄 B-進一步閱讀](#appendixb)包含廣泛的範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="7cf69-385">如果您看一下您應該會看到我們資料框架的 hello 摘要中的 hello 值是奇數這裡。</span><span class="sxs-lookup"><span data-stu-id="7cf69-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="7cf69-386">加州生產的冰淇淋比牛奶多？</span><span class="sxs-lookup"><span data-stu-id="7cf69-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="7cf69-387">否，當然不是，這樣會造成沒有意義，悲傷成為這個事實可能 toosome 我們冰淇淋能。</span><span class="sxs-lookup"><span data-stu-id="7cf69-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="7cf69-388">hello 單位都不同。</span><span class="sxs-lookup"><span data-stu-id="7cf69-388">hello units are different.</span></span> <span data-ttu-id="7cf69-389">hello 價格是以我們磅，單位 1 M 的冰淇淋美國磅 1000 的單位我們加侖，而且小屋 cheese 為 1,000 美國磅單位的牛奶。</span><span class="sxs-lookup"><span data-stu-id="7cf69-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="7cf69-390">假設冰淇淋充分權衡約 6.5 磅每加侖，我們可以輕鬆地執行 hello 乘法 tooconvert，因此它們都放在相同單位的 1,000 磅，這些值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="7cf69-391">針對我們的預測模型，我們使用乘法模型來進行此資料的趨勢和季節性調整。</span><span class="sxs-lookup"><span data-stu-id="7cf69-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="7cf69-392">記錄轉換，可讓我們 toouse 線性模型，以簡化此程序。</span><span class="sxs-lookup"><span data-stu-id="7cf69-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="7cf69-393">我們可以套用在 hello 相同函式套用 hello 乘數的位置中的 hello 記錄轉換。</span><span class="sxs-lookup"><span data-stu-id="7cf69-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="7cf69-394">在下列程式碼的 hello，定義新的函式， `log.transform()`，並將它套用 toohello 包含 hello 數值的資料列。</span><span class="sxs-lookup"><span data-stu-id="7cf69-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="7cf69-395">hello R`Map()`函式是使用的 tooapply hello`log.transform()`函式 toohello 選取 hello 資料框架的資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="7cf69-396">`Map()`太類似`apply()`，但允許多個引數 toohello 函式清單。</span><span class="sxs-lookup"><span data-stu-id="7cf69-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="7cf69-397">請注意，有一份提供第二個引數 toohello hello`log.transform()`函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="7cf69-398">hello`na.omit()`函式當做位元的清除 tooensure 我們沒有遺失或未定義的值在 hello 資料框架。</span><span class="sxs-lookup"><span data-stu-id="7cf69-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="7cf69-399">沒有在 hello 相當多的位元發生`log.transform()`函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="7cf69-400">大部分的這段程式碼會檢查 hello 引數的潛在問題，或處理的例外狀況，仍可能會發生在 hello 計算期間。</span><span class="sxs-lookup"><span data-stu-id="7cf69-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="7cf69-401">只需幾行，此程式碼的實際 hello 計算。</span><span class="sxs-lookup"><span data-stu-id="7cf69-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="7cf69-402">hello 防禦程式設計 hello 目標是 tooprevent hello 失敗會阻礙無法繼續處理的單一函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="7cf69-403">執行很久的分析如果突然失敗，可能會讓使用者深感挫折。</span><span class="sxs-lookup"><span data-stu-id="7cf69-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="7cf69-404">這種情況下，預設傳回值必須選擇，將會限制的 tooavoid 損害 toodownstream 處理。</span><span class="sxs-lookup"><span data-stu-id="7cf69-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="7cf69-405">訊息也是有錯誤哪裡發生的產生的 tooalert 使用者。</span><span class="sxs-lookup"><span data-stu-id="7cf69-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="7cf69-406">如果您不使用的 toodefensive 程式設計，在 R 中，所有這段程式碼看起來可能有點非常龐大。</span><span class="sxs-lookup"><span data-stu-id="7cf69-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="7cf69-407">我將引導您完成 hello 主要步驟：</span><span class="sxs-lookup"><span data-stu-id="7cf69-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="7cf69-408">定義包含四個訊息的向量。</span><span class="sxs-lookup"><span data-stu-id="7cf69-408">A vector of four messages is defined.</span></span> <span data-ttu-id="7cf69-409">這些訊息是部分 hello 可能的錯誤和例外狀況，可能會發生這段程式碼使用的 toocommunicate 資訊。</span><span class="sxs-lookup"><span data-stu-id="7cf69-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="7cf69-410">我會針對每個案例傳回一個 NA 值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-410">I return a value of NA for each case.</span></span> <span data-ttu-id="7cf69-411">有許多其他可能會有較少副作用的可能性。</span><span class="sxs-lookup"><span data-stu-id="7cf69-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="7cf69-412">我無法傳回向量的零或原始輸入的向量 hello，例如。</span><span class="sxs-lookup"><span data-stu-id="7cf69-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="7cf69-413">Hello 引數 toohello 函式上執行的檢查。</span><span class="sxs-lookup"><span data-stu-id="7cf69-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="7cf69-414">在每個案例中，如果偵測到錯誤時，會傳回預設值的訊息所產生和 hello`warning()`函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="7cf69-415">我使用`warning()`而不是`stop()`為 hello 後者將會終止執行，完全什麼我試著 tooavoid。</span><span class="sxs-lookup"><span data-stu-id="7cf69-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="7cf69-416">請注意，我是以程序性風格撰寫此程式碼，因此在此情況下，函式型方法看似既複雜又難以理解。</span><span class="sxs-lookup"><span data-stu-id="7cf69-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="7cf69-417">hello 記錄計算會包裝在`tryCatch()`，讓例外狀況並不會造成突然中止 tooprocessing。</span><span class="sxs-lookup"><span data-stu-id="7cf69-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="7cf69-418">如果沒有 `tryCatch()` ，R 函式所引發的大多數錯誤都會導致產生停止訊號，而此訊號所執行的就是停止。</span><span class="sxs-lookup"><span data-stu-id="7cf69-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="7cf69-419">執行此 R 程式碼在您實驗中，並查看 hello 列印 hello output.log 檔案的輸出。</span><span class="sxs-lookup"><span data-stu-id="7cf69-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="7cf69-420">您現在會看見 hello 轉換值的 hello hello 的四個資料行記錄，如圖 13 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="7cf69-421">*圖 13.摘要的 hello 轉換 hello 資料框架中的值。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="7cf69-422">我們會看到已轉換 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-422">We see hello values have been transformed.</span></span> <span data-ttu-id="7cf69-423">現在，牛奶產量大幅超過所有其他乳製品產量，還記得我們現在看的是對數刻度。</span><span class="sxs-lookup"><span data-stu-id="7cf69-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="7cf69-424">此時會清除我們的資料，而我們已經準備好進行一些建立模型工作。</span><span class="sxs-lookup"><span data-stu-id="7cf69-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="7cf69-425">查看 hello 視覺效果的輸出結果集的 hello 摘要我們[執行 R 指令碼][ execute-r-script]模組，就會看見 hello 'Month' 資料行是 '類別' 具有 12 個唯一值，一次，就像我們.</span><span class="sxs-lookup"><span data-stu-id="7cf69-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="7cf69-426"><a id="timeseries"></a>時間序列物件和相互關聯分析</span><span class="sxs-lookup"><span data-stu-id="7cf69-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="7cf69-427">這一節中，我們將探索幾個基本的 R 時間序列物件及分析 hello 相互關聯之間有些 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="7cf69-428">我們的目標是 toooutput 資料框架包含 hello 成對的相互關聯資訊在數個延遲。</span><span class="sxs-lookup"><span data-stu-id="7cf69-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="7cf69-429">hello 完整的 R 程式碼對此區段是您之前下載的 hello zip 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="7cf69-430">R 中的時間序列物件</span><span class="sxs-lookup"><span data-stu-id="7cf69-430">Time series objects in R</span></span>
<span data-ttu-id="7cf69-431">如已經提過的，時間序列是一系列依時間編制索引的資料值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="7cf69-432">R 時間序列物件是使用的 toocreate，而且管理 hello 時間索引。</span><span class="sxs-lookup"><span data-stu-id="7cf69-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="7cf69-433">有數個優點 toousing 時間數列物件。</span><span class="sxs-lookup"><span data-stu-id="7cf69-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="7cf69-434">時間序列物件讓您從 hello 管理 hello 時間序列索引值 hello 物件中封裝的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="7cf69-435">此外，時間序列物件允許您 toouse hello 許多時間數列方法來繪製，等模型列印。</span><span class="sxs-lookup"><span data-stu-id="7cf69-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="7cf69-436">hello POSIXct 時間數列類別通常用於和相當簡單。</span><span class="sxs-lookup"><span data-stu-id="7cf69-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="7cf69-437">這個時間數列類別測量從 hello hello epoch，自 1970 年 1 月 1 日開始的時間。</span><span class="sxs-lookup"><span data-stu-id="7cf69-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="7cf69-438">在此範例中，我們將使用 POSIXct 時間序列物件。</span><span class="sxs-lookup"><span data-stu-id="7cf69-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="7cf69-439">其他廣泛使用的 R 時間序列物件類別包括 zoo 和 xts (可延伸時間序列)。</span><span class="sxs-lookup"><span data-stu-id="7cf69-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="7cf69-440">時間序列物件範例</span><span class="sxs-lookup"><span data-stu-id="7cf69-440">Time series object example</span></span>
<span data-ttu-id="7cf69-441">讓我們開始進行我們的範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-441">Let's get started with our example.</span></span> <span data-ttu-id="7cf69-442">請將**新的**[執行 R 指令碼][execute-r-script]模組拖放到您的實驗中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="7cf69-443">連接現有 hello hello 結果 Dataset1 輸出連接埠[執行 R 指令碼][ execute-r-script]模組 toohello Dataset1 輸入 hello 新連接埠[執行 R 指令碼][execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="7cf69-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="7cf69-444">我在 hello 第一個範例中，當我們透過 hello 範例中，在一些重點，我將會顯示進度只 hello 累加的 R 程式碼在每個步驟的其他行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="7cf69-445">讀取 hello 資料框架</span><span class="sxs-lookup"><span data-stu-id="7cf69-445">Reading hello dataframe</span></span>
<span data-ttu-id="7cf69-446">第一個步驟中，我們在資料框架中讀取，並確定我們取得 hello 預期結果。</span><span class="sxs-lookup"><span data-stu-id="7cf69-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="7cf69-447">hello 下列程式碼應該執行 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="7cf69-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="7cf69-448">現在，執行 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="7cf69-448">Now, run hello experiment.</span></span> <span data-ttu-id="7cf69-449">新執行 R 指令碼圖形 hello hello 記錄看起來應該像圖 14。</span><span class="sxs-lookup"><span data-stu-id="7cf69-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="7cf69-450"> *14.Hello hello 執行 R 指令碼模組中的資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="7cf69-451">此資料是 hello 預期型別和格式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="7cf69-452">請注意，型別因素 hello 'Month' 資料行是 hello 是預期的層級數目。</span><span class="sxs-lookup"><span data-stu-id="7cf69-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="7cf69-453">建立時間序列物件</span><span class="sxs-lookup"><span data-stu-id="7cf69-453">Creating a time series object</span></span>
<span data-ttu-id="7cf69-454">我們需要 tooadd 時間序列物件 tooour 資料框架。</span><span class="sxs-lookup"><span data-stu-id="7cf69-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="7cf69-455">Hello 目前程式碼取代 hello 下列程式碼，這會將 POSIXct 類別的新資料行中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="7cf69-456">現在，檢查 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cf69-456">Now, check hello log.</span></span> <span data-ttu-id="7cf69-457">這應該會看起來像圖 15。</span><span class="sxs-lookup"><span data-stu-id="7cf69-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="7cf69-458"> *15.Hello 與時間序列物件的資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="7cf69-459">我們可以看到從 hello 摘要類別 POSIXct 事實上是該 hello 新資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="7cf69-460">瀏覽及 hello 資料轉換</span><span class="sxs-lookup"><span data-stu-id="7cf69-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="7cf69-461">讓我們來探索一些 hello 這個 dataset 中的變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="7cf69-462">Scatterplot 矩陣是很好的方式 tooproduce 快速瀏覽。</span><span class="sxs-lookup"><span data-stu-id="7cf69-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="7cf69-463">我正在取代 hello `str()` hello 先前 R 的程式碼以行下的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="7cf69-464">請執行此程式碼，然後看看結果如何。</span><span class="sxs-lookup"><span data-stu-id="7cf69-464">Run this code and see what happens.</span></span> <span data-ttu-id="7cf69-465">hello R 裝置連接埠在產生的 hello 圖看起來應該像圖 16。</span><span class="sxs-lookup"><span data-stu-id="7cf69-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![所選變數的散佈圖矩陣][17]

<span data-ttu-id="7cf69-467">*圖 16.所選變數的散佈圖矩陣。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="7cf69-468">一些奇怪的結構中沒有 hello 關聯性之間這些變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="7cf69-469">也許這就會發生與 hello 資料中的趨勢和 hello 事實，我們不標準化 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="7cf69-470">相互關聯分析</span><span class="sxs-lookup"><span data-stu-id="7cf69-470">Correlation analysis</span></span>
<span data-ttu-id="7cf69-471">我們需要 tooboth tooperform 相互關聯分析解除趨勢，並設立標準 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="7cf69-472">我們可以只使用 hello R`scale()`函式，以同時中心和縮放變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="7cf69-473">此函式可能也執行得更快。</span><span class="sxs-lookup"><span data-stu-id="7cf69-473">This function might well run faster.</span></span> <span data-ttu-id="7cf69-474">不過，我想 tooshow 您的防禦程式設計範例</span><span class="sxs-lookup"><span data-stu-id="7cf69-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="7cf69-475">hello`ts.detrend()`如下所示的函式會執行這兩種作業。</span><span class="sxs-lookup"><span data-stu-id="7cf69-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="7cf69-476">hello 下列兩行程式碼取消趨勢 hello 資料，然後標準化 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="7cf69-477">沒有在 hello 相當多的位元發生`ts.detrend()`函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="7cf69-478">大部分的這段程式碼會檢查 hello 引數的潛在問題，或處理的例外狀況，仍可能會發生在 hello 計算期間。</span><span class="sxs-lookup"><span data-stu-id="7cf69-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="7cf69-479">只需幾行，此程式碼的實際 hello 計算。</span><span class="sxs-lookup"><span data-stu-id="7cf69-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="7cf69-480">我們已經在[值轉換](#valuetransformations)中討論過防禦型程式設計的範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="7cf69-481">兩個計算區塊皆包裝在 `tryCatch()` 中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="7cf69-482">對於某些錯誤它意義 tooreturn hello 原始輸入的向量，而在其他情況下，傳回零的向量。</span><span class="sxs-lookup"><span data-stu-id="7cf69-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="7cf69-483">請注意，用來取消趨勢 hello 線性迴歸時間數列迴歸。</span><span class="sxs-lookup"><span data-stu-id="7cf69-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="7cf69-484">hello 預測量變數是時間序列物件。</span><span class="sxs-lookup"><span data-stu-id="7cf69-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="7cf69-485">一次`ts.detrend()`定義我們會套用它 toohello 變數，在我們的資料框架中有用。</span><span class="sxs-lookup"><span data-stu-id="7cf69-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="7cf69-486">我們必須強制轉型所建立的 hello 產生清單`lapply()`toodata 資料框架使用`as.data.frame()`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="7cf69-487">因為防禦層面`ts.detrend()`，失敗 tooprocess 其中 hello 變數並不會妨礙修正 hello 處理其他人。</span><span class="sxs-lookup"><span data-stu-id="7cf69-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="7cf69-488">hello 最後一行程式碼會建立成對 scatterplot。</span><span class="sxs-lookup"><span data-stu-id="7cf69-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="7cf69-489">執行 hello R 程式碼之後, 的 hello scatterplot 的 hello 結果會顯示在圖 17。</span><span class="sxs-lookup"><span data-stu-id="7cf69-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![已去除趨勢並已標準化之時間序列的成對散佈圖][18]

<span data-ttu-id="7cf69-491">*圖 17.已去除趨勢並已標準化之時間序列的成對散佈圖。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="7cf69-492">您可以比較這些結果 toothose，16 圖所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="7cf69-493">以 hello 趨勢移除與 hello 變數標準化，我們看到少很多 hello 這些變數之間的關聯性中的結構。</span><span class="sxs-lookup"><span data-stu-id="7cf69-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="7cf69-494">hello 程式碼 toocompute hello 相互關聯當做 R ccf 物件如下所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="7cf69-495">執行此程式碼會產生 hello 記錄圖 18 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-495">Running this code produces hello log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="7cf69-496">*圖 18.Ccf 的清單物件從 hello 成對的相互關聯分析。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="7cf69-497">每段延隔時間都有一個相互關聯值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="7cf69-498">這些相互關聯值的 「 無 」 夠大 toobe 顯著。</span><span class="sxs-lookup"><span data-stu-id="7cf69-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="7cf69-499">因此，可以推斷出我們可以獨立建立每個變數的模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="7cf69-500">輸出資料框架</span><span class="sxs-lookup"><span data-stu-id="7cf69-500">Output a dataframe</span></span>
<span data-ttu-id="7cf69-501">我們有一份 R ccf 物件為計算 hello 成對的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="7cf69-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="7cf69-502">因為 hello 結果資料集輸出連接埠真正需要的資料框架，這會有問題的位元。</span><span class="sxs-lookup"><span data-stu-id="7cf69-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="7cf69-503">此外，hello ccf 物件是本身的清單，我們想要只 hello 值 hello 這個清單中，在 hello hello 相互關聯的第一個項目中各種延遲。</span><span class="sxs-lookup"><span data-stu-id="7cf69-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="7cf69-504">hello hello ccf 物件清單，也就是本身的清單中的下列程式碼擷取 hello 延隔時間值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="7cf69-505">hello 第一行程式碼會有點困難，並說明可協助您了解它。</span><span class="sxs-lookup"><span data-stu-id="7cf69-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="7cf69-506">我們有 hello 下列出內部工作 hello:</span><span class="sxs-lookup"><span data-stu-id="7cf69-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="7cf69-507">hello '**[[**'hello 引數的運算子'**1**' 選取 hello 向量的相互關聯性在 hello 像是從 hello hello ccf 物件清單的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="7cf69-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="7cf69-508">hello`do.call()`函式適用於 hello`rbind()`透過 hello 清單元件的 hello 函式會傳回`lapply()`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="7cf69-509">hello`data.frame()`函式會強制使所產生的 hello 結果`do.call()`tooa 資料框架。</span><span class="sxs-lookup"><span data-stu-id="7cf69-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="7cf69-510">請注意，hello 列名稱資料行中的 hello 資料框架。</span><span class="sxs-lookup"><span data-stu-id="7cf69-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="7cf69-511">這樣會保留 hello 列名稱時，它們的 hello 輸出[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="7cf69-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="7cf69-512">執行 hello 程式碼會產生 hello 圖 19 所示的輸出時我**視覺化**hello 在 hello 結果資料集連接埠的輸出。</span><span class="sxs-lookup"><span data-stu-id="7cf69-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="7cf69-513">如預期般 hello 列名稱位於 hello 第一個資料行中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-513">hello row names are in hello first column, as intended.</span></span>

![從 hello 相互關聯分析的結果輸出][20]

<span data-ttu-id="7cf69-515">*圖 19.輸出來源 hello 相互關聯分析的結果。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="7cf69-516"><a id="seasonalforecasting"></a>時間序列範例：季節性預測</span><span class="sxs-lookup"><span data-stu-id="7cf69-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="7cf69-517">我們的資料現在是適用於分析，表單中，我們判定有沒有 hello 變數之間的重要相互關聯。</span><span class="sxs-lookup"><span data-stu-id="7cf69-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="7cf69-518">讓我們繼續來建立時間序列預測模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="7cf69-519">使用此模型會預測加州牛奶生產環境適用於 hello 12 個月的 2013年。</span><span class="sxs-lookup"><span data-stu-id="7cf69-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="7cf69-520">我們的預測模型將會有兩個元件，亦即趨勢元件和季節性元件。</span><span class="sxs-lookup"><span data-stu-id="7cf69-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="7cf69-521">hello 完成預測是 hello 的這兩個元件的產品。</span><span class="sxs-lookup"><span data-stu-id="7cf69-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="7cf69-522">這種模型稱為乘法模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="7cf69-523">hello 的替代方式是加總的模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-523">hello alternative is an additive model.</span></span> <span data-ttu-id="7cf69-524">我們已經有套用感興趣，使得這項分析容易處理的記錄檔轉換 toohello 變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="7cf69-525">hello 完整的 R 程式碼對此區段是您之前下載的 hello zip 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="7cf69-526">建立 hello 進行分析的資料框架</span><span class="sxs-lookup"><span data-stu-id="7cf69-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="7cf69-527">啟動新增**新**[執行 R 指令碼][ execute-r-script]模組 tooyour 實驗。</span><span class="sxs-lookup"><span data-stu-id="7cf69-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="7cf69-528">連接 hello**結果資料集**hello 現有輸出[執行 R 指令碼][ execute-r-script]模組 toohello **Dataset1** hello 新模組的輸入。</span><span class="sxs-lookup"><span data-stu-id="7cf69-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="7cf69-529">hello 結果看起來應該像圖 20。</span><span class="sxs-lookup"><span data-stu-id="7cf69-529">hello result should look something like Figure 20.</span></span>

![hello 試驗 hello 加入新執行 R 指令碼模組][21]

<span data-ttu-id="7cf69-531">*圖 20。hello 試驗 hello 加入新執行 R 指令碼模組。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="7cf69-532">與 hello 相互關聯分析我們剛完成時，我們需要 tooadd POSIXct 時間序列物件的資料行。</span><span class="sxs-lookup"><span data-stu-id="7cf69-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="7cf69-533">下列程式碼的 hello 會這樣做只。</span><span class="sxs-lookup"><span data-stu-id="7cf69-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="7cf69-534">執行這個程式碼，並查看 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cf69-534">Run this code and look at hello log.</span></span> <span data-ttu-id="7cf69-535">hello 結果看起來應該像圖 21。</span><span class="sxs-lookup"><span data-stu-id="7cf69-535">hello result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="7cf69-536">*圖 21.Hello 資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="7cf69-537">與這個結果中，我們會準備 toostart 我們的分析。</span><span class="sxs-lookup"><span data-stu-id="7cf69-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="7cf69-538">建立訓練資料集</span><span class="sxs-lookup"><span data-stu-id="7cf69-538">Create a training dataset</span></span>
<span data-ttu-id="7cf69-539">使用建構的 hello 資料框架中，我們需要 toocreate 定型資料集。</span><span class="sxs-lookup"><span data-stu-id="7cf69-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="7cf69-540">這項資料將會包含所有的 hello 觀察 hello 過去 12 的 hello 2013 年，但這是我們的測試資料集。</span><span class="sxs-lookup"><span data-stu-id="7cf69-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="7cf69-541">hello 下列子集 hello 資料框架的程式碼，並建立 hello 日常的生產環境和價格變數的繪圖。</span><span class="sxs-lookup"><span data-stu-id="7cf69-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="7cf69-542">然後建立繪圖 hello 的生產環境和價格的四個變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="7cf69-543">是使用的 toodefine 圖，某些加強匿名函式，然後逐一查看的 hello hello 清單與其他兩個引數`Map()`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="7cf69-544">如果您正在想著可以在這裡使用 for 迴圈，的確沒錯。</span><span class="sxs-lookup"><span data-stu-id="7cf69-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="7cf69-545">但是，由於 R 是函式型語言，因此我示範給您的是函式型方法。</span><span class="sxs-lookup"><span data-stu-id="7cf69-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="7cf69-546">執行 hello 程式碼會產生的 hello hello R 裝置輸出所示圖 22 繪製數列的時間序列。</span><span class="sxs-lookup"><span data-stu-id="7cf69-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="7cf69-547">請注意該 hello 時間軸中的日期，nice hello 時間數列繪製方法的優點的單位。</span><span class="sxs-lookup"><span data-stu-id="7cf69-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![加州乳製品產量和價格資料的第一個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![加州乳製品產量和價格資料的第二個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![加州乳製品產量和價格資料的第三個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![加州乳製品產量和價格資料的第四個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="7cf69-552">*圖 22.加州乳製品產量和價格資料的時間序列圖。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="7cf69-553">趨勢模型</span><span class="sxs-lookup"><span data-stu-id="7cf69-553">A trend model</span></span>
<span data-ttu-id="7cf69-554">一旦建立時間序列物件，但有查看 hello 資料，讓我們開始 tooconstruct hello 加州牛奶實際執行資料的趨勢模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="7cf69-555">我們可以使用時間序列迴歸來進行這項操作。</span><span class="sxs-lookup"><span data-stu-id="7cf69-555">We can do this with a time series regression.</span></span> <span data-ttu-id="7cf69-556">不過，它是清除來自 hello 繪圖，我們將會需要個以上的斜率和截距 tooaccurately 模型 hello 觀察到 hello 定型資料中的趨勢。</span><span class="sxs-lookup"><span data-stu-id="7cf69-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="7cf69-557">我會提供 hello 小規模的 hello 資料，來建置 RStudio 趨勢的 hello 模型，然後剪下並貼入 Azure Machine Learning 中的 hello 產生模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="7cf69-558">RStudio 針對這種互動式分析提供了互動式環境。</span><span class="sxs-lookup"><span data-stu-id="7cf69-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="7cf69-559">做為第一次嘗試，我會嘗試與向上 too3 的次方多項式迴歸。</span><span class="sxs-lookup"><span data-stu-id="7cf69-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="7cf69-560">這些種類的模型實際蘊藏過度配適的危險。</span><span class="sxs-lookup"><span data-stu-id="7cf69-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="7cf69-561">因此，它會是最佳 tooavoid 高序位條款。</span><span class="sxs-lookup"><span data-stu-id="7cf69-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="7cf69-562">hello`I()`函式會禁止 hello 內容的解譯 （解譯 hello 內容 「 依照原狀 」） 並可讓您在迴歸方程式的 toowrite 逐字解譯函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="7cf69-563">這會產生下列 hello。</span><span class="sxs-lookup"><span data-stu-id="7cf69-563">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="7cf69-564">從 P 值 (Pr (> | t |)) 在此輸出中，我們可以看到該 hello 平方的詞彙可能不重要。</span><span class="sxs-lookup"><span data-stu-id="7cf69-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="7cf69-565">我將使用 hello`update()`函式的 toomodify 此模型所卸除 hello 平方詞彙。</span><span class="sxs-lookup"><span data-stu-id="7cf69-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="7cf69-566">這會產生下列 hello。</span><span class="sxs-lookup"><span data-stu-id="7cf69-566">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="7cf69-567">這樣看起來較好。</span><span class="sxs-lookup"><span data-stu-id="7cf69-567">This looks better.</span></span> <span data-ttu-id="7cf69-568">所有 hello 詞彙皆屬於顯著。</span><span class="sxs-lookup"><span data-stu-id="7cf69-568">All of hello terms are significant.</span></span> <span data-ttu-id="7cf69-569">不過，hello 2e-16 個值是預設值，而且不應該太嚴重採用。</span><span class="sxs-lookup"><span data-stu-id="7cf69-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="7cf69-570">例行性進行測試，讓我們進行 hello 加州日常的實際執行資料的時間序列的圖以顯示 hello 趨勢曲線。</span><span class="sxs-lookup"><span data-stu-id="7cf69-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="7cf69-571">加入下列程式碼在 hello Azure Machine Learning 中的 hello[執行 R 指令碼][ execute-r-script]模型 (不 RStudio) toocreate hello 模型，然後進行繪圖。</span><span class="sxs-lookup"><span data-stu-id="7cf69-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="7cf69-572">hello 結果是以圖 23 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![顯示趨勢模型的加州牛奶產量資料](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="7cf69-574">*圖 23.顯示趨勢模型的加州牛奶產量資料。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="7cf69-575">您似乎 hello 趨勢模型也相當適合 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="7cf69-576">此外，那里似乎未 toobe 辨識項的過度配度，例如在 hello 模型曲線 wiggles 奇數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="7cf69-577">季節性模型</span><span class="sxs-lookup"><span data-stu-id="7cf69-577">Seasonal model</span></span>
<span data-ttu-id="7cf69-578">使用趨勢模型中時，我們需要 toopush 上，而且包含 hello 季節性效應。</span><span class="sxs-lookup"><span data-stu-id="7cf69-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="7cf69-579">我們將使用 hello hello 年度月份 hello 線性模型 toocapture hello 月的作用中的虛擬變數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="7cf69-580">請注意，當您引入因數變數到模型，hello 截距必須計算。</span><span class="sxs-lookup"><span data-stu-id="7cf69-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="7cf69-581">如果您不這樣做，hello 公式是過度指定 R 將卸除其中一個 hello 預期因素，但保留 hello 截距項。</span><span class="sxs-lookup"><span data-stu-id="7cf69-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="7cf69-582">由於我們有令人滿意的趨勢模型，我們就可以使用 hello`update()`函式 tooadd hello 新條款 toohello 現有模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="7cf69-583">hello 更新公式中的 hello-1 會卸除 hello 截距項。</span><span class="sxs-lookup"><span data-stu-id="7cf69-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="7cf69-584">延續中 RStudio hello 時間：</span><span class="sxs-lookup"><span data-stu-id="7cf69-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="7cf69-585">這會產生下列 hello。</span><span class="sxs-lookup"><span data-stu-id="7cf69-585">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="7cf69-586">我們看到該 hello 模型不會再有截距項並具有 12 個重要的月份因素。</span><span class="sxs-lookup"><span data-stu-id="7cf69-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="7cf69-587">這就是我們要 toosee。</span><span class="sxs-lookup"><span data-stu-id="7cf69-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="7cf69-588">讓我們進行另一個時間序列繪製 hello 加州日常的實際執行資料 toosee hello 季節性模型使用的程度。</span><span class="sxs-lookup"><span data-stu-id="7cf69-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="7cf69-589">加入下列程式碼在 hello Azure Machine Learning 中的 hello[執行 R 指令碼][ execute-r-script] toocreate hello 模型，然後進行繪圖。</span><span class="sxs-lookup"><span data-stu-id="7cf69-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="7cf69-590">Azure Machine Learning 中執行此程式碼會產生 hello 盒狀圖 24 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![模型包含季節性效果的加州牛奶產量](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="7cf69-592">*圖 24.模型包含季節性效果的加州牛奶產量。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="7cf69-593">hello 調整的 toohello 資料顯示在圖 24 為而不是令人滿意。</span><span class="sxs-lookup"><span data-stu-id="7cf69-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="7cf69-594">Hello 趨勢及 hello 季節性效果 （每月的變化） 的外觀合理。</span><span class="sxs-lookup"><span data-stu-id="7cf69-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="7cf69-595">在我們的模型上的另一個檢查，讓我們看一下 hello 剩餘數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="7cf69-596">hello 下列程式碼計算 hello 從我們的兩個模型的預測的值、 計算 hello 殘 hello 季節性的模型，並再繪製這些殘 hello 訓練資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="7cf69-597">顯示 hello 剩餘盒狀圖 25。</span><span class="sxs-lookup"><span data-stu-id="7cf69-597">hello residual plot is shown in Figure 25.</span></span>

![剩餘數的 hello 季節性 hello 定型資料模型](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="7cf69-599">*圖 25.剩餘的 hello 定型資料的 hello 季節性模型數。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="7cf69-600">這些殘差看起來相當合理。</span><span class="sxs-lookup"><span data-stu-id="7cf69-600">These residuals look reasonable.</span></span> <span data-ttu-id="7cf69-601">沒有特定結構，除了 hello 2008 2009年經歷，我們的模型並不考慮 hello 效果特別好。</span><span class="sxs-lookup"><span data-stu-id="7cf69-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="7cf69-602">hello 盒狀圖 25 所示適用於在 hello 殘中偵測到任何時間相依模式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="7cf69-603">hello 的計算並繪製用 hello 剩餘數的明確方式置於 hello 繪圖區上的時間順序的 hello 剩餘數。</span><span class="sxs-lookup"><span data-stu-id="7cf69-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="7cf69-604">如果在 hello 相反地，我必須繪製`milk.lm$residuals`，hello 繪圖不已經按照時間順序。</span><span class="sxs-lookup"><span data-stu-id="7cf69-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="7cf69-605">您也可以使用`plot.lm()`tooproduce 一系列診斷繪圖。</span><span class="sxs-lookup"><span data-stu-id="7cf69-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="7cf69-606">此程式碼會產生一系列診斷圖，如圖 26 所示。</span><span class="sxs-lookup"><span data-stu-id="7cf69-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![診斷繪圖 hello 季節性模型中的第一個](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![第二個診斷繪圖 hello 季節性模型](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![第三個診斷繪圖 hello 季節性模型](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![第四個的 hello 季節性模型診斷的繪圖](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="7cf69-611">*圖 26.診斷繪製 hello 季節性的模型。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="7cf69-612">有幾個高影響力點中這些的繪圖，但不是識別 toocause 相當大的問題。</span><span class="sxs-lookup"><span data-stu-id="7cf69-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="7cf69-613">此外，我們可以看到從 hello 一般 Q Q 繪圖 hello 殘會關閉 toonormally 分散，線性模型是很重要的假設。</span><span class="sxs-lookup"><span data-stu-id="7cf69-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="7cf69-614">預測和模型評估</span><span class="sxs-lookup"><span data-stu-id="7cf69-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="7cf69-615">沒有一個多個項目 toodo toocomplete 我們的範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="7cf69-616">我們需要 toocompute 預測，並針對 hello 實際資料測量 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="7cf69-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="7cf69-617">我們預測將會 hello 12 個月的 2013年。</span><span class="sxs-lookup"><span data-stu-id="7cf69-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="7cf69-618">我們可以計算此預測的 toohello 實際資料不是我們的定型資料集的一部分的錯誤量值。</span><span class="sxs-lookup"><span data-stu-id="7cf69-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="7cf69-619">此外，我們可以比較效能 hello 18 歲定型資料 toohello 12 個月的測試資料。</span><span class="sxs-lookup"><span data-stu-id="7cf69-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="7cf69-620">可用的幾個度量的時間序列模型 toomeasure hello 效能。</span><span class="sxs-lookup"><span data-stu-id="7cf69-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="7cf69-621">在我們的案例中，我們將使用 hello 均方根 (RMS) 錯誤。</span><span class="sxs-lookup"><span data-stu-id="7cf69-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="7cf69-622">hello 下列函數會計算兩個數列間的 hello RMS 錯誤。</span><span class="sxs-lookup"><span data-stu-id="7cf69-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="7cf69-623">如同 hello`log.transform()`函式中我們討論 hello"的值轉換 」 一節，有很多錯誤檢查和例外狀況復原程式碼，在這個函式。</span><span class="sxs-lookup"><span data-stu-id="7cf69-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="7cf69-624">採用 hello 原則是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="7cf69-624">hello principles employed are hello same.</span></span> <span data-ttu-id="7cf69-625">hello 工作都是在兩個地方包裝在`tryCatch()`。</span><span class="sxs-lookup"><span data-stu-id="7cf69-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="7cf69-626">首先，hello 時間序列都是 exponentiated，因為我們已使用的 hello 值 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cf69-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="7cf69-627">第二，計算 hello 實際 RMS 錯誤。</span><span class="sxs-lookup"><span data-stu-id="7cf69-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="7cf69-628">配備函式 toomeasure hello RMS 錯誤，我們會建置並輸出包含 hello RMS 錯誤的資料框架。</span><span class="sxs-lookup"><span data-stu-id="7cf69-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="7cf69-629">我們將包括 hello 趨勢單獨針對模型詞彙和 hello 完整模型以季節性的因素。</span><span class="sxs-lookup"><span data-stu-id="7cf69-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="7cf69-630">hello 下列程式碼沒有 hello 作業使用兩個 hello 我們建構線性模型。</span><span class="sxs-lookup"><span data-stu-id="7cf69-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="7cf69-631">執行此程式碼會產生 hello 輸出顯示在圖 27 hello 結果資料集輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="7cf69-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![RMS 錯誤 hello 模型的比較][26]

<span data-ttu-id="7cf69-633">*圖 27.RMS 錯誤 hello 模型的比較。*</span><span class="sxs-lookup"><span data-stu-id="7cf69-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="7cf69-634">從這些結果中，我們看到，加入 hello 季節性因素 toohello 模型可減少 hello RMS 錯誤明顯。</span><span class="sxs-lookup"><span data-stu-id="7cf69-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="7cf69-635">不太令 hello 定型資料的 hello RMS 錯誤元小於 hello 預測。</span><span class="sxs-lookup"><span data-stu-id="7cf69-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="7cf69-636"><a id="appendixa"></a>附錄 a： 指南 tooRStudio</span><span class="sxs-lookup"><span data-stu-id="7cf69-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="7cf69-637">RStudio 已經很完善記載，因此本附錄中，我會提供一些連結 toohello hello RStudio 文件 tooget 您啟動主要區段。</span><span class="sxs-lookup"><span data-stu-id="7cf69-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="7cf69-638">建立專案</span><span class="sxs-lookup"><span data-stu-id="7cf69-638">Creating projects</span></span>
   
   <span data-ttu-id="7cf69-639">您可以使用 RStudio，以專案方式組織和管理您的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7cf69-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="7cf69-640">使用專案的 hello 文件可以位於 https://support.rstudio.com/hc/articles/200526207-Using-Projects。</span><span class="sxs-lookup"><span data-stu-id="7cf69-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="7cf69-641">建議您遵循這些指示，並在此文件中建立 hello R 程式碼範例的專案。</span><span class="sxs-lookup"><span data-stu-id="7cf69-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="7cf69-642">編輯和執行 R 程式碼</span><span class="sxs-lookup"><span data-stu-id="7cf69-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="7cf69-643">RStudio 提供一個可編輯和執行 R 程式碼的整合式環境。</span><span class="sxs-lookup"><span data-stu-id="7cf69-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="7cf69-644">您可以在下列網址找到相關文件：https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code。</span><span class="sxs-lookup"><span data-stu-id="7cf69-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="7cf69-645">Debugging</span><span class="sxs-lookup"><span data-stu-id="7cf69-645">Debugging</span></span>
   
   <span data-ttu-id="7cf69-646">RStudio 包含強大的偵錯功能。</span><span class="sxs-lookup"><span data-stu-id="7cf69-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="7cf69-647">下列網址提供這些功能的相關文件：https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio。</span><span class="sxs-lookup"><span data-stu-id="7cf69-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="7cf69-648">hello 中斷點疑難排解功能會記載於 https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting。</span><span class="sxs-lookup"><span data-stu-id="7cf69-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="7cf69-649"><a id="appendixb"></a>附錄 B：進階閱讀</span><span class="sxs-lookup"><span data-stu-id="7cf69-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="7cf69-650">此 R 程式設計教學課程涵蓋 hello 基本概念的需要 toouse hello 與 Azure Machine Learning Studio 的 R 語言。</span><span class="sxs-lookup"><span data-stu-id="7cf69-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="7cf69-651">如果您不熟悉 R，CRAN 有提供兩本簡介：</span><span class="sxs-lookup"><span data-stu-id="7cf69-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="7cf69-652">為初學者所設計的 Emmanuel Paradis R 是很好的起點 toostart http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf 在。</span><span class="sxs-lookup"><span data-stu-id="7cf69-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="7cf69-653">由 W N 簡介導覽</span><span class="sxs-lookup"><span data-stu-id="7cf69-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="7cf69-654">Venables et. </span><span class="sxs-lookup"><span data-stu-id="7cf69-654">Venables et.</span></span> <span data-ttu-id="7cf69-655">所著的《An Introduction to R》</span><span class="sxs-lookup"><span data-stu-id="7cf69-655">al.</span></span> <span data-ttu-id="7cf69-656">提供略為深入的探討，網址為 http://cran.r-project.org/doc/manuals/R-intro.html。</span><span class="sxs-lookup"><span data-stu-id="7cf69-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="7cf69-657">有許多 R 的相關書籍可以協助您輕鬆上手。</span><span class="sxs-lookup"><span data-stu-id="7cf69-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="7cf69-658">以下是一些我認為實用的書籍：</span><span class="sxs-lookup"><span data-stu-id="7cf69-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="7cf69-659">封面 R 程式設計的 hello: 教學課程的統計軟體設計諾曼 Matloff 是絕佳的簡介 tooprogramming</span><span class="sxs-lookup"><span data-stu-id="7cf69-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="7cf69-660">R Cookbook Paul Teetor 所提供的問題和解決方案方法 toousing。</span><span class="sxs-lookup"><span data-stu-id="7cf69-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="7cf69-661">Robert Kabacoff 所著的《R in Action》是另一本實用的簡介書籍。</span><span class="sxs-lookup"><span data-stu-id="7cf69-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="7cf69-662">hello 附屬快速 R 網站是在 http://www.statmethods.net/ 實用的資源。</span><span class="sxs-lookup"><span data-stu-id="7cf69-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="7cf69-663">由 Patrick Burns R 煉獄是出乎意料幽默的書籍數目 r hello 活頁簿中的程式設計時可能遇到的複雜且困難主題處理是可免費從 http://www.burns-stat.com/documents/books/the-r-inferno/。</span><span class="sxs-lookup"><span data-stu-id="7cf69-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="7cf69-664">如果您想在 R 中的進階主題深入探討，看看 hello 進階 R Hadley Wickham 由活頁簿。</span><span class="sxs-lookup"><span data-stu-id="7cf69-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="7cf69-665">可以免費在 http://adv-r.had.co.nz/ 上這本書的 hello 線上版本。</span><span class="sxs-lookup"><span data-stu-id="7cf69-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="7cf69-666">時間序列的 R 封裝的目錄可以在 hello CRAN 工作檢視時間序列分析： http://cran.r-project.org/web/views/TimeSeries.html。</span><span class="sxs-lookup"><span data-stu-id="7cf69-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="7cf69-667">如需特定的時間序列物件的封裝，您應該參閱 toohello 文件，該套件。</span><span class="sxs-lookup"><span data-stu-id="7cf69-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="7cf69-668">hello 活頁簿與 R Paul Cowpertwait 和 Andrew Metcalfe 簡介時間序列提供時間序列分析簡介 toousing R。</span><span class="sxs-lookup"><span data-stu-id="7cf69-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="7cf69-669">許多理論文本皆有提供 R 範例。</span><span class="sxs-lookup"><span data-stu-id="7cf69-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="7cf69-670">一些絕佳的網際網路資源：</span><span class="sxs-lookup"><span data-stu-id="7cf69-670">Some great internet resources:</span></span>

* <span data-ttu-id="7cf69-671">DataCamp: DataCamp 教導 R hello 舒適度視訊課程與程式碼撰寫練習在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="7cf69-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="7cf69-672">有 hello 最新的 R 技巧和封裝上的互動式教學課程。</span><span class="sxs-lookup"><span data-stu-id="7cf69-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="7cf69-673">在 https://www.datacamp.com/courses/introduction-to-r 拍攝 hello 可用互動式 R 教學課程</span><span class="sxs-lookup"><span data-stu-id="7cf69-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="7cf69-674">有關從 Programiz 開始使用 R 的指南：https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="7cf69-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="7cf69-675">Clarkson 大學 Kelly Black 提供的快速 R 教學課程：http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="7cf69-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="7cf69-676">http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html 列出 60 個以上的 R 資源</span><span class="sxs-lookup"><span data-stu-id="7cf69-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
