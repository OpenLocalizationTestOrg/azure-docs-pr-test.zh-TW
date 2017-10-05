---
title: "將安全性產品連接至 Operations Management Suite (OMS) 安全性和稽核解決方案 | Microsoft Docs"
description: "本文件可協助您使用常見事件格式，將安全性產品連接至 Operations Management Suite 安全性和稽核解決方案。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 710a1fe0ce2b7a1841187cf75f4ffb090cc161e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="5d004-103">將安全性產品連接至 Operations Management Suite (OMS) 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="5d004-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="5d004-104">本文件可協助您將安全性產品連接至 OMS 安全性和稽核解決方案。</span><span class="sxs-lookup"><span data-stu-id="5d004-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="5d004-105">支援的來源如下：</span><span class="sxs-lookup"><span data-stu-id="5d004-105">The following sources are supported:</span></span>

- <span data-ttu-id="5d004-106">常見事件格式 (CEF) 事件</span><span class="sxs-lookup"><span data-stu-id="5d004-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="5d004-107">Cisco ASA 事件</span><span class="sxs-lookup"><span data-stu-id="5d004-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="5d004-108">什麼是 CEF？</span><span class="sxs-lookup"><span data-stu-id="5d004-108">What is CEF?</span></span>
<span data-ttu-id="5d004-109">常見事件格式 (CEF) 是一種以 Syslog 訊息為基礎的業界標準格式，許多安全性廠商使用此格式來讓事件可在不同平台之間互通。</span><span class="sxs-lookup"><span data-stu-id="5d004-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="5d004-110">OMS 安全性和稽核解決方案使用 CEF 支援資料擷取，而讓您可以連接安全性產品與 OMS 安全性。</span><span class="sxs-lookup"><span data-stu-id="5d004-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="5d004-111">藉由將資料來源連接至 OMS，您可以充分利用屬於此平台的下列功能︰</span><span class="sxs-lookup"><span data-stu-id="5d004-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="5d004-112">搜尋與相互關聯</span><span class="sxs-lookup"><span data-stu-id="5d004-112">Search & Correlation</span></span>
- <span data-ttu-id="5d004-113">稽核</span><span class="sxs-lookup"><span data-stu-id="5d004-113">Auditing</span></span>
- <span data-ttu-id="5d004-114">警示</span><span class="sxs-lookup"><span data-stu-id="5d004-114">Alert</span></span>
- <span data-ttu-id="5d004-115">威脅情報</span><span class="sxs-lookup"><span data-stu-id="5d004-115">Threat Intelligence</span></span>
- <span data-ttu-id="5d004-116">值得注意的問題</span><span class="sxs-lookup"><span data-stu-id="5d004-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="5d004-117">收集安全性解決方案的記錄檔</span><span class="sxs-lookup"><span data-stu-id="5d004-117">Collection of security solution logs</span></span>

