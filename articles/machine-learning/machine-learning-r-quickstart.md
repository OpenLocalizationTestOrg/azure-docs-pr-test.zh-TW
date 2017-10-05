---
title: "機器學習適用之 R 語言的快速入門教學課程 | Microsoft Docs"
description: "請透過此 R 程式設計教學課程快速開始搭配 Azure Machine Learning Studio 使用 R 語言來建立預測解決方案。"
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
ms.openlocfilehash: 598f5ce445e520b6cdc347c80f7f3dcbc9c2c9e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="04af9-104">Azure Machine Learning 之 R 程式設計語言的快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="04af9-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="04af9-105">簡介</span><span class="sxs-lookup"><span data-stu-id="04af9-105">Introduction</span></span>
<span data-ttu-id="04af9-106">本快速入門教學課程將協助您使用 R 程式設計語言來快速開始擴充 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="04af9-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="04af9-107">請跟著 R 程式設計教學課程來於 Azure Machine Learning 中建立、測試及執行 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="04af9-108">在您隨著此教學課程進行的過程中，您將在 Azure Machine Learning 中使用 R 語言來建立一個完整的預測解決方案。</span><span class="sxs-lookup"><span data-stu-id="04af9-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="04af9-109">Microsoft Azure Machine Learning 包含許多功能強大的機器學習和資料操作模組。</span><span class="sxs-lookup"><span data-stu-id="04af9-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="04af9-110">功能強大的 R 語言被描述為分析通用語言。</span><span class="sxs-lookup"><span data-stu-id="04af9-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="04af9-111">好消息是，在 Azure Machine Learning 中，分析和資料操作皆可藉由使用 R 來加以擴充。這個組合利用 R 的彈性和深入分析，讓 Azure Machine Learning 更具延展性且更易於部署。</span><span class="sxs-lookup"><span data-stu-id="04af9-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="04af9-112">預測和資料集</span><span class="sxs-lookup"><span data-stu-id="04af9-112">Forecasting and the dataset</span></span>
<span data-ttu-id="04af9-113">預測是一個獲得廣泛採用且相當實用的分析方法。</span><span class="sxs-lookup"><span data-stu-id="04af9-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="04af9-114">常見的用法範圍可從預測季節性項目的銷售額、判斷最佳的庫存量，一直到預測總體經濟變數。</span><span class="sxs-lookup"><span data-stu-id="04af9-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="04af9-115">進行預測時通常是搭配時間序列模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="04af9-116">時間序列資料係指其當中的值具有時間索引的資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="04af9-117">時間索引可以具規則性 (例如每個月或每分鐘) 或不具規則性。</span><span class="sxs-lookup"><span data-stu-id="04af9-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="04af9-118">時間序列模型會根據時間序列資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-118">A time series model is based on time series data.</span></span> <span data-ttu-id="04af9-119">R 程式設計語言包含時間序列資料的彈性架構和廣泛分析。</span><span class="sxs-lookup"><span data-stu-id="04af9-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="04af9-120">在本快速入門指南中，我們將使用加州乳製品產量和訂價資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="04af9-121">此資料包含數項乳製品之產量及奶油 (基準商品) 價格的每月相關資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="04af9-122">本文中使用的資料以及 R 指令碼可[在此下載][download]。</span><span class="sxs-lookup"><span data-stu-id="04af9-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="04af9-123">此資料原先是綜合自威斯康辛大學，網址為 http://future.aae.wisc.edu/tab/production.html。</span><span class="sxs-lookup"><span data-stu-id="04af9-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="04af9-124">組織</span><span class="sxs-lookup"><span data-stu-id="04af9-124">Organization</span></span>
<span data-ttu-id="04af9-125">我們將循序進行數個步驟，讓您了解如何在 Azure Machine Learning 環境中建立、測試及執行分析和資料操作 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="04af9-126">首先，我們將探討在 Azure Machine Learning Studio 環境中使用 R 語言的基本概念。</span><span class="sxs-lookup"><span data-stu-id="04af9-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="04af9-127">然後，我們將接著討論 Azure Machine Learning 環境中資料 I/O、R 程式碼及圖形的各個方面。</span><span class="sxs-lookup"><span data-stu-id="04af9-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="04af9-128">再接著，我們會藉由建立可清理和轉換資料的程式碼，建構預測解決方案的第一個部分。</span><span class="sxs-lookup"><span data-stu-id="04af9-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="04af9-129">在備妥資料後，我們將執行資料集內數個變數之間的相互關聯分析。</span><span class="sxs-lookup"><span data-stu-id="04af9-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="04af9-130">最後，我們將針對牛奶產量建立季節性的時間序列預測模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="04af9-131"><a id="mlstudio"></a>與 Machine Learning Studio 中的 R 語言互動</span><span class="sxs-lookup"><span data-stu-id="04af9-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="04af9-132">本節將帶領您了解在 Machine Learning Studio 環境中與 R 程式設計語言互動的一些基本概念。</span><span class="sxs-lookup"><span data-stu-id="04af9-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="04af9-133">R 語言提供一個功能強大的工具，可在 Azure Machine Learning 環境內建立自訂的分析和資料操作模組。</span><span class="sxs-lookup"><span data-stu-id="04af9-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="04af9-134">我將使用 RStudio 來進行小規模的 R 程式碼開發、測試及偵錯。</span><span class="sxs-lookup"><span data-stu-id="04af9-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="04af9-135">然後，將此程式碼剪下並貼到 Machine Learning Studio 中已準備好要執行的[執行 R 指令碼][execute-r-script]模組中。</span><span class="sxs-lookup"><span data-stu-id="04af9-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="04af9-136">執行 R 指令碼模組</span><span class="sxs-lookup"><span data-stu-id="04af9-136">The Execute R Script module</span></span>
<span data-ttu-id="04af9-137">在 Machine Learning Studio 中，R 指令碼是在[執行 R 指令碼][execute-r-script]模組內執行。</span><span class="sxs-lookup"><span data-stu-id="04af9-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-138">圖 1 顯示 Machine Learning Studio 中[執行 R 指令碼][execute-r-script]模組的範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![R 程式設計語言：在 Machine Learning Studio 中選取的執行 R 指令碼模組。][1]

