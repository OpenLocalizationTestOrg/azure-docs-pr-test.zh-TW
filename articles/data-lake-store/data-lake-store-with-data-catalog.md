---
title: "aaaRegister 資料從 Azure 資料目錄中的資料湖存放區 |Microsoft 文件"
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
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a><span data-ttu-id="f81a1-103">在 Azure 資料目錄中註冊來自 Data Lake Store 的資料</span><span class="sxs-lookup"><span data-stu-id="f81a1-103">Register data from Data Lake Store in Azure Data Catalog</span></span>
<span data-ttu-id="f81a1-104">在本文中，您將學習如何 toointegrate Azure 資料湖存放區與 Azure 資料目錄 toomake 您探索組織內的資料藉由整合以資料目錄。</span><span class="sxs-lookup"><span data-stu-id="f81a1-104">In this article you will learn how toointegrate Azure Data Lake Store with Azure Data Catalog toomake your data discoverable within an organization by integrating it with Data Catalog.</span></span> <span data-ttu-id="f81a1-105">如需編目資料的詳細資訊，請參閱 [Azure 資料目錄](../data-catalog/data-catalog-what-is-data-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="f81a1-105">For more information on cataloging data, see [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md).</span></span> <span data-ttu-id="f81a1-106">toounderstand 案例中，您可以使用資料目錄，請參閱[Azure 資料目錄的常見案例](../data-catalog/data-catalog-common-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="f81a1-106">toounderstand scenarios in which you can use Data Catalog, see [Azure Data Catalog common scenarios](../data-catalog/data-catalog-common-scenarios.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f81a1-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="f81a1-107">Prerequisites</span></span>
<span data-ttu-id="f81a1-108">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f81a1-108">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="f81a1-109">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-109">**An Azure subscription**.</span></span> <span data-ttu-id="f81a1-110">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f81a1-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f81a1-111">**啟用您的 Azure 訂用帳戶** 以使用「Data Lake Store 公開預覽版」。</span><span class="sxs-lookup"><span data-stu-id="f81a1-111">**Enable your Azure subscription** for Data Lake Store Public Preview.</span></span> <span data-ttu-id="f81a1-112">請參閱 [指示](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f81a1-112">See [instructions](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="f81a1-113">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-113">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="f81a1-114">請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f81a1-114">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="f81a1-115">在本教學課程中，讓我們建立名為 **datacatalogstore**的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f81a1-115">For this tutorial, let us create a Data Lake Store account called **datacatalogstore**.</span></span>

    <span data-ttu-id="f81a1-116">當您建立 hello 帳戶之後時上, 傳範例資料集 tooit。</span><span class="sxs-lookup"><span data-stu-id="f81a1-116">Once you have created hello account, upload a sample data set tooit.</span></span> <span data-ttu-id="f81a1-117">本教學課程，讓我們上載 hello 底下的所有 hello.csv 檔案**AmbulanceData**資料夾中 hello [Azure 資料湖 Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/)。</span><span class="sxs-lookup"><span data-stu-id="f81a1-117">For this tutorial, let us upload all hello .csv files under hello **AmbulanceData** folder in hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/).</span></span> <span data-ttu-id="f81a1-118">您可以使用各種用戶端，例如[Azure 儲存體總管](http://storageexplorer.com/)，tooupload 資料 tooa blob 容器。</span><span class="sxs-lookup"><span data-stu-id="f81a1-118">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>
* <span data-ttu-id="f81a1-119">**Azure 資料目錄**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-119">**Azure Data Catalog**.</span></span> <span data-ttu-id="f81a1-120">您的組織必須為組織建立 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="f81a1-120">Your organization must already have an Azure Data Catalog created for your organization.</span></span> <span data-ttu-id="f81a1-121">每個組織只允許有一個目錄。</span><span class="sxs-lookup"><span data-stu-id="f81a1-121">Only one catalog is allowed for each organization.</span></span>

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a><span data-ttu-id="f81a1-122">註冊 Data Lake Store 做為資料目錄的來源</span><span class="sxs-lookup"><span data-stu-id="f81a1-122">Register Data Lake Store as a source for Data Catalog</span></span>

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. <span data-ttu-id="f81a1-123">跳過`https://azure.microsoft.com/services/data-catalog`，然後按一下**開始**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-123">Go too`https://azure.microsoft.com/services/data-catalog`, and click **Get started**.</span></span>
2. <span data-ttu-id="f81a1-124">登入 hello Azure 資料目錄入口網站，並按一下**發行資料**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-124">Log into hello Azure Data Catalog portal, and click **Publish data**.</span></span>

    <span data-ttu-id="f81a1-125">![註冊資料來源](./media/data-lake-store-with-data-catalog/register-data-source.png "註冊資料來源")</span><span class="sxs-lookup"><span data-stu-id="f81a1-125">![Register a data source](./media/data-lake-store-with-data-catalog/register-data-source.png "Register a data source")</span></span>
3. <span data-ttu-id="f81a1-126">在 hello 下一個頁面上，按一下 **啟動應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-126">On hello next page, click **Launch Application**.</span></span> <span data-ttu-id="f81a1-127">這會下載您的電腦上 hello 應用程式資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="f81a1-127">This will download hello application manifest file on your computer.</span></span> <span data-ttu-id="f81a1-128">按兩下 hello 資訊清單檔案 toostart hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f81a1-128">Double-click hello manifest file toostart hello application.</span></span>
4. <span data-ttu-id="f81a1-129">在 hello  褖畫惎 頁面上，按一下 **登入**，並輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="f81a1-129">On hello Welcome page, click **Sign in**, and enter your credentials.</span></span>

    <span data-ttu-id="f81a1-130">![歡迎使用畫面](./media/data-lake-store-with-data-catalog/welcome.screen.png "歡迎使用畫面")</span><span class="sxs-lookup"><span data-stu-id="f81a1-130">![Welcome screen](./media/data-lake-store-with-data-catalog/welcome.screen.png "Welcome screen")</span></span>
5. <span data-ttu-id="f81a1-131">在 hello 選取資料來源 頁面上，選取  **Azure 資料湖**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-131">On hello Select a Data Source page, select **Azure Data Lake**, and then click **Next**.</span></span>

    <span data-ttu-id="f81a1-132">![選取資料來源](./media/data-lake-store-with-data-catalog/select-source.png "選取資料來源")</span><span class="sxs-lookup"><span data-stu-id="f81a1-132">![Select data source](./media/data-lake-store-with-data-catalog/select-source.png "Select data source")</span></span>
6. <span data-ttu-id="f81a1-133">在 hello 下一個頁面上，提供 hello 想 tooregister 資料目錄中的 Data Lake Store 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f81a1-133">On hello next page, provide hello Data Lake Store account name that you want tooregister in Data Catalog.</span></span> <span data-ttu-id="f81a1-134">保留 hello 做為預設值的其他選項，然後按**連接**。</span><span class="sxs-lookup"><span data-stu-id="f81a1-134">Leave hello other options as default and then click **Connect**.</span></span>

    <span data-ttu-id="f81a1-135">![連接 toodata 來源](./media/data-lake-store-with-data-catalog/connect-to-source.png "連接 toodata 來源")</span><span class="sxs-lookup"><span data-stu-id="f81a1-135">![Connect toodata source](./media/data-lake-store-with-data-catalog/connect-to-source.png "Connect toodata source")</span></span>
7. <span data-ttu-id="f81a1-136">hello 下一頁可以分成下列區段的 hello。</span><span class="sxs-lookup"><span data-stu-id="f81a1-136">hello next page can be divided into hello following segments.</span></span>

    <span data-ttu-id="f81a1-137">a.</span><span class="sxs-lookup"><span data-stu-id="f81a1-137">a.</span></span> <span data-ttu-id="f81a1-138">hello**伺服器階層**方塊都代表 hello Data Lake Store 帳戶的資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="f81a1-138">hello **Server Hierarchy** box represents hello Data Lake Store account folder structure.</span></span> <span data-ttu-id="f81a1-139">**$Root**代表 hello Data Lake Store 帳戶的根，和**AmbulanceData**代表 hello hello Data Lake Store 帳戶 hello 根目錄中建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="f81a1-139">**$Root** represents hello Data Lake Store account root, and **AmbulanceData** represents hello folder created in hello root of hello Data Lake Store account.</span></span>

    <span data-ttu-id="f81a1-140">b.</span><span class="sxs-lookup"><span data-stu-id="f81a1-140">b.</span></span> <span data-ttu-id="f81a1-141">hello**可用物件**方塊會列出 hello 檔案和資料夾下 hello **AmbulanceData**資料夾。</span><span class="sxs-lookup"><span data-stu-id="f81a1-141">hello **Available objects** box lists hello files and folders under hello **AmbulanceData** folder.</span></span>

    <span data-ttu-id="f81a1-142">c.</span><span class="sxs-lookup"><span data-stu-id="f81a1-142">c.</span></span> <span data-ttu-id="f81a1-143">**物件 toobe 註冊方塊**清單 hello 您想 tooregister 在 Azure 資料目錄中的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="f81a1-143">**Objects toobe registered box** lists hello files and folders that you want tooregister in Azure Data Catalog.</span></span>

    <span data-ttu-id="f81a1-144">![檢視資料結構](./media/data-lake-store-with-data-catalog/view-data-structure.png "檢視資料結構")</span><span class="sxs-lookup"><span data-stu-id="f81a1-144">![View data structure](./media/data-lake-store-with-data-catalog/view-data-structure.png "View data structure")</span></span>
8. <span data-ttu-id="f81a1-145">此教學課程中，您應該註冊所有 hello 檔案 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="f81a1-145">For this tutorial, you should register all hello files in hello directory.</span></span> <span data-ttu-id="f81a1-146">該作業，按一下 hello (![移動物件](./media/data-lake-store-with-data-catalog/move-objects.png "移動物件")) 所有 hello 按鈕 toomove 檔案太**註冊物件 toobe**方塊。</span><span class="sxs-lookup"><span data-stu-id="f81a1-146">For that, click hello (![move objects](./media/data-lake-store-with-data-catalog/move-objects.png "Move objects")) button toomove all hello files too**Objects toobe registered** box.</span></span>

    <span data-ttu-id="f81a1-147">因為 hello 資料將在整個組織的資料目錄中登錄，所以建議很接近 tooadd 一些可以在稍後使用的中繼資料 tooquickly 找出 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f81a1-147">Because hello data will be registered in an organization-wide data catalog, it is a recommened approach tooadd some metadata which you can later use tooquickly locate hello data.</span></span> <span data-ttu-id="f81a1-148">例如，您可以新增 hello 資料擁有者 （例如，一個人員會將 hello 資料上傳） 的電子郵件地址，或新增標記 tooidentify hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f81a1-148">For example, you can add an e-mail address for hello data owner (for example, one who is uploading hello data) or add a tag tooidentify hello data.</span></span> <span data-ttu-id="f81a1-149">hello 下列螢幕擷取畫面顯示標記，我們將新增 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="f81a1-149">hello screen capture below shows a tag that we add toohello data.</span></span>

    <span data-ttu-id="f81a1-150">![檢視資料結構](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "檢視資料結構")</span><span class="sxs-lookup"><span data-stu-id="f81a1-150">![View data structure](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "View data structure")</span></span>

    <span data-ttu-id="f81a1-151">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="f81a1-151">Click **Register**.</span></span>
9. <span data-ttu-id="f81a1-152">hello 下列螢幕擷取畫面表示 hello 資料已經成功註冊 hello 資料目錄中。</span><span class="sxs-lookup"><span data-stu-id="f81a1-152">hello following screen capture denotes that hello data is successfully registered in hello Data Catalog.</span></span>

    <span data-ttu-id="f81a1-153">![註冊完成](./media/data-lake-store-with-data-catalog/registration-complete.png "檢視資料結構")</span><span class="sxs-lookup"><span data-stu-id="f81a1-153">![Registration complete](./media/data-lake-store-with-data-catalog/registration-complete.png "View data structure")</span></span>
10. <span data-ttu-id="f81a1-154">按一下**檢視入口網站**toogo 回 toohello 資料目錄入口網站，並確認，您現在可以存取 hello 註冊 hello 入口網站的資料。</span><span class="sxs-lookup"><span data-stu-id="f81a1-154">Click **View Portal** toogo back toohello Data Catalog portal and verify that you can now access hello registered data from hello portal.</span></span> <span data-ttu-id="f81a1-155">toosearch hello 資料，您可以使用您註冊 hello 資料時所用的 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="f81a1-155">toosearch hello data, you can use hello tag you used while registering hello data.</span></span>

     <span data-ttu-id="f81a1-156">![搜尋目錄中的資料](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "搜尋目錄中的資料")</span><span class="sxs-lookup"><span data-stu-id="f81a1-156">![Search data in catalog](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Search data in catalog")</span></span>
11. <span data-ttu-id="f81a1-157">您現在可以執行作業，像是新增註釋和文件 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="f81a1-157">You can now perform operations like adding annotations and documentation toohello data.</span></span> <span data-ttu-id="f81a1-158">如需詳細資訊，請參閱下列連結查看 hello。</span><span class="sxs-lookup"><span data-stu-id="f81a1-158">For more information, see hello following links.</span></span>

    * [<span data-ttu-id="f81a1-159">註釋資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="f81a1-159">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
    * [<span data-ttu-id="f81a1-160">記錄資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="f81a1-160">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a><span data-ttu-id="f81a1-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f81a1-161">See also</span></span>
* [<span data-ttu-id="f81a1-162">註釋資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="f81a1-162">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
* [<span data-ttu-id="f81a1-163">記錄資料目錄中的資料來源</span><span class="sxs-lookup"><span data-stu-id="f81a1-163">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)
* [<span data-ttu-id="f81a1-164">整合 Data Lake Store 與其他 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="f81a1-164">Integrate Data Lake Store with other Azure services</span></span>](data-lake-store-integrate-with-other-services.md)
