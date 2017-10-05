---
title: "Azure 上使用 Python Tools 2.2 for Visual Studio 的 Flask 和 Azure 資料表儲存體"
description: "了解如何使用 Python Tools for Visual Studio 建立 Flask Web 應用程式，藉此將資料儲存在 Azure 資料表儲存體中，並部署到 Azure App Service Web Apps。"
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 2e1bc8eebd0b67b965cc70ac4b5dfe03c4720ddf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="6bebe-103">Azure 上使用 Python Tools 2.2 for Visual Studio 的 Flask 和 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="6bebe-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="6bebe-104">在此教學課程中，我們將使用 [Python Tools for Visual Studio] ，並使用其中一個 PTVS 範例範本來建立簡單的民調 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="6bebe-105">本教學課程也提供 [教學影片](https://www.youtube.com/watch?v=qUtZWtPwbTk)。</span><span class="sxs-lookup"><span data-stu-id="6bebe-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="6bebe-106">民調 Web 應用程式會為其儲存機制定義一個抽象概念，讓您輕鬆地切換不同類型的儲存機制 (記憶體內部、Azure 資料表儲存體、MongoDB)。</span><span class="sxs-lookup"><span data-stu-id="6bebe-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="6bebe-107">我們將學習如何建立 Azure 儲存體帳戶、如何設定 Web 應用程式以使用 Azure 資料表儲存體，以及如何將 Web 應用程式發佈至 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="6bebe-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="6bebe-108">如需更多相關文章 (說明透過使用 Bottle、Flask 和 Django 架構的 PTVS、透過 MongoDB、Azure 資料表儲存體、MySQL 和 SQL Database 服務進行 Azure App Service Web Apps 開發)，請參閱 [Python 開發人員中心] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="6bebe-109">雖然本文著重於 App Service，但其開發步驟類似於開發 [Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="6bebe-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bebe-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6bebe-110">Prerequisites</span></span>
* <span data-ttu-id="6bebe-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="6bebe-111">Visual Studio 2015</span></span>
* <span data-ttu-id="6bebe-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6bebe-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="6bebe-113">[Python Tools 2.2 for Visual Studio 範例 VSIX]</span><span class="sxs-lookup"><span data-stu-id="6bebe-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="6bebe-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="6bebe-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="6bebe-115">[Python 2.7 32 位元]或 [Python 3.4 32 位元]</span><span class="sxs-lookup"><span data-stu-id="6bebe-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="6bebe-116">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6bebe-117">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="6bebe-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="6bebe-118">建立專案</span><span class="sxs-lookup"><span data-stu-id="6bebe-118">Create the Project</span></span>
<span data-ttu-id="6bebe-119">在這一節中，我們將使用範例範本建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="6bebe-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="6bebe-120">我們將建立虛擬環境並安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="6bebe-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="6bebe-121">然後將使用預設記憶體內部存放庫，在本機執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="6bebe-122">在 Visual Studio 中，選取 [檔案]、[新增專案]。</span><span class="sxs-lookup"><span data-stu-id="6bebe-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="6bebe-123">在 [Python]、[範例] 之下可取得 [Python Tools 2.2 for Visual Studio 範例 VSIX] 中的專案範本。</span><span class="sxs-lookup"><span data-stu-id="6bebe-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="6bebe-124">選取 [Polls Flask Web Project]  ，然後按一下 [確定] 以建立專案。</span><span class="sxs-lookup"><span data-stu-id="6bebe-124">Select **Polls Flask Web Project** and click OK to create the project.</span></span>
   
     ![New Project Dialog](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="6bebe-126">系統會提示您安裝外部套件。</span><span class="sxs-lookup"><span data-stu-id="6bebe-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="6bebe-127">選取 [安裝到虛擬環境] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-127">Select **Install into a virtual environment**.</span></span>
   
     ![外部套件對話方塊](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="6bebe-129">選取 [Python 2.7] 或 [Python 3.4] 作為基礎解譯器。</span><span class="sxs-lookup"><span data-stu-id="6bebe-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="6bebe-131">按 `F5`確認應用程式可運作。</span><span class="sxs-lookup"><span data-stu-id="6bebe-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="6bebe-132">根據預設，應用程式會使用記憶體內部儲存機制，而不需要進行任何設定。</span><span class="sxs-lookup"><span data-stu-id="6bebe-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="6bebe-133">當 Web 伺服器停止時，所有資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="6bebe-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="6bebe-134">按一下 [Create Sample Polls] ，然後按一下某項民調並投票。</span><span class="sxs-lookup"><span data-stu-id="6bebe-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="6bebe-136">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6bebe-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="6bebe-137">若要使用儲存體作業，您需要 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bebe-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="6bebe-138">您可以依照下列步驟來建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bebe-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="6bebe-139">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6bebe-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6bebe-140">按一下入口網站左上方的 [新增] 圖示，然後按一下 [資料+儲存體]  >  [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="6bebe-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="6bebe-141">按一下 [建立]，接著為儲存體帳戶指定唯一名稱，並為它建立新的[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6bebe-141">Click on **Create**, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Quick Create](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="6bebe-143">建立儲存體帳戶後，[通知] 按鈕便會閃爍綠色 [成功]，儲存體帳戶的刀鋒視窗會開啟，顯示它屬於您所建立的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="6bebe-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="6bebe-144">按一下儲存體帳戶刀鋒視窗中的 [存取金鑰]  部分。</span><span class="sxs-lookup"><span data-stu-id="6bebe-144">Click the **Access Keys** part in the storage account's blade.</span></span> <span data-ttu-id="6bebe-145">記下帳戶名稱和金鑰1。</span><span class="sxs-lookup"><span data-stu-id="6bebe-145">Take note of the account name and the key1.</span></span>
   
      ![之間的信任](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="6bebe-147">我們在下一節中將需要此資訊來設定您的專案。</span><span class="sxs-lookup"><span data-stu-id="6bebe-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="6bebe-148">設定專案</span><span class="sxs-lookup"><span data-stu-id="6bebe-148">Configure the Project</span></span>
<span data-ttu-id="6bebe-149">在這一節中，我們會將應用程式設定為使用我們剛才建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bebe-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="6bebe-150">我們將了解如何從 Azure 入口網站取得連線設定。</span><span class="sxs-lookup"><span data-stu-id="6bebe-150">We'll see how to obtain connection settings from the Azure Portal.</span></span> <span data-ttu-id="6bebe-151">然後會在本機執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-151">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="6bebe-152">在 Visual Studio 的 [方案總管] 中，在您的專案節點上按一下滑鼠右鍵，然後選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="6bebe-153">按一下 [偵錯]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6bebe-153">Click on the **Debug** tab.</span></span>
   
     ![專案偵錯設定](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="6bebe-155">在 [偵錯伺服器命令]、[環境] 中設定應用程式所需的環境變數值。</span><span class="sxs-lookup"><span data-stu-id="6bebe-155">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="6bebe-156">此舉會在您 [開始偵錯] 時設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="6bebe-156">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="6bebe-157">如果您想要在 [啟動但不偵錯] 時設定變數，請在 [執行伺服器命令] 下設定相同的值。</span><span class="sxs-lookup"><span data-stu-id="6bebe-157">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="6bebe-158">此外，您也可以使用 Windows 控制台定義環境變數。</span><span class="sxs-lookup"><span data-stu-id="6bebe-158">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="6bebe-159">如果想要避免將認證儲存在原始碼 / 專案檔案中，這是比較好的選項。</span><span class="sxs-lookup"><span data-stu-id="6bebe-159">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="6bebe-160">請注意，您必須重新啟動 Visual Studio，新的環境值才可用於應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-160">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="6bebe-161">實作 Azure 資料表儲存體儲存機制的程式碼位於 **models/azuretablestorage.py**。</span><span class="sxs-lookup"><span data-stu-id="6bebe-161">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="6bebe-162">如需有關如何從 Python 使用表格服務的詳細資訊，請參閱 [說明文件] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-162">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="6bebe-163">使用 `F5`執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-163">Run the application with `F5`.</span></span> <span data-ttu-id="6bebe-164">使用 [Create Sample Polls]  建立的民調以及投票所提交的資料將會在 Azure 資料表儲存體中序列化。</span><span class="sxs-lookup"><span data-stu-id="6bebe-164">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6bebe-165">Python 2.7 虛擬環境可能會在 Visual Studio 中造成例外狀況中斷。</span><span class="sxs-lookup"><span data-stu-id="6bebe-165">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="6bebe-166">按下 `F5` 以繼續載入 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="6bebe-166">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="6bebe-167">瀏覽至 [關於] 頁面，確認應用程式是使用「Azure 資料表儲存體」儲存機制。</span><span class="sxs-lookup"><span data-stu-id="6bebe-167">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Web Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="6bebe-169">探索 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="6bebe-169">Explore the Azure Table Storage</span></span>
<span data-ttu-id="6bebe-170">使用 Visual Studio 中的 [雲端總管] 即可輕易檢視和編輯儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="6bebe-170">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="6bebe-171">在這一節中，我們將使用 [伺服器總管] 來檢視民調應用程式資料表的內容。</span><span class="sxs-lookup"><span data-stu-id="6bebe-171">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="6bebe-172">這需要安裝 Microsoft Azure Tools (可在 [Azure SDK for .NET]中取得)。</span><span class="sxs-lookup"><span data-stu-id="6bebe-172">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="6bebe-173">開啟 [雲端總管] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="6bebe-174">依序展開 [儲存體帳戶]、您的儲存體帳戶和 [資料表]。</span><span class="sxs-lookup"><span data-stu-id="6bebe-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![雲端總管](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="6bebe-176">按兩下 [民調] 或 [選擇] 資料表可在文件視窗中檢視目錄，以及新增/移除/編輯實體。</span><span class="sxs-lookup"><span data-stu-id="6bebe-176">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![資料表查詢結果](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="6bebe-178">將 Web 應用程式發佈至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6bebe-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="6bebe-179">Azure .NET SDK 提供簡單的方法將 Web 應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="6bebe-179">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="6bebe-180">在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="6bebe-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![發行 Web 對話方塊](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="6bebe-182">按一下 [Microsoft Azure Web Apps] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="6bebe-183">按一下 [新增]  以建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="6bebe-184">填寫下列欄位，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-184">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="6bebe-185">**Web 應用程式名稱**</span><span class="sxs-lookup"><span data-stu-id="6bebe-185">**Web App name**</span></span>
   * <span data-ttu-id="6bebe-186">**App Service 計劃**</span><span class="sxs-lookup"><span data-stu-id="6bebe-186">**App Service plan**</span></span>
   * <span data-ttu-id="6bebe-187">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="6bebe-187">**Resource group**</span></span>
   * <span data-ttu-id="6bebe-188">**區域**</span><span class="sxs-lookup"><span data-stu-id="6bebe-188">**Region**</span></span>
   * <span data-ttu-id="6bebe-189">讓「資料庫伺服器」維持設定為「沒有資料庫」</span><span class="sxs-lookup"><span data-stu-id="6bebe-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="6bebe-190">接受所有其他預設值並按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="6bebe-191">您的 Web 瀏覽器將會自動開啟到已發佈的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bebe-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="6bebe-192">如果您瀏覽至 [關於] 頁面，您會看到它使用 [記憶體內部] 儲存機制，而非 [Azure 資料表儲存體] 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="6bebe-192">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="6bebe-193">這是因為 Azure App Service 中未設定 Web Apps 執行個體的環境變數，所以使用在 **settings.py**中指定的預設值。</span><span class="sxs-lookup"><span data-stu-id="6bebe-193">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="6bebe-194">設定 Web Apps 執行個體</span><span class="sxs-lookup"><span data-stu-id="6bebe-194">Configure the Web Apps instance</span></span>
<span data-ttu-id="6bebe-195">在本節中，我們將設定 Web Apps 執行個體的環境變數。</span><span class="sxs-lookup"><span data-stu-id="6bebe-195">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="6bebe-196">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [瀏覽]  >  [應用程式服務] > [您的 Web 應用程式名稱] 以開啟 Web 應用程式的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6bebe-196">In [Azure Portal](https://portal.azure.com), open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="6bebe-197">在您的 Web 應用程式刀鋒視窗中，按一下 [所有設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="6bebe-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="6bebe-198">向下捲動到 [應用程式設定] 區段，並設定 [REPOSITORY**NAME]\_**、[STORAGE\_NAME] 和 [STORAGE\_KEY] 的值，如前面的＜設定專案＞一節所述。</span><span class="sxs-lookup"><span data-stu-id="6bebe-198">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![應用程式設定](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="6bebe-200">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6bebe-200">Click on **Save**.</span></span> <span data-ttu-id="6bebe-201">您收到已套用變更的通知後，請按一下 Web 應用程式主要刀鋒視窗上的 [瀏覽]  。</span><span class="sxs-lookup"><span data-stu-id="6bebe-201">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="6bebe-202">透過使用「Azure 資料表儲存體」  儲存機制，應該會看到 Web 應用程式如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="6bebe-202">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="6bebe-203">恭喜！</span><span class="sxs-lookup"><span data-stu-id="6bebe-203">Congratulations!</span></span>
   
     ![Web Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="6bebe-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bebe-205">Next steps</span></span>
<span data-ttu-id="6bebe-206">請遵循下列連結以深入了解 Python Tools for Visual Studio、Flask 和 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="6bebe-206">Follow these links to learn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="6bebe-207">[Python Tools for Visual Studio 說明文件]</span><span class="sxs-lookup"><span data-stu-id="6bebe-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="6bebe-208">[Web 專案]</span><span class="sxs-lookup"><span data-stu-id="6bebe-208">[Web Projects]</span></span>
  * <span data-ttu-id="6bebe-209">[雲端服務專案]</span><span class="sxs-lookup"><span data-stu-id="6bebe-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="6bebe-210">[在 Microsoft Azure 上進行遠端偵錯]</span><span class="sxs-lookup"><span data-stu-id="6bebe-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="6bebe-211">[Flask 說明文件 (英文)]</span><span class="sxs-lookup"><span data-stu-id="6bebe-211">[Flask Documentation]</span></span>
* <span data-ttu-id="6bebe-212">[Azure 儲存體]</span><span class="sxs-lookup"><span data-stu-id="6bebe-212">[Azure Storage]</span></span>
* <span data-ttu-id="6bebe-213">[Azure SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="6bebe-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="6bebe-214">[如何從 Python 使用資料表儲存體服務]</span><span class="sxs-lookup"><span data-stu-id="6bebe-214">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6bebe-215">變更的項目</span><span class="sxs-lookup"><span data-stu-id="6bebe-215">What's changed</span></span>
* <span data-ttu-id="6bebe-216">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6bebe-216">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python 開發人員中心]: /develop/python/
[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md
[說明文件]:../cosmos-db/table-storage-how-to-use-python.md
[如何從 Python 使用資料表儲存體服務]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK for .NET]: http://azure.microsoft.com/downloads/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs
[Flask 說明文件 (英文)]: http://flask.pocoo.org/
[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027
[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure 儲存體]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK for Python]: https://github.com/Azure/azure-sdk-for-python