<span data-ttu-id="04af9-140">*圖 1.顯示已選取 [執行 R 指令碼] 模組的 Machine Learning Studio 環境。*</span><span class="sxs-lookup"><span data-stu-id="04af9-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="04af9-141">參照圖 1，讓我們看看 ML Studio 環境的一些與[執行 R 指令碼][execute-r-script]模組搭配運作的主要部分。</span><span class="sxs-lookup"><span data-stu-id="04af9-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="04af9-142">實驗中的模組會顯示在中間的窗格。</span><span class="sxs-lookup"><span data-stu-id="04af9-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="04af9-143">右窗格的上半部包含一個可檢視和編輯 R 指令碼的視窗。</span><span class="sxs-lookup"><span data-stu-id="04af9-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="04af9-144">右窗格的下半部顯示[執行 R 指令碼][execute-r-script]的一些屬性。</span><span class="sxs-lookup"><span data-stu-id="04af9-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="04af9-145">您可以按一下此窗格上適當的點來檢視錯誤和輸出記錄檔。</span><span class="sxs-lookup"><span data-stu-id="04af9-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="04af9-146">當然，我們將會在這份文件的其餘部分更詳細地討論[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="04af9-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="04af9-147">使用複雜的 R 函式時，建議您在 RStudio 中進行編輯、測試及偵錯。</span><span class="sxs-lookup"><span data-stu-id="04af9-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="04af9-148">與進行任何軟體開發相同，請以累加方式擴充您的程式碼，並在小型的簡單測試案例上進行測試。</span><span class="sxs-lookup"><span data-stu-id="04af9-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="04af9-149">然後，將您的函式剪下並貼到[執行 R 指令碼][execute-r-script]模組的 [R 指令碼] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="04af9-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-150">這個方法既可讓您控制 RStudio 整合式開發環境 (IDE)，也可讓您控制 Azure Machine Learning 的強大功能。</span><span class="sxs-lookup"><span data-stu-id="04af9-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="04af9-151">執行 R 程式碼</span><span class="sxs-lookup"><span data-stu-id="04af9-151">Execute R code</span></span>
<span data-ttu-id="04af9-152">當您按一下 [執行] 按鈕來執行實驗時，將會執行[執行 R 指令碼][execute-r-script]模組中的所有 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="04af9-153">當執行完成時，[執行 R 指令碼][execute-r-script]圖示上將會出現打勾記號。</span><span class="sxs-lookup"><span data-stu-id="04af9-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="04af9-154">Azure Machine Learning 的防禦型 R 編碼</span><span class="sxs-lookup"><span data-stu-id="04af9-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="04af9-155">如果您正在使用 Azure Machine Learning 為 Web 服務開發 R 程式碼，您應該明確地規劃程式碼將如何處理非預期的資料輸入和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="04af9-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="04af9-156">為了清楚起見，在所示範的大多數程式碼中，並未包含太多有關檢查或例外狀況處理的部分。</span><span class="sxs-lookup"><span data-stu-id="04af9-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="04af9-157">不過，隨著我們繼續進行，我將會提供您幾個使用 R 例外狀況處理功能的函式範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="04af9-158">如果您需要更完整的 R 例外狀況處理方式，建議您閱讀 [附錄 B - 進階閱讀](#appendixb)列出之 Wickham 所著書籍中適用的小節。</span><span class="sxs-lookup"><span data-stu-id="04af9-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="04af9-159">在 Machine Learning Studio 中進行 R 程式碼偵錯和測試</span><span class="sxs-lookup"><span data-stu-id="04af9-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="04af9-160">再次提醒您，建議您在 RStudio 中進行小規模的 R 程式碼測試和偵錯。</span><span class="sxs-lookup"><span data-stu-id="04af9-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="04af9-161">不過，會有一些您將必須探究[執行 R 指令碼][execute-r-script]本身 R 程式碼問題的情況。</span><span class="sxs-lookup"><span data-stu-id="04af9-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="04af9-162">此外，在 Machine Learning Studio 中檢查結果也是相當好的做法。</span><span class="sxs-lookup"><span data-stu-id="04af9-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="04af9-163">R 程式碼的執行及在 Azure Machine Learning 平台上的執行所產生的輸出主要都在 output.log 中。</span><span class="sxs-lookup"><span data-stu-id="04af9-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="04af9-164">有些其他資訊會顯示在 error.log 中。</span><span class="sxs-lookup"><span data-stu-id="04af9-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="04af9-165">如果在執行 R 程式碼時，Machine Learning Studio 中發生錯誤，您的第一個行動方針應該是查看 error.log。</span><span class="sxs-lookup"><span data-stu-id="04af9-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="04af9-166">此檔案可能包含可協助您了解並更正錯誤的實用錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="04af9-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="04af9-167">若要檢視 error.log，請針對包含錯誤的[執行 R 指令碼][execute-r-script]，按一下 [屬性] 窗格上的 [檢視錯誤記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="04af9-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="04af9-168">例如，我執行了[執行 R 指令碼][execute-r-script]模組中含有未定義之變數 y 的 下列 R 程式碼：</span><span class="sxs-lookup"><span data-stu-id="04af9-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="04af9-169">此程式碼無法執行，導致發生錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="04af9-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="04af9-170">按一下 [屬性] 窗格上的 [檢視錯誤記錄檔]，便會產生如圖 2 所示的內容：</span><span class="sxs-lookup"><span data-stu-id="04af9-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![錯誤訊息快顯][2]

<span data-ttu-id="04af9-172">*圖 2.錯誤訊息快顯。*</span><span class="sxs-lookup"><span data-stu-id="04af9-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="04af9-173">看來我們必須查看 output.log 來找出 R 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="04af9-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="04af9-174">按一下[執行 R 指令碼][execute-r-script]，然後按一下右邊 [屬性] 窗格上的 [檢視 output.log] 項目。</span><span class="sxs-lookup"><span data-stu-id="04af9-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="04af9-175">新的瀏覽器視窗隨即開啟，我看到下列訊息。</span><span class="sxs-lookup"><span data-stu-id="04af9-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="04af9-176">此錯誤訊息沒有任何出人意料的內容，並且清楚地指出問題所在。</span><span class="sxs-lookup"><span data-stu-id="04af9-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="04af9-177">若要檢查 R 中任何物件的值，您可以將這些值列印至 output.log 檔案中。</span><span class="sxs-lookup"><span data-stu-id="04af9-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="04af9-178">檢查物件值的規則基本上與在互動式 R 工作階段中相同。</span><span class="sxs-lookup"><span data-stu-id="04af9-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="04af9-179">例如，如果您在一行輸入變數名稱，物件的值就會列印至 output.log 檔案中。</span><span class="sxs-lookup"><span data-stu-id="04af9-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="04af9-180">Machine Learning Studio 中的封裝</span><span class="sxs-lookup"><span data-stu-id="04af9-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="04af9-181">Azure Machine Learning 附有超過 350 個預先安裝的 R 語言封裝。</span><span class="sxs-lookup"><span data-stu-id="04af9-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="04af9-182">您可以使用[執行 R 指令碼][execute-r-script]模組中的下列程式碼，來擷取預先安裝的封裝清單。</span><span class="sxs-lookup"><span data-stu-id="04af9-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="04af9-183">如果您目前對此程式碼的最後一行還不了解，請往下閱讀。</span><span class="sxs-lookup"><span data-stu-id="04af9-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="04af9-184">在本文件的其餘部分，我們將大量討論如何在 Azure Machine Learning 環境中使用 R。</span><span class="sxs-lookup"><span data-stu-id="04af9-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="04af9-185">RStudio 簡介</span><span class="sxs-lookup"><span data-stu-id="04af9-185">Introduction to RStudio</span></span>
<span data-ttu-id="04af9-186">RStudio 是一個廣泛使用、適用於 R 的 IDE。我將使用 RStudio 對本快速入門指南中所用的 R 程式碼進行編輯、測試及偵錯。</span><span class="sxs-lookup"><span data-stu-id="04af9-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="04af9-187">測試並備妥 R 程式碼之後，您只要從 RStudio 編輯器剪下並貼到 Machine Learning Studio 的[執行 R 指令碼][execute-r-script]模組中即可。</span><span class="sxs-lookup"><span data-stu-id="04af9-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="04af9-188">如果您的桌上型電腦上並未安裝 R 程式設計語言，建議您現在安裝。</span><span class="sxs-lookup"><span data-stu-id="04af9-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="04af9-189">您可以從 Comprehensive R Archive Network (或稱為 CRAN) 免費下載開放原始碼 R 語言，網址為 [http://www.r-project.org/](http://www.r-project.org/)。</span><span class="sxs-lookup"><span data-stu-id="04af9-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="04af9-190">有提供適用於 Windows、MacOS 及 Linux/UNIX 的下載項目。</span><span class="sxs-lookup"><span data-stu-id="04af9-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="04af9-191">請選擇附近的鏡像，然後依照下載指示進行。</span><span class="sxs-lookup"><span data-stu-id="04af9-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="04af9-192">此外，CRAN 也包含大量實用的分析和資料操作封裝。</span><span class="sxs-lookup"><span data-stu-id="04af9-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="04af9-193">如果您是 RStudio 新手，您應該下載並安裝桌上型電腦版本。</span><span class="sxs-lookup"><span data-stu-id="04af9-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="04af9-194">您可以在 http://www.rstudio.com/products/RStudio/ 找到適用於 Windows、Mac OS 及 Linux/UNIX 的 RStudio 下載項目。</span><span class="sxs-lookup"><span data-stu-id="04af9-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="04af9-195">請依照提供的指示，在您的桌上型電腦上安裝 RStudio。</span><span class="sxs-lookup"><span data-stu-id="04af9-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="04af9-196">https://support.rstudio.com/hc/sections/200107586-Using-RStudio 有提供 RStudio 的教學課程簡介。</span><span class="sxs-lookup"><span data-stu-id="04af9-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="04af9-197">我在[附錄 A][appendixa] 中提供了一些使用 RStudio 的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="04af9-198"><a id="scriptmodule"></a>將資料輸入執行 R 指令碼模組及從此模組輸出</span><span class="sxs-lookup"><span data-stu-id="04af9-198"><a id="scriptmodule"></a>Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="04af9-199">在本節中，我們將討論如何將資料輸入[執行 R 指令碼][execute-r-script]模組及從此模組輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-200">我們將回顧如何處理讀入[執行 R 指令碼][execute-r-script]模組及從此模組讀出的各種資料類型。</span><span class="sxs-lookup"><span data-stu-id="04af9-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="04af9-201">您稍早下載的 Zip 檔案中有本節的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="04af9-202">在 Machine Learning Studio 中載入和檢查資料</span><span class="sxs-lookup"><span data-stu-id="04af9-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="04af9-203"><a id="loading"></a>載入資料集</span><span class="sxs-lookup"><span data-stu-id="04af9-203"><a id="loading"></a>Load the dataset</span></span>
<span data-ttu-id="04af9-204">我們將從把 **csdairydata.csv** 檔案載入到 Azure Learning Studio 中開始。</span><span class="sxs-lookup"><span data-stu-id="04af9-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="04af9-205">啟動 Azure Machine Learning Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="04af9-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="04af9-206">按一下畫面左下方的 [+ 新增]，然後選取 [資料集]。</span><span class="sxs-lookup"><span data-stu-id="04af9-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="04af9-207">選取 [從本機檔案]，然後按一下 [瀏覽] 以選取檔案。</span><span class="sxs-lookup"><span data-stu-id="04af9-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="04af9-208">請確定您已選取 **含標頭的一般 CSV 檔案 (.csv)** 做為資料集類型。</span><span class="sxs-lookup"><span data-stu-id="04af9-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="04af9-209">按一下核取記號。</span><span class="sxs-lookup"><span data-stu-id="04af9-209">Click the check mark.</span></span>
* <span data-ttu-id="04af9-210">上傳資料集後，按一下 [資料集]  索引標籤，您應該會看到新的資料集。</span><span class="sxs-lookup"><span data-stu-id="04af9-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="04af9-211">建立實驗</span><span class="sxs-lookup"><span data-stu-id="04af9-211">Create an experiment</span></span>
<span data-ttu-id="04af9-212">既然我們在 Machine Learning Studio 中已經有一些資料，我們需要建立一個實驗來執行分析。</span><span class="sxs-lookup"><span data-stu-id="04af9-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="04af9-213">按一下左下方的 [+ 新增] 並選取 [實驗]，然後選取 [空白實驗]。</span><span class="sxs-lookup"><span data-stu-id="04af9-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="04af9-214">您可以選取和修改頁面頂端的 **實驗建立目的** 標題，為您的實驗命名。</span><span class="sxs-lookup"><span data-stu-id="04af9-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="04af9-215">例如，將它變更為「加州乳製品分析」 。</span><span class="sxs-lookup"><span data-stu-id="04af9-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="04af9-216">在實驗頁面左側展開 [儲存的資料集]，然後選取 [我的資料集]。</span><span class="sxs-lookup"><span data-stu-id="04af9-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="04af9-217">您應該會看到先前上傳的 **cadairydata.csv** 檔案。</span><span class="sxs-lookup"><span data-stu-id="04af9-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="04af9-218">將 [ **csdairydata.csv 資料集** ] 拖放到實驗上。</span><span class="sxs-lookup"><span data-stu-id="04af9-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="04af9-219">在左窗格頂端的 [搜尋實驗項目] 方塊中，輸入[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="04af9-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="04af9-220">您會看到該模組出現在搜尋清單中。</span><span class="sxs-lookup"><span data-stu-id="04af9-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="04af9-221">將[執行 R 指令碼][execute-r-script]模組拖放到您的選盤上。</span><span class="sxs-lookup"><span data-stu-id="04af9-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="04af9-222">將 [csdairydata.csv 資料集] 的輸出連接到[執行 R 指令碼][execute-r-script]最左邊的輸入 (**資料集1**)。</span><span class="sxs-lookup"><span data-stu-id="04af9-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="04af9-223">**別忘了按一下 [儲存]！**</span><span class="sxs-lookup"><span data-stu-id="04af9-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="04af9-224">此時，您的實驗應該會看起來像圖 3。</span><span class="sxs-lookup"><span data-stu-id="04af9-224">At this point your experiment should look something like Figure 3.</span></span>

![含有資料集和 [執行 R 指令碼] 模組的「加州乳製品分析實驗」][3]

<span data-ttu-id="04af9-226">*圖 3.含有資料集和 [執行 R 指令碼] 模組的「加州乳製品分析實驗」。*</span><span class="sxs-lookup"><span data-stu-id="04af9-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="04af9-227">檢查資料</span><span class="sxs-lookup"><span data-stu-id="04af9-227">Check on the data</span></span>
<span data-ttu-id="04af9-228">讓我們看看已載入到實驗中的資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="04af9-229">在此實驗中，按一下 [cadairydata.csv 資料集] 的輸出，然後選取 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="04af9-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="04af9-230">您應該會看到類似圖 4 的內容。</span><span class="sxs-lookup"><span data-stu-id="04af9-230">You should see something like Figure 4.</span></span>  

![cadairydata.csv 資料集的摘要][4]

<span data-ttu-id="04af9-232">*圖 4：cadairydata.csv 資料集的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="04af9-233">在這個檢視中，我們會看到許多有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="04af9-234">我們可以看到該資料集的前幾列。</span><span class="sxs-lookup"><span data-stu-id="04af9-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="04af9-235">如果我們選取資料行，[統計資料] 區段會顯示有關資料行的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="04af9-236">例如，[功能類型] 資料列顯示 Azure Machine Learning Studio 指派給各資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="04af9-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="04af9-237">擁有一個類似這樣的快速檢視，對於開始執行任何正式工作來說，是相當好的執行前例行性檢查。</span><span class="sxs-lookup"><span data-stu-id="04af9-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="04af9-238">第一個 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="04af9-238">First R script</span></span>
<span data-ttu-id="04af9-239">讓我們建立第一個要在 Azure Machine Learning Studio 中實驗的簡單 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="04af9-240">我已在 RStudio 中建立並測試下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="04af9-241">現在，我需要將此指令碼轉移到 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="04af9-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="04af9-242">我可以只利用剪下並貼上。</span><span class="sxs-lookup"><span data-stu-id="04af9-242">I could simply cut and paste.</span></span> <span data-ttu-id="04af9-243">不過，在此案例中，我將透過 Zip 檔案轉移我的 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="04af9-244">執行 R 指令碼模組的資料輸入</span><span class="sxs-lookup"><span data-stu-id="04af9-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="04af9-245">讓我們看看[執行 R 指令碼][execute-r-script]模組的輸入。</span><span class="sxs-lookup"><span data-stu-id="04af9-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-246">在此範例中，我們將會把加州乳製品資料讀入[執行 R 指令碼][execute-r-script]模組中。</span><span class="sxs-lookup"><span data-stu-id="04af9-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="04af9-247">[執行 R 指令碼][execute-r-script]模組有三個可能的輸入。</span><span class="sxs-lookup"><span data-stu-id="04af9-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-248">視您的應用方式而定，您可以使用這當中的任何一個或所有輸入。</span><span class="sxs-lookup"><span data-stu-id="04af9-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="04af9-249">使用不接受任何輸入的 R 指令碼也是十分合理的。</span><span class="sxs-lookup"><span data-stu-id="04af9-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="04af9-250">讓我們從左到右看看這當中的每一個輸入。</span><span class="sxs-lookup"><span data-stu-id="04af9-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="04af9-251">您可以將游標放到輸入上方並閱讀工具提示，來查看每個輸入的名稱。</span><span class="sxs-lookup"><span data-stu-id="04af9-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="04af9-252">指令碼組合</span><span class="sxs-lookup"><span data-stu-id="04af9-252">Script Bundle</span></span>
<span data-ttu-id="04af9-253">「指令碼組合」輸入可讓您將 Zip 檔案的內容傳入到[執行 R 指令碼][execute-r-script]模組中。</span><span class="sxs-lookup"><span data-stu-id="04af9-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-254">您可以使用下列其中一個命令將 Zip 檔案的內容讀入到 R 程式碼中。</span><span class="sxs-lookup"><span data-stu-id="04af9-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="04af9-255">Azure Machine Learning 會將 Zip 中的檔案視為在 src/ 目錄中，因此您必須在您的檔案名稱前面加上此目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="04af9-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="04af9-256">例如，如果 Zip 在其根目錄中包含檔案 `yourfile.R` 和 `yourData.rdata`，使用 `source` 和 `load` 時，您會將這些處理為 `src/yourfile.R` 和 `src/yourData.rdata`。</span><span class="sxs-lookup"><span data-stu-id="04af9-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="04af9-257">我們已經在[載入資料集](#loading)中討論過如何載入資料集。</span><span class="sxs-lookup"><span data-stu-id="04af9-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="04af9-258">在您建立並測試上一節中所示的 R 指令碼之後，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="04af9-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="04af9-259">將 R 指令碼儲存成 .R 檔案。</span><span class="sxs-lookup"><span data-stu-id="04af9-259">Save the R script into a .R file.</span></span> <span data-ttu-id="04af9-260">我將我的指令碼檔案稱為 "simpleplot.R"。</span><span class="sxs-lookup"><span data-stu-id="04af9-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="04af9-261">內容如下。</span><span class="sxs-lookup"><span data-stu-id="04af9-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="04af9-262">建立一個 Zip 檔案，然後將您的指令碼複製到此 Zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="04af9-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="04af9-263">在 Windows 中，您可以用滑鼠右鍵按一下檔案，選取 [傳送到]、[壓縮的 (zipped) 資料夾]。</span><span class="sxs-lookup"><span data-stu-id="04af9-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="04af9-264">這會建立包含 "simpleplot.R" 檔案的新 Zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="04af9-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="04af9-265">將您的檔案新增到 Machine Learning Studio 中的 [資料集]，並將類型指定為 **zip**。</span><span class="sxs-lookup"><span data-stu-id="04af9-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="04af9-266">您現在應該會在您的資料集內看到的此 Zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="04af9-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="04af9-267">將此 Zip 檔案從 [資料集] 拖放到 **ML Studio 畫布**上。</span><span class="sxs-lookup"><span data-stu-id="04af9-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="04af9-268">將 [Zip 資料] 圖示的輸出連接到[執行 R 指令碼][execute-r-script]模組的 [指令碼組合] 輸入。</span><span class="sxs-lookup"><span data-stu-id="04af9-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="04af9-269">在[執行 R 指令碼][execute-r-script]模組的程式碼視窗中，輸入含有您 Zip 檔案名稱的 `source()` 函式。</span><span class="sxs-lookup"><span data-stu-id="04af9-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-270">在我的案例中，我鍵入了 `source("src/simpleplot.R")`。</span><span class="sxs-lookup"><span data-stu-id="04af9-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="04af9-271">確定按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="04af9-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="04af9-272">完成這些步驟之後，[執行 R 指令碼][execute-r-script]模組就會在實驗執行時，執行 Zip 檔案中的 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="04af9-273">此時，您的實驗應該會看起來像圖 5。</span><span class="sxs-lookup"><span data-stu-id="04af9-273">At this point your experiment should look something like Figure 5.</span></span>

![使用已壓縮之 R 指令碼的實驗][6]

<span data-ttu-id="04af9-275">*圖 5.使用已壓縮之 R 指令碼的實驗。*</span><span class="sxs-lookup"><span data-stu-id="04af9-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="04af9-276">資料集1</span><span class="sxs-lookup"><span data-stu-id="04af9-276">Dataset1</span></span>
<span data-ttu-id="04af9-277">您可以使用 [資料集1] 輸入將矩形資料表傳遞給您的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="04af9-278">在我們的簡單指令碼中， `maml.mapInputPort(1)` 函式會從連接埠 1 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="04af9-279">此資料會接著被指派給您程式碼中的資料框架變數名稱。</span><span class="sxs-lookup"><span data-stu-id="04af9-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="04af9-280">在我們的簡單指令碼中，第一行程式碼會執行這項指派。</span><span class="sxs-lookup"><span data-stu-id="04af9-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="04af9-281">請按一下 [ **執行** ] 按鈕來執行您的實驗。</span><span class="sxs-lookup"><span data-stu-id="04af9-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="04af9-282">執行完成時，請按一下[執行 R 指令碼][execute-r-script]模組，然後按一下 [屬性] 窗格上的 [檢視輸出記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="04af9-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="04af9-283">您的瀏覽器中應該會出現一個新頁面，當中顯示 output.log 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="04af9-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="04af9-284">當您向下捲動時，您應該會看到類似下列的內容。</span><span class="sxs-lookup"><span data-stu-id="04af9-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="04af9-285">頁面更下方有更詳細的資料行資訊，看起來與下列類似。</span><span class="sxs-lookup"><span data-stu-id="04af9-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

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

<span data-ttu-id="04af9-286">這些結果大致上如預期，資料框架中有 228 個觀察值和 9 個資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="04af9-287">我們可以看到資料行名稱、R 資料類型及每個資料行的範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="04af9-288">從[執行 R 指令碼][execute-r-script]模組的 [R 裝置] 輸出可以便利地取得這個相同的列印輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-289">我們將在下一節中討論[執行 R 指令碼][execute-r-script]模組的輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="04af9-290">資料集2</span><span class="sxs-lookup"><span data-stu-id="04af9-290">Dataset2</span></span>
<span data-ttu-id="04af9-291">[資料集2] 輸入的行為與 [資料集1] 的行為相同。</span><span class="sxs-lookup"><span data-stu-id="04af9-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="04af9-292">您可以使用此輸入將第二個矩形資料表傳遞給您的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="04af9-293">含有引數 2 的函式 `maml.mapInputPort(2)`可用來傳遞此資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="04af9-294">執行 R 指令碼輸出</span><span class="sxs-lookup"><span data-stu-id="04af9-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="04af9-295">輸出資料框架</span><span class="sxs-lookup"><span data-stu-id="04af9-295">Output a dataframe</span></span>
<span data-ttu-id="04af9-296">您可以使用 `maml.mapOutputPort()` 函式，透過 [結果資料集1] 連接埠將 R 資料框架的內容輸出成矩形資料表。</span><span class="sxs-lookup"><span data-stu-id="04af9-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="04af9-297">在我們的簡單 R 指令碼中，會由下列程式碼行執行此動作。</span><span class="sxs-lookup"><span data-stu-id="04af9-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="04af9-298">執行實驗之後，請按一下 [結果資料集1] 輸出連接埠，然後按一下 [ **視覺化**]。</span><span class="sxs-lookup"><span data-stu-id="04af9-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="04af9-299">您應該會看到類似圖 6 的內容。</span><span class="sxs-lookup"><span data-stu-id="04af9-299">You should see something like Figure 6.</span></span>

![加州乳製品資料的輸出視覺化][7]

<span data-ttu-id="04af9-301">*圖 6.加州乳製品資料的輸出視覺化。*</span><span class="sxs-lookup"><span data-stu-id="04af9-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="04af9-302">此輸出看起來與輸入相同，完全如我們的預期。</span><span class="sxs-lookup"><span data-stu-id="04af9-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="04af9-303">R 裝置輸出</span><span class="sxs-lookup"><span data-stu-id="04af9-303">R Device output</span></span>
<span data-ttu-id="04af9-304">[執行 R 指令碼][execute-r-script]模組的 [裝置] 輸出包含訊息和圖形輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="04af9-305">來自 R 的標準輸出和標準錯誤訊息都會傳送到 [R 裝置] 輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="04af9-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="04af9-306">若要檢視 [R 裝置] 輸出，請按一下該連接埠，然後按一下 [ **視覺化**]。</span><span class="sxs-lookup"><span data-stu-id="04af9-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="04af9-307">我們會看到如圖 7 中來自 R 指令碼的標準輸出和標準錯誤。</span><span class="sxs-lookup"><span data-stu-id="04af9-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![來自 [R 裝置] 連接埠的標準輸出和標準誤差][8]

<span data-ttu-id="04af9-309">*圖 7.來自 [R 裝置] 連接埠的標準輸出和標準錯誤。*</span><span class="sxs-lookup"><span data-stu-id="04af9-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="04af9-310">向下捲動之後，我們會看到如圖 8 中來自 R 指令碼的圖形輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![來自 [R 裝置] 連接埠的圖形輸出][9]

<span data-ttu-id="04af9-312">*圖 8.來自 [R 裝置] 連接埠的圖形輸出。*</span><span class="sxs-lookup"><span data-stu-id="04af9-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <span data-ttu-id="04af9-313"><a id="filtering"></a>資料篩選和轉換</span><span class="sxs-lookup"><span data-stu-id="04af9-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="04af9-314">在本節中，我們將對加州乳製品資料執行一些基本的資料篩選和轉換操作。</span><span class="sxs-lookup"><span data-stu-id="04af9-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="04af9-315">在本節的結尾，我們將會以適用於建置分析模型的格式備妥資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="04af9-316">更具體來說，在本節中，我們將會執行數個常見的資料清除和轉換工作：類型轉換、依據資料框架進行篩選、新增新的計算資料行，以及值轉換。</span><span class="sxs-lookup"><span data-stu-id="04af9-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="04af9-317">此背景應該可以協助您處理在真實世界問題中遇到的許多變化。</span><span class="sxs-lookup"><span data-stu-id="04af9-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="04af9-318">您稍早下載的 Zip 檔案中有本節的完整 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="04af9-319">類型轉換</span><span class="sxs-lookup"><span data-stu-id="04af9-319">Type transformations</span></span>
<span data-ttu-id="04af9-320">既然我們可以將加州乳製品資料讀入到[執行 R 指令碼][execute-r-script]模組的 R 程式碼中，我們需要確保資料行中的資料具有預期的類型和格式。</span><span class="sxs-lookup"><span data-stu-id="04af9-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="04af9-321">R 是動態指定類型的語言，這表示會視需要強制將資料類型從一種類型轉換成另一種類型。</span><span class="sxs-lookup"><span data-stu-id="04af9-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="04af9-322">R 中不可部分完成的資料類型包括數值、邏輯及字元。</span><span class="sxs-lookup"><span data-stu-id="04af9-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="04af9-323">因素類型可用來簡潔地儲存分類資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="04af9-324">您可以在 [附錄 B - 進階閱讀](#appendixb)的參考內容中，找到更多有關資料類型的資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="04af9-325">將表格式資料從外部來源讀入到 R 中時，最好一律檢查資料行中產生的類型。</span><span class="sxs-lookup"><span data-stu-id="04af9-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="04af9-326">您可能想要字元類型的資料行，但在許多情況下這會顯示為因素類型，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="04af9-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="04af9-327">在其他情況下，則是會以字元資料代表您認為應該是數值的資料行，例如 '1.23' 而非浮點數形式的 1.23。</span><span class="sxs-lookup"><span data-stu-id="04af9-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="04af9-328">幸運的是，只要能夠對應，將一個類型轉換成另一個類型相當容易。</span><span class="sxs-lookup"><span data-stu-id="04af9-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="04af9-329">例如，您無法將 'Nevada' 轉換成數值，但是可以將它轉換成因素 (類別變數)。</span><span class="sxs-lookup"><span data-stu-id="04af9-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="04af9-330">另舉一例，您可以將數值 1 轉換成字元 '1' 或因素。</span><span class="sxs-lookup"><span data-stu-id="04af9-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="04af9-331">任何這些轉換的語法都很簡單： `as.datatype()`。</span><span class="sxs-lookup"><span data-stu-id="04af9-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="04af9-332">這些類型轉換函式包括：</span><span class="sxs-lookup"><span data-stu-id="04af9-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="04af9-333">看看我們在上一節中輸入之資料行的資料類型：除了標示為 'Month' 的資料行為字元類型之外，所有資料行的類型都是數值。</span><span class="sxs-lookup"><span data-stu-id="04af9-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="04af9-334">讓我們將其轉換成因素，然後測試結果。</span><span class="sxs-lookup"><span data-stu-id="04af9-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="04af9-335">我已經刪除建立散佈圖矩陣的程式碼行，並新增將 'Month' 資料行轉換成因素的程式碼行。</span><span class="sxs-lookup"><span data-stu-id="04af9-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="04af9-336">在我的實驗中，我將只是把 R 程式碼剪下並貼到[執行 R 指令碼][execute-r-script]模組的程式碼視窗中。</span><span class="sxs-lookup"><span data-stu-id="04af9-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="04af9-337">您也可以更新 Zip 檔案，然後將它上傳到 Azure Machine Learning Studio，但這需要數個步驟。</span><span class="sxs-lookup"><span data-stu-id="04af9-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="04af9-338">讓我們執行這個程式碼並查看 R 指令碼的輸出記錄檔。</span><span class="sxs-lookup"><span data-stu-id="04af9-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="04af9-339">圖 9 顯示來自記錄檔的相關資料。</span><span class="sxs-lookup"><span data-stu-id="04af9-339">The relevant data from the log is shown in Figure 9.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="04af9-340">*圖 9.含有因素變數之資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="04af9-341">Month 的類型現在應該會表示為  '**Factor w/ 14 levels**'。</span><span class="sxs-lookup"><span data-stu-id="04af9-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="04af9-342">這會發生問題，因為一年只有 12 個月。</span><span class="sxs-lookup"><span data-stu-id="04af9-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="04af9-343">您也可以在 [結果資料集] 連接埠的 [視覺化] 中，檢查類型是否為 '**Categorical**'。</span><span class="sxs-lookup"><span data-stu-id="04af9-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="04af9-344">問題在於 'Month' 資料行的程式碼並非以有系統的方式撰寫。</span><span class="sxs-lookup"><span data-stu-id="04af9-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="04af9-345">在某些情況下，某個月份稱為 April ，在其他情況下則會縮寫成 Apr。我們可以將字串修剪成 3 個字元來解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="04af9-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="04af9-346">這行程式碼現在看起來如下：</span><span class="sxs-lookup"><span data-stu-id="04af9-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="04af9-347">重新執行實驗和檢視輸出記錄檔。</span><span class="sxs-lookup"><span data-stu-id="04af9-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="04af9-348">圖 10 顯示預期的結果。</span><span class="sxs-lookup"><span data-stu-id="04af9-348">The expected results are shown in Figure 10.</span></span>  

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="04af9-349">*圖 10.因素層級數目正確之資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="04af9-350">我們的因素變數現在具有所需的 12 個層級。</span><span class="sxs-lookup"><span data-stu-id="04af9-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="04af9-351">基本資料框架篩選</span><span class="sxs-lookup"><span data-stu-id="04af9-351">Basic data frame filtering</span></span>
<span data-ttu-id="04af9-352">R 資料框架支援強大的篩選功能。</span><span class="sxs-lookup"><span data-stu-id="04af9-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="04af9-353">藉由在資料列或資料行使用邏輯篩選，可將資料集再細分成子集。</span><span class="sxs-lookup"><span data-stu-id="04af9-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="04af9-354">在許多情況下，將會需要複雜的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="04af9-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="04af9-355">[附錄 B - 進階閱讀](#appendixb) 中的參考包含大量的篩選資料框架範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="04af9-356">有一些篩選是我們應該在資料集上執行的。</span><span class="sxs-lookup"><span data-stu-id="04af9-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="04af9-357">如果您看一下 cadariydata 資料框架中的資料行，您會看到兩個不必要的資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="04af9-358">第一個資料行只存放了資料列編號，這不是很有用。</span><span class="sxs-lookup"><span data-stu-id="04af9-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="04af9-359">第二個資料行 Year.Month 包含重複的資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="04af9-360">我們可以使用下列 R 程式碼輕鬆地排除這些資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="04af9-361">從現在起，在本節中，我將只會示範要在[執行 R 指令碼][execute-r-script]模組中新增的額外程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="04af9-362">我會在 `str()` 函式**之前**新增每個新程式碼行。</span><span class="sxs-lookup"><span data-stu-id="04af9-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="04af9-363">我會使用此函式在 Azure Machine Learning Studio 中確認我的結果。</span><span class="sxs-lookup"><span data-stu-id="04af9-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="04af9-364">我在[執行 R 指令碼][execute-r-script]模組的 R 程式碼中新增下列程式碼行。</span><span class="sxs-lookup"><span data-stu-id="04af9-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="04af9-365">在您的實驗中執行此程式碼，並檢查輸出記錄檔的結果。</span><span class="sxs-lookup"><span data-stu-id="04af9-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="04af9-366">這些結果如圖 11 所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-366">These results are shown in Figure 11.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="04af9-367">*圖 11.已移除兩個資料行之資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="04af9-368">好消息！</span><span class="sxs-lookup"><span data-stu-id="04af9-368">Good news!</span></span> <span data-ttu-id="04af9-369">我們得到預期的結果。</span><span class="sxs-lookup"><span data-stu-id="04af9-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="04af9-370">加入新的資料行</span><span class="sxs-lookup"><span data-stu-id="04af9-370">Add a new column</span></span>
<span data-ttu-id="04af9-371">若要建立時間序列模型，讓資料行包含自時間序列開始後的月份將會比較方便。</span><span class="sxs-lookup"><span data-stu-id="04af9-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="04af9-372">我們將會建立新資料行 'Month.Count'。</span><span class="sxs-lookup"><span data-stu-id="04af9-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="04af9-373">為了協助組織程式碼，我們將建立我們的第一個簡單函式 `num.month()`。</span><span class="sxs-lookup"><span data-stu-id="04af9-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="04af9-374">然後，我們會套用此函式在資料框架中建立新資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="04af9-375">新程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="04af9-376">現在，執行更新的實驗並使用輸出記錄檔來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="04af9-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="04af9-377">這些結果如圖 12 所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-377">These results are shown in Figure 12.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="04af9-378">*圖 12.含有其他資料行之資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="04af9-379">看來一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="04af9-379">It looks like everything is working.</span></span> <span data-ttu-id="04af9-380">我們的資料框架中有了包含預期值的新資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="04af9-381">值轉換</span><span class="sxs-lookup"><span data-stu-id="04af9-381">Value transformations</span></span>
<span data-ttu-id="04af9-382">在本節中，我們將對資料框架之某些資料行中的值執行一些簡單的轉換。</span><span class="sxs-lookup"><span data-stu-id="04af9-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="04af9-383">R 語言幾乎支援任何一種值轉換。</span><span class="sxs-lookup"><span data-stu-id="04af9-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="04af9-384">[附錄 B - 進階閱讀](#appendixb) 中的參考包含大量範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="04af9-385">如果您看看我們資料框架摘要中的值，您應該會發現此處有點奇怪。</span><span class="sxs-lookup"><span data-stu-id="04af9-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="04af9-386">加州生產的冰淇淋比牛奶多？</span><span class="sxs-lookup"><span data-stu-id="04af9-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="04af9-387">否，當然不是，因為這樣並不合理，雖然這對我們當中的一些冰淇淋愛好者來說是個令人悲傷的事實。</span><span class="sxs-lookup"><span data-stu-id="04af9-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="04af9-388">其單位並不相同。</span><span class="sxs-lookup"><span data-stu-id="04af9-388">The units are different.</span></span> <span data-ttu-id="04af9-389">計價單位為美制磅，牛奶是以 100 萬美制磅為單位、冰淇淋是以 1,000 美制加侖為單位，而卡達乾酪則是以 1,000 美制磅為單位。</span><span class="sxs-lookup"><span data-stu-id="04af9-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="04af9-390">假設冰淇淋每加侖重約 6.5 磅，我們便可輕鬆地進行乘法運算來轉換這些值，讓它們都同樣以 1000 磅為單位。</span><span class="sxs-lookup"><span data-stu-id="04af9-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="04af9-391">針對我們的預測模型，我們使用乘法模型來進行此資料的趨勢和季節性調整。</span><span class="sxs-lookup"><span data-stu-id="04af9-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="04af9-392">對數轉換可讓我們使用線性模型，以簡化此程序。</span><span class="sxs-lookup"><span data-stu-id="04af9-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="04af9-393">我們可以在套用乘數的相同函式中套用對數轉換。</span><span class="sxs-lookup"><span data-stu-id="04af9-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="04af9-394">在下列程式碼中，我定義了新函式 `log.transform()`，並將它套用至包含數值的資料列。</span><span class="sxs-lookup"><span data-stu-id="04af9-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="04af9-395">R `Map()` 函式可用來將 `log.transform()` 函式套用至資料框架中的所選資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="04af9-396">`Map()` 與 `apply()` 類似，但可允許函式有多個引數清單。</span><span class="sxs-lookup"><span data-stu-id="04af9-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="04af9-397">請注意，乘數清單會提供 `log.transform()` 函式的第二個引數。</span><span class="sxs-lookup"><span data-stu-id="04af9-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="04af9-398">`na.omit()` 函式是用來進行一點清除，以確保我們在資料框架中沒有遺失或未定義的值。</span><span class="sxs-lookup"><span data-stu-id="04af9-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="04af9-399">`log.transform()` 函式中進行的事情不少。</span><span class="sxs-lookup"><span data-stu-id="04af9-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="04af9-400">此程式碼中大部分會檢查引數的潛在問題，或是處理仍可能在計算期間發生的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="04af9-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="04af9-401">此程式碼中實際上只有幾行在進行計算。</span><span class="sxs-lookup"><span data-stu-id="04af9-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="04af9-402">防禦型程式設計的目標，是要防止因單一函式失敗而導致無法繼續處理的情況。</span><span class="sxs-lookup"><span data-stu-id="04af9-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="04af9-403">執行很久的分析如果突然失敗，可能會讓使用者深感挫折。</span><span class="sxs-lookup"><span data-stu-id="04af9-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="04af9-404">為了避免這種情況，必須選擇預設的傳回值，以將損害限制在下游處理。</span><span class="sxs-lookup"><span data-stu-id="04af9-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="04af9-405">系統也會產生訊息來警示使用者發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="04af9-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="04af9-406">如果您不熟悉使用 R 進行防禦型程式設計，此程式碼的一切可能會讓您不知所措。</span><span class="sxs-lookup"><span data-stu-id="04af9-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="04af9-407">我將引導您完成主要的步驟：</span><span class="sxs-lookup"><span data-stu-id="04af9-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="04af9-408">定義包含四個訊息的向量。</span><span class="sxs-lookup"><span data-stu-id="04af9-408">A vector of four messages is defined.</span></span> <span data-ttu-id="04af9-409">這些訊息用來傳達一些可能在此程式碼發生的錯誤和例外狀況的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="04af9-410">我會針對每個案例傳回一個 NA 值。</span><span class="sxs-lookup"><span data-stu-id="04af9-410">I return a value of NA for each case.</span></span> <span data-ttu-id="04af9-411">有許多其他可能會有較少副作用的可能性。</span><span class="sxs-lookup"><span data-stu-id="04af9-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="04af9-412">例如，我可以傳回零向量或原始輸入向量。</span><span class="sxs-lookup"><span data-stu-id="04af9-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="04af9-413">對函式的引數執行檢查。</span><span class="sxs-lookup"><span data-stu-id="04af9-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="04af9-414">在每個案例中，如果偵測到錯誤，便會傳回預設值，並且由 `warning()` 函式產生訊息。</span><span class="sxs-lookup"><span data-stu-id="04af9-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="04af9-415">我使用的是 `warning()` 而非 `stop()`，因為後者會終止執行，而這正是我試著要避免的情況。</span><span class="sxs-lookup"><span data-stu-id="04af9-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="04af9-416">請注意，我是以程序性風格撰寫此程式碼，因此在此情況下，函式型方法看似既複雜又難以理解。</span><span class="sxs-lookup"><span data-stu-id="04af9-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="04af9-417">對數計算被包裝在 `tryCatch()` 中，如此例外狀況就不會導致處理突然停止。</span><span class="sxs-lookup"><span data-stu-id="04af9-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="04af9-418">如果沒有 `tryCatch()` ，R 函式所引發的大多數錯誤都會導致產生停止訊號，而此訊號所執行的就是停止。</span><span class="sxs-lookup"><span data-stu-id="04af9-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="04af9-419">請在您的實驗中執行此 R 程式碼，然後看看 output.log 檔案中的列印輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="04af9-420">您現在會在記錄中看到四個資料行的已轉換值，如圖 13 所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="04af9-421">*圖 13.資料框架中已轉換之值的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="04af9-422">我們會看到值已經轉換。</span><span class="sxs-lookup"><span data-stu-id="04af9-422">We see the values have been transformed.</span></span> <span data-ttu-id="04af9-423">現在，牛奶產量大幅超過所有其他乳製品產量，還記得我們現在看的是對數刻度。</span><span class="sxs-lookup"><span data-stu-id="04af9-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="04af9-424">此時會清除我們的資料，而我們已經準備好進行一些建立模型工作。</span><span class="sxs-lookup"><span data-stu-id="04af9-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="04af9-425">看看[執行 R 指令碼][execute-r-script]模組之 [結果資料集] 輸出的視覺化摘要，您會看到 'Month' 資料行是 'Categorical' 並具有 12 個唯一值，這又再次是我們所想要的。</span><span class="sxs-lookup"><span data-stu-id="04af9-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="04af9-426"><a id="timeseries"></a>時間序列物件和相互關聯分析</span><span class="sxs-lookup"><span data-stu-id="04af9-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="04af9-427">在本節中，我們將探討一些基本的 R 時間序列物件，並分析一些變數之間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="04af9-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="04af9-428">我們的目標是要輸出資料框架，此框架中包含數段延隔時間的成對相互關聯資訊。</span><span class="sxs-lookup"><span data-stu-id="04af9-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="04af9-429">您稍早下載的 Zip 檔中有本節的完整 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="04af9-430">R 中的時間序列物件</span><span class="sxs-lookup"><span data-stu-id="04af9-430">Time series objects in R</span></span>
<span data-ttu-id="04af9-431">如已經提過的，時間序列是一系列依時間編制索引的資料值。</span><span class="sxs-lookup"><span data-stu-id="04af9-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="04af9-432">R 時間序列物件可用來建立和管理時間索引。</span><span class="sxs-lookup"><span data-stu-id="04af9-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="04af9-433">使用時間序列物件有數個優點。</span><span class="sxs-lookup"><span data-stu-id="04af9-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="04af9-434">時間序列物件可讓您不必理會管理封裝在物件中之時間序列索引值的許多細節。</span><span class="sxs-lookup"><span data-stu-id="04af9-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="04af9-435">此外，時間序列物件還可讓您使用許多時間序列方法來繪製、列印、建立模型等。</span><span class="sxs-lookup"><span data-stu-id="04af9-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="04af9-436">POSIXct 時間序列類別是常用且相對簡單的類別。</span><span class="sxs-lookup"><span data-stu-id="04af9-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="04af9-437">此時間序列類別是從 1970 年 1 月 1 日開始計量時間。</span><span class="sxs-lookup"><span data-stu-id="04af9-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="04af9-438">在此範例中，我們將使用 POSIXct 時間序列物件。</span><span class="sxs-lookup"><span data-stu-id="04af9-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="04af9-439">其他廣泛使用的 R 時間序列物件類別包括 zoo 和 xts (可延伸時間序列)。</span><span class="sxs-lookup"><span data-stu-id="04af9-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="04af9-440">時間序列物件範例</span><span class="sxs-lookup"><span data-stu-id="04af9-440">Time series object example</span></span>
<span data-ttu-id="04af9-441">讓我們開始進行我們的範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-441">Let's get started with our example.</span></span> <span data-ttu-id="04af9-442">請將**新的**[執行 R 指令碼][execute-r-script]模組拖放到您的實驗中。</span><span class="sxs-lookup"><span data-stu-id="04af9-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="04af9-443">將現有[執行 R 指令碼][execute-r-script]模組的 [結果資料集 1] 輸出連接埠連接到新的[執行 R 指令碼][execute-r-script]模組的 [資料集 1] 輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="04af9-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="04af9-444">如同我為前幾個範例所做的，隨著我們循序進行此範例，在某些點，我將只會示範在每個步驟累加的額外 R 程式碼行。</span><span class="sxs-lookup"><span data-stu-id="04af9-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="04af9-445">讀取資料框架</span><span class="sxs-lookup"><span data-stu-id="04af9-445">Reading the dataframe</span></span>
<span data-ttu-id="04af9-446">第一步是先讀入一個資料框架，然後確定得到預期的結果。</span><span class="sxs-lookup"><span data-stu-id="04af9-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="04af9-447">下列程式碼應該能執行此作業。</span><span class="sxs-lookup"><span data-stu-id="04af9-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="04af9-448">現在，請執行實驗。</span><span class="sxs-lookup"><span data-stu-id="04af9-448">Now, run the experiment.</span></span> <span data-ttu-id="04af9-449">新的執行 R 指令碼圖形的記錄檔看起來應該像圖 14。</span><span class="sxs-lookup"><span data-stu-id="04af9-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

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

<span data-ttu-id="04af9-450"> *14.[執行 R 指令碼] 模組中資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="04af9-451">此資料的類型和格式皆如預期。</span><span class="sxs-lookup"><span data-stu-id="04af9-451">This data is of the expected types and format.</span></span> <span data-ttu-id="04af9-452">請注意，'Month' 資料行的類型是因素，並且具有預期的層級數目。</span><span class="sxs-lookup"><span data-stu-id="04af9-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="04af9-453">建立時間序列物件</span><span class="sxs-lookup"><span data-stu-id="04af9-453">Creating a time series object</span></span>
<span data-ttu-id="04af9-454">我們需要將時間序列物件新增到我們的資料框架中。</span><span class="sxs-lookup"><span data-stu-id="04af9-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="04af9-455">請以下列程式碼取代目前的程式碼，這會新增新的 POSIXct 類別資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="04af9-456">現在，請檢查記錄檔。</span><span class="sxs-lookup"><span data-stu-id="04af9-456">Now, check the log.</span></span> <span data-ttu-id="04af9-457">這應該會看起來像圖 15。</span><span class="sxs-lookup"><span data-stu-id="04af9-457">It should look like Figure 15.</span></span>

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

<span data-ttu-id="04af9-458"> *15.含有時間序列物件之資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="04af9-459">我們可以從摘要看出，新資料行的類別事實上是 POSIXct。</span><span class="sxs-lookup"><span data-stu-id="04af9-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="04af9-460">探索和轉換資料</span><span class="sxs-lookup"><span data-stu-id="04af9-460">Exploring and transforming the data</span></span>
<span data-ttu-id="04af9-461">讓我們探索此資料集內的一些變數。</span><span class="sxs-lookup"><span data-stu-id="04af9-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="04af9-462">散佈圖矩陣是產生快速檢視的好方法。</span><span class="sxs-lookup"><span data-stu-id="04af9-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="04af9-463">我將以下列程式碼行取代前一個 R 程式碼中的 `str()` 函式：</span><span class="sxs-lookup"><span data-stu-id="04af9-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="04af9-464">請執行此程式碼，然後看看結果如何。</span><span class="sxs-lookup"><span data-stu-id="04af9-464">Run this code and see what happens.</span></span> <span data-ttu-id="04af9-465">在 [R 裝置] 連接埠產生的圖應該看起來像圖 16。</span><span class="sxs-lookup"><span data-stu-id="04af9-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![所選變數的散佈圖矩陣][17]

<span data-ttu-id="04af9-467">*圖 16.所選變數的散佈圖矩陣。*</span><span class="sxs-lookup"><span data-stu-id="04af9-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="04af9-468">這些變數之間的關係中有看似奇怪的結構。</span><span class="sxs-lookup"><span data-stu-id="04af9-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="04af9-469">這可能是產生自資料中的趨勢，以及產生自我們未將變數標準化的事實。</span><span class="sxs-lookup"><span data-stu-id="04af9-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="04af9-470">相互關聯分析</span><span class="sxs-lookup"><span data-stu-id="04af9-470">Correlation analysis</span></span>
<span data-ttu-id="04af9-471">若要執行相互關聯分析，我們必須將變數去除趨勢並標準化。</span><span class="sxs-lookup"><span data-stu-id="04af9-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="04af9-472">我們可以就使用既可將變數置中又可縮放變數的 R `scale()` 函式。</span><span class="sxs-lookup"><span data-stu-id="04af9-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="04af9-473">此函式可能也執行得更快。</span><span class="sxs-lookup"><span data-stu-id="04af9-473">This function might well run faster.</span></span> <span data-ttu-id="04af9-474">不過，我想要示範以 R 撰寫的防禦型程式設計範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="04af9-475">以下所示的 `ts.detrend()` 函式即可執行這兩種作業。</span><span class="sxs-lookup"><span data-stu-id="04af9-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="04af9-476">下列兩行程式碼會將資料去除趨勢，然後將值標準化。</span><span class="sxs-lookup"><span data-stu-id="04af9-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="04af9-477">`ts.detrend()` 函式中進行的事情不少。</span><span class="sxs-lookup"><span data-stu-id="04af9-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="04af9-478">此程式碼中大部分會檢查引數的潛在問題，或是處理仍可能在計算期間發生的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="04af9-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="04af9-479">此程式碼中實際上只有幾行在進行計算。</span><span class="sxs-lookup"><span data-stu-id="04af9-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="04af9-480">我們已經在[值轉換](#valuetransformations)中討論過防禦型程式設計的範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="04af9-481">兩個計算區塊皆包裝在 `tryCatch()` 中。</span><span class="sxs-lookup"><span data-stu-id="04af9-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="04af9-482">就某些錯誤而言，傳回原始輸入向量相當合理，而在其他情況下，我會傳回零向量。</span><span class="sxs-lookup"><span data-stu-id="04af9-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="04af9-483">請注意，用於去除趨勢的線性迴歸是時間序列迴歸。</span><span class="sxs-lookup"><span data-stu-id="04af9-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="04af9-484">預測工具變數是時間序列物件。</span><span class="sxs-lookup"><span data-stu-id="04af9-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="04af9-485">定義 `ts.detrend()` 之後，我們會將它套用到資料框架中感興趣的變數。</span><span class="sxs-lookup"><span data-stu-id="04af9-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="04af9-486">我們必須使用 `as.data.frame()` 將 `lapply()` 所建立的結果清單強制轉換成資料框架。</span><span class="sxs-lookup"><span data-stu-id="04af9-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="04af9-487">由於 `ts.detrend()`的防禦性層面緣故，因此即使無法處理其中一個變數，也不會導致無法處理其他變數。</span><span class="sxs-lookup"><span data-stu-id="04af9-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="04af9-488">最後一行程式碼會建立成對的散佈圖。</span><span class="sxs-lookup"><span data-stu-id="04af9-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="04af9-489">執行 R 程式碼之後，散佈圖的結果會如圖 17 所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![已去除趨勢並已標準化之時間序列的成對散佈圖][18]

<span data-ttu-id="04af9-491">*圖 17.已去除趨勢並已標準化之時間序列的成對散佈圖。*</span><span class="sxs-lookup"><span data-stu-id="04af9-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="04af9-492">您可以將這些結果與圖 16 所示的結果做比較。</span><span class="sxs-lookup"><span data-stu-id="04af9-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="04af9-493">在已移除趨勢並將變數標準化的情況下，我們會看到這些變數之間的關係少了許多結構。</span><span class="sxs-lookup"><span data-stu-id="04af9-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="04af9-494">以 R ccf 物件方式計算相互關聯的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="04af9-495">執行此程式碼會產生如圖 18 所示的記錄。</span><span class="sxs-lookup"><span data-stu-id="04af9-495">Running this code produces the log shown in Figure 18.</span></span>

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

<span data-ttu-id="04af9-496">*圖 18.來自成對相互關聯分析的 ccf 物件清單。*</span><span class="sxs-lookup"><span data-stu-id="04af9-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="04af9-497">每段延隔時間都有一個相互關聯值。</span><span class="sxs-lookup"><span data-stu-id="04af9-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="04af9-498">這些相互關聯值都沒有大到足以具有重要性。</span><span class="sxs-lookup"><span data-stu-id="04af9-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="04af9-499">因此，可以推斷出我們可以獨立建立每個變數的模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="04af9-500">輸出資料框架</span><span class="sxs-lookup"><span data-stu-id="04af9-500">Output a dataframe</span></span>
<span data-ttu-id="04af9-501">我們已經以 R cff 物件清單方式計算成對的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="04af9-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="04af9-502">這樣會有一點問題，因為 [結果資料集] 輸出連接埠確實需要資料框架。</span><span class="sxs-lookup"><span data-stu-id="04af9-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="04af9-503">此外，ccf 物件本身是清單，而我們只想要此清單第一個元素中的值，亦即各段延隔時間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="04af9-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="04af9-504">下列程式碼會從 ccf 物件 (本身是清單) 的清單中擷取延隔時間值。</span><span class="sxs-lookup"><span data-stu-id="04af9-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="04af9-505">第一行程式碼是需要一點技巧，一些說明可以幫助您了解它。</span><span class="sxs-lookup"><span data-stu-id="04af9-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="04af9-506">由內而外可分為下列項目：</span><span class="sxs-lookup"><span data-stu-id="04af9-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="04af9-507">含有引數 '**1**' 的 '**[[**' 運算子會從 ccf 物件清單的第一個元素選取各段延隔時間的相互關聯向量。</span><span class="sxs-lookup"><span data-stu-id="04af9-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="04af9-508">`do.call()` 函式會在 `lapply()` 所傳回之清單的項目上套用 `rbind()` 函式。</span><span class="sxs-lookup"><span data-stu-id="04af9-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="04af9-509">`data.frame()` 函式會強制將 `do.call()` 產生的結果轉換成資料框架。</span><span class="sxs-lookup"><span data-stu-id="04af9-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="04af9-510">請注意，資料列名稱會在資料框架的資料行中。</span><span class="sxs-lookup"><span data-stu-id="04af9-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="04af9-511">這麼做可在從[執行 R 指令碼][execute-r-script]輸出資料列名稱時，保留這些資料列名稱。</span><span class="sxs-lookup"><span data-stu-id="04af9-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="04af9-512">執行此程式碼時，會在我將 [結果資料集] 連接埠的輸出 [ **視覺化** ] 時，產生如圖 19 所示的輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="04af9-513">資料列名稱如預期般在第一個資料行中。</span><span class="sxs-lookup"><span data-stu-id="04af9-513">The row names are in the first column, as intended.</span></span>

![來自相互關聯分析的結果輸出][20]

<span data-ttu-id="04af9-515">*圖 19.來自相互關聯分析的結果輸出。*</span><span class="sxs-lookup"><span data-stu-id="04af9-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <span data-ttu-id="04af9-516"><a id="seasonalforecasting"></a>時間序列範例：季節性預測</span><span class="sxs-lookup"><span data-stu-id="04af9-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="04af9-517">我們的資料現在是適用於分析的形式，而我們已判斷出變數之間沒有重大的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="04af9-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="04af9-518">讓我們繼續來建立時間序列預測模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="04af9-519">我們將使用此模型預測 2013 年 12 個月的加州牛奶產量。</span><span class="sxs-lookup"><span data-stu-id="04af9-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="04af9-520">我們的預測模型將會有兩個元件，亦即趨勢元件和季節性元件。</span><span class="sxs-lookup"><span data-stu-id="04af9-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="04af9-521">這兩個元件的乘積即是完整預測。</span><span class="sxs-lookup"><span data-stu-id="04af9-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="04af9-522">這種模型稱為乘法模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="04af9-523">替代模型是加法模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-523">The alternative is an additive model.</span></span> <span data-ttu-id="04af9-524">我們已經將對數轉換套用到感興趣的變數，以便控制這項分析。</span><span class="sxs-lookup"><span data-stu-id="04af9-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="04af9-525">您稍早下載的 Zip 檔中有本節的完整 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="04af9-526">建立用於分析的資料框架</span><span class="sxs-lookup"><span data-stu-id="04af9-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="04af9-527">首先，請將**新的**[執行 R 指令碼][execute-r-script]模組新增到您的實驗中。</span><span class="sxs-lookup"><span data-stu-id="04af9-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="04af9-528">將現有[執行 R 指令碼][execute-r-script]模組的 [結果資料集] 輸出連接到新模組的 [資料集1] 輸入。</span><span class="sxs-lookup"><span data-stu-id="04af9-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="04af9-529">結果應該會看起來像圖 20。</span><span class="sxs-lookup"><span data-stu-id="04af9-529">The result should look something like Figure 20.</span></span>

![新增了 [執行 R 指令碼] 模組的實驗][21]

<span data-ttu-id="04af9-531">*圖 20.新增了 [執行 R 指令碼] 模組的實驗。*</span><span class="sxs-lookup"><span data-stu-id="04af9-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="04af9-532">與我們剛剛完成的相互關聯分析相同，我們需要新增一個含有 POSIXct 時間序列物件的資料行。</span><span class="sxs-lookup"><span data-stu-id="04af9-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="04af9-533">下列程式碼將執行的就是這個動作。</span><span class="sxs-lookup"><span data-stu-id="04af9-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="04af9-534">執行此程式碼並查看記錄檔。</span><span class="sxs-lookup"><span data-stu-id="04af9-534">Run this code and look at the log.</span></span> <span data-ttu-id="04af9-535">結果應該會看起來像圖 21。</span><span class="sxs-lookup"><span data-stu-id="04af9-535">The result should look like Figure 21.</span></span>

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

<span data-ttu-id="04af9-536">*圖 21.資料框架的摘要。*</span><span class="sxs-lookup"><span data-stu-id="04af9-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="04af9-537">有了這個結果之後，我們便已準備好開始進行分析。</span><span class="sxs-lookup"><span data-stu-id="04af9-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="04af9-538">建立訓練資料集</span><span class="sxs-lookup"><span data-stu-id="04af9-538">Create a training dataset</span></span>
<span data-ttu-id="04af9-539">建構資料框架之後，我們需要建立訓練資料集。</span><span class="sxs-lookup"><span data-stu-id="04af9-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="04af9-540">此資料將包含所有觀察值，但 2013 年最後一個的 12 除外，這是我們的測試資料集。</span><span class="sxs-lookup"><span data-stu-id="04af9-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="04af9-541">下列程式碼會將資料框架細分成子集，並繪製乳製品產量和價格變數的圖。</span><span class="sxs-lookup"><span data-stu-id="04af9-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="04af9-542">然後，我會繪製四個產量和價格變數的圖。</span><span class="sxs-lookup"><span data-stu-id="04af9-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="04af9-543">匿名函式可用來定義一些用於繪圖的引數，然後藉由 `Map()`逐一查看其他兩個引數的清單。</span><span class="sxs-lookup"><span data-stu-id="04af9-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="04af9-544">如果您正在想著可以在這裡使用 for 迴圈，的確沒錯。</span><span class="sxs-lookup"><span data-stu-id="04af9-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="04af9-545">但是，由於 R 是函式型語言，因此我示範給您的是函式型方法。</span><span class="sxs-lookup"><span data-stu-id="04af9-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="04af9-546">執行此程式碼會從 [R 裝置] 輸出產生一系列時間序列圖，如圖 22 所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="04af9-547">請注意，時間軸的單位是日期，這是時間序列圖方法的一個極佳優點。</span><span class="sxs-lookup"><span data-stu-id="04af9-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![加州乳製品產量和價格資料的第一個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![加州乳製品產量和價格資料的第二個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![加州乳製品產量和價格資料的第三個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![加州乳製品產量和價格資料的第四個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="04af9-552">*圖 22.加州乳製品產量和價格資料的時間序列圖。*</span><span class="sxs-lookup"><span data-stu-id="04af9-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="04af9-553">趨勢模型</span><span class="sxs-lookup"><span data-stu-id="04af9-553">A trend model</span></span>
<span data-ttu-id="04af9-554">建立時間序列物件並查看過資料之後，讓我們開始建構加州牛奶產量資料的趨勢模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="04af9-555">我們可以使用時間序列迴歸來進行這項操作。</span><span class="sxs-lookup"><span data-stu-id="04af9-555">We can do this with a time series regression.</span></span> <span data-ttu-id="04af9-556">不過，從圖中可以清楚看出，若要精確地為在訓練資料中所觀察到的趨勢建立模型，我們所需要的將不只是一個斜率和截距。</span><span class="sxs-lookup"><span data-stu-id="04af9-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="04af9-557">在資料規模較小的情況下，我會在 RStudio 中為趨勢建置模型，再將產生的模型剪下並貼到 Azure Machine Learning 中。</span><span class="sxs-lookup"><span data-stu-id="04af9-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="04af9-558">RStudio 針對這種互動式分析提供了互動式環境。</span><span class="sxs-lookup"><span data-stu-id="04af9-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="04af9-559">在第一個嘗試中，我會試試最多 3 次方的多項式迴歸。</span><span class="sxs-lookup"><span data-stu-id="04af9-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="04af9-560">這些種類的模型實際蘊藏過度配適的危險。</span><span class="sxs-lookup"><span data-stu-id="04af9-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="04af9-561">因此，最好避免高階項。</span><span class="sxs-lookup"><span data-stu-id="04af9-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="04af9-562">`I()` 函式禁止解譯內容 (會「依照原狀」解譯內容 )，並且允許您在迴歸方程式中撰寫逐字解譯的函式。</span><span class="sxs-lookup"><span data-stu-id="04af9-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="04af9-563">這會產生下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-563">This generates the following.</span></span>

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

<span data-ttu-id="04af9-564">從這個輸出的 P 值 (Pr(>|t|))，我們可以看出平方項可能沒有意義。</span><span class="sxs-lookup"><span data-stu-id="04af9-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="04af9-565">我將使用 `update()` 函式來卸除平方項，以修改此模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="04af9-566">這會產生下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-566">This generates the following.</span></span>

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

<span data-ttu-id="04af9-567">這樣看起來較好。</span><span class="sxs-lookup"><span data-stu-id="04af9-567">This looks better.</span></span> <span data-ttu-id="04af9-568">所有的項都變得有意義。</span><span class="sxs-lookup"><span data-stu-id="04af9-568">All of the terms are significant.</span></span> <span data-ttu-id="04af9-569">不過，2e-16 值是預設值，因此不應該太認真看待。</span><span class="sxs-lookup"><span data-stu-id="04af9-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="04af9-570">讓我們繪製顯示趨勢曲線的加州乳製品產量資料時間序列圖，來做為例行性測試。</span><span class="sxs-lookup"><span data-stu-id="04af9-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="04af9-571">我已經在 Azure Machine Learning [執行 R 指令碼][execute-r-script]模型 (非 RStudio) 中新增下列程式碼，以建立模型並繪圖。</span><span class="sxs-lookup"><span data-stu-id="04af9-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="04af9-572">結果顯示在「圖 23」中。</span><span class="sxs-lookup"><span data-stu-id="04af9-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![顯示趨勢模型的加州牛奶產量資料](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="04af9-574">*圖 23.顯示趨勢模型的加州牛奶產量資料。*</span><span class="sxs-lookup"><span data-stu-id="04af9-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="04af9-575">看起來趨勢模型與資料非常相符。</span><span class="sxs-lookup"><span data-stu-id="04af9-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="04af9-576">此外，看來似乎也沒有過度配適的跡象，例如模型曲線中有奇怪的擺動。</span><span class="sxs-lookup"><span data-stu-id="04af9-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="04af9-577">季節性模型</span><span class="sxs-lookup"><span data-stu-id="04af9-577">Seasonal model</span></span>
<span data-ttu-id="04af9-578">有了趨勢模型之後，我們還需要繼續進行來納入季節性效果。</span><span class="sxs-lookup"><span data-stu-id="04af9-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="04af9-579">我們將使用年中月份做為線性模型中的虛擬變數，以擷取逐月的效果。</span><span class="sxs-lookup"><span data-stu-id="04af9-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="04af9-580">請注意，當您將因素變數導入到模型中時，必須不計算截距。</span><span class="sxs-lookup"><span data-stu-id="04af9-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="04af9-581">如果不這麼做，便會過度指定該公式，R 將會卸除其中一個想要的因素，而保留截距項。</span><span class="sxs-lookup"><span data-stu-id="04af9-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="04af9-582">既然我們有了令人滿意的趨勢模型，我們可以使用 `update()` 函式將新項新增到現有的模型。</span><span class="sxs-lookup"><span data-stu-id="04af9-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="04af9-583">更新公式中的-1 會卸除截距項。</span><span class="sxs-lookup"><span data-stu-id="04af9-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="04af9-584">目前先繼續在 RStudio 中進行：</span><span class="sxs-lookup"><span data-stu-id="04af9-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="04af9-585">這會產生下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-585">This generates the following.</span></span>

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

<span data-ttu-id="04af9-586">我們會看到模型不再具有截距項，並且擁有 12 個重要的月份因素。</span><span class="sxs-lookup"><span data-stu-id="04af9-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="04af9-587">這就是我們想要看到的。</span><span class="sxs-lookup"><span data-stu-id="04af9-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="04af9-588">讓我們繪製另一張加州乳製品產量資料的時間序列圖，看看季節性模型運作得如何。</span><span class="sxs-lookup"><span data-stu-id="04af9-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="04af9-589">我已經在 Azure Machine Learning [執行 R 指令碼][execute-r-script]中新增下列程式碼，以建立模型並繪圖。</span><span class="sxs-lookup"><span data-stu-id="04af9-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="04af9-590">在 Azure Machine Learning 中執行此程式碼會產生如圖 24 所示的圖。</span><span class="sxs-lookup"><span data-stu-id="04af9-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![模型包含季節性效果的加州牛奶產量](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="04af9-592">*圖 24.模型包含季節性效果的加州牛奶產量。*</span><span class="sxs-lookup"><span data-stu-id="04af9-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="04af9-593">圖 24 所示的資料相符程度相當令人振奮。</span><span class="sxs-lookup"><span data-stu-id="04af9-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="04af9-594">趨勢和季節性效果 (每月變化) 看起來都相當合理。</span><span class="sxs-lookup"><span data-stu-id="04af9-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="04af9-595">接下來，對模型進行另一項檢查，讓我們看看殘差。</span><span class="sxs-lookup"><span data-stu-id="04af9-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="04af9-596">下列程式碼會從我們的兩個模型計算預測值、計算季節性模型的殘差，然後繪製這些殘差的圖以供訓練資料使用。</span><span class="sxs-lookup"><span data-stu-id="04af9-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="04af9-597">殘差圖如圖 25 所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-597">The residual plot is shown in Figure 25.</span></span>

![訓練資料之季節性模型的殘差](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="04af9-599">*圖 25.訓練資料之季節性模型的殘差。*</span><span class="sxs-lookup"><span data-stu-id="04af9-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="04af9-600">這些殘差看起來相當合理。</span><span class="sxs-lookup"><span data-stu-id="04af9-600">These residuals look reasonable.</span></span> <span data-ttu-id="04af9-601">除了我們模型無法很好地解釋的 2008-2009 年衰退現象之外，並沒有特定的結構。</span><span class="sxs-lookup"><span data-stu-id="04af9-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="04af9-602">圖 25 所示的圖對於偵測殘差中任何時間相依模式來說，相當有用。</span><span class="sxs-lookup"><span data-stu-id="04af9-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="04af9-603">我用來計算殘差及繪製殘差圖的明確方法，會讓殘差在圖上依時間排序。</span><span class="sxs-lookup"><span data-stu-id="04af9-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="04af9-604">如果在另一方面，我已經繪製 `milk.lm$residuals`的圖，此圖就不會依時間排序。</span><span class="sxs-lookup"><span data-stu-id="04af9-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="04af9-605">您也可以使用 `plot.lm()` 來產生一系列診斷圖：</span><span class="sxs-lookup"><span data-stu-id="04af9-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="04af9-606">此程式碼會產生一系列診斷圖，如圖 26 所示。</span><span class="sxs-lookup"><span data-stu-id="04af9-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![季節性模型的第一個診斷圖](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![季節性模型的第二個診斷圖](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![季節性模型的第三個診斷圖](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![季節性模型的第四個診斷圖](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="04af9-611">*圖 26.季節性模型的診斷圖。*</span><span class="sxs-lookup"><span data-stu-id="04af9-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="04af9-612">這些圖中有指出一些高影響力的點，但是不需要太過關注。</span><span class="sxs-lookup"><span data-stu-id="04af9-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="04af9-613">此外，我們可以從常態分佈 Q-Q 圖看出殘差接近常態分佈，這是線性模型的重要認定依據。</span><span class="sxs-lookup"><span data-stu-id="04af9-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="04af9-614">預測和模型評估</span><span class="sxs-lookup"><span data-stu-id="04af9-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="04af9-615">距離完成我們的範例，只剩一件事情要做。</span><span class="sxs-lookup"><span data-stu-id="04af9-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="04af9-616">我們需要計算預測，並對照實際資料來測量誤差。</span><span class="sxs-lookup"><span data-stu-id="04af9-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="04af9-617">我們的預測將會針對 2013 年的 12 個月。</span><span class="sxs-lookup"><span data-stu-id="04af9-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="04af9-618">我們可以針對這項不屬於我們訓練資料集之實際資料的預測，計算誤差衡量值。</span><span class="sxs-lookup"><span data-stu-id="04af9-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="04af9-619">此外，我們可以將 18 年訓練資料的相關表現與 12 個月的測試資料做比較。</span><span class="sxs-lookup"><span data-stu-id="04af9-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="04af9-620">有一些衡量標準可用來衡量時間序列模型的表現。</span><span class="sxs-lookup"><span data-stu-id="04af9-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="04af9-621">在我們的案例中，我們將使用均方根 (RMS) 誤差。</span><span class="sxs-lookup"><span data-stu-id="04af9-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="04af9-622">下列函式會計算兩個數列間的 RMS 誤差。</span><span class="sxs-lookup"><span data-stu-id="04af9-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
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

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="04af9-623">與我們在＜值轉換＞一節中討論的 `log.transform()` 函式相同，此函式中也有許多錯誤檢查和例外狀況復原程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="04af9-624">所採用的原則相同。</span><span class="sxs-lookup"><span data-stu-id="04af9-624">The principles employed are the same.</span></span> <span data-ttu-id="04af9-625">工作會由包裝在 `tryCatch()`中的兩個地方完成。</span><span class="sxs-lookup"><span data-stu-id="04af9-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="04af9-626">首先，由於我們一直以來都是使用值的對數，因此會將時間序列乘冪。</span><span class="sxs-lookup"><span data-stu-id="04af9-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="04af9-627">其次，則是會計算實際的 RMS 誤差。</span><span class="sxs-lookup"><span data-stu-id="04af9-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="04af9-628">在具備測量 RMS 誤差的函式之後，讓我們建置並輸出包含 RMS 誤差的資料框架。</span><span class="sxs-lookup"><span data-stu-id="04af9-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="04af9-629">我們將會包含只針對趨勢模型的各個項，以及針對含有季節性因素之完整模型的各個項。</span><span class="sxs-lookup"><span data-stu-id="04af9-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="04af9-630">下列程式碼會使用我們已建構的兩個線性模型來進行此作業。</span><span class="sxs-lookup"><span data-stu-id="04af9-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
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

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="04af9-631">執行此程式碼會在 [結果資料集] 輸出連接埠產生如圖 27 所示的輸出。</span><span class="sxs-lookup"><span data-stu-id="04af9-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![模型的 RMS 誤差比較][26]

<span data-ttu-id="04af9-633">*圖 27.模型的 RMS 誤差比較。*</span><span class="sxs-lookup"><span data-stu-id="04af9-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="04af9-634">我們可以從這些結果看出，將季節性因素新增到模型中可大幅降低 RMS 誤差。</span><span class="sxs-lookup"><span data-stu-id="04af9-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="04af9-635">不出所料，訓練資料的 RMS 誤差比預測的 RMS 誤差小一些。</span><span class="sxs-lookup"><span data-stu-id="04af9-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <span data-ttu-id="04af9-636"><a id="appendixa"></a>附錄 A：RStudio 指南</span><span class="sxs-lookup"><span data-stu-id="04af9-636"><a id="appendixa"></a>APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="04af9-637">RStudio 已經有相當充分的說明，因此在本附錄中，我將提供一些 RStudio 文件中重要小節的連結，讓您能夠輕鬆上手。</span><span class="sxs-lookup"><span data-stu-id="04af9-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="04af9-638">建立專案</span><span class="sxs-lookup"><span data-stu-id="04af9-638">Creating projects</span></span>
   
   <span data-ttu-id="04af9-639">您可以使用 RStudio，以專案方式組織和管理您的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="04af9-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="04af9-640">您可以在下列網址找到使用專案的文件：https://support.rstudio.com/hc/articles/200526207-Using-Projects。</span><span class="sxs-lookup"><span data-stu-id="04af9-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="04af9-641">建議您依照這些指示，為本文件中的 R 程式碼範例建立專案。</span><span class="sxs-lookup"><span data-stu-id="04af9-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="04af9-642">編輯和執行 R 程式碼</span><span class="sxs-lookup"><span data-stu-id="04af9-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="04af9-643">RStudio 提供一個可編輯和執行 R 程式碼的整合式環境。</span><span class="sxs-lookup"><span data-stu-id="04af9-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="04af9-644">您可以在下列網址找到相關文件：https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code。</span><span class="sxs-lookup"><span data-stu-id="04af9-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="04af9-645">Debugging</span><span class="sxs-lookup"><span data-stu-id="04af9-645">Debugging</span></span>
   
   <span data-ttu-id="04af9-646">RStudio 包含強大的偵錯功能。</span><span class="sxs-lookup"><span data-stu-id="04af9-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="04af9-647">下列網址提供這些功能的相關文件：https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio。</span><span class="sxs-lookup"><span data-stu-id="04af9-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="04af9-648">下列網址提供中斷點疑難排解功能的相關文件：https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting。</span><span class="sxs-lookup"><span data-stu-id="04af9-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="04af9-649"><a id="appendixb"></a>附錄 B：進階閱讀</span><span class="sxs-lookup"><span data-stu-id="04af9-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="04af9-650">此 R 程式設計教學課程涵蓋您搭配 Azure Machine Learning Studio 使用 R 語言時所需的基本知識。</span><span class="sxs-lookup"><span data-stu-id="04af9-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="04af9-651">如果您不熟悉 R，CRAN 有提供兩本簡介：</span><span class="sxs-lookup"><span data-stu-id="04af9-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="04af9-652">Emmanuel Paradis 所著的《R for Beginners》是初學者的首選，網址為 http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf。</span><span class="sxs-lookup"><span data-stu-id="04af9-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="04af9-653">W. N. </span><span class="sxs-lookup"><span data-stu-id="04af9-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="04af9-654">Venables et. </span><span class="sxs-lookup"><span data-stu-id="04af9-654">Venables et.</span></span> <span data-ttu-id="04af9-655">所著的《An Introduction to R》</span><span class="sxs-lookup"><span data-stu-id="04af9-655">al.</span></span> <span data-ttu-id="04af9-656">提供略為深入的探討，網址為 http://cran.r-project.org/doc/manuals/R-intro.html。</span><span class="sxs-lookup"><span data-stu-id="04af9-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="04af9-657">有許多 R 的相關書籍可以協助您輕鬆上手。</span><span class="sxs-lookup"><span data-stu-id="04af9-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="04af9-658">以下是一些我認為實用的書籍：</span><span class="sxs-lookup"><span data-stu-id="04af9-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="04af9-659">Norman Matloff 所著的《The Art of R Programming: A Tour of Statistical Software Design》是一本使用 R 進行程式設計的出色簡介。</span><span class="sxs-lookup"><span data-stu-id="04af9-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="04af9-660">Paul Teetor 所著的《R Cookbook》提供關於使用 R 的問題與解決方法。</span><span class="sxs-lookup"><span data-stu-id="04af9-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="04af9-661">Robert Kabacoff 所著的《R in Action》是另一本實用的簡介書籍。</span><span class="sxs-lookup"><span data-stu-id="04af9-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="04af9-662">指南 Quick R 網站是相當實用的資源，網址為 http://www.statmethods.net/。</span><span class="sxs-lookup"><span data-stu-id="04af9-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="04af9-663">Patrick Burns 所著的《R Inferno》是一本令人出乎意料的幽默書籍，當中處理一些使用 R 進行程式設計時，可能遇到的較具技巧性和困難度的主題。這本書提供免費下載，網址為 http://www.burns-stat.com/documents/books/the-r-inferno/。</span><span class="sxs-lookup"><span data-stu-id="04af9-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="04af9-664">如果您想要深入探索 R 中的進階主題，可以看看 Hadley Wickham 所著的《Advanced R》。</span><span class="sxs-lookup"><span data-stu-id="04af9-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="04af9-665">這本書的線上版本提供免費下載，網址為 http://adv-r.had.co.nz/。</span><span class="sxs-lookup"><span data-stu-id="04af9-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="04af9-666">您可以在「CRAN 工作檢視：時間序列分析」找到 R 時間序列套件目錄：http://cran.r-project.org/web/views/TimeSeries.html。</span><span class="sxs-lookup"><span data-stu-id="04af9-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="04af9-667">如需特定時間序列物件封裝的資訊，您應該參考該封裝的相關文件。</span><span class="sxs-lookup"><span data-stu-id="04af9-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="04af9-668">Paul Cowpertwait 與 Andrew Metcalfe 所著的 《Introductory Time Series with R》介紹如何使用 R 進行時間序列分析。</span><span class="sxs-lookup"><span data-stu-id="04af9-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="04af9-669">許多理論文本皆有提供 R 範例。</span><span class="sxs-lookup"><span data-stu-id="04af9-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="04af9-670">一些絕佳的網際網路資源：</span><span class="sxs-lookup"><span data-stu-id="04af9-670">Some great internet resources:</span></span>

* <span data-ttu-id="04af9-671">DataCamp：DataCamp 利用視訊課程和程式碼撰寫練習在瀏覽器中輕鬆教導 R。</span><span class="sxs-lookup"><span data-stu-id="04af9-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="04af9-672">最新 R 技巧和封裝均有互動式教學課程。</span><span class="sxs-lookup"><span data-stu-id="04af9-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="04af9-673">請至 https://www.datacamp.com/courses/introduction-to-r 觀看免費的互動式 R 教學課程</span><span class="sxs-lookup"><span data-stu-id="04af9-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="04af9-674">有關從 Programiz 開始使用 R 的指南：https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="04af9-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="04af9-675">Clarkson 大學 Kelly Black 提供的快速 R 教學課程：http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="04af9-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="04af9-676">http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html 列出 60 個以上的 R 資源</span><span class="sxs-lookup"><span data-stu-id="04af9-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

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
