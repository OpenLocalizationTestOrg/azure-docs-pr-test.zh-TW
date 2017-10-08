---
title: "教學課程：使用複製精靈建立管線 | Microsoft Docs"
description: "在本教學課程中，您建立 Azure Data Factory 管線與複製活動使用 hello 複製精靈支援的 Data Factory"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="5635d-103">教學課程：使用 Data Factory 複製精靈建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="5635d-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5635d-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="5635d-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="5635d-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="5635d-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="5635d-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5635d-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="5635d-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5635d-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="5635d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5635d-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="5635d-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="5635d-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="5635d-110">REST API</span><span class="sxs-lookup"><span data-stu-id="5635d-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="5635d-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="5635d-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="5635d-112">本教學課程示範如何 toouse hello**複製精靈**toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="5635d-112">This tutorial shows you how toouse hello **Copy Wizard** toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

<span data-ttu-id="5635d-113">hello Azure Data Factory**複製精靈**可讓您 tooquickly 建立將資料從支援的來源資料存放區支援 tooa 目的地資料存放區複製在資料管線。</span><span class="sxs-lookup"><span data-stu-id="5635d-113">hello Azure Data Factory **Copy Wizard** allows you tooquickly create a data pipeline that copies data from a supported source data store tooa supported destination data store.</span></span> <span data-ttu-id="5635d-114">因此，我們建議當做第一個步驟 toocreate 範例管線使用 hello 精靈，為您的資料移動案例。</span><span class="sxs-lookup"><span data-stu-id="5635d-114">Therefore, we recommend that you use hello wizard as a first step toocreate a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="5635d-115">如需作為來源和目的地支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="5635d-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="5635d-116">本教學課程會示範如何 toocreate Azure data factory，啟動 hello 複製精靈 」，通過一連串的步驟 tooprovide 詳細資料的擷取/移動案例。</span><span class="sxs-lookup"><span data-stu-id="5635d-116">This tutorial shows you how toocreate an Azure data factory, launch hello Copy Wizard, go through a series of steps tooprovide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="5635d-117">當您完成在 hello 精靈的步驟時，hello 精靈會自動建立管線複製活動 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="5635d-117">When you finish steps in hello wizard, hello wizard automatically creates a pipeline with a Copy Activity toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="5635d-118">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="5635d-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5635d-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="5635d-119">Prerequisites</span></span>
<span data-ttu-id="5635d-120">完成 hello 中所列必要條件[教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)發行項，然後再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="5635d-120">Complete prerequisites listed in hello [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="5635d-121">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="5635d-121">Create data factory</span></span>
<span data-ttu-id="5635d-122">在此步驟中，您使用 Azure 入口網站 toocreate 名為 Azure data factory hello **ADFTutorialDataFactory**。</span><span class="sxs-lookup"><span data-stu-id="5635d-122">In this step, you use hello Azure portal toocreate an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="5635d-123">登入太[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5635d-123">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5635d-124">按一下**+ 新增**從 hello 左上角，按一下 **資料 + 分析**，然後按一下**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="5635d-124">Click **+ NEW** from hello top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![新增->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="5635d-126">在 hello**新的 data factory**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="5635d-126">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="5635d-127">輸入**ADFTutorialDataFactory** hello**名稱**。</span><span class="sxs-lookup"><span data-stu-id="5635d-127">Enter **ADFTutorialDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="5635d-128">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="5635d-128">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="5635d-129">如果您收到 hello 錯誤： `Data factory name “ADFTutorialDataFactory” is not available`、 變更 hello hello data factory (例如，yournameADFTutorialDataFactoryYYYYMMDD) 名稱，然後再次嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="5635d-129">If you receive hello error: `Data factory name “ADFTutorialDataFactory” is not available`, change hello name of hello data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="5635d-130">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="5635d-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Data Factory 名稱無法使用](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="5635d-132">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="5635d-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="5635d-133">資源群組，請執行步驟的 hello 其中一項：</span><span class="sxs-lookup"><span data-stu-id="5635d-133">For Resource Group, do one of hello following steps:</span></span> 
      
      - <span data-ttu-id="5635d-134">選取**使用現有**tooselect 現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5635d-134">Select **Use existing** tooselect an existing resource group.</span></span>
      - <span data-ttu-id="5635d-135">選取**建立新**tooenter 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="5635d-135">Select **Create new** tooenter a name for a resource group.</span></span>
          
        <span data-ttu-id="5635d-136">部分 hello 步驟在本教學課程假設您使用 hello 名稱： **ADFTutorialResourceGroup** hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="5635d-136">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="5635d-137">toolearn 解資源群組，請參閱[資源使用您的 Azure 資源群組 toomanage](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5635d-137">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="5635d-138">選取**位置**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="5635d-138">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="5635d-139">選取**Pin toodashboard**在 hello hello 刀鋒視窗底部的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5635d-139">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="5635d-140">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5635d-140">Click **Create**.</span></span>
      
       ![新增 Data Factory 刀鋒視窗](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="5635d-142">Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="5635d-142">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>
   
   ![Data Factory 首頁](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="5635d-144">啟動複製精靈</span><span class="sxs-lookup"><span data-stu-id="5635d-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="5635d-145">在 hello Data Factory 刀鋒視窗中，按一下 **複製資料 [預覽]** toolaunch hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="5635d-145">On hello Data Factory blade, click **Copy data [PREVIEW]** toolaunch hello **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5635d-146">如果您看到該 hello 網頁瀏覽器卡在 [授權]，停用/取消核取**封鎖第三方 cookie 和站台資料**在 hello 瀏覽器設定 （或） 保持啟用此設定，並建立的例外狀況**login.microsoftonline.com** ，然後再次嘗試重新啟動 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="5635d-146">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in hello browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="5635d-147">在 hello**屬性**頁面：</span><span class="sxs-lookup"><span data-stu-id="5635d-147">In hello **Properties** page:</span></span>
   
   1. <span data-ttu-id="5635d-148">輸入 **CopyFromBlobToAzureSql** 做為 [工作名稱]</span><span class="sxs-lookup"><span data-stu-id="5635d-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="5635d-149">輸入 **說明** (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="5635d-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="5635d-150">變更 hello**的開始日期時間**和 hello**結束日期時間**使 hello 結束日期設定 tootoday 且開始日期 toofive 天前。</span><span class="sxs-lookup"><span data-stu-id="5635d-150">Change hello **Start date time** and hello **End date time** so that hello end date is set tootoday and start date toofive days earlier.</span></span>  
   4. <span data-ttu-id="5635d-151">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5635d-151">Click **Next**.</span></span>  
      
      ![複製工具 - 屬性頁面](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="5635d-153">在 hello**來源資料存放區**頁面上，按一下**Azure Blob 儲存體**磚。</span><span class="sxs-lookup"><span data-stu-id="5635d-153">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="5635d-154">您可以使用這個頁面 toospecify hello 來源資料存放區 hello 複製工作。</span><span class="sxs-lookup"><span data-stu-id="5635d-154">You use this page toospecify hello source data store for hello copy task.</span></span> 
   
    ![複製工具 - 來源資料儲存頁面](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="5635d-156">在 hello**指定 hello Azure Blob 儲存體帳戶**頁面：</span><span class="sxs-lookup"><span data-stu-id="5635d-156">On hello **Specify hello Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="5635d-157">輸入 **AzureStorageLinkedService** 做為 [連結服務名稱]。</span><span class="sxs-lookup"><span data-stu-id="5635d-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="5635d-158">確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="5635d-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="5635d-159">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="5635d-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="5635d-160">選取**Azure 儲存體帳戶**從 hello hello 選取訂用帳戶中可使用的清單中的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5635d-160">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="5635d-161">您也可以選擇 tooenter 儲存體帳戶設定手動選取**手動輸入**選項 hello**帳戶選取方法**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5635d-161">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**, and then click **Next**.</span></span> 
      
      ![複製工具-指定 hello Azure Blob 儲存體帳戶](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="5635d-163">在**選擇 hello 輸入的檔案或資料夾**頁面：</span><span class="sxs-lookup"><span data-stu-id="5635d-163">On **Choose hello input file or folder** page:</span></span>
   
   1. <span data-ttu-id="5635d-164">按兩下 **adftutorial** (資料夾)。</span><span class="sxs-lookup"><span data-stu-id="5635d-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="5635d-165">選取 **emp.txt**，然後按一下 [選擇]</span><span class="sxs-lookup"><span data-stu-id="5635d-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="5635d-167">在 hello**選擇 hello 輸入的檔案或資料夾**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5635d-167">On hello **Choose hello input file or folder** page, click **Next**.</span></span> <span data-ttu-id="5635d-168">請勿選取 [二進位複本] 。</span><span class="sxs-lookup"><span data-stu-id="5635d-168">Do not select **Binary copy**.</span></span> 
   
    ![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="5635d-170">在 hello**檔案格式設定** 頁面上，您會看到 hello 分隔符號和是藉由剖析 hello 檔案的 自動偵測到的 hello 精靈的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="5635d-170">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> <span data-ttu-id="5635d-171">您也可以手動輸入 hello 分隔符號 hello 複製精靈 toostop 自動偵測或 toooverride。</span><span class="sxs-lookup"><span data-stu-id="5635d-171">You can also enter hello delimiters manually for hello copy wizard toostop auto-detecting or toooverride.</span></span> <span data-ttu-id="5635d-172">按一下**下一步**在檢閱 hello 分隔符號和預覽資料。</span><span class="sxs-lookup"><span data-stu-id="5635d-172">Click **Next** after you review hello delimiters and preview data.</span></span> 
   
    ![複製工具 - 檔案格式設定](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="5635d-174">Hello 目的地資料存放區 頁面中，選取**Azure SQL Database**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5635d-174">On hello Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![複製工具 - 選擇目的地存放區](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="5635d-176">在**指定 hello Azure SQL database**頁面：</span><span class="sxs-lookup"><span data-stu-id="5635d-176">On **Specify hello Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="5635d-177">輸入**AzureSqlLinkedService** hello**連接名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="5635d-177">Enter **AzureSqlLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="5635d-178">確認已針對 [伺服器 / 資料庫選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="5635d-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="5635d-179">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="5635d-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="5635d-180">選取 [伺服器名稱] 和 [資料庫]。</span><span class="sxs-lookup"><span data-stu-id="5635d-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="5635d-181">輸入 [使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="5635d-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="5635d-182">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5635d-182">Click **Next**.</span></span>  
      
      ![複製工具 - 指定 Azure SQL Database](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="5635d-184">在 hello**資料表對應**頁面上，選取**emp** hello**目的地**欄位從 hello 下拉式清單中，按一下**向下箭號**（選擇性）toosee hello 結構描述和 toopreview hello 資料。</span><span class="sxs-lookup"><span data-stu-id="5635d-184">On hello **Table mapping** page, select **emp** for hello **Destination** field from hello drop-down list, click **down arrow** (optional) toosee hello schema and toopreview hello data.</span></span>
    
     ![複製工具 - 資料表對應](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="5635d-186">在 hello**結構描述對應**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5635d-186">On hello **Schema mapping** page, click **Next**.</span></span>
    
    ![複製工具 - 結構描述對應](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="5635d-188">在 hello**效能設定**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5635d-188">On hello **Performance settings** page, click **Next**.</span></span> 
    
    ![複製工具 - 效能設定](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="5635d-190">檢閱資訊在 hello**摘要**頁面，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="5635d-190">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="5635d-191">hello 精靈會建立兩個連結的服務、 兩個資料集 （輸入與輸出），以及一個管線 （從啟動 hello 複製精靈 」 的位置） 的 hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="5635d-191">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span> 
    
    ![複製工具 - 效能設定](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="5635d-193">啟動監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="5635d-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="5635d-194">在 hello**部署**頁面上，按一下 hello 連結： `Click here toomonitor copy pipeline`。</span><span class="sxs-lookup"><span data-stu-id="5635d-194">On hello **Deployment** page, click hello link: `Click here toomonitor copy pipeline`.</span></span>
   
   ![複製工具 - 部署成功](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="5635d-196">hello 監視應用程式會啟動網頁瀏覽器中的個別索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="5635d-196">hello monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![監視應用程式](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="5635d-198">toosee hello 最新狀態的每小時的配量，按一下**重新整理**按鈕在 hello**活動 WINDOWS** hello 底部的清單。</span><span class="sxs-lookup"><span data-stu-id="5635d-198">toosee hello latest status of hourly slices, click **Refresh** button in hello **ACTIVITY WINDOWS** list at hello bottom.</span></span> <span data-ttu-id="5635d-199">您會看到五天之間 hello 管線的開始和結束時間的五個活動視窗。</span><span class="sxs-lookup"><span data-stu-id="5635d-199">You see five activity windows for five days between start and end times for hello pipeline.</span></span> <span data-ttu-id="5635d-200">hello 清單不會自動重新整理，因此您可能需要 tooclick 重新整理數次，才會看到 hello 就緒狀態中的所有 hello 活動視窗。</span><span class="sxs-lookup"><span data-stu-id="5635d-200">hello list is not automatically refreshed, so you may need tooclick Refresh a couple of times before you see all hello activity windows in hello Ready state.</span></span> 
4. <span data-ttu-id="5635d-201">Hello 清單中選取活動視窗。</span><span class="sxs-lookup"><span data-stu-id="5635d-201">Select an activity window in hello list.</span></span> <span data-ttu-id="5635d-202">Hello 中檢視詳細資料資訊，請參閱 hello**活動視窗總管**hello 右上。</span><span class="sxs-lookup"><span data-stu-id="5635d-202">See hello details about it in hello **Activity Window Explorer** on hello right.</span></span>

    ![活動時段詳細資料](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="5635d-204">請注意，11、 12、 13、 14 和 15 hello 日期都為綠色，表示已經所產生 hello 每日輸出配量這些日期。</span><span class="sxs-lookup"><span data-stu-id="5635d-204">Notice that hello dates 11, 12, 13, 14, and 15 are in green color, which means that hello daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="5635d-205">您也可以看到這個色彩編碼 hello 管線然後 hello hello 圖表檢視 中的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="5635d-205">You also see this color coding on hello pipeline and hello output dataset in hello diagram view.</span></span> <span data-ttu-id="5635d-206">在 hello 先前步驟中，請注意，兩個配量已產生，目前正在處理一個扇區，hello 其他兩個正在等候處理的 toobe （根據 hello 色彩編碼）。</span><span class="sxs-lookup"><span data-stu-id="5635d-206">In hello previous step, notice that two slices have already been produced, one slice is currently being processed, and hello other two are waiting toobe processed (based on hello color coding).</span></span> 

    <span data-ttu-id="5635d-207">如需使用此應用程式的詳細資訊，請參閱[使用監視應用程式來監視和管理管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="5635d-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5635d-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5635d-208">Next steps</span></span>
<span data-ttu-id="5635d-209">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5635d-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="5635d-210">hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單：</span><span class="sxs-lookup"><span data-stu-id="5635d-210">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="5635d-211">如需您在資料存放區的 hello 複製精靈中看到的欄位/屬性的詳細資訊，按一下 hello 連結 hello hello 資料表中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5635d-211">For details about fields/properties that you see in hello copy wizard for a data store, click hello link for hello data store in hello table.</span></span> 
