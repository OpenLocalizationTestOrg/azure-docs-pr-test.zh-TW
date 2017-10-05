---
title: "Azure Analysis Services 教學課程第 1 課：建立新的表格式模型專案 | Microsoft Docs"
description: "說明如何建立新的 Azure Analysis Services 教學課程專案。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: ebd160372fc75c6d0fc323be9e948fa2475b71cf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-1-create-a-tabular-model-project"></a><span data-ttu-id="7b4fc-103">第 1 課：建立表格式模型專案</span><span class="sxs-lookup"><span data-stu-id="7b4fc-103">Lesson 1: Create a tabular model project</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="7b4fc-104">在這堂課中，您會使用 SQL Server Data Tool (SSDT) 建立 1400 相容性等級的新表格式模型專案。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-104">In this lesson, you use SQL Server Data Tools (SSDT) to create a new tabular model project at the 1400 compatibility level.</span></span> <span data-ttu-id="7b4fc-105">建立新的專案之後，您就可以開始新增資料和製作模型。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-105">Once your new project is created, you can begin adding data and authoring your model.</span></span> <span data-ttu-id="7b4fc-106">本課程也簡介 SSDT 中的表格式模型製作環境。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-106">This lesson also gives you a brief introduction to the tabular model authoring environment in SSDT.</span></span>  
  
