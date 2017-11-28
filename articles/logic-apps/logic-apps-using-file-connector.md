---
title: "從 Azure Logic Apps 連線到內部部署檔案系統 | Microsoft Docs"
description: "透過內部部署資料閘道和檔案系統連接器，連線到邏輯應用程式工作流程中的內部部署檔案系統"
keywords: "檔案系統"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="9f941-104">使用檔案系統連接器，從邏輯應用程式連線到內部部署檔案系統</span><span class="sxs-lookup"><span data-stu-id="9f941-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="9f941-105">混合式雲端連線的核心是邏輯應用程式，因此，若要管理資料，並安全地存取內部部署資源，則您的邏輯應用程式可以使用內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="9f941-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="9f941-106">在本文中，我們會以一個基本的案例來示範如何連線至內部部署檔案系統︰將已上傳至 Dropbox 的檔案複製到檔案共用，然後傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9f941-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f941-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f941-107">Prerequisites</span></span>

- <span data-ttu-id="9f941-108">安裝及設定最新的[內部部署資料閘道](https://www.microsoft.com/download/details.aspx?id=53127)。</span><span class="sxs-lookup"><span data-stu-id="9f941-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="9f941-109">安裝版本 1.15.6150.1 或更高版本的最新內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="9f941-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="9f941-110">[連接至內部部署資料閘道](http://aka.ms/logicapps-gateway)會列出步驟。</span><span class="sxs-lookup"><span data-stu-id="9f941-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="9f941-111">必須先在內部部署機器上安裝閘道，才能繼續執行其餘的步驟。</span><span class="sxs-lookup"><span data-stu-id="9f941-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="9f941-112">新增用來連線到檔案系統的觸發程序和動作</span><span class="sxs-lookup"><span data-stu-id="9f941-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="9f941-113">建立邏輯應用程式，並新增這個 Dropbox 觸發程序：**建立檔案時**</span><span class="sxs-lookup"><span data-stu-id="9f941-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="9f941-114">在觸發程序下方，選擇 [下一步] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="9f941-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="9f941-115">在搜尋方塊中，輸入 `file system`，讓您可以檢視檔案系統連接器支援的所有動作。</span><span class="sxs-lookup"><span data-stu-id="9f941-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![搜尋檔案連接器](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="9f941-117">選擇 [建立檔案] 動作，然後建立與您檔案系統的連線。</span><span class="sxs-lookup"><span data-stu-id="9f941-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="9f941-118">如果您目前沒有連線，系統會提示您建立連線。</span><span class="sxs-lookup"><span data-stu-id="9f941-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="9f941-119">選擇 [透過內部部署資料閘道連線]。</span><span class="sxs-lookup"><span data-stu-id="9f941-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="9f941-120">隨即出現更多屬性。</span><span class="sxs-lookup"><span data-stu-id="9f941-120">More properties appear.</span></span>
   2. <span data-ttu-id="9f941-121">選取檔案系統的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="9f941-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="9f941-122">根資料夾是主要的父資料夾，會作為所有檔案相關動作的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="9f941-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="9f941-123">您可以指定內部部署資料閘道安裝所在電腦的本機資料夾，或者資料夾可以是電腦可存取的網路共用。</span><span class="sxs-lookup"><span data-stu-id="9f941-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="9f941-124">輸入閘道的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="9f941-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="9f941-125">選取您先前安裝的閘道。</span><span class="sxs-lookup"><span data-stu-id="9f941-125">Select the gateway that you previously installed.</span></span>

       ![設定連線](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="9f941-127">提供所有詳細資料之後，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="9f941-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="9f941-128">Logic Apps 會設定並測試連線，以確定連線運作正常。</span><span class="sxs-lookup"><span data-stu-id="9f941-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="9f941-129">如果已正確設定連線，則會看到您先前所選取動作的選項。</span><span class="sxs-lookup"><span data-stu-id="9f941-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="9f941-130">檔案系統連接器現在已可供使用。</span><span class="sxs-lookup"><span data-stu-id="9f941-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="9f941-131">指定您想要將檔案從 Dropbox 複製到您內部部署檔案共用的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="9f941-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![建立檔案動作](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="9f941-133">邏輯應用程式複製檔案之後，請新增傳送電子郵件的 Outlook 動作，讓相關使用者了解新的檔案。</span><span class="sxs-lookup"><span data-stu-id="9f941-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="9f941-134">輸入電子郵件的收件者、標題和本文。</span><span class="sxs-lookup"><span data-stu-id="9f941-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="9f941-135">在動態內容選取器中，您可以選擇來自檔案連接器的資料輸出，以將更多詳細資料新增至電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9f941-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![傳送電子郵件動作](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="9f941-137">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f941-137">Save your logic app.</span></span> <span data-ttu-id="9f941-138">將檔案上傳至 Dropbox，以測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f941-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="9f941-139">檔案應該會複製到內部部署檔案共用，而且您應該會收到該作業的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9f941-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="9f941-140">了解如何[監視邏輯應用程式](../logic-apps/logic-apps-monitor-your-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="9f941-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="9f941-141">恭喜，您現在已經有可運作的邏輯應用程式，可連線到內部部署檔案系統的。</span><span class="sxs-lookup"><span data-stu-id="9f941-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="9f941-142">請嘗試探索連接器所提供的其他功能，例如︰</span><span class="sxs-lookup"><span data-stu-id="9f941-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="9f941-143">建立檔案</span><span class="sxs-lookup"><span data-stu-id="9f941-143">Create file</span></span>
- <span data-ttu-id="9f941-144">列出資料夾中的檔案</span><span class="sxs-lookup"><span data-stu-id="9f941-144">List files in folder</span></span>
- <span data-ttu-id="9f941-145">附加檔案</span><span class="sxs-lookup"><span data-stu-id="9f941-145">Append file</span></span>
- <span data-ttu-id="9f941-146">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="9f941-146">Delete file</span></span>
- <span data-ttu-id="9f941-147">取得檔案內容</span><span class="sxs-lookup"><span data-stu-id="9f941-147">Get file content</span></span>
- <span data-ttu-id="9f941-148">使用路徑來取得檔案內容</span><span class="sxs-lookup"><span data-stu-id="9f941-148">Get file content using path</span></span>
- <span data-ttu-id="9f941-149">取得檔案中繼資料</span><span class="sxs-lookup"><span data-stu-id="9f941-149">Get file metadata</span></span>
- <span data-ttu-id="9f941-150">使用路徑取得檔案中繼資料</span><span class="sxs-lookup"><span data-stu-id="9f941-150">Get file metadata using path</span></span>
- <span data-ttu-id="9f941-151">列出根資料夾中的檔案</span><span class="sxs-lookup"><span data-stu-id="9f941-151">List files in root folder</span></span>
- <span data-ttu-id="9f941-152">更新檔案</span><span class="sxs-lookup"><span data-stu-id="9f941-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="9f941-153">檢視 Swagger</span><span class="sxs-lookup"><span data-stu-id="9f941-153">View the swagger</span></span>
<span data-ttu-id="9f941-154">請參閱 [Swagger 詳細資料](/connectors/fileconnector/)。</span><span class="sxs-lookup"><span data-stu-id="9f941-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="9f941-155">取得說明</span><span class="sxs-lookup"><span data-stu-id="9f941-155">Get help</span></span>

<span data-ttu-id="9f941-156">若要提出問題、回答問題以及了解其他 Azure Logic Apps 使用者的做法，請造訪 [Azure Logic Apps 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="9f941-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="9f941-157">若要改善 Azure Logic Apps 和連接器，請在 [Azure Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)上票選或提交想法。</span><span class="sxs-lookup"><span data-stu-id="9f941-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f941-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f941-158">Next steps</span></span>

- <span data-ttu-id="9f941-159">從邏輯應用程式[連線到內部部署資料](../logic-apps/logic-apps-gateway-connection.md)</span><span class="sxs-lookup"><span data-stu-id="9f941-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="9f941-160">了解[企業整合](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9f941-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
