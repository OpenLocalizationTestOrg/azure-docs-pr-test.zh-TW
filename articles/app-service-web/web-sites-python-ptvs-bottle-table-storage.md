---
title: "aaaBottle 和使用 Python Tools 2.2 for Visual Studio 在 Azure 上的 Azure 資料表儲存體"
description: "了解如何 toouse hello Python Tools for Visual Studio toocreate Bottle 應用程式在 Azure 資料表儲存體中儲存資料，並部署 hello web 應用程式 tooAzure App Service Web 應用程式。"
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="3c20a-103">Azure 上使用 Python Tools 2.2 for Visual Studio 的 Bottle 和 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="3c20a-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="3c20a-104">在此教學課程中，我們將使用[Python Tools for Visual Studio] toocreate 簡單輪詢 web 應用程式使用其中一個 hello PTVS 範例範本。</span><span class="sxs-lookup"><span data-stu-id="3c20a-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="3c20a-105">本教學課程也提供 [教學影片](https://www.youtube.com/watch?v=GJXDGaEPy94)。</span><span class="sxs-lookup"><span data-stu-id="3c20a-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="3c20a-106">hello 輪詢 web 應用程式定義它的儲存機制的抽象概念，因此您可以輕鬆切換不同類型的儲存機制 (記憶體中，Azure 資料表儲存體，MongoDB) 之間。</span><span class="sxs-lookup"><span data-stu-id="3c20a-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="3c20a-107">我們也將學習如何 toocreate Azure 儲存體帳戶，tooconfigure hello web 應用程式 toouse Azure 資料表儲存體，以及如何 toopublish hello web 應用程式太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="3c20a-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="3c20a-108">請參閱 hello [Python 開發人員中心]涵蓋 Azure App Service Web 應用程式與使用 Bottle PTVS 開發的多個發行項，酒瓶和 Django web 架構，來使用 MongoDB、 Azure 資料表儲存體、 MySQL 及 SQL Database 的服務。</span><span class="sxs-lookup"><span data-stu-id="3c20a-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="3c20a-109">本文著重在應用程式服務，而開發時 hello 步驟均相似[Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="3c20a-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c20a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3c20a-110">Prerequisites</span></span>
* <span data-ttu-id="3c20a-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3c20a-111">Visual Studio 2015</span></span>
* <span data-ttu-id="3c20a-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="3c20a-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="3c20a-113">[Python Tools 2.2 for Visual Studio 範例 VSIX]</span><span class="sxs-lookup"><span data-stu-id="3c20a-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="3c20a-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="3c20a-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="3c20a-115">[Python 2.7 32 位元]或 [Python 3.4 32 位元]</span><span class="sxs-lookup"><span data-stu-id="3c20a-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="3c20a-116">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="3c20a-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3c20a-117">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="3c20a-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="3c20a-118">建立 hello 專案</span><span class="sxs-lookup"><span data-stu-id="3c20a-118">Create hello Project</span></span>
<span data-ttu-id="3c20a-119">在這一節中，我們將使用範例範本建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="3c20a-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="3c20a-120">我們將建立虛擬環境並安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="3c20a-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="3c20a-121">然後我們將執行 hello 應用程式在本機使用 hello 預設記憶體中儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3c20a-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="3c20a-122">在 Visual Studio 中，選取 [檔案]、[新增專案]。</span><span class="sxs-lookup"><span data-stu-id="3c20a-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="3c20a-123">hello 專案範本從 hello [Python Tools 2.2 for Visual Studio 範例 VSIX]底下可使用**Python**，**範例**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="3c20a-124">選取**輪詢 Bottle Web 專案**然後按一下 [確定] toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="3c20a-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![New Project Dialog](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="3c20a-126">系統會提示的 tooinstall 外部的封裝。</span><span class="sxs-lookup"><span data-stu-id="3c20a-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="3c20a-127">選取 [安裝到虛擬環境] 。</span><span class="sxs-lookup"><span data-stu-id="3c20a-127">Select **Install into a virtual environment**.</span></span>
   
     ![外部套件對話方塊](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="3c20a-129">選取**Python 2.7**或**Python 3.4**為 hello 基底直譯器。</span><span class="sxs-lookup"><span data-stu-id="3c20a-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="3c20a-131">確認 hello 應用程式運作方式是按`F5`。</span><span class="sxs-lookup"><span data-stu-id="3c20a-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="3c20a-132">根據預設，hello 應用程式會使用記憶體中儲存機制並不需要任何設定。</span><span class="sxs-lookup"><span data-stu-id="3c20a-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="3c20a-133">Hello web 伺服器停止時，所有資料都都會遺失。</span><span class="sxs-lookup"><span data-stu-id="3c20a-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="3c20a-134">按一下 [Create Sample Polls] ，然後按一下某項民調並投票。</span><span class="sxs-lookup"><span data-stu-id="3c20a-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web Browser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="3c20a-136">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3c20a-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="3c20a-137">toouse 儲存作業，您需要 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c20a-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="3c20a-138">您可以依照下列步驟來建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c20a-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="3c20a-139">登入 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="3c20a-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3c20a-140">按一下 hello**新增**hello 上方的圖示左邊 hello 入口網站，請按一下 **資料 + 儲存體** > **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="3c20a-141">按一下 hello**建立**按鈕，然後提供 hello 儲存體帳戶的唯一名稱，並建立新[資源群組](../azure-resource-manager/resource-group-overview.md)它。</span><span class="sxs-lookup"><span data-stu-id="3c20a-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Quick Create](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="3c20a-143">Hello 儲存體帳戶建立後，hello**通知** 按鈕會閃爍綠色**成功**且 hello 儲存體帳戶的刀鋒視窗已開啟 tooshow 其所屬 toohello 新資源群組建立。</span><span class="sxs-lookup"><span data-stu-id="3c20a-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="3c20a-144">按一下 hello**存取金鑰**hello 儲存體帳戶的刀鋒視窗的一部分。</span><span class="sxs-lookup"><span data-stu-id="3c20a-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="3c20a-145">請注意 hello 帳戶名稱和 key1。</span><span class="sxs-lookup"><span data-stu-id="3c20a-145">Take note of hello account name and key1.</span></span>
   
      ![之間的信任](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="3c20a-147">我們需要此資訊 tooconfigure hello 下一節中的專案。</span><span class="sxs-lookup"><span data-stu-id="3c20a-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="3c20a-148">設定 hello 專案</span><span class="sxs-lookup"><span data-stu-id="3c20a-148">Configure hello Project</span></span>
<span data-ttu-id="3c20a-149">在本節中，我們稍後會設定剛才所建立我們應用程式 toouse hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c20a-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="3c20a-150">然後我們將在本機執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c20a-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="3c20a-151">在 Visual Studio 的 [方案總管] 中，在您的專案節點上按一下滑鼠右鍵，然後選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="3c20a-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="3c20a-152">按一下 hello**偵錯** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c20a-152">Click on hello **Debug** tab.</span></span>
   
     ![專案偵錯設定](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="3c20a-154">設定環境變數中的 hello 應用程式所需的 hello 值**偵錯伺服器指令**，**環境**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="3c20a-155">這會將 hello 環境變數時您**開始偵錯**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="3c20a-156">如果您想要 hello 變數 toobe 設定時您**啟動但不偵錯**，集 hello 相同值的下**執行伺服器命令**以及。</span><span class="sxs-lookup"><span data-stu-id="3c20a-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="3c20a-157">或者，您可以定義使用 hello Windows 控制台中的環境變數。</span><span class="sxs-lookup"><span data-stu-id="3c20a-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="3c20a-158">如果您想要將認證儲存在原始程式碼中 tooavoid / 專案檔，這會是較好的選擇。</span><span class="sxs-lookup"><span data-stu-id="3c20a-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="3c20a-159">請注意，您將需要 Visual Studio toorestart hello 新環境值 toobe 可用 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c20a-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="3c20a-160">實作 hello Azure 資料表儲存體儲存機制的 hello 程式碼位於**models/azuretablestorage.py**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="3c20a-161">請參閱 hello[文件]如需有關如何 toouse 來自 Python 的表格服務。</span><span class="sxs-lookup"><span data-stu-id="3c20a-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="3c20a-162">執行與 hello 應用程式`F5`。</span><span class="sxs-lookup"><span data-stu-id="3c20a-162">Run hello application with `F5`.</span></span> <span data-ttu-id="3c20a-163">利用所建立的輪詢**建立範例輪詢**和送出的投票 hello 資料會序列化 Azure 資料表儲存體中。</span><span class="sxs-lookup"><span data-stu-id="3c20a-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3c20a-164">hello Python 2.7 虛擬環境，可能會在 Visual Studio 中導致例外狀況中斷。</span><span class="sxs-lookup"><span data-stu-id="3c20a-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="3c20a-165">按`F5`toocontinue 載入 hello web 專案。</span><span class="sxs-lookup"><span data-stu-id="3c20a-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="3c20a-166">瀏覽 toohello**有關**hello 應用程式的頁面 tooverify 使用 hello **Azure 資料表儲存體**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3c20a-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Web Browser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="3c20a-168">瀏覽 hello Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="3c20a-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="3c20a-169">它是簡單 tooview 並編輯使用 Cloud Explorer Visual Studio 中的儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="3c20a-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="3c20a-170">本節中，我們會使用伺服器總管 tooview hello 資料表內容的 hello 輪詢應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c20a-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="3c20a-171">這需要安裝，Microsoft Azure Tools toobe 所提供的 hello 一部分[Azure SDK for.NET]。</span><span class="sxs-lookup"><span data-stu-id="3c20a-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="3c20a-172">開啟 [雲端總管] 。</span><span class="sxs-lookup"><span data-stu-id="3c20a-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="3c20a-173">依序展開 [儲存體帳戶]、您的儲存體帳戶和 [資料表]。</span><span class="sxs-lookup"><span data-stu-id="3c20a-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![雲端總管](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="3c20a-175">按兩下 hello**輪詢**或**選擇**資料表 tooview hello hello 資料表文件視窗中，以及加入/移除/編輯實體內容。</span><span class="sxs-lookup"><span data-stu-id="3c20a-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![資料表查詢結果](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="3c20a-177">發行 hello web 應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="3c20a-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="3c20a-178">hello Azure.NET SDK 提供簡單的方式 toodeploy 您 web 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="3c20a-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="3c20a-179">在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![發行 Web 對話方塊](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="3c20a-181">按一下 [Microsoft Azure Web Apps] 。</span><span class="sxs-lookup"><span data-stu-id="3c20a-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="3c20a-182">按一下**新增**toocreate 新的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c20a-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="3c20a-183">填寫下列欄位的 hello，並按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="3c20a-184">**Web 應用程式名稱**</span><span class="sxs-lookup"><span data-stu-id="3c20a-184">**Web App name**</span></span>
   * <span data-ttu-id="3c20a-185">**App Service 計劃**</span><span class="sxs-lookup"><span data-stu-id="3c20a-185">**App Service plan**</span></span>
   * <span data-ttu-id="3c20a-186">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="3c20a-186">**Resource group**</span></span>
   * <span data-ttu-id="3c20a-187">**區域**</span><span class="sxs-lookup"><span data-stu-id="3c20a-187">**Region**</span></span>
   * <span data-ttu-id="3c20a-188">保留**資料庫伺服器**設定得**沒有資料庫**</span><span class="sxs-lookup"><span data-stu-id="3c20a-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="3c20a-189">接受所有其他預設值並按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="3c20a-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="3c20a-190">網頁瀏覽器會自動開啟 toohello 已發佈的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c20a-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="3c20a-191">如果您瀏覽 toohello 有關頁面，您會看到它會使用 hello **In-memory**儲存機制、 不 hello **Azure 資料表儲存體**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3c20a-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="3c20a-192">這是因為 hello 環境變數上未設定 hello Web 應用程式的執行個體在 Azure 應用程式服務中，因此它會使用 hello 中指定的預設值**settings.py**。</span><span class="sxs-lookup"><span data-stu-id="3c20a-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="3c20a-193">設定 hello Web 應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="3c20a-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="3c20a-194">在本節中，我們會將設定環境變數 hello Web 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="3c20a-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="3c20a-195">在[Azure 入口網站]，開啟 hello web 應用程式的刀鋒視窗中，依序按一下**瀏覽** > **應用程式服務**> web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="3c20a-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="3c20a-196">在您的 Web 應用程式刀鋒視窗中，按一下 [所有設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="3c20a-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="3c20a-197">捲動 toohello**應用程式設定**區段，並設定 hello 值**儲存機制\_名稱**，**儲存體\_名稱**和**儲存體\_金鑰**hello 中所述**設定 hello 專案**上一節。</span><span class="sxs-lookup"><span data-stu-id="3c20a-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![應用程式設定](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="3c20a-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3c20a-199">Click on **Save**.</span></span> <span data-ttu-id="3c20a-200">收到 hello 變更已套用的 hello 通知之後，請按一下**瀏覽**hello Web 應用程式主要刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3c20a-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="3c20a-201">您應該看到 hello web 應用程式工作，如預期般，使用 hello **Azure 資料表儲存體**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3c20a-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="3c20a-202">恭喜！</span><span class="sxs-lookup"><span data-stu-id="3c20a-202">Congratulations!</span></span>
   
     ![Web Browser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="3c20a-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c20a-204">Next steps</span></span>
<span data-ttu-id="3c20a-205">遵循這些連結 toolearn 更多關於 Python Tools for Visual Studio、 Bottle 和 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="3c20a-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="3c20a-206">[Python Tools for Visual Studio 說明文件]</span><span class="sxs-lookup"><span data-stu-id="3c20a-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="3c20a-207">[Web 專案]</span><span class="sxs-lookup"><span data-stu-id="3c20a-207">[Web Projects]</span></span>
  * <span data-ttu-id="3c20a-208">[雲端服務專案]</span><span class="sxs-lookup"><span data-stu-id="3c20a-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="3c20a-209">[在 Microsoft Azure 上進行遠端偵錯]</span><span class="sxs-lookup"><span data-stu-id="3c20a-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="3c20a-210">[Bottle 說明文件]</span><span class="sxs-lookup"><span data-stu-id="3c20a-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="3c20a-211">[Azure 儲存體]</span><span class="sxs-lookup"><span data-stu-id="3c20a-211">[Azure Storage]</span></span>
* <span data-ttu-id="3c20a-212">[Azure SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="3c20a-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="3c20a-213">[如何 tooUse hello 來自 Python 的資料表儲存體服務]</span><span class="sxs-lookup"><span data-stu-id="3c20a-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="3c20a-214">變更的項目</span><span class="sxs-lookup"><span data-stu-id="3c20a-214">What's changed</span></span>
* <span data-ttu-id="3c20a-215">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3c20a-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python 開發人員中心]: /develop/python/
[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md
[文件]:../cosmos-db/table-storage-how-to-use-python.md
[如何 tooUse hello 來自 Python 的資料表儲存體服務]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure 入口網站]: https://portal.azure.com
[Azure SDK for.NET]: http://azure.microsoft.com/downloads/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs
[Bottle 說明文件]: http://bottlepy.org/docs/dev/index.html
[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027
[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure 儲存體]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK for Python]: https://github.com/Azure/azure-sdk-for-python
