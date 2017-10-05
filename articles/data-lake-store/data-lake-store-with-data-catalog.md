---
title: "在 Azure 資料目錄中註冊來自 Data Lake Store 的資料 | Microsoft Docs"
description: "在 Azure 資料目錄中註冊來自 Data Lake Store 的資料"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 41f7ca0d638479b013e77cb949a71c566bc66aa4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a><span data-ttu-id="75b42-103">在 Azure 資料目錄中註冊來自 Data Lake Store 的資料</span><span class="sxs-lookup"><span data-stu-id="75b42-103">Register data from Data Lake Store in Azure Data Catalog</span></span>
<span data-ttu-id="75b42-104">在本文中，您將了解如何使用 Azure 資料目錄整合 Azure Data Lake Store，讓您的資料可在組織中藉由與資料目錄整合進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="75b42-104">In this article you will learn how to integrate Azure Data Lake Store with Azure Data Catalog to make your data discoverable within an organization by integrating it with Data Catalog.</span></span> <span data-ttu-id="75b42-105">如需編目資料的詳細資訊，請參閱 [Azure 資料目錄](../data-catalog/data-catalog-what-is-data-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="75b42-105">For more information on cataloging data, see [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md).</span></span> <span data-ttu-id="75b42-106">若要了解您可以使用資料目錄的案例，請參閱 [Azure 資料目錄常見案例](../data-catalog/data-catalog-common-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="75b42-106">To understand scenarios in which you can use Data Catalog, see [Azure Data Catalog common scenarios](../data-catalog/data-catalog-common-scenarios.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75b42-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="75b42-107">Prerequisites</span></span>
<span data-ttu-id="75b42-108">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="75b42-108">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="75b42-109">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="75b42-109">**An Azure subscription**.</span></span> <span data-ttu-id="75b42-110">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="75b42-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="75b42-111">**啟用您的 Azure 訂用帳戶** 以使用「Data Lake Store 公開預覽版」。</span><span class="sxs-lookup"><span data-stu-id="75b42-111">**Enable your Azure subscription** for Data Lake Store Public Preview.</span></span> <span data-ttu-id="75b42-112">請參閱 [指示](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="75b42-112">See [instructions](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="75b42-113">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="75b42-113">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="75b42-114">遵循 [使用 Azure 入口網站開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="75b42-114">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="75b42-115">在本教學課程中，讓我們建立名為 **datacatalogstore**的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="75b42-115">For this tutorial, let us create a Data Lake Store account called **datacatalogstore**.</span></span>

    <span data-ttu-id="75b42-116">一旦您建立帳戶之後，請將範例資料集上傳給它。</span><span class="sxs-lookup"><span data-stu-id="75b42-116">Once you have created the account, upload a sample data set to it.</span></span> <span data-ttu-id="75b42-117">在本教學課程中，讓我們上傳 **Azure Data Lake Git 儲存機制** 中 [AmbulanceData](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/)資料夾下的所有 .csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="75b42-117">For this tutorial, let us upload all the .csv files under the **AmbulanceData** folder in the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/).</span></span> <span data-ttu-id="75b42-118">您可以使用各種用戶端，例如： [Azure 儲存體總管](http://storageexplorer.com/)，將資料上傳至 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="75b42-118">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>
* <span data-ttu-id="75b42-119">**Azure 資料目錄**。</span><span class="sxs-lookup"><span data-stu-id="75b42-119">**Azure Data Catalog**.</span></span> <span data-ttu-id="75b42-120">您的組織必須為組織建立 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="75b42-120">Your organization must already have an Azure Data Catalog created for your organization.</span></span> <span data-ttu-id="75b42-121">每個組織只允許有一個目錄。</span><span class="sxs-lookup"><span data-stu-id="75b42-121">Only one catalog is allowed for each organization.</span></span>

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a><span data-ttu-id="75b42-122">註冊 Data Lake Store 做為資料目錄的來源</span><span class="sxs-lookup"><span data-stu-id="75b42-122">Register Data Lake Store as a source for Data Catalog</span></span>

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. <span data-ttu-id="75b42-123">前往 `https://azure.microsoft.com/services/data-catalog`，然後按一下 [開始使用]。</span><span class="sxs-lookup"><span data-stu-id="75b42-123">Go to `https://azure.microsoft.com/services/data-catalog`, and click **Get started**.</span></span>
2. <span data-ttu-id="75b42-124">登入 Azure 資料目錄入口網站，再按一下 [發佈資料] 。</span><span class="sxs-lookup"><span data-stu-id="75b42-124">Log into the Azure Data Catalog portal, and click **Publish data**.</span></span>

    <span data-ttu-id="75b42-125">![註冊資料來源](./media/data-lake-store-with-data-catalog/register-data-source.png "註冊資料來源")</span><span class="sxs-lookup"><span data-stu-id="75b42-125">![Register a data source](./media/data-lake-store-with-data-catalog/register-data-source.png "Register a data source")</span></span>
3. <span data-ttu-id="75b42-126">在下一個頁面上，按一下 [啟動應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="75b42-126">On the next page, click **Launch Application**.</span></span> <span data-ttu-id="75b42-127">這樣會下載電腦上的應用程式資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="75b42-127">This will download the application manifest file on your computer.</span></span> <span data-ttu-id="75b42-128">按兩下此資訊清單檔案以啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b42-128">Double-click the manifest file to start the application.</span></span>
4. <span data-ttu-id="75b42-129">在 [歡迎使用] 頁面上，按一下 [登入] ，並輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="75b42-129">On the Welcome page, click **Sign in**, and enter your credentials.</span></span>

    <span data-ttu-id="75b42-130">![歡迎使用畫面](./media/data-lake-store-with-data-catalog/welcome.screen.png "歡迎使用畫面")</span><span class="sxs-lookup"><span data-stu-id="75b42-130">![Welcome screen](./media/data-lake-store-with-data-catalog/welcome.screen.png "Welcome screen")</span></span>
5. <span data-ttu-id="75b42-131">在 [選取資料來源] 頁面上，選取 [Azure Data Lake]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="75b42-131">On the Select a Data Source page, select **Azure Data Lake**, and then click **Next**.</span></span>

    <span data-ttu-id="75b42-132">![選取資料來源](./media/data-lake-store-with-data-catalog/select-source.png "選取資料來源")</span><span class="sxs-lookup"><span data-stu-id="75b42-132">![Select data source](./media/data-lake-store-with-data-catalog/select-source.png "Select data source")</span></span>
6. <span data-ttu-id="75b42-133">在下一個頁面上，提供您想要在資料目錄中註冊的 Data Lake Store 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="75b42-133">On the next page, provide the Data Lake Store account name that you want to register in Data Catalog.</span></span> <span data-ttu-id="75b42-134">其他選項保留為預設值，然後按一下 [連線] 。</span><span class="sxs-lookup"><span data-stu-id="75b42-134">Leave the other options as default and then click **Connect**.</span></span>

    <span data-ttu-id="75b42-135">![連接到資料來源](./media/data-lake-store-with-data-catalog/connect-to-source.png "連接到資料來源")</span><span class="sxs-lookup"><span data-stu-id="75b42-135">![Connect to data source](./media/data-lake-store-with-data-catalog/connect-to-source.png "Connect to data source")</span></span>
7. <span data-ttu-id="75b42-136">下一個頁面可以分成下列區段。</span><span class="sxs-lookup"><span data-stu-id="75b42-136">The next page can be divided into the following segments.</span></span>

    <span data-ttu-id="75b42-137">a.</span><span class="sxs-lookup"><span data-stu-id="75b42-137">a.</span></span> <span data-ttu-id="75b42-138">[伺服器階層] 方塊代表 Data Lake Store 帳戶資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="75b42-138">The **Server Hierarchy** box represents the Data Lake Store account folder structure.</span></span> <span data-ttu-id="75b42-139">[$Root] 代表 Data Lake Store 帳戶根目錄，而 [AmbulanceData] 則代表在 Data Lake Store 帳戶的根目錄中建立的資料夾。</span><span class="sxs-lookup"><span data-stu-id="75b42-139">**$Root** represents the Data Lake Store account root, and **AmbulanceData** represents the folder created in the root of the Data Lake Store account.</span></span>

    <span data-ttu-id="75b42-140">b.</span><span class="sxs-lookup"><span data-stu-id="75b42-140">b.</span></span> <span data-ttu-id="75b42-141">[可用物件] 方塊會列出 [AmbulanceData] 資料夾下的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="75b42-141">The **Available objects** box lists the files and folders under the **AmbulanceData** folder.</span></span>

    <span data-ttu-id="75b42-142">c.</span><span class="sxs-lookup"><span data-stu-id="75b42-142">c.</span></span> <span data-ttu-id="75b42-143">[要註冊的物件] 方塊會列出您想要在「Azure 資料目錄」中註冊的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="75b42-143">**Objects to be registered box** lists the files and folders that you want to register in Azure Data Catalog.</span></span>

    <span data-ttu-id="75b42-144">![檢視資料結構](./media/data-lake-store-with-data-catalog/view-data-structure.png "檢視資料結構")</span><span class="sxs-lookup"><span data-stu-id="75b42-144">![View data structure](./media/data-lake-store-with-data-catalog/view-data-structure.png "View data structure")</span></span>
8. <span data-ttu-id="75b42-145">在本教學課程中，您應該在目錄中註冊所有檔案。</span><span class="sxs-lookup"><span data-stu-id="75b42-145">For this tutorial, you should register all the files in the directory.</span></span> <span data-ttu-id="75b42-146">因此，請按一下 (![移動物件](./media/data-lake-store-with-data-catalog/move-objects.png "移動物件")) 按鈕來將所有檔案移至 [要註冊的物件] 方塊。</span><span class="sxs-lookup"><span data-stu-id="75b42-146">For that, click the (![move objects](./media/data-lake-store-with-data-catalog/move-objects.png "Move objects")) button to move all the files to **Objects to be registered** box.</span></span>

    <span data-ttu-id="75b42-147">因為資料將會在整個組織的資料目錄中註冊，建議新增一些元資料，讓您稍後可以用來快速尋找資料。</span><span class="sxs-lookup"><span data-stu-id="75b42-147">Because the data will be registered in an organization-wide data catalog, it is a recommened approach to add some metadata which you can later use to quickly locate the data.</span></span> <span data-ttu-id="75b42-148">例如，您可以新增資料擁有者 (例如，上傳資料的人員) 的電子郵件地址，或新增可識別資料的標籤。</span><span class="sxs-lookup"><span data-stu-id="75b42-148">For example, you can add an e-mail address for the data owner (for example, one who is uploading the data) or add a tag to identify the data.</span></span> <span data-ttu-id="75b42-149">下方螢幕擷取畫面顯示我們新增至資料的標籤。</span><span class="sxs-lookup"><span data-stu-id="75b42-149">The screen capture below shows a tag that we add to the data.</span></span>

    <span data-ttu-id="75b42-150">![檢視資料結構](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "檢視資料結構")</span><span class="sxs-lookup"><span data-stu-id="75b42-150">![View data structure](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "View data structure")</span></span>

    <span data-ttu-id="75b42-151">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="75b42-151">Click **Register**.</span></span>
9. <span data-ttu-id="75b42-152">下列螢幕擷取畫面表示已成功在資料目錄中註冊資料。</span><span class="sxs-lookup"><span data-stu-id="75b42-152">The following screen capture denotes that the data is successfully registered in the Data Catalog.</span></span>

    <span data-ttu-id="75b42-153">![註冊完成](./media/data-lake-store-with-data-catalog/registration-complete.png "檢視資料結構")</span><span class="sxs-lookup"><span data-stu-id="75b42-153">![Registration complete](./media/data-lake-store-with-data-catalog/registration-complete.png "View data structure")</span></span>
10. <span data-ttu-id="75b42-154">按一下 [檢視入口網站]  以回到資料目錄入口網站，並確認您現在可以從入口網站存取已註冊的資料。</span><span class="sxs-lookup"><span data-stu-id="75b42-154">Click **View Portal** to go back to the Data Catalog portal and verify that you can now access the registered data from the portal.</span></span> <span data-ttu-id="75b42-155">若要搜尋資料，您可以使用您在註冊資料時使用的標籤。</span><span class="sxs-lookup"><span data-stu-id="75b42-155">To search the data, you can use the tag you used while registering the data.</span></span>

     <span data-ttu-id="75b42-156">![搜尋目錄中的資料](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "搜尋目錄中的資料")</span><span class="sxs-lookup"><span data-stu-id="75b42-156">![Search data in catalog](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Search data in catalog")</span></span>
11. <span data-ttu-id="75b42-157">您現在可以執行將註釋和文件新增至資料等作業。</span><span class="sxs-lookup"><span data-stu-id="75b42-157">You can now perform operations like adding annotations and documentation to the data.</span></span> <span data-ttu-id="75b42-158">如需詳細資訊，請參閱下列連結。</span><span class="sxs-lookup"><span data-stu-id="75b42-158">For more information, see the following links.</span></span>

    * [<span data-ttu-id="75b42-159">註釋資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="75b42-159">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
    * [<span data-ttu-id="75b42-160">記錄資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="75b42-160">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a><span data-ttu-id="75b42-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="75b42-161">See also</span></span>
* [<span data-ttu-id="75b42-162">註釋資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="75b42-162">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
* [<span data-ttu-id="75b42-163">記錄資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="75b42-163">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)
* [<span data-ttu-id="75b42-164">整合 Data Lake Store 與其他 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="75b42-164">Integrate Data Lake Store with other Azure services</span></span>](data-lake-store-integrate-with-other-services.md)