<span data-ttu-id="7b4fc-107">這堂課的預估完成時間：**10 分鐘**</span><span class="sxs-lookup"><span data-stu-id="7b4fc-107">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7b4fc-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b4fc-108">Prerequisites</span></span>  
<span data-ttu-id="7b4fc-109">本主題是表格式模型製作教學課程的第一課。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-109">This topic is the first lesson in a tabular model authoring tutorial.</span></span> <span data-ttu-id="7b4fc-110">若要完成本課程，您需要備齊許多必要條件。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-110">To complete this lesson, there are several prerequisites you need to have in-place.</span></span> <span data-ttu-id="7b4fc-111">若要深入了解，請參閱 [Azure Analysis Services - Adventure Works 教學課程](../tutorials/aas-adventure-works-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-111">To learn more, see [Azure Analysis Services - Adventure Works tutorial](../tutorials/aas-adventure-works-tutorial.md).</span></span>  
  
## <a name="create-a-new-tabular-model-project"></a><span data-ttu-id="7b4fc-112">建立新的表格式模型專案</span><span class="sxs-lookup"><span data-stu-id="7b4fc-112">Create a new tabular model project</span></span>  
  
#### <a name="to-create-a-new-tabular-model-project"></a><span data-ttu-id="7b4fc-113">建立新的表格式模型專案</span><span class="sxs-lookup"><span data-stu-id="7b4fc-113">To create a new tabular model project</span></span>  
  
1.  <span data-ttu-id="7b4fc-114">在 SSDT 中，在 [檔案] 功能表上按一下 [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-114">In SSDT, on the **File** menu, click **New** > **Project**.</span></span>  
  
2.  <span data-ttu-id="7b4fc-115">在 [新增專案] 對話方塊中，展開 [已安裝] > [商業智慧] > [Analysis Services]，然後按一下 [Analysis Services 表格式專案]。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-115">In the **New Project** dialog box, expand **Installed** > **Business Intelligence** > **Analysis Services**, and then click **Analysis Services Tabular Project**.</span></span>  
  
3.  <span data-ttu-id="7b4fc-116">在 [名稱] 中，輸入 **AW 網際網路銷售**，然後指定專案檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-116">In  **Name**, type **AW Internet Sales**, and then specify a location for the project files.</span></span>  
  
    <span data-ttu-id="7b4fc-117">根據預設，[解決方案名稱] 會與專案名稱相同。不過，您可以輸入不同的解決方案名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-117">By default, **Solution Name** is the same as the project name; however, you can type a different solution name.</span></span>  
  
4.  <span data-ttu-id="7b4fc-118">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-118">Click **OK**.</span></span>  
  
5.  <span data-ttu-id="7b4fc-119">在 [表格式模型設計師] 對話方塊中，選取 [整合式工作區]。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-119">In the **Tabular model designer** dialog box, select **Integrated workspace**.</span></span>  
  
    <span data-ttu-id="7b4fc-120">在製作模型期間，工作區會裝載與專案同名的表格式模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-120">The workspace hosts a tabular model database with the same name as the project during model authoring.</span></span> <span data-ttu-id="7b4fc-121">整合式工作區意味著 SSDT 會使用內建的執行個體，不必只為了撰寫模型而安裝個別的 Analysis Services 伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-121">Integrated workspace means SSDT uses a built-in instance, eliminating the need to install a separate Analysis Services server instance just for model authoring.</span></span>
      
6.  <span data-ttu-id="7b4fc-122">在 [相容性等級] 中，選取 [SQL Server 2017 / Azure Analysis Services (1400)]。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-122">In **Compatibility level**, select **SQL Server 2017 / Azure Analysis Services (1400)**.</span></span>   
 
    ![aas 第 1 課 tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    <span data-ttu-id="7b4fc-124">如果您在 [相容性等級] 清單方塊中沒看到 [SQL Server 2017 / Azure Analysis Services (1400)]，就表示您使用的 SQL Server Data Tools 不是最新版本。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-124">If you don’t see SQL Server 2017 / Azure Analysis Services (1400) in the Compatibility level listbox, you’re not using the latest version of SQL Server Data Tools.</span></span> <span data-ttu-id="7b4fc-125">若要取得最新版本，請參閱[安裝 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-125">To get the latest version, see [Install SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a><span data-ttu-id="7b4fc-126">了解 SSDT 表格式模型撰寫環境</span><span class="sxs-lookup"><span data-stu-id="7b4fc-126">Understanding the SSDT tabular model authoring environment</span></span>  
<span data-ttu-id="7b4fc-127">現在，您已建立新的表格式模型專案，讓我們花一點時間瀏覽 SSDT 中的表格式模型製作環境。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-127">Now that you’ve created a new tabular model project, let’s take a moment to explore the tabular model authoring environment in SSDT.</span></span>  
  
<span data-ttu-id="7b4fc-128">專案建立之後會在 SSDT 中開啟。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-128">After your project is created, it opens in SSDT.</span></span> <span data-ttu-id="7b4fc-129">在右側的 [表格式模型總管] 中，您會看到樹狀檢視呈現模型中的物件。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-129">On the right side, in **Tabular Model Explorer**, you see a tree view of the objects in your model.</span></span> <span data-ttu-id="7b4fc-130">您還沒有匯入資料，所以資料夾是空的。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-130">Since you haven't yet imported data, the folders are empty.</span></span> <span data-ttu-id="7b4fc-131">您可以在物件資料夾上按一下滑鼠右鍵來執行動作，類似於功能表列。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-131">You can right-click an object folder to perform actions, similar to the menu bar.</span></span> <span data-ttu-id="7b4fc-132">當您逐步執行本教學課程時，您會使用 [表格式模型總管] 來瀏覽模型專案中的不同物件。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-132">As you step through this tutorial, you use the Tabular Model Explorer to navigate different objects in your model project.</span></span>

![aas 第 1 課 tme](../tutorials/media/aas-lesson1-tme.png)

<span data-ttu-id="7b4fc-134">按一下 [方案總管] 索引標籤。在這裡，您可看到 **Model.bim** 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-134">Click the **Solution Explorer** tab. Here, you see your **Model.bim** file.</span></span> <span data-ttu-id="7b4fc-135">如果您在左邊沒看到設計工具視窗 (含 Model.bim 索引標籤的空視窗)，請在 [方案總管] 的 [AW 網際網路銷售專案] 下，按兩下 [Model.bim] 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-135">If you don’t see the designer window to the left (the empty window with the Model.bim tab), in **Solution Explorer**, under **AW Internet Sales Project**, double-click the **Model.bim** file.</span></span> <span data-ttu-id="7b4fc-136">Model.bim 檔案包含模型專案的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-136">The Model.bim file contains the metadata for your model project.</span></span> 

![aas 第 1 課 se](../tutorials/media/aas-lesson1-se.png)
  
<span data-ttu-id="7b4fc-138">按一下 [Model.bim]。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-138">Click **Model.bim**.</span></span> <span data-ttu-id="7b4fc-139">在 [屬性] 視窗中，您會看到模型屬性，最重要的是 [DirectQuery 模式] 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-139">In the **Properties** window, you see the model properties, most important of which is the **DirectQuery Mode** property.</span></span> <span data-ttu-id="7b4fc-140">這個屬性可指定以 In-Memory 模式 (關閉) 還是 DirectQuery 模式 (開啟) 來部署模型。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-140">This property specifies if the model is deployed in In-Memory mode (Off) or DirectQuery mode (On).</span></span> <span data-ttu-id="7b4fc-141">本教學課程中，您會以 In-Memory 模式來製作和部署模型。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-141">For this tutorial, you author and deploy your model in In-Memory mode.</span></span>

![aas 第 1 課屬性](../tutorials/media/aas-lesson1-properties.png)
  
<span data-ttu-id="7b4fc-143">當您建立模型專案時，根據 [工具] 功能表 > [選項] 對話方塊中可指定的 [資料模型化] 設定，自動會設定某些模型屬性。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-143">When you create a model project, certain model properties are set automatically according to the Data Modeling settings that can be specified in the **Tools** menu > **Options** dialog box.</span></span> <span data-ttu-id="7b4fc-144">[資料備份]、[ 工作空間保留] 和 [工作空間伺服器] 屬性可指定如何及在何處備份、在記憶體中保留和建置工作空間資料庫 (您的模型製作資料庫)。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-144">Data Backup, Workspace Retention, and Workspace Server properties specify how and where the workspace database (your model authoring database) is backed up, retained in-memory, and built.</span></span> <span data-ttu-id="7b4fc-145">稍後，如有必要，您可以變更這些設定，但現在，讓這些屬性保持不變即可。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-145">You can change these settings later if necessary, but for now, leave these properties as they are.</span></span>  

<span data-ttu-id="7b4fc-146">在 [方案總管] 中，以滑鼠右鍵按一下 [AW 網際網路銷售] \(專案)，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-146">In **Solution Explorer**, right-click **AW Internet Sales** (project), and then click **Properties**.</span></span> <span data-ttu-id="7b4fc-147">[AW 網際網路銷售屬性頁] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-147">The **AW Internet Sales Property Pages** dialog box appears.</span></span> <span data-ttu-id="7b4fc-148">稍後部署模型時，您會設定其中一些屬性。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-148">You set some of these properties later when you deploy your model.</span></span>  
  
<span data-ttu-id="7b4fc-149">當您安裝 SSDT 時，有數個新的功能表項目新增至 Visual Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-149">When you installed SSDT, several new menu items were added to the Visual Studio environment.</span></span> <span data-ttu-id="7b4fc-150">按一下 [模型] 功能表。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-150">Click the **Model** menu.</span></span> <span data-ttu-id="7b4fc-151">從這裡，您可以匯入資料、重新整理工作區資料、在 Excel 中瀏覽模型、建立檢視方塊和角色、選取模型檢視，以及設定計算選項。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-151">From here, you can import data, refresh workspace data, browse your model in Excel, create perspectives and roles, select the model view, and set calculation options.</span></span> <span data-ttu-id="7b4fc-152">按一下 [資料表] 功能表。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-152">Click the **Table** menu.</span></span> <span data-ttu-id="7b4fc-153">從這裡，您可以建立和管理關聯性、指定日期資料表設定、建立分割區，以及編輯資料表屬性。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-153">From here, you can create and manage relationships, specify date table settings, create partitions, and edit table properties.</span></span> <span data-ttu-id="7b4fc-154">如果您按一下 [資料行] 功能表，您可以新增和刪除資料表中的資料行、凍結資料行，以及指定排序順序。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-154">If you click the **Column** menu, you can add and delete columns in a table, freeze columns, and specify sort order.</span></span> <span data-ttu-id="7b4fc-155">SSDT 也會在工具列新增某些按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-155">SSDT also adds some buttons to the bar.</span></span> <span data-ttu-id="7b4fc-156">「自動加總」功能最實用，可以為選取的資料行建立標準彙總量值。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-156">Most useful is the AutoSum feature to create a standard aggregation measure for a selected column.</span></span> <span data-ttu-id="7b4fc-157">其他工具列按鈕可讓您快速存取常用的功能和命令。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-157">Other toolbar buttons provide quick access to frequently used features and commands.</span></span>  
  
<span data-ttu-id="7b4fc-158">請瀏覽一些對話方塊和位置，以了解與表格式模型製作有關的各種功能。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-158">Explore some of the dialogs and locations for various features specific to authoring tabular models.</span></span> <span data-ttu-id="7b4fc-159">雖然某些項目尚無作用，但可讓您更熟悉表格式模型製作環境。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-159">While some items are not yet active, you can get a good idea of the tabular model authoring environment.</span></span>  
  

## <a name="whats-next"></a><span data-ttu-id="7b4fc-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b4fc-160">What's next?</span></span>
<span data-ttu-id="7b4fc-161">[第 2 課：取得資料](../tutorials/aas-lesson-2-get-data.md)。</span><span class="sxs-lookup"><span data-stu-id="7b4fc-161">[Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span>

  
  
  
