---
title: "在 OMS IT 服務管理連接器 aaaITSM 連線 |Microsoft 文件"
description: "連接您 ITSM 產品/服務 IT 服務管理連接器在 OMS toocentrally 監視及管理 hello ITSM 工作項目。"
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
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a><span data-ttu-id="2a7aa-103">將 ITSM 產品/服務與 IT 服務管理連接器進行連線 (預覽)</span><span class="sxs-lookup"><span data-stu-id="2a7aa-103">Connect ITSM products/services with IT Service Management Connector (Preview)</span></span>
<span data-ttu-id="2a7aa-104">這篇文章提供有關如何資訊 tooconnect 您 ITSM 產品/服務 tooIT Service Management Connector 在 OMS 中，以及集中管理您的工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-104">This article provides information about how tooconnect your ITSM product/service tooIT Service Management Connector in OMS and centrally manage your work items.</span></span> <span data-ttu-id="2a7aa-105">如需有關 IT 服務管理連接器的詳細資訊，請參閱[概觀](log-analytics-itsmc-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-105">More information about IT Service Management Connector, see [Overview](log-analytics-itsmc-overview.md).</span></span>

<span data-ttu-id="2a7aa-106">支援下列產品/服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-106">hello following products/services are supported:</span></span>

- [<span data-ttu-id="2a7aa-107">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="2a7aa-107">System Center Service Manager</span></span>](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="2a7aa-108">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="2a7aa-108">ServiceNow</span></span>](#connect-servicenow-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="2a7aa-109">Provance</span><span class="sxs-lookup"><span data-stu-id="2a7aa-109">Provance</span></span>](#connect-provance-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="2a7aa-110">Cherwell</span><span class="sxs-lookup"><span data-stu-id="2a7aa-110">Cherwell</span></span>](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a><span data-ttu-id="2a7aa-111">連接 System Center Service Manager tooIT 在 OMS 中的服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="2a7aa-111">Connect System Center Service Manager tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="2a7aa-112">hello 下列各節提供詳細說明如何 tooconnect 您的 System Center Service Manager 產品 toohello 在 OMS 中的 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-112">hello following sections provide details about how tooconnect your System Center Service Manager product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2a7aa-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a7aa-113">Prerequisites</span></span>

<span data-ttu-id="2a7aa-114">請確定您有下列必要條件符合 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-114">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="2a7aa-115">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-115">IT Service Management Connector installed.</span></span>
<span data-ttu-id="2a7aa-116">詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-116">More information:  [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="2a7aa-117">hello 服務管理員 Web 應用程式 （Web 應用程式） 是部署和設定。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-117">hello Service Manager Web application (Web app) is deployed and configured.</span></span> <span data-ttu-id="2a7aa-118">Web 應用程式的相關在[這裡](#create-and-deploy-service-manager-web-app-service)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-118">Information on Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
- <span data-ttu-id="2a7aa-119">已建立及設定的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-119">Hybrid connection created and configured.</span></span> <span data-ttu-id="2a7aa-120">更多資訊：[設定 hello 混合式連線](#configure-the-hybrid-connection)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-120">More information: [Configure hello hybrid Connection](#configure-the-hybrid-connection).</span></span>
- <span data-ttu-id="2a7aa-121">Service Manager 的支援版本：2012 R2 或 2016。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-121">Supported versions of Service Manager:  2012 R2 or 2016.</span></span>
- <span data-ttu-id="2a7aa-122">使用者角色︰[進階操作員](https://technet.microsoft.com/library/ff461054.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-122">User role:  [Advanced operator](https://technet.microsoft.com/library/ff461054.aspx).</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="2a7aa-123">連線程序</span><span class="sxs-lookup"><span data-stu-id="2a7aa-123">Connection procedure</span></span>

<span data-ttu-id="2a7aa-124">使用下列程序 tooconnect hello 您的 System Center Service Manager 執行個體 toohello IT 服務管理連接器：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-124">Use hello following procedure tooconnect your System Center Service Manager instance toohello IT Service Management Connector:</span></span>

1. <span data-ttu-id="2a7aa-125">跳過**OMS** >**設定** > **連線來源**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-125">Go too**OMS** >**Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="2a7aa-126">選取**ITSM 連接器**，然後按一下新增新的連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-126">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![<span data-ttu-id="2a7aa-127">Service Manager</span><span class="sxs-lookup"><span data-stu-id="2a7aa-127">Service manager</span></span> ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. <span data-ttu-id="2a7aa-128">下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-128">Provide hello information as described in hello following table, and click **Save** toocreate hello connection:</span></span>

> [!NOTE]
> <span data-ttu-id="2a7aa-129">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-129">All these parameters are mandatory.</span></span>

| <span data-ttu-id="2a7aa-130">**欄位**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-130">**Field**</span></span> | <span data-ttu-id="2a7aa-131">**說明**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-131">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="2a7aa-132">**名稱**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-132">**Name**</span></span>   | <span data-ttu-id="2a7aa-133">輸入您想要以 hello IT 服務管理連接器 tooconnect hello System Center Service Manager 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-133">Type a name for hello System Center Service Manager instance that you want tooconnect with hello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-134">稍後當您設定這個執行個體的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-134">You use this name later when you configure work items in this instance/ view detailed log analytics.</span></span> |
| <span data-ttu-id="2a7aa-135">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-135">**Select Connection type**</span></span>   | <span data-ttu-id="2a7aa-136">選取 **System Center Service Manager**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-136">Select **System Center Service Manager**.</span></span> |
| <span data-ttu-id="2a7aa-137">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-137">**Server URL**</span></span>   | <span data-ttu-id="2a7aa-138">輸入 hello hello 服務管理員 Web 應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-138">Type hello URL of hello Service Manager Web app.</span></span> <span data-ttu-id="2a7aa-139">Service Manager Web 應用程式的相關詳細資訊在[這裡](#create-and-deploy-service-manager-web-app-service)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-139">More information about Service Manager Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
| <span data-ttu-id="2a7aa-140">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-140">**Client ID**</span></span>   | <span data-ttu-id="2a7aa-141">輸入您產生 （使用 hello 自動指令碼） 來驗證 hello Web 應用程式的用戶端識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-141">Type hello client ID that you generated (using hello automatic script) for authenticating hello Web app.</span></span> <span data-ttu-id="2a7aa-142">Hello 自動化指令碼的詳細資訊[這裡。](log-analytics-itsmc-service-manager-script.md)</span><span class="sxs-lookup"><span data-stu-id="2a7aa-142">More information about hello automated script is [here.](log-analytics-itsmc-service-manager-script.md)</span></span>|
| <span data-ttu-id="2a7aa-143">**用戶端祕密**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-143">**Client Secret**</span></span>   | <span data-ttu-id="2a7aa-144">型別 hello 用戶端密碼，產生此識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-144">Type hello client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="2a7aa-145">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-145">**Data Sync Scope**</span></span>   | <span data-ttu-id="2a7aa-146">選取您想透過 hello IT 服務管理連接器 toosync 的 hello Service Manager 工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-146">Select hello Service Manager work items that you want toosync through hello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-147">系統會將這些工作項目匯入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-147">These work items are imported into Log Analytics.</span></span> <span data-ttu-id="2a7aa-148">**選項︰**事件、變更要求。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-148">**Options:**  Incidents, Change Requests.</span></span>|
| <span data-ttu-id="2a7aa-149">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-149">**Sync Data**</span></span> | <span data-ttu-id="2a7aa-150">輸入經過天數 hello 資料從 hello 數的字。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-150">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="2a7aa-151">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-151">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="2a7aa-152">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-152">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="2a7aa-153">如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-153">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="2a7aa-154">選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-154">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="2a7aa-155">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-155">**Default**: disabled.</span></span> |

<span data-ttu-id="2a7aa-156">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="2a7aa-156">When successfully connected, and synced:</span></span>

- <span data-ttu-id="2a7aa-157">從 Service Manager 選取的工作項目將匯入 OMS **Log Analytics。**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-157">Selected work items from Service Manager are imported into OMS **Log Analytics.**</span></span> <span data-ttu-id="2a7aa-158">您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-158">You can view hello summary of these work items on hello IT Service Management Connector tile.</span></span>

- <span data-ttu-id="2a7aa-159">您可以從 OMS 建立這個 Service Manager 執行個體中的 OMS 警示或記錄搜尋事件。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-159">From OMS, you can create incidents from OMS alerts or from log search, in this Service Manager instance.</span></span>

<span data-ttu-id="2a7aa-160">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-160">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-and-deploy-service-manager-web-app-service"></a><span data-ttu-id="2a7aa-161">建立及部署 Service Manager Web 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="2a7aa-161">Create and deploy Service Manager web app service</span></span>

<span data-ttu-id="2a7aa-162">tooconnect hello 以 hello OMS 上的 IT 服務管理連接器在內部部署 Service Manager 時，Microsoft 已建立 hello GitHub 上的服務管理員 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-162">tooconnect hello on-premises Service Manager with hello IT Service Management Connector on OMS, Microsoft has created a Service Manager Web app on hello GitHub.</span></span>

<span data-ttu-id="2a7aa-163">tooset 設定 hello ITSM Web 應用程式為您的服務管理員，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-163">tooset up hello ITSM Web app for your Service Manager, do hello following:</span></span>

- <span data-ttu-id="2a7aa-164">**部署 hello Web 應用程式**– 部署 hello Web 應用程式、 設定 hello 屬性，以及使用 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-164">**Deploy hello Web app** – Deploy hello Web app, set hello properties, and authenticate with Azure AD.</span></span> <span data-ttu-id="2a7aa-165">您可以部署 hello web 應用程式使用 hello[自動化指令碼](log-analytics-itsmc-service-manager-script.md)Microsoft 已提供您。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-165">You can deploy hello web app by using hello [automated script](log-analytics-itsmc-service-manager-script.md) that Microsoft has provided you.</span></span>
- <span data-ttu-id="2a7aa-166">**設定 hello 混合式連接** - [設定此連線](#configure-the-hybrid-connection)、 以手動方式。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-166">**Configure hello hybrid connection** - [Configure this connection](#configure-the-hybrid-connection), manually.</span></span>

#### <a name="deploy-hello-web-app"></a><span data-ttu-id="2a7aa-167">部署 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2a7aa-167">Deploy hello web app</span></span>
<span data-ttu-id="2a7aa-168">使用 hello 自動化[指令碼](log-analytics-itsmc-service-manager-script.md)toodeploy hello Web 應用程式、 設定 hello 屬性，以及使用 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-168">Use hello automated [script](log-analytics-itsmc-service-manager-script.md) toodeploy hello Web app, set hello properties, and authenticate with Azure AD.</span></span>

<span data-ttu-id="2a7aa-169">藉由提供下列必要的詳細資料的 hello 執行 hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-169">Run hello script by providing hello following required details:</span></span>

- <span data-ttu-id="2a7aa-170">Azure 訂用帳戶詳細資料</span><span class="sxs-lookup"><span data-stu-id="2a7aa-170">Azure subscription details</span></span>
- <span data-ttu-id="2a7aa-171">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="2a7aa-171">Resource group name</span></span>
- <span data-ttu-id="2a7aa-172">位置</span><span class="sxs-lookup"><span data-stu-id="2a7aa-172">Location</span></span>
- <span data-ttu-id="2a7aa-173">Service Manager 伺服器詳細資料 (伺服器名稱、網域、使用者名稱和密碼)</span><span class="sxs-lookup"><span data-stu-id="2a7aa-173">Service Manager server details (server name, domain, user name, and password)</span></span>
- <span data-ttu-id="2a7aa-174">Web 應用程式的網站名稱前置詞</span><span class="sxs-lookup"><span data-stu-id="2a7aa-174">Site name prefix for your Web app</span></span>
- <span data-ttu-id="2a7aa-175">服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-175">ServiceBus Namespace.</span></span>

<span data-ttu-id="2a7aa-176">hello 指令碼會建立使用您指定的 hello 名稱 hello Web 應用程式 (以及幾個額外字串 toomake 它唯一)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-176">hello script creates hello Web app using hello name that you specified (along with few additional strings toomake it unique).</span></span> <span data-ttu-id="2a7aa-177">它會產生 hello **Web 應用程式 URL**，**用戶端識別碼**和**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-177">It generates hello **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="2a7aa-178">Hello 值儲存您使用它們的 IT 服務管理 Connector 建立連線時。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-178">Save hello values, you use them when you create a connection with IT Service Management Connector.</span></span>

<span data-ttu-id="2a7aa-179">**檢查 hello Web 應用程式安裝**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-179">**Check hello Web app installation**</span></span>

1. <span data-ttu-id="2a7aa-180">跳過**Azure 入口網站** > **資源**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-180">Go too**Azure portal** > **Resources**.</span></span>
2. <span data-ttu-id="2a7aa-181">選取 hello Web 應用程式中，按一下**設定** > **應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-181">Select hello Web app, click **Settings** > **Application Settings**.</span></span>
3. <span data-ttu-id="2a7aa-182">確認您提供的 hello 透過 hello 指令碼的應用程式部署的 hello 時間 hello Service Manager 執行個體的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-182">Confirm hello information about hello Service Manager instance that you provided at hello time of deploying hello app through hello script.</span></span>

### <a name="configure-hello-hybrid-connection"></a><span data-ttu-id="2a7aa-183">設定 hello 混合式連接</span><span class="sxs-lookup"><span data-stu-id="2a7aa-183">Configure hello hybrid connection</span></span>

<span data-ttu-id="2a7aa-184">使用下列程序 tooconfigure hello 混合式連接的 hello Service Manager 執行個體連接與 hello IT 服務管理連接器在 OMS 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-184">Use hello following procedure tooconfigure hello hybrid connection that connects hello Service Manager instance with hello IT Service Management Connector in OMS.</span></span>

1. <span data-ttu-id="2a7aa-185">Hello 服務管理員 Web 應用程式中，尋找底下**Azure 資源**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-185">Find hello Service Manager Web app, under **Azure Resources**.</span></span>
2. <span data-ttu-id="2a7aa-186">按一下 [設定] > [網路]。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-186">Click **Settings** > **Networking**.</span></span>
3. <span data-ttu-id="2a7aa-187">在 [混合式連線] 下，按一下 [設定混合式連線端點]。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-187">Under **Hybrid Connections**, click **Configure your hybrid connection endpoints**.</span></span>

    ![混合式連線網路](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. <span data-ttu-id="2a7aa-189">在 hello**混合式連線**刀鋒視窗中，按一下 **新增混合式連接**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-189">In hello **Hybrid Connections** blade, click **Add hybrid connection**.</span></span>

    ![混合式連線新增](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. <span data-ttu-id="2a7aa-191">在 hello**新增混合式連線**刀鋒視窗中，按一下 **建立新的混合式連線**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-191">In hello **Add Hybrid Connections** blade, click **Create new hybrid Connection**.</span></span>

    ![新增混合式連線](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. <span data-ttu-id="2a7aa-193">輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-193">Type hello following values:</span></span>

    - <span data-ttu-id="2a7aa-194">**端點名稱**： 指定 hello 新混合式連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-194">**EndPoint Name**: Specify a name for hello new Hybrid connection.</span></span>
    -  <span data-ttu-id="2a7aa-195">**端點主機**: hello Service Manager 管理伺服器的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-195">**EndPoint Host**: FQDN of hello Service Manager management server.</span></span>
    - <span data-ttu-id="2a7aa-196">**端點連接埠**：輸入 5724</span><span class="sxs-lookup"><span data-stu-id="2a7aa-196">**EndPoint Port**: Type 5724</span></span>
    - <span data-ttu-id="2a7aa-197">**服務匯流排命名空間**︰使用現有的或建立一個新的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-197">**Servicebus namespace**: Use an existing servicebus namespace or create a new one.</span></span>
    - <span data-ttu-id="2a7aa-198">**位置**： 選取 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-198">**Location**: select hello location.</span></span>
    -  <span data-ttu-id="2a7aa-199">**名稱**： 指定名稱 toohello servicebus，如果您要建立它。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-199">**Name**: Specify a name toohello servicebus if you are creating it.</span></span>

    ![混合式連線值](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. <span data-ttu-id="2a7aa-201">按一下**確定**tooclose hello**建立混合式連接**刀鋒視窗，然後開始建立 hello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-201">Click **OK** tooclose hello **Create hybrid connection** blade and start creating hello hybrid connection.</span></span>

    <span data-ttu-id="2a7aa-202">Hello 混合式連線建立之後，它會顯示在 [hello] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-202">Once hello Hybrid connection is created, it is displayed under hello blade.</span></span>

7. <span data-ttu-id="2a7aa-203">建立 hello 混合式連線之後，請選取 hello 連線，然後按一下**新增選取的混合式連接**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-203">After hello hybrid connection is created, select hello connection and click **Add selected hybrid connection**.</span></span>

    ![新增混合式連線](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a><span data-ttu-id="2a7aa-205">設定 hello 接聽程式的安裝程式</span><span class="sxs-lookup"><span data-stu-id="2a7aa-205">Configure hello listener setup</span></span>

<span data-ttu-id="2a7aa-206">使用下列程序 tooconfigure hello hello 混合式連接的接聽程式設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-206">Use hello following procedure tooconfigure hello listener setup for hello hybrid connection.</span></span>

1. <span data-ttu-id="2a7aa-207">在 hello**混合式連線**刀鋒視窗中，按一下**下載 hello 連線管理員**並將它安裝在 hello System Center Service Manager 執行個體執行所在的電腦上。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-207">In hello **Hybrid Connections** blade, click **Download hello Connection Manager** and install it on hello machine where System Center Service Manager instance is running.</span></span>

    <span data-ttu-id="2a7aa-208">Hello 安裝完成之後，**混合式連接管理員 UI**才可使用選項**啟動**功能表。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-208">Once hello installation is complete, **Hybrid Connection Manager UI** option is available under **Start** menu.</span></span>

2. <span data-ttu-id="2a7aa-209">按一下 [混合式連線管理員 UI]，系統會提示您輸入 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-209">Click **Hybrid Connection Manager UI** , you will be prompted for your Azure credentials.</span></span>

3. <span data-ttu-id="2a7aa-210">使用您的 Azure 認證登入並選取您建立 hello 混合式連接所在的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-210">Login with your Azure credentials and select your subscription where hello Hybrid connection was created.</span></span>

4. <span data-ttu-id="2a7aa-211">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-211">Click **Save**.</span></span>

<span data-ttu-id="2a7aa-212">混合式連線已成功連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-212">Your hybrid connection is successfully connected.</span></span>

![混合式連線成功](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> <span data-ttu-id="2a7aa-214">建立 hello 混合式連線之後，請確認，然後瀏覽 hello 測試 hello 連接 Service Manager Web 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-214">After hello hybrid connection is created, verify and test hello connection by visiting hello deployed Service Manager Web app.</span></span> <span data-ttu-id="2a7aa-215">請確定 hello 連接成功之前 tooconnect toohello IT 服務管理連接器在 OMS 中再試一次。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-215">Ensure hello connection is successful before you try tooconnect toohello IT Service Management Connector in OMS.</span></span>

<span data-ttu-id="2a7aa-216">hello 下列影像顯示 hello 成功連接詳細資料：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-216">hello following image shows hello details of a successful connection:</span></span>

![混合式連線測試](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a><span data-ttu-id="2a7aa-218">連接 ServiceNow tooIT 在 OMS 中的服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="2a7aa-218">Connect ServiceNow tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="2a7aa-219">hello 下列各節提供詳細說明如何 tooconnect 您的 ServiceNow 產品 toohello 在 OMS 中的 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-219">hello following sections provide details about how tooconnect your ServiceNow product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2a7aa-220">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a7aa-220">Prerequisites</span></span>

<span data-ttu-id="2a7aa-221">請確定您有下列必要條件符合 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-221">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="2a7aa-222">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-222">IT Service Management Connector installed.</span></span> <span data-ttu-id="2a7aa-223">詳細資訊︰[設定。](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="2a7aa-223">More information: [Configuration.](log-analytics-itsmc-overview.md#configuration)</span></span>
- <span data-ttu-id="2a7aa-224">ServiceNow 支援版本 – Fuji、Geneva、Helsinki。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-224">ServiceNow supported versions – Fuji, Geneva, Helsinki.</span></span>

<span data-ttu-id="2a7aa-225">ServiceNow 管理員必須執行 hello 依照它們的 ServiceNow 執行個體：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-225">ServiceNow Admins must do hello following in their ServiceNow instance:</span></span>
- <span data-ttu-id="2a7aa-226">產生用戶端識別碼和 hello ServiceNow 產品的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-226">Generate client ID and client secret for hello ServiceNow product.</span></span> <span data-ttu-id="2a7aa-227">如需有關如何 toogenerate 用戶端識別碼和密碼，請參閱詳細[OAuth 設定](http://wiki.servicenow.com/index.php?title=OAuth_Setup)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-227">For information on how toogenerate client ID and secret, see [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span>
- <span data-ttu-id="2a7aa-228">安裝 Microsoft OMS 整合 （ServiceNow 的應用程式） 的 hello 使用者應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-228">Install hello User App for Microsoft OMS integration (ServiceNow app).</span></span> <span data-ttu-id="2a7aa-229">[深入了解](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 )。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-229">[Learn more](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).</span></span>
- <span data-ttu-id="2a7aa-230">建立整合 hello 使用者安裝應用程式的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-230">Create integration user role for hello user app installed.</span></span> <span data-ttu-id="2a7aa-231">有關 toocreate hello 整合使用者角色的方式[這裡](#create-integration-user-role-in-servicenow-app)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-231">Information on how toocreate hello integration user role is [here](#create-integration-user-role-in-servicenow-app).</span></span>


### <a name="connection-procedure"></a><span data-ttu-id="2a7aa-232">**連線程序**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-232">**Connection procedure**</span></span>

<span data-ttu-id="2a7aa-233">使用下列程序 toocreate ServiceNow 連接 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-233">Use hello following procedure toocreate a ServiceNow connection:</span></span>

1. <span data-ttu-id="2a7aa-234">跳過**OMS** > **設定** > **連線來源**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-234">Go too**OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="2a7aa-235">選取**ITSM 連接器**，然後按一下新增新的連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-235">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![ServiceNow 連線](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. <span data-ttu-id="2a7aa-237">下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-237">Provide hello information as described in hello following table, and click **Save** toocreate hello connection:</span></span>

> [!NOTE]
> <span data-ttu-id="2a7aa-238">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-238">All these parameters are mandatory.</span></span>

| <span data-ttu-id="2a7aa-239">**欄位**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-239">**Field**</span></span> | <span data-ttu-id="2a7aa-240">**說明**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-240">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="2a7aa-241">**名稱**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-241">**Name**</span></span>   | <span data-ttu-id="2a7aa-242">輸入您想要以 hello IT 服務管理連接器 tooconnect hello ServiceNow 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-242">Type a name for hello ServiceNow instance that you want tooconnect with hello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-243">稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-243">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="2a7aa-244">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-244">**Select Connection type**</span></span>   | <span data-ttu-id="2a7aa-245">選取 **ServiceNow**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-245">Select **ServiceNow**.</span></span> |
| <span data-ttu-id="2a7aa-246">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-246">**Username**</span></span>   | <span data-ttu-id="2a7aa-247">輸入您在 hello ServiceNow 的應用程式 toosupport hello 連接 toohello IT 服務管理連接器中建立的 hello 整合使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-247">Type hello integration user name that you created in hello ServiceNow app toosupport hello connection toohello IT Service Management Connector.</span></span> <span data-ttu-id="2a7aa-248">詳細資訊︰[建立 ServiceNow 應用程式使用者角色](#create-integration-user-role-in-servicenow-app)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-248">More information: [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app).</span></span>|
| <span data-ttu-id="2a7aa-249">**密碼**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-249">**Password**</span></span>   | <span data-ttu-id="2a7aa-250">輸入 hello 這個使用者名稱相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-250">Type hello password associated with this user name.</span></span> <span data-ttu-id="2a7aa-251">**請注意**： 使用者名稱和密碼用來產生驗證權杖，並會不會儲存在 hello OMS 服務中。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-251">**Note**: User name and password are used for generating authentication tokens only, and are not stored anywhere within hello OMS service.</span></span>  |
| <span data-ttu-id="2a7aa-252">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-252">**Server URL**</span></span>   | <span data-ttu-id="2a7aa-253">輸入您想 tooconnect tooIT Service Management Connector hello ServiceNow 執行個體的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-253">Type hello URL of hello ServiceNow instance that you want tooconnect tooIT Service Management Connector.</span></span> |
| <span data-ttu-id="2a7aa-254">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-254">**Client ID**</span></span>   | <span data-ttu-id="2a7aa-255">輸入您想 toouse OAuth2 驗證，您先前產生的 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-255">Type hello client ID that you want toouse for OAuth2 Authentication, which you generated earlier.</span></span>  <span data-ttu-id="2a7aa-256">如需產生用戶端識別碼和祕密的資訊：[OAuth 設定](http://wiki.servicenow.com/index.php?title=OAuth_Setup)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-256">More information on generating client ID and secret:   [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span> |
| <span data-ttu-id="2a7aa-257">**用戶端祕密**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-257">**Client Secret**</span></span>   | <span data-ttu-id="2a7aa-258">型別 hello 用戶端密碼，產生此識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-258">Type hello client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="2a7aa-259">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-259">**Data Sync Scope**</span></span>   | <span data-ttu-id="2a7aa-260">選取您想 toosync tooOMS，透過 hello IT 服務管理連接器的 hello ServiceNow 工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-260">Select hello ServiceNow work items that you want toosync tooOMS, through hello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-261">選取的 hello 值會匯入記錄分析。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-261">hello selected values are imported into log analytics.</span></span>   <span data-ttu-id="2a7aa-262">**選項︰**事件和變更要求。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-262">**Options:**  Incidents and Change Requests.</span></span>|
| <span data-ttu-id="2a7aa-263">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-263">**Sync Data**</span></span> | <span data-ttu-id="2a7aa-264">輸入經過天數 hello 資料從 hello 數的字。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-264">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="2a7aa-265">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-265">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="2a7aa-266">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-266">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="2a7aa-267">如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-267">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="2a7aa-268">選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-268">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="2a7aa-269">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-269">**Default**: disabled.</span></span> |


<span data-ttu-id="2a7aa-270">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="2a7aa-270">When successfully connected, and synced:</span></span>

- <span data-ttu-id="2a7aa-271">從 ServiceNow 連線選取的工作項目將匯入 OMS Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-271">Selected work items from ServiceNow connection are imported into OMS Log Analytics.</span></span>  <span data-ttu-id="2a7aa-272">您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-272">You can view hello summary of these work items on hello IT Service Management Connector tile.</span></span>
- <span data-ttu-id="2a7aa-273">您可以在這個 ServiceNow 執行個體中建立 OMS 警示或記錄搜尋的事件、警示和活動。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-273">You can create incidents, alerts, and events from OMS Alerts or log search in this ServiceNow instance.</span></span>  


<span data-ttu-id="2a7aa-274">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-274">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-integration-user-role-in-servicenow-app"></a><span data-ttu-id="2a7aa-275">在 ServiceNow 應用程式中建立整合使用者角色</span><span class="sxs-lookup"><span data-stu-id="2a7aa-275">Create integration user role in ServiceNow app</span></span>

<span data-ttu-id="2a7aa-276">下列程序的使用者 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-276">User hello following procedure:</span></span>

1.  <span data-ttu-id="2a7aa-277">請瀏覽 hello [ServiceNow 存放區](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0)並安裝 hello **ServiceNow 與 Microsoft OMS 整合的使用者應用程式**到 ServiceNow 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-277">Visit hello [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) and install hello **User App for ServiceNow and Microsoft OMS Integration** into your ServiceNow Instance.</span></span>
2.  <span data-ttu-id="2a7aa-278">安裝之後，請瀏覽 hello 左導覽列的 hello ServiceNow 執行個體、 搜尋和選取 Microsoft OMS 整合器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-278">After installation, visit hello left navigation bar of hello ServiceNow instance, search, and select Microsoft OMS integrator.</span></span>  
3.  <span data-ttu-id="2a7aa-279">按一下 [安裝檢查清單]。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-279">Click **Installation Checklist**.</span></span>

    <span data-ttu-id="2a7aa-280">hello 狀態會顯示為**完成**如果 hello 」 使用者角色，但 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-280">hello status is displayed as  **Not complete** if hello user role is yet toobe created.</span></span>

4.  <span data-ttu-id="2a7aa-281">中的 hello 文字方塊，接下來太**建立整合使用者**，輸入可以連接 toohello IT 服務管理連接器在 OMS 中的 hello 使用者 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-281">In hello text boxes, next too**Create integration user**, enter hello user name for hello user that can connect toohello IT Service Management Connector in OMS.</span></span>
5.  <span data-ttu-id="2a7aa-282">輸入對這個使用者而言 hello 密碼，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-282">Enter hello password for this user, and click **OK**.</span></span>  

>[!NOTE]

> <span data-ttu-id="2a7aa-283">您在 OMS 中使用這些認證 toomake hello ServiceNow 連接。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-283">You use these credentials toomake hello ServiceNow connection in OMS.</span></span>

<span data-ttu-id="2a7aa-284">hello 預設角色指派會顯示 hello 新建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-284">hello newly created user is displayed with hello default roles assigned.</span></span>

<span data-ttu-id="2a7aa-285">預設角色︰</span><span class="sxs-lookup"><span data-stu-id="2a7aa-285">Default roles:</span></span>
- <span data-ttu-id="2a7aa-286">personalize_choices</span><span class="sxs-lookup"><span data-stu-id="2a7aa-286">personalize_choices</span></span>
- <span data-ttu-id="2a7aa-287">import_transformer</span><span class="sxs-lookup"><span data-stu-id="2a7aa-287">import_transformer</span></span>
-   <span data-ttu-id="2a7aa-288">x_mioms_microsoft.user</span><span class="sxs-lookup"><span data-stu-id="2a7aa-288">x_mioms_microsoft.user</span></span>
-   <span data-ttu-id="2a7aa-289">itil</span><span class="sxs-lookup"><span data-stu-id="2a7aa-289">itil</span></span>
-   <span data-ttu-id="2a7aa-290">template_editor</span><span class="sxs-lookup"><span data-stu-id="2a7aa-290">template_editor</span></span>
-   <span data-ttu-id="2a7aa-291">view_changer</span><span class="sxs-lookup"><span data-stu-id="2a7aa-291">view_changer</span></span>

<span data-ttu-id="2a7aa-292">已成功建立 hello 使用者時，一旦 hello 狀態**檢查安裝檢查清單**移動 tooCompleted，列出 hello hello hello 應用程式建立的使用者角色的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-292">Once hello user is successfully created, hello status of **Check Installation Checklist** moves tooCompleted, listing hello details of hello user role created for hello app.</span></span>

> [!NOTE]

> <span data-ttu-id="2a7aa-293">tooallow 使用者 toocreate**警示**和**事件**從 OMS ServiceNow 中：</span><span class="sxs-lookup"><span data-stu-id="2a7aa-293">tooallow a user toocreate **alerts** and **events** in ServiceNow from OMS:</span></span>

> - <span data-ttu-id="2a7aa-294">確定您擁有 hello 事件管理模組已安裝在您的 ServiceNow 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-294">Ensure you have hello Event Management module Installed on your ServiceNow instance.</span></span>

> - <span data-ttu-id="2a7aa-295">新增下列角色 toohello 整合使用者的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-295">Add hello following roles toohello integration user:</span></span>
>      - <span data-ttu-id="2a7aa-296">evt_mgmt_integration</span><span class="sxs-lookup"><span data-stu-id="2a7aa-296">evt_mgmt_integration</span></span>
>      - <span data-ttu-id="2a7aa-297">evt_mgmt_operator</span><span class="sxs-lookup"><span data-stu-id="2a7aa-297">evt_mgmt_operator</span></span>  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a><span data-ttu-id="2a7aa-298">連接 Provance tooIT 在 OMS 中的服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="2a7aa-298">Connect Provance tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="2a7aa-299">hello 下列各節提供詳細說明如何 tooconnect 您 Provance 產品 toohello 在 OMS 中的 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-299">hello following sections provide details about how tooconnect your Provance product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2a7aa-300">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a7aa-300">Prerequisites</span></span>

<span data-ttu-id="2a7aa-301">請確定您有下列必要條件符合 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-301">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="2a7aa-302">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-302">IT Service Management Connector installed.</span></span> <span data-ttu-id="2a7aa-303">詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-303">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="2a7aa-304">應該向 Azure AD 註冊 Provance 應用程式 - 並將用戶端識別碼設為可用。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-304">Provance App should be registered with Azure AD - and client ID is made available.</span></span> <span data-ttu-id="2a7aa-305">如需詳細資訊，請參閱[如何 tooconfigure active directory 驗證](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-305">For detailed information, see [how tooconfigure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
- <span data-ttu-id="2a7aa-306">使用者角色：管理員。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-306">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="2a7aa-307">連線程序</span><span class="sxs-lookup"><span data-stu-id="2a7aa-307">Connection Procedure</span></span>

<span data-ttu-id="2a7aa-308">使用下列程序 toocreate Provance 連接 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-308">Use hello following procedure toocreate a Provance connection:</span></span>

1. <span data-ttu-id="2a7aa-309">跳過**OMS** > **設定** > **連線來源**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-309">Go too**OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="2a7aa-310">選取**ITSM 連接器**，然後按一下新增新的連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-310">Select **ITSM Connector,** click **Add New Connection**.</span></span>  

    ![Provance 連線](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. <span data-ttu-id="2a7aa-312">下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-312">Provide hello information as described in hello following table, and click **Save** toocreate hello connection.</span></span>

> [!NOTE]
> <span data-ttu-id="2a7aa-313">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-313">All these parameters are mandatory.</span></span>

| <span data-ttu-id="2a7aa-314">**欄位**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-314">**Field**</span></span> | <span data-ttu-id="2a7aa-315">**說明**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-315">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="2a7aa-316">**名稱**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-316">**Name**</span></span>   | <span data-ttu-id="2a7aa-317">輸入您想要以 hello IT 服務管理連接器 tooconnect hello Provance 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-317">Type a name for hello Provance instance that you want tooconnect with hello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-318">稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-318">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="2a7aa-319">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-319">**Select Connection type**</span></span>   | <span data-ttu-id="2a7aa-320">選取 [Provance]。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-320">Select **Provance**.</span></span> |
| <span data-ttu-id="2a7aa-321">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-321">**Username**</span></span>   | <span data-ttu-id="2a7aa-322">輸入可以連接 toohello IT 服務管理連接器的 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-322">Type hello user name that can connect toohello IT Service Management Connector.</span></span>    |
| <span data-ttu-id="2a7aa-323">**密碼**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-323">**Password**</span></span>   | <span data-ttu-id="2a7aa-324">輸入 hello 這個使用者名稱相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-324">Type hello password associated with this user name.</span></span> <span data-ttu-id="2a7aa-325">**注意：**使用者名稱和密碼用來產生驗證權杖，並會不會儲存在 hello OMS 服務內。 _</span><span class="sxs-lookup"><span data-stu-id="2a7aa-325">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within hello OMS service._</span></span>|
| <span data-ttu-id="2a7aa-326">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-326">**Server URL**</span></span>   | <span data-ttu-id="2a7aa-327">輸入您想 tooconnect tooIT Service Management Connector Provance 執行個體的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-327">Type hello URL of your Provance instance that you want tooconnect tooIT Service Management Connector.</span></span> |
| <span data-ttu-id="2a7aa-328">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-328">**Client ID**</span></span>   | <span data-ttu-id="2a7aa-329">型別 hello 來驗證此連線，您在 Provance 執行個體中產生的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-329">Type hello client ID for authenticating this connection, which you generated in your Provance instance.</span></span>  <span data-ttu-id="2a7aa-330">在用戶端識別碼的詳細資訊，請參閱[如何 tooconfigure active directory 驗證](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-330">More information on client ID, see [how tooconfigure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> |
| <span data-ttu-id="2a7aa-331">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-331">**Data Sync Scope**</span></span>   | <span data-ttu-id="2a7aa-332">選取您想 toosync tooOMS，透過 hello IT 服務管理連接器的 hello Provance 工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-332">Select hello Provance work items that you want toosync tooOMS, through hello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-333">系統會將這些工作項目匯入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-333">These work items are imported into log analytics.</span></span>   <span data-ttu-id="2a7aa-334">**選項︰**事件、變更要求。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-334">**Options:**   Incidents, Change Requests.</span></span>|
| <span data-ttu-id="2a7aa-335">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-335">**Sync Data**</span></span> | <span data-ttu-id="2a7aa-336">輸入經過天數 hello 資料從 hello 數的字。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-336">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="2a7aa-337">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-337">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="2a7aa-338">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-338">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="2a7aa-339">如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-339">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="2a7aa-340">選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-340">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="2a7aa-341">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-341">**Default**: disabled.</span></span>|

<span data-ttu-id="2a7aa-342">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="2a7aa-342">When successfully connected, and synced:</span></span>

- <span data-ttu-id="2a7aa-343">從 Provance 連線選取的工作項目將匯入 OMS **Log Analytics**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-343">Selected work items from Provance connection are imported into OMS **Log Analytics.**</span></span>  <span data-ttu-id="2a7aa-344">您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-344">You can view hello summary of these work items on hello IT Service Management Connector tile.</span></span>
- <span data-ttu-id="2a7aa-345">您可以在這個 Provance 執行個體中建立 OMS 警示或記錄搜尋的事件和活動。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-345">You can create incidents and events from OMS Alerts or Log Search in this Provance instance.</span></span>

<span data-ttu-id="2a7aa-346">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-346">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a><span data-ttu-id="2a7aa-347">連接 Cherwell tooIT 在 OMS 中的服務管理連接器</span><span class="sxs-lookup"><span data-stu-id="2a7aa-347">Connect Cherwell tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="2a7aa-348">hello 下列各節提供詳細說明如何 tooconnect 您 Cherwell 產品 toohello 在 OMS 中的 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-348">hello following sections provide details about how tooconnect your Cherwell product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2a7aa-349">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a7aa-349">Prerequisites</span></span>

<span data-ttu-id="2a7aa-350">請確定您有下列必要條件符合 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-350">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="2a7aa-351">已安裝 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-351">IT Service Management Connector installed.</span></span> <span data-ttu-id="2a7aa-352">詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-352">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="2a7aa-353">所產生的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-353">Client ID generated.</span></span> <span data-ttu-id="2a7aa-354">詳細資訊︰[產生 Cherwell 的用戶端識別碼](#generate-client-id-for-cherwell)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-354">More information: [Generate client ID for Cherwell](#generate-client-id-for-cherwell).</span></span>
- <span data-ttu-id="2a7aa-355">使用者角色：管理員。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-355">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="2a7aa-356">連線程序</span><span class="sxs-lookup"><span data-stu-id="2a7aa-356">Connection Procedure</span></span>

<span data-ttu-id="2a7aa-357">使用下列程序 toocreate Cherwell 連接 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-357">Use hello following procedure toocreate a Cherwell connection:</span></span>

1. <span data-ttu-id="2a7aa-358">跳過**OMS** >  **設定** > **連線來源**。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-358">Go too**OMS** >  **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="2a7aa-359">選取 ITSM 連接器，然後按一下新增新的連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-359">Select **ITSM Connector** click **Add New Connection**.</span></span>  

    ![Cherwell 使用者識別碼](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. <span data-ttu-id="2a7aa-361">下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-361">Provide hello information as described in hello following table, and click  **Save** toocreate hello connection.</span></span>

> [!NOTE]
> <span data-ttu-id="2a7aa-362">這些全部都是必要參數。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-362">All these parameters are mandatory.</span></span>

| <span data-ttu-id="2a7aa-363">**欄位**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-363">**Field**</span></span> | <span data-ttu-id="2a7aa-364">**說明**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-364">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="2a7aa-365">**名稱**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-365">**Name**</span></span>   | <span data-ttu-id="2a7aa-366">輸入您想 tooconnect toohello IT 服務管理連接器 hello Cherwell 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-366">Type a name for hello Cherwell instance that you want tooconnect toohello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-367">稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-367">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="2a7aa-368">**選取連線類型**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-368">**Select Connection type**</span></span>   | <span data-ttu-id="2a7aa-369">選取 [Cherwell]。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-369">Select **Cherwell.**</span></span> |
| <span data-ttu-id="2a7aa-370">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-370">**Username**</span></span>   | <span data-ttu-id="2a7aa-371">輸入可以連接 toohello IT 服務管理連接器的 hello Cherwell 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-371">Type hello Cherwell user name that can connect toohello IT Service Management Connector.</span></span> |
| <span data-ttu-id="2a7aa-372">**密碼**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-372">**Password**</span></span>   | <span data-ttu-id="2a7aa-373">輸入 hello 這個使用者名稱相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-373">Type hello password associated with this user name.</span></span> <span data-ttu-id="2a7aa-374">**注意：**使用者名稱和密碼用來產生驗證權杖，並會不會儲存在 hello OMS 服務中。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-374">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within hello OMS service.</span></span>|
| <span data-ttu-id="2a7aa-375">**伺服器 URL**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-375">**Server URL**</span></span>   | <span data-ttu-id="2a7aa-376">輸入您想 tooconnect tooIT Service Management Connector Cherwell 執行個體的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-376">Type hello URL of your Cherwell instance that you want tooconnect tooIT Service Management Connector.</span></span> |
| <span data-ttu-id="2a7aa-377">**用戶端識別碼**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-377">**Client ID**</span></span>   | <span data-ttu-id="2a7aa-378">型別 hello 來驗證此連線，您在您 Cherwell 的執行個體中產生的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-378">Type hello client ID for authenticating this connection, which you generated in your Cherwell instance.</span></span>   |
| <span data-ttu-id="2a7aa-379">**資料同步範圍**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-379">**Data Sync Scope**</span></span>   | <span data-ttu-id="2a7aa-380">選取您想透過 hello IT 服務管理連接器 toosync 的 hello Cherwell 工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-380">Select hello Cherwell work items that you want toosync through hello IT Service Management Connector.</span></span>  <span data-ttu-id="2a7aa-381">系統會將這些工作項目匯入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-381">These work items are imported into log analytics.</span></span>   <span data-ttu-id="2a7aa-382">**選項︰**事件、變更要求。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-382">**Options:**  Incidents, Change Requests.</span></span> |
| <span data-ttu-id="2a7aa-383">**同步資料**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-383">**Sync Data**</span></span> | <span data-ttu-id="2a7aa-384">輸入經過天數 hello 資料從 hello 數的字。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-384">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="2a7aa-385">**上限**：120 天。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-385">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="2a7aa-386">**在 ITSM 解決方案中建立新的設定項目**</span><span class="sxs-lookup"><span data-stu-id="2a7aa-386">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="2a7aa-387">如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-387">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="2a7aa-388">選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-388">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="2a7aa-389">**預設**︰停用。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-389">**Default**: disabled.</span></span> |

<span data-ttu-id="2a7aa-390">順利連線並同步處理時︰</span><span class="sxs-lookup"><span data-stu-id="2a7aa-390">When successfully connected, and synced:</span></span>

- <span data-ttu-id="2a7aa-391">從這個 Cherwell 連線選取的工作項目將匯入 OMS Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-391">Selected work items from this Cherwell connection are imported into OMS Log Analytics.</span></span> <span data-ttu-id="2a7aa-392">您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-392">You can view hello summary of these work items  on hello IT Service Management Connector tile.</span></span>
- <span data-ttu-id="2a7aa-393">您可以從 OMS 建立這個 Cherwell 執行個體的事件和活動。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-393">You can create incidents and events in this Cherwell instance from OMS.</span></span> <span data-ttu-id="2a7aa-394">詳細資訊︰建立 OMS 警示的 ITSM工作項目及建立 OMS 記錄的 ITSM 工作項目。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-394">More information: Create ITSM work items for OMS alerts and Create ITSM work items from OMS logs.</span></span>

<span data-ttu-id="2a7aa-395">詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-395">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="generate-client-id-for-cherwell"></a><span data-ttu-id="2a7aa-396">產生 Cherwell 的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="2a7aa-396">Generate client ID for Cherwell</span></span>

<span data-ttu-id="2a7aa-397">toogenerate hello cherwell 的用戶端識別碼/金鑰，請使用下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7aa-397">toogenerate hello client ID/key for Cherwell, use hello following procedure:</span></span>

1. <span data-ttu-id="2a7aa-398">登入 tooyour Cherwell 的執行個體為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-398">Log in tooyour Cherwell instance as admin.</span></span>
2. <span data-ttu-id="2a7aa-399">按一下 [安全性] > [編輯 REST API 用戶端設定]。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-399">Click **Security** > **Edit REST API client settings**.</span></span>
3. <span data-ttu-id="2a7aa-400">選取 [建立新的用戶端] > [用戶端祕密]。</span><span class="sxs-lookup"><span data-stu-id="2a7aa-400">Select **Create new client** > **client secret**.</span></span>

    ![Cherwell 使用者識別碼](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a><span data-ttu-id="2a7aa-402">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a7aa-402">Next steps</span></span>
 - [<span data-ttu-id="2a7aa-403">建立 OMS 警示的 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="2a7aa-403">Create ITSM work items for OMS alerts</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [<span data-ttu-id="2a7aa-404">從 OMS 記錄建立 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="2a7aa-404">Create ITSM work items from OMS logs</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [<span data-ttu-id="2a7aa-405">檢視您連線的 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2a7aa-405">View log analytics for your connection</span></span>](log-analytics-itsmc-overview.md#using-the-solution)
