---
title: "aaaConnect tooon 內部檔案系統從 Azure 邏輯應用程式 |Microsoft 文件"
description: "邏輯應用程式工作流程透過 hello 在內部部署資料閘道和檔案系統連接器連接 tooon 內部部署檔案系統"
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
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="f6dc5-104">邏輯應用程式與 hello 檔案系統連接器連接 tooon 內部部署檔案系統</span><span class="sxs-lookup"><span data-stu-id="f6dc5-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="f6dc5-105">混合式雲端連線是中央 toologic 應用程式，因此 toomanage 資料和安全地存取內部資源，您的 logic apps 可以使用 hello 在內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="f6dc5-106">在本文中，我們會示範如何 tooconnect tooan 內部檔案系統與基本案例： 複製的檔案的上傳的 tooDropbox tooa 檔案共用，然後傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6dc5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="f6dc5-107">Prerequisites</span></span>

- <span data-ttu-id="f6dc5-108">安裝及最新設定 hello[在內部部署資料閘道](https://www.microsoft.com/download/details.aspx?id=53127)。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="f6dc5-109">安裝 hello 最新的內部部署資料閘道，1.15.6150.1 版本或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="f6dc5-110">[Toohello 在內部部署資料閘道連接](http://aka.ms/logicapps-gateway)清單 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="f6dc5-111">hello 閘道必須安裝在內部部署電腦上，才能繼續與 hello 步驟 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="f6dc5-112">加入觸發程序和連接 tooyour 檔案系統的動作</span><span class="sxs-lookup"><span data-stu-id="f6dc5-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="f6dc5-113">建立邏輯應用程式，並新增這個 Dropbox 觸發程序：**建立檔案時**</span><span class="sxs-lookup"><span data-stu-id="f6dc5-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="f6dc5-114">在 hello 觸發程序中，選擇**下一個步驟** > **將動作加入**。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="f6dc5-115">在 [hello] 搜尋方塊中，輸入`file system`使您可以檢視 hello 檔案系統連接器的所有支援的動作。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![搜尋檔案連接器](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="f6dc5-117">選擇 hello**建立檔案**動作，並建立連接 tooyour 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="f6dc5-118">如果您沒有現有的連接，您必須提示的 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="f6dc5-119">選擇 [透過內部部署資料閘道連線]。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="f6dc5-120">隨即出現更多屬性。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-120">More properties appear.</span></span>
   2. <span data-ttu-id="f6dc5-121">選取檔案系統的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="f6dc5-122">hello 根資料夾為 hello 主要父資料夾，用於所有檔案相關動作的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="f6dc5-123">您可以指定本機資料夾 hello 機器 hello 在內部部署資料閘道已安裝，或 hello 資料夾可以是可以存取 hello 機器的網路共用位置上。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="f6dc5-124">輸入 hello 閘道 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="f6dc5-125">選取您先前安裝的 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-125">Select hello gateway that you previously installed.</span></span>

       ![設定連線](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="f6dc5-127">提供所有 hello 詳細資料之後，請選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="f6dc5-128">邏輯應用程式設定，並測試您的連線，並確定 hello 連線正常運作。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="f6dc5-129">如果 hello 連線已正確設定時，您會看到您先前選取的 hello 動作選項。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="f6dc5-130">hello 檔案系統連接器現在可供使用。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="f6dc5-131">指定您要 toocopy Dropbox toohello 根資料夾中的檔案，您的內部檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![建立檔案動作](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="f6dc5-133">邏輯應用程式複本 hello 檔案之後, 加入的 Outlook 動作傳送電子郵件，因此相關使用者了解 hello 新檔案。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="f6dc5-134">輸入 hello 收件者、 標題和 hello 電子郵件的本文。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="f6dc5-135">在 hello 動態的內容選取器，您可以選擇資料輸出 hello 檔案連接器好讓您可以加入更多詳細資料 toohello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![傳送電子郵件動作](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="f6dc5-137">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-137">Save your logic app.</span></span> <span data-ttu-id="f6dc5-138">上傳檔案 tooDropbox 來測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="f6dc5-139">hello 檔案應該會收到複製的 toohello 內部檔案共用，以及您應該會收到 hello 作業的相關電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="f6dc5-140">了解如何太[監視您的 logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="f6dc5-141">恭喜，您現在可以使用邏輯應用程式可以連接 tooyour 在內部部署檔案系統。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="f6dc5-142">請嘗試瀏覽例如 hello 連接器提供其他功能：</span><span class="sxs-lookup"><span data-stu-id="f6dc5-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="f6dc5-143">建立檔案</span><span class="sxs-lookup"><span data-stu-id="f6dc5-143">Create file</span></span>
- <span data-ttu-id="f6dc5-144">列出資料夾中的檔案</span><span class="sxs-lookup"><span data-stu-id="f6dc5-144">List files in folder</span></span>
- <span data-ttu-id="f6dc5-145">附加檔案</span><span class="sxs-lookup"><span data-stu-id="f6dc5-145">Append file</span></span>
- <span data-ttu-id="f6dc5-146">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="f6dc5-146">Delete file</span></span>
- <span data-ttu-id="f6dc5-147">取得檔案內容</span><span class="sxs-lookup"><span data-stu-id="f6dc5-147">Get file content</span></span>
- <span data-ttu-id="f6dc5-148">使用路徑來取得檔案內容</span><span class="sxs-lookup"><span data-stu-id="f6dc5-148">Get file content using path</span></span>
- <span data-ttu-id="f6dc5-149">取得檔案中繼資料</span><span class="sxs-lookup"><span data-stu-id="f6dc5-149">Get file metadata</span></span>
- <span data-ttu-id="f6dc5-150">使用路徑取得檔案中繼資料</span><span class="sxs-lookup"><span data-stu-id="f6dc5-150">Get file metadata using path</span></span>
- <span data-ttu-id="f6dc5-151">列出根資料夾中的檔案</span><span class="sxs-lookup"><span data-stu-id="f6dc5-151">List files in root folder</span></span>
- <span data-ttu-id="f6dc5-152">更新檔案</span><span class="sxs-lookup"><span data-stu-id="f6dc5-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="f6dc5-153">檢視 hello swagger</span><span class="sxs-lookup"><span data-stu-id="f6dc5-153">View hello swagger</span></span>
<span data-ttu-id="f6dc5-154">請參閱 hello [swagger 詳細資料](/connectors/fileconnector/)。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="f6dc5-155">取得說明</span><span class="sxs-lookup"><span data-stu-id="f6dc5-155">Get help</span></span>

<span data-ttu-id="f6dc5-156">tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="f6dc5-157">toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。</span><span class="sxs-lookup"><span data-stu-id="f6dc5-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6dc5-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6dc5-158">Next steps</span></span>

- <span data-ttu-id="f6dc5-159">[Tooon 內部部署資料連接](../logic-apps/logic-apps-gateway-connection.md)從邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f6dc5-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="f6dc5-160">了解[企業整合](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f6dc5-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
