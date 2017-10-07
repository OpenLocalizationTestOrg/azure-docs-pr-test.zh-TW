---
title: "aaaConnect tooan 內部 Azure 邏輯應用程式中的 SAP 系統 |Microsoft 文件"
description: "Tooan 在內部部署 SAP 系統連接與邏輯應用程式工作流程透過 hello 在內部部署資料閘道"
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
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="1acf9-103">從邏輯應用程式與 hello SAP 連接器連接 tooan 在內部部署 SAP 系統</span><span class="sxs-lookup"><span data-stu-id="1acf9-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="1acf9-104">hello 在內部部署資料閘道可讓您 toomanage 資料，並安全地存取內部部署的資源。</span><span class="sxs-lookup"><span data-stu-id="1acf9-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="1acf9-105">本主題說明如何連接邏輯應用程式 tooan 在內部部署 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="1acf9-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="1acf9-106">在此範例中，邏輯應用程式會透過 HTTP 要求 IDOC，並將傳送 hello 回應傳回。</span><span class="sxs-lookup"><span data-stu-id="1acf9-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="1acf9-107">目前限制：</span><span class="sxs-lookup"><span data-stu-id="1acf9-107">Current limitations:</span></span> 
> - <span data-ttu-id="1acf9-108">邏輯應用程式逾時，如果 hello 回應所需的所有步驟不 hello 內都完成[要求逾時限制](./logic-apps-limits-and-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1acf9-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="1acf9-109">在此情況下，可能會封鎖要求。</span><span class="sxs-lookup"><span data-stu-id="1acf9-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="1acf9-110">hello 檔案選擇器不會顯示所有的 hello 可用的欄位。</span><span class="sxs-lookup"><span data-stu-id="1acf9-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="1acf9-111">在此案例中，您可以手動新增路徑。</span><span class="sxs-lookup"><span data-stu-id="1acf9-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1acf9-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="1acf9-112">Prerequisites</span></span>

- <span data-ttu-id="1acf9-113">安裝及最新設定 hello[在內部部署資料閘道](https://www.microsoft.com/download/details.aspx?id=53127)1.15.6150.1 版本或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1acf9-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="1acf9-114">[如何 tooconnect toohello 內部部署資料閘道，在邏輯應用程式中](http://aka.ms/logicapps-gateway)清單 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="1acf9-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="1acf9-115">您可以繼續之前，必須安裝 hello 閘道在內部部署電腦上。</span><span class="sxs-lookup"><span data-stu-id="1acf9-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="1acf9-116">下載並安裝 hello 最新 SAP 用戶端程式庫上 hello 相同機器 hello 資料閘道的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="1acf9-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="1acf9-117">使用任何下列 SAP 版本 hello:</span><span class="sxs-lookup"><span data-stu-id="1acf9-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="1acf9-118">SAP 伺服器</span><span class="sxs-lookup"><span data-stu-id="1acf9-118">SAP Server</span></span>
        - <span data-ttu-id="1acf9-119">任何 SAP 伺服器的支援 hello.NET 連接器 (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="1acf9-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="1acf9-120">SAP 用戶端</span><span class="sxs-lookup"><span data-stu-id="1acf9-120">SAP Client</span></span>
        - <span data-ttu-id="1acf9-121">SAP.NET 連接器 (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="1acf9-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="1acf9-122">加入觸發程序和連接 tooyour SAP 系統的動作</span><span class="sxs-lookup"><span data-stu-id="1acf9-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="1acf9-123">hello SAP 連接器具有的動作，但未觸發程序。</span><span class="sxs-lookup"><span data-stu-id="1acf9-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="1acf9-124">因此，我們有 toouse 另一個觸發程序在 hello hello 工作流程的開頭。</span><span class="sxs-lookup"><span data-stu-id="1acf9-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="1acf9-125">加入 hello 要求/回應觸發程序，然後選取**新步驟**。</span><span class="sxs-lookup"><span data-stu-id="1acf9-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="1acf9-126">選取**將動作加入**，然後輸入選取 hello SAP 連接器`SAP`hello [搜尋] 欄位中：</span><span class="sxs-lookup"><span data-stu-id="1acf9-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![選取 SAP 應用程式伺服器或 SAP 訊息伺服器](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="1acf9-128">選取 [**SAP 應用程式伺服器**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server)或 [**SAP 訊息伺服器**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm)，這取決於您的 SAP 設定。</span><span class="sxs-lookup"><span data-stu-id="1acf9-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="1acf9-129">如果您沒有現有的連接，您必須提示的 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="1acf9-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="1acf9-130">選取**連接透過內部部署資料閘道**，並輸入您的 SAP 系統的 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="1acf9-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![加入連接字串 tooSAP](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="1acf9-132">在下**閘道**、 選取現有的閘道或新的閘道 tooinstall、 選取**安裝閘道**。</span><span class="sxs-lookup"><span data-stu-id="1acf9-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![安裝新的閘道](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="1acf9-134">您輸入所有 hello 詳細資料之後，請選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="1acf9-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="1acf9-135">邏輯應用程式設定，並測試 hello 連線，並確定 hello 連線正常運作。</span><span class="sxs-lookup"><span data-stu-id="1acf9-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="1acf9-136">輸入 SAP 連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="1acf9-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="1acf9-137">現在可以使用 hello 不同 SAP 選項。</span><span class="sxs-lookup"><span data-stu-id="1acf9-137">hello different SAP options are now available.</span></span> <span data-ttu-id="1acf9-138">toofind IDOC 分類，則請從 hello 清單中選取。</span><span class="sxs-lookup"><span data-stu-id="1acf9-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="1acf9-139">或以手動方式輸入 hello 路徑中的和選取 hello HTTP 回應 hello**主體**欄位：</span><span class="sxs-lookup"><span data-stu-id="1acf9-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![SAP 動作](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="1acf9-141">加入建立 hello 動作**HTTP 回應**。</span><span class="sxs-lookup"><span data-stu-id="1acf9-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="1acf9-142">hello 回應訊息應該從 hello SAP 輸出。</span><span class="sxs-lookup"><span data-stu-id="1acf9-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="1acf9-143">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="1acf9-143">Save your logic app.</span></span> <span data-ttu-id="1acf9-144">傳送 IDOC 透過 hello HTTP 觸發程序 URL 來測試它。</span><span class="sxs-lookup"><span data-stu-id="1acf9-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="1acf9-145">Hello 傳送 IDOC 之後, 等候 hello 回應 hello 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="1acf9-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="1acf9-146">如何查看太[監視您的 Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="1acf9-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="1acf9-147">既然 hello SAP 連接器加入 tooyour 邏輯應用程式，開始探索其他功能：</span><span class="sxs-lookup"><span data-stu-id="1acf9-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="1acf9-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="1acf9-148">BAPI</span></span>
- <span data-ttu-id="1acf9-149">RFC</span><span class="sxs-lookup"><span data-stu-id="1acf9-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="1acf9-150">取得說明</span><span class="sxs-lookup"><span data-stu-id="1acf9-150">Get help</span></span>

<span data-ttu-id="1acf9-151">tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="1acf9-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1acf9-152">toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。</span><span class="sxs-lookup"><span data-stu-id="1acf9-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1acf9-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1acf9-153">Next steps</span></span>

- <span data-ttu-id="1acf9-154">深入了解如何 toovalidate、 轉換和其他 BizTalk 類似函式，在 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1acf9-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="1acf9-155">[Tooon 內部部署資料連接](../logic-apps/logic-apps-gateway-connection.md)從邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="1acf9-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
