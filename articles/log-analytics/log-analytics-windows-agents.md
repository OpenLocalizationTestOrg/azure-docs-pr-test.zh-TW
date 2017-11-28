---
title: "將 Windows 電腦連接到 Azure Log Analytics | Microsoft Docs"
description: "本文說明使用自訂版本的 Microsoft Monitoring Agent (MMA) 將內部部署基礎結構中的 Windows 電腦連接到 Log Analytics 服務的步驟。"
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
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="bd221-103">將 Windows 電腦連接到 Azure 中的 Log Analytics 服務</span><span class="sxs-lookup"><span data-stu-id="bd221-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="bd221-104">本文說明使用自訂版本的 Microsoft Monitoring Agent (MMA) 將內部部署基礎結構中的 Windows 電腦連接到 OMS 工作區的步驟。</span><span class="sxs-lookup"><span data-stu-id="bd221-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="bd221-105">您必須安裝並連接所有您想要上架之電腦的代理程式，以便讓它們將資料傳送給 Log Analytics 服務，以及檢視及處理此資料。</span><span class="sxs-lookup"><span data-stu-id="bd221-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="bd221-106">每個代理程式可以向多個工作區報告。</span><span class="sxs-lookup"><span data-stu-id="bd221-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="bd221-107">您可以使用安裝程式、命令列、或 Azure 自動化中的期望狀態設定 (DSC) 來安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="bd221-108">若需要在 Azure 中執行的虛擬機器，可使用[虛擬機器擴充功能](log-analytics-azure-vm-extension.md)簡化安裝。</span><span class="sxs-lookup"><span data-stu-id="bd221-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="bd221-109">在有網際網路連線的電腦上，代理程式會使用網際網路連線將資料傳送給 OMS。</span><span class="sxs-lookup"><span data-stu-id="bd221-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="bd221-110">若電腦沒有網際網路連線，您可以使用 Proxy 或 [OMS 閘道](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="bd221-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="bd221-111">使用 3 個簡單步驟可直接將 Windows 電腦連接至 OMS︰</span><span class="sxs-lookup"><span data-stu-id="bd221-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="bd221-112">從 OMS 入口網站下載代理程式安裝檔案</span><span class="sxs-lookup"><span data-stu-id="bd221-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="bd221-113">使用您選擇的方法安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="bd221-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="bd221-114">設定代理程式，或視需要新增額外的工作區</span><span class="sxs-lookup"><span data-stu-id="bd221-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="bd221-115">下圖顯示您安裝並設定代理程式之後您的 Windows 電腦和 OMS 之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="bd221-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="bd221-117">如果您的 IT 安全性原則不允許網路上的電腦連線到網際網路，您可以將電腦設定為連線到 OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="bd221-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="bd221-118">如需如何設定伺服器以透過 OMS 閘道與 OMS 服務進行通訊的詳細資訊和步驟，請參閱[使用 OMS 閘道將電腦連線到 OMS](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="bd221-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="bd221-119">系統需求和所需的設定</span><span class="sxs-lookup"><span data-stu-id="bd221-119">System requirements and required configuration</span></span>
<span data-ttu-id="bd221-120">在安裝或部署代理程式之前，請檢閱下列詳細資料，以確保您符合需求。</span><span class="sxs-lookup"><span data-stu-id="bd221-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="bd221-121">您只能將 OMS MMA 安裝在執行 Windows Server 2008 SP1 或更新版本亦或是 Windows 7 SP1 或更新版本的電腦上。</span><span class="sxs-lookup"><span data-stu-id="bd221-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="bd221-122">您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd221-122">You need an Azure subscription.</span></span>  <span data-ttu-id="bd221-123">如需詳細資訊，請參閱[開始使用 Log Analytics](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="bd221-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="bd221-124">每一部 Windows 電腦都必須能夠使用 HTTPS 連線到網際網路或連線到 OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="bd221-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="bd221-125">此連線可以是直接連線、透過 Proxy 連線、或透過 OMS 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="bd221-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="bd221-126">OMS MMA 可以安裝在獨立電腦、伺服器和虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="bd221-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="bd221-127">如果您想要將 Azure 託管的虛擬機器連接至 OMS，請參閱 [將 Azure 虛擬機器連接至 Log Analytics](log-analytics-azure-vm-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="bd221-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="bd221-128">代理程式必須使用 TCP 連接埠 443 來收送各種資源。</span><span class="sxs-lookup"><span data-stu-id="bd221-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="bd221-129">網路</span><span class="sxs-lookup"><span data-stu-id="bd221-129">Network</span></span>

<span data-ttu-id="bd221-130">Windows 代理程式若要連線到 OMS 服務並向其註冊，就必須能夠存取網路資源，包括連接埠號碼和網域 URL。</span><span class="sxs-lookup"><span data-stu-id="bd221-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="bd221-131">對於 Proxy 伺服器，您需要確保代理程式設定中已設定了適當的 Proxy 伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="bd221-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="bd221-132">對於會限制網際網路存取的防火牆，您或您的網路工程師必須將防火牆設定為允許存取 OMS。</span><span class="sxs-lookup"><span data-stu-id="bd221-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="bd221-133">您不需要在代理程式設定中進行任何動作。</span><span class="sxs-lookup"><span data-stu-id="bd221-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="bd221-134">下表說明通訊所需資源。</span><span class="sxs-lookup"><span data-stu-id="bd221-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="bd221-135">下列某些資源所提到的 Operational Insights 是 Log Analytics 先前的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd221-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="bd221-136">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="bd221-136">Agent Resource</span></span> | <span data-ttu-id="bd221-137">連接埠</span><span class="sxs-lookup"><span data-stu-id="bd221-137">Ports</span></span> | <span data-ttu-id="bd221-138">略過 HTTPS 檢查</span><span class="sxs-lookup"><span data-stu-id="bd221-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="bd221-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd221-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="bd221-140">443</span><span class="sxs-lookup"><span data-stu-id="bd221-140">443</span></span> | <span data-ttu-id="bd221-141">是</span><span class="sxs-lookup"><span data-stu-id="bd221-141">Yes</span></span> |
| <span data-ttu-id="bd221-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd221-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="bd221-143">443</span><span class="sxs-lookup"><span data-stu-id="bd221-143">443</span></span> | <span data-ttu-id="bd221-144">是</span><span class="sxs-lookup"><span data-stu-id="bd221-144">Yes</span></span> |
| <span data-ttu-id="bd221-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="bd221-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="bd221-146">443</span><span class="sxs-lookup"><span data-stu-id="bd221-146">443</span></span> | <span data-ttu-id="bd221-147">是</span><span class="sxs-lookup"><span data-stu-id="bd221-147">Yes</span></span> |
| <span data-ttu-id="bd221-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="bd221-148">*.azure-automation.net</span></span> | <span data-ttu-id="bd221-149">443</span><span class="sxs-lookup"><span data-stu-id="bd221-149">443</span></span> | <span data-ttu-id="bd221-150">是</span><span class="sxs-lookup"><span data-stu-id="bd221-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="bd221-151">從 OMS 下載代理程式安裝檔案</span><span class="sxs-lookup"><span data-stu-id="bd221-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="bd221-152">在 OMS 入口網站的 [概觀] 頁面中，按一下 [設定] 圖格。</span><span class="sxs-lookup"><span data-stu-id="bd221-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="bd221-153">按一下頂端的 [連接的來源] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bd221-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="bd221-154">![連接的來源索引標籤](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="bd221-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="bd221-155">按一下 [Windows 伺服器]，然後按一下適用於電腦處理器類型的 [下載 Windows 代理程式] 來下載安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="bd221-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="bd221-156">按一下 [工作區識別碼] 右邊的複製圖示，然後將識別碼貼入記事本中。</span><span class="sxs-lookup"><span data-stu-id="bd221-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="bd221-157">按一下 [主要索引鍵] 右邊的複製圖示，然後將識別碼貼入記事本中。</span><span class="sxs-lookup"><span data-stu-id="bd221-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="bd221-158">使用安裝程式安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="bd221-158">Install the agent using setup</span></span>
1. <span data-ttu-id="bd221-159">在您想要管理的電腦上執行安裝程式以安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="bd221-160">在 [歡迎] 頁面中按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="bd221-161">閱讀 [授權條款] 頁面上的授權，然後按一下 [我接受] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="bd221-162">在 [目的地資料夾] 頁面中，變更或保留預設的安裝資料夾，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="bd221-163">在 [代理程式安裝程式選項] 頁面中，您可以選擇將代理程式連接至 Azure Log Analytics (OMS)、Operations Manager，或者，如果您想要稍後再設定代理程式可以選擇保留空白。</span><span class="sxs-lookup"><span data-stu-id="bd221-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="bd221-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-164">Click **Next**.</span></span>   
    - <span data-ttu-id="bd221-165">如果您選擇連接至 Azure Log Analytics (OMS)，請將您在上一個程序複製到 [記事本] 的內容貼到 [工作區識別碼] 和 [工作區索引鍵 (主索引鍵)]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bd221-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="bd221-166">![貼上工作區識別碼和主索引鍵](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="bd221-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="bd221-167">如果您選擇連接到 Operations Manager，請輸入 [管理群組名稱]、[管理伺服器] 名稱、[管理伺服器連接埠]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bd221-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="bd221-168">在 [代理程式動作帳戶] 頁面上，選擇本機系統帳戶或本機網域帳戶，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="bd221-169">![管理群組設定](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![代理程式動作帳戶](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="bd221-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="bd221-170">在 [準備好安裝] 頁面上，檢閱您的選擇，然後按一下 [安裝] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="bd221-171">在 [組態完成] 頁面中，按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="bd221-172">完成時，[Microsoft 監視代理程式] 會出現在 [控制台] 中。</span><span class="sxs-lookup"><span data-stu-id="bd221-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="bd221-173">您可以檢閱您的設定，並確認代理程式已連接到 Operational Insights (OMS)。</span><span class="sxs-lookup"><span data-stu-id="bd221-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="bd221-174">當連接到 OMS，代理程式會顯示訊息︰**Microsoft Monitoring Agent 已成功連接到 Microsoft Operations Management Suite 服務。**</span><span class="sxs-lookup"><span data-stu-id="bd221-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="bd221-175">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="bd221-175">Configure proxy settings</span></span>

<span data-ttu-id="bd221-176">您可以使用以下程序來使用控制台為 Microsoft Monitoring Agent 設定 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="bd221-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="bd221-177">您需要針對每部伺服器使用此程序。</span><span class="sxs-lookup"><span data-stu-id="bd221-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="bd221-178">如果您需要設定許多伺服器，使用指令碼將此程序自動化會比較容易。</span><span class="sxs-lookup"><span data-stu-id="bd221-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="bd221-179">如果是，請參閱下一個程序 [使用指令碼設定 Microsoft Monitoring Agent 的 Proxy 設定](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script)。</span><span class="sxs-lookup"><span data-stu-id="bd221-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="bd221-180">使用控制台設定 Microsoft Monitoring Agent 的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="bd221-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="bd221-181">開啟 [ **控制台**]。</span><span class="sxs-lookup"><span data-stu-id="bd221-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="bd221-182">開啟 [ **Microsoft Monitoring Agent**].</span><span class="sxs-lookup"><span data-stu-id="bd221-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="bd221-183">按一下 [ **Proxy 設定** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bd221-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="bd221-184">![[Proxy 設定] 索引標籤](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="bd221-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="bd221-185">選取 [ **使用 Proxy 伺服器** ] 並輸入 URL 與連接埠號碼 (如果需要)，如範例所示。</span><span class="sxs-lookup"><span data-stu-id="bd221-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="bd221-186">如果您的 Proxy 伺服器需要驗證，請輸入使用者名稱與密碼以存取 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bd221-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="bd221-187">確認代理程式能夠連線到 OMS</span><span class="sxs-lookup"><span data-stu-id="bd221-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="bd221-188">您可以使用下列程序，輕鬆地確認代理程式是否能夠與 OMS 通訊︰</span><span class="sxs-lookup"><span data-stu-id="bd221-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="bd221-189">在具有 Windows 代理程式的電腦上，開啟 [控制台]。</span><span class="sxs-lookup"><span data-stu-id="bd221-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="bd221-190">開啟 [Microsoft Monitoring Agent]。</span><span class="sxs-lookup"><span data-stu-id="bd221-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="bd221-191">按一下 [Azure Log Analytics (OMS)] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bd221-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="bd221-192">在 [狀態] 欄中，您應該會看到代理程式已成功連線到 Operations Management Suite 服務。</span><span class="sxs-lookup"><span data-stu-id="bd221-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![代理程式已連線](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="bd221-194">使用指令碼設定 Microsoft Monitoring Agent 的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="bd221-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="bd221-195">複製下列範例、以您的環境的特定資訊進行更新、儲存為 PS1 副檔名，然後在直接連接到 OMS 服務的每一部電腦上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="bd221-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
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

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="bd221-196">使用命令列安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="bd221-196">Install the agent using the command line</span></span>
- <span data-ttu-id="bd221-197">修改，然後搭配使用下列範例與命令列來安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="bd221-198">這個範例會執行完全無訊息安裝。</span><span class="sxs-lookup"><span data-stu-id="bd221-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="bd221-199">如果您想要升級代理程式，您需要使用 Log Analytics 指令碼 API。</span><span class="sxs-lookup"><span data-stu-id="bd221-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="bd221-200">請參閱下一節來升級代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="bd221-201">代理程式使用 `/c` 命令將 IExpress 用作其自我解壓縮程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="bd221-202">您可以在 [IExpress 的命令列參數](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages)中查看命令列參數，然後更新範例以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="bd221-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="bd221-203">MMA 專屬選項</span><span class="sxs-lookup"><span data-stu-id="bd221-203">MMA-specific options</span></span>                   |<span data-ttu-id="bd221-204">注意事項</span><span class="sxs-lookup"><span data-stu-id="bd221-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="bd221-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="bd221-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="bd221-206">1 = 將代理程式設定為向工作區報告</span><span class="sxs-lookup"><span data-stu-id="bd221-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="bd221-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="bd221-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="bd221-208">要新增之工作區的工作區識別碼 (guid)</span><span class="sxs-lookup"><span data-stu-id="bd221-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="bd221-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="bd221-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="bd221-210">用來向工作區進行初始驗證的工作區金鑰</span><span class="sxs-lookup"><span data-stu-id="bd221-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="bd221-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="bd221-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="bd221-212">指定工作區所在的雲端環境</span><span class="sxs-lookup"><span data-stu-id="bd221-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="bd221-213">0 = Azure 商業雲端 (預設值)</span><span class="sxs-lookup"><span data-stu-id="bd221-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="bd221-214">1 = Azure Government</span><span class="sxs-lookup"><span data-stu-id="bd221-214">1 = Azure Government</span></span> |
|<span data-ttu-id="bd221-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="bd221-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="bd221-216">要使用的 Proxy URI</span><span class="sxs-lookup"><span data-stu-id="bd221-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="bd221-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="bd221-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="bd221-218">要存取已驗證 Proxy 的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="bd221-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="bd221-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="bd221-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="bd221-220">要存取已驗證 Proxy 的密碼</span><span class="sxs-lookup"><span data-stu-id="bd221-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="bd221-221">為了避免達到 IExpress 的命令列長度限制，請安裝沒有設定工作區的代理程式，然後使用指令碼來設定工作區組態。</span><span class="sxs-lookup"><span data-stu-id="bd221-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="bd221-222">如果您在使用 `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` 參數時收到 `Command line option syntax error.`，您可以使用下列因應措施︰</span><span class="sxs-lookup"><span data-stu-id="bd221-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="bd221-223">使用指令碼來新增工作區</span><span class="sxs-lookup"><span data-stu-id="bd221-223">Add a workspace using a script</span></span>
<span data-ttu-id="bd221-224">您可以參考下列範例，使用 Log Analytics 代理程式指令碼 API 來新增工作區：</span><span class="sxs-lookup"><span data-stu-id="bd221-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="bd221-225">若要在適用於美國政府的 Azure 中新增工作區，請使用下列指令碼範例︰</span><span class="sxs-lookup"><span data-stu-id="bd221-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="bd221-226">如果您先前使用過命令列或指令碼來安裝或設定代理程式，`EnableAzureOperationalInsights` 會換成 `AddCloudWorkspace`。</span><span class="sxs-lookup"><span data-stu-id="bd221-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="bd221-227">使用 Azure 自動化中的 DSC 安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="bd221-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="bd221-228">您可以用下列指令碼範例，使用 Azure 自動化中的 DSC 來安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="bd221-229">此範例會安裝 64 位元代理程式，可由 `URI` 值識別。</span><span class="sxs-lookup"><span data-stu-id="bd221-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="bd221-230">您也可以取代 URI 值改為使用 32 位元版本。</span><span class="sxs-lookup"><span data-stu-id="bd221-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="bd221-231">這兩個版本的 URI 分別是︰</span><span class="sxs-lookup"><span data-stu-id="bd221-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="bd221-232">Windows 64 位元代理程式 - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="bd221-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="bd221-233">Windows 32 位元代理程式 - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="bd221-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="bd221-234">此程序和指令碼範例不會升級現有的代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="bd221-235">從 [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) 將 xPSDesiredStateConfiguration DSC 模組匯入 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="bd221-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="bd221-236">建立 Azure 自動化的 *OPSINSIGHTS_WS_ID* 和 *OPSINSIGHTS_WS_KEY* 變數資產。</span><span class="sxs-lookup"><span data-stu-id="bd221-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="bd221-237">將 *OPSINSIGHTS_WS_ID* 設定為您的 OMS Log Analytics 工作區識別碼，將 *OPSINSIGHTS_WS_KEY* 設定為工作區的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bd221-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="bd221-238">使用下列指令碼並將其儲存為 MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="bd221-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="bd221-239">修改並使用下列範例來使用 Azure 自動化中的 DSC 安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="bd221-240">使用 Azure 自動化介面或 Cmdlet 將 MMAgent.ps1 匯入 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="bd221-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="bd221-241">指派節點至設定。</span><span class="sxs-lookup"><span data-stu-id="bd221-241">Assign a node to the configuration.</span></span> <span data-ttu-id="bd221-242">在 15 分鐘內，節點會檢查其設定，然後系統會將 MMA 推送至節點。</span><span class="sxs-lookup"><span data-stu-id="bd221-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

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

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="bd221-243">取得最新的 ProductId 值</span><span class="sxs-lookup"><span data-stu-id="bd221-243">Get the latest ProductId value</span></span>

<span data-ttu-id="bd221-244">MMAgent.ps1 指令碼中的 `ProductId value`，對應不同的代理程式版本。</span><span class="sxs-lookup"><span data-stu-id="bd221-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="bd221-245">當每個代理程式的更新的版本發佈時，ProductId 的值隨之變更。</span><span class="sxs-lookup"><span data-stu-id="bd221-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="bd221-246">因此，當未來 ProductId 變更時，您可以使用簡單的指令碼找到代理程式版本。</span><span class="sxs-lookup"><span data-stu-id="bd221-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="bd221-247">在測試伺服器上安裝最新的代理程式版本之後，您可以使用下列指令碼取得已安裝的 ProductId 值。</span><span class="sxs-lookup"><span data-stu-id="bd221-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="bd221-248">您可以使用最新的 ProductId 值，更新 MMAgent.ps1 指令碼中的這個值。</span><span class="sxs-lookup"><span data-stu-id="bd221-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="bd221-249">手動設定代理程式，或新增額外的工作區</span><span class="sxs-lookup"><span data-stu-id="bd221-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="bd221-250">如果您已安裝代理程式但尚未設定，或是您希望代理程式向多個工作區報告，您可以使用下列資訊來啟用或重新設定代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="bd221-251">設定代理程式之後，它會註冊代理程式服務，並將獲得所需的組態資訊及包含解決方案資訊的管理組件。</span><span class="sxs-lookup"><span data-stu-id="bd221-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="bd221-252">安裝 Microsoft Monitoring Agent 之後，開啟 [控制台] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="bd221-253">開啟 **Microsoft Monitoring Agent**，然後按一下 [Azure Log Analytics (OMS)] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bd221-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="bd221-254">按一下 [新增] 以開啟 [新增 Log Analytics 工作區] 方塊。</span><span class="sxs-lookup"><span data-stu-id="bd221-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="bd221-255">針對您要新增的工作區，將您在上一個程序複製到 [記事本] 的內容貼到 [工作區識別碼] 和 [工作區索引鍵 (主索引鍵)]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bd221-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="bd221-256">![設定 Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="bd221-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="bd221-257">代理程式從所監視的電腦收集資料之後，受 OMS 監視的電腦數目會出現在 OMS 入口網站的 [設定] 中 [連接的來源] 索引標籤下的 [連接的伺服器]。</span><span class="sxs-lookup"><span data-stu-id="bd221-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="bd221-258">停用代理程式</span><span class="sxs-lookup"><span data-stu-id="bd221-258">To disable an agent</span></span>
1. <span data-ttu-id="bd221-259">安裝代理程式之後，開啟 [ **控制台**]。</span><span class="sxs-lookup"><span data-stu-id="bd221-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="bd221-260">開啟 Microsoft Monitoring Agent，然後按一下 [Azure Log Analytics (OMS)]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bd221-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="bd221-261">選取工作區，然後按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="bd221-262">對其他所有工作區重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="bd221-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="bd221-263">(選擇性) 將代理程式設定為向 Operations Manager 管理群組報告</span><span class="sxs-lookup"><span data-stu-id="bd221-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="bd221-264">如果您在 IT 基礎結構中使用 Operations Manager，您也可以使用 MMA 代理程式做為 Operations Manager 代理程式。</span><span class="sxs-lookup"><span data-stu-id="bd221-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="bd221-265">將 MMA 代理程式設定為向 Operations Manager 管理群組報告</span><span class="sxs-lookup"><span data-stu-id="bd221-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="bd221-266">在已安裝代理程式的電腦上，開啟 [控制台] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="bd221-267">開啟 **Microsoft Monitoring Agent**，然後按一下 [Operations Manager] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bd221-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="bd221-268">![Microsoft 監視代理程式 Operations Manager 索引標籤](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="bd221-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="bd221-269">如果 Operations Manager 伺服器已與 Active Directory 整合，請按一下 [自動更新來自 AD DS 的管理群組指派] 。</span><span class="sxs-lookup"><span data-stu-id="bd221-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="bd221-270">按一下 [新增] 以開啟 [新增管理群組] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bd221-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="bd221-271">![Microsoft 監視代理程式新增管理群組](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="bd221-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="bd221-272">在[管理群組名稱]  方塊中，輸入管理群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd221-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="bd221-273">在 [主要管理伺服器]  方塊中，輸入主要管理伺服器的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="bd221-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="bd221-274">在 [管理伺服器連接埠]  方塊中，輸入 TCP 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="bd221-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="bd221-275">在 [代理程式動作帳戶] 頁面下，選擇本機系統帳戶或本機網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd221-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="bd221-276">按一下 [確定] 關閉 [新增管理群組] 對話方塊，然後按一下 [確定] 關閉 [Microsoft 監視代理程式內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bd221-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd221-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd221-277">Next steps</span></span>

- <span data-ttu-id="bd221-278">[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)，以新增功能和收集資料。</span><span class="sxs-lookup"><span data-stu-id="bd221-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
