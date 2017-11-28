---
title: "將 Configuration Manager 連線至 Log Analytics | Microsoft Docs"
description: "本文說明將 Configuration Manager 連線至 Log Analytics 並開始分析資料的步驟。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: 62d31ed486458245156f7fc832294d662c62991e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-configuration-manager-to-log-analytics"></a><span data-ttu-id="55340-103">將 Configuration Manager 連線至 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="55340-103">Connect Configuration Manager to Log Analytics</span></span>
<span data-ttu-id="55340-104">您可以在 OMS 中將 System Center Configuration Manager 連線至 Log Analytics 來同步處理裝置集合資料。</span><span class="sxs-lookup"><span data-stu-id="55340-104">You can connect System Center Configuration Manager to Log Analytics in OMS to sync device collection data.</span></span> <span data-ttu-id="55340-105">這可讓 Configuration Manager 階層中的資料可在 OMS 中使用。</span><span class="sxs-lookup"><span data-stu-id="55340-105">This makes data from your Configuration Manager hierarchy available in OMS.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55340-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="55340-106">Prerequisites</span></span>

<span data-ttu-id="55340-107">Log Analytics 支援 System Center Configuration Manager 目前分支，1606 版和更高版本。</span><span class="sxs-lookup"><span data-stu-id="55340-107">Log Analytics supports System Center Configuration Manager current branch, version 1606 and higher.</span></span>  

## <a name="configuration-overview"></a><span data-ttu-id="55340-108">組態概觀</span><span class="sxs-lookup"><span data-stu-id="55340-108">Configuration overview</span></span>
<span data-ttu-id="55340-109">下列步驟摘要說明將 Configuration Manager 連線至 Log Analytics 的程序。</span><span class="sxs-lookup"><span data-stu-id="55340-109">The following steps summarizes the process to connect Configuration Manager to Log Analytics.</span></span>  

