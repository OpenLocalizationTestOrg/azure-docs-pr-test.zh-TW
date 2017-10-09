---
title: "aaaConnect Windows 電腦 tooAzure 記錄分析 |Microsoft 文件"
description: "本文將說明在您的內部部署基礎結構 toohello 記錄分析服務 hello 步驟 tooconnect hello Windows 電腦使用 hello Microsoft Monitoring Agent (MMA) 的自訂的版本。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="8ae83-103">連接 Windows Azure 中的電腦 toohello 記錄分析服務</span><span class="sxs-lookup"><span data-stu-id="8ae83-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="8ae83-104">本文示範 hello 步驟 tooconnect Windows 電腦在內部部署基礎結構 tooOMS 工作區中使用自訂的 hello Microsoft Monitoring Agent (MMA) 的版本。</span><span class="sxs-lookup"><span data-stu-id="8ae83-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="8ae83-105">您需要 tooinstall，並連線 toosend 資料 toohello 記錄分析服務，且 tooview 和在該資料上的運作，想要使其 tooonboard hello 電腦的所有代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="8ae83-106">每個代理程式可以報告 toomultiple 工作區。</span><span class="sxs-lookup"><span data-stu-id="8ae83-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="8ae83-107">您可以使用安裝程式、命令列、或 Azure 自動化中的期望狀態設定 (DSC) 來安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="8ae83-108">在 Azure 中執行的虛擬機器，您可以使用來簡化安裝 hello[虛擬機器擴充功能](log-analytics-azure-vm-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="8ae83-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="8ae83-109">在電腦上透過網際網路連線，hello 代理程式會使用 hello 連接 toohello 網際網路 toosend 資料 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="8ae83-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="8ae83-110">對於沒有網際網路連線的電腦，您可以使用 proxy 或 hello [OMS 閘道](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="8ae83-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="8ae83-111">連接您的 Windows 電腦 tooOMS 是直接使用三個簡單步驟：</span><span class="sxs-lookup"><span data-stu-id="8ae83-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="8ae83-112">從 hello OMS 入口網站下載 hello 代理程式安裝檔案</span><span class="sxs-lookup"><span data-stu-id="8ae83-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="8ae83-113">安裝 hello 代理程式使用您所選擇的 hello 方法</span><span class="sxs-lookup"><span data-stu-id="8ae83-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="8ae83-114">設定 hello 代理程式，或視需要新增額外的工作區</span><span class="sxs-lookup"><span data-stu-id="8ae83-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="8ae83-115">hello 下列圖表顯示 hello 您 Windows 電腦和 OMS 之間的關聯性之後，您已安裝並設定代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="8ae83-117">如果您的 IT 安全性原則不允許您的網路 tooconnect toohello 網際網路上的電腦，您可以設定您的電腦 tooconnect toohello OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="8ae83-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="8ae83-118">如需詳細資訊以及有關如何 tooconfigure 您的伺服器 toocommunicate 透過 OMS 閘道 toohello OMS 服務，請參閱步驟[連接使用 hello OMS 閘道電腦 tooOMS](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="8ae83-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="8ae83-119">系統需求和所需的設定</span><span class="sxs-lookup"><span data-stu-id="8ae83-119">System requirements and required configuration</span></span>
<span data-ttu-id="8ae83-120">您安裝或部署代理程式之前，請檢閱下列符合 hello 需求的詳細資料 tooensure hello。</span><span class="sxs-lookup"><span data-stu-id="8ae83-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="8ae83-121">您只能在執行 Windows Server 2008 SP 1 或更新版本的電腦或 Windows 7 SP1 上安裝 OMS MMA hello 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8ae83-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="8ae83-122">您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ae83-122">You need an Azure subscription.</span></span>  <span data-ttu-id="8ae83-123">如需詳細資訊，請參閱[開始使用 Log Analytics](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8ae83-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="8ae83-124">每一部 Windows 電腦必須能夠 tooconnect toohello 網際網路使用 HTTPS 或 toohello OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="8ae83-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="8ae83-125">此連接可以是直接透過 proxy，或透過 hello OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="8ae83-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="8ae83-126">您可以在獨立電腦、 伺服器和虛擬機器上安裝 OMS MMA hello。</span><span class="sxs-lookup"><span data-stu-id="8ae83-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="8ae83-127">如果您想 tooconnect Azure 託管的虛擬機器 tooOMS，請參閱[連接 Azure 虛擬機器 tooLog 分析](log-analytics-azure-vm-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="8ae83-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="8ae83-128">hello 代理程式需要的各種資源建立 toouse TCP 連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="8ae83-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="8ae83-129">網路</span><span class="sxs-lookup"><span data-stu-id="8ae83-129">Network</span></span>

<span data-ttu-id="8ae83-130">Windows 代理程式 tooconnect tooand 向 hello OMS 服務，它們必須存取 toonetwork 資源，包括 hello 連接埠號碼和網域 Url。</span><span class="sxs-lookup"><span data-stu-id="8ae83-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="8ae83-131">Proxy 伺服器，您需要 hello 資源在代理程式設定中設定適當的 proxy 伺服器的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="8ae83-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="8ae83-132">限制存取 toohello 網際網路的防火牆，您的網路工程師必須 tooconfigure 您防火牆 toopermit 存取 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="8ae83-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="8ae83-133">您不需要在代理程式設定中進行任何動作。</span><span class="sxs-lookup"><span data-stu-id="8ae83-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="8ae83-134">hello 下表會顯示通訊所需的資源。</span><span class="sxs-lookup"><span data-stu-id="8ae83-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="8ae83-135">有部分的下列資源的 hello 提及 Operational Insights，這是供記錄分析先前的名稱。</span><span class="sxs-lookup"><span data-stu-id="8ae83-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="8ae83-136">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="8ae83-136">Agent Resource</span></span> | <span data-ttu-id="8ae83-137">連接埠</span><span class="sxs-lookup"><span data-stu-id="8ae83-137">Ports</span></span> | <span data-ttu-id="8ae83-138">略過 HTTPS 檢查</span><span class="sxs-lookup"><span data-stu-id="8ae83-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="8ae83-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="8ae83-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="8ae83-140">443</span><span class="sxs-lookup"><span data-stu-id="8ae83-140">443</span></span> | <span data-ttu-id="8ae83-141">是</span><span class="sxs-lookup"><span data-stu-id="8ae83-141">Yes</span></span> |
| <span data-ttu-id="8ae83-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="8ae83-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="8ae83-143">443</span><span class="sxs-lookup"><span data-stu-id="8ae83-143">443</span></span> | <span data-ttu-id="8ae83-144">是</span><span class="sxs-lookup"><span data-stu-id="8ae83-144">Yes</span></span> |
| <span data-ttu-id="8ae83-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8ae83-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="8ae83-146">443</span><span class="sxs-lookup"><span data-stu-id="8ae83-146">443</span></span> | <span data-ttu-id="8ae83-147">是</span><span class="sxs-lookup"><span data-stu-id="8ae83-147">Yes</span></span> |
| <span data-ttu-id="8ae83-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="8ae83-148">*.azure-automation.net</span></span> | <span data-ttu-id="8ae83-149">443</span><span class="sxs-lookup"><span data-stu-id="8ae83-149">443</span></span> | <span data-ttu-id="8ae83-150">是</span><span class="sxs-lookup"><span data-stu-id="8ae83-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="8ae83-151">從 OMS 下載 hello 代理程式安裝檔案</span><span class="sxs-lookup"><span data-stu-id="8ae83-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="8ae83-152">在 hello OMS 入口網站上 hello**概觀**頁面上，按一下 hello**設定**磚。</span><span class="sxs-lookup"><span data-stu-id="8ae83-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="8ae83-153">按一下 hello**連線來源**hello 頂端的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8ae83-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="8ae83-154">![連接的來源索引標籤](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="8ae83-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="8ae83-155">按一下**Windows 伺服器**，然後按一下**下載 Windows 代理程式**適用 tooyour 電腦處理器類型 toodownload hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="8ae83-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="8ae83-156">在右邊的 hello**工作區識別碼**，按一下 hello 複製圖示，然後貼入 [記事本] 中的 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="8ae83-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="8ae83-157">在右邊的 hello**主索引鍵**，按一下 hello 複製圖示，然後貼入 [記事本] 中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8ae83-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="8ae83-158">Hello 使用安裝代理程式安裝程式</span><span class="sxs-lookup"><span data-stu-id="8ae83-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="8ae83-159">您想 toomanage 的電腦上執行安裝程式 tooinstall hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="8ae83-160">在 hello  褖畫惎 頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="8ae83-161">在 hello 授權條款 頁面上，讀取 hello 授權，然後按一下**我同意**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="8ae83-162">在 hello 目的地資料夾 頁面上，變更或保留 hello 預設安裝資料夾，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="8ae83-163">在 hello 代理程式安裝選項 頁面上，您可以選擇 tooconnect hello 代理程式 tooAzure 記錄分析 (OMS)，Operations Manager 中，或者可以 hello 選項保留為空白如果您稍後想 tooconfigure hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="8ae83-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8ae83-164">Click **Next**.</span></span>   
    - <span data-ttu-id="8ae83-165">如果您選擇 tooconnect tooAzure 記錄分析 (OMS)，貼上 hello**工作區識別碼**和**（主索引鍵） 的工作區金鑰**hello 前一個程序中複製到 [記事本]，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="8ae83-166">![貼上工作區識別碼和主索引鍵](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="8ae83-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="8ae83-167">如果您選擇 tooconnect tooOperations 管理員，請輸入 hello**管理群組名稱**，**管理伺服器**名稱，和**管理伺服器連接埠**，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="8ae83-168">在 hello 代理程式動作帳戶] 頁面上，選擇 [hello 本機系統帳戶或本機網域帳戶，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="8ae83-169">![管理群組設定](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![代理程式動作帳戶](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="8ae83-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="8ae83-170">在 hello 準備 tooInstall 頁面上，檢閱您的選擇，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="8ae83-171">在 [hello 組態已順利完成] 頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="8ae83-172">完成時，hello **Microsoft Monitoring Agent**會出現在**控制台**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="8ae83-173">您可以檢閱您的設定，並確認該 hello 代理程式連接的 tooOperational Insights (OMS)。</span><span class="sxs-lookup"><span data-stu-id="8ae83-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="8ae83-174">當連接的 tooOMS hello 代理程式會顯示訊息指出： **hello Microsoft Monitoring Agent 已成功連接 toohello Microsoft Operations Management Suite 服務。**</span><span class="sxs-lookup"><span data-stu-id="8ae83-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="8ae83-175">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="8ae83-175">Configure proxy settings</span></span>

<span data-ttu-id="8ae83-176">您可以使用下列程序 tooconfigure hello 使用控制台中的 Microsoft Monitoring Agent 的 proxy 設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="8ae83-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="8ae83-177">您需要 toouse 此程序的每一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="8ae83-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="8ae83-178">如果您有許多您需要 tooconfigure 的伺服器，您可能會發現它更容易 toouse 指令碼 tooautomate 此程序。</span><span class="sxs-lookup"><span data-stu-id="8ae83-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="8ae83-179">若是如此，請參閱下一個程序 hello [tooconfigure hello 使用指令碼的 Microsoft Monitoring Agent 的 proxy 設定](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script)。</span><span class="sxs-lookup"><span data-stu-id="8ae83-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="8ae83-180">tooconfigure hello 使用控制台中的 Microsoft Monitoring Agent 的 proxy 設定</span><span class="sxs-lookup"><span data-stu-id="8ae83-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="8ae83-181">開啟 [ **控制台**]。</span><span class="sxs-lookup"><span data-stu-id="8ae83-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="8ae83-182">開啟 [ **Microsoft Monitoring Agent**].</span><span class="sxs-lookup"><span data-stu-id="8ae83-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="8ae83-183">按一下 hello **Proxy 設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8ae83-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="8ae83-184">![[Proxy 設定] 索引標籤](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="8ae83-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="8ae83-185">選取**使用 proxy 伺服器**輸入 hello URL 和連接埠號碼，如有需要，類似 toohello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="8ae83-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="8ae83-186">如果您的 proxy 伺服器需要驗證，請輸入 hello 使用者名稱和密碼 tooaccess hello proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8ae83-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="8ae83-187">確認代理程式連線能力 tooOMS</span><span class="sxs-lookup"><span data-stu-id="8ae83-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="8ae83-188">您可以輕鬆地確認您的代理程式是否會與使用下列程序的 hello 的 OMS 的通訊：</span><span class="sxs-lookup"><span data-stu-id="8ae83-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="8ae83-189">在 hello hello Windows 代理程式電腦，開啟控制台。</span><span class="sxs-lookup"><span data-stu-id="8ae83-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="8ae83-190">開啟 [Microsoft Monitoring Agent]。</span><span class="sxs-lookup"><span data-stu-id="8ae83-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="8ae83-191">按一下 hello Azure 記錄分析 (OMS) 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8ae83-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="8ae83-192">在 hello 狀態 資料行，您應該會看到該 hello 代理程式已成功連接 toohello Operations Management Suite 服務。</span><span class="sxs-lookup"><span data-stu-id="8ae83-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![代理程式已連線](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="8ae83-194">tooconfigure hello 使用指令碼的 Microsoft Monitoring Agent 的 proxy 設定</span><span class="sxs-lookup"><span data-stu-id="8ae83-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="8ae83-195">複製下列範例，資訊特定 tooyour 環境以更新、 儲存 PS1 副檔名為檔案名稱，然後再執行 hello 指令碼直接連接 toohello OMS 服務的每一部電腦上的 hello。</span><span class="sxs-lookup"><span data-stu-id="8ae83-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="8ae83-196">Hello 使用安裝代理程式 hello 命令列</span><span class="sxs-lookup"><span data-stu-id="8ae83-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="8ae83-197">修改，然後使用 hello 遵循範例 tooinstall hello 代理程式使用 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="8ae83-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="8ae83-198">hello 範例會執行完全無訊息安裝。</span><span class="sxs-lookup"><span data-stu-id="8ae83-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="8ae83-199">如果您想 tooupgrade 代理程式，您需要 toouse hello 記錄分析指令碼應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="8ae83-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="8ae83-200">請參閱下一個區段 tooupgrade hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="8ae83-201">hello 代理程式是使用 IExpress 做為其自我解壓縮程式使用 hello`/c`命令。</span><span class="sxs-lookup"><span data-stu-id="8ae83-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="8ae83-202">您可以看到在 hello 命令列參數[IExpress 的命令列參數](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages)，然後更新會 hello 範例 toosuit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="8ae83-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="8ae83-203">MMA 專屬選項</span><span class="sxs-lookup"><span data-stu-id="8ae83-203">MMA-specific options</span></span>                   |<span data-ttu-id="8ae83-204">注意事項</span><span class="sxs-lookup"><span data-stu-id="8ae83-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="8ae83-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="8ae83-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="8ae83-206">1 = 設定 hello 代理程式 tooreport tooa 工作區</span><span class="sxs-lookup"><span data-stu-id="8ae83-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="8ae83-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="8ae83-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="8ae83-208">Hello 工作區 tooadd 的工作區識別碼 (guid)</span><span class="sxs-lookup"><span data-stu-id="8ae83-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="8ae83-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="8ae83-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="8ae83-210">工作區的索引鍵使用的 tooinitially 向 hello 工作區</span><span class="sxs-lookup"><span data-stu-id="8ae83-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="8ae83-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="8ae83-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="8ae83-212">指定 hello hello 工作區所在位置的雲端環境</span><span class="sxs-lookup"><span data-stu-id="8ae83-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="8ae83-213">0 = Azure 商業雲端 (預設值)</span><span class="sxs-lookup"><span data-stu-id="8ae83-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="8ae83-214">1 = Azure Government</span><span class="sxs-lookup"><span data-stu-id="8ae83-214">1 = Azure Government</span></span> |
|<span data-ttu-id="8ae83-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="8ae83-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="8ae83-216">Hello proxy toouse URI</span><span class="sxs-lookup"><span data-stu-id="8ae83-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="8ae83-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="8ae83-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="8ae83-218">使用者名稱 tooaccess 驗證的 proxy</span><span class="sxs-lookup"><span data-stu-id="8ae83-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="8ae83-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="8ae83-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="8ae83-220">密碼 tooaccess 驗證的 proxy</span><span class="sxs-lookup"><span data-stu-id="8ae83-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="8ae83-221">IExpress 的 tooavoid 達到 hello 命令列的長度限制 hello 代理程式安裝與設定任何工作區，然後再使用 hello 工作區的 指令碼 tooset 組態。</span><span class="sxs-lookup"><span data-stu-id="8ae83-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="8ae83-222">如果您收到`Command line option syntax error.`時使用 hello`OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE`參數，您可以使用下列因應措施的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ae83-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="8ae83-223">使用指令碼來新增工作區</span><span class="sxs-lookup"><span data-stu-id="8ae83-223">Add a workspace using a script</span></span>
<span data-ttu-id="8ae83-224">加入工作區中以 hello 下列範例使用 hello 記錄分析代理程式的指令碼 API:</span><span class="sxs-lookup"><span data-stu-id="8ae83-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="8ae83-225">tooadd 美國政府，下列指令碼範例使用 hello 的 Azure 中的工作區：</span><span class="sxs-lookup"><span data-stu-id="8ae83-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="8ae83-226">如果您曾經使用 hello 命令列或指令碼先前 tooinstall 或設定 hello 代理程式，`EnableAzureOperationalInsights`取代為`AddCloudWorkspace`。</span><span class="sxs-lookup"><span data-stu-id="8ae83-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="8ae83-227">安裝在 Azure 自動化中使用 DSC 的 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="8ae83-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="8ae83-228">您可以使用下列指令碼範例 tooinstall hello 代理程式在 Azure 自動化中使用 DSC 的 hello。</span><span class="sxs-lookup"><span data-stu-id="8ae83-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="8ae83-229">hello 範例安裝 hello 64 位元代理程式，由 hello`URI`值。</span><span class="sxs-lookup"><span data-stu-id="8ae83-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="8ae83-230">您也可以使用 hello 32 位元版本來取代 hello URI 值。</span><span class="sxs-lookup"><span data-stu-id="8ae83-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="8ae83-231">這兩個版本的 hello Uri 是：</span><span class="sxs-lookup"><span data-stu-id="8ae83-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="8ae83-232">Windows 64 位元代理程式 - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="8ae83-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="8ae83-233">Windows 32 位元代理程式 - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="8ae83-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="8ae83-234">此程序和指令碼範例不會升級現有的代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="8ae83-235">匯入 hello xPSDesiredStateConfiguration DSC 模組從[http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration)至 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="8ae83-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="8ae83-236">建立 Azure 自動化的 *OPSINSIGHTS_WS_ID* 和 *OPSINSIGHTS_WS_KEY* 變數資產。</span><span class="sxs-lookup"><span data-stu-id="8ae83-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="8ae83-237">設定*OPSINSIGHTS_WS_ID* tooyour OMS 記錄分析工作區識別碼和設定*OPSINSIGHTS_WS_KEY* toohello 工作區的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8ae83-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="8ae83-238">使用下列指令碼，並將它儲存為 MMAgent.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="8ae83-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="8ae83-239">修改，然後使用下列範例 tooinstall hello 代理程式在 Azure 自動化中使用 DSC 的 hello。</span><span class="sxs-lookup"><span data-stu-id="8ae83-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="8ae83-240">匯入 MMAgent.ps1 Azure 自動化使用 hello Azure 自動化介面或指令程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="8ae83-241">請指派節點 toohello 設定。</span><span class="sxs-lookup"><span data-stu-id="8ae83-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="8ae83-242">15 分鐘內，hello 節點會檢查其組態和 hello MMA 推入 toohello 節點。</span><span class="sxs-lookup"><span data-stu-id="8ae83-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="8ae83-243">取得最新 ProductId 值 hello</span><span class="sxs-lookup"><span data-stu-id="8ae83-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="8ae83-244">hello`ProductId value`在 hello MMAgent.ps1 指令碼是唯一的 tooeach 代理程式版本。</span><span class="sxs-lookup"><span data-stu-id="8ae83-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="8ae83-245">每個代理程式的更新的版本發行時，變更 hello ProductId 值。</span><span class="sxs-lookup"><span data-stu-id="8ae83-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="8ae83-246">因此，當 hello ProductId 變更 hello 未來時，您可以找到 hello 代理程式版本使用簡單的指令碼。</span><span class="sxs-lookup"><span data-stu-id="8ae83-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="8ae83-247">您擁有 hello 測試伺服器上安裝最新的代理程式版本之後，您可以使用下列指令碼 tooget hello 安裝 ProductId 值 hello。</span><span class="sxs-lookup"><span data-stu-id="8ae83-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="8ae83-248">您可以使用 hello 最新的產品識別碼值，更新 hello MMAgent.ps1 指令碼中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8ae83-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="8ae83-249">手動設定代理程式，或新增額外的工作區</span><span class="sxs-lookup"><span data-stu-id="8ae83-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="8ae83-250">如果您已安裝的代理程式但未設定或者您想 hello 代理程式 tooreport toomultiple 工作區，您可以使用下列資訊 tooenable 代理程式的 hello 或重新設定它。</span><span class="sxs-lookup"><span data-stu-id="8ae83-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="8ae83-251">設定 hello 代理程式之後，它會註冊 hello 代理程式服務，並將獲得所需的組態資訊及包含解決方案資訊的管理組件。</span><span class="sxs-lookup"><span data-stu-id="8ae83-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="8ae83-252">您已安裝 Microsoft Monitoring Agent hello 之後，請開啟**控制台**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="8ae83-253">開啟**Microsoft Monitoring Agent**然後按一下hello **Azure 記錄分析 (OMS)**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8ae83-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="8ae83-254">按一下**新增**tooopen hello**新增記錄分析工作區**方塊。</span><span class="sxs-lookup"><span data-stu-id="8ae83-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="8ae83-255">貼上 hello**工作區識別碼**和**（主索引鍵） 的工作區金鑰**您在先前的程序，您想 tooadd，然後按一下 「 hello 」 工作區中複製到 [記事本]**確定**.</span><span class="sxs-lookup"><span data-stu-id="8ae83-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="8ae83-256">![設定 Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="8ae83-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="8ae83-257">從 hello 代理程式所監視的電腦收集資料之後，hello OMS 監視的電腦數目會出現在 hello OMS 入口網站上 hello**連線來源**索引標籤中**設定**為**伺服器連接**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="8ae83-258">toodisable 代理程式</span><span class="sxs-lookup"><span data-stu-id="8ae83-258">toodisable an agent</span></span>
1. <span data-ttu-id="8ae83-259">安裝之後 hello 代理程式，開啟**控制台**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="8ae83-260">開啟 Microsoft Monitoring Agent，然後按一下hello **Azure 記錄分析 (OMS)**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8ae83-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="8ae83-261">選取工作區，然後按一下移除 。</span><span class="sxs-lookup"><span data-stu-id="8ae83-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="8ae83-262">對其他所有工作區重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="8ae83-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="8ae83-263">（選擇性） 設定代理程式 tooreport tooan Operations Manager 管理群組</span><span class="sxs-lookup"><span data-stu-id="8ae83-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="8ae83-264">如果您使用 Operations Manager 在您的 IT 基礎結構，您也可以使用 hello MMA 代理程式與 Operations Manager 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8ae83-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="8ae83-265">tooconfigure MMA 代理程式 tooreport tooan Operations Manager 管理群組</span><span class="sxs-lookup"><span data-stu-id="8ae83-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="8ae83-266">Hello hello 代理程式安裝所在的電腦，開啟**控制台**。</span><span class="sxs-lookup"><span data-stu-id="8ae83-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="8ae83-267">開啟**Microsoft Monitoring Agent**然後按一下hello **Operations Manager**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8ae83-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="8ae83-268">![Microsoft 監視代理程式 Operations Manager 索引標籤](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="8ae83-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="8ae83-269">如果 Operations Manager 伺服器已與 Active Directory 整合，請按一下 [自動更新來自 AD DS 的管理群組指派] 。</span><span class="sxs-lookup"><span data-stu-id="8ae83-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="8ae83-270">按一下**新增**tooopen hello**新增管理群組** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8ae83-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="8ae83-271">![Microsoft 監視代理程式新增管理群組](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="8ae83-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="8ae83-272">在**管理群組名稱** 方塊中，輸入 hello 名稱的管理群組。</span><span class="sxs-lookup"><span data-stu-id="8ae83-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="8ae83-273">在 [hello**主要管理伺服器**] 方塊中，輸入 hello 電腦名稱的 hello 主要管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="8ae83-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="8ae83-274">在 hello**管理伺服器連接埠**方塊中，型別 hello TCP 通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="8ae83-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="8ae83-275">在下**代理程式動作帳戶**，選擇 hello 本機系統帳戶或本機網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ae83-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="8ae83-276">按一下**確定**tooclose hello**新增管理群組**對話方塊，然後按一下**確定**tooclose hello **Microsoft Monitoring Agent 內容** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8ae83-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8ae83-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ae83-277">Next steps</span></span>

- <span data-ttu-id="8ae83-278">[新增記錄分析解決方案從 hello 解決方案資源庫](log-analytics-add-solutions.md)tooadd 功能和收集資料。</span><span class="sxs-lookup"><span data-stu-id="8ae83-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
