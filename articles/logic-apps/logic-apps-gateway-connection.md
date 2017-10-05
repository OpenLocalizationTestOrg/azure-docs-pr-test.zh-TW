---
title: "存取 Azure Logic Apps 的內部部署資料來源 | Microsoft Docs"
description: "設定內部部署資料閘道，以便從邏輯應用程式存取內部部署資料來源"
keywords: "存取資料, 內部部署, 資料傳輸, 加密, 資料來源"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a><span data-ttu-id="8ab40-104">使用內部部署資料閘道從邏輯應用程式存取內部部署資料來源</span><span class="sxs-lookup"><span data-stu-id="8ab40-104">Access data sources on premises from logic apps with the on-premises data gateway</span></span>

<span data-ttu-id="8ab40-105">若要從邏輯應用程式存取內部部署資料來源，請使用支援的連接器來設定可供邏輯應用程式使用的內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="8ab40-105">To access data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="8ab40-106">此閘道可作為橋樑，讓內部部署資料來源與邏輯應用程式之間快速地傳輸和加密資料。</span><span class="sxs-lookup"><span data-stu-id="8ab40-106">The gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="8ab40-107">閘道會在加密通道上經過 Azure 服務匯流排轉送來自內部部署來源的資料。</span><span class="sxs-lookup"><span data-stu-id="8ab40-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="8ab40-108">源自閘道代理程式的所有流量都是安全輸出流量。</span><span class="sxs-lookup"><span data-stu-id="8ab40-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="8ab40-109">深入了解[資料閘道的運作方式](logic-apps-gateway-install.md#gateway-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="8ab40-109">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="8ab40-110">閘道可連線到下列內部部署資料來源︰</span><span class="sxs-lookup"><span data-stu-id="8ab40-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="8ab40-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="8ab40-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="8ab40-112">DB2</span><span class="sxs-lookup"><span data-stu-id="8ab40-112">DB2</span></span>  
*   <span data-ttu-id="8ab40-113">檔案系統</span><span class="sxs-lookup"><span data-stu-id="8ab40-113">File System</span></span>
*   <span data-ttu-id="8ab40-114">Informix</span><span class="sxs-lookup"><span data-stu-id="8ab40-114">Informix</span></span>
*   <span data-ttu-id="8ab40-115">MQ</span><span class="sxs-lookup"><span data-stu-id="8ab40-115">MQ</span></span>
*   <span data-ttu-id="8ab40-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="8ab40-116">MySQL</span></span>
*   <span data-ttu-id="8ab40-117">Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="8ab40-117">Oracle Database</span></span>
*   <span data-ttu-id="8ab40-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8ab40-118">PostgreSQL</span></span>
*   <span data-ttu-id="8ab40-119">SAP 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="8ab40-119">SAP Application Server</span></span> 
*   <span data-ttu-id="8ab40-120">SAP 訊息伺服器</span><span class="sxs-lookup"><span data-stu-id="8ab40-120">SAP Message Server</span></span>
*   <span data-ttu-id="8ab40-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="8ab40-121">SharePoint</span></span>
*   <span data-ttu-id="8ab40-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8ab40-122">SQL Server</span></span>
*   <span data-ttu-id="8ab40-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="8ab40-123">Teradata</span></span>

<span data-ttu-id="8ab40-124">下列步驟示範如何設定內部部署資料閘道，使其與邏輯應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="8ab40-124">These steps show how to set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="8ab40-125">如需所支援連接器的詳細資訊，請參閱 [Azure Logic Apps 的連接器](../connectors/apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab40-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="8ab40-126">如需如何使用閘道與其他服務的資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="8ab40-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="8ab40-127">Microsoft Power BI 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="8ab40-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="8ab40-128">Azure Analysis Services 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="8ab40-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="8ab40-129">Microsoft Flow 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="8ab40-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="8ab40-130">Microsoft PowerApps 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="8ab40-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="8ab40-131">需求</span><span class="sxs-lookup"><span data-stu-id="8ab40-131">Requirements</span></span>

* <span data-ttu-id="8ab40-132">您必須[已在本機電腦上安裝資料閘道](logic-apps-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab40-132">You must have already [installed the data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="8ab40-133">登入 Azure 入口網站時，您必須使用之前用來[安裝內部部署資料閘道](logic-apps-gateway-install.md#requirements)的同一個公司或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ab40-133">When you sign in to the Azure portal, you have to use the same work or school account that was used to [install the on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="8ab40-134">為閘道安裝在 Azure 入口網站建立閘道資源時，登入的帳戶也必須擁有 Azure 訂用帳戶以供使用。</span><span class="sxs-lookup"><span data-stu-id="8ab40-134">Your sign-in account must also have an Azure subscription to use when you create a gateway resource in the Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="8ab40-135">您的閘道安裝不能已由 Azure 閘道資源加以宣告。</span><span class="sxs-lookup"><span data-stu-id="8ab40-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="8ab40-136">您只能將閘道安裝關聯至一個 Azure 閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8ab40-136">You can associate your gateway installation to only one Azure gateway resource.</span></span> <span data-ttu-id="8ab40-137">當您建立閘道資源時便已完成宣告，因此該安裝無法再供其他資源使用。</span><span class="sxs-lookup"><span data-stu-id="8ab40-137">Claim happens when you create the gateway resource so that the installation is unavailable for other resources.</span></span>

## <a name="set-up-the-data-gateway-connection"></a><span data-ttu-id="8ab40-138">設定資料閘道連線</span><span class="sxs-lookup"><span data-stu-id="8ab40-138">Set up the data gateway connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="8ab40-139">1.安裝內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="8ab40-139">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="8ab40-140">如果您還沒有這麼做，請依照[步驟來安裝內部部署資料閘道](logic-apps-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab40-140">If you haven't already, follow the [steps to install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="8ab40-141">在繼續進行其他步驟前，請先確定您已在本機電腦上安裝資料閘道。</span><span class="sxs-lookup"><span data-stu-id="8ab40-141">Before you continue with the other steps, make sure that you installed the data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a><span data-ttu-id="8ab40-142">2.建立內部部署資料閘道的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="8ab40-142">2. Create an Azure resource for the on-premises data gateway</span></span>

<span data-ttu-id="8ab40-143">在本機電腦上安裝閘道之後，您必須將資料閘道建立為 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="8ab40-143">After you install the gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="8ab40-144">此步驟也會讓閘道資源與 Azure 訂用帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="8ab40-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="8ab40-145">登入 [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="8ab40-145">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="8ab40-146">請務必使用您在安裝閘道時所使用的同一個 Azure 公司或學校電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8ab40-146">Make sure to use the same Azure work or school email address used to install the gateway.</span></span>

2. <span data-ttu-id="8ab40-147">在 Azure 的左側功能表中，選擇 [新增] > [企業整合] > [內部部署資料閘道]，如以下所示︰</span><span class="sxs-lookup"><span data-stu-id="8ab40-147">On the left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![尋找 [內部部署資料閘道]](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="8ab40-149">在 [建立連線閘道] 刀鋒視窗中，提供下列詳細資料以建立資料閘道資源︰</span><span class="sxs-lookup"><span data-stu-id="8ab40-149">On the **Create connection gateway** blade, provide these details to create your data gateway resource:</span></span>

    * <span data-ttu-id="8ab40-150">**名稱**：輸入閘道資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="8ab40-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="8ab40-151">**訂用帳戶**︰選取要與閘道資源關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ab40-151">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="8ab40-152">此訂用帳戶必須是和邏輯應用程式相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ab40-152">This subscription should be the same subscription as your logic app.</span></span>
   
      <span data-ttu-id="8ab40-153">預設的訂用帳戶會由您用來登入的 Azure 帳戶來決定。</span><span class="sxs-lookup"><span data-stu-id="8ab40-153">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="8ab40-154">**資源群組**：建立資源群組或選取現有資源群組來部署閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8ab40-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="8ab40-155">資源群組可協助您集合管理相關的 Azure 資產。</span><span class="sxs-lookup"><span data-stu-id="8ab40-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="8ab40-156">**位置**：Azure 對此位置有所限制，它的所在區域必須和[閘道安裝](logic-apps-gateway-install.md)期間為閘道雲端服務所選取的區域相同。</span><span class="sxs-lookup"><span data-stu-id="8ab40-156">**Location**: Azure restricts this location to the same region that was selected for the gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="8ab40-157">請確定閘道資源位置符合閘道雲端服務的位置。</span><span class="sxs-lookup"><span data-stu-id="8ab40-157">Make sure that the gateway resource location matches the gateway cloud service location.</span></span> <span data-ttu-id="8ab40-158">否則，已安裝的閘道清單中可能不會出現您的閘道安裝，從而供您在下一個步驟中選取。</span><span class="sxs-lookup"><span data-stu-id="8ab40-158">Otherwise, your gateway installation might not appear in the installed gateways list for you to select in the next step.</span></span>
      > 
      > <span data-ttu-id="8ab40-159">閘道資源和邏輯應用程式可使用不同的區域。</span><span class="sxs-lookup"><span data-stu-id="8ab40-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="8ab40-160">**安裝名稱**︰如果您的閘道安裝還不是選取狀態，請選取您先前安裝的閘道。</span><span class="sxs-lookup"><span data-stu-id="8ab40-160">**Installation Name**: If your gateway installation isn't already selected, select the gateway that you previously installed.</span></span> 

    <span data-ttu-id="8ab40-161">若要在 Azure 儀表板中新增閘道資源，請選擇 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-161">To add the gateway resource to your Azure dashboard, choose **Pin to dashboard**.</span></span> 
    <span data-ttu-id="8ab40-162">完成之後，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="8ab40-163">例如：</span><span class="sxs-lookup"><span data-stu-id="8ab40-163">For example:</span></span>

    ![提供詳細資料以建立內部部署資料閘道](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="8ab40-165">任何時候若想尋找或檢視資料閘道，請從主要的 Azure 左側功能表，移至 [更多服務]> [企業整合]> [內部部署資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-165">To find or view your data gateway at any time,  from the main Azure left menu, go to  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![移至 [更多服務] > [企業整合] > [內部部署資料閘道]](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a><span data-ttu-id="8ab40-167">3.將邏輯應用程式連線到內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="8ab40-167">3. Connect your logic app to the on-premises data gateway</span></span>

<span data-ttu-id="8ab40-168">您已建立資料閘道資源並讓 Azure 訂用帳戶與該資源相關聯，接下來請建立邏輯應用程式與資料閘道之間的連線。</span><span class="sxs-lookup"><span data-stu-id="8ab40-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and the data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="8ab40-169">閘道連線位置必須和邏輯應用程式位於相同區域，但您可以使用位於不同區域的資料閘道。</span><span class="sxs-lookup"><span data-stu-id="8ab40-169">Your gateway connection location must exist in the same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="8ab40-170">在 Azure 入口網站中，於邏輯應用程式設計工具中建立或開啟邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ab40-170">In the Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="8ab40-171">新增支援內部部署連線的連接器 (例如 SQL Server)。</span><span class="sxs-lookup"><span data-stu-id="8ab40-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="8ab40-172">按照所示順序，選取 [透過內部部署資料閘道連線]、提供唯一的連線名稱和必要資訊，然後選取您要使用的資料閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8ab40-172">Following the order shown, select **Connect via on-premises data gateway**, provide a unique connection name and the required information, and select the data gateway resource that you want to use.</span></span> <span data-ttu-id="8ab40-173">完成之後，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="8ab40-174">唯一的連線名稱可在之後協助您輕鬆識別該連線，尤其是當您建立了多個連線時。</span><span class="sxs-lookup"><span data-stu-id="8ab40-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="8ab40-175">如果情況允許，也請在使用者名稱中包含完整網域。</span><span class="sxs-lookup"><span data-stu-id="8ab40-175">If applicable, also include the qualified domain for your username.</span></span> 

   ![建立邏輯應用程式與資料閘道之間的連線](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="8ab40-177">恭喜，閘道連線現已可供邏輯應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="8ab40-177">Congratulations, your gateway connection is now ready for your logic app to use.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="8ab40-178">編輯閘道連線設定</span><span class="sxs-lookup"><span data-stu-id="8ab40-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="8ab40-179">在為邏輯應用程式建立閘道連線之後，您之後或許會想更新該特定連線的設定。</span><span class="sxs-lookup"><span data-stu-id="8ab40-179">After you create a gateway connection for your logic app, you might want to later update the settings for that specific connection.</span></span>

1. <span data-ttu-id="8ab40-180">若要尋找閘道連線︰</span><span class="sxs-lookup"><span data-stu-id="8ab40-180">To find the gateway connection:</span></span>

   * <span data-ttu-id="8ab40-181">在邏輯應用程式刀鋒視窗的 [開發工具] 下，選取 [API 連線]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-181">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="8ab40-182">[API 連線] 窗格會顯示與邏輯應用程式相關聯的所有 API 連線，包括閘道連線。</span><span class="sxs-lookup"><span data-stu-id="8ab40-182">The **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![移至邏輯應用程式，選取 [API 連線]](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="8ab40-184">或者，從主要的 Azure 左側功能表中，移至 [更多服務]> [Web 和行動服務]> [API 連線]，來找到與 Azure 訂用帳戶相關聯的所有 API 連線，包括閘道連線。</span><span class="sxs-lookup"><span data-stu-id="8ab40-184">Or, from the main Azure left menu, go to **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="8ab40-185">或者，在主要的 Azure 左側功能表中，移至 [所有資源]，來找到與 Azure 訂用帳戶相關聯的所有 API 連線，包括閘道連線。</span><span class="sxs-lookup"><span data-stu-id="8ab40-185">Or, on the main Azure left menu, go to **All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="8ab40-186">選取您要檢視或編輯的閘道連線，然後選擇 [編輯 API 連線]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-186">Select the gateway connection that you want to view or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="8ab40-187">如果您的更新未生效，請嘗試[先停止再重新啟動閘道 Windows 服務](./logic-apps-gateway-install.md#restart-gateway)。</span><span class="sxs-lookup"><span data-stu-id="8ab40-187">If your updates don't take effect, try [stopping and restarting the gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="8ab40-188">切換或刪除內部部署資料閘道資源</span><span class="sxs-lookup"><span data-stu-id="8ab40-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="8ab40-189">若要建立不同的閘道資源、讓閘道與其他資源相關連，或是要移除閘道資源，您可以直接刪除閘道資源，這並不會影響閘道安裝。</span><span class="sxs-lookup"><span data-stu-id="8ab40-189">To create a different gateway resource, associate your gateway with a different resource, or remove the gateway resource, you can delete the gateway resource without affecting the gateway installation.</span></span> 

1. <span data-ttu-id="8ab40-190">從主要的 Azure 左側功能表，移至 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-190">From the main Azure left menu, go to **All resources**.</span></span> 
2. <span data-ttu-id="8ab40-191">尋找並選取資料閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8ab40-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="8ab40-192">選擇 [內部部署資料閘道]，然後在 [資源] 工具列上選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="8ab40-192">Choose **On-premises Data Gateway**, and on the resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="8ab40-193">常見問題集</span><span class="sxs-lookup"><span data-stu-id="8ab40-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="8ab40-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ab40-194">Next steps</span></span>

* [<span data-ttu-id="8ab40-195">保護邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="8ab40-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="8ab40-196">Logic Apps 範例和常見案例</span><span class="sxs-lookup"><span data-stu-id="8ab40-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
