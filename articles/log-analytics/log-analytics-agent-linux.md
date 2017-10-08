---
title: "aaaConnect 您的 Linux 電腦 tooOperations Management Suite (OMS) |Microsoft 文件"
description: "本文說明如何 tooconnect Linux 電腦裝載於 Azure、 其他雲端或內部部署 tooOMS 使用 hello OMS Agent for Linux。"
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
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a><span data-ttu-id="3647f-103">連接您的 Linux 電腦 tooOperations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="3647f-103">Connect your Linux Computers tooOperations Management Suite (OMS)</span></span> 

<span data-ttu-id="3647f-104">透過 Microsoft Operations Management Suite (OMS)，您可以收集從下列位置產生的資料，並對資料採取動作：從 Linux 電腦；存放在內部部署資料中心做為實體伺服器或虛擬機器的容器解決方案，如 Docker；如 Amazon Web Services (AWS) 或 Microsoft Azure 等雲端託管服務中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3647f-104">With Microsoft Operations Management Suite (OMS), you can collect and act on data generated from Linux computers and container solutions like Docker, residing in your on-premises data center as physical servers or virtual machines, virtual machines in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure.</span></span> <span data-ttu-id="3647f-105">您也可以使用變更追蹤，tooidentify 組態變更，例如在 OMS 中可用的管理解決方案，並更新管理 toomanage 軟體更新 tooproactively 管理的 Linux Vm 的 hello 生命週期。</span><span class="sxs-lookup"><span data-stu-id="3647f-105">You can also use management solutions available in OMS such as Change Tracking, tooidentify configuration changes, and Update Management toomanage software updates tooproactively manage hello lifecycle of your Linux VMs.</span></span> 

