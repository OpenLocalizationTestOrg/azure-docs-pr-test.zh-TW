---
title: "在 Azure 邏輯應用程式的內部部署 aaaAccess 資料來源 |Microsoft 文件"
description: "設定 hello 在內部部署資料閘道，讓您可以從邏輯應用程式存取內部部署資料來源"
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
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="57c7a-104">在從邏輯應用程式使用 hello 在內部部署資料閘道的內部部署存取資料來源</span><span class="sxs-lookup"><span data-stu-id="57c7a-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="57c7a-105">在您的 logic apps，從內部部署 tooaccess 資料來源設定邏輯應用程式可以使用支援的連接器的內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="57c7a-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="57c7a-106">hello gateway 是做為提供快速的資料傳輸和加密您的 logic apps 在內部部署資料來源之間的橋樑。</span><span class="sxs-lookup"><span data-stu-id="57c7a-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="57c7a-107">hello 閘道轉送上 hello Azure Service Bus 透過加密通道在內部部署來源的資料。</span><span class="sxs-lookup"><span data-stu-id="57c7a-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="57c7a-108">所有流量都來自為 hello 閘道代理程式的安全輸出流量。</span><span class="sxs-lookup"><span data-stu-id="57c7a-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="57c7a-109">深入了解[hello 資料閘道的運作方式](logic-apps-gateway-install.md#gateway-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="57c7a-110">hello 閘道支援連線 toothese 資料來源，在內部部署：</span><span class="sxs-lookup"><span data-stu-id="57c7a-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="57c7a-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="57c7a-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="57c7a-112">DB2</span><span class="sxs-lookup"><span data-stu-id="57c7a-112">DB2</span></span>  
*   <span data-ttu-id="57c7a-113">檔案系統</span><span class="sxs-lookup"><span data-stu-id="57c7a-113">File System</span></span>
*   <span data-ttu-id="57c7a-114">Informix</span><span class="sxs-lookup"><span data-stu-id="57c7a-114">Informix</span></span>
*   <span data-ttu-id="57c7a-115">MQ</span><span class="sxs-lookup"><span data-stu-id="57c7a-115">MQ</span></span>
*   <span data-ttu-id="57c7a-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="57c7a-116">MySQL</span></span>
*   <span data-ttu-id="57c7a-117">Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="57c7a-117">Oracle Database</span></span>
*   <span data-ttu-id="57c7a-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="57c7a-118">PostgreSQL</span></span>
*   <span data-ttu-id="57c7a-119">SAP 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="57c7a-119">SAP Application Server</span></span> 
*   <span data-ttu-id="57c7a-120">SAP 訊息伺服器</span><span class="sxs-lookup"><span data-stu-id="57c7a-120">SAP Message Server</span></span>
*   <span data-ttu-id="57c7a-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="57c7a-121">SharePoint</span></span>
*   <span data-ttu-id="57c7a-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="57c7a-122">SQL Server</span></span>
*   <span data-ttu-id="57c7a-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="57c7a-123">Teradata</span></span>

<span data-ttu-id="57c7a-124">這些步驟顯示如何 tooset hello 註冊內部部署資料閘道 toowork 隨應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="57c7a-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="57c7a-125">如需所支援連接器的詳細資訊，請參閱 [Azure Logic Apps 的連接器](../connectors/apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="57c7a-126">如需如何 toouse hello 閘道與其他服務資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="57c7a-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="57c7a-127">Microsoft Power BI 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="57c7a-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="57c7a-128">Azure Analysis Services 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="57c7a-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="57c7a-129">Microsoft Flow 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="57c7a-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="57c7a-130">Microsoft PowerApps 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="57c7a-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="57c7a-131">需求</span><span class="sxs-lookup"><span data-stu-id="57c7a-131">Requirements</span></span>

