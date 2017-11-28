---
title: "aaaMove 資料-資料管理閘道器 |Microsoft 文件"
description: "設定內部部署與 hello 之間的資料閘道 toomove 資料雲端。 使用資料管理閘道器在 Azure Data Factory toomove 您的資料。"
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
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="a0dc3-105">在內部部署來源和資料管理閘道與 hello 雲端之間移動資料</span><span class="sxs-lookup"><span data-stu-id="a0dc3-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="a0dc3-106">本文提供使用 Data Factory 整合內部部署資料存放區與雲端資料存放區資料的概觀。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="a0dc3-107">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件和其他資料處理站核心概念文件：[資料集](data-factory-create-datasets.md)和[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="a0dc3-108">資料管理閘道</span><span class="sxs-lookup"><span data-stu-id="a0dc3-108">Data Management Gateway</span></span>
<span data-ttu-id="a0dc3-109">您必須將資料從內部部署資料存放區移動您在內部部署機器 tooenable 上安裝資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="a0dc3-110">hello 閘道可以安裝在相同電腦做為 hello 資料存放區或不同電腦上，只要 hello 閘道可以連接 toohello 資料存放區的 hello。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0dc3-111">如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="a0dc3-112">hello 下列逐步解說將示範如何 toocreate data factory 管線，將資料從內部部署移**SQL Server**資料庫 tooan Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="a0dc3-113">Hello 逐步解說中，您可以安裝並設定 hello 資料管理閘道器電腦上。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="a0dc3-114">逐步解說： 將複製內部部署資料 toocloud</span><span class="sxs-lookup"><span data-stu-id="a0dc3-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="a0dc3-115">在此逐步解說中您不要 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="a0dc3-116">建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-116">Create a data factory.</span></span>
2. <span data-ttu-id="a0dc3-117">建立資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="a0dc3-118">為來源和接收的資料存放區建立已連結的服務。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="a0dc3-119">建立資料集 toorepresent 輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="a0dc3-120">複製活動 toomove hello 資料以建立管線。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="a0dc3-121">Hello 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="a0dc3-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="a0dc3-122">開始本逐步解說之前，您必須具備下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="a0dc3-123">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-123">**Azure subscription**.</span></span>  <span data-ttu-id="a0dc3-124">如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a0dc3-125">請參閱 hello[免費試用版](http://azure.microsoft.com/pricing/free-trial/)文件以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="a0dc3-126">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-126">**Azure Storage Account**.</span></span> <span data-ttu-id="a0dc3-127">您使用做為 hello blob 儲存體**目的地/接收器**資料儲存在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="a0dc3-128">如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)步驟 toocreate 其中一個發行項。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="a0dc3-129">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-129">**SQL Server**.</span></span> <span data-ttu-id="a0dc3-130">在本教學課程中，您會使用內部部署 SQL 資料庫作為**來源**資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="a0dc3-131">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="a0dc3-131">Create data factory</span></span>
<span data-ttu-id="a0dc3-132">在此步驟中，您可以使用 hello Azure Data Factory 執行個體名為的 Azure 入口網站 toocreate **ADFTutorialOnPremDF**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="a0dc3-133">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a0dc3-134">依序按一下 [+ 新增]、[智慧 + 分析] 及 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![新增->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="a0dc3-136">在 hello**新的 data factory**頁面上，輸入**ADFTutorialOnPremDF** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![新增 tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="a0dc3-138">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="a0dc3-139">如果您收到 hello 錯誤： **Data factory 名稱"ADFTutorialOnPremDF"不是使用**、 變更 hello hello data factory (例如，yournameADFTutorialOnPremDF) 名稱，然後再次嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="a0dc3-140">執行此教學課程中的其餘步驟時，請使用此名稱來取代 ADFTutorialOnPremDF。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="a0dc3-141">hello hello data factory 名稱可能會註冊為**DNS** hello 未來中的名稱，因此公開可見。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="a0dc3-142">選取 hello **Azure 訂用帳戶**您想要建立 hello 資料 factory toobe。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="a0dc3-143">請選取現有的 **資源群組** ，或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="a0dc3-144">Hello 教學課程中，建立名為的資源群組： **ADFTutorialResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="a0dc3-145">按一下**建立**上 hello**新的 data factory**頁面。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a0dc3-146">toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="a0dc3-147">建立完成之後，您會看到 hello **Data Factory**頁面 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Data Factory 首頁](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="a0dc3-149">建立閘道</span><span class="sxs-lookup"><span data-stu-id="a0dc3-149">Create gateway</span></span>
1. <span data-ttu-id="a0dc3-150">在 hello **Data Factory**頁面上，按一下**作者及部署**磚 toolaunch hello**編輯器**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![[製作和部署] 磚](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="a0dc3-152">在 hello Data Factory 編輯器中，按一下  **...多個**在 hello 工具列，然後按一下**新的資料閘道**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="a0dc3-153">或者，您可以以滑鼠右鍵按一下**資料閘道**在 hello 樹狀檢視中，然後按一下**新的資料閘道**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![工具列上的 [新增資料閘道]](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="a0dc3-155">在 hello**建立**頁面上，輸入**adftutorialgateway** hello**名稱**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![[建立閘道] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="a0dc3-157">本逐步解說中，您可以建立 hello 邏輯閘道與只有一個節點 （在內部部署 Windows 電腦）。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="a0dc3-158">您可以向外延展資料管理閘道將多部在內部部署電腦與 hello 閘道產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="a0dc3-159">您可以增加可在節點上同時執行的資料移動作業數目來進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="a0dc3-160">這項功能也適用於具有單一節點的邏輯閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="a0dc3-161">如需得詳細資料，請參閱[在 Azure Data Factory 中調整資料管理閘道](data-factory-data-management-gateway-high-availability-scalability.md)一文。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="a0dc3-162">在 hello**設定**頁面上，按一下**直接在這部電腦上安裝**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="a0dc3-163">這個動作 hello hello 閘道的安裝套件下載、 安裝、 設定和註冊 hello hello 電腦上的閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="a0dc3-164">使用 Internet Explorer 或 Microsoft ClickOnce 相容的 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="a0dc3-165">如果您使用 Chrome，請移至 toohello [Chrome web store](https://chrome.google.com/webstore/)、 搜尋與"ClickOnce"關鍵字、 選擇其中一個 hello ClickOnce 擴充功能，及安裝它。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="a0dc3-166">請勿 hello 相同 Firefox （安裝增益集）。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="a0dc3-167">按一下**開啟功能表**hello 工具列上的按鈕 (**三條水平線**hello 右上角)，按一下 **附加元件**、 搜尋與"ClickOnce"關鍵字，選擇其中一個 helloClickOnce 擴充功能，並安裝它。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![閘道 - [設定] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="a0dc3-169">這種方式是最簡單的方式 （一種單鍵） toodownload hello、 安裝、 設定及登錄一個單一步驟中的 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="a0dc3-170">您可以看到 hello **Microsoft 資料管理閘道組態管理員**應用程式安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="a0dc3-171">您也可以尋找 hello 可執行檔**ConfigManager.exe** hello 資料夾中： **C:\Program Files\Microsoft 資料管理 Gateway\2.0\Shared**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="a0dc3-172">您可以同時下載和使用此頁面中的 hello 連結，以手動方式安裝閘道及顯示 hello 中的 hello 金鑰進行註冊**新金鑰**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="a0dc3-173">請參閱[資料管理閘道器](data-factory-data-management-gateway.md)發行項的所有 hello hello 閘道的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0dc3-174">您必須是 hello 本機電腦 tooinstall 的系統管理員，並已成功設定 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="a0dc3-175">您可以加入其他使用者 toohello**資料管理閘道使用者**本機 Windows 群組。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="a0dc3-176">hello 這個群組的成員可以使用 hello 資料管理閘道組態管理員工具 tooconfigure hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="a0dc3-177">等候數分鐘，或等候直至您看見 hello 下通知訊息：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![閘道安裝成功](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="a0dc3-179">在電腦上啟動**資料管理閘道組態管理員**應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="a0dc3-180">在 hello**搜尋**視窗中，輸入**資料管理閘道器**tooaccess 此公用程式。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="a0dc3-181">您也可以尋找 hello 可執行檔**ConfigManager.exe** hello 資料夾中： **C:\Program Files\Microsoft 資料管理 Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="a0dc3-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![閘道器組態管理員](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="a0dc3-183">確認您有看到 `adftutorialgateway is connected toohello cloud service` 訊息。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="a0dc3-184">hello hello 底部顯示狀態列**連接 toohello 雲端服務**連同**綠色核取記號**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="a0dc3-185">在 hello**首頁**索引標籤上，您也可以執行下列作業 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="a0dc3-186">**註冊**具有索引鍵從 hello 使用 hello 註冊按鈕的 Azure 入口網站的閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="a0dc3-187">**停止**hello 閘道機器上執行的資料管理閘道主機服務。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="a0dc3-188">**更新排程**toobe hello 一天的特定時間安裝。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="a0dc3-189">檢視何時 hello 閘道**上次更新**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="a0dc3-190">指定可以在安裝更新 toohello 閘道的時間。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="a0dc3-191">切換 toohello**設定**hello 中所指定的索引 hello 憑證**憑證**區段是 hello 在內部部署資料存放區，您指定 hello 入口網站上的使用的 tooencrypt/解密憑證。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="a0dc3-192">（選擇性）按一下**變更**toouse 您自己的憑證而。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="a0dc3-193">根據預設，hello 閘道會使用 hello 憑證由 hello Data Factory 服務自動產生。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![閘道器憑證組態](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="a0dc3-195">您也可以執行下列動作上 hello hello**設定** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="a0dc3-196">檢視或匯出 hello hello 閘道使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="a0dc3-197">變更 hello hello 閘道使用的 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="a0dc3-198">設定 hello 閘道使用的 HTTP proxy toobe。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="a0dc3-199">（選擇性）切換 toohello**診斷**索引標籤上，檢查 hello**啟用詳細資訊記錄**選項，如果您想 tooenable 詳細資訊記錄，您可以搭配 tootroubleshoot 任何問題 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="a0dc3-200">hello 記錄資訊位於**事件檢視器**下**Applications and Services Logs** -> **資料管理閘道器**節點。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![[診斷] 索引標籤](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="a0dc3-202">您也可以執行下列動作，在 hello hello**診斷** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="a0dc3-203">使用**測試連接**區段 tooan 在內部部署資料來源使用 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="a0dc3-204">按一下**檢視記錄檔**toosee hello 資料管理閘道會記錄在事件檢視器 視窗中。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="a0dc3-205">按一下**傳送記錄檔**tooupload zip 檔案的最後七天 tooMicrosoft toofacilitate 問題的疑難排解您的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="a0dc3-206">在 hello**診斷**索引標籤上，在 hello**測試連接**區段中，選取**SqlServer** hello 類型 hello 資料存放區中，輸入 hello hello 資料庫伺服器的名稱，名稱hello 資料庫，指定驗證類型，輸入使用者名稱和密碼，然後按一下**測試**tootest hello 閘道是否可連接 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="a0dc3-207">交換器 toohello 網頁瀏覽器，在 hello **Azure 入口網站**，按一下  **確定**上 hello**設定**頁面，然後在 hello**新的資料閘道**頁面。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="a0dc3-208">您應該會看到**adftutorialgateway**下**資料閘道**hello hello 左側的樹狀檢視中。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="a0dc3-209">如果您按一下它，您應該會看到 hello 相關聯的 JSON。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="a0dc3-210">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="a0dc3-210">Create linked services</span></span>
<span data-ttu-id="a0dc3-211">在此步驟中，您會建立兩個連結服務：**AzureStorageLinkedService** 和 **SqlServerLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="a0dc3-212">hello **SqlServerLinkedService**連結在內部部署 SQL Server 資料庫和 hello **AzureStorageLinkedService**連結的服務連結的 Azure blob 存放區 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="a0dc3-213">您稍後在 hello 在內部部署 SQL Server 資料庫 toohello Azure blob 存放區中的資料複製本逐步解說中建立管線。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="a0dc3-214">加入連結的服務 tooan 在內部部署 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="a0dc3-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="a0dc3-215">在 hello **Data Factory 編輯器**，按一下 **新建資料存放區**hello 工具列，然後選取**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![新增 SQL Server 連結服務](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="a0dc3-217">在 hello **JSON 編輯器**上 hello 右，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="a0dc3-218">Hello **gatewayName**，指定**adftutorialgateway**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="a0dc3-219">在 hello **connectionString**，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="a0dc3-220">如**servername**，輸入裝載 hello SQL Server 資料庫的 hello 伺服器 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="a0dc3-221">如**databasename**，輸入 hello hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="a0dc3-222">按一下**加密**hello 工具列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="a0dc3-223">您會看見 hello 認證管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-223">You see hello Credentials Manager application.</span></span>

         ![認證管理員應用程式](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="a0dc3-225">在 hello**設定認證**對話方塊中，指定驗證類型、 使用者名稱和密碼，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="a0dc3-226">Hello 連線成功時，如果 hello 加密認證儲存在 hello JSON 和 hello 對話框會關閉。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="a0dc3-227">關閉 hello 空的瀏覽器索引標籤啟動 hello 對話方塊中，如果它不會自動關閉並取回 toohello 索引標籤以 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="a0dc3-228">這些認證會在 hello 閘道機器上，**加密**服務擁有使用 hello Data Factory 的認證。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="a0dc3-229">如果您想改為與 hello 資料管理閘道器相關聯的 toouse hello 憑證，請參閱[安全地設定認證](#set-credentials-and-security)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="a0dc3-230">按一下**部署**hello 命令列 toodeploy hello 連結的 SQL Server 服務。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="a0dc3-231">您應該會看到 hello 樹狀檢視中的 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-231">You should see hello linked service in hello tree view.</span></span>

      ![Hello 樹狀檢視中的 SQL Server 連結服務](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="a0dc3-233">新增 Azure 儲存體帳戶的連結服務</span><span class="sxs-lookup"><span data-stu-id="a0dc3-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="a0dc3-234">在 hello **Data Factory 編輯器**，按一下 **新建資料存放區**在 hello 命令列，然後按一下**Azure 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="a0dc3-235">輸入您的 Azure 儲存體帳戶 hello hello 名稱**帳戶名稱**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="a0dc3-236">輸入您的 Azure 儲存體帳戶的 hello 金鑰 hello**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="a0dc3-237">按一下**部署**toodeploy hello **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="a0dc3-238">建立資料集</span><span class="sxs-lookup"><span data-stu-id="a0dc3-238">Create datasets</span></span>
<span data-ttu-id="a0dc3-239">在此步驟中，您需要建立輸入和輸出資料集代表 hello 複製作業的輸入和輸出資料 (在內部部署 SQL Server 資料庫 = > Azure blob 儲存體)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="a0dc3-240">然後再建立資料集，請勿 hello （hello 清單之後的詳細的步驟） 的步驟：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="a0dc3-241">建立了名為**emp**在 hello 您加入成為連結的服務 toohello data factory 的 SQL Server 資料庫，並插入幾個範例到 hello 資料表的項目。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="a0dc3-242">建立名為的 blob 容器**adftutorial**在 hello Azure blob 儲存體帳戶，您加入成為連結的服務 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="a0dc3-243">在內部部署 SQL Server 準備 hello 教學課程</span><span class="sxs-lookup"><span data-stu-id="a0dc3-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="a0dc3-244">您所指定的 hello 內部部署 SQL Server 的 hello 資料庫中已連結的服務 (**SqlServerLinkedService**)，使用下列 SQL 指令碼 toocreate hello hello **emp** hello 資料庫資料表中的。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

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
2. <span data-ttu-id="a0dc3-245">Hello 資料表中插入一些範例：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="a0dc3-246">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="a0dc3-246">Create input dataset</span></span>

1. <span data-ttu-id="a0dc3-247">在 hello **Data Factory 編輯器**，按一下  **...多個**，按一下 **新的資料集**hello 命令列，以及按一下**SQL Server 資料表**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="a0dc3-248">Hello 右窗格中的 hello JSON 替換成下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-248">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="a0dc3-249">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-249">Note hello following points:</span></span>

   * <span data-ttu-id="a0dc3-250">**型別**設定得**SqlServerTable**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="a0dc3-251">**tableName**設定得**emp**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="a0dc3-252">**linkedServiceName**設定得**SqlServerLinkedService** （您必須建立此連結的服務稍早在本逐步解說中）。。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="a0dc3-253">對於不由 Azure Data Factory 中的另一個管線產生輸入資料集，您必須設定**外部**太**true**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="a0dc3-254">它代表 hello 輸入的資料而產生外部 toohello Azure Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="a0dc3-255">您可以選擇性地指定外部資料原則使用 hello **externalData** hello 中的項目**原則**> 一節。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="a0dc3-256">如需 JSON 屬性的詳細資訊，請參閱[在 SQL Server 來回移動資料](data-factory-sqlserver-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="a0dc3-257">按一下**部署**hello 命令列 toodeploy hello 資料集上。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="a0dc3-258">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="a0dc3-258">Create output dataset</span></span>

1. <span data-ttu-id="a0dc3-259">在 hello **Data Factory 編輯器**，按一下 **新的資料集**在 hello 命令列，然後按一下**Azure Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="a0dc3-260">Hello 右窗格中的 hello JSON 替換成下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-260">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="a0dc3-261">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-261">Note hello following points:</span></span>

   * <span data-ttu-id="a0dc3-262">**型別**設定得**AzureBlob**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="a0dc3-263">**linkedServiceName**設定得**AzureStorageLinkedService** （您已在步驟 2 中建立這項連結的服務）。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="a0dc3-264">**folderPath**設定得**adftutorial/outfromonpremdf** outfromonpremdf 所在 hello adftutorial 容器中的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="a0dc3-265">建立 hello **adftutorial**容器不存在時。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="a0dc3-266">hello**可用性**設定得**每小時**(**頻率**設定得**小時**和**間隔**太設定**1**)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="a0dc3-267">hello Data Factory 服務會產生輸出的資料配量每小時 hello **emp** hello Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="a0dc3-268">如果您未指定**fileName**如**輸出資料表**，hello 中的 hello 產生檔案**folderPath** hello 下列格式命名： 資料。<Guid>。txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt。)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="a0dc3-269">tooset **folderPath**和**fileName**動態根據 hello **SliceStart**時間，請使用 hello partitionedBy 屬性。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="a0dc3-270">在下列範例的 hello，folderPath 使用年、 月和日 hello SliceStart （hello 正在處理的配量的開始時間） 並檔名使用來自 hello SliceStart 的小時。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="a0dc3-271">例如，如果正在產生配量 2014-10-20T08:00:00，hello folderName 設定 toowikidatagateway/wikisampledataout/2014年/10/20 而且 hello fileName 設定 too08.csv。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

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

    <span data-ttu-id="a0dc3-272">如需 JSON 屬性的詳細資訊，請參閱[在 Azure Blob 儲存體來回移動資料](data-factory-azure-blob-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="a0dc3-273">按一下**部署**hello 命令列 toodeploy hello 資料集上。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="a0dc3-274">確認您看到兩個 hello 樹狀檢視中的 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="a0dc3-275">建立管線</span><span class="sxs-lookup"><span data-stu-id="a0dc3-275">Create pipeline</span></span>
<span data-ttu-id="a0dc3-276">在此步驟中，您會建立一個**管線**，其中包含一個使用 **EmpOnPremSQLTable** 做為輸入和 **OutputBlobTable** 做為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="a0dc3-277">在 [Data Factory 編輯器] 中，按一下 **[...更多]** 和 [新增管線]。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="a0dc3-278">Hello 右窗格中的 hello JSON 替換成下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
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
   > <span data-ttu-id="a0dc3-279">取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="a0dc3-280">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-280">Note hello following points:</span></span>

   * <span data-ttu-id="a0dc3-281">在 [hello 活動] 區段中，沒有只有活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="a0dc3-282">**輸入**hello 活動設定太**EmpOnPremSQLTable**和**輸出**hello 活動設定太**OutputBlobTable**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="a0dc3-283">在 [hello **typeProperties** ] 區段中， **SqlSource**指定為 hello**來源類型**和 * * BlobSink * * 指定為 hello**接收器類型**.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="a0dc3-284">SQL 查詢`select * from emp`指定 hello **sqlReaderQuery**屬性**SqlSource**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="a0dc3-285">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="a0dc3-286">例如：2014-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="a0dc3-287">hello**結束**時間是選擇性的但我們在本教學課程中使用它。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="a0dc3-288">如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="a0dc3-289">無限期地指定 toorun hello 管線**9/9/9999**為 hello hello 值**結束**屬性。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="a0dc3-290">您正在定義 hello 的持續時間中的 hello 處理資料配量會根據 hello**可用性**已針對每個 Azure Data Factory 資料集定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="a0dc3-291">在 hello 範例中，有 24 資料配量每個資料配量會每小時產生。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="a0dc3-292">按一下**部署**hello 命令列 toodeploy hello 資料集 （資料表是矩形的資料集）。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="a0dc3-293">確認 [hello] 下的樹狀結構檢視中顯示該 hello 管線**管線**節點。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="a0dc3-294">現在，按一下  **X**兩次 tooclose hello 頁面 tooget 後 toohello **Data Factory**頁面 hello **ADFTutorialOnPremDF**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="a0dc3-295">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="a0dc3-295">**Congratulations!**</span></span> <span data-ttu-id="a0dc3-296">您已成功建立 Azure data factory、 連結的服務、 資料集和管線和排程的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="a0dc3-297">在圖表檢視中檢視 hello 資料 factory</span><span class="sxs-lookup"><span data-stu-id="a0dc3-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="a0dc3-298">在 hello **Azure 入口網站**，按一下 **圖表**hello hello 首頁上並排顯示**ADFTutorialOnPremDF**資料 factory。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="a0dc3-299">：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-299">:</span></span>

    ![圖表連結](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="a0dc3-301">您應該會看到 hello 圖表類似 toohello 下列映像：</span><span class="sxs-lookup"><span data-stu-id="a0dc3-301">You should see hello diagram similar toohello following image:</span></span>

    ![圖表檢視](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="a0dc3-303">您可以放大、 縮小，縮放 too100%、 縮放 toofit、 自動位置的管線和資料集，並顯示歷程資訊 （反白顯示選取項目的上游及下游項目）。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="a0dc3-304">您可以為其按兩下物件 （輸入/輸出資料集或管線） toosee 屬性。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="a0dc3-305">監視管線</span><span class="sxs-lookup"><span data-stu-id="a0dc3-305">Monitor pipeline</span></span>
<span data-ttu-id="a0dc3-306">在此步驟中，您可以使用 hello Azure 入口網站的 toomonitor Azure data factory 中運作。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="a0dc3-307">您也可以使用 PowerShell cmdlet toomonitor 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="a0dc3-308">如需監視的詳細資料，請參閱 [監視和管理管線](data-factory-monitor-manage-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="a0dc3-309">在 hello 圖表中，按兩下**EmpOnPremSQLTable**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable 配量](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="a0dc3-311">請注意，所有的 hello 資料配量上位於**準備**hello 過去在 hello 管線持續時間 （開始時間 tooend 時間），所以狀態。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="a0dc3-312">它也是因為您已插入 hello SQL Server 資料庫中的 hello 資料就會有所有 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="a0dc3-313">確認任何扇區顯示在 hello**問題配量**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="a0dc3-314">所有 hello 配量中，都按一下 tooview**查看更多**hello hello 清單底端的配量。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="a0dc3-315">現在，在 hello**資料集**頁面上，按一下**OutputBlobTable**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable 配量](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="a0dc3-317">按一下 從 hello 清單的任何資料分割，您應該會看見 hello**資料配量**頁面。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="a0dc3-318">您會看到活動已執行 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="a0dc3-319">您通常只會看到一個活動執行。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-319">You see only one activity run usually.</span></span>  

    ![資料配量刀鋒視窗](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="a0dc3-321">如果 hello 配量不在 hello**準備**狀態，您可以看到未就緒，並封鎖 hello hello 中執行的目前配量的 hello 上游配量**未就緒的上游配量**清單。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="a0dc3-322">按一下 hello**活動執行**從 hello 清單在 hello 底部 toosee**活動執行詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![[活動執行詳細資料] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="a0dc3-324">您會看到資訊，例如輸送量、 期間與 hello 閘道使用 tootransfer hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="a0dc3-325">按一下**X** tooclose 所有 hello 直到您的頁面</span><span class="sxs-lookup"><span data-stu-id="a0dc3-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="a0dc3-326">hello 取回 toohello 首頁**ADFTutorialOnPremDF**。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="a0dc3-327">(選擇性) 依序按一下 [管線] 及 [ADFTutorialOnPremDF]，然後深入檢視輸入資料表 (**已使用**) 或輸出資料集 (**已產生**)。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="a0dc3-328">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)tooverify blob/檔案建立的每個小時。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Azure 儲存體總管](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="a0dc3-330">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0dc3-330">Next steps</span></span>
* <span data-ttu-id="a0dc3-331">請參閱[資料管理閘道器](data-factory-data-management-gateway.md)發行項的所有 hello hello 資料管理閘道器的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="a0dc3-332">請參閱[資料複製到 Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn 有關 toouse 複製活動 toomove 資料從來源資料如何儲存 tooa 接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a0dc3-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