1. <span data-ttu-id="55340-110">在 Azure 管理入口網站中，將 Configuration Manager 註冊為 Web 應用程式和/或 Web API 應用程式，並確保您擁有 Azure Active Directory 註冊中的用戶端識別碼和用戶端秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="55340-110">In the Azure Management Portal, register Configuration Manager as a Web Application and/or Web API app, and ensure that you have the client ID and client secret key from the registration from Azure Active Directory.</span></span> <span data-ttu-id="55340-111">如需如何完成此步驟的詳細資訊，請參閱[使用入口網站來建立可存取資源的 Active Directory 應用程式和服務主體](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="55340-111">See [Use portal to create Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md) for detailed information about how accomplish this step.</span></span>
2. <span data-ttu-id="55340-112">在 Azure 管理入口網站中，[為 Configuration Manager (已註冊的 Web 應用程式) 提供存取 OMS 的權限](#provide-configuration-manager-with-permissions-to-oms)。</span><span class="sxs-lookup"><span data-stu-id="55340-112">In the Azure Management Portal, [provide Configuration Manager (the registered web app) with permission to access OMS](#provide-configuration-manager-with-permissions-to-oms).</span></span>
3. <span data-ttu-id="55340-113">在 Configuration Manager 中，[使用新增 OMS 連線精靈新增連線](#add-an-oms-connection-to-configuration-manager)。</span><span class="sxs-lookup"><span data-stu-id="55340-113">In Configuration Manager, [add a connection using the Add OMS Connection Wizard](#add-an-oms-connection-to-configuration-manager).</span></span>
4. <span data-ttu-id="55340-114">如果密碼或用戶端祕密金鑰過期或遺失，在 Configuration Manager 中[更新連線屬性](#update-oms-connection-properties)。</span><span class="sxs-lookup"><span data-stu-id="55340-114">In Configuration Manager, [update the connection properties](#update-oms-connection-properties) if the password or client secret key ever expires or is lost.</span></span>
5. <span data-ttu-id="55340-115">使用 OMS 入口網站的資訊，在執行 Configuration Manager 服務連線點網站系統角色的電腦上[下載並安裝 Microsoft Monitoring Agent](#download-and-install-the-agent)。</span><span class="sxs-lookup"><span data-stu-id="55340-115">With information from the OMS portal, [download and install the Microsoft Monitoring Agent](#download-and-install-the-agent) on the computer running the Configuration Manager service connection point site system role.</span></span> <span data-ttu-id="55340-116">代理程式會將 Configuration Manager 資料傳送至 OMS。</span><span class="sxs-lookup"><span data-stu-id="55340-116">The agent sends Configuration Manager data to OMS.</span></span>
6. <span data-ttu-id="55340-117">在 Log Analytics 中，以電腦群組的形式[從 Configuration Manager 匯入集合](#import-collections)。</span><span class="sxs-lookup"><span data-stu-id="55340-117">In Log Analytics, [import collections from Configuration Manager](#import-collections) as computer groups.</span></span>
7. <span data-ttu-id="55340-118">在 Log Analytics 中，以電腦群組的形式[從 Configuration Manager 檢視資料](log-analytics-computer-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="55340-118">In Log Analytics, view data from Configuration Manager as [computer groups](log-analytics-computer-groups.md).</span></span>

<span data-ttu-id="55340-119">若要深入了解如何將 Configuration Manager 連線至 OMS，請參閱[將資料從 Configuration Manager 同步處理至 Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx)。</span><span class="sxs-lookup"><span data-stu-id="55340-119">You can read more about connecting Configuration Manager to OMS at [Sync data from Configuration Manager to the Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).</span></span>

## <a name="provide-configuration-manager-with-permissions-to-oms"></a><span data-ttu-id="55340-120">為 Configuration Manager 提供 OMS 的權限</span><span class="sxs-lookup"><span data-stu-id="55340-120">Provide Configuration Manager with permissions to OMS</span></span>
<span data-ttu-id="55340-121">下列程序可為 Azure 管理入口網站提供存取 OMS 的權限。</span><span class="sxs-lookup"><span data-stu-id="55340-121">The following procedure provides the Azure Management Portal with permissions to access OMS.</span></span> <span data-ttu-id="55340-122">具體來說，您必須授與參與者角色給資源群組中的使用者，以允許 Azure 管理入口網站將 Configuration Manager 連線至 OMS。</span><span class="sxs-lookup"><span data-stu-id="55340-122">Specifically, you must grant the *Contributor role* to users in the resource group in order to allow the Azure Management Portal to connect Configuration Manager to OMS.</span></span>

> [!NOTE]
> <span data-ttu-id="55340-123">您必須為 Configuration Manager 指定 OMS 的權限。</span><span class="sxs-lookup"><span data-stu-id="55340-123">You must specify permissions in OMS for Configuration Manager.</span></span> <span data-ttu-id="55340-124">否則，當您在 Configuration Manager 中使用組態精靈時，將會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="55340-124">Otherwise, you'll receive an error message when you use the configuration wizard in Configuration Manager.</span></span>
>
>

1. <span data-ttu-id="55340-125">開啟 [Azure 入口網站](https://portal.azure.com/)，然後按一下 [瀏覽] > [Log Analytics (OMS)] 以開啟 [Log Analytics (OMS)] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55340-125">Open the [Azure portal](https://portal.azure.com/) and click **Browse** > **Log Analytics (OMS)** to open the Log Analytics (OMS) blade.</span></span>  
2. <span data-ttu-id="55340-126">在 [Log Analytics (OMS)] 刀鋒視窗上按一下 [新增]，開啟 [OMS 工作區] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55340-126">On the **Log Analytics (OMS)** blade, click **Add** to open the **OMS Workspace** blade.</span></span>  
   <span data-ttu-id="55340-127">![OMS 刀鋒視窗](./media/log-analytics-sccm/sccm-azure01.png)</span><span class="sxs-lookup"><span data-stu-id="55340-127">![OMS blade](./media/log-analytics-sccm/sccm-azure01.png)</span></span>
3. <span data-ttu-id="55340-128">在 [OMS 工作區] 刀鋒視窗上提供下列資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="55340-128">On the **OMS Workspace** blade, provide the following information and then click **OK**.</span></span>

   * <span data-ttu-id="55340-129">**OMS 工作區**</span><span class="sxs-lookup"><span data-stu-id="55340-129">**OMS Workspace**</span></span>
   * <span data-ttu-id="55340-130">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="55340-130">**Subscription**</span></span>
   * <span data-ttu-id="55340-131">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="55340-131">**Resource group**</span></span>
   * <span data-ttu-id="55340-132">**位置**</span><span class="sxs-lookup"><span data-stu-id="55340-132">**Location**</span></span>
   * <span data-ttu-id="55340-133">**定價層**</span><span class="sxs-lookup"><span data-stu-id="55340-133">**Pricing tier**</span></span>  
     <span data-ttu-id="55340-134">![OMS 刀鋒視窗](./media/log-analytics-sccm/sccm-azure02.png)</span><span class="sxs-lookup"><span data-stu-id="55340-134">![OMS blade](./media/log-analytics-sccm/sccm-azure02.png)</span></span>  

     > [!NOTE]
     > <span data-ttu-id="55340-135">上述範例會建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="55340-135">The example above creates a new resource group.</span></span> <span data-ttu-id="55340-136">在此範例中，資源群組只會用來為 Configuration Manager 提供 OMS 工作區的權限。</span><span class="sxs-lookup"><span data-stu-id="55340-136">The resource group is only used to provide Configuration Manager with permissions to the OMS workspace in this example.</span></span>
     >
     >
4. <span data-ttu-id="55340-137">按一下 [瀏覽] > [資源群組]，開啟 [資源群組] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55340-137">Click **Browse** > **Resource groups** to open the **Resource groups** blade.</span></span>
5. <span data-ttu-id="55340-138">在 [資源群組] 刀鋒視窗中按一下您先前建立的資源群組，開啟 [&lt;資源群組名稱&gt; 設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55340-138">In the **Resource groups** blade, click the resource group that you created above to open the &lt;resource group name&gt; settings blade.</span></span>  
   <span data-ttu-id="55340-139">![資源群組設定刀鋒視窗](./media/log-analytics-sccm/sccm-azure03.png)</span><span class="sxs-lookup"><span data-stu-id="55340-139">![resource group settings blade](./media/log-analytics-sccm/sccm-azure03.png)</span></span>
6. <span data-ttu-id="55340-140">在 [&lt;資源群組名稱&gt; 設定] 刀鋒視窗中按一下 [存取控制 (IAM)]，開啟 [&lt;資源群組名稱&gt; 使用者] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55340-140">In the &lt;resource group name&gt; settings blade, click Access control (IAM) to open the &lt;resource group name&gt; Users blade.</span></span>  
   ![資源群組使用者刀鋒視窗](./media/log-analytics-sccm/sccm-azure04.png)  
7. <span data-ttu-id="55340-142">在 [&lt;資源群組名稱&gt; 使用者] 刀鋒視窗中按一下 [新增]，開啟 [新增存取] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55340-142">In the &lt;resource group name&gt; Users blade, click **Add** to open the **Add access** blade.</span></span>
8. <span data-ttu-id="55340-143">在 [新增存取] 刀鋒視窗中按一下 [選取角色]，然後選取 [參與者] 角色。</span><span class="sxs-lookup"><span data-stu-id="55340-143">In the **Add access** blade, click **Select a role**, and then select the **Contributor** role.</span></span>  
   <span data-ttu-id="55340-144">![選取角色](./media/log-analytics-sccm/sccm-azure05.png)</span><span class="sxs-lookup"><span data-stu-id="55340-144">![select a role](./media/log-analytics-sccm/sccm-azure05.png)</span></span>  
9. <span data-ttu-id="55340-145">按一下 [新增使用者]，選取 Configuration Manager 使用者，然後依序按一下 [選取] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="55340-145">Click **Add users**, select the Configuration Manager user, click **Select**, and then click **OK**.</span></span>  
   <span data-ttu-id="55340-146">![新增使用者](./media/log-analytics-sccm/sccm-azure06.png)</span><span class="sxs-lookup"><span data-stu-id="55340-146">![add users](./media/log-analytics-sccm/sccm-azure06.png)</span></span>  

## <a name="add-an-oms-connection-to-configuration-manager"></a><span data-ttu-id="55340-147">對 Configuration Manager 新增 OMS 連線</span><span class="sxs-lookup"><span data-stu-id="55340-147">Add an OMS connection to Configuration Manager</span></span>
<span data-ttu-id="55340-148">若要新增 OMS 連線，Configuration Manager 環境的[服務連線點](https://technet.microsoft.com/library/mt627781.aspx)必須設定成線上模式。</span><span class="sxs-lookup"><span data-stu-id="55340-148">In order to add an OMS connection, your Configuration Manager environment must have a [service connection point](https://technet.microsoft.com/library/mt627781.aspx) configured for online mode.</span></span>

1. <span data-ttu-id="55340-149">在 Configuration Manager 的 [管理] 工作區中選取 [OMS 連接器]。</span><span class="sxs-lookup"><span data-stu-id="55340-149">In the **Administration** workspace of Configuration Manager, select **OMS Connector**.</span></span> <span data-ttu-id="55340-150">這會開啟**新增 OMS 連線精靈**。</span><span class="sxs-lookup"><span data-stu-id="55340-150">This opens the **Add OMS Connection Wizard**.</span></span> <span data-ttu-id="55340-151">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="55340-151">Select **Next**.</span></span>
2. <span data-ttu-id="55340-152">在 [一般] 畫面上，確認您已完成下列動作而且您有每個項目的詳細資料，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="55340-152">On the **General** screen, confirm that you have done the following actions and that you have details for each item, then select **Next**.</span></span>

   1. <span data-ttu-id="55340-153">在 Azure 管理入口網站中，您已將 Configuration Manager 註冊為 Web 應用程式和/或 Web API 應用程式，而且您擁有[註冊中的用戶端識別碼](../active-directory/active-directory-integrating-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="55340-153">In the Azure Management Portal, you've registered Configuration Manager as a Web Application and/or Web API app, and that you have the [client ID from the registration](../active-directory/active-directory-integrating-applications.md).</span></span>
   2. <span data-ttu-id="55340-154">在 Azure 管理入口網站中，您已經為 Azure Active Directory 中已註冊的應用程式建立應用程式祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="55340-154">In the Azure Management Portal, you've created an app secret key for the registered app in Azure Active Directory.</span></span>  
   3. <span data-ttu-id="55340-155">在 Azure 管理入口網站中，您已經為已註冊的 Web 應用程式提供存取 OMS 的權限。</span><span class="sxs-lookup"><span data-stu-id="55340-155">In the Azure Management Portal, you've provided the registered web app with permission to access OMS.</span></span>  
      ![OMS 連線精靈的一般頁面](./media/log-analytics-sccm/sccm-console-general01.png)
3. <span data-ttu-id="55340-157">在 [Azure Active Directory] 畫面上對 OMS 設定連線設定 (方法是提供 [租用戶]、[用戶端識別碼] 和 [用戶端秘密金鑰])，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="55340-157">On the **Azure Active Directory** screen, configure your connection settings to OMS by providing your **Tenant** , **Client ID** , and **Client Secret Key** , then select **Next**.</span></span>  
   <span data-ttu-id="55340-158">![OMS 連線精靈的 Azure Active Directory 頁面](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)</span><span class="sxs-lookup"><span data-stu-id="55340-158">![Connection to OMS Wizard Azure Active Directory page](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)</span></span>
4. <span data-ttu-id="55340-159">如果您成功完成其他所有程序，則 [OMS 連線組態] 畫面上的資訊會自動出現在此頁面。</span><span class="sxs-lookup"><span data-stu-id="55340-159">If you accomplished all the other procedures successfully, then the information on the **OMS Connection Configuration** screen will automatically appear on this page.</span></span> <span data-ttu-id="55340-160">[Azure 訂用帳戶]、[Azure 資源群組] 和 [Operations Management Suite 工作區] 應該會出現連線設定資訊。</span><span class="sxs-lookup"><span data-stu-id="55340-160">Information for the connection settings should appear for your **Azure subscription** , **Azure resource group** , and **Operations Management Suite Workspace**.</span></span>  
   <span data-ttu-id="55340-161">![OMS 連線精靈的 OMS 連線頁面](./media/log-analytics-sccm/sccm-wizard-configure04.png)</span><span class="sxs-lookup"><span data-stu-id="55340-161">![Connection to OMS Wizard OMS Connection page](./media/log-analytics-sccm/sccm-wizard-configure04.png)</span></span>
5. <span data-ttu-id="55340-162">精靈會使用您輸入的資訊連線至 OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="55340-162">The wizard connects to the OMS service using the information you've input.</span></span> <span data-ttu-id="55340-163">選取想要與 OMS 同步處理的裝置集合，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="55340-163">Select the device collections that you want to sync with OMS and then click **Add**.</span></span>  
   <span data-ttu-id="55340-164">![選取集合](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)</span><span class="sxs-lookup"><span data-stu-id="55340-164">![Select Collections](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)</span></span>
6. <span data-ttu-id="55340-165">確認 [摘要] 畫面上的連線設定，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="55340-165">Verify your connection settings on the **Summary** screen, then select **Next**.</span></span> <span data-ttu-id="55340-166">[進度] 畫面會顯示連線狀態，然後應該 [完成]。</span><span class="sxs-lookup"><span data-stu-id="55340-166">The **Progress** screen shows the connection status, then should **Complete**.</span></span>

> [!NOTE]
> <span data-ttu-id="55340-167">您必須將 OMS 連線至階層中的最上層網站。</span><span class="sxs-lookup"><span data-stu-id="55340-167">You must connect OMS to the top-tier site in your hierarchy.</span></span> <span data-ttu-id="55340-168">如果您將 OMS 連線至獨立主要網站，然後在環境中新增管理中心網站，則必須在新階層內先刪除再重新建立 OMS 連線。</span><span class="sxs-lookup"><span data-stu-id="55340-168">If you connect OMS to a standalone primary site and then add a central administration site to your environment, you'll have to delete and recreate the OMS connection within the new hierarchy.</span></span>
>
>

<span data-ttu-id="55340-169">在將 Configuration Manager 連結至 OMS 之後，您可以新增或移除集合，並檢視 OMS 連線的屬性。</span><span class="sxs-lookup"><span data-stu-id="55340-169">After you have linked Configuration Manager to OMS, you can add or remove collections, and view the properties of the OMS connection.</span></span>

## <a name="update-oms-connection-properties"></a><span data-ttu-id="55340-170">更新 OMS 連線屬性</span><span class="sxs-lookup"><span data-stu-id="55340-170">Update OMS connection properties</span></span>
<span data-ttu-id="55340-171">如果密碼或用戶端秘密金鑰過期或遺失，您必須手動更新 OMS 連線屬性。</span><span class="sxs-lookup"><span data-stu-id="55340-171">If a password or client secret key ever expires or is lost, you'll need to manually update the OMS connection properties.</span></span>

1. <span data-ttu-id="55340-172">在 Configuration Manager 中瀏覽至 [雲端服務]，然後選取 [OMS 連接器] 以開啟 [OMS 連線屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="55340-172">In Configuration Manager, navigate to **Cloud Services** , then select **OMS Connector** to open the **OMS Connection Properties** page.</span></span>
2. <span data-ttu-id="55340-173">在此頁面上按一下 [Azure Active Directory] 索引標籤，檢視 [租用戶]、[用戶端識別碼] 和 [用戶端秘密金鑰到期]。</span><span class="sxs-lookup"><span data-stu-id="55340-173">On this page, click the **Azure Active Directory** tab to view your **Tenant**, **Client ID**, **Client secret key expiration**.</span></span> <span data-ttu-id="55340-174">**確認****用戶端秘密金鑰**是否已過期。</span><span class="sxs-lookup"><span data-stu-id="55340-174">**Verify** your **Client secret key** if it has expired.</span></span>

## <a name="download-and-install-the-agent"></a><span data-ttu-id="55340-175">下載並安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="55340-175">Download and install the agent</span></span>
1. <span data-ttu-id="55340-176">在 OMS 入口網站中，[從 OMS 下載代理程式安裝檔案](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms)。</span><span class="sxs-lookup"><span data-stu-id="55340-176">In the OMS portal, [Download the agent setup file from OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).</span></span>
2. <span data-ttu-id="55340-177">使用下列其中一個方法，在執行 Configuration Manager 服務連線點網站系統角色的電腦上安裝並設定代理程式：</span><span class="sxs-lookup"><span data-stu-id="55340-177">Use one of the following methods to install and configure the agent on the computer running the Configuration Manager service connection point site system role:</span></span>
   * [<span data-ttu-id="55340-178">使用安裝程式安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="55340-178">Install the agent using setup</span></span>](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [<span data-ttu-id="55340-179">使用命令列安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="55340-179">Install the agent using the command line</span></span>](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [<span data-ttu-id="55340-180">使用 Azure 自動化中的 DSC 安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="55340-180">Install the agent using DSC in Azure Automation</span></span>](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a><span data-ttu-id="55340-181">匯入集合</span><span class="sxs-lookup"><span data-stu-id="55340-181">Import collections</span></span>
<span data-ttu-id="55340-182">在 Configuration Manager 新增了 OMS 連線，並在執行 Configuration Manager 服務連線點網站系統角色的電腦上安裝了代理程式之後，下一個步驟是從 Configuration Manager 將集合匯入 OMS 中做為電腦群組。</span><span class="sxs-lookup"><span data-stu-id="55340-182">After you've added an OMS connection to Configuration Manager and installed the agent on the computer running the Configuration Manager service connection point site system role, the next step is to import collections from Configuration Manager in OMS as computer groups.</span></span>

<span data-ttu-id="55340-183">啟用匯入之後，每 3 個小時就會擷取一次集合成員資格資訊，以便集合成員資格會隨時保持最新狀態。</span><span class="sxs-lookup"><span data-stu-id="55340-183">After importation is enabled, the collection membership information is retrieved every 3 hours to keep the collection memberships current.</span></span> <span data-ttu-id="55340-184">您可以隨時選擇停用匯入。</span><span class="sxs-lookup"><span data-stu-id="55340-184">You can choose to disable importation at any time.</span></span>

1. <span data-ttu-id="55340-185">在 OMS 入口網站中，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="55340-185">In the OMS portal, click **Settings**.</span></span>
2. <span data-ttu-id="55340-186">按一下 [電腦群組] 索引標籤，然後按一下 [SCCM] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="55340-186">Click the **Computer Groups** tab and then click the **SCCM** tab.</span></span>
3. <span data-ttu-id="55340-187">選取 [匯入 Configuration Manager 集合成員資格]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="55340-187">Select **Import Configuration Manager collection memberships** and then click **Save**.</span></span>  
   <span data-ttu-id="55340-188">![電腦群組 - SCCM 索引標籤](./media/log-analytics-sccm/sccm-computer-groups01.png)</span><span class="sxs-lookup"><span data-stu-id="55340-188">![Computer Groups - SCCM tab](./media/log-analytics-sccm/sccm-computer-groups01.png)</span></span>

## <a name="view-data-from-configuration-manager"></a><span data-ttu-id="55340-189">從 Configuration Manager 檢視資料</span><span class="sxs-lookup"><span data-stu-id="55340-189">View data from Configuration Manager</span></span>
<span data-ttu-id="55340-190">在 Configuration Manager 新增了 OMS 連線，並在執行 Configuration Manager 服務連線點網站系統角色的電腦上安裝了代理程式之後，代理程式的資料會傳送至 OMS。</span><span class="sxs-lookup"><span data-stu-id="55340-190">After you've added an OMS connection to Configuration Manager and installed the agent on the computer running the Configuration Manager service connection point site system role, data from the agent is sent to OMS.</span></span> <span data-ttu-id="55340-191">在 OMS 中，Configuration Manager 集合會顯示為[電腦群組](log-analytics-computer-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="55340-191">In OMS, your Configuration Manager collections appear as [computer groups](log-analytics-computer-groups.md).</span></span> <span data-ttu-id="55340-192">您可以從 [設定] 中 [電腦群組]下的 [Configuration Manager] 頁面檢視群組。</span><span class="sxs-lookup"><span data-stu-id="55340-192">You can view the groups from the **Configuration Manager** page under **Computer Groups** in **Settings**.</span></span>

<span data-ttu-id="55340-193">匯入集合之後，您可以看到已偵測到多少部具有集合成員資格的電腦。</span><span class="sxs-lookup"><span data-stu-id="55340-193">After the collections are imported, you can see how many computers with collection memberships have been detected.</span></span> <span data-ttu-id="55340-194">您也可以看到已匯入的集合數目。</span><span class="sxs-lookup"><span data-stu-id="55340-194">You can also see the number of collections that have been imported.</span></span>

![電腦群組 - SCCM 索引標籤](./media/log-analytics-sccm/sccm-computer-groups02.png)

<span data-ttu-id="55340-196">當您按一下其中一項時，[搜尋] 會開啟，顯示所有匯入的群組或是屬於每個群組的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="55340-196">When you click either one, Search opens, displaying either all of the imported groups or all computers that belong to each group.</span></span> <span data-ttu-id="55340-197">使用 [記錄搜尋](log-analytics-log-searches.md)，您就可以開始深入分析 Configuration Manager 資料。</span><span class="sxs-lookup"><span data-stu-id="55340-197">Using [Log Search](log-analytics-log-searches.md), you can start in-depth analysis of Configuration Manager data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55340-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55340-198">Next steps</span></span>
* <span data-ttu-id="55340-199">請使用 [記錄檔搜尋](log-analytics-log-searches.md)，檢視有關 Configuration Manager 資料的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="55340-199">Use [Log Search](log-analytics-log-searches.md) to view detailed information about your Configuration Manager data.</span></span>
