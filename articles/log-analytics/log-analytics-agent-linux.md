---
title: "將 Linux 電腦連線至 Operations Management Suite (OMS) | Microsoft Docs"
description: "本文說明如何使用 OMS Agent for Linux，將在 Azure、其他雲端或內部部署中託管的 Linux 電腦連線至 OMS。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: 1c05f68235aafd0fa098a3b0edaba1258df09380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-linux-computers-to-operations-management-suite-oms"></a><span data-ttu-id="b01ba-103">將 Linux 電腦連線至 Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="b01ba-103">Connect your Linux Computers to Operations Management Suite (OMS)</span></span> 

<span data-ttu-id="b01ba-104">透過 Microsoft Operations Management Suite (OMS)，您可以收集從下列位置產生的資料，並對資料採取動作：從 Linux 電腦；存放在內部部署資料中心做為實體伺服器或虛擬機器的容器解決方案，如 Docker；如 Amazon Web Services (AWS) 或 Microsoft Azure 等雲端託管服務中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b01ba-104">With Microsoft Operations Management Suite (OMS), you can collect and act on data generated from Linux computers and container solutions like Docker, residing in your on-premises data center as physical servers or virtual machines, virtual machines in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure.</span></span> <span data-ttu-id="b01ba-105">您也可以使用 OMS 中可用的管理解決方案 (例如「變更追蹤」) 來識別組態變更，並使用「更新管理」管理軟體更新，以主動管理 Linux VM 的生命週期。</span><span class="sxs-lookup"><span data-stu-id="b01ba-105">You can also use management solutions available in OMS such as Change Tracking, to identify configuration changes, and Update Management to manage software updates to proactively manage the lifecycle of your Linux VMs.</span></span> 

<span data-ttu-id="b01ba-106">OMS Agent for Linux 會透過 TCP 通訊埠 443 對外與 OMS 服務通訊，如果電腦連線至防火牆或 Proxy 伺服器以透過網際網路通訊，請檢閱[設定代理程式以搭配 HTTP Proxy 伺服器或 OMS 閘道使用](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway)，以了解必須套用哪些組態變更。</span><span class="sxs-lookup"><span data-stu-id="b01ba-106">The OMS Agent for Linux communicates outbound with the OMS service over TCP port 443, and if the computer connects to a firewall or proxy server to communicate over the Internet, review [Configuring the agent for use with an HTTP proxy server or OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) to understand what configuration changes will need to be applied.</span></span>  <span data-ttu-id="b01ba-107">如果您正在監視的電腦已安裝 System Center 2016 - Operations Manager 或 Operations Manager 2012 R2，則該電腦為多重主目錄，並採用 OMS 服務來收集資料及轉寄至該服務，且仍然受到 Operations Manager 監視。</span><span class="sxs-lookup"><span data-stu-id="b01ba-107">If you are monitoring the computer with System Center 2016 - Operations Manager or Operations Manager 2012 R2, it can be multi-homed with the OMS service to collect data and forward to the service and still be monitored by Operations Manager.</span></span>  <span data-ttu-id="b01ba-108">Linux 電腦會由與 OMS 整合的 Operations Manager 管理群組所監視，其不會收到資料來源的組態，也不會透過該管理群組轉寄收集到的資料。</span><span class="sxs-lookup"><span data-stu-id="b01ba-108">Linux computers monitored by an Operations Manager management group that is integrated with OMS do not receive configuration for data sources and forward collected data through the management group.</span></span>  <span data-ttu-id="b01ba-109">OMS 代理程式無法設定為多個工作區的報表。</span><span class="sxs-lookup"><span data-stu-id="b01ba-109">The OMS agent cannot be configured to report to more than one workspace.</span></span>  

