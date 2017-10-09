---
title: "Configuration Manager tooLog 分析 aaaConnect |Microsoft 文件"
description: "本文示範 hello 步驟 tooconnect Configuration Manager tooLog 分析和分析資料的開始。"
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
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a><span data-ttu-id="f6b21-103">Connect Configuration Manager tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="f6b21-103">Connect Configuration Manager tooLog Analytics</span></span>
<span data-ttu-id="f6b21-104">您可以連接 System Center Configuration Manager tooLog 分析 OMS toosync 裝置收集資料。</span><span class="sxs-lookup"><span data-stu-id="f6b21-104">You can connect System Center Configuration Manager tooLog Analytics in OMS toosync device collection data.</span></span> <span data-ttu-id="f6b21-105">這可讓 Configuration Manager 階層中的資料可在 OMS 中使用。</span><span class="sxs-lookup"><span data-stu-id="f6b21-105">This makes data from your Configuration Manager hierarchy available in OMS.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6b21-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="f6b21-106">Prerequisites</span></span>

<span data-ttu-id="f6b21-107">Log Analytics 支援 System Center Configuration Manager 目前分支，1606 版和更高版本。</span><span class="sxs-lookup"><span data-stu-id="f6b21-107">Log Analytics supports System Center Configuration Manager current branch, version 1606 and higher.</span></span>  

## <a name="configuration-overview"></a><span data-ttu-id="f6b21-108">組態概觀</span><span class="sxs-lookup"><span data-stu-id="f6b21-108">Configuration overview</span></span>
<span data-ttu-id="f6b21-109">hello 步驟摘要說明 hello 程序 tooconnect Configuration Manager tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="f6b21-109">hello following steps summarizes hello process tooconnect Configuration Manager tooLog Analytics.</span></span>  

