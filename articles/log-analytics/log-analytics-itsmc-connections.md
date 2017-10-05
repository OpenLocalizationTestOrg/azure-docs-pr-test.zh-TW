---
title: "OMS IT 服務管理連接器中的 ITSM 連線 | Microsoft Docs"
description: "將 OMS 中的 ITSM 產品/服務與 IT 服務管理連接器進行連線，並將 ITSM 工作項目集中監視及管理。"
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: e4f2e0a23aa52a0e02e7047916b77fb15107defa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a><span data-ttu-id="f47f6-103">將 ITSM 產品/服務與 IT 服務管理連接器進行連線 (預覽)</span><span class="sxs-lookup"><span data-stu-id="f47f6-103">Connect ITSM products/services with IT Service Management Connector (Preview)</span></span>
<span data-ttu-id="f47f6-104">本文章提供的資訊，是有關如何將 OMS 中的 ITSM 產品/服務連線至 IT 服務管理連接器，並將工作項目集中管理。</span><span class="sxs-lookup"><span data-stu-id="f47f6-104">This article provides information about how to connect your ITSM product/service to IT Service Management Connector in OMS and centrally manage your work items.</span></span> <span data-ttu-id="f47f6-105">如需有關 IT 服務管理連接器的詳細資訊，請參閱[概觀](log-analytics-itsmc-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-105">More information about IT Service Management Connector, see [Overview](log-analytics-itsmc-overview.md).</span></span>

<span data-ttu-id="f47f6-106">支援下列產品/服務：</span><span class="sxs-lookup"><span data-stu-id="f47f6-106">The following products/services are supported:</span></span>

- [<span data-ttu-id="f47f6-107">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="f47f6-107">System Center Service Manager</span></span>](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="f47f6-108">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="f47f6-108">ServiceNow</span></span>](#connect-servicenow-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="f47f6-109">Provance</span><span class="sxs-lookup"><span data-stu-id="f47f6-109">Provance</span></span>](#connect-provance-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="f47f6-110">Cherwell</span><span class="sxs-lookup"><span data-stu-id="f47f6-110">Cherwell</span></span>](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-to-it-service-management-connector-in-oms"></a><span data-ttu-id="f47f6-111">將 System Center Service Manager 連線到 OMS 中的 IT 服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="f47f6-111">Connect System Center Service Manager to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="f47f6-112">下列各節提供有關如何將 System Center Service Manager 產品連線到 OMS 中的 IT 服務管理連接器之詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f47f6-112">The following sections provide details about how to connect your System Center Service Manager product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f47f6-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="f47f6-113">Prerequisites</span></span>

<span data-ttu-id="f47f6-114">請確定您已符合這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="f47f6-114">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="f47f6-115">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="f47f6-115">IT Service Management Connector installed.</span></span>
<span data-ttu-id="f47f6-116">詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-116">More information:  [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="f47f6-117">已部署及設定 Service Manager Web 應用程式 (Web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-117">The Service Manager Web application (Web app) is deployed and configured.</span></span> <span data-ttu-id="f47f6-118">Web 應用程式的相關在[這裡](#create-and-deploy-service-manager-web-app-service)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-118">Information on Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
- <span data-ttu-id="f47f6-119">已建立及設定的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-119">Hybrid connection created and configured.</span></span> <span data-ttu-id="f47f6-120">詳細資訊︰[設定混合式連線](#configure-the-hybrid-connection)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-120">More information: [Configure the hybrid Connection](#configure-the-hybrid-connection).</span></span>
- <span data-ttu-id="f47f6-121">Service Manager 的支援版本：2012 R2 或 2016。</span><span class="sxs-lookup"><span data-stu-id="f47f6-121">Supported versions of Service Manager:  2012 R2 or 2016.</span></span>
- <span data-ttu-id="f47f6-122">使用者角色︰[進階操作員](https://technet.microsoft.com/library/ff461054.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-122">User role:  [Advanced operator](https://technet.microsoft.com/library/ff461054.aspx).</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="f47f6-123">連線程序</span><span class="sxs-lookup"><span data-stu-id="f47f6-123">Connection procedure</span></span>

<span data-ttu-id="f47f6-124">您可以使用下列程序，將 System Center Service Manager 執行個體連線到 IT 服務管理連接器：</span><span class="sxs-lookup"><span data-stu-id="f47f6-124">Use the following procedure to connect your System Center Service Manager instance to the IT Service Management Connector:</span></span>

1. <span data-ttu-id="f47f6-125">移至 [OMS] >[設定] > [連線的來源]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-125">Go to **OMS** >**Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="f47f6-126">選取**ITSM 連接器**，然後按一下 [新增新的連線]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-126">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![<span data-ttu-id="f47f6-127">Service Manager</span><span class="sxs-lookup"><span data-stu-id="f47f6-127">Service manager</span></span> ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. <span data-ttu-id="f47f6-128">提供下表中所述的資訊，然後按一下 [儲存] 來建立連線︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-128">Provide the information as described in the following table, and click **Save** to create the connection:</span></span>

> [!NOTE]
> <span data-ttu-id="f47f6-129">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-129">All these parameters are mandatory.</span></span>

| <span data-ttu-id="f47f6-130">**欄位**</span><span class="sxs-lookup"><span data-stu-id="f47f6-130">**Field**</span></span> | <span data-ttu-id="f47f6-131">**說明**</span><span class="sxs-lookup"><span data-stu-id="f47f6-131">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f47f6-132">**名稱**</span><span class="sxs-lookup"><span data-stu-id="f47f6-132">**Name**</span></span>   | <span data-ttu-id="f47f6-133">輸入您想要與 IT 服務管理連接器連線之 System Center Service Manager 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-133">Type a name for the System Center Service Manager instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-134">稍後當您設定這個執行個體的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-134">You use this name later when you configure work items in this instance/ view detailed log analytics.</span></span> |
| <span data-ttu-id="f47f6-135">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="f47f6-135">**Select Connection type**</span></span>   | <span data-ttu-id="f47f6-136">選取 **System Center Service Manager**。</span><span class="sxs-lookup"><span data-stu-id="f47f6-136">Select **System Center Service Manager**.</span></span> |
| <span data-ttu-id="f47f6-137">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="f47f6-137">**Server URL**</span></span>   | <span data-ttu-id="f47f6-138">輸入 Service Manager Web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="f47f6-138">Type the URL of the Service Manager Web app.</span></span> <span data-ttu-id="f47f6-139">Service Manager Web 應用程式的相關詳細資訊在[這裡](#create-and-deploy-service-manager-web-app-service)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-139">More information about Service Manager Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
| <span data-ttu-id="f47f6-140">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="f47f6-140">**Client ID**</span></span>   | <span data-ttu-id="f47f6-141">將您所產生 (使用自動指令碼) 用來驗證 Web 應用程式的用戶端識別碼輸入。</span><span class="sxs-lookup"><span data-stu-id="f47f6-141">Type the client ID that you generated (using the automatic script) for authenticating the Web app.</span></span> <span data-ttu-id="f47f6-142">自動化指令碼的相關詳細資訊在[這裡](log-analytics-itsmc-service-manager-script.md)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-142">More information about the automated script is [here.](log-analytics-itsmc-service-manager-script.md)</span></span>|
| <span data-ttu-id="f47f6-143">**用戶端祕密**</span><span class="sxs-lookup"><span data-stu-id="f47f6-143">**Client Secret**</span></span>   | <span data-ttu-id="f47f6-144">輸入針對此識別碼產生的用戶端祕密。</span><span class="sxs-lookup"><span data-stu-id="f47f6-144">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="f47f6-145">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="f47f6-145">**Data Sync Scope**</span></span>   | <span data-ttu-id="f47f6-146">選取您想要透過 IT 服務管理連接器同步的 Service Manager 工作項目。</span><span class="sxs-lookup"><span data-stu-id="f47f6-146">Select the Service Manager work items that you want to sync through the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-147">系統會將這些工作項目匯入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="f47f6-147">These work items are imported into Log Analytics.</span></span> <span data-ttu-id="f47f6-148">**選項︰**事件、變更要求。</span><span class="sxs-lookup"><span data-stu-id="f47f6-148">**Options:**  Incidents, Change Requests.</span></span>|
| <span data-ttu-id="f47f6-149">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="f47f6-149">**Sync Data**</span></span> | <span data-ttu-id="f47f6-150">輸入您想要起算資料的過去天數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-150">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="f47f6-151">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="f47f6-151">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="f47f6-152">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="f47f6-152">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="f47f6-153">如果您想要在 ITSM 產品中建立設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="f47f6-153">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="f47f6-154">選取時，OMS 會在支援的 ITSM 系統中建立受影響的 CI 作為設定項目 (如果 CI 不存在)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-154">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="f47f6-155">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="f47f6-155">**Default**: disabled.</span></span> |

<span data-ttu-id="f47f6-156">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-156">When successfully connected, and synced:</span></span>

- <span data-ttu-id="f47f6-157">從 Service Manager 選取的工作項目將匯入 OMS **Log Analytics。**</span><span class="sxs-lookup"><span data-stu-id="f47f6-157">Selected work items from Service Manager are imported into OMS **Log Analytics.**</span></span> <span data-ttu-id="f47f6-158">您可以在 [IT 服務管理連接器] 圖格上檢視這些工作項目的摘要。</span><span class="sxs-lookup"><span data-stu-id="f47f6-158">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>

- <span data-ttu-id="f47f6-159">您可以從 OMS 建立這個 Service Manager 執行個體中的 OMS 警示或記錄搜尋事件。</span><span class="sxs-lookup"><span data-stu-id="f47f6-159">From OMS, you can create incidents from OMS alerts or from log search, in this Service Manager instance.</span></span>

<span data-ttu-id="f47f6-160">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-160">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-and-deploy-service-manager-web-app-service"></a><span data-ttu-id="f47f6-161">建立及部署 Service Manager Web 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="f47f6-161">Create and deploy Service Manager web app service</span></span>

<span data-ttu-id="f47f6-162">為了將內部部署 Service Manager 與 OMS 上的 IT 服務管理連接器連線，Microsoft 已在 GitHub 上建立 Service Manager Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f47f6-162">To connect the on-premises Service Manager with the IT Service Management Connector on OMS, Microsoft has created a Service Manager Web app on the GitHub.</span></span>

<span data-ttu-id="f47f6-163">若要為您的 Service Manager 設定 ITSM Web 應用程式，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-163">To set up the ITSM Web app for your Service Manager, do the following:</span></span>

- <span data-ttu-id="f47f6-164">**部署 Web 應用程式** – 部署 Web 應用程式、設定屬性，以及驗證 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="f47f6-164">**Deploy the Web app** – Deploy the Web app, set the properties, and authenticate with Azure AD.</span></span> <span data-ttu-id="f47f6-165">您可以使用 Microsoft 所提供給您的[自動化指令碼](log-analytics-itsmc-service-manager-script.md)來部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f47f6-165">You can deploy the web app by using the [automated script](log-analytics-itsmc-service-manager-script.md) that Microsoft has provided you.</span></span>
- <span data-ttu-id="f47f6-166">**設定混合式連線** - [以手動方式設定此連線](#configure-the-hybrid-connection)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-166">**Configure the hybrid connection** - [Configure this connection](#configure-the-hybrid-connection), manually.</span></span>

#### <a name="deploy-the-web-app"></a><span data-ttu-id="f47f6-167">部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f47f6-167">Deploy the web app</span></span>
<span data-ttu-id="f47f6-168">使用自動化[指令碼](log-analytics-itsmc-service-manager-script.md)來部署 Web 應用程式、設定屬性，以及驗證 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="f47f6-168">Use the automated [script](log-analytics-itsmc-service-manager-script.md) to deploy the Web app, set the properties, and authenticate with Azure AD.</span></span>

<span data-ttu-id="f47f6-169">提供下列必要的詳細資料來執行指令碼︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-169">Run the script by providing the following required details:</span></span>

- <span data-ttu-id="f47f6-170">Azure 訂用帳戶詳細資料</span><span class="sxs-lookup"><span data-stu-id="f47f6-170">Azure subscription details</span></span>
- <span data-ttu-id="f47f6-171">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="f47f6-171">Resource group name</span></span>
- <span data-ttu-id="f47f6-172">位置</span><span class="sxs-lookup"><span data-stu-id="f47f6-172">Location</span></span>
- <span data-ttu-id="f47f6-173">Service Manager 伺服器詳細資料 (伺服器名稱、網域、使用者名稱和密碼)</span><span class="sxs-lookup"><span data-stu-id="f47f6-173">Service Manager server details (server name, domain, user name, and password)</span></span>
- <span data-ttu-id="f47f6-174">Web 應用程式的網站名稱前置詞</span><span class="sxs-lookup"><span data-stu-id="f47f6-174">Site name prefix for your Web app</span></span>
- <span data-ttu-id="f47f6-175">服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="f47f6-175">ServiceBus Namespace.</span></span>

<span data-ttu-id="f47f6-176">指令碼會使用您指定的名稱 (與其他可使它成為唯一的字串) 來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f47f6-176">The script creates the Web app using the name that you specified (along with few additional strings to make it unique).</span></span> <span data-ttu-id="f47f6-177">它會產生 **Web 應用程式 URL**、**用戶端識別碼**和**用戶端祕密**。</span><span class="sxs-lookup"><span data-stu-id="f47f6-177">It generates the **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="f47f6-178">將值儲存，當您使用 IT 服務管理連接器建立連線時會用到這些值。</span><span class="sxs-lookup"><span data-stu-id="f47f6-178">Save the values, you use them when you create a connection with IT Service Management Connector.</span></span>

<span data-ttu-id="f47f6-179">**檢查 Web 應用程式安裝**</span><span class="sxs-lookup"><span data-stu-id="f47f6-179">**Check the Web app installation**</span></span>

1. <span data-ttu-id="f47f6-180">移至 [Azure 入口網站] > [資源]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-180">Go to **Azure portal** > **Resources**.</span></span>
2. <span data-ttu-id="f47f6-181">選取 Web 應用程式，按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-181">Select the Web app, click **Settings** > **Application Settings**.</span></span>
3. <span data-ttu-id="f47f6-182">確認您在透過指令碼部署應用程式時所提供的 Service Manager 執行個體之相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f47f6-182">Confirm the information about the Service Manager instance that you provided at the time of deploying the app through the script.</span></span>

### <a name="configure-the-hybrid-connection"></a><span data-ttu-id="f47f6-183">設定混合式連線</span><span class="sxs-lookup"><span data-stu-id="f47f6-183">Configure the hybrid connection</span></span>

<span data-ttu-id="f47f6-184">您可以使用下列程序，設定將 Service Manager 執行個體與 OMS 中的 IT 服務管理連接器連線之混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-184">Use the following procedure to configure the hybrid connection that connects the Service Manager instance with the IT Service Management Connector in OMS.</span></span>

1. <span data-ttu-id="f47f6-185">在 **Azure 資源**下，尋找 Service Manager Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f47f6-185">Find the Service Manager Web app, under **Azure Resources**.</span></span>
2. <span data-ttu-id="f47f6-186">按一下 [設定] > [網路]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-186">Click **Settings** > **Networking**.</span></span>
3. <span data-ttu-id="f47f6-187">在 [混合式連線] 下，按一下 [設定混合式連線端點]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-187">Under **Hybrid Connections**, click **Configure your hybrid connection endpoints**.</span></span>

    ![混合式連線網路](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. <span data-ttu-id="f47f6-189">在 [混合式連線] 刀鋒視窗上，按一下 [新增混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-189">In the **Hybrid Connections** blade, click **Add hybrid connection**.</span></span>

    ![混合式連線新增](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. <span data-ttu-id="f47f6-191">在 [新增混合式連線] 刀鋒視窗上，按一下 [建立新的混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-191">In the **Add Hybrid Connections** blade, click **Create new hybrid Connection**.</span></span>

    ![新增混合式連線](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. <span data-ttu-id="f47f6-193">輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="f47f6-193">Type the following values:</span></span>

    - <span data-ttu-id="f47f6-194">**端點名稱**︰指定新混合式連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-194">**EndPoint Name**: Specify a name for the new Hybrid connection.</span></span>
    -  <span data-ttu-id="f47f6-195">**端點主機**︰Service Manager 管理伺服器的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="f47f6-195">**EndPoint Host**: FQDN of the Service Manager management server.</span></span>
    - <span data-ttu-id="f47f6-196">**端點連接埠**：輸入 5724</span><span class="sxs-lookup"><span data-stu-id="f47f6-196">**EndPoint Port**: Type 5724</span></span>
    - <span data-ttu-id="f47f6-197">**服務匯流排命名空間**︰使用現有的或建立一個新的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="f47f6-197">**Servicebus namespace**: Use an existing servicebus namespace or create a new one.</span></span>
    - <span data-ttu-id="f47f6-198">**位置**：選取位置。</span><span class="sxs-lookup"><span data-stu-id="f47f6-198">**Location**: select the location.</span></span>
    -  <span data-ttu-id="f47f6-199">**名稱**︰如果您要建立服務匯流排，請為它指定名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-199">**Name**: Specify a name to the servicebus if you are creating it.</span></span>

    ![混合式連線值](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. <span data-ttu-id="f47f6-201">按一下 [確定] 將 [建立混合式連線] 刀鋒視窗關閉，然後開始建立混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-201">Click **OK** to close the **Create hybrid connection** blade and start creating the hybrid connection.</span></span>

    <span data-ttu-id="f47f6-202">建立混合式連線之後，它會顯示在刀鋒視窗下。</span><span class="sxs-lookup"><span data-stu-id="f47f6-202">Once the Hybrid connection is created, it is displayed under the blade.</span></span>

7. <span data-ttu-id="f47f6-203">建立混合式連線之後，請選取連線，然後按一下 [新增所選的混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-203">After the hybrid connection is created, select the connection and click **Add selected hybrid connection**.</span></span>

    ![新增混合式連線](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-the-listener-setup"></a><span data-ttu-id="f47f6-205">設定接聽程式設定</span><span class="sxs-lookup"><span data-stu-id="f47f6-205">Configure the listener setup</span></span>

<span data-ttu-id="f47f6-206">您可以使用下列程序來設定混合式連線的接聽程式設定。</span><span class="sxs-lookup"><span data-stu-id="f47f6-206">Use the following procedure to configure the listener setup for the hybrid connection.</span></span>

1. <span data-ttu-id="f47f6-207">在 [混合式連線] 刀鋒視窗中，按 [下載連線管理員]，並將它安裝在執行 System Center Service Manager 執行個體的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f47f6-207">In the **Hybrid Connections** blade, click **Download the Connection Manager** and install it on the machine where System Center Service Manager instance is running.</span></span>

    <span data-ttu-id="f47f6-208">一旦安裝完成後，可在 [啟動] 功能表下使用 [混合式連線管理員 UI]選項。</span><span class="sxs-lookup"><span data-stu-id="f47f6-208">Once the installation is complete, **Hybrid Connection Manager UI** option is available under **Start** menu.</span></span>

2. <span data-ttu-id="f47f6-209">按一下 [混合式連線管理員 UI]，系統會提示您輸入 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="f47f6-209">Click **Hybrid Connection Manager UI** , you will be prompted for your Azure credentials.</span></span>

3. <span data-ttu-id="f47f6-210">使用您的 Azure 認證登入，然後選取您在其中建立混合式連線的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f47f6-210">Login with your Azure credentials and select your subscription where the Hybrid connection was created.</span></span>

4. <span data-ttu-id="f47f6-211">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f47f6-211">Click **Save**.</span></span>

<span data-ttu-id="f47f6-212">混合式連線已成功連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-212">Your hybrid connection is successfully connected.</span></span>

![混合式連線成功](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> <span data-ttu-id="f47f6-214">建立混合式連線之後，可瀏覽已部署的 Service Manager Web 應用程式來驗證及測試連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-214">After the hybrid connection is created, verify and test the connection by visiting the deployed Service Manager Web app.</span></span> <span data-ttu-id="f47f6-215">嘗試連線到 OMS 中的 IT 服務管理連接器之前，請確定連線成功。</span><span class="sxs-lookup"><span data-stu-id="f47f6-215">Ensure the connection is successful before you try to connect to the IT Service Management Connector in OMS.</span></span>

<span data-ttu-id="f47f6-216">下圖顯示連線成功的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-216">The following image shows the details of a successful connection:</span></span>

![混合式連線測試](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-to-it-service-management-connector-in-oms"></a><span data-ttu-id="f47f6-218">將 ServiceNow 連線到 OMS 中的 IT 服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="f47f6-218">Connect ServiceNow to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="f47f6-219">下列各節提供有關如何將 ServiceNow 產品連線到 OMS 中的 IT 服務管理連接器之詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f47f6-219">The following sections provide details about how to connect your ServiceNow product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f47f6-220">必要條件</span><span class="sxs-lookup"><span data-stu-id="f47f6-220">Prerequisites</span></span>

<span data-ttu-id="f47f6-221">請確定您已符合這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="f47f6-221">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="f47f6-222">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="f47f6-222">IT Service Management Connector installed.</span></span> <span data-ttu-id="f47f6-223">詳細資訊︰[設定。](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="f47f6-223">More information: [Configuration.](log-analytics-itsmc-overview.md#configuration)</span></span>
- <span data-ttu-id="f47f6-224">ServiceNow 支援版本 – Fuji、Geneva、Helsinki。</span><span class="sxs-lookup"><span data-stu-id="f47f6-224">ServiceNow supported versions – Fuji, Geneva, Helsinki.</span></span>

<span data-ttu-id="f47f6-225">ServiceNow 管理員必須在 ServiceNow 執行個體中執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f47f6-225">ServiceNow Admins must do the following in their ServiceNow instance:</span></span>
- <span data-ttu-id="f47f6-226">產生 ServiceNow 產品的用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="f47f6-226">Generate client ID and client secret for the ServiceNow product.</span></span> <span data-ttu-id="f47f6-227">如需如何產生用戶端識別碼和祕密的資訊，請參閱 [OAuth 設定](http://wiki.servicenow.com/index.php?title=OAuth_Setup)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-227">For information on how to generate client ID and secret, see [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span>
- <span data-ttu-id="f47f6-228">安裝適用於 Microsoft OMS 整合的使用者應用程式 (ServiceNow 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-228">Install the User App for Microsoft OMS integration (ServiceNow app).</span></span> <span data-ttu-id="f47f6-229">[深入了解](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 )。</span><span class="sxs-lookup"><span data-stu-id="f47f6-229">[Learn more](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).</span></span>
- <span data-ttu-id="f47f6-230">為安裝的使用者應用程式建立整合使用者角色。</span><span class="sxs-lookup"><span data-stu-id="f47f6-230">Create integration user role for the user app installed.</span></span> <span data-ttu-id="f47f6-231">關於如何建立整合使用者角色的資訊在[這裡](#create-integration-user-role-in-servicenow-app)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-231">Information on how to create the integration user role is [here](#create-integration-user-role-in-servicenow-app).</span></span>


### <a name="connection-procedure"></a><span data-ttu-id="f47f6-232">**連線程序**</span><span class="sxs-lookup"><span data-stu-id="f47f6-232">**Connection procedure**</span></span>

<span data-ttu-id="f47f6-233">請使用下列程序來建立 ServiceNow 連線：</span><span class="sxs-lookup"><span data-stu-id="f47f6-233">Use the following procedure to create a ServiceNow connection:</span></span>

1. <span data-ttu-id="f47f6-234">移至 [OMS] > [設定] > [連線的來源]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-234">Go to **OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="f47f6-235">選取**ITSM 連接器**，然後按一下 [新增新的連線]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-235">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![ServiceNow 連線](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. <span data-ttu-id="f47f6-237">提供下表中所述的資訊，然後按一下 [儲存] 來建立連線︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-237">Provide the information as described in the following table, and click **Save** to create the connection:</span></span>

> [!NOTE]
> <span data-ttu-id="f47f6-238">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-238">All these parameters are mandatory.</span></span>

| <span data-ttu-id="f47f6-239">**欄位**</span><span class="sxs-lookup"><span data-stu-id="f47f6-239">**Field**</span></span> | <span data-ttu-id="f47f6-240">**說明**</span><span class="sxs-lookup"><span data-stu-id="f47f6-240">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f47f6-241">**名稱**</span><span class="sxs-lookup"><span data-stu-id="f47f6-241">**Name**</span></span>   | <span data-ttu-id="f47f6-242">輸入您想要與 IT 服務管理連接器連線之 ServiceNow 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-242">Type a name for the ServiceNow instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-243">稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-243">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="f47f6-244">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="f47f6-244">**Select Connection type**</span></span>   | <span data-ttu-id="f47f6-245">選取 **ServiceNow**。</span><span class="sxs-lookup"><span data-stu-id="f47f6-245">Select **ServiceNow**.</span></span> |
| <span data-ttu-id="f47f6-246">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="f47f6-246">**Username**</span></span>   | <span data-ttu-id="f47f6-247">輸入您在 ServiceNow 應用程式中建立的整合使用者名稱，以支援 IT 服務管理連接器的連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-247">Type the integration user name that you created in the ServiceNow app to support the connection to the IT Service Management Connector.</span></span> <span data-ttu-id="f47f6-248">詳細資訊︰[建立 ServiceNow 應用程式使用者角色](#create-integration-user-role-in-servicenow-app)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-248">More information: [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app).</span></span>|
| <span data-ttu-id="f47f6-249">**密碼**</span><span class="sxs-lookup"><span data-stu-id="f47f6-249">**Password**</span></span>   | <span data-ttu-id="f47f6-250">將與此使用者名稱與相關聯的密碼輸入。</span><span class="sxs-lookup"><span data-stu-id="f47f6-250">Type the password associated with this user name.</span></span> <span data-ttu-id="f47f6-251">**請注意**︰使用者名稱和密碼僅用來產生驗證權杖，並不會儲存在 OMS 服務內。</span><span class="sxs-lookup"><span data-stu-id="f47f6-251">**Note**: User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service.</span></span>  |
| <span data-ttu-id="f47f6-252">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="f47f6-252">**Server URL**</span></span>   | <span data-ttu-id="f47f6-253">輸入您想要連線到 IT 服務管理連接器之 ServiceNow 執行個體的 URL。</span><span class="sxs-lookup"><span data-stu-id="f47f6-253">Type the URL of the ServiceNow instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="f47f6-254">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="f47f6-254">**Client ID**</span></span>   | <span data-ttu-id="f47f6-255">將您想要用於先前產生之 OAuth2 驗證的用戶端識別碼輸入。</span><span class="sxs-lookup"><span data-stu-id="f47f6-255">Type the client ID that you want to use for OAuth2 Authentication, which you generated earlier.</span></span>  <span data-ttu-id="f47f6-256">如需產生用戶端識別碼和祕密的資訊：[OAuth 設定](http://wiki.servicenow.com/index.php?title=OAuth_Setup)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-256">More information on generating client ID and secret:   [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span> |
| <span data-ttu-id="f47f6-257">**用戶端祕密**</span><span class="sxs-lookup"><span data-stu-id="f47f6-257">**Client Secret**</span></span>   | <span data-ttu-id="f47f6-258">輸入針對此識別碼產生的用戶端祕密。</span><span class="sxs-lookup"><span data-stu-id="f47f6-258">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="f47f6-259">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="f47f6-259">**Data Sync Scope**</span></span>   | <span data-ttu-id="f47f6-260">選取您想要透過 IT 服務管理連接器同步到 OMS 的 ServiceNow 工作項目。</span><span class="sxs-lookup"><span data-stu-id="f47f6-260">Select the ServiceNow work items that you want to sync to OMS, through the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-261">系統會將這些值匯入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="f47f6-261">The selected values are imported into log analytics.</span></span>   <span data-ttu-id="f47f6-262">**選項︰**事件和變更要求。</span><span class="sxs-lookup"><span data-stu-id="f47f6-262">**Options:**  Incidents and Change Requests.</span></span>|
| <span data-ttu-id="f47f6-263">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="f47f6-263">**Sync Data**</span></span> | <span data-ttu-id="f47f6-264">輸入您想要起算資料的過去天數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-264">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="f47f6-265">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="f47f6-265">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="f47f6-266">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="f47f6-266">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="f47f6-267">如果您想要在 ITSM 產品中建立設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="f47f6-267">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="f47f6-268">選取時，OMS 會在支援的 ITSM 系統中建立受影響的 CI 作為設定項目 (如果 CI 不存在)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-268">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="f47f6-269">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="f47f6-269">**Default**: disabled.</span></span> |


<span data-ttu-id="f47f6-270">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-270">When successfully connected, and synced:</span></span>

- <span data-ttu-id="f47f6-271">從 ServiceNow 連線選取的工作項目將匯入 OMS Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="f47f6-271">Selected work items from ServiceNow connection are imported into OMS Log Analytics.</span></span>  <span data-ttu-id="f47f6-272">您可以在 [IT 服務管理連接器] 圖格上檢視這些工作項目的摘要。</span><span class="sxs-lookup"><span data-stu-id="f47f6-272">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="f47f6-273">您可以在這個 ServiceNow 執行個體中建立 OMS 警示或記錄搜尋的事件、警示和活動。</span><span class="sxs-lookup"><span data-stu-id="f47f6-273">You can create incidents, alerts, and events from OMS Alerts or log search in this ServiceNow instance.</span></span>  


<span data-ttu-id="f47f6-274">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-274">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-integration-user-role-in-servicenow-app"></a><span data-ttu-id="f47f6-275">在 ServiceNow 應用程式中建立整合使用者角色</span><span class="sxs-lookup"><span data-stu-id="f47f6-275">Create integration user role in ServiceNow app</span></span>

<span data-ttu-id="f47f6-276">請使用下列程序：</span><span class="sxs-lookup"><span data-stu-id="f47f6-276">User the following procedure:</span></span>

1.  <span data-ttu-id="f47f6-277">請瀏覽 [ServiceNow 存放區](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0)，並將 **ServiceNow 和 Microsoft OMS 整合的使用者應用程式**安裝到 ServiceNow 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f47f6-277">Visit the [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) and install the **User App for ServiceNow and Microsoft OMS Integration** into your ServiceNow Instance.</span></span>
2.  <span data-ttu-id="f47f6-278">安裝完成後，請瀏覽左側導覽列中的 [ServiceNow 執行個體]、[搜尋] 並選取 [Microsoft OMS 整合器]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-278">After installation, visit the left navigation bar of the ServiceNow instance, search, and select Microsoft OMS integrator.</span></span>  
3.  <span data-ttu-id="f47f6-279">按一下 [安裝檢查清單]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-279">Click **Installation Checklist**.</span></span>

    <span data-ttu-id="f47f6-280">如果尚未建立使用者角色，則狀態會顯示為 [未完成]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-280">The status is displayed as  **Not complete** if the user role is yet to be created.</span></span>

4.  <span data-ttu-id="f47f6-281">在 [建立整合使用者] 旁邊的文字方塊中，輸入可連線到 OMS 中的 IT 服務管理連接器之使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-281">In the text boxes, next to **Create integration user**, enter the user name for the user that can connect to the IT Service Management Connector in OMS.</span></span>
5.  <span data-ttu-id="f47f6-282">輸入這個使用者的密碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-282">Enter the password for this user, and click **OK**.</span></span>  

>[!NOTE]

> <span data-ttu-id="f47f6-283">您可以使用這些認證在 OMS 中進行 ServiceNow 連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-283">You use these credentials to make the ServiceNow connection in OMS.</span></span>

<span data-ttu-id="f47f6-284">會使用預設的角色指派來顯示新建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="f47f6-284">The newly created user is displayed with the default roles assigned.</span></span>

<span data-ttu-id="f47f6-285">預設角色︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-285">Default roles:</span></span>
- <span data-ttu-id="f47f6-286">personalize_choices</span><span class="sxs-lookup"><span data-stu-id="f47f6-286">personalize_choices</span></span>
- <span data-ttu-id="f47f6-287">import_transformer</span><span class="sxs-lookup"><span data-stu-id="f47f6-287">import_transformer</span></span>
-   <span data-ttu-id="f47f6-288">x_mioms_microsoft.user</span><span class="sxs-lookup"><span data-stu-id="f47f6-288">x_mioms_microsoft.user</span></span>
-   <span data-ttu-id="f47f6-289">itil</span><span class="sxs-lookup"><span data-stu-id="f47f6-289">itil</span></span>
-   <span data-ttu-id="f47f6-290">template_editor</span><span class="sxs-lookup"><span data-stu-id="f47f6-290">template_editor</span></span>
-   <span data-ttu-id="f47f6-291">view_changer</span><span class="sxs-lookup"><span data-stu-id="f47f6-291">view_changer</span></span>

<span data-ttu-id="f47f6-292">成功建立使用者之後，[檢查安裝檢查清單] 狀態會改變為 [已完成]，並列出針對應用程式所建立的使用者角色詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f47f6-292">Once the user is successfully created, the status of **Check Installation Checklist** moves to Completed, listing the details of the user role created for the app.</span></span>

> [!NOTE]

> <span data-ttu-id="f47f6-293">若要允許使用者從 OMS 建立 ServiceNow 中的 [警示] 和 [事件]︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-293">To allow a user to create **alerts** and **events** in ServiceNow from OMS:</span></span>

> - <span data-ttu-id="f47f6-294">請確定您已在 ServiceNow 執行個體上安裝事件管理模組。</span><span class="sxs-lookup"><span data-stu-id="f47f6-294">Ensure you have the Event Management module Installed on your ServiceNow instance.</span></span>

> - <span data-ttu-id="f47f6-295">將下列角色新增至整合使用者︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-295">Add the following roles to the integration user:</span></span>
>      - <span data-ttu-id="f47f6-296">evt_mgmt_integration</span><span class="sxs-lookup"><span data-stu-id="f47f6-296">evt_mgmt_integration</span></span>
>      - <span data-ttu-id="f47f6-297">evt_mgmt_operator</span><span class="sxs-lookup"><span data-stu-id="f47f6-297">evt_mgmt_operator</span></span>  


## <a name="connect-provance-to-it-service-management-connector-in-oms"></a><span data-ttu-id="f47f6-298">將 Provance 連線到 OMS 中的 IT 服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="f47f6-298">Connect Provance to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="f47f6-299">下列各節提供有關如何將 Provance 產品連線到 OMS 中的 IT 服務管理連接器之詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f47f6-299">The following sections provide details about how to connect your Provance product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f47f6-300">必要條件</span><span class="sxs-lookup"><span data-stu-id="f47f6-300">Prerequisites</span></span>

<span data-ttu-id="f47f6-301">請確定您已符合這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="f47f6-301">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="f47f6-302">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="f47f6-302">IT Service Management Connector installed.</span></span> <span data-ttu-id="f47f6-303">詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-303">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="f47f6-304">應該向 Azure AD 註冊 Provance 應用程式 - 並將用戶端識別碼設為可用。</span><span class="sxs-lookup"><span data-stu-id="f47f6-304">Provance App should be registered with Azure AD - and client ID is made available.</span></span> <span data-ttu-id="f47f6-305">如需詳細資訊，請參閱[如何設定 Active Directory 驗證](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-305">For detailed information, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
- <span data-ttu-id="f47f6-306">使用者角色：管理員。</span><span class="sxs-lookup"><span data-stu-id="f47f6-306">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="f47f6-307">連線程序</span><span class="sxs-lookup"><span data-stu-id="f47f6-307">Connection Procedure</span></span>

<span data-ttu-id="f47f6-308">請使用下列程序來建立 Provance 連線：</span><span class="sxs-lookup"><span data-stu-id="f47f6-308">Use the following procedure to create a Provance connection:</span></span>

1. <span data-ttu-id="f47f6-309">移至 [OMS] > [設定] > [連線的來源]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-309">Go to **OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="f47f6-310">選取**ITSM 連接器**，然後按一下 [新增新的連線]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-310">Select **ITSM Connector,** click **Add New Connection**.</span></span>  

    ![Provance 連線](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. <span data-ttu-id="f47f6-312">提供下表中所述的資訊，然後按一下 [儲存] 來建立連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-312">Provide the information as described in the following table, and click **Save** to create the connection.</span></span>

> [!NOTE]
> <span data-ttu-id="f47f6-313">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-313">All these parameters are mandatory.</span></span>

| <span data-ttu-id="f47f6-314">**欄位**</span><span class="sxs-lookup"><span data-stu-id="f47f6-314">**Field**</span></span> | <span data-ttu-id="f47f6-315">**說明**</span><span class="sxs-lookup"><span data-stu-id="f47f6-315">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f47f6-316">**名稱**</span><span class="sxs-lookup"><span data-stu-id="f47f6-316">**Name**</span></span>   | <span data-ttu-id="f47f6-317">輸入您想要與 IT 服務管理連接器連線之 Provance 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-317">Type a name for the Provance instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-318">稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-318">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="f47f6-319">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="f47f6-319">**Select Connection type**</span></span>   | <span data-ttu-id="f47f6-320">選取 [Provance]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-320">Select **Provance**.</span></span> |
| <span data-ttu-id="f47f6-321">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="f47f6-321">**Username**</span></span>   | <span data-ttu-id="f47f6-322">輸入可連線到 IT 服務管理連接器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-322">Type the user name that can connect to the IT Service Management Connector.</span></span>    |
| <span data-ttu-id="f47f6-323">**密碼**</span><span class="sxs-lookup"><span data-stu-id="f47f6-323">**Password**</span></span>   | <span data-ttu-id="f47f6-324">將與此使用者名稱與相關聯的密碼輸入。</span><span class="sxs-lookup"><span data-stu-id="f47f6-324">Type the password associated with this user name.</span></span> <span data-ttu-id="f47f6-325">**請注意**︰使用者名稱和密碼僅用來產生驗證權杖，並不會儲存在 OMS 服務內。</span><span class="sxs-lookup"><span data-stu-id="f47f6-325">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service._</span></span>|
| <span data-ttu-id="f47f6-326">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="f47f6-326">**Server URL**</span></span>   | <span data-ttu-id="f47f6-327">輸入您想要連線到 IT 服務管理連接器之 Provance 執行個體的 URL。</span><span class="sxs-lookup"><span data-stu-id="f47f6-327">Type the URL of your Provance instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="f47f6-328">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="f47f6-328">**Client ID**</span></span>   | <span data-ttu-id="f47f6-329">將您在 Provance 執行個體中產生的用戶端識別碼輸入以驗證此連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-329">Type the client ID for authenticating this connection, which you generated in your Provance instance.</span></span>  <span data-ttu-id="f47f6-330">如需用戶端識別碼的詳細資訊，請參閱[如何設定 Active Directory 驗證](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-330">More information on client ID, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> |
| <span data-ttu-id="f47f6-331">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="f47f6-331">**Data Sync Scope**</span></span>   | <span data-ttu-id="f47f6-332">選取您想要透過 IT 服務管理連接器同步到 OMS 的 Provance 工作項目。</span><span class="sxs-lookup"><span data-stu-id="f47f6-332">Select the Provance work items that you want to sync to OMS, through the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-333">系統會將這些工作項目匯入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="f47f6-333">These work items are imported into log analytics.</span></span>   <span data-ttu-id="f47f6-334">**選項︰**事件、變更要求。</span><span class="sxs-lookup"><span data-stu-id="f47f6-334">**Options:**   Incidents, Change Requests.</span></span>|
| <span data-ttu-id="f47f6-335">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="f47f6-335">**Sync Data**</span></span> | <span data-ttu-id="f47f6-336">輸入您想要起算資料的過去天數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-336">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="f47f6-337">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="f47f6-337">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="f47f6-338">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="f47f6-338">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="f47f6-339">如果您想要在 ITSM 產品中建立設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="f47f6-339">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="f47f6-340">選取時，OMS 會在支援的 ITSM 系統中建立受影響的 CI 作為設定項目 (如果 CI 不存在)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-340">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="f47f6-341">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="f47f6-341">**Default**: disabled.</span></span>|

<span data-ttu-id="f47f6-342">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-342">When successfully connected, and synced:</span></span>

- <span data-ttu-id="f47f6-343">從 Provance 連線選取的工作項目將匯入 OMS **Log Analytics**。</span><span class="sxs-lookup"><span data-stu-id="f47f6-343">Selected work items from Provance connection are imported into OMS **Log Analytics.**</span></span>  <span data-ttu-id="f47f6-344">您可以在 [IT 服務管理連接器] 圖格上檢視這些工作項目的摘要。</span><span class="sxs-lookup"><span data-stu-id="f47f6-344">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="f47f6-345">您可以在這個 Provance 執行個體中建立 OMS 警示或記錄搜尋的事件和活動。</span><span class="sxs-lookup"><span data-stu-id="f47f6-345">You can create incidents and events from OMS Alerts or Log Search in this Provance instance.</span></span>

<span data-ttu-id="f47f6-346">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-346">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

## <a name="connect-cherwell-to-it-service-management-connector-in-oms"></a><span data-ttu-id="f47f6-347">將 Cherwell 連線到 OMS 中的 IT 服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="f47f6-347">Connect Cherwell to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="f47f6-348">下列各節提供有關如何將 Cherwell 產品連線到 OMS 中的 IT服務管理連接器之詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f47f6-348">The following sections provide details about how to connect your Cherwell product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f47f6-349">必要條件</span><span class="sxs-lookup"><span data-stu-id="f47f6-349">Prerequisites</span></span>

<span data-ttu-id="f47f6-350">請確定您已符合這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="f47f6-350">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="f47f6-351">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="f47f6-351">IT Service Management Connector installed.</span></span> <span data-ttu-id="f47f6-352">詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-352">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="f47f6-353">所產生的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="f47f6-353">Client ID generated.</span></span> <span data-ttu-id="f47f6-354">詳細資訊︰[產生 Cherwell 的用戶端識別碼](#generate-client-id-for-cherwell)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-354">More information: [Generate client ID for Cherwell](#generate-client-id-for-cherwell).</span></span>
- <span data-ttu-id="f47f6-355">使用者角色：管理員。</span><span class="sxs-lookup"><span data-stu-id="f47f6-355">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="f47f6-356">連線程序</span><span class="sxs-lookup"><span data-stu-id="f47f6-356">Connection Procedure</span></span>

<span data-ttu-id="f47f6-357">請使用下列程序來建立 Cherwell 連線：</span><span class="sxs-lookup"><span data-stu-id="f47f6-357">Use the following procedure to create a Cherwell connection:</span></span>

1. <span data-ttu-id="f47f6-358">移至 [OMS] >  [設定] > [連線的來源]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-358">Go to **OMS** >  **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="f47f6-359">選取 [ITSM 連接器]，然後按一下 [新增新的連線]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-359">Select **ITSM Connector** click **Add New Connection**.</span></span>  

    ![Cherwell 使用者識別碼](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. <span data-ttu-id="f47f6-361">提供下表中所述的資訊，然後按一下 [儲存] 來建立連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-361">Provide the information as described in the following table, and click  **Save** to create the connection.</span></span>

> [!NOTE]
> <span data-ttu-id="f47f6-362">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-362">All these parameters are mandatory.</span></span>

| <span data-ttu-id="f47f6-363">**欄位**</span><span class="sxs-lookup"><span data-stu-id="f47f6-363">**Field**</span></span> | <span data-ttu-id="f47f6-364">**說明**</span><span class="sxs-lookup"><span data-stu-id="f47f6-364">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f47f6-365">**名稱**</span><span class="sxs-lookup"><span data-stu-id="f47f6-365">**Name**</span></span>   | <span data-ttu-id="f47f6-366">輸入您想要連線到 IT 服務管理連接器之 Cherwell 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-366">Type a name for the Cherwell instance that you want to connect to the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-367">稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-367">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="f47f6-368">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="f47f6-368">**Select Connection type**</span></span>   | <span data-ttu-id="f47f6-369">選取 [Cherwell]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-369">Select **Cherwell.**</span></span> |
| <span data-ttu-id="f47f6-370">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="f47f6-370">**Username**</span></span>   | <span data-ttu-id="f47f6-371">輸入可連線到 IT 服務管理連接器的 Cherwell 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f47f6-371">Type the Cherwell user name that can connect to the IT Service Management Connector.</span></span> |
| <span data-ttu-id="f47f6-372">**密碼**</span><span class="sxs-lookup"><span data-stu-id="f47f6-372">**Password**</span></span>   | <span data-ttu-id="f47f6-373">將與此使用者名稱與相關聯的密碼輸入。</span><span class="sxs-lookup"><span data-stu-id="f47f6-373">Type the password associated with this user name.</span></span> <span data-ttu-id="f47f6-374">**請注意**︰使用者名稱和密碼僅用來產生驗證權杖，並不會儲存在 OMS 服務內。</span><span class="sxs-lookup"><span data-stu-id="f47f6-374">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service.</span></span>|
| <span data-ttu-id="f47f6-375">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="f47f6-375">**Server URL**</span></span>   | <span data-ttu-id="f47f6-376">輸入您想要連線到 IT 服務管理連接器之 Cherwell 執行個體的 URL。</span><span class="sxs-lookup"><span data-stu-id="f47f6-376">Type the URL of your Cherwell instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="f47f6-377">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="f47f6-377">**Client ID**</span></span>   | <span data-ttu-id="f47f6-378">將您在 Cherwell 執行個體中產生的用戶端識別碼輸入以驗證此連線。</span><span class="sxs-lookup"><span data-stu-id="f47f6-378">Type the client ID for authenticating this connection, which you generated in your Cherwell instance.</span></span>   |
| <span data-ttu-id="f47f6-379">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="f47f6-379">**Data Sync Scope**</span></span>   | <span data-ttu-id="f47f6-380">選取您想要透過 IT 服務管理連接器同步的 Cherwell 工作項目。</span><span class="sxs-lookup"><span data-stu-id="f47f6-380">Select the Cherwell work items that you want to sync through the IT Service Management Connector.</span></span>  <span data-ttu-id="f47f6-381">系統會將這些工作項目匯入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="f47f6-381">These work items are imported into log analytics.</span></span>   <span data-ttu-id="f47f6-382">**選項︰**事件、變更要求。</span><span class="sxs-lookup"><span data-stu-id="f47f6-382">**Options:**  Incidents, Change Requests.</span></span> |
| <span data-ttu-id="f47f6-383">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="f47f6-383">**Sync Data**</span></span> | <span data-ttu-id="f47f6-384">輸入您想要起算資料的過去天數。</span><span class="sxs-lookup"><span data-stu-id="f47f6-384">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="f47f6-385">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="f47f6-385">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="f47f6-386">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="f47f6-386">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="f47f6-387">如果您想要在 ITSM 產品中建立設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="f47f6-387">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="f47f6-388">選取時，OMS 會在支援的 ITSM 系統中建立受影響的 CI 作為設定項目 (如果 CI 不存在)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-388">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="f47f6-389">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="f47f6-389">**Default**: disabled.</span></span> |

<span data-ttu-id="f47f6-390">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-390">When successfully connected, and synced:</span></span>

- <span data-ttu-id="f47f6-391">從這個 Cherwell 連線選取的工作項目將匯入 OMS Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="f47f6-391">Selected work items from this Cherwell connection are imported into OMS Log Analytics.</span></span> <span data-ttu-id="f47f6-392">您可以在 [IT 服務管理連接器] 圖格上檢視這些工作項目的摘要。</span><span class="sxs-lookup"><span data-stu-id="f47f6-392">You can view the summary of these work items  on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="f47f6-393">您可以從 OMS 建立這個 Cherwell 執行個體的事件和活動。</span><span class="sxs-lookup"><span data-stu-id="f47f6-393">You can create incidents and events in this Cherwell instance from OMS.</span></span> <span data-ttu-id="f47f6-394">詳細資訊︰建立 OMS 警示的 ITSM工作項目及建立 OMS 記錄的 ITSM 工作項目。</span><span class="sxs-lookup"><span data-stu-id="f47f6-394">More information: Create ITSM work items for OMS alerts and Create ITSM work items from OMS logs.</span></span>

<span data-ttu-id="f47f6-395">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="f47f6-395">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="generate-client-id-for-cherwell"></a><span data-ttu-id="f47f6-396">產生 Cherwell 的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="f47f6-396">Generate client ID for Cherwell</span></span>

<span data-ttu-id="f47f6-397">若要產生用戶端識別碼/Cherwell 的金鑰，請使用下列程序︰</span><span class="sxs-lookup"><span data-stu-id="f47f6-397">To generate the client ID/key for Cherwell, use the following procedure:</span></span>

1. <span data-ttu-id="f47f6-398">以管理員身分登入您的 Cherwell 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f47f6-398">Log in to your Cherwell instance as admin.</span></span>
2. <span data-ttu-id="f47f6-399">按一下 [安全性] > [編輯 REST API 用戶端設定]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-399">Click **Security** > **Edit REST API client settings**.</span></span>
3. <span data-ttu-id="f47f6-400">選取 [建立新的用戶端] > [用戶端祕密]。</span><span class="sxs-lookup"><span data-stu-id="f47f6-400">Select **Create new client** > **client secret**.</span></span>

    ![Cherwell 使用者識別碼](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a><span data-ttu-id="f47f6-402">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f47f6-402">Next steps</span></span>
 - [<span data-ttu-id="f47f6-403">建立 OMS 警示的 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="f47f6-403">Create ITSM work items for OMS alerts</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [<span data-ttu-id="f47f6-404">從 OMS 記錄建立 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="f47f6-404">Create ITSM work items from OMS logs</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [<span data-ttu-id="f47f6-405">檢視您連線的 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f47f6-405">View log analytics for your connection</span></span>](log-analytics-itsmc-overview.md#using-the-solution)