<span data-ttu-id="b01ba-110">如果 IT 安全性原則不允許您網路上的電腦連線到網際網路，則可以將代理程式設定為連線到 OMS 閘道，以根據您已啟用的解決方案來接收組態資訊和傳送收集到的資料。</span><span class="sxs-lookup"><span data-stu-id="b01ba-110">If your IT security policies do not allow computers on your network to connect to the Internet, the agent can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span> <span data-ttu-id="b01ba-111">如需如何設定 OMS Linux Agent 以透過 OMS 閘道與 OMS 服務進行通訊的詳細資訊和步驟，請參閱[使用 OMS 閘道將電腦連線到 OMS](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="b01ba-111">For more information and steps on how to configure your OMS Linux Agent to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

<span data-ttu-id="b01ba-112">下圖說明代理程式管理的 Linux 電腦與 OMS 之間的連線，包括方向與連接埠。</span><span class="sxs-lookup"><span data-stu-id="b01ba-112">The following diagram depicts the connection between the agent-managed Linux computers and OMS, including the direction and ports.</span></span>

![代理程式直接與 OMS 通訊的圖表](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a><span data-ttu-id="b01ba-114">系統需求</span><span class="sxs-lookup"><span data-stu-id="b01ba-114">System requirements</span></span>
<span data-ttu-id="b01ba-115">開始之前請檢閱下列詳細資料，以確認符合必要條件。</span><span class="sxs-lookup"><span data-stu-id="b01ba-115">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="supported-linux-operating-systems"></a><span data-ttu-id="b01ba-116">支援的 Linux 作業系統</span><span class="sxs-lookup"><span data-stu-id="b01ba-116">Supported Linux operating systems</span></span>
<span data-ttu-id="b01ba-117">以下為正式支援的 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="b01ba-117">The following Linux distributions are officially supported.</span></span>  <span data-ttu-id="b01ba-118">不過，OMS Agent for Linux 也可能在未列出的其他散發套件上執行。</span><span class="sxs-lookup"><span data-stu-id="b01ba-118">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="b01ba-119">Amazon Linux 2012.09 至 2015.09 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b01ba-119">Amazon Linux 2012.09 to 2015.09 (x86/x64)</span></span>
* <span data-ttu-id="b01ba-120">CentOS Linux 5、6 和 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b01ba-120">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="b01ba-121">Oracle Linux 5、6 和 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b01ba-121">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="b01ba-122">Red Hat Enterprise Linux Server 5、6 和 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b01ba-122">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
* <span data-ttu-id="b01ba-123">Debian GNU/Linux 6、7 和 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b01ba-123">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="b01ba-124">Ubuntu 12.04 LTS、14.04 LTS、15.04、15.10、16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b01ba-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="b01ba-125">SUSE Linux Enterprise Server 11 和 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b01ba-125">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

### <a name="network"></a><span data-ttu-id="b01ba-126">網路</span><span class="sxs-lookup"><span data-stu-id="b01ba-126">Network</span></span>
<span data-ttu-id="b01ba-127">下列資訊列出 Linux 代理程式與 OMS 通訊所需的 Proxy 和防火牆組態資訊。</span><span class="sxs-lookup"><span data-stu-id="b01ba-127">The information below list the proxy and firewall configuration information required for the Linux agent to communicate with OMS.</span></span> <span data-ttu-id="b01ba-128">流量會從您的網路輸出至 OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="b01ba-128">Traffic is outbound from your network to the OMS service.</span></span> 

|<span data-ttu-id="b01ba-129">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="b01ba-129">Agent Resource</span></span>| <span data-ttu-id="b01ba-130">連接埠</span><span class="sxs-lookup"><span data-stu-id="b01ba-130">Ports</span></span> |  
|------|---------|  
|<span data-ttu-id="b01ba-131">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="b01ba-131">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="b01ba-132">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-132">Port 443</span></span>|   
|<span data-ttu-id="b01ba-133">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="b01ba-133">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="b01ba-134">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-134">Port 443</span></span>|   
|<span data-ttu-id="b01ba-135">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="b01ba-135">*.blob.core.windows.net/</span></span> | <span data-ttu-id="b01ba-136">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-136">Port 443</span></span>|   
|<span data-ttu-id="b01ba-137">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="b01ba-137">*.azure-automation.net</span></span> | <span data-ttu-id="b01ba-138">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-138">Port 443</span></span>|  

### <a name="package-requirements"></a><span data-ttu-id="b01ba-139">封裝需求</span><span class="sxs-lookup"><span data-stu-id="b01ba-139">Package requirements</span></span>

 <span data-ttu-id="b01ba-140">**必要封裝**</span><span class="sxs-lookup"><span data-stu-id="b01ba-140">**Required package**</span></span>   | <span data-ttu-id="b01ba-141">**說明**</span><span class="sxs-lookup"><span data-stu-id="b01ba-141">**Description**</span></span>   | <span data-ttu-id="b01ba-142">**最低版本**</span><span class="sxs-lookup"><span data-stu-id="b01ba-142">**Minimum version**</span></span>
--------------------- | --------------------- | -------------------
<span data-ttu-id="b01ba-143">Glibc</span><span class="sxs-lookup"><span data-stu-id="b01ba-143">Glibc</span></span> | <span data-ttu-id="b01ba-144">GNU C 程式庫</span><span class="sxs-lookup"><span data-stu-id="b01ba-144">GNU C Library</span></span>   | <span data-ttu-id="b01ba-145">2.5-12</span><span class="sxs-lookup"><span data-stu-id="b01ba-145">2.5-12</span></span> 
<span data-ttu-id="b01ba-146">Openssl</span><span class="sxs-lookup"><span data-stu-id="b01ba-146">Openssl</span></span> | <span data-ttu-id="b01ba-147">OpenSSL 程式庫</span><span class="sxs-lookup"><span data-stu-id="b01ba-147">OpenSSL Libraries</span></span> | <span data-ttu-id="b01ba-148">0.9.8e 或 1.0</span><span class="sxs-lookup"><span data-stu-id="b01ba-148">0.9.8e or 1.0</span></span>
<span data-ttu-id="b01ba-149">Curl</span><span class="sxs-lookup"><span data-stu-id="b01ba-149">Curl</span></span> | <span data-ttu-id="b01ba-150">cURL Web 用戶端</span><span class="sxs-lookup"><span data-stu-id="b01ba-150">cURL web client</span></span> | <span data-ttu-id="b01ba-151">7.15.5</span><span class="sxs-lookup"><span data-stu-id="b01ba-151">7.15.5</span></span>
<span data-ttu-id="b01ba-152">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="b01ba-152">Python-ctypes</span></span> | | 
<span data-ttu-id="b01ba-153">PAM</span><span class="sxs-lookup"><span data-stu-id="b01ba-153">PAM</span></span> | <span data-ttu-id="b01ba-154">插入式驗證模組</span><span class="sxs-lookup"><span data-stu-id="b01ba-154">Pluggable authentication Modules</span></span> | 

> [!NOTE]
>  <span data-ttu-id="b01ba-155">需要有 rsyslog 或 syslog-ng，才能收集 syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="b01ba-155">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="b01ba-156">Red Hat Enterprise Linux 第 5 版、CentOS 和 Oracle Linux 版本 (sysklog) 不支援預設 syslog 精靈，進行 syslog 事件收集。</span><span class="sxs-lookup"><span data-stu-id="b01ba-156">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="b01ba-157">若要從此版的這些散發套件收集 syslog 資料，rsyslog 精靈應安裝和設定為取代 sysklog。</span><span class="sxs-lookup"><span data-stu-id="b01ba-157">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog,</span></span> 

<span data-ttu-id="b01ba-158">代理程式包含多個封裝。</span><span class="sxs-lookup"><span data-stu-id="b01ba-158">The agent includes multiple packages.</span></span> <span data-ttu-id="b01ba-159">發行檔案包含下列封裝 (搭配執行殼層套件組合與 `--extract` 即可取得)：</span><span class="sxs-lookup"><span data-stu-id="b01ba-159">The release file contains the following packages, available by running the shell bundle with `--extract`:</span></span>

<span data-ttu-id="b01ba-160">**Package**</span><span class="sxs-lookup"><span data-stu-id="b01ba-160">**Package**</span></span> | <span data-ttu-id="b01ba-161">**版本**</span><span class="sxs-lookup"><span data-stu-id="b01ba-161">**Version**</span></span> | <span data-ttu-id="b01ba-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="b01ba-162">**Description**</span></span>
----------- | ----------- | --------------
<span data-ttu-id="b01ba-163">omsagent</span><span class="sxs-lookup"><span data-stu-id="b01ba-163">omsagent</span></span> | <span data-ttu-id="b01ba-164">1.4.0</span><span class="sxs-lookup"><span data-stu-id="b01ba-164">1.4.0</span></span> | <span data-ttu-id="b01ba-165">Operations Management Suite Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="b01ba-165">The Operations Management Suite Agent for Linux</span></span>
<span data-ttu-id="b01ba-166">omsconfig</span><span class="sxs-lookup"><span data-stu-id="b01ba-166">omsconfig</span></span> | <span data-ttu-id="b01ba-167">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b01ba-167">1.1.1</span></span> | <span data-ttu-id="b01ba-168">OMS 代理程式的組態代理程式</span><span class="sxs-lookup"><span data-stu-id="b01ba-168">Configuration agent for the OMS Agent</span></span>
<span data-ttu-id="b01ba-169">omi</span><span class="sxs-lookup"><span data-stu-id="b01ba-169">omi</span></span> | <span data-ttu-id="b01ba-170">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b01ba-170">1.2.0</span></span> | <span data-ttu-id="b01ba-171">開放式管理基礎結構 (OMI) - 輕量型 CIM 伺服器</span><span class="sxs-lookup"><span data-stu-id="b01ba-171">Open Management Infrastructure (OMI) - a lightweight CIM Server</span></span>
<span data-ttu-id="b01ba-172">scx</span><span class="sxs-lookup"><span data-stu-id="b01ba-172">scx</span></span> | <span data-ttu-id="b01ba-173">1.6.3</span><span class="sxs-lookup"><span data-stu-id="b01ba-173">1.6.3</span></span> | <span data-ttu-id="b01ba-174">作業系統效能計量的 OMI CIM 提供者</span><span class="sxs-lookup"><span data-stu-id="b01ba-174">OMI CIM Providers for operating system performance metrics</span></span>
<span data-ttu-id="b01ba-175">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="b01ba-175">apache-cimprov</span></span> | <span data-ttu-id="b01ba-176">1.0.1</span><span class="sxs-lookup"><span data-stu-id="b01ba-176">1.0.1</span></span> | <span data-ttu-id="b01ba-177">OMI 的 Apache HTTP 伺服器效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="b01ba-177">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="b01ba-178">在偵測到 Apache HTTP 伺服器時安裝。</span><span class="sxs-lookup"><span data-stu-id="b01ba-178">Installed if Apache HTTP Server is detected.</span></span>
<span data-ttu-id="b01ba-179">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="b01ba-179">mysql-cimprov</span></span> | <span data-ttu-id="b01ba-180">1.0.1</span><span class="sxs-lookup"><span data-stu-id="b01ba-180">1.0.1</span></span> | <span data-ttu-id="b01ba-181">OMI 的 MySQL 伺服器效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="b01ba-181">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="b01ba-182">在偵測到 MySQL/MariaDB 伺服器時安裝。</span><span class="sxs-lookup"><span data-stu-id="b01ba-182">Installed if MySQL/MariaDB server is detected.</span></span>
<span data-ttu-id="b01ba-183">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="b01ba-183">docker-cimprov</span></span> | <span data-ttu-id="b01ba-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b01ba-184">1.0.0</span></span> | <span data-ttu-id="b01ba-185">OMI 的 Docker 提供者。</span><span class="sxs-lookup"><span data-stu-id="b01ba-185">Docker provider for OMI.</span></span> <span data-ttu-id="b01ba-186">在偵測到 Docker 時安裝。</span><span class="sxs-lookup"><span data-stu-id="b01ba-186">Installed if Docker is detected.</span></span>

### <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="b01ba-187">與 System Center Operations Manager 的相容性</span><span class="sxs-lookup"><span data-stu-id="b01ba-187">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="b01ba-188">OMS Agent for Linux 會與 System Center Operations Manager 代理程式共用代理程式二進位檔。</span><span class="sxs-lookup"><span data-stu-id="b01ba-188">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="b01ba-189">如果您要在 Operations Manager 目前所管理的系統上安裝 OMS Agent for Linux，將電腦上的 OMI 和 SCX 封裝升級到較新版本。</span><span class="sxs-lookup"><span data-stu-id="b01ba-189">If you install the OMS Agent for Linux on a system currently managed by Operations Manager, it the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="b01ba-190">在此版本中，OMS 與 Linux 適用的 System Center 2016 - Operations Manager/Operations Manager 2012 R2 代理程式相容。</span><span class="sxs-lookup"><span data-stu-id="b01ba-190">In this release, the OMS and System Center 2016 - Operations Manager/Operations Manager 2012 R2 agents for Linux are compatible.</span></span> 

> [!NOTE]
> <span data-ttu-id="b01ba-191">System Center 2012 SP1 和舊版本目前與 OMS Agent for Linux 不相容或不受其支援。</span><span class="sxs-lookup"><span data-stu-id="b01ba-191">System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.</span></span><br>
> <span data-ttu-id="b01ba-192">如果 OMS Agent for Linux 安裝到 Operations Manager 目前未監視的電腦，且您之後想要使用 Operations Manager 監視該電腦，您必須先修改 [OMI 組態](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager)，再探索電腦。</span><span class="sxs-lookup"><span data-stu-id="b01ba-192">If the OMS Agent for Linux is installed to a computer that is not currently monitored by Operations Manager, and you then wish to monitor the computer with Operations Manager, you must modify the [OMI configuration](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) prior to discovering the computer.</span></span> <span data-ttu-id="b01ba-193">**如果先安裝 Operations Manager 代理程式，再安裝 OMS Agent for Linux，則*不*需要這個步驟。**</span><span class="sxs-lookup"><span data-stu-id="b01ba-193">**This step is *not* needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>

### <a name="system-configuration-changes"></a><span data-ttu-id="b01ba-194">系統組態變更</span><span class="sxs-lookup"><span data-stu-id="b01ba-194">System configuration changes</span></span>
<span data-ttu-id="b01ba-195">安裝 OMS Agent for Linux 封裝之後，會套用下列額外的全系統組態變更。</span><span class="sxs-lookup"><span data-stu-id="b01ba-195">After installing the OMS Agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="b01ba-196">解除安裝 omsagent 封裝時，會移除這些構件。</span><span class="sxs-lookup"><span data-stu-id="b01ba-196">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="b01ba-197">會建立名為 `omsagent` 的非特殊權限使用者。</span><span class="sxs-lookup"><span data-stu-id="b01ba-197">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="b01ba-198">這是 omsagent 精靈所執行的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b01ba-198">This is the account the omsagent daemon runs as.</span></span>
* <span data-ttu-id="b01ba-199">sudoers “include” 檔案建立在 /etc/sudoers.d/omsagent。</span><span class="sxs-lookup"><span data-stu-id="b01ba-199">A sudoers “include” file is created at /etc/sudoers.d/omsagent.</span></span> <span data-ttu-id="b01ba-200">這會授權 omsagent 重新啟動 syslog 與 omsagent 精靈。</span><span class="sxs-lookup"><span data-stu-id="b01ba-200">This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="b01ba-201">如果已安裝的 sudo 版本不支援 sudo “include” 指示詞，這些項目會寫入 /etc/sudoers。</span><span class="sxs-lookup"><span data-stu-id="b01ba-201">If sudo “include” directives are not supported in the installed version of sudo, these entries are written to /etc/sudoers.</span></span>
* <span data-ttu-id="b01ba-202">syslog 組態修改成將事件子集轉送給代理程式。</span><span class="sxs-lookup"><span data-stu-id="b01ba-202">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="b01ba-203">如需詳細資訊，請參閱下面 **設定資料收集** 一節。</span><span class="sxs-lookup"><span data-stu-id="b01ba-203">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="upgrade-from-a-previous-release"></a><span data-ttu-id="b01ba-204">從舊版升級</span><span class="sxs-lookup"><span data-stu-id="b01ba-204">Upgrade from a previous release</span></span>
<span data-ttu-id="b01ba-205">此版本支援從 1.0.0-47 之前的版本升級。</span><span class="sxs-lookup"><span data-stu-id="b01ba-205">Upgrade from versions earlier than 1.0.0-47 is supported in this release.</span></span> <span data-ttu-id="b01ba-206">使用 `--upgrade` 命令執行安裝，會將代理程式的所有元件升級為最新版本。</span><span class="sxs-lookup"><span data-stu-id="b01ba-206">Performing the installation with the `--upgrade` command upgrades all components of the agent to the latest version.</span></span>

## <a name="installing-the-agent"></a><span data-ttu-id="b01ba-207">安裝代理程式</span><span class="sxs-lookup"><span data-stu-id="b01ba-207">Installing the agent</span></span>

<span data-ttu-id="b01ba-208">本節說明如何以套件組合安裝 OMS Agent for Linux，其中包含各代理程式元件的 Debian 與 RPM 封裝。</span><span class="sxs-lookup"><span data-stu-id="b01ba-208">This section describes how to install the OMS Agent for Linux using a bunndle, which contains Debian and RPM packages for each of the agent components.</span></span>  <span data-ttu-id="b01ba-209">代理程式可以直接安裝，或是經擷取將個別封裝取出。</span><span class="sxs-lookup"><span data-stu-id="b01ba-209">It can be installed directly or extracted to retrieve the individual packages.</span></span>  

<span data-ttu-id="b01ba-210">您首先需要您的 OMS 工作區識別碼和金鑰，這可以透過切換至 [OMS 傳統入口網站](https://mms.microsoft.com)找到。</span><span class="sxs-lookup"><span data-stu-id="b01ba-210">First you need your OMS workspace ID and key, which you can find by switching to the [OMS classic portal](https://mms.microsoft.com).</span></span>  <span data-ttu-id="b01ba-211">在 [概觀] 頁面上，從頂端功能表選取 [設定]，然後巡覽至 [連接的來源]\[Linux 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="b01ba-211">On the **Overview** page, from the top menu select **Settings**, and then navigate to **Connected Sources\Linux Servers**.</span></span>  <span data-ttu-id="b01ba-212">您會看到 [工作區識別碼] 和 [主索引鍵] 右邊的值。</span><span class="sxs-lookup"><span data-stu-id="b01ba-212">You see the value to the right of **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="b01ba-213">將兩者複製並貼到您最愛的編輯器。</span><span class="sxs-lookup"><span data-stu-id="b01ba-213">Copy and paste both into your favorite editor.</span></span>    

1. <span data-ttu-id="b01ba-214">在 GitHub 下載最新的 [OMS Ageent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) 或 [OMS Agent for Linux (x86)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh)。</span><span class="sxs-lookup"><span data-stu-id="b01ba-214">Download the latest [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) or [OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) from GitHub.</span></span>  
2. <span data-ttu-id="b01ba-215">使用 scp/sftp 將適當的套件組合 (x86 或 x64) 傳輸到 Linux 電腦。</span><span class="sxs-lookup"><span data-stu-id="b01ba-215">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span></span>
3. <span data-ttu-id="b01ba-216">使用 `--install` 或 `--upgrade` 引數安裝該套件組合。</span><span class="sxs-lookup"><span data-stu-id="b01ba-216">Install the bundle by using the `--install` or `--upgrade` argument.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="b01ba-217">若已安裝任何現有封裝，例如已安裝適用於 Linux 的 System Center Operations Manager 時，則使用 `--upgrade` 引數。</span><span class="sxs-lookup"><span data-stu-id="b01ba-217">If any existing packages are installed such as when the System Center Operations Manager agent for Linux is already installed, use the `--upgrade` argument.</span></span> <span data-ttu-id="b01ba-218">若要在安裝期間連線到 Operations Management Suite，請提供 `-w <WorkspaceID>` 和 `-s <Shared Key>` 參數。</span><span class="sxs-lookup"><span data-stu-id="b01ba-218">To connect to Operations Management Suite during installation, provide the `-w <WorkspaceID>` and `-s <Shared Key>` parameters.</span></span>


#### <a name="to-install-and-onboard-directly"></a><span data-ttu-id="b01ba-219">直接安裝並上架</span><span class="sxs-lookup"><span data-stu-id="b01ba-219">To install and onboard directly</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="to-upgrade-the-agent-package"></a><span data-ttu-id="b01ba-220">若要升級代理程式封裝</span><span class="sxs-lookup"><span data-stu-id="b01ba-220">To upgrade the agent package</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="to-install-and-onboard-to-a-workspace-in-us-government-cloud"></a><span data-ttu-id="b01ba-221">安裝並上架到美國政府雲端</span><span class="sxs-lookup"><span data-stu-id="b01ba-221">To install and onboard to a workspace in US Government Cloud</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a><span data-ttu-id="b01ba-222">設定代理程式搭配 HTTP Proxy 伺服器或 OMS 閘道使用</span><span class="sxs-lookup"><span data-stu-id="b01ba-222">Configuring the agent for use with an HTTP proxy server or OMS Gateway</span></span>
<span data-ttu-id="b01ba-223">適用於 Linux 的 OMS 代理程式支援透過 HTTP 或 HTTPS Proxy 伺服器或 OMS 閘道，與 OMS 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b01ba-223">The OMS Agent for Linux supports communicating either through an HTTP or HTTPS proxy server or OMS Gateway to the OMS service.</span></span>  <span data-ttu-id="b01ba-224">不支援匿名和基本驗證 (使用者名稱/密碼)。</span><span class="sxs-lookup"><span data-stu-id="b01ba-224">Both anonymous and basic authentication (username/password) is supported.</span></span>  

### <a name="proxy-configuration"></a><span data-ttu-id="b01ba-225">Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="b01ba-225">Proxy configuration</span></span>
<span data-ttu-id="b01ba-226">Proxy 組態值的語法如下︰</span><span class="sxs-lookup"><span data-stu-id="b01ba-226">The proxy configuration value has the following syntax:</span></span>

`[protocol://][user:password@]proxyhost[:port]`

<span data-ttu-id="b01ba-227">屬性</span><span class="sxs-lookup"><span data-stu-id="b01ba-227">Property</span></span>|<span data-ttu-id="b01ba-228">說明</span><span class="sxs-lookup"><span data-stu-id="b01ba-228">Description</span></span>
-|-
<span data-ttu-id="b01ba-229">通訊協定</span><span class="sxs-lookup"><span data-stu-id="b01ba-229">Protocol</span></span>|<span data-ttu-id="b01ba-230">http 或 https</span><span class="sxs-lookup"><span data-stu-id="b01ba-230">http or https</span></span>
<span data-ttu-id="b01ba-231">user</span><span class="sxs-lookup"><span data-stu-id="b01ba-231">user</span></span>|<span data-ttu-id="b01ba-232">用於驗證 Proxy 的選擇性使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b01ba-232">Optional username for proxy authentication</span></span>
<span data-ttu-id="b01ba-233">password</span><span class="sxs-lookup"><span data-stu-id="b01ba-233">password</span></span>|<span data-ttu-id="b01ba-234">用於驗證 Proxy 的選擇性密碼</span><span class="sxs-lookup"><span data-stu-id="b01ba-234">Optional password for proxy authentication</span></span>
<span data-ttu-id="b01ba-235">proxyhost</span><span class="sxs-lookup"><span data-stu-id="b01ba-235">proxyhost</span></span>|<span data-ttu-id="b01ba-236">Proxy 伺服器/OMS 閘道的位址或 FQDN</span><span class="sxs-lookup"><span data-stu-id="b01ba-236">Address or FQDN of the proxy server/OMS Gateway</span></span>
<span data-ttu-id="b01ba-237">port</span><span class="sxs-lookup"><span data-stu-id="b01ba-237">port</span></span>|<span data-ttu-id="b01ba-238">Proxy 伺服器/OMS 閘道的選擇性連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="b01ba-238">Optional port number for the proxy server/OMS Gateway</span></span>

<span data-ttu-id="b01ba-239">例如：`http://user01:password@proxy01.contoso.com:8080`</span><span class="sxs-lookup"><span data-stu-id="b01ba-239">For example: `http://user01:password@proxy01.contoso.com:8080`</span></span>

<span data-ttu-id="b01ba-240">可在安裝期間指定或在安裝後透過修改 proxy.conf 組態檔案指定的 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b01ba-240">The proxy server can be specified during installation or by modifying the proxy.conf configuration file after installation.</span></span>   

### <a name="specify-proxy-configuration-during-installation"></a><span data-ttu-id="b01ba-241">安裝期間指定 Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="b01ba-241">Specify proxy configuration during installation</span></span>
<span data-ttu-id="b01ba-242">omsagent 安裝套件組合的 `-p` 或 `--proxy` 引數可指定要使用的 Proxy 組態。</span><span class="sxs-lookup"><span data-stu-id="b01ba-242">The `-p` or `--proxy` argument for the omsagent installation bundle specifies the proxy configuration to use.</span></span> 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-the-proxy-configuration-in-a-file"></a><span data-ttu-id="b01ba-243">在檔案中定義 Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="b01ba-243">Define the proxy configuration in a file</span></span>
<span data-ttu-id="b01ba-244">可在檔案 `/etc/opt/microsoft/omsagent/proxy.conf` 和 `/etc/opt/microsoft/omsagent/conf/proxy.conf ` 中設定 Proxy 組態。</span><span class="sxs-lookup"><span data-stu-id="b01ba-244">The proxy configuration can be set in the files `/etc/opt/microsoft/omsagent/proxy.conf`  and `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span></span> <span data-ttu-id="b01ba-245">可以直接建立或編輯檔案，但必須更新其權限，才能對 omiuser 使用者授與檔案的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="b01ba-245">The files can be directly created or edited, but their permissions must be updated to grant the omiuser user read permission on the files.</span></span> <span data-ttu-id="b01ba-246">例如：</span><span class="sxs-lookup"><span data-stu-id="b01ba-246">For example:</span></span>
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-the-proxy-configuration"></a><span data-ttu-id="b01ba-247">移除 Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="b01ba-247">Removing the proxy configuration</span></span>
<span data-ttu-id="b01ba-248">若要移除先前定義的 Proxy 組態並還原至直接連線，請移除 proxy.conf 檔案：</span><span class="sxs-lookup"><span data-stu-id="b01ba-248">To remove a previously defined proxy configuration and revert to direct connectivity, remove the proxy.conf file:</span></span>
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a><span data-ttu-id="b01ba-249">透過 Operations Management Suite 上架</span><span class="sxs-lookup"><span data-stu-id="b01ba-249">Onboarding with Operations Management Suite</span></span>
<span data-ttu-id="b01ba-250">如果套件組合安裝期間未提供工作區識別碼與金鑰，則之後必須向 Operations Management Suite 註冊代理程式。</span><span class="sxs-lookup"><span data-stu-id="b01ba-250">If a workspace ID and key were not provided during the bundle installation, the agent must be subsequently registered with Operations Management Suite.</span></span>

### <a name="onboarding-using-the-command-line"></a><span data-ttu-id="b01ba-251">使用命令列上架</span><span class="sxs-lookup"><span data-stu-id="b01ba-251">Onboarding using the command line</span></span>
<span data-ttu-id="b01ba-252">透過提供您工作區的工作區識別碼與金鑰來執行 omsadmin.sh 命令。</span><span class="sxs-lookup"><span data-stu-id="b01ba-252">Run the omsadmin.sh command supplying the workspace id and key for your workspace.</span></span> <span data-ttu-id="b01ba-253">此命令必須以根身分 (具有 sudo 提升權限) 執行：</span><span class="sxs-lookup"><span data-stu-id="b01ba-253">This command must be run as root (with sudo elevation):</span></span>
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a><span data-ttu-id="b01ba-254">使用檔案上架</span><span class="sxs-lookup"><span data-stu-id="b01ba-254">Onboarding using a file</span></span>
1.  <span data-ttu-id="b01ba-255">建立檔案 `/etc/omsagent-onboard.conf`。</span><span class="sxs-lookup"><span data-stu-id="b01ba-255">Create the file `/etc/omsagent-onboard.conf`.</span></span> <span data-ttu-id="b01ba-256">此檔案必須可讓根使用者讀取與寫入。</span><span class="sxs-lookup"><span data-stu-id="b01ba-256">The file must be readable and writable for root.</span></span>
`sudo vi /etc/omsagent-onboard.conf`
2.  <span data-ttu-id="b01ba-257">在檔案中插入以下幾行，並以您的工作區識別碼與共用金鑰取代：</span><span class="sxs-lookup"><span data-stu-id="b01ba-257">Insert the following lines in the file with your Workspace ID and Shared Key:</span></span>

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  <span data-ttu-id="b01ba-258">執行下列命令以上架至 OMS：`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="b01ba-258">Run the following command to Onboard to OMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span></span>
4.  <span data-ttu-id="b01ba-259">此檔案會在成功上架時刪除。</span><span class="sxs-lookup"><span data-stu-id="b01ba-259">The file is deleted on successful onboarding.</span></span>

## <a name="enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager"></a><span data-ttu-id="b01ba-260">啟用 OMS Agent for Linux 以向 System Center Operations Manager 報告</span><span class="sxs-lookup"><span data-stu-id="b01ba-260">Enable the OMS Agent for Linux to report to System Center Operations Manager</span></span>
<span data-ttu-id="b01ba-261">執行下列步驟設定 OMS Agent for Linux 向 System Center Operations Manager 管理群組報告。</span><span class="sxs-lookup"><span data-stu-id="b01ba-261">Perform the following steps to configure the OMS Agent for Linux to report to a System Center Operations Manager management group.</span></span>  

1. <span data-ttu-id="b01ba-262">編輯 `/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="b01ba-262">Edit the file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="b01ba-263">確認開頭為 **httpsport=** 的行定義連接埠 1270。</span><span class="sxs-lookup"><span data-stu-id="b01ba-263">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="b01ba-264">例如：`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="b01ba-264">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="b01ba-265">重新啟動 OMI 伺服器：`sudo /opt/omi/bin/service_control restart`</span><span class="sxs-lookup"><span data-stu-id="b01ba-265">Restart the OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="agent-logs"></a><span data-ttu-id="b01ba-266">代理程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="b01ba-266">Agent logs</span></span>
<span data-ttu-id="b01ba-267">OMS Agent for Linux 的記錄檔位於：`/var/opt/microsoft/omsagent/<workspace id>/log/` omsconfig (代理程式組態) 程式的記錄檔位於：`/var/opt/microsoft/omsconfig/log/` OMI 與 SCX 元件 (可提供效能計量資料) 的記錄檔位於：`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span><span class="sxs-lookup"><span data-stu-id="b01ba-267">The logs for the OMS Agent for Linux can be found at: `/var/opt/microsoft/omsagent/<workspace id>/log/` The logs for the omsconfig (agent configuration) program can be found at: `/var/opt/microsoft/omsconfig/log/` Logs for the OMI and SCX components (which provide performance metrics data) can be found at: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span></span>

### <a name="log-rotation-configuration"></a><span data-ttu-id="b01ba-268">記錄輪替組態##</span><span class="sxs-lookup"><span data-stu-id="b01ba-268">Log rotation configuration##</span></span>
<span data-ttu-id="b01ba-269">omsagent 的記錄輪替組態位於：`/etc/logrotate.d/omsagent-<workspace id>`</span><span class="sxs-lookup"><span data-stu-id="b01ba-269">The log rotate configuration for omsagent can be found at: `/etc/logrotate.d/omsagent-<workspace id>`</span></span>

<span data-ttu-id="b01ba-270">預設設定值為：</span><span class="sxs-lookup"><span data-stu-id="b01ba-270">The default settings are:</span></span> 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-the-oms-agent-for-linux"></a><span data-ttu-id="b01ba-271">解除安裝 OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="b01ba-271">Uninstalling the OMS Agent for Linux</span></span>
<span data-ttu-id="b01ba-272">可以藉由使用 `--purge` 引數執行搭售的 .sh 檔案，以解除安裝代理程式封裝，將代理程式及其組態從電腦中完全移除。</span><span class="sxs-lookup"><span data-stu-id="b01ba-272">The agent packages can be uninstalled by running the bundle .sh file with the `--purge` argument, which completely removes the agent and its configuration from the computer.</span></span>   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a><span data-ttu-id="b01ba-273">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b01ba-273">Troubleshooting</span></span>

### <a name="issue-unable-to-connect-through-proxy-to-oms"></a><span data-ttu-id="b01ba-274">問題︰ 無法透過 Proxy 連線至 OMS</span><span class="sxs-lookup"><span data-stu-id="b01ba-274">Issue: Unable to connect through proxy to OMS</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="b01ba-275">可能的原因</span><span class="sxs-lookup"><span data-stu-id="b01ba-275">Probable causes</span></span>
* <span data-ttu-id="b01ba-276">上架期間指定的 Proxy 不正確</span><span class="sxs-lookup"><span data-stu-id="b01ba-276">The proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="b01ba-277">OMS 服務端點未列入您資料中心的允許清單</span><span class="sxs-lookup"><span data-stu-id="b01ba-277">The OMS Service Endpoints are not whitelistested in your datacenter</span></span> 

#### <a name="resolutions"></a><span data-ttu-id="b01ba-278">解決方式</span><span class="sxs-lookup"><span data-stu-id="b01ba-278">Resolutions</span></span>
1. <span data-ttu-id="b01ba-279">將下列命令搭配已啟用的 `-v` 選項使用，以透過 OMS Agent for Linux 重新上架至 OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="b01ba-279">Reonboard to the OMS Service with the OMS Agent for Linux by using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="b01ba-280">這可讓透過 Proxy 連接到 OMS 服務的代理程式產生詳細資訊輸出。</span><span class="sxs-lookup"><span data-stu-id="b01ba-280">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="b01ba-281">檢閱 [設定代理程式搭配 HTTP Proxy 伺服器(#configuring the-agent-for-use-with-a-http-proxy-server) 一節，以確認您已適當地設定代理程式透過 Proxy 伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="b01ba-281">Review the section [Configuring the agent for use with an HTTP proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) to verify you have properly configured the agent to communicate through a proxy server.</span></span>    
* <span data-ttu-id="b01ba-282">再次檢查以確認下列 OMS 服務端點已在允許清單中：</span><span class="sxs-lookup"><span data-stu-id="b01ba-282">Double check that the following OMS Service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="b01ba-283">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="b01ba-283">Agent Resource</span></span>| <span data-ttu-id="b01ba-284">連接埠</span><span class="sxs-lookup"><span data-stu-id="b01ba-284">Ports</span></span> |  
    |------|---------|  
    |<span data-ttu-id="b01ba-285">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="b01ba-285">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="b01ba-286">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-286">Port 443</span></span>|   
    |<span data-ttu-id="b01ba-287">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="b01ba-287">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="b01ba-288">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-288">Port 443</span></span>|   
    |<span data-ttu-id="b01ba-289">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="b01ba-289">ods.systemcenteradvisor.com</span></span> | <span data-ttu-id="b01ba-290">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-290">Port 443</span></span>|   
    |<span data-ttu-id="b01ba-291">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="b01ba-291">*.blob.core.windows.net/</span></span> | <span data-ttu-id="b01ba-292">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="b01ba-292">Port 443</span></span>|   

### <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a><span data-ttu-id="b01ba-293">問題：您在嘗試上架時收到 403 錯誤</span><span class="sxs-lookup"><span data-stu-id="b01ba-293">Issue: You receive a 403 error when trying to onboard</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="b01ba-294">可能的原因</span><span class="sxs-lookup"><span data-stu-id="b01ba-294">Probable causes</span></span>
* <span data-ttu-id="b01ba-295">Linux 伺服器上的日期與時間不正確</span><span class="sxs-lookup"><span data-stu-id="b01ba-295">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="b01ba-296">使用的工作區識別碼和工作區金鑰不正確</span><span class="sxs-lookup"><span data-stu-id="b01ba-296">Workspace ID and Workspace Key used are not correct</span></span>

#### <a name="resolution"></a><span data-ttu-id="b01ba-297">解決方案</span><span class="sxs-lookup"><span data-stu-id="b01ba-297">Resolution</span></span>

1. <span data-ttu-id="b01ba-298">使用命令日期檢查 Linux 伺服器上的時間。</span><span class="sxs-lookup"><span data-stu-id="b01ba-298">Check the time on your Linux server with the command date.</span></span> <span data-ttu-id="b01ba-299">如果時間為自目前時間起的 + /-15 分鐘，則上架失敗。</span><span class="sxs-lookup"><span data-stu-id="b01ba-299">If the time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="b01ba-300">若要修正此問題，請更新 Linux 伺服器的日期和/或時區。</span><span class="sxs-lookup"><span data-stu-id="b01ba-300">To correct this update the date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="b01ba-301">確認您已安裝最新版的 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="b01ba-301">Verify you have installed the latest version of the OMS Agent for Linux.</span></span>  <span data-ttu-id="b01ba-302">最新版本現在會通知您時間差異是否造成上架失敗。</span><span class="sxs-lookup"><span data-stu-id="b01ba-302">The newest version now notifies you if time skew is causing the onboarding failure.</span></span>
3. <span data-ttu-id="b01ba-303">使用正確的工作區識別碼和工作區金鑰並遵循本主題中前面的安裝指示重新上架。</span><span class="sxs-lookup"><span data-stu-id="b01ba-303">Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.</span></span>

### <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a><span data-ttu-id="b01ba-304">問題︰上架後您隨即在記錄檔中看到 500 與 404 錯誤</span><span class="sxs-lookup"><span data-stu-id="b01ba-304">Issue: You see a 500 and 404 error in the log file right after onboarding</span></span>
<span data-ttu-id="b01ba-305">這是已知第一次將 Linux 資料上傳至 OMS 工作區時會發生的問題。</span><span class="sxs-lookup"><span data-stu-id="b01ba-305">This is a known issue that occurs on first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="b01ba-306">這不會影響正在傳送的資料或服務體驗。</span><span class="sxs-lookup"><span data-stu-id="b01ba-306">This does not affect data being sent or service experience.</span></span>

### <a name="issue--you-are-not-seeing-any-data-in-the-oms-portal"></a><span data-ttu-id="b01ba-307">問題︰您在 OMS 入口網站中看不到任何資料</span><span class="sxs-lookup"><span data-stu-id="b01ba-307">Issue:  You are not seeing any data in the OMS portal</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="b01ba-308">可能的原因</span><span class="sxs-lookup"><span data-stu-id="b01ba-308">Probable causes</span></span>

- <span data-ttu-id="b01ba-309">上架至 OMS 服務失敗</span><span class="sxs-lookup"><span data-stu-id="b01ba-309">Onboarding to the OMS Service failed</span></span>
- <span data-ttu-id="b01ba-310">對 OMS 服務的連線遭到封鎖</span><span class="sxs-lookup"><span data-stu-id="b01ba-310">Connection to the OMS Service is blocked</span></span>
- <span data-ttu-id="b01ba-311">OMS Agent for Linux 資料已備份</span><span class="sxs-lookup"><span data-stu-id="b01ba-311">OMS Agent for Linux data is backed up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b01ba-312">解決方式</span><span class="sxs-lookup"><span data-stu-id="b01ba-312">Resolutions</span></span>
1. <span data-ttu-id="b01ba-313">確認 OMS 服務是否成功上架，做法是檢查下列檔案是否存在：`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span><span class="sxs-lookup"><span data-stu-id="b01ba-313">Check if onboarding the OMS Service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="b01ba-314">使用 `omsadmin.sh` 命令列指示重新上架</span><span class="sxs-lookup"><span data-stu-id="b01ba-314">Reonboard using the `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="b01ba-315">如果使用 Proxy，請參閱稍早所提供的 Proxy 解決步驟。</span><span class="sxs-lookup"><span data-stu-id="b01ba-315">If using a proxy, refer to the proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="b01ba-316">在某些情況下，當 OMS Agent for Linux 無法與 OMS 服務通訊時，系統會將整個緩衝區大小 (亦即 50 MB) 的資料加入佇列。</span><span class="sxs-lookup"><span data-stu-id="b01ba-316">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the agent is queued to the full buffer size, which is 50 MB.</span></span> <span data-ttu-id="b01ba-317">應該執行下列命令重新啟動 OMS Agent for Linux：`/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`。</span><span class="sxs-lookup"><span data-stu-id="b01ba-317">The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="b01ba-318">此問題已在代理程式 1.1.0-28 版和更新版本中修正。</span><span class="sxs-lookup"><span data-stu-id="b01ba-318">This issue is fixed in agent version 1.1.0-28 and later.</span></span>
> 