<span data-ttu-id="5d004-118">OMS 安全性支援收集使用 CEF over Syslogs 的記錄檔和 [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d004-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="5d004-119">在此範例中，來源 (會產生記錄檔的電腦) 是執行 syslog-ng 精靈的 Linux 電腦，目標則是 OMS 安全性。</span><span class="sxs-lookup"><span data-stu-id="5d004-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="5d004-120">若要準備 Linux 電腦，您必須執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="5d004-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="5d004-121">下載 OMS Agent for Linux 1.2.0-25 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5d004-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="5d004-122">依照[這篇文章](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)的**快速安裝指南**一節，將代理程式安裝並加入工作區。</span><span class="sxs-lookup"><span data-stu-id="5d004-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="5d004-123">一般而言，代理程式安裝所在的電腦會與產生記錄檔的電腦不同。</span><span class="sxs-lookup"><span data-stu-id="5d004-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="5d004-124">將記錄檔轉送至代理程式機器通常需要進行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="5d004-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="5d004-125">在代理程式機器上，將記錄產品/機器設定為轉送所需事件到 syslog 精靈 (rsyslog 或 syslog-ng)。</span><span class="sxs-lookup"><span data-stu-id="5d004-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="5d004-126">在代理程式機器上啟用 syslog 精靈，以從遠端系統接收訊息。</span><span class="sxs-lookup"><span data-stu-id="5d004-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="5d004-127">在代理程式機器上，必須從 syslog 精靈將事件傳送到本機 UDP 連接埠 25226。</span><span class="sxs-lookup"><span data-stu-id="5d004-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="5d004-128">代理程式將會接聽此連接埠上的內送事件。</span><span class="sxs-lookup"><span data-stu-id="5d004-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="5d004-129">以下範例組態會將本機系統的所有事件傳送至代理程式 (您可以修改組態以符合您的本機設定)︰</span><span class="sxs-lookup"><span data-stu-id="5d004-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="5d004-130">開啟終端機視窗，並移至目錄 /etc/syslog-ng/</span><span class="sxs-lookup"><span data-stu-id="5d004-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="5d004-131">建立新檔案 security-config-omsagent.conf，並新增下列內容︰OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="5d004-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="5d004-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="5d004-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="5d004-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="5d004-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="5d004-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="5d004-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="5d004-135">下載 security_events.conf 檔案並放在 OMS Agent 電腦中的 */etc/opt/microsoft/omsagent/conf/omsagent.d/*。</span><span class="sxs-lookup"><span data-stu-id="5d004-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="5d004-136">輸入下列命令重新啟動 syslog 服務精靈：*的 syslog ng 執行：*</span><span class="sxs-lookup"><span data-stu-id="5d004-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="5d004-137">若為 rsyslog 執行︰</span><span class="sxs-lookup"><span data-stu-id="5d004-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="5d004-138">輸入下列命令來重新啟動 OMS Agent︰</span><span class="sxs-lookup"><span data-stu-id="5d004-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="5d004-139">*若為 syslog-ng 執行* ︰</span><span class="sxs-lookup"><span data-stu-id="5d004-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="5d004-140">若為 rsyslog 執行︰</span><span class="sxs-lookup"><span data-stu-id="5d004-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="5d004-141">輸入下列命令並檢閱結果，以確認 OMS Agent 記錄檔中沒有任何錯誤︰</span><span class="sxs-lookup"><span data-stu-id="5d004-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="5d004-142">檢閱收集到的安全性事件</span><span class="sxs-lookup"><span data-stu-id="5d004-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="5d004-143">設定完成之後，OMS 安全性就會開始擷取安全性事件。</span><span class="sxs-lookup"><span data-stu-id="5d004-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="5d004-144">若要以視覺化方式檢視這些事件，請開啟記錄檔搜尋、在搜尋欄位中輸入命令 Type=CommonSecurityLog，然後按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="5d004-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="5d004-145">下列範例顯示此命令的結果，請您注意，在此案例中 OMS 安全性已從多家廠商擷取安全性記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="5d004-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![OMS 安全性和稽核基準評估](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="5d004-147">您可以針對單一廠商縮小此搜尋範圍，例如，以便以視覺化方式檢視線上 Cisco 記錄檔，輸入︰Type=CommonSecurityLog DeviceVendor=Cisco。</span><span class="sxs-lookup"><span data-stu-id="5d004-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="5d004-148">「CommonSecurityLog」已針對 CEF 頁首預先定義欄位，包括基本的擴充功能，其他任何擴充功能無論是不是「自訂擴充功能」，都會插入到「AdditionalExtensions」欄位。</span><span class="sxs-lookup"><span data-stu-id="5d004-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="5d004-149">您可以使用自訂欄位功能，以從中獲得專用欄位。</span><span class="sxs-lookup"><span data-stu-id="5d004-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="5d004-150">存取遺失基準評估的電腦</span><span class="sxs-lookup"><span data-stu-id="5d004-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="5d004-151">OMS 支援 Windows Server 2008 R2 至 Windows Server 2012 R2 的網域成員基準設定檔。</span><span class="sxs-lookup"><span data-stu-id="5d004-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="5d004-152">Windows Server 2016 基準尚未定案，將在發佈後盡快新增。</span><span class="sxs-lookup"><span data-stu-id="5d004-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="5d004-153">透過 OMS 安全性和稽核基準評估掃描的其他所有作業系統會顯示在 [遺失基準評估的電腦] 區段之下。</span><span class="sxs-lookup"><span data-stu-id="5d004-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="5d004-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5d004-154">See also</span></span>
<span data-ttu-id="5d004-155">在本文件中，您已了解如何將 CEF 解決方案連接至 OMS。</span><span class="sxs-lookup"><span data-stu-id="5d004-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="5d004-156">若要深入了解 OMS 安全性，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="5d004-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="5d004-157">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="5d004-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="5d004-158">在 Operations Management Suite 安全性和稽核內監視及回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="5d004-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="5d004-159">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="5d004-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

