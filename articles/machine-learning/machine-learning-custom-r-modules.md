---
title: "Azure Machine Learning 中的自訂 R 模組 aaaAuthor |Microsoft 文件"
description: "在 Azure Machine Learning 中撰寫自訂 R 模組的快速入門。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="33675-103">在 Azure Machine Learning 中撰寫自訂 R 模組</span><span class="sxs-lookup"><span data-stu-id="33675-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="33675-104">本主題描述如何 tooauthor 和部署 Azure Machine Learning 中的自訂 R 模組。</span><span class="sxs-lookup"><span data-stu-id="33675-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="33675-105">它會說明自訂 R 模組為何，以及哪些檔案是使用的 toodefine 它們。</span><span class="sxs-lookup"><span data-stu-id="33675-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="33675-106">它會說明如何 tooconstruct hello 定義模組的檔案和 tooregister hello Machine Learning 工作區中的部署模組的方式。</span><span class="sxs-lookup"><span data-stu-id="33675-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="33675-107">hello 項目和屬性中的 hello 自訂模組的 hello 定義使用然後詳述於更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="33675-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="33675-108">如何也討論 toouse 輔助功能以及檔案和多個輸出。</span><span class="sxs-lookup"><span data-stu-id="33675-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="33675-109">什麼是自訂 R 模組？</span><span class="sxs-lookup"><span data-stu-id="33675-109">What is a custom R module?</span></span>
<span data-ttu-id="33675-110">A**自訂模組**是使用者定義的模組可以上傳 tooyour 工作區及 Azure 機器學習實驗的一部分執行。</span><span class="sxs-lookup"><span data-stu-id="33675-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="33675-111">**自訂 R 模組** 是執行使用者定義之 R 函數的自訂模組。</span><span class="sxs-lookup"><span data-stu-id="33675-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="33675-112">**R** 是一種適用於統計運算和圖形的程式設計語言，由實作演算法的統計學家和資料科學家廣泛使用。</span><span class="sxs-lookup"><span data-stu-id="33675-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="33675-113">目前，R 是 hello 唯一自訂模組，但支援其他語言排程在未來的版本支援的語言。</span><span class="sxs-lookup"><span data-stu-id="33675-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="33675-114">自訂模組有**第一級狀態**hello 意義而言，它們可以用於就像任何其他模組的 Azure Machine Learning 中。</span><span class="sxs-lookup"><span data-stu-id="33675-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="33675-115">它們可以與已發行實驗或視覺效果中包含的其他模組一起執行。</span><span class="sxs-lookup"><span data-stu-id="33675-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="33675-116">您充分掌控 hello 模組所實作的 hello 演算法、 hello 使用輸入和輸出連接埠 toobe、 hello 模型參數和其他各種執行階段行為。</span><span class="sxs-lookup"><span data-stu-id="33675-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="33675-117">包含自訂模組的實驗也可以發行成 hello Cortana 智慧組件庫以方便共用。</span><span class="sxs-lookup"><span data-stu-id="33675-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="33675-118">自訂 R 模組中的檔案</span><span class="sxs-lookup"><span data-stu-id="33675-118">Files in a custom R module</span></span>
<span data-ttu-id="33675-119">自訂 R 模組是由至少包含兩個檔案的 .zip 檔案所定義：</span><span class="sxs-lookup"><span data-stu-id="33675-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="33675-120">A**原始程式檔**實作 hello 模組所公開的 hello R 函式</span><span class="sxs-lookup"><span data-stu-id="33675-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="33675-121">**XML 定義檔**描述 hello 自訂模組介面</span><span class="sxs-lookup"><span data-stu-id="33675-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="33675-122">其他的輔助檔案也可以包含在 hello.zip 檔案，提供可以從 hello 自訂模組存取的功能。</span><span class="sxs-lookup"><span data-stu-id="33675-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="33675-123">此選項會討論 hello**引數**屬於 hello 參考章節**hello XML 定義檔中的項目**下列 hello 快速入門範例。</span><span class="sxs-lookup"><span data-stu-id="33675-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="33675-124">快速入門範例：定義、封裝及註冊自訂 R 模組</span><span class="sxs-lookup"><span data-stu-id="33675-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="33675-125">此範例說明如何 tooconstruct hello 自訂 R 模組所需的檔案，將它們封裝成 zip 檔案，然後在您的機器學習服務工作區中的暫存器 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="33675-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="33675-126">hello 範例 zip 封裝檔及範例檔可以從下載[下載 CustomAddRows.zip 檔案](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="33675-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="33675-127">hello 原始程式檔</span><span class="sxs-lookup"><span data-stu-id="33675-127">hello source file</span></span>
<span data-ttu-id="33675-128">Hello 的範例，請考慮**自訂加入資料列**修改 hello hello 標準實作的模組**加入資料列**使用 tooconcatenate 資料列 （觀察） 從兩個資料集 （資料框架） 的模組。</span><span class="sxs-lookup"><span data-stu-id="33675-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="33675-129">hello 標準**加入資料列**模組附加 hello 資料列的 hello 第二個輸入資料集 toohello hello 第一個輸入資料集的結尾使用 hello`rbind`演算法。</span><span class="sxs-lookup"><span data-stu-id="33675-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="33675-130">自訂的 hello`CustomAddRows`函式類似接受兩個資料集，但也接受布林交換做為其他的輸入參數。</span><span class="sxs-lookup"><span data-stu-id="33675-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="33675-131">如果設定太 hello 交換參數**FALSE**，它傳回 hello 相同的資料集，因為 hello 標準的實作。</span><span class="sxs-lookup"><span data-stu-id="33675-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="33675-132">但是，如果 hello 交換參數是**TRUE**，hello 函式將改為附加資料列的第一個輸入資料集 toohello 結尾 hello 第二個資料集。</span><span class="sxs-lookup"><span data-stu-id="33675-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="33675-133">hello CustomAddRows.R 檔案，其中包含實作 hello R hello `CustomAddRows` hello 所公開的函數**自訂加入資料列**模組有 hello 下列 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="33675-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a><span data-ttu-id="33675-134">hello XML 定義檔</span><span class="sxs-lookup"><span data-stu-id="33675-134">hello XML definition file</span></span>
<span data-ttu-id="33675-135">tooexpose 這`CustomAddRows`函式，為 Azure 機器學習模組時，XML 定義檔必須建立 toospecify 如何 hello**自訂加入資料列**模組應該外觀和行為。</span><span class="sxs-lookup"><span data-stu-id="33675-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="33675-136">它是 hello hello 值的關鍵 toonote**識別碼**hello 屬性**輸入**和**Arg** hello XML 檔案中的項目必須符合 hello R hello 函式參數名稱中的程式碼 hello CustomAddRows.R 檔案完全: (*dataset1*， *dataset2*，和*交換*hello 範例中)。</span><span class="sxs-lookup"><span data-stu-id="33675-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="33675-137">同樣地，hello 值 hello **entryPoint**屬性 hello**語言**項目必須完全符合 hello hello R 指令碼中的 hello 函式名稱: (*CustomAddRows*在 hello 範例）。</span><span class="sxs-lookup"><span data-stu-id="33675-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="33675-138">相反地，hello**識別碼**屬性 hello**輸出**項目沒有對應 tooany hello R 指令碼中的變數。</span><span class="sxs-lookup"><span data-stu-id="33675-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="33675-139">需要一個以上的輸出時，只傳回清單從 hello R 函式的結果放*hello 中相同的順序*為**輸出**hello XML 檔案中宣告項目。</span><span class="sxs-lookup"><span data-stu-id="33675-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="33675-140">封裝和註冊 hello 模組</span><span class="sxs-lookup"><span data-stu-id="33675-140">Package and register hello module</span></span>
<span data-ttu-id="33675-141">儲存為這兩個檔案*CustomAddRows.R*和*CustomAddRows.xml* ，然後 zip hello 兩個檔案一起到*CustomAddRows.zip*檔案。</span><span class="sxs-lookup"><span data-stu-id="33675-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="33675-142">在您機器學習服務工作區中，移 tooyour 工作區中 hello Machine Learning Studio 中，按一下 hello tooregister **+ 新增**hello 下方的按鈕，然後選擇**模組]-> [從 ZIP 封裝**tooupload新的 hello**自訂加入資料列**模組。</span><span class="sxs-lookup"><span data-stu-id="33675-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![上傳 Zip 檔案](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="33675-144">hello**自訂加入資料列**模組現在是透過機器學習實驗的準備 toobe。</span><span class="sxs-lookup"><span data-stu-id="33675-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="33675-145">Hello XML 定義檔中的項目</span><span class="sxs-lookup"><span data-stu-id="33675-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="33675-146">Module 元素</span><span class="sxs-lookup"><span data-stu-id="33675-146">Module elements</span></span>
<span data-ttu-id="33675-147">hello**模組**項目，則使用的 toodefine hello XML 檔案中的自訂模組。</span><span class="sxs-lookup"><span data-stu-id="33675-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="33675-148">您可以在一個 XML 檔案中，使用多個 **Module** 元素來定義多個模組。</span><span class="sxs-lookup"><span data-stu-id="33675-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="33675-149">工作區中的每個模組都必須有唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="33675-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="33675-150">以相同的名稱，為現有的自訂模組的 hello 註冊自訂的模組，並取代 hello 新 hello 現有的模組。</span><span class="sxs-lookup"><span data-stu-id="33675-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="33675-151">自訂模組，不過，可以使用相同的名稱，為現有的 Azure 機器學習模組的 hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="33675-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="33675-152">因此，出現在 hello**自訂**hello 模組調色盤的分類。</span><span class="sxs-lookup"><span data-stu-id="33675-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="33675-153">在 hello**模組**項目，您可以指定兩個額外的選擇性項目：</span><span class="sxs-lookup"><span data-stu-id="33675-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="33675-154">**擁有者**hello 模組將內嵌的項目</span><span class="sxs-lookup"><span data-stu-id="33675-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="33675-155">**描述**包含的文字，會顯示在 hello 模組的快速說明，當您將滑鼠停留在 hello 機器學習 UI 中的 hello 模組項目。</span><span class="sxs-lookup"><span data-stu-id="33675-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="33675-156">Hello 模組項目中的字元限制的規則：</span><span class="sxs-lookup"><span data-stu-id="33675-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="33675-157">hello 值 hello**名稱**中 hello 屬性**模組**項目不能超過 64 個字元的長度。</span><span class="sxs-lookup"><span data-stu-id="33675-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="33675-158">hello 的 hello 內容**描述**項目不能超過 128 個字元的長度。</span><span class="sxs-lookup"><span data-stu-id="33675-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="33675-159">hello 的 hello 內容**擁有者**項目不能超過 32 個字元的長度。</span><span class="sxs-lookup"><span data-stu-id="33675-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="33675-160">模組的結果可以是具決定性或 nondeterministic.* * 依預設，所有模組都視為 toobe 具決定性。</span><span class="sxs-lookup"><span data-stu-id="33675-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="33675-161">也就是假設不可變的輸入的參數和資料集，hello 模組應該傳回的 hello eacRAND 或 functionh 執行時相同的結果。</span><span class="sxs-lookup"><span data-stu-id="33675-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="33675-162">指定此行為，Azure Machine Learning Studio 只重新執行標示為具決定性，如果參數的模組，或 hello 輸入的資料已變更。</span><span class="sxs-lookup"><span data-stu-id="33675-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="33675-163">傳回快取的 hello 結果也會提供實驗多更快地執行。</span><span class="sxs-lookup"><span data-stu-id="33675-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="33675-164">有不具決定性的例如 RAND 或傳回目前的日期或時間的 hello 函式的函式。</span><span class="sxs-lookup"><span data-stu-id="33675-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="33675-165">如果您的模組會使用不具決定性的函式，您可以指定該 hello 模組是不具決定性的選擇性設定 hello **isDeterministic**屬性太**FALSE**。</span><span class="sxs-lookup"><span data-stu-id="33675-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="33675-166">這樣可確保該 hello 模組將會重新執行每次執行 hello 實驗時，即使 hello 模組輸入參數中未變更和複本。</span><span class="sxs-lookup"><span data-stu-id="33675-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="33675-167">語言定義</span><span class="sxs-lookup"><span data-stu-id="33675-167">Language Definition</span></span>
<span data-ttu-id="33675-168">hello**語言**XML 定義檔中的項目是使用的 toospecify hello 自訂模組語言。</span><span class="sxs-lookup"><span data-stu-id="33675-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="33675-169">目前，R 是 hello 只支援的語言。</span><span class="sxs-lookup"><span data-stu-id="33675-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="33675-170">hello 值 hello **sourceFile**屬性必須是 hello hello 模組執行時所在 hello 函式 toocall hello R 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="33675-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="33675-171">這個檔案必須是 hello zip 封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="33675-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="33675-172">hello 值 hello **entryPoint**屬性是 hello 所呼叫的 hello 函式名稱，且必須符合有效 hello 原始程式檔中定義的函數。</span><span class="sxs-lookup"><span data-stu-id="33675-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="33675-173">連接埠</span><span class="sxs-lookup"><span data-stu-id="33675-173">Ports</span></span>
<span data-ttu-id="33675-174">hello 自訂模組的輸入和輸出連接埠中指定子項目的 hello**連接埠**hello XML 定義檔的區段。</span><span class="sxs-lookup"><span data-stu-id="33675-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="33675-175">這些項目 hello 順序決定 hello 配置經驗 (UX) 的使用者。</span><span class="sxs-lookup"><span data-stu-id="33675-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="33675-176">hello 第一個子系**輸入**或**輸出**列在 hello**連接埠**hello XML 檔案的項目會成為 hello 最左邊的輸入連接埠在 hello 機器學習經驗</span><span class="sxs-lookup"><span data-stu-id="33675-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="33675-177">每一個輸入和輸出連接埠可能會有一個選擇性**描述**子元素，指定顯示當您 hello 滑鼠游標 hello hello 機器學習 UI 中的連接埠的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="33675-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="33675-178">**連接埠規則**：</span><span class="sxs-lookup"><span data-stu-id="33675-178">**Ports Rules**:</span></span>

* <span data-ttu-id="33675-179">**輸入和輸出連接埠** 數目上限各為 8 個。</span><span class="sxs-lookup"><span data-stu-id="33675-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="33675-180">Input 元素</span><span class="sxs-lookup"><span data-stu-id="33675-180">Input elements</span></span>
<span data-ttu-id="33675-181">輸入連接埠可讓您 toopass 資料 tooyour R 函式和工作區。</span><span class="sxs-lookup"><span data-stu-id="33675-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="33675-182">hello**資料型別**支援的輸入連接埠，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33675-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="33675-183">**DataTable:**這個型別會當做 data.frame 傳遞 tooyour R 函式。</span><span class="sxs-lookup"><span data-stu-id="33675-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="33675-184">事實上，機器學習和所支援的任何類型 （例如，CSV 檔案或 ARFF 檔案） 是否相容**DataTable**會自動轉換的 tooa data.frame。</span><span class="sxs-lookup"><span data-stu-id="33675-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="33675-185">hello**識別碼**每個相關聯的屬性**DataTable**輸入連接埠必須具有唯一值，這個值必須符合其對應的命名您的 R 函數中的參數。</span><span class="sxs-lookup"><span data-stu-id="33675-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="33675-186">選擇性**DataTable**不會傳遞做為實驗中輸入的連接埠有 hello 值**NULL**傳遞的 toohello R 函式和選擇性 zip 連接埠會忽略如果 hello 輸入未連接。</span><span class="sxs-lookup"><span data-stu-id="33675-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="33675-187">hello **isOptional**屬性是選擇性的這兩個 hello **DataTable**和**Zip**類型，並為*false*預設。</span><span class="sxs-lookup"><span data-stu-id="33675-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="33675-188">**Zip：** 自訂模組可以接受 zip 檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="33675-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="33675-189">此輸入會解壓縮到您的函式的 hello R 工作目錄</span><span class="sxs-lookup"><span data-stu-id="33675-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="33675-190">針對自訂 R 模組 Zip 連接埠的 hello 識別碼沒有 toomatch hello R 函式的任何參數。</span><span class="sxs-lookup"><span data-stu-id="33675-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="33675-191">這是因為 hello zip 檔案是自動解壓縮的 toohello R 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="33675-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="33675-192">**輸入規則：**</span><span class="sxs-lookup"><span data-stu-id="33675-192">**Input Rules:**</span></span>

* <span data-ttu-id="33675-193">hello 值 hello**識別碼**屬性 hello**輸入**元素必須是有效的 R 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="33675-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="33675-194">hello 值 hello**識別碼**屬性 hello**輸入**項目不能超過 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="33675-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="33675-195">hello 值 hello**名稱**屬性 hello**輸入**項目不能超過 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="33675-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="33675-196">hello 的 hello 內容**描述**項目不能超過 128 個字元</span><span class="sxs-lookup"><span data-stu-id="33675-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="33675-197">hello 值 hello**類型**屬性 hello**輸入**項目必須是*Zip*或*DataTable*。</span><span class="sxs-lookup"><span data-stu-id="33675-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="33675-198">hello hello 值**isOptional** hello 屬性**輸入**項目不需要 (且*false*時未指定，預設情況); 但如果有指定，它必須是*true*或*false*。</span><span class="sxs-lookup"><span data-stu-id="33675-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="33675-199">Output 元素</span><span class="sxs-lookup"><span data-stu-id="33675-199">Output elements</span></span>
<span data-ttu-id="33675-200">**標準輸出連接埠：**輸出連接埠會從您的 R 函數，然後由後續的模組的對應的 toohello 傳回值。</span><span class="sxs-lookup"><span data-stu-id="33675-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="33675-201">*DataTable*是 hello 目前支援的唯一標準的輸出連接埠類型。</span><span class="sxs-lookup"><span data-stu-id="33675-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="33675-202">(即將推出 *Learners* 和 *Transforms* 的支援。)*DataTable* 輸出的定義如下：</span><span class="sxs-lookup"><span data-stu-id="33675-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="33675-203">若為自訂 R 模組中的輸出，hello hello 值**識別碼**屬性中並沒有與任何項目 toocorrespond hello R 指令碼，但它必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="33675-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="33675-204">Hello hello R 函式傳回值必須是單一模組的輸出， *data.frame*。</span><span class="sxs-lookup"><span data-stu-id="33675-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="33675-205">在排序 toooutput 支援的資料類型的多個物件、 hello 適當的輸出連接埠需要 toobe hello XML 定義檔中指定與 hello 物件需要 toobe 的清單傳回。</span><span class="sxs-lookup"><span data-stu-id="33675-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="33675-206">hello 輸出物件會從左 tooright，反映 hello 物件會置於傳回清單中的 hello hello 順序指派 toooutput 連接埠。</span><span class="sxs-lookup"><span data-stu-id="33675-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="33675-207">例如，如果您想要 toomodify hello**自訂加入資料列**模組 toooutput hello 原始的兩個資料集， *dataset1*和*dataset2*，此外 toohello 新聯結資料集，*資料集*，(順序，從左 tooright，做為：*資料集*， *dataset1*， *dataset2*)，然後定義 hello輸出 hello CustomAddRows.xml 檔案中的連接埠，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33675-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="33675-208">並在清單中的 hello 物件清單傳回 hello 'CustomAddRows.R' 中的正確順序：</span><span class="sxs-lookup"><span data-stu-id="33675-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="33675-209">**視覺效果輸出：**您也可以指定類型的輸出連接埠*視覺效果*，這會顯示 hello hello R 圖形裝置主控台輸出和輸出。</span><span class="sxs-lookup"><span data-stu-id="33675-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="33675-210">此連接埠不是 hello R 函式輸出的一部分，並不會干擾其他 hello hello 順序輸出連接埠類型。</span><span class="sxs-lookup"><span data-stu-id="33675-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="33675-211">tooadd 視覺效果的連接埠 toohello 自訂模組，新增**輸出**值的項目*視覺效果*針對其**類型**屬性：</span><span class="sxs-lookup"><span data-stu-id="33675-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="33675-212">**輸出規則：**</span><span class="sxs-lookup"><span data-stu-id="33675-212">**Output Rules:**</span></span>

* <span data-ttu-id="33675-213">hello 值 hello**識別碼**屬性 hello**輸出**元素必須是有效的 R 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="33675-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="33675-214">hello 值 hello**識別碼**屬性 hello**輸出**項目不能超過 32 個字元。</span><span class="sxs-lookup"><span data-stu-id="33675-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="33675-215">hello 值 hello**名稱**屬性 hello**輸出**項目不能超過 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="33675-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="33675-216">hello 值 hello**類型**屬性 hello**輸出**項目必須是*視覺效果*。</span><span class="sxs-lookup"><span data-stu-id="33675-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="33675-217">引數</span><span class="sxs-lookup"><span data-stu-id="33675-217">Arguments</span></span>
<span data-ttu-id="33675-218">其他資料可以透過 hello 中定義的模組參數傳遞 toohello R 函式**引數**項目。</span><span class="sxs-lookup"><span data-stu-id="33675-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="33675-219">選取 hello 模組時，這些參數會顯示 hello 機器學習 UI hello 最右邊的屬性 窗格中。</span><span class="sxs-lookup"><span data-stu-id="33675-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="33675-220">引數可以是任何支援的 hello 類型，或者您可以建立時所需的自訂列舉型別。</span><span class="sxs-lookup"><span data-stu-id="33675-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="33675-221">類似 toohello**連接埠**項目，**引數**項目可以有選擇性**描述**項目，指定顯示 hello 滑鼠暫留時的 hello 文字透過 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="33675-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="33675-222">選擇性的模組，例如 defaultValue、 minValue 和 maxValue 屬性加入 tooany 引數屬性 tooa**屬性**項目。</span><span class="sxs-lookup"><span data-stu-id="33675-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="33675-223">有效的屬性，如 hello**屬性**元素 hello 引數型別而定，並且會描述 hello 下一節中的 hello 支援的引數類型。</span><span class="sxs-lookup"><span data-stu-id="33675-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="33675-224">引數以 hello **isOptional**屬性設定太**"true"**不需要 hello 使用者 tooenter 值。</span><span class="sxs-lookup"><span data-stu-id="33675-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="33675-225">如果未提供值 toohello 引數，然後 hello 引數不會傳遞 toohello 進入點函式。</span><span class="sxs-lookup"><span data-stu-id="33675-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="33675-226">是選擇性需要 toobe hello 函式，明確處理 hello 進入點函式的引數例如指派預設值是 NULL hello 進入點函式定義中。</span><span class="sxs-lookup"><span data-stu-id="33675-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="33675-227">選擇性引數只會強制執行 hello 其他引數的限制，也就是最小值或最大值，如果 hello 使用者所提供的值。</span><span class="sxs-lookup"><span data-stu-id="33675-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="33675-228">與輸入和輸出，很重要的每一個 hello 參數有與其相關聯的唯一識別碼值。</span><span class="sxs-lookup"><span data-stu-id="33675-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="33675-229">在快速入門中的 hello 相關聯的識別碼/參數的範例是*交換*。</span><span class="sxs-lookup"><span data-stu-id="33675-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="33675-230">Arg 元素</span><span class="sxs-lookup"><span data-stu-id="33675-230">Arg element</span></span>
<span data-ttu-id="33675-231">模組參數定義使用 hello **Arg** hello 子項目**引數**hello XML 定義檔的區段。</span><span class="sxs-lookup"><span data-stu-id="33675-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="33675-232">如同在 hello hello 子項目**連接埠**區段中，hello hello 中參數的順序**引數**區段會定義在 hello UX 中遇到的 hello 版面配置</span><span class="sxs-lookup"><span data-stu-id="33675-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="33675-233">hello 參數會出現從上往下在 hello UI 中相同訂單在其定義所在的 hello hello XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="33675-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="33675-234">以下列出 hello Machine learning 支援參數的型別。</span><span class="sxs-lookup"><span data-stu-id="33675-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="33675-235">**int** ：整數 (32 位元) 類型的參數。</span><span class="sxs-lookup"><span data-stu-id="33675-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="33675-236">*選擇性屬性*：**min**、**max**、**default** 和 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="33675-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="33675-237">**double** ：double 類型的參數。</span><span class="sxs-lookup"><span data-stu-id="33675-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="33675-238">*選擇性屬性*：**min**、**max**、**default** 和 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="33675-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="33675-239">**bool** ：在 UX 中以核取方塊代表的布林值參數。</span><span class="sxs-lookup"><span data-stu-id="33675-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="33675-240">*選擇性屬性*： **default** - 如果未設定，則為 false</span><span class="sxs-lookup"><span data-stu-id="33675-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="33675-241">**string**：標準字串</span><span class="sxs-lookup"><span data-stu-id="33675-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="33675-242">*選擇性屬性*：**default** 和 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="33675-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="33675-243">**ColumnPicker**：資料行選取參數。</span><span class="sxs-lookup"><span data-stu-id="33675-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="33675-244">此類型會在 hello UX 成活欄位選擇器。</span><span class="sxs-lookup"><span data-stu-id="33675-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="33675-245">hello**屬性**項目是使用這裡 toospecify hello 識別碼 hello 從中選取資料行，必須 hello 目標連接埠類型的連接埠*DataTable*。</span><span class="sxs-lookup"><span data-stu-id="33675-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="33675-246">hello 資料行選取範圍的 hello 結果會傳遞 toohello R 函式，以包含 hello 選取資料行名稱的字串清單。</span><span class="sxs-lookup"><span data-stu-id="33675-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="33675-247">*必要屬性*: **portId** -比對 hello 輸入項目的 id 與型別*DataTable*。</span><span class="sxs-lookup"><span data-stu-id="33675-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="33675-248">*選擇性屬性*：</span><span class="sxs-lookup"><span data-stu-id="33675-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="33675-249">**allowedTypes** -您可以挑選篩選 hello 資料行類型。</span><span class="sxs-lookup"><span data-stu-id="33675-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="33675-250">有效值包含：</span><span class="sxs-lookup"><span data-stu-id="33675-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="33675-251">數值</span><span class="sxs-lookup"><span data-stu-id="33675-251">Numeric</span></span>
    * <span data-ttu-id="33675-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="33675-252">Boolean</span></span>
    * <span data-ttu-id="33675-253">類別</span><span class="sxs-lookup"><span data-stu-id="33675-253">Categorical</span></span>
    * <span data-ttu-id="33675-254">string</span><span class="sxs-lookup"><span data-stu-id="33675-254">String</span></span>
    * <span data-ttu-id="33675-255">標籤</span><span class="sxs-lookup"><span data-stu-id="33675-255">Label</span></span>
    * <span data-ttu-id="33675-256">功能</span><span class="sxs-lookup"><span data-stu-id="33675-256">Feature</span></span>
    * <span data-ttu-id="33675-257">分數</span><span class="sxs-lookup"><span data-stu-id="33675-257">Score</span></span>
    * <span data-ttu-id="33675-258">全部</span><span class="sxs-lookup"><span data-stu-id="33675-258">All</span></span>
  * <span data-ttu-id="33675-259">**預設**-hello 資料行選擇器的有效預設選取項目包括：</span><span class="sxs-lookup"><span data-stu-id="33675-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="33675-260">None</span><span class="sxs-lookup"><span data-stu-id="33675-260">None</span></span>
    * <span data-ttu-id="33675-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="33675-261">NumericFeature</span></span>
    * <span data-ttu-id="33675-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="33675-262">NumericLabel</span></span>
    * <span data-ttu-id="33675-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="33675-263">NumericScore</span></span>
    * <span data-ttu-id="33675-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="33675-264">NumericAll</span></span>
    * <span data-ttu-id="33675-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="33675-265">BooleanFeature</span></span>
    * <span data-ttu-id="33675-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="33675-266">BooleanLabel</span></span>
    * <span data-ttu-id="33675-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="33675-267">BooleanScore</span></span>
    * <span data-ttu-id="33675-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="33675-268">BooleanAll</span></span>
    * <span data-ttu-id="33675-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="33675-269">CategoricalFeature</span></span>
    * <span data-ttu-id="33675-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="33675-270">CategoricalLabel</span></span>
    * <span data-ttu-id="33675-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="33675-271">CategoricalScore</span></span>
    * <span data-ttu-id="33675-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="33675-272">CategoricalAll</span></span>
    * <span data-ttu-id="33675-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="33675-273">StringFeature</span></span>
    * <span data-ttu-id="33675-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="33675-274">StringLabel</span></span>
    * <span data-ttu-id="33675-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="33675-275">StringScore</span></span>
    * <span data-ttu-id="33675-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="33675-276">StringAll</span></span>
    * <span data-ttu-id="33675-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="33675-277">AllLabel</span></span>
    * <span data-ttu-id="33675-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="33675-278">AllFeature</span></span>
    * <span data-ttu-id="33675-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="33675-279">AllScore</span></span>
    * <span data-ttu-id="33675-280">全部</span><span class="sxs-lookup"><span data-stu-id="33675-280">All</span></span>

<span data-ttu-id="33675-281">**DropDown**：使用者指定的列舉 (下拉式) 清單。</span><span class="sxs-lookup"><span data-stu-id="33675-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="33675-282">hello 下拉式清單中的項目指定在 hello**屬性**項目使用**項目**項目。</span><span class="sxs-lookup"><span data-stu-id="33675-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="33675-283">hello**識別碼**每個**項目**必須是唯一的以及有效的 R 變數。</span><span class="sxs-lookup"><span data-stu-id="33675-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="33675-284">hello 值 hello**名稱**的**項目**做為您所看到的 hello 文字和傳遞 toohello R 函式的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="33675-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="33675-285">*選擇性屬性*：</span><span class="sxs-lookup"><span data-stu-id="33675-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="33675-286">**預設**-hello hello 預設屬性必須對應於從 hello 的其中一個識別碼值的值**項目**項目。</span><span class="sxs-lookup"><span data-stu-id="33675-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="33675-287">輔助檔案</span><span class="sxs-lookup"><span data-stu-id="33675-287">Auxiliary Files</span></span>
<span data-ttu-id="33675-288">將自訂模組 ZIP 檔案中放置任何檔案在執行階段是持續 toobe 可供使用。</span><span class="sxs-lookup"><span data-stu-id="33675-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="33675-289">所有存在的目錄結構皆會保留。</span><span class="sxs-lookup"><span data-stu-id="33675-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="33675-290">這表示檔案來源 works hello 相同本機及 Azure 機器學習服務執行中。</span><span class="sxs-lookup"><span data-stu-id="33675-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="33675-291">請注意，所有檔案解壓縮的 too'src' directory，讓所有路徑應該都有 ' src /' 前置詞。</span><span class="sxs-lookup"><span data-stu-id="33675-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="33675-292">例如，假設您想 tooremove NAs hello 資料集，從任何資料列也之前輸出到 CustomAddRows，移除任何重複的資料列，並已撰寫的也 RemoveDupNARows.R 檔案中的 R 函數：</span><span class="sxs-lookup"><span data-stu-id="33675-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="33675-293">您可以來源 hello 輔助檔案 RemoveDupNARows.R，hello CustomAddRows 函式中：</span><span class="sxs-lookup"><span data-stu-id="33675-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="33675-294">接著，上傳包含 ‘CustomAddRows.R’、‘CustomAddRows.xml’ 和 ‘RemoveDupNARows.R’ 的 zip 檔案，做為自訂 R 模組。</span><span class="sxs-lookup"><span data-stu-id="33675-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="33675-295">執行環境</span><span class="sxs-lookup"><span data-stu-id="33675-295">Execution Environment</span></span>
<span data-ttu-id="33675-296">hello 執行環境的 hello R 指令碼會使用 hello 相同版本的 R hello**執行 R 指令碼**模組和使用可以 hello 相同預設封裝。</span><span class="sxs-lookup"><span data-stu-id="33675-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="33675-297">您也可以包含在 hello 自訂模組 zip 套件，以加入其他 R 封裝 tooyour 自訂模組。</span><span class="sxs-lookup"><span data-stu-id="33675-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="33675-298">只要在您的 R 指令碼中載入它們，就像在您自己的 R 環境中一樣。</span><span class="sxs-lookup"><span data-stu-id="33675-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="33675-299">**Hello 執行環境的限制**包括：</span><span class="sxs-lookup"><span data-stu-id="33675-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="33675-300">非持續的檔案系統： hello 自訂模組執行時，寫入的檔案不會保存跨多個回合的 hello 相同的模組。</span><span class="sxs-lookup"><span data-stu-id="33675-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="33675-301">無法存取網路</span><span class="sxs-lookup"><span data-stu-id="33675-301">No network access</span></span>

