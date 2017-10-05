---
title: "教學課程：使用複製精靈建立管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 Data Factory 所支援的複製精靈，建立具有複製活動的 Azure Data Factory 管線。"
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
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="591c0-103">教學課程：使用 Data Factory 複製精靈建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="591c0-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="591c0-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="591c0-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="591c0-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="591c0-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="591c0-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="591c0-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="591c0-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="591c0-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="591c0-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="591c0-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="591c0-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="591c0-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="591c0-110">REST API</span><span class="sxs-lookup"><span data-stu-id="591c0-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="591c0-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="591c0-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="591c0-112">本教學課程說明如何使用**複製精靈**，將資料從 Azure Blob 儲存體複製到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="591c0-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="591c0-113">Azure Data Factory 的[複製精靈] 可讓您快速建立資料管線，以將資料從支援的來源資料存放區複製到支援的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="591c0-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="591c0-114">因此，建議在第一個步驟中使用精靈來建立資料移動案例的範例管線。</span><span class="sxs-lookup"><span data-stu-id="591c0-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="591c0-115">如需作為來源和目的地支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="591c0-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="591c0-116">本教學課程說明如何建立 Azure data factory、啟動 [複製精靈]、執行一系列的步驟，以提供有關資料擷取/移動案例的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="591c0-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="591c0-117">當您完成精靈中的步驟時，精靈會自動建立具有複製活動的管線，以將資料從 Azure Blob 儲存體複製到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="591c0-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="591c0-118">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="591c0-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="591c0-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="591c0-119">Prerequisites</span></span>
<span data-ttu-id="591c0-120">請先完成 [教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 一文中列出的必要條件，再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="591c0-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="591c0-121">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="591c0-121">Create data factory</span></span>
<span data-ttu-id="591c0-122">在此步驟中，您會使用 Azure 入口網站來建立名為 **ADFTutorialDataFactory**的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="591c0-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="591c0-123">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="591c0-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="591c0-124">按一下左上角的 [+ 新增]，並按一下 [資料 + 分析]，然後按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="591c0-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![新增->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="591c0-126">在 [ **新增 Data Factory** ] 刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="591c0-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="591c0-127">輸入 **ADFTutorialDataFactory** 做為**名稱**。</span><span class="sxs-lookup"><span data-stu-id="591c0-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="591c0-128">Azure Data Factory 的名稱在全域必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="591c0-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="591c0-129">如果您收到錯誤：`Data factory name “ADFTutorialDataFactory” is not available`，請變更資料處理站名稱 (例如 yournameADFTutorialDataFactoryYYYYMMDD)，然後試著重新建立。</span><span class="sxs-lookup"><span data-stu-id="591c0-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="591c0-130">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="591c0-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Data Factory 名稱無法使用](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="591c0-132">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="591c0-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="591c0-133">針對資源群組，請執行下列其中一個步驟︰</span><span class="sxs-lookup"><span data-stu-id="591c0-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="591c0-134">選取 [使用現有的] 以選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="591c0-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="591c0-135">選取 [建立新的] 以輸入資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="591c0-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="591c0-136">本教學課程的某些步驟是假設您使用 **ADFTutorialResourceGroup** 做為資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="591c0-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="591c0-137">若要了解資源群組，請參閱 [使用資源群組管理您的 Azure 資源](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="591c0-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="591c0-138">選取 Data Factory 的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="591c0-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="591c0-139">選取刀鋒視窗底部的 [釘選到儀表板] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="591c0-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="591c0-140">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="591c0-140">Click **Create**.</span></span>
      
       ![新增 Data Factory 刀鋒視窗](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="591c0-142">建立完成之後，您會看到 [Data Factory] 刀鋒視窗，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="591c0-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Data Factory 首頁](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="591c0-144">啟動複製精靈</span><span class="sxs-lookup"><span data-stu-id="591c0-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="591c0-145">在 Data Factory 刀鋒視窗上，按一下 [複製資料 (預覽)] 來啟動 [複製精靈]。</span><span class="sxs-lookup"><span data-stu-id="591c0-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="591c0-146">如果您看到網頁瀏覽器停留在「授權中...」，請停用/取消核取瀏覽器設定中的 [封鎖第三方 Cookie 和站台資料] 設定 (或) 將它保持啟用並為 **login.microsoftonline.com** 建立例外狀況，然後再次嘗試啟動精靈。</span><span class="sxs-lookup"><span data-stu-id="591c0-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="591c0-147">在 [屬性]  頁面︰</span><span class="sxs-lookup"><span data-stu-id="591c0-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="591c0-148">輸入 **CopyFromBlobToAzureSql** 做為 [工作名稱]</span><span class="sxs-lookup"><span data-stu-id="591c0-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="591c0-149">輸入 **說明** (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="591c0-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="591c0-150">變更 [開始日期時間] 和 [結束日期時間]，讓結束日期設為今天，而開始日期設為五天前。</span><span class="sxs-lookup"><span data-stu-id="591c0-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="591c0-151">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="591c0-151">Click **Next**.</span></span>  
      
      ![複製工具 - 屬性頁面](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="591c0-153">在 [來源資料存放區] 頁面上，按一下 [Azure Blob 儲存體] 圖格。</span><span class="sxs-lookup"><span data-stu-id="591c0-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="591c0-154">您可以使用此頁面來指定複製工作的來源資料存放區。</span><span class="sxs-lookup"><span data-stu-id="591c0-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![複製工具 - 來源資料儲存頁面](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="591c0-156">在 [指定 Azure Blob 儲存體帳戶]  頁面︰</span><span class="sxs-lookup"><span data-stu-id="591c0-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="591c0-157">輸入 **AzureStorageLinkedService** 做為 [連結服務名稱]。</span><span class="sxs-lookup"><span data-stu-id="591c0-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="591c0-158">確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="591c0-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="591c0-159">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="591c0-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="591c0-160">從所選訂用帳戶中可用的 Azure 儲存體帳戶清單中，選取 [Azure 儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="591c0-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="591c0-161">您也可以選擇手動輸入儲存體帳戶設定，其做法是選取 [帳戶選取方法] 的 [手動輸入] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="591c0-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![複製工具 - 指定 Azure Blob 儲存體帳戶](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="591c0-163">在 [選擇輸入檔案或資料夾]  頁面︰</span><span class="sxs-lookup"><span data-stu-id="591c0-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="591c0-164">按兩下 **adftutorial** (資料夾)。</span><span class="sxs-lookup"><span data-stu-id="591c0-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="591c0-165">選取 **emp.txt**，然後按一下 [選擇]</span><span class="sxs-lookup"><span data-stu-id="591c0-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![複製工具 - 選擇輸入檔案或資料夾](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="591c0-167">在 [選擇輸入檔案或資料夾] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="591c0-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="591c0-168">請勿選取 [二進位複本] 。</span><span class="sxs-lookup"><span data-stu-id="591c0-168">Do not select **Binary copy**.</span></span> 
   
    ![複製工具 - 選擇輸入檔案或資料夾](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="591c0-170">在 [檔案格式設定] 頁面上，您會看到分隔符號以及精靈藉由剖析檔案自動偵測到的結構描述。</span><span class="sxs-lookup"><span data-stu-id="591c0-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="591c0-171">您也可以手動輸入複製精靈的分隔符號，以停止自動偵測或進行覆寫。</span><span class="sxs-lookup"><span data-stu-id="591c0-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="591c0-172">檢閱分隔符號並預覽資料之後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="591c0-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![複製工具 - 檔案格式設定](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="591c0-174">在 [目的地資料存放區] 頁面上，選取 [Azure SQL Database]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="591c0-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![複製工具 - 選擇目的地存放區](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="591c0-176">在 [指定 Azure SQL Database]  頁面︰</span><span class="sxs-lookup"><span data-stu-id="591c0-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="591c0-177">針對 [連線名稱] 欄位輸入 **AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="591c0-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="591c0-178">確認已針對 [伺服器 / 資料庫選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="591c0-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="591c0-179">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="591c0-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="591c0-180">選取 [伺服器名稱] 和 [資料庫]。</span><span class="sxs-lookup"><span data-stu-id="591c0-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="591c0-181">輸入 [使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="591c0-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="591c0-182">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="591c0-182">Click **Next**.</span></span>  
      
      ![複製工具 - 指定 Azure SQL Database](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="591c0-184">在 [資料表對應] 頁面上，從 [目的地] 欄位的下拉式清單中選取 **emp**，按一下**向下箭號** (選擇性) 以查看結構描述及預覽資料。</span><span class="sxs-lookup"><span data-stu-id="591c0-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![複製工具 - 資料表對應](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="591c0-186">在 [結構描述對應] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="591c0-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![複製工具 - 結構描述對應](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="591c0-188">在 [效能設定] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="591c0-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![複製工具 - 效能設定](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="591c0-190">在 [摘要] 頁面中檢閱資訊，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="591c0-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="591c0-191">此精靈會在 Data Factory (從您啟動複製精靈的位置) 中建立兩個連結服務、兩個資料集 (輸入和輸出)，以及一個管線。</span><span class="sxs-lookup"><span data-stu-id="591c0-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![複製工具 - 效能設定](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="591c0-193">啟動監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="591c0-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="591c0-194">在 [部署] 頁面上，按一下連結︰`Click here to monitor copy pipeline`。</span><span class="sxs-lookup"><span data-stu-id="591c0-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![複製工具 - 部署成功](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="591c0-196">監視應用程式會在網頁瀏覽器中的個別索引標籤中啟動。</span><span class="sxs-lookup"><span data-stu-id="591c0-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![監視應用程式](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="591c0-198">若要查看每小時配量的最新狀態，請按一下底部 [活動時段] 清單中的 [重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="591c0-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="591c0-199">您可看到介於管線開始與結束時間之間五天的五個活動時段。</span><span class="sxs-lookup"><span data-stu-id="591c0-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="591c0-200">此清單不會自動重新整理，所以您可能需要按一下 [重新整理] 數次，才能看見處於 [就緒] 狀態的所有活動時段。</span><span class="sxs-lookup"><span data-stu-id="591c0-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="591c0-201">選取清單中的活動時段。</span><span class="sxs-lookup"><span data-stu-id="591c0-201">Select an activity window in the list.</span></span> <span data-ttu-id="591c0-202">請參閱右側 [活動時段總管] 中的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="591c0-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![活動時段詳細資料](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="591c0-204">請注意，日期 11、12、13、14 及 15 均為綠色，這表示已經產生這些日期的每日輸出配量。</span><span class="sxs-lookup"><span data-stu-id="591c0-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="591c0-205">您也可在圖表檢視中的管線和輸出資料集上看到此色彩編碼。</span><span class="sxs-lookup"><span data-stu-id="591c0-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="591c0-206">在上一個步驟中，請注意，已經產生兩個配量，有一個配量目前處理中，還有其他兩個配量等待處理 (根據色彩編碼)。</span><span class="sxs-lookup"><span data-stu-id="591c0-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="591c0-207">如需使用此應用程式的詳細資訊，請參閱[使用監視應用程式來監視和管理管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="591c0-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="591c0-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="591c0-208">Next steps</span></span>
<span data-ttu-id="591c0-209">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="591c0-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="591c0-210">下表提供複製活動所支援作為來源或目的地的資料存放區清單：</span><span class="sxs-lookup"><span data-stu-id="591c0-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="591c0-211">如需您在資料存放區的複製精靈中看到的欄位/屬性詳細資訊，請按一下資料表中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="591c0-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 