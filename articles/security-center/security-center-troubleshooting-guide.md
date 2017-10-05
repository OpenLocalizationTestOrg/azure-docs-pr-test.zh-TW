---
title: "Azure 資訊安全中心疑難排解指南 | Microsoft Docs"
description: "本文件有助於在 Azure 資訊安全中心排解疑難問題。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 0e0a0ce5c0795cec0e47cd5f729099f4762381a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a><span data-ttu-id="16cc5-103">Azure 資訊安全中心疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="16cc5-103">Azure Security Center Troubleshooting Guide</span></span>
<span data-ttu-id="16cc5-104">本指南適用於組織目前採用 Azure 資訊安全中心，且需要針對資訊安全中心相關問題進行疑難排解的資訊技術 (IT) 專業人員、資訊安全性分析師和雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="16cc5-104">This guide is for information technology (IT) professionals, information security analysts, and cloud administrators whose organizations are using Azure Security Center and need to troubleshoot Security Center related issues.</span></span>

>[!NOTE] 
><span data-ttu-id="16cc5-105">從 2017 年 6 月初開始，資訊安全中心會使用 Microsoft Monitoring Agent 來收集和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="16cc5-105">Beginning in early June 2017, Security Center uses the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="16cc5-106">若要深入了解，請參閱 [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="16cc5-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="16cc5-107">本文中的資訊說明轉換至 Microsoft Monitoring Agent 後的資訊安全中心功能。</span><span class="sxs-lookup"><span data-stu-id="16cc5-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>

## <a name="troubleshooting-guide"></a><span data-ttu-id="16cc5-108">疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="16cc5-108">Troubleshooting guide</span></span>
<span data-ttu-id="16cc5-109">本指南說明如何針對資訊安全中心相關問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="16cc5-109">This guide explains how to troubleshoot Security Center related issues.</span></span> <span data-ttu-id="16cc5-110">大多數在資訊安全中心進行的疑難排解作業會先查看失敗元件的[稽核記錄](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/)。</span><span class="sxs-lookup"><span data-stu-id="16cc5-110">Most of the troubleshooting done in Security Center takes place by first looking at the [Audit Log](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) records for the failed component.</span></span> <span data-ttu-id="16cc5-111">透過稽核記錄檔，您可以判斷︰</span><span class="sxs-lookup"><span data-stu-id="16cc5-111">Through audit logs, you can determine:</span></span>

* <span data-ttu-id="16cc5-112">已發生的作業</span><span class="sxs-lookup"><span data-stu-id="16cc5-112">Which operations were taken place</span></span>
* <span data-ttu-id="16cc5-113">起始作業的人員</span><span class="sxs-lookup"><span data-stu-id="16cc5-113">Who initiated the operation</span></span>
* <span data-ttu-id="16cc5-114">發生作業的時間</span><span class="sxs-lookup"><span data-stu-id="16cc5-114">When the operation occurred</span></span>
* <span data-ttu-id="16cc5-115">作業的狀態</span><span class="sxs-lookup"><span data-stu-id="16cc5-115">The status of the operation</span></span>
* <span data-ttu-id="16cc5-116">其他可能協助您研究作業的屬性值</span><span class="sxs-lookup"><span data-stu-id="16cc5-116">The values of other properties that might help you research the operation</span></span>

<span data-ttu-id="16cc5-117">稽核記錄檔包含在您的資源上執行的所有寫入作業 (PUT、POST、DELETE)，但不包含讀取作業 (GET)。</span><span class="sxs-lookup"><span data-stu-id="16cc5-117">The audit log contains all write operations (PUT, POST, DELETE) performed on your resources, however it does not include read operations (GET).</span></span>

## <a name="microsoft-monitoring-agent"></a><span data-ttu-id="16cc5-118">Microsoft Monitoring Agent</span><span class="sxs-lookup"><span data-stu-id="16cc5-118">Microsoft Monitoring Agent</span></span>
<span data-ttu-id="16cc5-119">資訊安全中心會使用 Microsoft Monitoring Agent (這是 Operations Management Suite 和 Log Analytics 服務所用的相同代理程式) 從 Azure 虛擬機器收集安全性資料。</span><span class="sxs-lookup"><span data-stu-id="16cc5-119">Security Center uses the Microsoft Monitoring Agent – this is the same agent used by the Operations Management Suite and Log Analytics service – to collect security data from your Azure virtual machines.</span></span> <span data-ttu-id="16cc5-120">啟用資料收集且代理程式已正確安裝在目標電腦之後，以下處理序應在執行中︰</span><span class="sxs-lookup"><span data-stu-id="16cc5-120">After data collection is enabled and the agent is correctly installed in the target machine, the process below should be in execution:</span></span>

* <span data-ttu-id="16cc5-121">HealthService.exe</span><span class="sxs-lookup"><span data-stu-id="16cc5-121">HealthService.exe</span></span>

<span data-ttu-id="16cc5-122">如果您開啟服務管理主控台 (services.msc)，您也會看到執行中的 Microsoft Monitoring Agent 服務，如下所示：</span><span class="sxs-lookup"><span data-stu-id="16cc5-122">If you open the services management console (services.msc), you will also see the Microsoft Monitoring Agent service running as shown below:</span></span>

![服務](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

<span data-ttu-id="16cc5-124">若要查看您擁有的代理程式版本，請開啟 [工作管理員]，在 [處理序] 索引標籤中找出 [Microsoft Monitoring Agent 服務]，以滑鼠右鍵按一下它並按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="16cc5-124">To see which version of the agent you have, open **Task Manager**, in the **Processes** tab locate the **Microsoft Monitoring Agent Service**, right-click on it and click **Properties**.</span></span> <span data-ttu-id="16cc5-125">在 [詳細資料] 索引標籤上，查看如下所示的檔案版本：</span><span class="sxs-lookup"><span data-stu-id="16cc5-125">In the **Details** tab, look the file version as shown below:</span></span>

![檔案](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a><span data-ttu-id="16cc5-127">Microsoft Monitoring Agent 安裝案例</span><span class="sxs-lookup"><span data-stu-id="16cc5-127">Microsoft Monitoring Agent installation scenarios</span></span>
<span data-ttu-id="16cc5-128">在電腦上安裝 Microsoft Monitoring Agent 時，有兩個可產生不同結果的安裝案例。</span><span class="sxs-lookup"><span data-stu-id="16cc5-128">There are two installation scenarios that can produce different results when installing the Microsoft Monitoring Agent on your computer.</span></span> <span data-ttu-id="16cc5-129">支援的案例如下：</span><span class="sxs-lookup"><span data-stu-id="16cc5-129">The supported scenarios are:</span></span>

* <span data-ttu-id="16cc5-130">**資訊安全中心自動安裝的代理程式**：在此案例中，您能夠在兩個位置 (資訊安全中心和記錄搜尋) 檢視警示。</span><span class="sxs-lookup"><span data-stu-id="16cc5-130">**Agent installed automatically by Security Center**: in this scenario you will be able to view the alerts in both locations, Security Center and Log search.</span></span> <span data-ttu-id="16cc5-131">您會收到電子郵件通知，這些通知會寄送至在資源所屬訂用帳戶的安全性原則中設定的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="16cc5-131">You will receive e-mail notifications to the email address that was configured in the security policy for the subscription the resource belongs to.</span></span>
<span data-ttu-id="16cc5-132">。</span><span class="sxs-lookup"><span data-stu-id="16cc5-132">.</span></span>
* <span data-ttu-id="16cc5-133">**手動安裝於 Azure 中 VM 上的代理程式**：在此案例中，如果您使用在 2017 年 2 月之前下載並手動安裝的代理程式，唯有依據工作區所屬的訂用帳戶篩選，您才能夠在資訊安全中心入口網站中檢視警示。</span><span class="sxs-lookup"><span data-stu-id="16cc5-133">**Agent manually installed on a VM located in Azure**: in this scenario, if you are using agents downloaded and installed manually prior to February 2017, you will be able to view the alerts in the Security Center portal only if you filter on the subscription the workspace belongs to.</span></span> <span data-ttu-id="16cc5-134">在您依據資源所屬的訂用帳戶篩選時，您將無法看到任何警示。</span><span class="sxs-lookup"><span data-stu-id="16cc5-134">In case you filter on the subscription the resource belongs to, you won’t be able to see any alerts.</span></span> <span data-ttu-id="16cc5-135">您會收到電子郵件通知，這些通知會寄送至在工作區所屬訂用帳戶的安全性原則中設定的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="16cc5-135">You will receive e-mail notifications to the email address that was configured in the security policy for the subscription the workspace belongs to.</span></span>

>[!NOTE]
> <span data-ttu-id="16cc5-136">若要避免第二個案例中說明的行為，務必下載最新版的代理程式。</span><span class="sxs-lookup"><span data-stu-id="16cc5-136">To avoid the behavior explained in the second, make sure you download the latest version of the agent.</span></span>
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a><span data-ttu-id="16cc5-137">針對監視代理程式網路需求進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="16cc5-137">Troubleshooting monitoring agent network requirements</span></span>
<span data-ttu-id="16cc5-138">代理程式若要連線到資訊安全中心並向其註冊，就必須能夠存取網路資源，包括連接埠號碼和網域 URL。</span><span class="sxs-lookup"><span data-stu-id="16cc5-138">For agents to connect to and register with Security Center, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="16cc5-139">對於 Proxy 伺服器，您需要確保代理程式設定中已設定了適當的 Proxy 伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="16cc5-139">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span> <span data-ttu-id="16cc5-140">如需有關[如何變更 Proxy 設定](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings)的詳細資訊，請參閱這篇文章。</span><span class="sxs-lookup"><span data-stu-id="16cc5-140">Read this article for more information on [how to change the proxy settings](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).</span></span>
- <span data-ttu-id="16cc5-141">對於限制網際網路存取的防火牆，您需要設定防火牆以允許存取 OMS。</span><span class="sxs-lookup"><span data-stu-id="16cc5-141">For firewalls that restrict access to the Internet, you need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="16cc5-142">您不需要在代理程式設定中進行任何動作。</span><span class="sxs-lookup"><span data-stu-id="16cc5-142">No action is needed in agent settings.</span></span>

<span data-ttu-id="16cc5-143">下表說明通訊所需資源。</span><span class="sxs-lookup"><span data-stu-id="16cc5-143">The following table shows resources needed for communication.</span></span>

| <span data-ttu-id="16cc5-144">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="16cc5-144">Agent Resource</span></span> | <span data-ttu-id="16cc5-145">連接埠</span><span class="sxs-lookup"><span data-stu-id="16cc5-145">Ports</span></span> | <span data-ttu-id="16cc5-146">略過 HTTPS 檢查</span><span class="sxs-lookup"><span data-stu-id="16cc5-146">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="16cc5-147">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="16cc5-147">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="16cc5-148">443</span><span class="sxs-lookup"><span data-stu-id="16cc5-148">443</span></span> | <span data-ttu-id="16cc5-149">是</span><span class="sxs-lookup"><span data-stu-id="16cc5-149">Yes</span></span> |
| <span data-ttu-id="16cc5-150">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="16cc5-150">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="16cc5-151">443</span><span class="sxs-lookup"><span data-stu-id="16cc5-151">443</span></span> | <span data-ttu-id="16cc5-152">是</span><span class="sxs-lookup"><span data-stu-id="16cc5-152">Yes</span></span> |
| <span data-ttu-id="16cc5-153">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="16cc5-153">*.blob.core.windows.net</span></span> | <span data-ttu-id="16cc5-154">443</span><span class="sxs-lookup"><span data-stu-id="16cc5-154">443</span></span> | <span data-ttu-id="16cc5-155">是</span><span class="sxs-lookup"><span data-stu-id="16cc5-155">Yes</span></span> |
| <span data-ttu-id="16cc5-156">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="16cc5-156">*.azure-automation.net</span></span> | <span data-ttu-id="16cc5-157">443</span><span class="sxs-lookup"><span data-stu-id="16cc5-157">443</span></span> | <span data-ttu-id="16cc5-158">是</span><span class="sxs-lookup"><span data-stu-id="16cc5-158">Yes</span></span> |

<span data-ttu-id="16cc5-159">如果您遇到代理程式的登入問題，請務必閱讀[如何針對 Operations Management Suite 登入問題進行疑難排解](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues)一文。</span><span class="sxs-lookup"><span data-stu-id="16cc5-159">If you encounter onboarding issues with the agent, make sure to read the article [How to troubleshoot Operations Management Suite onboarding issues](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).</span></span>


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a><span data-ttu-id="16cc5-160">針對端點保護無法正常運作的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="16cc5-160">Troubleshooting endpoint protection not working properly</span></span>

<span data-ttu-id="16cc5-161">客體代理程式為 [Microsoft Antimalware](../security/azure-security-antimalware.md) 擴充功能所做一切的父處理序。</span><span class="sxs-lookup"><span data-stu-id="16cc5-161">The guest agent is the parent process of everything the [Microsoft Antimalware](../security/azure-security-antimalware.md) extension does.</span></span> <span data-ttu-id="16cc5-162">當客體代理程式處理序失敗時，做為客體代理程式子處理序執行的 Microsoft Antimalware 可能也會失敗。</span><span class="sxs-lookup"><span data-stu-id="16cc5-162">When the guest agent process fails, the Microsoft Antimalware that runs as a child process of the guest agent may also fail.</span></span>  <span data-ttu-id="16cc5-163">在類似案例中，建議您確認下列選項：</span><span class="sxs-lookup"><span data-stu-id="16cc5-163">In scenarios like that is recommended to verify the following options:</span></span>

- <span data-ttu-id="16cc5-164">目標 VM 是否為自訂映像，而且 VM 的建立者從未安裝客體代理程式。</span><span class="sxs-lookup"><span data-stu-id="16cc5-164">If the target VM is a custom image and the creator of the VM never installed guest agent.</span></span>
- <span data-ttu-id="16cc5-165">如果目標為 Linux VM 而不是 Windows VM，則在 Linux VM 上安裝反惡意程式碼擴充功能的 Windows 版本將會失敗。</span><span class="sxs-lookup"><span data-stu-id="16cc5-165">If the target is a Linux VM instead of a Windows VM then installing the Windows version of the antimalware extension on a Linux VM will fail.</span></span> <span data-ttu-id="16cc5-166">Linux 客體代理程式對於 OS 版本和所需的套件具有特定需求，而且如果未符合這些需求，VM 代理程式也無法在該處運作。</span><span class="sxs-lookup"><span data-stu-id="16cc5-166">The Linux guest agent has specific requirements in terms of OS version and required packages, and if those requirements are not met the VM agent will not work there either.</span></span> 
- <span data-ttu-id="16cc5-167">VM 是否是使用舊版客體代理程式所建立。</span><span class="sxs-lookup"><span data-stu-id="16cc5-167">If the VM was created with an old version of guest agent.</span></span> <span data-ttu-id="16cc5-168">如果是，您應該注意，某些舊版代理程式可能不會將本身自動更新為較新版本，而這會導致此問題。</span><span class="sxs-lookup"><span data-stu-id="16cc5-168">If it was, you should be aware that some old agents could not auto-update itself to the newer version and this could lead to this problem.</span></span> <span data-ttu-id="16cc5-169">如果建立您自己的映像，請一律使用最新版的客體代理程式。</span><span class="sxs-lookup"><span data-stu-id="16cc5-169">Always use the latest version of guest agent if creating your own images.</span></span>
- <span data-ttu-id="16cc5-170">某些第三方系統管理軟體可能會停用客體代理程式，或封鎖特定檔案位置的存取。</span><span class="sxs-lookup"><span data-stu-id="16cc5-170">Some third-party administration software may disable the guest agent, or block access to certain file locations.</span></span> <span data-ttu-id="16cc5-171">如果您在 VM 上安裝了第三方軟體，請確定代理程式位於排除清單上。</span><span class="sxs-lookup"><span data-stu-id="16cc5-171">If you have third-party installed on your VM, make sure that the agent is on the exclusion list.</span></span>
- <span data-ttu-id="16cc5-172">某些防火牆設定或網路安全性群組 (NSG) 可能會封鎖進出客體代理程式的網路流量。</span><span class="sxs-lookup"><span data-stu-id="16cc5-172">Certain firewall settings or Network Security Group (NSG) may block network traffic to and from guest agent.</span></span>
- <span data-ttu-id="16cc5-173">某些存取控制清單 (ACL) 可能會防止磁碟存取。</span><span class="sxs-lookup"><span data-stu-id="16cc5-173">Certain Access Control List (ACL) may prevent disk access.</span></span>
- <span data-ttu-id="16cc5-174">磁碟空間不足會封鎖客體代理程式而使其無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="16cc5-174">Lack of disk space can block the guest agent from functioning properly.</span></span> 

<span data-ttu-id="16cc5-175">預設會停用 Microsoft Antimalware 使用者介面，如需如何視需要啟用此功能的詳細資訊，請閱讀[在 Azure Resource Manager VM 後續部署上啟用 Microsoft Antimalware 使用者介面 (英文)](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/)。</span><span class="sxs-lookup"><span data-stu-id="16cc5-175">By default the Microsoft Antimalware User Interface is disabled, read [Enabling Microsoft Antimalware User Interface on Azure Resource Manager VMs Post Deployment](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) for more information on how to enable it if you need.</span></span>

## <a name="troubleshooting-problems-loading-the-dashboard"></a><span data-ttu-id="16cc5-176">針對載入儀表板的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="16cc5-176">Troubleshooting problems loading the dashboard</span></span>

<span data-ttu-id="16cc5-177">如果您遇到載入資訊安全中心儀表板的問題，請確定向資訊安全中心註冊訂用帳戶的使用者 (也就是第一位使用訂用帳戶開啟資訊安全中心的使用者) 以及想要開啟資料收集的使用者，應該是訂用帳戶的「擁有者」或「參與者」。</span><span class="sxs-lookup"><span data-stu-id="16cc5-177">If you experience issues loading the Security Center dashboard, ensure that the user that registers the subscription to Security Center (i.e. the first user one who opened Security Center with the subscription) and the user who would like to turn on data collection should be *Owner* or *Contributor* on the subscription.</span></span> <span data-ttu-id="16cc5-178">另外，從那時起，訂用帳戶上具有「讀取者」身分的使用者就可以看到儀表板/警示/建議/原則。</span><span class="sxs-lookup"><span data-stu-id="16cc5-178">From that moment on also users with *Reader* on the subscription can see the dashboard/alerts/recommendation/policy.</span></span>

## <a name="contacting-microsoft-support"></a><span data-ttu-id="16cc5-179">連絡 Microsoft 支援服務</span><span class="sxs-lookup"><span data-stu-id="16cc5-179">Contacting Microsoft Support</span></span>
<span data-ttu-id="16cc5-180">使用本文提供的指導方針可識別一些問題，您也可能發現的其他問題則記載於資訊安全中心的公開 [論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter)。</span><span class="sxs-lookup"><span data-stu-id="16cc5-180">Some issues can be identified using the guidelines provided in this article, others you can also find documented at the Security Center public [Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter).</span></span> <span data-ttu-id="16cc5-181">不過，如果您需要進一步疑難排解，您可以使用 **Azure 入口網站**開啟新的支援要求，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="16cc5-181">However if you need further troubleshooting, you can open a new support request using **Azure portal** as shown below:</span></span> 

![Microsoft 支援服務](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a><span data-ttu-id="16cc5-183">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16cc5-183">See also</span></span>
<span data-ttu-id="16cc5-184">在本文件中，您已了解如何在「Azure 資訊安全中心」設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="16cc5-184">In this document, you learned how to configure security policies in Azure Security Center.</span></span> <span data-ttu-id="16cc5-185">若要深入了解「Azure 資訊安全中心」，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="16cc5-185">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="16cc5-186">[Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md) — 了解如何規劃及了解採用 Azure 資訊安全中心的設計考量。</span><span class="sxs-lookup"><span data-stu-id="16cc5-186">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="16cc5-187">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) — 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="16cc5-187">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources</span></span>
* <span data-ttu-id="16cc5-188">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) — 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="16cc5-188">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts</span></span>
* <span data-ttu-id="16cc5-189">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) — 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="16cc5-189">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="16cc5-190">[Azure 資訊安全中心常見問題集](security-center-faq.md) — 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="16cc5-190">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service</span></span>
* <span data-ttu-id="16cc5-191">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="16cc5-191">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>

