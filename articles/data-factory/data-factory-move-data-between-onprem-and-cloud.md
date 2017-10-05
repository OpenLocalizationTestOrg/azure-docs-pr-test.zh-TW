---
title: "移動資料 - 資料管理閘道 | Microsoft Docs"
description: "設定資料閘道器以在內部部署與雲端之間移動資料。 使用 Azure Data Factory 中的資料管理閘道器移動資料。"
keywords: "資料閘道器, 資料整合, 移動資料, 閘道認證"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="98867-105">利用資料管理閘道在內部部署來源和雲端之間移動資料</span><span class="sxs-lookup"><span data-stu-id="98867-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="98867-106">本文提供使用 Data Factory 整合內部部署資料存放區與雲端資料存放區資料的概觀。</span><span class="sxs-lookup"><span data-stu-id="98867-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="98867-107">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文和其他 Data Factory 核心概念文章：[資料集](data-factory-create-datasets.md)和[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="98867-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="98867-108">資料管理閘道</span><span class="sxs-lookup"><span data-stu-id="98867-108">Data Management Gateway</span></span>
<span data-ttu-id="98867-109">若要將資料移入/移出內部部署資料存放區，您必須在內部部署機器上安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="98867-110">您可以將閘道安裝在與資料存放區相同或相異的電腦上，只要閘道可以連接資料存放區即可。</span><span class="sxs-lookup"><span data-stu-id="98867-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98867-111">如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="98867-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="98867-112">以下逐步解說將示範如何使用將資料從內部部署 **SQL Server** 資料庫移至 Azure Blob 儲存體的管線來建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="98867-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="98867-113">在逐步解說中，您會在電腦上安裝及設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="98867-114">逐步解說︰將內部部署資料複製到雲端</span><span class="sxs-lookup"><span data-stu-id="98867-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="98867-115">在本逐步解說中，您會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="98867-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="98867-116">建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="98867-116">Create a data factory.</span></span>
2. <span data-ttu-id="98867-117">建立資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="98867-118">為來源和接收的資料存放區建立已連結的服務。</span><span class="sxs-lookup"><span data-stu-id="98867-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="98867-119">建立資料集來代表輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="98867-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="98867-120">建立具有複製活動的管線來移動資料。</span><span class="sxs-lookup"><span data-stu-id="98867-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="98867-121">教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="98867-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="98867-122">開始進行本逐步解說之前，您必須具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="98867-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="98867-123">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="98867-123">**Azure subscription**.</span></span>  <span data-ttu-id="98867-124">如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="98867-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="98867-125">如需詳細資料，請參閱 [免費試用](http://azure.microsoft.com/pricing/free-trial/) 一文。</span><span class="sxs-lookup"><span data-stu-id="98867-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="98867-126">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="98867-126">**Azure Storage Account**.</span></span> <span data-ttu-id="98867-127">在本教學課程中，您會使用 Blob 儲存體作為**目的地/接收**資料存放區。</span><span class="sxs-lookup"><span data-stu-id="98867-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="98867-128">如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account) 一文以取得建立步驟。</span><span class="sxs-lookup"><span data-stu-id="98867-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="98867-129">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="98867-129">**SQL Server**.</span></span> <span data-ttu-id="98867-130">在本教學課程中，您會使用內部部署 SQL 資料庫作為**來源**資料存放區。</span><span class="sxs-lookup"><span data-stu-id="98867-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="98867-131">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="98867-131">Create data factory</span></span>
<span data-ttu-id="98867-132">在此步驟中，您將使用 Azure 入口網站來建立名為 **ADFTutorialOnPremDF**的 Azure Data Factory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="98867-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="98867-133">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="98867-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="98867-134">依序按一下 [+ 新增]、[智慧 + 分析] 及 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="98867-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![新增->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="98867-136">在 [新增 Data Factory] 頁面中，輸入 **ADFTutorialOnPremDF** 作為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="98867-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![新增至儀表板](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="98867-138">Azure Data Factory 的名稱在全域必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="98867-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="98867-139">如果您收到錯誤： **Data Factory 名稱 “ADFTutorialOnPremDF” 無法使用**，請變更 Data Factory 名稱 (例如 yournameADFTutorialOnPremDF)，然後嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="98867-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="98867-140">執行此教學課程中的其餘步驟時，請使用此名稱來取代 ADFTutorialOnPremDF。</span><span class="sxs-lookup"><span data-stu-id="98867-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="98867-141">Data Factory 的名稱未來可能會註冊為 **DNS** 名稱，因此會變成公開可見的名稱。</span><span class="sxs-lookup"><span data-stu-id="98867-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="98867-142">選取您想要建立 Data Factory 的 [Azure 訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="98867-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="98867-143">請選取現有的 **資源群組** ，或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="98867-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="98867-144">在教學課程中，建立名稱如下的資源群組：**ADFTutorialResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="98867-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="98867-145">按一下 [新增 Data Factory] 頁面上的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="98867-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="98867-146">若要建立 Data Factory 執行個體，您必須是訂用帳戶/資源群組層級的 [Data Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 角色成員。</span><span class="sxs-lookup"><span data-stu-id="98867-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="98867-147">建立完成之後，您會看到 [Data Factory] 頁面，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="98867-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Data Factory 首頁](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="98867-149">建立閘道</span><span class="sxs-lookup"><span data-stu-id="98867-149">Create gateway</span></span>
1. <span data-ttu-id="98867-150">在 [Data Factory] 頁面中，按一下 [製作和部署] 圖格來啟動 Data Factory 的 [編輯器]。</span><span class="sxs-lookup"><span data-stu-id="98867-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![[製作和部署] 磚](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="98867-152">在 [Data Factory 編輯器] 中，按一下工具列上的 [...**更多]**，然後按一下 [新增資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="98867-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="98867-153">或者，您也可以在樹狀檢視中，以滑鼠右鍵按一下 [資料閘道]，再按一下 [新增資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="98867-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![工具列上的 [新增資料閘道]](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="98867-155">在 [建立] 頁面上，輸入 **adftutorialgateway** 作為 [名稱]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="98867-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![[建立閘道] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="98867-157">在本逐步解說中，您會建立只具有一個節點的邏輯閘道 (內部部署 Windows 機器)。</span><span class="sxs-lookup"><span data-stu-id="98867-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="98867-158">您可以將多個內部部署機器關聯到閘道以相應放大資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="98867-159">您可以增加可在節點上同時執行的資料移動作業數目來進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="98867-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="98867-160">這項功能也適用於具有單一節點的邏輯閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="98867-161">如需得詳細資料，請參閱[在 Azure Data Factory 中調整資料管理閘道](data-factory-data-management-gateway-high-availability-scalability.md)一文。</span><span class="sxs-lookup"><span data-stu-id="98867-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="98867-162">在 [設定] 頁面中，按一下 [直接安裝在此電腦上]。</span><span class="sxs-lookup"><span data-stu-id="98867-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="98867-163">此動作會下載閘道的安裝套件、在電腦上安裝、設定和註冊閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="98867-164">使用 Internet Explorer 或 Microsoft ClickOnce 相容的 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="98867-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="98867-165">如果您使用 Chrome，請移至 [Chrome 線上應用程式商店](https://chrome.google.com/webstore/)，使用關鍵字 "ClickOnce" 進行搜尋，選擇其中一個 ClickOnce 擴充功能並安裝。</span><span class="sxs-lookup"><span data-stu-id="98867-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="98867-166">針對 Firefox 進行相同的操作 (安裝附加元件)。</span><span class="sxs-lookup"><span data-stu-id="98867-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="98867-167">按一下工具列上的 [開啟功能表] 按鈕 (右上角的**三條水平線**)，按一下 [附加元件]，以「ClickOnce」關鍵字進行搜尋，選擇其中一個 ClickOnce 延伸模組並安裝。</span><span class="sxs-lookup"><span data-stu-id="98867-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![閘道 - [設定] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="98867-169">這是最簡單的方式 (一鍵)，透過單一步驟即可下載、安裝、設定和註冊閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="98867-170">您可以看到 **Microsoft 資料管理閘道組態管理員**應用程式已安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="98867-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="98867-171">您也可以在 **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared** 資料夾中找到執行檔 **ConfigManager.exe**。</span><span class="sxs-lookup"><span data-stu-id="98867-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="98867-172">您也可以使用此頁面中的連結手動下載與安裝閘道器，並使用 [新金鑰]  文字方塊中顯示的金鑰來加以註冊。</span><span class="sxs-lookup"><span data-stu-id="98867-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="98867-173">如需閘道的所有詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="98867-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="98867-174">您必須是本機電腦上的系統管理員，才能成功安裝和設定「資料管理閘道」。</span><span class="sxs-lookup"><span data-stu-id="98867-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="98867-175">您可以將其他使用者加入至 [資料管理閘道使用者]  本機 Windows 群組。</span><span class="sxs-lookup"><span data-stu-id="98867-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="98867-176">此群組的成員可以使用「資料管理閘道組態管理員」工具來設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="98867-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="98867-177">等候幾分鐘，或等候直到您看見下列通知訊息︰</span><span class="sxs-lookup"><span data-stu-id="98867-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![閘道安裝成功](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="98867-179">在電腦上啟動**資料管理閘道組態管理員**應用程式。</span><span class="sxs-lookup"><span data-stu-id="98867-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="98867-180">在 [搜尋] 視窗中，輸入**資料管理閘道**以存取這個公用程式。</span><span class="sxs-lookup"><span data-stu-id="98867-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="98867-181">您也可以在 **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared** 資料夾中找到執行檔 **ConfigManager.exe**</span><span class="sxs-lookup"><span data-stu-id="98867-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![閘道器組態管理員](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="98867-183">確認您有看到 `adftutorialgateway is connected to the cloud service` 訊息。</span><span class="sxs-lookup"><span data-stu-id="98867-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="98867-184">底部的狀態列會顯示 [已連接到雲端服務] 和一個**綠色的核取記號**。</span><span class="sxs-lookup"><span data-stu-id="98867-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="98867-185">在 [首頁] 索引標籤上，您也可以執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="98867-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="98867-186">從 Azure 入口網站中使用 [註冊] 按鈕，以金鑰**註冊**閘道。</span><span class="sxs-lookup"><span data-stu-id="98867-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="98867-187">**停止**在閘道電腦上執行的資料管理閘道主機服務。</span><span class="sxs-lookup"><span data-stu-id="98867-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="98867-188">將更新安裝作業**排程**在一天當中的指定時間。</span><span class="sxs-lookup"><span data-stu-id="98867-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="98867-189">檢視閘道的 **上次更新**時間。</span><span class="sxs-lookup"><span data-stu-id="98867-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="98867-190">指定可以安裝閘道更新的時間。</span><span class="sxs-lookup"><span data-stu-id="98867-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="98867-191">切換到 [設定]  索引標籤。在 [憑證]  區段中指定的憑證，可用來加密/解密在入口網站指定的內部部署資料存放區認證 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="98867-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="98867-192">按一下 [變更]  以改用您自己的憑證。</span><span class="sxs-lookup"><span data-stu-id="98867-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="98867-193">根據預設，閘道器會使用由 Data Factory 服務自動產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="98867-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![閘道器憑證組態](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="98867-195">您也可以在 [設定] 索引標籤上執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="98867-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="98867-196">檢視或匯出閘道所使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="98867-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="98867-197">變更閘道使用的 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="98867-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="98867-198">設定閘道要使用的 HTTP Proxy。</span><span class="sxs-lookup"><span data-stu-id="98867-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="98867-199">(選擇性) 切換到 [診斷] 索引標籤，如果您想啟用詳細資訊記錄功能，以便對閘道的任何問題進行疑難排解，請勾選 [啟用詳細資訊記錄] 選項。</span><span class="sxs-lookup"><span data-stu-id="98867-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="98867-200">在 [應用程式及服務記錄檔]  ->  [資料管理閘道] 節點之下的 [事件檢視器] 中可找到記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="98867-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![[診斷] 索引標籤](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="98867-202">您也可以在 [診斷]  索引標籤上執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="98867-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="98867-203">使用 **測試連線** 一節來對使用閘道器的內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="98867-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="98867-204">按一下 [檢視記錄檔]  以查看 [事件檢視器] 視窗中的資料管理閘道記錄檔。</span><span class="sxs-lookup"><span data-stu-id="98867-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="98867-205">按一下 [傳送記錄檔]  將含有過去七天記錄檔的 zip 檔案上傳到 Microsoft，以幫助針對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="98867-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="98867-206">在 [診斷] 索引標籤的 [測試連接] 區段中，選取 [SqlServer] 做為資料存放區的類型，輸入資料庫伺服器名稱和資料庫名稱，指定驗證類型，輸入使用者名稱和密碼，然後按一下 [測試] 來測試閘道是否可連線到資料庫。</span><span class="sxs-lookup"><span data-stu-id="98867-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="98867-207">切換到網頁瀏覽器，然後在 **Azure 入口網站**中，依序在 [設定] 頁面和 [新增資料閘道] 頁面中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="98867-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="98867-208">左側的樹狀檢視中，[資料閘道] 下方應該會顯示 **adftutorialgateway**。</span><span class="sxs-lookup"><span data-stu-id="98867-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="98867-209">如果按一下，應該會看到相關聯的 JSON。</span><span class="sxs-lookup"><span data-stu-id="98867-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="98867-210">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="98867-210">Create linked services</span></span>
<span data-ttu-id="98867-211">在此步驟中，您會建立兩個連結服務：**AzureStorageLinkedService** 和 **SqlServerLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="98867-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="98867-212">**SqlServerLinkedService** 會連結內部部署 SQL Server 資料庫，而 **AzureStorageLinkedService** 連結服務則會將 Azure Blob 存放區連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="98867-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="98867-213">稍後在本逐步解說中，您會建立可將內部部署 SQL Server 資料庫的資料複製到 Azure Blob 存放區的管線。</span><span class="sxs-lookup"><span data-stu-id="98867-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="98867-214">在內部部署 SQL Server 資料庫中新增連結服務</span><span class="sxs-lookup"><span data-stu-id="98867-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="98867-215">在 [Data Factory 編輯器] 中，按一下工具列上的 [新增資料存放區]，然後選取 [SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="98867-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![新增 SQL Server 連結服務](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="98867-217">在右邊的 [JSON 編輯器] 中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="98867-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="98867-218">將 **gatewayName** 指定為 **adftutorialgateway**。</span><span class="sxs-lookup"><span data-stu-id="98867-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="98867-219">在 [connectionString] 中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="98867-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="98867-220">針對 **servername**，輸入裝載 SQL Server 資料庫的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="98867-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="98867-221">針對 **databasename**，輸入資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="98867-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="98867-222">按一下工具列上的 [加密] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="98867-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="98867-223">您會看到認證管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="98867-223">You see the Credentials Manager application.</span></span>

         ![認證管理員應用程式](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="98867-225">在 [設定認證] 對話方塊中，指定驗證類型、使用者名稱和密碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="98867-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="98867-226">如果連線成功，加密的認證會儲存在 JSON 中，並關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="98867-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="98867-227">請關閉啟動對話方塊的空白瀏覽器索引標籤 (如果未自動關閉)，然後返回具有 Azure 入口網站的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="98867-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="98867-228">在閘道電腦上，這些認證會以 Data Factory 服務所擁有的憑證**加密** 。</span><span class="sxs-lookup"><span data-stu-id="98867-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="98867-229">如果您想要改用與「資料管理閘道」關聯的憑證，請參閱 [安全地設定認證](#set-credentials-and-security)。</span><span class="sxs-lookup"><span data-stu-id="98867-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="98867-230">按一下命令列上的 [部署]  ，部署 SQL Server 連結服務。</span><span class="sxs-lookup"><span data-stu-id="98867-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="98867-231">您應該會在樹狀檢視中看到連結服務。</span><span class="sxs-lookup"><span data-stu-id="98867-231">You should see the linked service in the tree view.</span></span>

      ![樹狀檢視中的 SQL Server 連結服務](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="98867-233">新增 Azure 儲存體帳戶的連結服務</span><span class="sxs-lookup"><span data-stu-id="98867-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="98867-234">在 [Data Factory 編輯器] 中，按一下命令列上的 [新增資料存放區]，然後按一下 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="98867-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="98867-235">在 [帳戶名稱] 中輸入您的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="98867-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="98867-236">在 [帳戶金鑰] 中輸入您的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="98867-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="98867-237">按一下 [部署] 以部署 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="98867-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="98867-238">建立資料集</span><span class="sxs-lookup"><span data-stu-id="98867-238">Create datasets</span></span>
<span data-ttu-id="98867-239">在此步驟中，您會建立代表複製作業的輸入和輸出資料的輸入和輸出資料集 (內部部署 SQL Server 資料庫 => Azure Blob 儲存體)。</span><span class="sxs-lookup"><span data-stu-id="98867-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="98867-240">建立資料集之前，請執行下列步驟 (詳細步驟隨附於清單後)：</span><span class="sxs-lookup"><span data-stu-id="98867-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="98867-241">在您新增為 Data Factory 連結服務的 SQL Server 資料庫中，建立名為 **emp** 的資料表，並在資料表中插入幾個範例項目。</span><span class="sxs-lookup"><span data-stu-id="98867-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="98867-242">在您加入 Data Factory 作為連結服務的 Azure Blob 儲存體帳戶中，建立名為 **adftutorial** 的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="98867-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="98867-243">準備用於教學課程的內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="98867-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="98867-244">在您指定用於內部部署 SQL Server 連結服務 (**SqlServerLinkedService**) 的資料庫中，使用下列 SQL 指令碼在資料庫中建立 **emp** 資料表。</span><span class="sxs-lookup"><span data-stu-id="98867-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="98867-245">在資料表中插入一些範例：</span><span class="sxs-lookup"><span data-stu-id="98867-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="98867-246">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="98867-246">Create input dataset</span></span>

1. <span data-ttu-id="98867-247">在 [Data Factory 編輯器] 中，按一下命令列上的 [...**更多]**、按一下命令列上的 [新增資料集]，然後按一下 [SQL Server 資料表]。</span><span class="sxs-lookup"><span data-stu-id="98867-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="98867-248">使用下列文字取代右窗格中的 JSON：</span><span class="sxs-lookup"><span data-stu-id="98867-248">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="98867-249">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="98867-249">Note the following points:</span></span>

   * <span data-ttu-id="98867-250">**type** 設定為 **SqlServerTable**。</span><span class="sxs-lookup"><span data-stu-id="98867-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="98867-251">**tableName** 設定為 **emp**。</span><span class="sxs-lookup"><span data-stu-id="98867-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="98867-252">**linkedServiceName** 設定為 **OnPremSqlLinkedService** (您稍早已在此逐步解說建立此連結服務)。</span><span class="sxs-lookup"><span data-stu-id="98867-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="98867-253">針對並非由 Azure Data Factory 中另一個管線所產生的輸入資料集，您必須將 **external** 設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="98867-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="98867-254">它代表輸入資料產生於 Azure Data Factory 服務外部。</span><span class="sxs-lookup"><span data-stu-id="98867-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="98867-255">您可以使用 **Policy** 區段中的 **externalData** 元素，選擇性地指定任何外部資料原則。</span><span class="sxs-lookup"><span data-stu-id="98867-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="98867-256">如需 JSON 屬性的詳細資訊，請參閱[在 SQL Server 來回移動資料](data-factory-sqlserver-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="98867-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="98867-257">按一下命令列上的 [部署]  來部署資料集。</span><span class="sxs-lookup"><span data-stu-id="98867-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="98867-258">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="98867-258">Create output dataset</span></span>

1. <span data-ttu-id="98867-259">在 [Data Factory 編輯器] 中，按一下命令列的 [新增資料集]，然後按一下 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="98867-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="98867-260">使用下列文字取代右窗格中的 JSON：</span><span class="sxs-lookup"><span data-stu-id="98867-260">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="98867-261">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="98867-261">Note the following points:</span></span>

   * <span data-ttu-id="98867-262">**type** 設定為 **AzureBlob**。</span><span class="sxs-lookup"><span data-stu-id="98867-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="98867-263">**linkedServiceName** 設定為 **AzureStorageLinkedService** (您已在步驟 2 中建立此連結服務)。</span><span class="sxs-lookup"><span data-stu-id="98867-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="98867-264">**folderPath** 設定為 **adftutorial/outfromonpremdf**，其中 outfromonpremdf 是 adftutorial 容器中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="98867-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="98867-265">建立 **adftutorial** 容器 (如果尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="98867-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="98867-266">**availability** 設定為**每小時** (**frequency** 設為 **hour**，**interval** 設為 **1**)。</span><span class="sxs-lookup"><span data-stu-id="98867-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="98867-267">Data Factory 服務會每隔一小時在 Azure SQL Database 的 **emp** 資料表中產生輸出資料配量。</span><span class="sxs-lookup"><span data-stu-id="98867-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="98867-268">如果您沒有指定**輸出資料表**的 **fileName**，**folderPath** 中產生的檔案會依照下列格式命名：Data<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)。</span><span class="sxs-lookup"><span data-stu-id="98867-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="98867-269">若要根據 **SliceStart** 時間動態設定 **folderPath** 和 **fileName**，請使用 partitionedBy 屬性。</span><span class="sxs-lookup"><span data-stu-id="98867-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="98867-270">在下列範例中，folderPath 使用 SliceStart (所處理配量的開始時間) 中的年、月和日，fileName 使用 SliceStart 中的小時。</span><span class="sxs-lookup"><span data-stu-id="98867-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="98867-271">例如，如果配量產生於 2014-10-20T08:00:00，folderName 設定為 wikidatagateway/wikisampledataout/2014/10/20，而 fileName 設定為 08.csv。</span><span class="sxs-lookup"><span data-stu-id="98867-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="98867-272">如需 JSON 屬性的詳細資訊，請參閱[在 Azure Blob 儲存體來回移動資料](data-factory-azure-blob-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="98867-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="98867-273">按一下命令列上的 [部署]  來部署資料集。</span><span class="sxs-lookup"><span data-stu-id="98867-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="98867-274">確認您已在樹狀檢視中看到這兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="98867-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="98867-275">建立管線</span><span class="sxs-lookup"><span data-stu-id="98867-275">Create pipeline</span></span>
<span data-ttu-id="98867-276">在此步驟中，您會建立一個**管線**，其中包含一個使用 **EmpOnPremSQLTable** 做為輸入和 **OutputBlobTable** 做為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="98867-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="98867-277">在 [Data Factory 編輯器] 中，按一下 **[...更多]** 和 [新增管線]。</span><span class="sxs-lookup"><span data-stu-id="98867-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="98867-278">使用下列文字取代右窗格中的 JSON：</span><span class="sxs-lookup"><span data-stu-id="98867-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="98867-279">將 **start** 屬性的值取代為目前日期，並將 **end** 值取代為隔天的日期。</span><span class="sxs-lookup"><span data-stu-id="98867-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="98867-280">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="98867-280">Note the following points:</span></span>

   * <span data-ttu-id="98867-281">在 activities 區段中，只會有 **type** 設定為 **Copy** 的活動。</span><span class="sxs-lookup"><span data-stu-id="98867-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="98867-282">活動的**輸入**設定為 **EmpOnPremSQLTable**，活動的**輸出**則設定為 **OutputBlobTable**。</span><span class="sxs-lookup"><span data-stu-id="98867-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="98867-283">在 **typeProperties** 區段中，**來源類型**指定為 **SqlSource**，**接收類型**指定為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="98867-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="98867-284">**SqlSource** 的 **sqlReaderQuery** 屬性指定為 SQL 查詢 `select * from emp`。</span><span class="sxs-lookup"><span data-stu-id="98867-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="98867-285">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="98867-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="98867-286">例如：2014-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="98867-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="98867-287">**end** 時間為選擇性項目，但在本教學課程中會用到。</span><span class="sxs-lookup"><span data-stu-id="98867-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="98867-288">如果您未指定 **end** 屬性的值，則會以「**start + 48 小時**」計算。</span><span class="sxs-lookup"><span data-stu-id="98867-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="98867-289">若要無限期地執行管線，請指定 **9/9/9999** 做為 **end** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="98867-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="98867-290">您定義會根據為每個 Azure Data Factory 資料集定義的 **Availability** 屬性來處理資料配量的持續時間。</span><span class="sxs-lookup"><span data-stu-id="98867-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="98867-291">在此範例中，由於每小時即產生一個資料配量，共會有 24 個資料配量。</span><span class="sxs-lookup"><span data-stu-id="98867-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="98867-292">按一下命令列的 [部署]  ，以部署資料集 (資料表是矩形的資料集)。</span><span class="sxs-lookup"><span data-stu-id="98867-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="98867-293">確認管線顯示在樹狀檢視的**管線**節點底下。</span><span class="sxs-lookup"><span data-stu-id="98867-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="98867-294">現在，按兩下 [X] 關閉頁面，以回到 **ADFTutorialOnPremDF** 的 [Data Factory] 頁面。</span><span class="sxs-lookup"><span data-stu-id="98867-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="98867-295">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="98867-295">**Congratulations!**</span></span> <span data-ttu-id="98867-296">您已成功建立 Azure Data Factory、連結服務、資料集和管線，以及排定的管線。</span><span class="sxs-lookup"><span data-stu-id="98867-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="98867-297">在圖表檢視中檢視 Data Factory</span><span class="sxs-lookup"><span data-stu-id="98867-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="98867-298">在 **Azure 入口網站**中，按一下 [ADFTutorialOnPremDF] Data Factory 首頁上的 [圖表] 圖格。</span><span class="sxs-lookup"><span data-stu-id="98867-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="98867-299">：</span><span class="sxs-lookup"><span data-stu-id="98867-299">:</span></span>

    ![圖表連結](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="98867-301">您應該會看到如下圖所示的圖表：</span><span class="sxs-lookup"><span data-stu-id="98867-301">You should see the diagram similar to the following image:</span></span>

    ![圖表檢視](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="98867-303">您可以將管線和資料集放大、縮小、放大到 100%、縮放至適當比例和自動定位，以及顯示歷程資訊 (反白顯示所選取項目的上游和下游項目)。</span><span class="sxs-lookup"><span data-stu-id="98867-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="98867-304">您可以按兩下物件 (輸入/輸出資料集或管線) 查看其屬性。</span><span class="sxs-lookup"><span data-stu-id="98867-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="98867-305">監視管線</span><span class="sxs-lookup"><span data-stu-id="98867-305">Monitor pipeline</span></span>
<span data-ttu-id="98867-306">在此步驟中，您會使用 Azure 入口網站來監視 Azure Data Factory 的運作情形。</span><span class="sxs-lookup"><span data-stu-id="98867-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="98867-307">您也可以使用 PowerShell Cmdlet 來監視資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="98867-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="98867-308">如需監視的詳細資料，請參閱 [監視和管理管線](data-factory-monitor-manage-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="98867-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="98867-309">在圖中按兩下 **EmpOnPremSQLTable**。</span><span class="sxs-lookup"><span data-stu-id="98867-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable 配量](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="98867-311">請注意，上面的所有資料配量都是**就緒**狀態，因為管線持續期間 (開始時間到結束時間) 是過去的時間。</span><span class="sxs-lookup"><span data-stu-id="98867-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="98867-312">這也是因為您已將資料插入 SQL Server 資料庫中，而資料一直留存於其中。</span><span class="sxs-lookup"><span data-stu-id="98867-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="98867-313">確認下方的 [問題配量]  區段中沒有顯示任何配量。</span><span class="sxs-lookup"><span data-stu-id="98867-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="98867-314">若要檢視所有配量，請按一下配量清單底部的 [更多資訊]。</span><span class="sxs-lookup"><span data-stu-id="98867-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="98867-315">現在，在 [資料集] 頁面中，按一下 [OutputBlobTable]。</span><span class="sxs-lookup"><span data-stu-id="98867-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable 配量](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="98867-317">按一下清單中的任何資料配量，您應該會看到 [資料配量] 頁面。</span><span class="sxs-lookup"><span data-stu-id="98867-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="98867-318">您會看到該配量的活動執行。</span><span class="sxs-lookup"><span data-stu-id="98867-318">You see activity runs for the slice.</span></span> <span data-ttu-id="98867-319">您通常只會看到一個活動執行。</span><span class="sxs-lookup"><span data-stu-id="98867-319">You see only one activity run usually.</span></span>  

    ![資料配量刀鋒視窗](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="98867-321">若配量不是處於 [就緒] 狀態，您可以在 [未就緒的上游配量] 清單中看到未就緒且阻礙目前配量執行的上游配量。</span><span class="sxs-lookup"><span data-stu-id="98867-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="98867-322">按一下底部清單中的 [活動執行]，可查看 [活動執行詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="98867-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![[活動執行詳細資料] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="98867-324">您會看到輸送量、持續時間和用來傳輸資料的閘道等資訊。</span><span class="sxs-lookup"><span data-stu-id="98867-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="98867-325">按一下 [X] 關閉所有頁面，直到您</span><span class="sxs-lookup"><span data-stu-id="98867-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="98867-326">回到 **ADFTutorialOnPremDF** 的首頁為止。</span><span class="sxs-lookup"><span data-stu-id="98867-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="98867-327">(選擇性) 依序按一下 [管線] 及 [ADFTutorialOnPremDF]，然後深入檢視輸入資料表 (**已使用**) 或輸出資料集 (**已產生**)。</span><span class="sxs-lookup"><span data-stu-id="98867-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="98867-328">使用 [Microsoft 儲存體總管](http://storageexplorer.com/)等工具來確認每個小時會建立一個 Blob/檔案。</span><span class="sxs-lookup"><span data-stu-id="98867-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Azure 儲存體總管](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="98867-330">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98867-330">Next steps</span></span>
* <span data-ttu-id="98867-331">如需資料管理閘道的所有詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="98867-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="98867-332">若要了解如何使用複製活動將資料從來源資料存放區移動到接收資料存放區，請參閱 [從 Azure Blob 複製資料到 Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 。</span><span class="sxs-lookup"><span data-stu-id="98867-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