* <span data-ttu-id="57c7a-132">您必須已經[hello 資料閘道安裝在本機電腦上](logic-apps-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="57c7a-133">當您登入 toohello Azure 入口網站時，您可以 toouse hello 相同的工作或學校帳戶，使用了太[安裝 hello 在內部部署資料閘道](logic-apps-gateway-install.md#requirements)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="57c7a-134">Hello Azure 入口網站中建立的閘道安裝閘道資源時，您登入的帳戶也必須具有 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="57c7a-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="57c7a-135">您的閘道安裝不能已由 Azure 閘道資源加以宣告。</span><span class="sxs-lookup"><span data-stu-id="57c7a-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="57c7a-136">您可以將閘道安裝 tooonly 一個 Azure 閘道資源產生關聯。</span><span class="sxs-lookup"><span data-stu-id="57c7a-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="57c7a-137">當您建立 hello 閘道資源以便 hello 安裝不適用於其他資源時，就會發生宣告。</span><span class="sxs-lookup"><span data-stu-id="57c7a-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="57c7a-138">Hello 資料閘道連接設定</span><span class="sxs-lookup"><span data-stu-id="57c7a-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="57c7a-139">1.安裝 hello 在內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="57c7a-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="57c7a-140">如果您還沒有這麼做，請遵循 hello[步驟 tooinstall hello 在內部部署資料閘道](logic-apps-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="57c7a-141">在繼續 hello 之前的其他步驟，請確定您在本機電腦上安裝 hello 資料閘道。</span><span class="sxs-lookup"><span data-stu-id="57c7a-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="57c7a-142">2.建立 hello 在內部部署資料閘道的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="57c7a-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="57c7a-143">您在本機電腦上安裝 hello 閘道之後，您必須建立您的 data gateway 為 Azure 中的資源。</span><span class="sxs-lookup"><span data-stu-id="57c7a-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="57c7a-144">此步驟也會讓閘道資源與 Azure 訂用帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="57c7a-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="57c7a-145">登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="57c7a-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="57c7a-146">請確定 toouse hello 相同的 Azure 工作或學校電子郵件地址使用 tooinstall hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="57c7a-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="57c7a-147">在 Azure 中的 hello 左功能表中選擇**新增** > **企業整合** > **在內部部署資料閘道**如下所示：</span><span class="sxs-lookup"><span data-stu-id="57c7a-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![尋找 [內部部署資料閘道]](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="57c7a-149">在 hello**建立連接閘道**刀鋒視窗中，提供這些詳細資料 toocreate 您的資料閘道資源：</span><span class="sxs-lookup"><span data-stu-id="57c7a-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="57c7a-150">**名稱**：輸入閘道資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="57c7a-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="57c7a-151">**訂用帳戶**： 選取 hello Azure 訂用帳戶 tooassociate 與閘道資源。</span><span class="sxs-lookup"><span data-stu-id="57c7a-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="57c7a-152">此訂用帳戶應為 hello 邏輯應用程式相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="57c7a-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="57c7a-153">hello 預設訂用帳戶根據 hello 用 toosign 中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57c7a-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="57c7a-154">**資源群組**：建立資源群組或選取現有資源群組來部署閘道資源。</span><span class="sxs-lookup"><span data-stu-id="57c7a-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="57c7a-155">資源群組可協助您集合管理相關的 Azure 資產。</span><span class="sxs-lookup"><span data-stu-id="57c7a-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="57c7a-156">**位置**: Azure 限制此位置 toohello hello 閘道器雲端服務時所選取的相同區域[閘道安裝](logic-apps-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="57c7a-157">請確定 hello 閘道資源位置符合 hello 閘道雲端服務的位置。</span><span class="sxs-lookup"><span data-stu-id="57c7a-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="57c7a-158">否則，閘道安裝可能不會出現在您 tooselect hello 安裝閘道的清單中 hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="57c7a-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="57c7a-159">閘道資源和邏輯應用程式可使用不同的區域。</span><span class="sxs-lookup"><span data-stu-id="57c7a-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="57c7a-160">**安裝名稱**： 如果尚未選取閘道安裝，請選取您先前安裝的 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="57c7a-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="57c7a-161">tooadd hello 閘道資源 tooyour Azure 儀表板中，選擇**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="57c7a-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="57c7a-162">完成之後，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="57c7a-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="57c7a-163">例如：</span><span class="sxs-lookup"><span data-stu-id="57c7a-163">For example:</span></span>

    ![提供詳細資料 toocreate 您的內部部署資料閘道](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="57c7a-165">您的 data gateway，任何時候 hello 主要 Azure 左窗格中，從 toofind 或檢視表太移**更服務** > **企業整合** > **在內部部署資料閘道**。</span><span class="sxs-lookup"><span data-stu-id="57c7a-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![移太 「 多個服務 」，「 企業整合 」，「 內部部署資料閘道 」](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="57c7a-167">3.連接邏輯應用程式 toohello 在內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="57c7a-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="57c7a-168">現在您已建立您的資料閘道資源，並與該資源相關聯 Azure 訂用帳戶，建立邏輯應用程式與 hello 資料閘道之間的連線。</span><span class="sxs-lookup"><span data-stu-id="57c7a-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="57c7a-169">閘道連線您的位置必須存在於 hello 相同區域，做為應用程式邏輯，但您可以使用存在的資料閘道位於不同的區域。</span><span class="sxs-lookup"><span data-stu-id="57c7a-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="57c7a-170">在 hello Azure 入口網站，建立或開啟邏輯應用程式邏輯應用程式的設計工具中。</span><span class="sxs-lookup"><span data-stu-id="57c7a-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="57c7a-171">新增支援內部部署連線的連接器 (例如 SQL Server)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="57c7a-172">遵循 hello 順序如下所示，選取**連接透過內部部署資料閘道**，提供唯一的連接名稱和 hello 必要的資訊，然後選取您想 toouse hello 資料閘道資源。</span><span class="sxs-lookup"><span data-stu-id="57c7a-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="57c7a-173">完成之後，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="57c7a-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="57c7a-174">唯一的連線名稱可在之後協助您輕鬆識別該連線，尤其是當您建立了多個連線時。</span><span class="sxs-lookup"><span data-stu-id="57c7a-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="57c7a-175">如果適用的話，也包含 hello 合格的網域使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="57c7a-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![建立邏輯應用程式與資料閘道之間的連線](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="57c7a-177">恭喜，您的閘道連線已準備好您的邏輯應用程式 toouse 進行。</span><span class="sxs-lookup"><span data-stu-id="57c7a-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="57c7a-178">編輯閘道連線設定</span><span class="sxs-lookup"><span data-stu-id="57c7a-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="57c7a-179">邏輯應用程式建立的閘道連接之後，您可能想 toolater 更新 hello 設定為該特定的連接。</span><span class="sxs-lookup"><span data-stu-id="57c7a-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="57c7a-180">toofind hello 閘道連線：</span><span class="sxs-lookup"><span data-stu-id="57c7a-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="57c7a-181">Hello 邏輯應用程式 刀鋒視窗，在**開發工具**，選取**API 連線**。</span><span class="sxs-lookup"><span data-stu-id="57c7a-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="57c7a-182">hello **API 連線** 窗格會顯示邏輯應用程式，包括閘道連線相關聯的所有應用程式開發介面連線。</span><span class="sxs-lookup"><span data-stu-id="57c7a-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![移 tooyour 邏輯應用程式中，選取 [API 連線]](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="57c7a-184">或從 hello 主要 Azure 左窗格中，移過**更服務** > **Web 和行動服務** > **API 連線**對於所有應用程式開發介面的連線，包括閘道連線，與您 Azure 訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="57c7a-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="57c7a-185">或在 hello 主要 Azure 左窗格中，移過**所有資源**對於所有應用程式開發介面的連線，包括您 Azure 訂用帳戶相關聯的閘道連線。</span><span class="sxs-lookup"><span data-stu-id="57c7a-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="57c7a-186">選取您想要 tooview 或編輯，並選擇 hello 閘道連接**編輯 API 連線**。</span><span class="sxs-lookup"><span data-stu-id="57c7a-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="57c7a-187">如果您的更新才會生效，請嘗試[停止並重新啟動 hello 閘道 Windows 服務](./logic-apps-gateway-install.md#restart-gateway)。</span><span class="sxs-lookup"><span data-stu-id="57c7a-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="57c7a-188">切換或刪除內部部署資料閘道資源</span><span class="sxs-lookup"><span data-stu-id="57c7a-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="57c7a-189">toocreate 不同閘道資源時，將您的閘道與不同的資源，建立關聯或移除 hello 閘道資源，您可以刪除 hello 閘道資源，而不會影響 hello 閘道安裝。</span><span class="sxs-lookup"><span data-stu-id="57c7a-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="57c7a-190">從 hello 主要 Azure 左窗格中，移過**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="57c7a-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="57c7a-191">尋找並選取資料閘道資源。</span><span class="sxs-lookup"><span data-stu-id="57c7a-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="57c7a-192">選擇**在內部部署資料閘道**，hello 資源在工具列上，選擇 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="57c7a-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="57c7a-193">常見問題集</span><span class="sxs-lookup"><span data-stu-id="57c7a-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="57c7a-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57c7a-194">Next steps</span></span>

* [<span data-ttu-id="57c7a-195">保護邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="57c7a-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="57c7a-196">Logic Apps 範例和常見案例</span><span class="sxs-lookup"><span data-stu-id="57c7a-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