1. <span data-ttu-id="f6b21-110">在 hello Azure 管理入口網站中，Configuration Manager 登錄為 Web 應用程式和/或 Web API 的應用程式，並確認您擁有 hello 用戶端識別碼和用戶端秘密金鑰與 Azure Active Directory 中的 hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="f6b21-110">In hello Azure Management Portal, register Configuration Manager as a Web Application and/or Web API app, and ensure that you have hello client ID and client secret key from hello registration from Azure Active Directory.</span></span> <span data-ttu-id="f6b21-111">請參閱[使用入口網站 toocreate Active Directory 應用程式和服務主體可存取資源](../azure-resource-manager/resource-group-create-service-principal-portal.md)如需如何完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="f6b21-111">See [Use portal toocreate Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md) for detailed information about how accomplish this step.</span></span>
2. <span data-ttu-id="f6b21-112">在 hello Azure 管理入口網站中， [Configuration Manager （hello 註冊的 web 應用程式） 提供權限 tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-112">In hello Azure Management Portal, [provide Configuration Manager (hello registered web app) with permission tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).</span></span>
3. <span data-ttu-id="f6b21-113">在 Configuration Manager[新增連線使用 hello 加入 OMS 連線精靈](#add-an-oms-connection-to-configuration-manager)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-113">In Configuration Manager, [add a connection using hello Add OMS Connection Wizard](#add-an-oms-connection-to-configuration-manager).</span></span>
4. <span data-ttu-id="f6b21-114">在 Configuration Manager[更新 hello 連接屬性](#update-oms-connection-properties)如果 hello 密碼或用戶端秘密金鑰曾經過期，或遺失。</span><span class="sxs-lookup"><span data-stu-id="f6b21-114">In Configuration Manager, [update hello connection properties](#update-oms-connection-properties) if hello password or client secret key ever expires or is lost.</span></span>
5. <span data-ttu-id="f6b21-115">Hello OMS 入口網站，從資訊[下載並安裝 Microsoft Monitoring Agent hello](#download-and-install-the-agent) hello 電腦執行 hello Configuration Manager 服務連線點站台系統角色。</span><span class="sxs-lookup"><span data-stu-id="f6b21-115">With information from hello OMS portal, [download and install hello Microsoft Monitoring Agent](#download-and-install-the-agent) on hello computer running hello Configuration Manager service connection point site system role.</span></span> <span data-ttu-id="f6b21-116">hello 代理程式會將 Configuration Manager 資料 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="f6b21-116">hello agent sends Configuration Manager data tooOMS.</span></span>
6. <span data-ttu-id="f6b21-117">在 Log Analytics 中，以電腦群組的形式[從 Configuration Manager 匯入集合](#import-collections)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-117">In Log Analytics, [import collections from Configuration Manager](#import-collections) as computer groups.</span></span>
7. <span data-ttu-id="f6b21-118">在 Log Analytics 中，以電腦群組的形式[從 Configuration Manager 檢視資料](log-analytics-computer-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-118">In Log Analytics, view data from Configuration Manager as [computer groups](log-analytics-computer-groups.md).</span></span>

<span data-ttu-id="f6b21-119">閱讀更多有關連接在 Configuration Manager tooOMS [Configuration Manager toohello Microsoft Operations Management Suite 中的資料同步](https://technet.microsoft.com/library/mt757374.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-119">You can read more about connecting Configuration Manager tooOMS at [Sync data from Configuration Manager toohello Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).</span></span>

## <a name="provide-configuration-manager-with-permissions-toooms"></a><span data-ttu-id="f6b21-120">Configuration Manager 提供權限 tooOMS</span><span class="sxs-lookup"><span data-stu-id="f6b21-120">Provide Configuration Manager with permissions tooOMS</span></span>
<span data-ttu-id="f6b21-121">hello 下列程序提供具有權限 tooaccess OMS hello Azure 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="f6b21-121">hello following procedure provides hello Azure Management Portal with permissions tooaccess OMS.</span></span> <span data-ttu-id="f6b21-122">具體來說，您必須授與 hello*參與者角色*hello 資源群組中的順序 tooallow toousers hello Azure 管理入口網站 tooconnect Configuration Manager tooOMS。</span><span class="sxs-lookup"><span data-stu-id="f6b21-122">Specifically, you must grant hello *Contributor role* toousers in hello resource group in order tooallow hello Azure Management Portal tooconnect Configuration Manager tooOMS.</span></span>

> [!NOTE]
> <span data-ttu-id="f6b21-123">您必須為 Configuration Manager 指定 OMS 的權限。</span><span class="sxs-lookup"><span data-stu-id="f6b21-123">You must specify permissions in OMS for Configuration Manager.</span></span> <span data-ttu-id="f6b21-124">否則，您就會收到錯誤訊息 Configuration Manager 中使用 hello 組態精靈。</span><span class="sxs-lookup"><span data-stu-id="f6b21-124">Otherwise, you'll receive an error message when you use hello configuration wizard in Configuration Manager.</span></span>
>
>

1. <span data-ttu-id="f6b21-125">開啟 hello [Azure 入口網站](https://portal.azure.com/)按一下**瀏覽** > **記錄分析 (OMS)** tooopen hello 記錄分析 (OMS) 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6b21-125">Open hello [Azure portal](https://portal.azure.com/) and click **Browse** > **Log Analytics (OMS)** tooopen hello Log Analytics (OMS) blade.</span></span>  
2. <span data-ttu-id="f6b21-126">在 hello**記錄分析 (OMS)**刀鋒視窗中，按一下 **新增**tooopen hello **OMS 工作區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6b21-126">On hello **Log Analytics (OMS)** blade, click **Add** tooopen hello **OMS Workspace** blade.</span></span>  
   <span data-ttu-id="f6b21-127">![OMS 刀鋒視窗](./media/log-analytics-sccm/sccm-azure01.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-127">![OMS blade](./media/log-analytics-sccm/sccm-azure01.png)</span></span>
3. <span data-ttu-id="f6b21-128">在 hello **OMS 工作區**刀鋒視窗中，提供下列資訊的 hello，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-128">On hello **OMS Workspace** blade, provide hello following information and then click **OK**.</span></span>

   * <span data-ttu-id="f6b21-129">**OMS 工作區**</span><span class="sxs-lookup"><span data-stu-id="f6b21-129">**OMS Workspace**</span></span>
   * <span data-ttu-id="f6b21-130">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="f6b21-130">**Subscription**</span></span>
   * <span data-ttu-id="f6b21-131">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="f6b21-131">**Resource group**</span></span>
   * <span data-ttu-id="f6b21-132">**位置**</span><span class="sxs-lookup"><span data-stu-id="f6b21-132">**Location**</span></span>
   * <span data-ttu-id="f6b21-133">**定價層**</span><span class="sxs-lookup"><span data-stu-id="f6b21-133">**Pricing tier**</span></span>  
     <span data-ttu-id="f6b21-134">![OMS 刀鋒視窗](./media/log-analytics-sccm/sccm-azure02.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-134">![OMS blade](./media/log-analytics-sccm/sccm-azure02.png)</span></span>  

     > [!NOTE]
     > <span data-ttu-id="f6b21-135">上述的 hello 範例會建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f6b21-135">hello example above creates a new resource group.</span></span> <span data-ttu-id="f6b21-136">hello 資源群組都只能使用的 tooprovide Configuration Manager 與在此範例中的權限 toohello OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="f6b21-136">hello resource group is only used tooprovide Configuration Manager with permissions toohello OMS workspace in this example.</span></span>
     >
     >
4. <span data-ttu-id="f6b21-137">按一下**瀏覽** > **資源群組**tooopen hello**資源群組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6b21-137">Click **Browse** > **Resource groups** tooopen hello **Resource groups** blade.</span></span>
5. <span data-ttu-id="f6b21-138">在 [hello**資源群組**刀鋒視窗中，按一下 hello tooopen hello 先前建立的資源群組&lt;資源群組名稱&gt;設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6b21-138">In hello **Resource groups** blade, click hello resource group that you created above tooopen hello &lt;resource group name&gt; settings blade.</span></span>  
   <span data-ttu-id="f6b21-139">![資源群組設定刀鋒視窗](./media/log-analytics-sccm/sccm-azure03.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-139">![resource group settings blade](./media/log-analytics-sccm/sccm-azure03.png)</span></span>
6. <span data-ttu-id="f6b21-140">在 hello&lt;資源群組名稱&gt;設定刀鋒視窗中，按一下 存取控制 (IAM) tooopen hello&lt;資源群組名稱&gt;使用者 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6b21-140">In hello &lt;resource group name&gt; settings blade, click Access control (IAM) tooopen hello &lt;resource group name&gt; Users blade.</span></span>  
   ![資源群組使用者刀鋒視窗](./media/log-analytics-sccm/sccm-azure04.png)  
7. <span data-ttu-id="f6b21-142">在 [hello&lt;資源群組名稱&gt;使用者] 刀鋒視窗中，按一下**新增**tooopen hello**新增存取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6b21-142">In hello &lt;resource group name&gt; Users blade, click **Add** tooopen hello **Add access** blade.</span></span>
8. <span data-ttu-id="f6b21-143">在 hello**新增存取**刀鋒視窗中，按一下 **選取角色**，然後選取 hello**參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="f6b21-143">In hello **Add access** blade, click **Select a role**, and then select hello **Contributor** role.</span></span>  
   <span data-ttu-id="f6b21-144">![選取角色](./media/log-analytics-sccm/sccm-azure05.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-144">![select a role](./media/log-analytics-sccm/sccm-azure05.png)</span></span>  
9. <span data-ttu-id="f6b21-145">按一下**將使用者新增**hello Configuration Manager 使用者進行選取，按一下 **選取**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-145">Click **Add users**, select hello Configuration Manager user, click **Select**, and then click **OK**.</span></span>  
   <span data-ttu-id="f6b21-146">![新增使用者](./media/log-analytics-sccm/sccm-azure06.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-146">![add users](./media/log-analytics-sccm/sccm-azure06.png)</span></span>  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a><span data-ttu-id="f6b21-147">加入 OMS 連線 tooConfiguration 管理員</span><span class="sxs-lookup"><span data-stu-id="f6b21-147">Add an OMS connection tooConfiguration Manager</span></span>
<span data-ttu-id="f6b21-148">在訂單 tooadd OMS 連線，必須具有 Configuration Manager 環境[服務連接點](https://technet.microsoft.com/library/mt627781.aspx)設定為線上模式。</span><span class="sxs-lookup"><span data-stu-id="f6b21-148">In order tooadd an OMS connection, your Configuration Manager environment must have a [service connection point](https://technet.microsoft.com/library/mt627781.aspx) configured for online mode.</span></span>

1. <span data-ttu-id="f6b21-149">在 hello**管理**工作區的 Configuration Manager，選取**OMS Connector**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-149">In hello **Administration** workspace of Configuration Manager, select **OMS Connector**.</span></span> <span data-ttu-id="f6b21-150">這會開啟 hello**加入 OMS 連線精靈**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-150">This opens hello **Add OMS Connection Wizard**.</span></span> <span data-ttu-id="f6b21-151">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f6b21-151">Select **Next**.</span></span>
2. <span data-ttu-id="f6b21-152">在 hello**一般**畫面上，確認您已完成下列動作的 hello 和您擁有詳細資料，每個項目，然後選取 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-152">On hello **General** screen, confirm that you have done hello following actions and that you have details for each item, then select **Next**.</span></span>

   1. <span data-ttu-id="f6b21-153">在 hello Azure 管理入口網站，您已註冊，Configuration Manager 做為 Web 應用程式和/或 Web API 的應用程式，而且您擁有 hello， [hello 註冊用戶端識別碼](../active-directory/active-directory-integrating-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-153">In hello Azure Management Portal, you've registered Configuration Manager as a Web Application and/or Web API app, and that you have hello [client ID from hello registration](../active-directory/active-directory-integrating-applications.md).</span></span>
   2. <span data-ttu-id="f6b21-154">在 hello Azure 管理入口網站，您已建立 hello Azure Active Directory 中註冊應用程式的應用程式祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f6b21-154">In hello Azure Management Portal, you've created an app secret key for hello registered app in Azure Active Directory.</span></span>  
   3. <span data-ttu-id="f6b21-155">Hello Azure 管理入口網站，在您提供了 hello 註冊的 web 應用程式的權限 tooaccess OMS。</span><span class="sxs-lookup"><span data-stu-id="f6b21-155">In hello Azure Management Portal, you've provided hello registered web app with permission tooaccess OMS.</span></span>  
      ![連接 tooOMS 精靈一般頁面](./media/log-analytics-sccm/sccm-console-general01.png)
3. <span data-ttu-id="f6b21-157">在 hello **Azure Active Directory**畫面上，設定您的連接設定 tooOMS 藉由提供您**租用戶**，**用戶端識別碼**，和**用戶端秘密金鑰** ，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-157">On hello **Azure Active Directory** screen, configure your connection settings tooOMS by providing your **Tenant** , **Client ID** , and **Client Secret Key** , then select **Next**.</span></span>  
   <span data-ttu-id="f6b21-158">![連接 tooOMS 精靈 Azure Active Directory 頁面](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-158">![Connection tooOMS Wizard Azure Active Directory page](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)</span></span>
4. <span data-ttu-id="f6b21-159">如果您已完成所有 hello 其他程序成功，然後 hello 有關 hello **OMS 連線設定**畫面會自動出現在此頁面。</span><span class="sxs-lookup"><span data-stu-id="f6b21-159">If you accomplished all hello other procedures successfully, then hello information on hello **OMS Connection Configuration** screen will automatically appear on this page.</span></span> <span data-ttu-id="f6b21-160">Hello 連接設定的資訊應該會出現為您**Azure 訂用帳戶**， **Azure 資源群組**，和**Operations Management Suite 工作區**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-160">Information for hello connection settings should appear for your **Azure subscription** , **Azure resource group** , and **Operations Management Suite Workspace**.</span></span>  
   <span data-ttu-id="f6b21-161">![連接 tooOMS 精靈 OMS 連接 頁面](./media/log-analytics-sccm/sccm-wizard-configure04.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-161">![Connection tooOMS Wizard OMS Connection page](./media/log-analytics-sccm/sccm-wizard-configure04.png)</span></span>
5. <span data-ttu-id="f6b21-162">hello 精靈會連線 toohello OMS 服務使用您已輸入 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f6b21-162">hello wizard connects toohello OMS service using hello information you've input.</span></span> <span data-ttu-id="f6b21-163">選取您想要使用 OMS toosync，然後按一下 hello 裝置集合**新增**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-163">Select hello device collections that you want toosync with OMS and then click **Add**.</span></span>  
   <span data-ttu-id="f6b21-164">![選取集合](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-164">![Select Collections](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)</span></span>
6. <span data-ttu-id="f6b21-165">確認您的連線設定上 hello**摘要**畫面，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-165">Verify your connection settings on hello **Summary** screen, then select **Next**.</span></span> <span data-ttu-id="f6b21-166">hello**進度**螢幕會顯示 hello 連接狀態，則應該**完成**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-166">hello **Progress** screen shows hello connection status, then should **Complete**.</span></span>

> [!NOTE]
> <span data-ttu-id="f6b21-167">您必須連接 OMS toohello 頂層站台階層中。</span><span class="sxs-lookup"><span data-stu-id="f6b21-167">You must connect OMS toohello top-tier site in your hierarchy.</span></span> <span data-ttu-id="f6b21-168">如果您連線到 OMS tooa 獨立主要網站，然後再新增管理中心網站 tooyour 環境，您會有 toodelete，並重新建立 hello 新階層中的 hello OMS 連線。</span><span class="sxs-lookup"><span data-stu-id="f6b21-168">If you connect OMS tooa standalone primary site and then add a central administration site tooyour environment, you'll have toodelete and recreate hello OMS connection within hello new hierarchy.</span></span>
>
>

<span data-ttu-id="f6b21-169">您已將 Configuration Manager tooOMS 連結之後，您可以新增或移除的集合，並檢視 hello hello OMS 連線屬性。</span><span class="sxs-lookup"><span data-stu-id="f6b21-169">After you have linked Configuration Manager tooOMS, you can add or remove collections, and view hello properties of hello OMS connection.</span></span>

## <a name="update-oms-connection-properties"></a><span data-ttu-id="f6b21-170">更新 OMS 連線屬性</span><span class="sxs-lookup"><span data-stu-id="f6b21-170">Update OMS connection properties</span></span>
<span data-ttu-id="f6b21-171">如果曾密碼或用戶端秘密金鑰會過期，或遺失，您將需要 toomanually 更新 hello OMS 連線內容。</span><span class="sxs-lookup"><span data-stu-id="f6b21-171">If a password or client secret key ever expires or is lost, you'll need toomanually update hello OMS connection properties.</span></span>

1. <span data-ttu-id="f6b21-172">在 [組態管理員] 中，瀏覽過**雲端服務**，然後選取**OMS Connector** tooopen hello **OMS 連線內容**頁面。</span><span class="sxs-lookup"><span data-stu-id="f6b21-172">In Configuration Manager, navigate too**Cloud Services** , then select **OMS Connector** tooopen hello **OMS Connection Properties** page.</span></span>
2. <span data-ttu-id="f6b21-173">這個頁面上，按一下 hello **Azure Active Directory**索引標籤上 tooview 您**租用戶**，**用戶端識別碼**，**用戶端秘密金鑰到期**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-173">On this page, click hello **Azure Active Directory** tab tooview your **Tenant**, **Client ID**, **Client secret key expiration**.</span></span> <span data-ttu-id="f6b21-174">**確認****用戶端秘密金鑰**是否已過期。</span><span class="sxs-lookup"><span data-stu-id="f6b21-174">**Verify** your **Client secret key** if it has expired.</span></span>

## <a name="download-and-install-hello-agent"></a><span data-ttu-id="f6b21-175">下載並安裝 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="f6b21-175">Download and install hello agent</span></span>
1. <span data-ttu-id="f6b21-176">在 hello OMS 入口網站，[下載 hello 代理程式安裝程式檔案從 OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-176">In hello OMS portal, [Download hello agent setup file from OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).</span></span>
2. <span data-ttu-id="f6b21-177">使用其中一種下列方法 tooinstall hello hello 代理程式電腦上及設定 hello 執行 hello Configuration Manager 服務連線點站台系統角色：</span><span class="sxs-lookup"><span data-stu-id="f6b21-177">Use one of hello following methods tooinstall and configure hello agent on hello computer running hello Configuration Manager service connection point site system role:</span></span>
   * [<span data-ttu-id="f6b21-178">Hello 使用安裝代理程式安裝程式</span><span class="sxs-lookup"><span data-stu-id="f6b21-178">Install hello agent using setup</span></span>](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [<span data-ttu-id="f6b21-179">Hello 使用安裝代理程式 hello 命令列</span><span class="sxs-lookup"><span data-stu-id="f6b21-179">Install hello agent using hello command line</span></span>](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [<span data-ttu-id="f6b21-180">安裝在 Azure 自動化中使用 DSC 的 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="f6b21-180">Install hello agent using DSC in Azure Automation</span></span>](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a><span data-ttu-id="f6b21-181">匯入集合</span><span class="sxs-lookup"><span data-stu-id="f6b21-181">Import collections</span></span>
<span data-ttu-id="f6b21-182">您加入 OMS 連線 tooConfiguration 管理員，並安裝 hello 代理程式後 hello 電腦執行 hello Configuration Manager 服務連線點站台系統角色，hello 下一個步驟是 tooimport 集合從 Configuration Manager 在 OMS 中為電腦群組。</span><span class="sxs-lookup"><span data-stu-id="f6b21-182">After you've added an OMS connection tooConfiguration Manager and installed hello agent on hello computer running hello Configuration Manager service connection point site system role, hello next step is tooimport collections from Configuration Manager in OMS as computer groups.</span></span>

<span data-ttu-id="f6b21-183">Hello 集合成員資格資訊啟用匯入之後，會擷取每個過去 3 小時內 tookeep hello 集合成員資格目前。</span><span class="sxs-lookup"><span data-stu-id="f6b21-183">After importation is enabled, hello collection membership information is retrieved every 3 hours tookeep hello collection memberships current.</span></span> <span data-ttu-id="f6b21-184">您可以選擇在任何時候 toodisable 匯入作業。</span><span class="sxs-lookup"><span data-stu-id="f6b21-184">You can choose toodisable importation at any time.</span></span>

1. <span data-ttu-id="f6b21-185">在 hello OMS 入口網站中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-185">In hello OMS portal, click **Settings**.</span></span>
2. <span data-ttu-id="f6b21-186">按一下 hello**電腦群組**索引標籤，然後按一下hello **SCCM**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f6b21-186">Click hello **Computer Groups** tab and then click hello **SCCM** tab.</span></span>
3. <span data-ttu-id="f6b21-187">選取 匯入 Configuration Manager 集合成員資格，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="f6b21-187">Select **Import Configuration Manager collection memberships** and then click **Save**.</span></span>  
   <span data-ttu-id="f6b21-188">![電腦群組 - SCCM 索引標籤](./media/log-analytics-sccm/sccm-computer-groups01.png)</span><span class="sxs-lookup"><span data-stu-id="f6b21-188">![Computer Groups - SCCM tab](./media/log-analytics-sccm/sccm-computer-groups01.png)</span></span>

## <a name="view-data-from-configuration-manager"></a><span data-ttu-id="f6b21-189">從 Configuration Manager 檢視資料</span><span class="sxs-lookup"><span data-stu-id="f6b21-189">View data from Configuration Manager</span></span>
<span data-ttu-id="f6b21-190">在您加入 OMS 連線 tooConfiguration 管理員，並執行 hello Configuration Manager 服務連線點站台系統角色的 hello 電腦上安裝 hello 代理程式之後，從 hello 代理程式的資料會傳送 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="f6b21-190">After you've added an OMS connection tooConfiguration Manager and installed hello agent on hello computer running hello Configuration Manager service connection point site system role, data from hello agent is sent tooOMS.</span></span> <span data-ttu-id="f6b21-191">在 OMS 中，Configuration Manager 集合會顯示為[電腦群組](log-analytics-computer-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="f6b21-191">In OMS, your Configuration Manager collections appear as [computer groups](log-analytics-computer-groups.md).</span></span> <span data-ttu-id="f6b21-192">您可以檢視從 hello hello 分組**Configuration Manager**頁面**電腦群組**中**設定**。</span><span class="sxs-lookup"><span data-stu-id="f6b21-192">You can view hello groups from hello **Configuration Manager** page under **Computer Groups** in **Settings**.</span></span>

<span data-ttu-id="f6b21-193">之後 hello 匯入集合，您會看到已偵測到多少部電腦與集合成員資格。</span><span class="sxs-lookup"><span data-stu-id="f6b21-193">After hello collections are imported, you can see how many computers with collection memberships have been detected.</span></span> <span data-ttu-id="f6b21-194">您也可以看到已匯入集合的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="f6b21-194">You can also see hello number of collections that have been imported.</span></span>

![電腦群組 - SCCM 索引標籤](./media/log-analytics-sccm/sccm-computer-groups02.png)

<span data-ttu-id="f6b21-196">當您按一下其中一個，搜尋會開啟，顯示 hello 的所有匯入群組或屬於 tooeach 群組的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="f6b21-196">When you click either one, Search opens, displaying either all of hello imported groups or all computers that belong tooeach group.</span></span> <span data-ttu-id="f6b21-197">使用 [記錄搜尋](log-analytics-log-searches.md)，您就可以開始深入分析 Configuration Manager 資料。</span><span class="sxs-lookup"><span data-stu-id="f6b21-197">Using [Log Search](log-analytics-log-searches.md), you can start in-depth analysis of Configuration Manager data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6b21-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6b21-198">Next steps</span></span>
* <span data-ttu-id="f6b21-199">使用[記錄搜尋](log-analytics-log-searches.md)tooview 詳細的 Configuration Manager 資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f6b21-199">Use [Log Search](log-analytics-log-searches.md) tooview detailed information about your Configuration Manager data.</span></span>
