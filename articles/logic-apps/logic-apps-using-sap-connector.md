---
title: "連線到 Azure Logic Apps 中的內部部署 SAP 系統 | Microsoft Docs"
description: "透過內部部署資料閘道，連線到邏輯應用程式工作流程中的內部部署 SAP 系統"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="2bd1a-103">使用 SAP 連接器，從邏輯應用程式連線到內部部署 SAP 系統</span><span class="sxs-lookup"><span data-stu-id="2bd1a-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="2bd1a-104">內部部署資料閘道可讓您管理資料，並且安全地存取內部部署的資源。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="2bd1a-105">本主題示範如何將邏輯應用程式連線到內部部署 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="2bd1a-106">在此範例中，邏輯應用程式會透過 HTTP 要求 IDOC，並傳回回應。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="2bd1a-107">目前限制：</span><span class="sxs-lookup"><span data-stu-id="2bd1a-107">Current limitations:</span></span> 
> - <span data-ttu-id="2bd1a-108">如果回應所需的所有步驟未在[要求逾時限制](./logic-apps-limits-and-config.md)內完成，則邏輯應用程式會逾時。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="2bd1a-109">在此情況下，可能會封鎖要求。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="2bd1a-110">檔案選擇器不會顯示所有可用的欄位。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="2bd1a-111">在此案例中，您可以手動新增路徑。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bd1a-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="2bd1a-112">Prerequisites</span></span>

- <span data-ttu-id="2bd1a-113">安裝及設定最新的[內部部署資料閘道](https://www.microsoft.com/download/details.aspx?id=53127)版本 1.15.6150.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="2bd1a-114">[如何連接至邏輯應用程式中的內部部署資料閘道](http://aka.ms/logicapps-gateway)中有列出步驟。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="2bd1a-115">必須先在內部部署機器上安裝閘道，然後才能繼續。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="2bd1a-116">在您已安裝資料閘道的同一部電腦上，下載並安裝最新的 SAP 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="2bd1a-117">使用下列任一 SAP 版本：</span><span class="sxs-lookup"><span data-stu-id="2bd1a-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="2bd1a-118">SAP 伺服器</span><span class="sxs-lookup"><span data-stu-id="2bd1a-118">SAP Server</span></span>
        - <span data-ttu-id="2bd1a-119">任何支援 .NET 連接器 (NCo) 3.0 的 SAP 伺服器</span><span class="sxs-lookup"><span data-stu-id="2bd1a-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="2bd1a-120">SAP 用戶端</span><span class="sxs-lookup"><span data-stu-id="2bd1a-120">SAP Client</span></span>
        - <span data-ttu-id="2bd1a-121">SAP.NET 連接器 (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="2bd1a-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="2bd1a-122">新增用來連線到 SAP 系統的觸發程序和動作</span><span class="sxs-lookup"><span data-stu-id="2bd1a-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="2bd1a-123">SAP 連接器具有動作，但沒有觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="2bd1a-124">因此，我們需要在工作流程的開頭使用另一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="2bd1a-125">新增要求/回應觸發程序，然後選取 [新增步驟]。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="2bd1a-126">選取 [新增動作]，然後在搜尋欄位輸入 `SAP` 以選取 SAP 連接器：</span><span class="sxs-lookup"><span data-stu-id="2bd1a-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![選取 SAP 應用程式伺服器或 SAP 訊息伺服器](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="2bd1a-128">選取 [**SAP 應用程式伺服器**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server)或 [**SAP 訊息伺服器**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm)，這取決於您的 SAP 設定。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="2bd1a-129">如果您目前沒有連線，系統會提示您建立連線。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="2bd1a-130">選取 [透過內部部署資料閘道連接]，並輸入 SAP 系統的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="2bd1a-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![將連接字串新增到 SAP](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="2bd1a-132">在 [閘道] 下方，選取現有閘道，或者，若要安裝新的閘道，請選取 [安裝閘道]。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![安裝新的閘道](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="2bd1a-134">輸入所有詳細資料之後，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="2bd1a-135">Logic Apps 會設定並測試連線，以確定連線運作正常。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="2bd1a-136">輸入 SAP 連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="2bd1a-137">不同的 SAP 選項現已推出。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-137">The different SAP options are now available.</span></span> <span data-ttu-id="2bd1a-138">若要尋找 IDOC 類別，請從清單中進行選取。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="2bd1a-139">或者，以手動方式輸入路徑，並在 **body** 欄位中選取 HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="2bd1a-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![SAP 動作](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="2bd1a-141">新增用於建立 [HTTP 回應] 的動作。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="2bd1a-142">回應訊息應該都來自 SAP 輸出。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="2bd1a-143">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-143">Save your logic app.</span></span> <span data-ttu-id="2bd1a-144">透過 HTTP 觸發程序 URL 傳送 IDOC 加以測試。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="2bd1a-145">傳送 IDOC 之後，請等待邏輯應用程式的回應：</span><span class="sxs-lookup"><span data-stu-id="2bd1a-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="2bd1a-146">請查看如何[監視 Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="2bd1a-147">現在，SAP 連接器新增至邏輯應用程式，開始探索其他功能︰</span><span class="sxs-lookup"><span data-stu-id="2bd1a-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="2bd1a-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="2bd1a-148">BAPI</span></span>
- <span data-ttu-id="2bd1a-149">RFC</span><span class="sxs-lookup"><span data-stu-id="2bd1a-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="2bd1a-150">取得說明</span><span class="sxs-lookup"><span data-stu-id="2bd1a-150">Get help</span></span>

<span data-ttu-id="2bd1a-151">若要提出問題、回答問題以及了解其他 Azure Logic Apps 使用者的做法，請造訪 [Azure Logic Apps 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="2bd1a-152">若要改善 Azure Logic Apps 和連接器，請在 [Azure Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)上票選或提交想法。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bd1a-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2bd1a-153">Next steps</span></span>

- <span data-ttu-id="2bd1a-154">了解如何驗證、轉換及[企業整合套件](../logic-apps/logic-apps-enterprise-integration-overview.md)中其他與 BizTalk 類似的功能。</span><span class="sxs-lookup"><span data-stu-id="2bd1a-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="2bd1a-155">從邏輯應用程式[連線到內部部署資料](../logic-apps/logic-apps-gateway-connection.md)</span><span class="sxs-lookup"><span data-stu-id="2bd1a-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