<span data-ttu-id="3647f-106">hello OMS Agent for Linux 通訊會透過 TCP 連接埠 443，輸出以 hello OMS 服務，而且如果 hello 電腦透過 hello 網際網路，連線 tooa 防火牆或 proxy 伺服器 toocommunicate 檢閱[設定用於 HTTP proxy 的 hello 代理程式伺服器或閘道 OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand 何種設定變更必須套用 toobe。</span><span class="sxs-lookup"><span data-stu-id="3647f-106">hello OMS Agent for Linux communicates outbound with hello OMS service over TCP port 443, and if hello computer connects tooa firewall or proxy server toocommunicate over hello Internet, review [Configuring hello agent for use with an HTTP proxy server or OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand what configuration changes will need toobe applied.</span></span>  <span data-ttu-id="3647f-107">如果您要監視 hello 與 System Center 2016-Operations Manager 或 Operations Manager 2012 R2 的電腦可以是多重主目錄 hello OMS 服務 toocollect 資料與正向 toohello 服務並仍由 Operations Manager 監視。</span><span class="sxs-lookup"><span data-stu-id="3647f-107">If you are monitoring hello computer with System Center 2016 - Operations Manager or Operations Manager 2012 R2, it can be multi-homed with hello OMS service toocollect data and forward toohello service and still be monitored by Operations Manager.</span></span>  <span data-ttu-id="3647f-108">由整合與 OMS 的 Operations Manager 管理群組監視的 Linux 電腦不會收到資料來源的組態，並收集轉寄透過 hello 管理群組的資料。</span><span class="sxs-lookup"><span data-stu-id="3647f-108">Linux computers monitored by an Operations Manager management group that is integrated with OMS do not receive configuration for data sources and forward collected data through hello management group.</span></span>  <span data-ttu-id="3647f-109">hello OMS 代理程式不能設定的 tooreport toomore 比一個工作區。</span><span class="sxs-lookup"><span data-stu-id="3647f-109">hello OMS agent cannot be configured tooreport toomore than one workspace.</span></span>  

<span data-ttu-id="3647f-110">如果您的 IT 安全性原則不允許您的網路 tooconnect toohello 網際網路上的電腦，hello 代理程式可以設定的 tooconnect toohello OMS 閘道 tooreceive 組態資訊和傳送收集的資料，取決於您擁有 hello 解決方案啟用。</span><span class="sxs-lookup"><span data-stu-id="3647f-110">If your IT security policies do not allow computers on your network tooconnect toohello Internet, hello agent can be configured tooconnect toohello OMS Gateway tooreceive configuration information and send collected data depending on hello solution you have enabled.</span></span> <span data-ttu-id="3647f-111">如需詳細資訊以及有關如何 tooconfigure 您的 OMS Linux 代理程式 toocommunicate 透過 OMS 閘道 toohello OMS 服務，請參閱步驟[連接使用 hello OMS 閘道電腦 tooOMS](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="3647f-111">For more information and steps on how tooconfigure your OMS Linux Agent toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

<span data-ttu-id="3647f-112">hello 下列圖表描述 hello hello 代理程式管理的 Linux 電腦和 OMS，包括 hello 方向和連接埠之間的連線。</span><span class="sxs-lookup"><span data-stu-id="3647f-112">hello following diagram depicts hello connection between hello agent-managed Linux computers and OMS, including hello direction and ports.</span></span>

![代理程式直接與 OMS 通訊的圖表](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a><span data-ttu-id="3647f-114">系統需求</span><span class="sxs-lookup"><span data-stu-id="3647f-114">System requirements</span></span>
<span data-ttu-id="3647f-115">開始之前，請檢閱下列符合 hello 必要條件的詳細資料 tooverify hello。</span><span class="sxs-lookup"><span data-stu-id="3647f-115">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="supported-linux-operating-systems"></a><span data-ttu-id="3647f-116">支援的 Linux 作業系統</span><span class="sxs-lookup"><span data-stu-id="3647f-116">Supported Linux operating systems</span></span>
<span data-ttu-id="3647f-117">hello 下列 Linux 發佈都正式支援。</span><span class="sxs-lookup"><span data-stu-id="3647f-117">hello following Linux distributions are officially supported.</span></span>  <span data-ttu-id="3647f-118">不過，其他未列出的發佈也可能執行 OMS Agent for Linux hello。</span><span class="sxs-lookup"><span data-stu-id="3647f-118">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="3647f-119">Amazon Linux 2012.09 too2015.09 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3647f-119">Amazon Linux 2012.09 too2015.09 (x86/x64)</span></span>
* <span data-ttu-id="3647f-120">CentOS Linux 5、6 和 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3647f-120">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="3647f-121">Oracle Linux 5、6 和 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3647f-121">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="3647f-122">Red Hat Enterprise Linux Server 5、6 和 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3647f-122">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
* <span data-ttu-id="3647f-123">Debian GNU/Linux 6、7 和 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3647f-123">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="3647f-124">Ubuntu 12.04 LTS、14.04 LTS、15.04、15.10、16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3647f-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="3647f-125">SUSE Linux Enterprise Server 11 和 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3647f-125">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

### <a name="network"></a><span data-ttu-id="3647f-126">網路</span><span class="sxs-lookup"><span data-stu-id="3647f-126">Network</span></span>
<span data-ttu-id="3647f-127">hello 資訊底下清單 hello proxy 和防火牆設定資訊所需的 hello Linux 代理程式 toocommunicate 與 OMS。</span><span class="sxs-lookup"><span data-stu-id="3647f-127">hello information below list hello proxy and firewall configuration information required for hello Linux agent toocommunicate with OMS.</span></span> <span data-ttu-id="3647f-128">已從您的網路 toohello OMS 服務的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="3647f-128">Traffic is outbound from your network toohello OMS service.</span></span> 

|<span data-ttu-id="3647f-129">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="3647f-129">Agent Resource</span></span>| <span data-ttu-id="3647f-130">連接埠</span><span class="sxs-lookup"><span data-stu-id="3647f-130">Ports</span></span> |  
|------|---------|  
|<span data-ttu-id="3647f-131">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3647f-131">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="3647f-132">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-132">Port 443</span></span>|   
|<span data-ttu-id="3647f-133">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3647f-133">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="3647f-134">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-134">Port 443</span></span>|   
|<span data-ttu-id="3647f-135">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="3647f-135">*.blob.core.windows.net/</span></span> | <span data-ttu-id="3647f-136">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-136">Port 443</span></span>|   
|<span data-ttu-id="3647f-137">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="3647f-137">*.azure-automation.net</span></span> | <span data-ttu-id="3647f-138">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-138">Port 443</span></span>|  

### <a name="package-requirements"></a><span data-ttu-id="3647f-139">封裝需求</span><span class="sxs-lookup"><span data-stu-id="3647f-139">Package requirements</span></span>

 <span data-ttu-id="3647f-140">**必要封裝**</span><span class="sxs-lookup"><span data-stu-id="3647f-140">**Required package**</span></span>   | <span data-ttu-id="3647f-141">**說明**</span><span class="sxs-lookup"><span data-stu-id="3647f-141">**Description**</span></span>   | <span data-ttu-id="3647f-142">**最低版本**</span><span class="sxs-lookup"><span data-stu-id="3647f-142">**Minimum version**</span></span>
--------------------- | --------------------- | -------------------
<span data-ttu-id="3647f-143">Glibc</span><span class="sxs-lookup"><span data-stu-id="3647f-143">Glibc</span></span> | <span data-ttu-id="3647f-144">GNU C 程式庫</span><span class="sxs-lookup"><span data-stu-id="3647f-144">GNU C Library</span></span>   | <span data-ttu-id="3647f-145">2.5-12</span><span class="sxs-lookup"><span data-stu-id="3647f-145">2.5-12</span></span> 
<span data-ttu-id="3647f-146">Openssl</span><span class="sxs-lookup"><span data-stu-id="3647f-146">Openssl</span></span> | <span data-ttu-id="3647f-147">OpenSSL 程式庫</span><span class="sxs-lookup"><span data-stu-id="3647f-147">OpenSSL Libraries</span></span> | <span data-ttu-id="3647f-148">0.9.8e 或 1.0</span><span class="sxs-lookup"><span data-stu-id="3647f-148">0.9.8e or 1.0</span></span>
<span data-ttu-id="3647f-149">Curl</span><span class="sxs-lookup"><span data-stu-id="3647f-149">Curl</span></span> | <span data-ttu-id="3647f-150">cURL Web 用戶端</span><span class="sxs-lookup"><span data-stu-id="3647f-150">cURL web client</span></span> | <span data-ttu-id="3647f-151">7.15.5</span><span class="sxs-lookup"><span data-stu-id="3647f-151">7.15.5</span></span>
<span data-ttu-id="3647f-152">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="3647f-152">Python-ctypes</span></span> | | 
<span data-ttu-id="3647f-153">PAM</span><span class="sxs-lookup"><span data-stu-id="3647f-153">PAM</span></span> | <span data-ttu-id="3647f-154">插入式驗證模組</span><span class="sxs-lookup"><span data-stu-id="3647f-154">Pluggable authentication Modules</span></span> | 

> [!NOTE]
>  <span data-ttu-id="3647f-155">需要 rsyslog 或 syslog-ng 是必要的 toocollect syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="3647f-155">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="3647f-156">在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。</span><span class="sxs-lookup"><span data-stu-id="3647f-156">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="3647f-157">toocollect syslog 資料，從這一版的這些發佈，hello rsyslog 精靈應該安裝和設定 tooreplace sysklog</span><span class="sxs-lookup"><span data-stu-id="3647f-157">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog,</span></span> 

<span data-ttu-id="3647f-158">hello 代理程式包含多個封裝。</span><span class="sxs-lookup"><span data-stu-id="3647f-158">hello agent includes multiple packages.</span></span> <span data-ttu-id="3647f-159">hello 發行檔案包含下列套件，以執行 hello 殼層配套 hello `--extract`:</span><span class="sxs-lookup"><span data-stu-id="3647f-159">hello release file contains hello following packages, available by running hello shell bundle with `--extract`:</span></span>

<span data-ttu-id="3647f-160">**Package**</span><span class="sxs-lookup"><span data-stu-id="3647f-160">**Package**</span></span> | <span data-ttu-id="3647f-161">**版本**</span><span class="sxs-lookup"><span data-stu-id="3647f-161">**Version**</span></span> | <span data-ttu-id="3647f-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="3647f-162">**Description**</span></span>
----------- | ----------- | --------------
<span data-ttu-id="3647f-163">omsagent</span><span class="sxs-lookup"><span data-stu-id="3647f-163">omsagent</span></span> | <span data-ttu-id="3647f-164">1.4.0</span><span class="sxs-lookup"><span data-stu-id="3647f-164">1.4.0</span></span> | <span data-ttu-id="3647f-165">hello Operations Management Suite Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="3647f-165">hello Operations Management Suite Agent for Linux</span></span>
<span data-ttu-id="3647f-166">omsconfig</span><span class="sxs-lookup"><span data-stu-id="3647f-166">omsconfig</span></span> | <span data-ttu-id="3647f-167">1.1.1</span><span class="sxs-lookup"><span data-stu-id="3647f-167">1.1.1</span></span> | <span data-ttu-id="3647f-168">Hello OMS 代理程式的設定代理程式</span><span class="sxs-lookup"><span data-stu-id="3647f-168">Configuration agent for hello OMS Agent</span></span>
<span data-ttu-id="3647f-169">omi</span><span class="sxs-lookup"><span data-stu-id="3647f-169">omi</span></span> | <span data-ttu-id="3647f-170">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3647f-170">1.2.0</span></span> | <span data-ttu-id="3647f-171">開放式管理基礎結構 (OMI) - 輕量型 CIM 伺服器</span><span class="sxs-lookup"><span data-stu-id="3647f-171">Open Management Infrastructure (OMI) - a lightweight CIM Server</span></span>
<span data-ttu-id="3647f-172">scx</span><span class="sxs-lookup"><span data-stu-id="3647f-172">scx</span></span> | <span data-ttu-id="3647f-173">1.6.3</span><span class="sxs-lookup"><span data-stu-id="3647f-173">1.6.3</span></span> | <span data-ttu-id="3647f-174">作業系統效能計量的 OMI CIM 提供者</span><span class="sxs-lookup"><span data-stu-id="3647f-174">OMI CIM Providers for operating system performance metrics</span></span>
<span data-ttu-id="3647f-175">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="3647f-175">apache-cimprov</span></span> | <span data-ttu-id="3647f-176">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3647f-176">1.0.1</span></span> | <span data-ttu-id="3647f-177">OMI 的 Apache HTTP 伺服器效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="3647f-177">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="3647f-178">在偵測到 Apache HTTP 伺服器時安裝。</span><span class="sxs-lookup"><span data-stu-id="3647f-178">Installed if Apache HTTP Server is detected.</span></span>
<span data-ttu-id="3647f-179">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="3647f-179">mysql-cimprov</span></span> | <span data-ttu-id="3647f-180">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3647f-180">1.0.1</span></span> | <span data-ttu-id="3647f-181">OMI 的 MySQL 伺服器效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="3647f-181">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="3647f-182">在偵測到 MySQL/MariaDB 伺服器時安裝。</span><span class="sxs-lookup"><span data-stu-id="3647f-182">Installed if MySQL/MariaDB server is detected.</span></span>
<span data-ttu-id="3647f-183">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="3647f-183">docker-cimprov</span></span> | <span data-ttu-id="3647f-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3647f-184">1.0.0</span></span> | <span data-ttu-id="3647f-185">OMI 的 Docker 提供者。</span><span class="sxs-lookup"><span data-stu-id="3647f-185">Docker provider for OMI.</span></span> <span data-ttu-id="3647f-186">在偵測到 Docker 時安裝。</span><span class="sxs-lookup"><span data-stu-id="3647f-186">Installed if Docker is detected.</span></span>

### <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="3647f-187">與 System Center Operations Manager 的相容性</span><span class="sxs-lookup"><span data-stu-id="3647f-187">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="3647f-188">hello OMS Agent for Linux 與 hello System Center Operations Manager 代理程式共用代理程式二進位檔。</span><span class="sxs-lookup"><span data-stu-id="3647f-188">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="3647f-189">如果您安裝 hello OMS Agent for Linux 目前由 Operations Manager 管理的系統上，它會 hello hello 電腦 tooa 較新版本的 OMI 和 SCX 封裝。</span><span class="sxs-lookup"><span data-stu-id="3647f-189">If you install hello OMS Agent for Linux on a system currently managed by Operations Manager, it hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="3647f-190">這個版本、 hello OMS 與 System Center 2016-適用於 Linux 的 Operations Manager/Operations Manager 2012 R2 代理程式都相容。</span><span class="sxs-lookup"><span data-stu-id="3647f-190">In this release, hello OMS and System Center 2016 - Operations Manager/Operations Manager 2012 R2 agents for Linux are compatible.</span></span> 

> [!NOTE]
> <span data-ttu-id="3647f-191">System Center 2012 SP1 和較早版本。 目前不相容或支援以 hello OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="3647f-191">System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.</span></span><br>
> <span data-ttu-id="3647f-192">如果 hello OMS Agent for Linux 安裝的 tooa 目前不是由 Operations Manager 監視的電腦，然後想 toomonitor hello 電腦與 Operations Manager，您就必須修改 hello [OMI 設定](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager)先前toodiscovering hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="3647f-192">If hello OMS Agent for Linux is installed tooa computer that is not currently monitored by Operations Manager, and you then wish toomonitor hello computer with Operations Manager, you must modify hello [OMI configuration](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) prior toodiscovering hello computer.</span></span> <span data-ttu-id="3647f-193">**這是步驟*不*如果 hello Operations Manager 代理程式安裝之前 hello OMS Agent for Linux 需要。**</span><span class="sxs-lookup"><span data-stu-id="3647f-193">**This step is *not* needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>

### <a name="system-configuration-changes"></a><span data-ttu-id="3647f-194">系統組態變更</span><span class="sxs-lookup"><span data-stu-id="3647f-194">System configuration changes</span></span>
<span data-ttu-id="3647f-195">在安裝之後 hello OMS Agent for Linux 套件，hello 下列全系統設定變更會套用。</span><span class="sxs-lookup"><span data-stu-id="3647f-195">After installing hello OMS Agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="3647f-196">解除安裝 hello omsagent 套件時，會移除這些成品。</span><span class="sxs-lookup"><span data-stu-id="3647f-196">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="3647f-197">會建立名為 `omsagent` 的非特殊權限使用者。</span><span class="sxs-lookup"><span data-stu-id="3647f-197">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="3647f-198">這是 hello hello omsagent 精靈執行的帳戶做為。</span><span class="sxs-lookup"><span data-stu-id="3647f-198">This is hello account hello omsagent daemon runs as.</span></span>
* <span data-ttu-id="3647f-199">sudoers “include” 檔案建立在 /etc/sudoers.d/omsagent。</span><span class="sxs-lookup"><span data-stu-id="3647f-199">A sudoers “include” file is created at /etc/sudoers.d/omsagent.</span></span> <span data-ttu-id="3647f-200">這會授權 omsagent toorestart hello syslog 和 omsagent 精靈。</span><span class="sxs-lookup"><span data-stu-id="3647f-200">This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="3647f-201">如果 sudo 安裝 hello 版本不支援 sudo"include"指示詞，這些項目會寫入太/等/sudoers。</span><span class="sxs-lookup"><span data-stu-id="3647f-201">If sudo “include” directives are not supported in hello installed version of sudo, these entries are written too/etc/sudoers.</span></span>
* <span data-ttu-id="3647f-202">hello syslog 組態是修改的 tooforward 事件 toohello 代理程式的子集。</span><span class="sxs-lookup"><span data-stu-id="3647f-202">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="3647f-203">如需詳細資訊，請參閱 hello**設定資料收集**下一節</span><span class="sxs-lookup"><span data-stu-id="3647f-203">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="upgrade-from-a-previous-release"></a><span data-ttu-id="3647f-204">從舊版升級</span><span class="sxs-lookup"><span data-stu-id="3647f-204">Upgrade from a previous release</span></span>
<span data-ttu-id="3647f-205">此版本支援從 1.0.0-47 之前的版本升級。</span><span class="sxs-lookup"><span data-stu-id="3647f-205">Upgrade from versions earlier than 1.0.0-47 is supported in this release.</span></span> <span data-ttu-id="3647f-206">執行以 hello hello 安裝`--upgrade`命令升級 hello 代理程式 toohello 最新版本的所有元件。</span><span class="sxs-lookup"><span data-stu-id="3647f-206">Performing hello installation with hello `--upgrade` command upgrades all components of hello agent toohello latest version.</span></span>

## <a name="installing-hello-agent"></a><span data-ttu-id="3647f-207">Hello 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="3647f-207">Installing hello agent</span></span>

<span data-ttu-id="3647f-208">本章節描述如何 tooinstall hello OMS Agent for Linux 使用 bunndle，其中包含 Debian 和 RPM 封裝每一個 hello 代理程式元件。</span><span class="sxs-lookup"><span data-stu-id="3647f-208">This section describes how tooinstall hello OMS Agent for Linux using a bunndle, which contains Debian and RPM packages for each of hello agent components.</span></span>  <span data-ttu-id="3647f-209">它可以直接安裝，或擷取 tooretrieve hello 個別封裝。</span><span class="sxs-lookup"><span data-stu-id="3647f-209">It can be installed directly or extracted tooretrieve hello individual packages.</span></span>  

<span data-ttu-id="3647f-210">您首先需要您的 OMS 工作區識別碼和金鑰，您可以藉由切換 toohello 找到[OMS 傳統入口網站](https://mms.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="3647f-210">First you need your OMS workspace ID and key, which you can find by switching toohello [OMS classic portal](https://mms.microsoft.com).</span></span>  <span data-ttu-id="3647f-211">在 [hello**概觀**從 hello 上方功能表中選取] 頁面上，**設定**，然後瀏覽過**連接 Sources\Linux 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="3647f-211">On hello **Overview** page, from hello top menu select **Settings**, and then navigate too**Connected Sources\Linux Servers**.</span></span>  <span data-ttu-id="3647f-212">您會看到 hello 值 toohello 右邊的**工作區識別碼**和**主索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="3647f-212">You see hello value toohello right of **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="3647f-213">將兩者複製並貼到您最愛的編輯器。</span><span class="sxs-lookup"><span data-stu-id="3647f-213">Copy and paste both into your favorite editor.</span></span>    

1. <span data-ttu-id="3647f-214">最新版本下載 hello [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh)或[OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh)從 GitHub。</span><span class="sxs-lookup"><span data-stu-id="3647f-214">Download hello latest [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) or [OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) from GitHub.</span></span>  
2. <span data-ttu-id="3647f-215">傳送嗨適當的配套 （x86 或 x64） tooyour Linux 電腦使用 scp/sftp 來進行。</span><span class="sxs-lookup"><span data-stu-id="3647f-215">Transfer hello appropriate bundle (x86 or x64) tooyour Linux computer using scp/sftp.</span></span>
3. <span data-ttu-id="3647f-216">安裝 hello 組合使用 hello`--install`或`--upgrade`引數。</span><span class="sxs-lookup"><span data-stu-id="3647f-216">Install hello bundle by using hello `--install` or `--upgrade` argument.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3647f-217">例如，當已安裝適用於 Linux 的 hello System Center Operations Manager 代理程式安裝任何現有的封裝，如果使用 hello`--upgrade`引數。</span><span class="sxs-lookup"><span data-stu-id="3647f-217">If any existing packages are installed such as when hello System Center Operations Manager agent for Linux is already installed, use hello `--upgrade` argument.</span></span> <span data-ttu-id="3647f-218">在安裝期間，tooconnect tooOperations Management Suite 提供 hello`-w <WorkspaceID>`和`-s <Shared Key>`參數。</span><span class="sxs-lookup"><span data-stu-id="3647f-218">tooconnect tooOperations Management Suite during installation, provide hello `-w <WorkspaceID>` and `-s <Shared Key>` parameters.</span></span>


#### <a name="tooinstall-and-onboard-directly"></a><span data-ttu-id="3647f-219">tooinstall 並將產品上架直接</span><span class="sxs-lookup"><span data-stu-id="3647f-219">tooinstall and onboard directly</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a><span data-ttu-id="3647f-220">tooupgrade hello 代理程式套件</span><span class="sxs-lookup"><span data-stu-id="3647f-220">tooupgrade hello agent package</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a><span data-ttu-id="3647f-221">tooinstall 和美國政府雲端中的上架 tooa 工作區</span><span class="sxs-lookup"><span data-stu-id="3647f-221">tooinstall and onboard tooa workspace in US Government Cloud</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a><span data-ttu-id="3647f-222">設定 HTTP proxy 伺服器或 OMS 閘道使用的 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="3647f-222">Configuring hello agent for use with an HTTP proxy server or OMS Gateway</span></span>
<span data-ttu-id="3647f-223">hello OMS Agent for Linux 支援透過 HTTP 或 HTTPS 的 proxy 伺服器或閘道 OMS toohello OMS 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="3647f-223">hello OMS Agent for Linux supports communicating either through an HTTP or HTTPS proxy server or OMS Gateway toohello OMS service.</span></span>  <span data-ttu-id="3647f-224">不支援匿名和基本驗證 (使用者名稱/密碼)。</span><span class="sxs-lookup"><span data-stu-id="3647f-224">Both anonymous and basic authentication (username/password) is supported.</span></span>  

### <a name="proxy-configuration"></a><span data-ttu-id="3647f-225">Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="3647f-225">Proxy configuration</span></span>
<span data-ttu-id="3647f-226">hello proxy 組態值具有 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="3647f-226">hello proxy configuration value has hello following syntax:</span></span>

`[protocol://][user:password@]proxyhost[:port]`

<span data-ttu-id="3647f-227">屬性</span><span class="sxs-lookup"><span data-stu-id="3647f-227">Property</span></span>|<span data-ttu-id="3647f-228">說明</span><span class="sxs-lookup"><span data-stu-id="3647f-228">Description</span></span>
-|-
<span data-ttu-id="3647f-229">通訊協定</span><span class="sxs-lookup"><span data-stu-id="3647f-229">Protocol</span></span>|<span data-ttu-id="3647f-230">http 或 https</span><span class="sxs-lookup"><span data-stu-id="3647f-230">http or https</span></span>
<span data-ttu-id="3647f-231">user</span><span class="sxs-lookup"><span data-stu-id="3647f-231">user</span></span>|<span data-ttu-id="3647f-232">用於驗證 Proxy 的選擇性使用者名稱</span><span class="sxs-lookup"><span data-stu-id="3647f-232">Optional username for proxy authentication</span></span>
<span data-ttu-id="3647f-233">password</span><span class="sxs-lookup"><span data-stu-id="3647f-233">password</span></span>|<span data-ttu-id="3647f-234">用於驗證 Proxy 的選擇性密碼</span><span class="sxs-lookup"><span data-stu-id="3647f-234">Optional password for proxy authentication</span></span>
<span data-ttu-id="3647f-235">proxyhost</span><span class="sxs-lookup"><span data-stu-id="3647f-235">proxyhost</span></span>|<span data-ttu-id="3647f-236">Hello proxy 伺服器/OMS 閘道的位址或者 FQDN</span><span class="sxs-lookup"><span data-stu-id="3647f-236">Address or FQDN of hello proxy server/OMS Gateway</span></span>
<span data-ttu-id="3647f-237">連接埠</span><span class="sxs-lookup"><span data-stu-id="3647f-237">port</span></span>|<span data-ttu-id="3647f-238">選擇性的連接埠號碼為 hello proxy 伺服器/OMS 閘道</span><span class="sxs-lookup"><span data-stu-id="3647f-238">Optional port number for hello proxy server/OMS Gateway</span></span>

<span data-ttu-id="3647f-239">例如：`http://user01:password@proxy01.contoso.com:8080`</span><span class="sxs-lookup"><span data-stu-id="3647f-239">For example: `http://user01:password@proxy01.contoso.com:8080`</span></span>

<span data-ttu-id="3647f-240">在安裝期間或安裝後修改 hello proxy.conf 組態檔，可以指定 hello proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3647f-240">hello proxy server can be specified during installation or by modifying hello proxy.conf configuration file after installation.</span></span>   

### <a name="specify-proxy-configuration-during-installation"></a><span data-ttu-id="3647f-241">安裝期間指定 Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="3647f-241">Specify proxy configuration during installation</span></span>
<span data-ttu-id="3647f-242">hello`-p`或`--proxy`hello omsagent 安裝配套的引數指定 hello proxy 組態 toouse。</span><span class="sxs-lookup"><span data-stu-id="3647f-242">hello `-p` or `--proxy` argument for hello omsagent installation bundle specifies hello proxy configuration toouse.</span></span> 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a><span data-ttu-id="3647f-243">在檔案中定義 hello proxy 設定</span><span class="sxs-lookup"><span data-stu-id="3647f-243">Define hello proxy configuration in a file</span></span>
<span data-ttu-id="3647f-244">hello proxy 組態可以設定在 hello 檔案`/etc/opt/microsoft/omsagent/proxy.conf`和`/etc/opt/microsoft/omsagent/conf/proxy.conf `。</span><span class="sxs-lookup"><span data-stu-id="3647f-244">hello proxy configuration can be set in hello files `/etc/opt/microsoft/omsagent/proxy.conf`  and `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span></span> <span data-ttu-id="3647f-245">hello 檔案可以直接建立或編輯，但其權限必須是更新的 toogrant hello omiuser 使用者 hello 檔案讀取權限。</span><span class="sxs-lookup"><span data-stu-id="3647f-245">hello files can be directly created or edited, but their permissions must be updated toogrant hello omiuser user read permission on hello files.</span></span> <span data-ttu-id="3647f-246">例如：</span><span class="sxs-lookup"><span data-stu-id="3647f-246">For example:</span></span>
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a><span data-ttu-id="3647f-247">正在移除 hello proxy 設定</span><span class="sxs-lookup"><span data-stu-id="3647f-247">Removing hello proxy configuration</span></span>
<span data-ttu-id="3647f-248">tooremove 先前定義的 proxy 設定並還原 toodirect 連線之後，移除 hello proxy.conf 檔案：</span><span class="sxs-lookup"><span data-stu-id="3647f-248">tooremove a previously defined proxy configuration and revert toodirect connectivity, remove hello proxy.conf file:</span></span>
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a><span data-ttu-id="3647f-249">透過 Operations Management Suite 上架</span><span class="sxs-lookup"><span data-stu-id="3647f-249">Onboarding with Operations Management Suite</span></span>
<span data-ttu-id="3647f-250">如果 hello 配套安裝期間未提供工作區識別碼和金鑰，hello 代理程式必須接著向 Operations Management Suite。</span><span class="sxs-lookup"><span data-stu-id="3647f-250">If a workspace ID and key were not provided during hello bundle installation, hello agent must be subsequently registered with Operations Management Suite.</span></span>

### <a name="onboarding-using-hello-command-line"></a><span data-ttu-id="3647f-251">使用 hello 命令列的上架</span><span class="sxs-lookup"><span data-stu-id="3647f-251">Onboarding using hello command line</span></span>
<span data-ttu-id="3647f-252">執行提供 hello 工作區識別碼 hello omsadmin.sh 命令，並為您工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="3647f-252">Run hello omsadmin.sh command supplying hello workspace id and key for your workspace.</span></span> <span data-ttu-id="3647f-253">此命令必須以根身分 (具有 sudo 提升權限) 執行：</span><span class="sxs-lookup"><span data-stu-id="3647f-253">This command must be run as root (with sudo elevation):</span></span>
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a><span data-ttu-id="3647f-254">使用檔案上架</span><span class="sxs-lookup"><span data-stu-id="3647f-254">Onboarding using a file</span></span>
1.  <span data-ttu-id="3647f-255">建立 hello 檔案`/etc/omsagent-onboard.conf`。</span><span class="sxs-lookup"><span data-stu-id="3647f-255">Create hello file `/etc/omsagent-onboard.conf`.</span></span> <span data-ttu-id="3647f-256">hello 檔案必須是可讀取和寫入的根。</span><span class="sxs-lookup"><span data-stu-id="3647f-256">hello file must be readable and writable for root.</span></span>
`sudo vi /etc/omsagent-onboard.conf`
2.  <span data-ttu-id="3647f-257">插入下列行 hello 與工作區識別碼和共用金鑰的檔案中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3647f-257">Insert hello following lines in hello file with your Workspace ID and Shared Key:</span></span>

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  <span data-ttu-id="3647f-258">執行下列命令 tooOnboard tooOMS hello:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="3647f-258">Run hello following command tooOnboard tooOMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span></span>
4.  <span data-ttu-id="3647f-259">在順利上架上刪除 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="3647f-259">hello file is deleted on successful onboarding.</span></span>

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a><span data-ttu-id="3647f-260">啟用 hello OMS Agent for Linux tooreport tooSystem Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3647f-260">Enable hello OMS Agent for Linux tooreport tooSystem Center Operations Manager</span></span>
<span data-ttu-id="3647f-261">執行下列步驟 tooconfigure hello OMS Agent for Linux tooreport tooa System Center Operations Manager 管理群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="3647f-261">Perform hello following steps tooconfigure hello OMS Agent for Linux tooreport tooa System Center Operations Manager management group.</span></span>  

1. <span data-ttu-id="3647f-262">編輯 hello 檔案`/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="3647f-262">Edit hello file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="3647f-263">請確定該 hello 行首**httpsport =**定義 hello 連接埠 1270年。</span><span class="sxs-lookup"><span data-stu-id="3647f-263">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="3647f-264">例如：`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="3647f-264">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="3647f-265">重新啟動 hello OMI 伺服器：`sudo /opt/omi/bin/service_control restart`</span><span class="sxs-lookup"><span data-stu-id="3647f-265">Restart hello OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="agent-logs"></a><span data-ttu-id="3647f-266">代理程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="3647f-266">Agent logs</span></span>
<span data-ttu-id="3647f-267">hello 記錄檔的 hello OMS Agent for Linux，請參閱： `/var/opt/microsoft/omsagent/<workspace id>/log/` hello omsconfig （代理程式組態） 程式可以找到在 hello 記錄檔： `/var/opt/microsoft/omsconfig/log/` hello OMI 和 SCX 元件 （提供效能標準資料） 的記錄檔，請參閱：`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span><span class="sxs-lookup"><span data-stu-id="3647f-267">hello logs for hello OMS Agent for Linux can be found at: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello logs for hello omsconfig (agent configuration) program can be found at: `/var/opt/microsoft/omsconfig/log/` Logs for hello OMI and SCX components (which provide performance metrics data) can be found at: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span></span>

### <a name="log-rotation-configuration"></a><span data-ttu-id="3647f-268">記錄輪替組態##</span><span class="sxs-lookup"><span data-stu-id="3647f-268">Log rotation configuration##</span></span>
<span data-ttu-id="3647f-269">omsagent 的 hello 記錄旋轉組態，請參閱：`/etc/logrotate.d/omsagent-<workspace id>`</span><span class="sxs-lookup"><span data-stu-id="3647f-269">hello log rotate configuration for omsagent can be found at: `/etc/logrotate.d/omsagent-<workspace id>`</span></span>

<span data-ttu-id="3647f-270">hello 預設設定是：</span><span class="sxs-lookup"><span data-stu-id="3647f-270">hello default settings are:</span></span> 
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

## <a name="uninstalling-hello-oms-agent-for-linux"></a><span data-ttu-id="3647f-271">解除安裝 hello OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="3647f-271">Uninstalling hello OMS Agent for Linux</span></span>
<span data-ttu-id="3647f-272">hello 代理程式套件可以解除安裝執行 hello 配套.sh 檔案與 hello`--purge`引數，這完全從 hello 電腦中移除 hello 代理程式和其組態。</span><span class="sxs-lookup"><span data-stu-id="3647f-272">hello agent packages can be uninstalled by running hello bundle .sh file with hello `--purge` argument, which completely removes hello agent and its configuration from hello computer.</span></span>   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a><span data-ttu-id="3647f-273">疑難排解</span><span class="sxs-lookup"><span data-stu-id="3647f-273">Troubleshooting</span></span>

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a><span data-ttu-id="3647f-274">問題： 無法 tooconnect 透過 proxy tooOMS</span><span class="sxs-lookup"><span data-stu-id="3647f-274">Issue: Unable tooconnect through proxy tooOMS</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="3647f-275">可能的原因</span><span class="sxs-lookup"><span data-stu-id="3647f-275">Probable causes</span></span>
* <span data-ttu-id="3647f-276">hello proxy 登入期間指定不正確</span><span class="sxs-lookup"><span data-stu-id="3647f-276">hello proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="3647f-277">hello OMS 服務端點不是在您的資料中心 whitelistested</span><span class="sxs-lookup"><span data-stu-id="3647f-277">hello OMS Service Endpoints are not whitelistested in your datacenter</span></span> 

#### <a name="resolutions"></a><span data-ttu-id="3647f-278">解決方式</span><span class="sxs-lookup"><span data-stu-id="3647f-278">Resolutions</span></span>
1. <span data-ttu-id="3647f-279">Reonboard toohello OMS 服務以使用下列命令以 hello 選項 hello hello OMS Agent for Linux`-v`啟用。</span><span class="sxs-lookup"><span data-stu-id="3647f-279">Reonboard toohello OMS Service with hello OMS Agent for Linux by using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="3647f-280">這可讓透過 hello proxy toohello OMS 服務的 hello 代理程式的詳細資訊輸出。</span><span class="sxs-lookup"><span data-stu-id="3647f-280">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="3647f-281">檢閱 hello 區段 [設定用於 HTTP proxy 的 hello 代理程式 server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify 您正確設定 hello 代理程式 toocommunicate 透過 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3647f-281">Review hello section [Configuring hello agent for use with an HTTP proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify you have properly configured hello agent toocommunicate through a proxy server.</span></span>    
* <span data-ttu-id="3647f-282">再次確認 hello 下列 OMS 服務端點會在允許清單中：</span><span class="sxs-lookup"><span data-stu-id="3647f-282">Double check that hello following OMS Service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="3647f-283">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="3647f-283">Agent Resource</span></span>| <span data-ttu-id="3647f-284">連接埠</span><span class="sxs-lookup"><span data-stu-id="3647f-284">Ports</span></span> |  
    |------|---------|  
    |<span data-ttu-id="3647f-285">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3647f-285">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="3647f-286">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-286">Port 443</span></span>|   
    |<span data-ttu-id="3647f-287">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3647f-287">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="3647f-288">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-288">Port 443</span></span>|   
    |<span data-ttu-id="3647f-289">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="3647f-289">ods.systemcenteradvisor.com</span></span> | <span data-ttu-id="3647f-290">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-290">Port 443</span></span>|   
    |<span data-ttu-id="3647f-291">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="3647f-291">*.blob.core.windows.net/</span></span> | <span data-ttu-id="3647f-292">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="3647f-292">Port 443</span></span>|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a><span data-ttu-id="3647f-293">問題： 您收到 403 錯誤時嘗試 tooonboard</span><span class="sxs-lookup"><span data-stu-id="3647f-293">Issue: You receive a 403 error when trying tooonboard</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="3647f-294">可能的原因</span><span class="sxs-lookup"><span data-stu-id="3647f-294">Probable causes</span></span>
* <span data-ttu-id="3647f-295">Linux 伺服器上的日期與時間不正確</span><span class="sxs-lookup"><span data-stu-id="3647f-295">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="3647f-296">使用的工作區識別碼和工作區金鑰不正確</span><span class="sxs-lookup"><span data-stu-id="3647f-296">Workspace ID and Workspace Key used are not correct</span></span>

#### <a name="resolution"></a><span data-ttu-id="3647f-297">解決方案</span><span class="sxs-lookup"><span data-stu-id="3647f-297">Resolution</span></span>

1. <span data-ttu-id="3647f-298">請檢查 hello Linux 伺服器 hello 命令日期與時間。</span><span class="sxs-lookup"><span data-stu-id="3647f-298">Check hello time on your Linux server with hello command date.</span></span> <span data-ttu-id="3647f-299">如果 hello 時間 + /-15 分鐘，從目前的時間，就會失敗登入。</span><span class="sxs-lookup"><span data-stu-id="3647f-299">If hello time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="3647f-300">toocorrect 此更新 hello 日期及/或 Linux 伺服器的時區。</span><span class="sxs-lookup"><span data-stu-id="3647f-300">toocorrect this update hello date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="3647f-301">請確認您已經安裝 hello 最新版 hello OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="3647f-301">Verify you have installed hello latest version of hello OMS Agent for Linux.</span></span>  <span data-ttu-id="3647f-302">hello 最新版本現在會通知您如果時間誤差導致 hello 登入失敗。</span><span class="sxs-lookup"><span data-stu-id="3647f-302">hello newest version now notifies you if time skew is causing hello onboarding failure.</span></span>
3. <span data-ttu-id="3647f-303">Reonboard 使用正確的工作區識別碼和工作區金鑰 hello 稍早在本主題中的安裝指示。</span><span class="sxs-lookup"><span data-stu-id="3647f-303">Reonboard using correct Workspace ID and Workspace Key following hello installation instructions earlier in this topic.</span></span>

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a><span data-ttu-id="3647f-304">問題： 您看到 500 和 404 錯誤 hello 記錄檔中的登入之後，權限</span><span class="sxs-lookup"><span data-stu-id="3647f-304">Issue: You see a 500 and 404 error in hello log file right after onboarding</span></span>
<span data-ttu-id="3647f-305">這是已知第一次將 Linux 資料上傳至 OMS 工作區時會發生的問題。</span><span class="sxs-lookup"><span data-stu-id="3647f-305">This is a known issue that occurs on first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="3647f-306">這不會影響正在傳送的資料或服務體驗。</span><span class="sxs-lookup"><span data-stu-id="3647f-306">This does not affect data being sent or service experience.</span></span>

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a><span data-ttu-id="3647f-307">問題： 您未看見 hello OMS 入口網站中的任何資料</span><span class="sxs-lookup"><span data-stu-id="3647f-307">Issue:  You are not seeing any data in hello OMS portal</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="3647f-308">可能的原因</span><span class="sxs-lookup"><span data-stu-id="3647f-308">Probable causes</span></span>

- <span data-ttu-id="3647f-309">上架 toohello OMS 服務失敗</span><span class="sxs-lookup"><span data-stu-id="3647f-309">Onboarding toohello OMS Service failed</span></span>
- <span data-ttu-id="3647f-310">OMS 服務會封鎖連接 toohello</span><span class="sxs-lookup"><span data-stu-id="3647f-310">Connection toohello OMS Service is blocked</span></span>
- <span data-ttu-id="3647f-311">OMS Agent for Linux 資料已備份</span><span class="sxs-lookup"><span data-stu-id="3647f-311">OMS Agent for Linux data is backed up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3647f-312">解決方式</span><span class="sxs-lookup"><span data-stu-id="3647f-312">Resolutions</span></span>
1. <span data-ttu-id="3647f-313">檢查上架 hello OMS 服務是否成功藉由檢查有 hello 下列檔案：`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span><span class="sxs-lookup"><span data-stu-id="3647f-313">Check if onboarding hello OMS Service was successful by checking if hello following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="3647f-314">使用 hello Reonboard`omsadmin.sh`命令列指示</span><span class="sxs-lookup"><span data-stu-id="3647f-314">Reonboard using hello `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="3647f-315">如果使用 proxy，請參閱稍早提供的 toohello proxy 解決步驟。</span><span class="sxs-lookup"><span data-stu-id="3647f-315">If using a proxy, refer toohello proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="3647f-316">在某些情況下，hello 適用於 Linux 的 OMS 代理程式無法與 hello OMS 服務通訊時 hello 代理程式上的資料會是 toohello 佇列已滿的緩衝區大小為 50 MB。</span><span class="sxs-lookup"><span data-stu-id="3647f-316">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello agent is queued toohello full buffer size, which is 50 MB.</span></span> <span data-ttu-id="3647f-317">藉由執行下列命令的 hello hello OMS Agent for Linux 應該重新啟動： `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`。</span><span class="sxs-lookup"><span data-stu-id="3647f-317">hello OMS Agent for Linux should be restarted by running hello following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="3647f-318">此問題已在代理程式 1.1.0-28 版和更新版本中修正。</span><span class="sxs-lookup"><span data-stu-id="3647f-318">This issue is fixed in agent version 1.1.0-28 and later.</span></span>
> 