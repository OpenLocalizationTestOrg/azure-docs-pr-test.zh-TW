---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="83ae6-101">連接您的 Linux 電腦 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="83ae6-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="83ae6-102">使用 Log Analytics，您可以收集和處理從 Linux 電腦所產生的資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="83ae6-103">加入從 Linux tooOMS 收集的資料可讓您 toomanage Linux 系統和像使用 Docker，容器解決方案，無論您的電腦位於何處，任何地點。</span><span class="sxs-lookup"><span data-stu-id="83ae6-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="83ae6-104">資料來源可能位於您的內部部署資料中心，作為實體伺服器，例如 Amazon Web Services (AWS) 或 Microsoft Azure 雲端託管服務中的虛擬電腦，或甚至 hello 您桌上的膝上型電腦。</span><span class="sxs-lookup"><span data-stu-id="83ae6-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="83ae6-105">此外，OMS 同樣也會收集來自 Windows 電腦的資料，因此支援真正混合式 IT 環境。</span><span class="sxs-lookup"><span data-stu-id="83ae6-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="83ae6-106">您可以使用單一管理入口網站，來檢視和管理來自具有 OMS 中 Log Analytics 之所有來源的資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="83ae6-107">這會減少 hello 需要 toomonitor 使用許多不同的系統，可讓您輕鬆 tooconsume，因此，您可以匯出您喜歡 toowhatever 商務分析解決方案或系統已經有任何資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="83ae6-108">本文是快速入門指南可協助您收集和管理 Linux 電腦使用 hello OMS Agent for Linux 的資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="83ae6-109">如需其他技術詳細資訊 (例如 Proxy 伺服器組態、CollectD 計量相關資訊，以及自訂 JSON 資料來源)，您可在 GitHub 上的 [OMS Agent for Linux 概觀 (英文)](https://github.com/Microsoft/OMS-Agent-for-Linux) 和 [OMS Agent for Linux 完整文件 (英文)](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) 中找到該資訊。</span><span class="sxs-lookup"><span data-stu-id="83ae6-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="83ae6-110">目前，您可以收集下列類型的資料從 Linux 電腦的 hello:</span><span class="sxs-lookup"><span data-stu-id="83ae6-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="83ae6-111">效能度量</span><span class="sxs-lookup"><span data-stu-id="83ae6-111">Performance metrics</span></span>
* <span data-ttu-id="83ae6-112">Syslog 事件</span><span class="sxs-lookup"><span data-stu-id="83ae6-112">Syslog events</span></span>
* <span data-ttu-id="83ae6-113">來自 Nagios 和 Zabbix 的警示</span><span class="sxs-lookup"><span data-stu-id="83ae6-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="83ae6-114">Docker 容器效能計量、清查和記錄檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="83ae6-115">支援的 Linux 版本</span><span class="sxs-lookup"><span data-stu-id="83ae6-115">Supported Linux versions</span></span>
<span data-ttu-id="83ae6-116">各種 Linux 散發套件正式支援 x86 和 x64 版本。</span><span class="sxs-lookup"><span data-stu-id="83ae6-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="83ae6-117">不過，其他未列出的發佈也可能執行 OMS Agent for Linux hello。</span><span class="sxs-lookup"><span data-stu-id="83ae6-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="83ae6-118">Amazon Linux 2012.09 到 2015.09</span><span class="sxs-lookup"><span data-stu-id="83ae6-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="83ae6-119">CentOS Linux 5、6 和 7</span><span class="sxs-lookup"><span data-stu-id="83ae6-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="83ae6-120">Oracle Linux 5、6 和 7</span><span class="sxs-lookup"><span data-stu-id="83ae6-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="83ae6-121">Red Hat Enterprise Linux Server 5、6 和 7</span><span class="sxs-lookup"><span data-stu-id="83ae6-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="83ae6-122">Debian GNU/Linux 6、7 和 8</span><span class="sxs-lookup"><span data-stu-id="83ae6-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="83ae6-123">Ubuntu 12.04 LTS、14.04 LTS、15.04、15.10</span><span class="sxs-lookup"><span data-stu-id="83ae6-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="83ae6-124">SUSE Linux Enterprise Server 11 和 12</span><span class="sxs-lookup"><span data-stu-id="83ae6-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="83ae6-125">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="83ae6-125">OMS Agent for Linux</span></span>
<span data-ttu-id="83ae6-126">hello Operations Management Suite Agent for Linux 包含多個套件。</span><span class="sxs-lookup"><span data-stu-id="83ae6-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="83ae6-127">hello 發行檔案包含下列套件，以執行 hello 殼層配套 hello `--extract`。</span><span class="sxs-lookup"><span data-stu-id="83ae6-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="83ae6-128">**Package**</span><span class="sxs-lookup"><span data-stu-id="83ae6-128">**Package**</span></span> | <span data-ttu-id="83ae6-129">**版本**</span><span class="sxs-lookup"><span data-stu-id="83ae6-129">**Version**</span></span> | <span data-ttu-id="83ae6-130">**說明**</span><span class="sxs-lookup"><span data-stu-id="83ae6-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83ae6-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="83ae6-131">omsagent</span></span> |<span data-ttu-id="83ae6-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="83ae6-132">1.1.0</span></span> |<span data-ttu-id="83ae6-133">hello Operations Management Suite Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="83ae6-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="83ae6-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="83ae6-134">omsconfig</span></span> |<span data-ttu-id="83ae6-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="83ae6-135">1.1.1</span></span> |<span data-ttu-id="83ae6-136">Hello OMS 代理程式的設定代理程式</span><span class="sxs-lookup"><span data-stu-id="83ae6-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="83ae6-137">omi</span><span class="sxs-lookup"><span data-stu-id="83ae6-137">omi</span></span> |<span data-ttu-id="83ae6-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="83ae6-138">1.0.8.3</span></span> |<span data-ttu-id="83ae6-139">開放式管理基礎結構 (OMI) -- 輕量型 CIM 伺服器</span><span class="sxs-lookup"><span data-stu-id="83ae6-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="83ae6-140">scx</span><span class="sxs-lookup"><span data-stu-id="83ae6-140">scx</span></span> |<span data-ttu-id="83ae6-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="83ae6-141">1.6.2</span></span> |<span data-ttu-id="83ae6-142">作業系統效能計量的 OMI CIM 提供者</span><span class="sxs-lookup"><span data-stu-id="83ae6-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="83ae6-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="83ae6-143">apache-cimprov</span></span> |<span data-ttu-id="83ae6-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="83ae6-144">1.0.0</span></span> |<span data-ttu-id="83ae6-145">OMI 的 Apache HTTP 伺服器效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="83ae6-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="83ae6-146">僅在偵測到 Apache HTTP 伺服器時才安裝。</span><span class="sxs-lookup"><span data-stu-id="83ae6-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="83ae6-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="83ae6-147">mysql-cimprov</span></span> |<span data-ttu-id="83ae6-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="83ae6-148">1.0.0</span></span> |<span data-ttu-id="83ae6-149">OMI 的 MySQL 伺服器效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="83ae6-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="83ae6-150">僅在偵測到 MySQL/MariaDB 伺服器時才安裝。</span><span class="sxs-lookup"><span data-stu-id="83ae6-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="83ae6-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="83ae6-151">docker-cimprov</span></span> |<span data-ttu-id="83ae6-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="83ae6-152">0.1.0</span></span> |<span data-ttu-id="83ae6-153">OMI 的 Docker 提供者。</span><span class="sxs-lookup"><span data-stu-id="83ae6-153">Docker provider for OMI.</span></span> <span data-ttu-id="83ae6-154">僅在偵測到 Docker 時才安裝。</span><span class="sxs-lookup"><span data-stu-id="83ae6-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="83ae6-155">其他安裝構件</span><span class="sxs-lookup"><span data-stu-id="83ae6-155">Additional installation artifacts</span></span>
<span data-ttu-id="83ae6-156">在安裝之後 hello OMS agent for Linux 套件，hello 下列全系統設定變更會套用。</span><span class="sxs-lookup"><span data-stu-id="83ae6-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="83ae6-157">解除安裝 hello omsagent 套件時，會移除這些成品。</span><span class="sxs-lookup"><span data-stu-id="83ae6-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="83ae6-158">會建立名為 `omsagent` 的非特殊權限使用者。</span><span class="sxs-lookup"><span data-stu-id="83ae6-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="83ae6-159">這是 hello hello omsagent 精靈執行的帳戶為</span><span class="sxs-lookup"><span data-stu-id="83ae6-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="83ae6-160">Sudoers 的"include"檔案建立在 /etc/sudoers.d/omsagent 這會授權 omsagent toorestart hello syslog 和 omsagent 精靈。</span><span class="sxs-lookup"><span data-stu-id="83ae6-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="83ae6-161">如果 sudo 安裝 hello 版本不支援 sudo"include"指示詞，這些項目會寫入太/等/sudoers。</span><span class="sxs-lookup"><span data-stu-id="83ae6-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="83ae6-162">hello syslog 組態是修改的 tooforward 事件 toohello 代理程式的子集。</span><span class="sxs-lookup"><span data-stu-id="83ae6-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="83ae6-163">如需詳細資訊，請參閱 hello**設定資料收集**下一節</span><span class="sxs-lookup"><span data-stu-id="83ae6-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="83ae6-164">Linux 資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="83ae6-164">Linux data collection details</span></span>
<span data-ttu-id="83ae6-165">hello 下表顯示資料收集方法，以及如何收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="83ae6-166">來源</span><span class="sxs-lookup"><span data-stu-id="83ae6-166">source</span></span> | <span data-ttu-id="83ae6-167">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="83ae6-167">Direct Agent</span></span> | <span data-ttu-id="83ae6-168">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="83ae6-168">SCOM agent</span></span> | <span data-ttu-id="83ae6-169">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="83ae6-169">Azure Storage</span></span> | <span data-ttu-id="83ae6-170">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="83ae6-170">SCOM required?</span></span> | <span data-ttu-id="83ae6-171">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="83ae6-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="83ae6-172">收集頻率</span><span class="sxs-lookup"><span data-stu-id="83ae6-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="83ae6-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="83ae6-173">Zabbix</span></span> |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="83ae6-179">1 分鐘</span><span class="sxs-lookup"><span data-stu-id="83ae6-179">1 minute</span></span> |
| <span data-ttu-id="83ae6-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="83ae6-180">Nagios</span></span> |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="83ae6-186">與抵達同時</span><span class="sxs-lookup"><span data-stu-id="83ae6-186">on arrival</span></span> |
| <span data-ttu-id="83ae6-187">syslog</span><span class="sxs-lookup"><span data-stu-id="83ae6-187">syslog</span></span> |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="83ae6-193">從 Azure 儲存體：10 分鐘；從代理程式：與抵達同時</span><span class="sxs-lookup"><span data-stu-id="83ae6-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="83ae6-194">Linux 效能計數器</span><span class="sxs-lookup"><span data-stu-id="83ae6-194">Linux performance counters</span></span> |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="83ae6-200">依排程，最少 10 秒</span><span class="sxs-lookup"><span data-stu-id="83ae6-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="83ae6-201">變更追蹤</span><span class="sxs-lookup"><span data-stu-id="83ae6-201">change tracking</span></span> |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="83ae6-207">每小時</span><span class="sxs-lookup"><span data-stu-id="83ae6-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="83ae6-208">封裝需求</span><span class="sxs-lookup"><span data-stu-id="83ae6-208">Package Requirements</span></span>
| <span data-ttu-id="83ae6-209">**必要封裝**</span><span class="sxs-lookup"><span data-stu-id="83ae6-209">**Required package**</span></span> | <span data-ttu-id="83ae6-210">**說明**</span><span class="sxs-lookup"><span data-stu-id="83ae6-210">**Description**</span></span> | <span data-ttu-id="83ae6-211">**最低版本**</span><span class="sxs-lookup"><span data-stu-id="83ae6-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83ae6-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="83ae6-212">Glibc</span></span> |<span data-ttu-id="83ae6-213">GNU C 程式庫</span><span class="sxs-lookup"><span data-stu-id="83ae6-213">GNU C library</span></span> |<span data-ttu-id="83ae6-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="83ae6-214">2.5-12</span></span> |
| <span data-ttu-id="83ae6-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="83ae6-215">Openssl</span></span> |<span data-ttu-id="83ae6-216">OpenSSL 程式庫</span><span class="sxs-lookup"><span data-stu-id="83ae6-216">OpenSSL libraries</span></span> |<span data-ttu-id="83ae6-217">0.9.8e 或 1.0</span><span class="sxs-lookup"><span data-stu-id="83ae6-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="83ae6-218">Curl</span><span class="sxs-lookup"><span data-stu-id="83ae6-218">Curl</span></span> |<span data-ttu-id="83ae6-219">cURL Web 用戶端</span><span class="sxs-lookup"><span data-stu-id="83ae6-219">cURL web client</span></span> |<span data-ttu-id="83ae6-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="83ae6-220">7.15.5</span></span> |
| <span data-ttu-id="83ae6-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="83ae6-221">Python-ctypes</span></span> |<span data-ttu-id="83ae6-222">函數程式庫</span><span class="sxs-lookup"><span data-stu-id="83ae6-222">function libraries</span></span> |<span data-ttu-id="83ae6-223">n/a</span><span class="sxs-lookup"><span data-stu-id="83ae6-223">n/a</span></span> |
| <span data-ttu-id="83ae6-224">PAM</span><span class="sxs-lookup"><span data-stu-id="83ae6-224">PAM</span></span> |<span data-ttu-id="83ae6-225">插入式驗證模組</span><span class="sxs-lookup"><span data-stu-id="83ae6-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="83ae6-226">n/a</span><span class="sxs-lookup"><span data-stu-id="83ae6-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="83ae6-227">需要 rsyslog 或 syslog-ng 是必要的 toocollect syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="83ae6-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="83ae6-228">在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。</span><span class="sxs-lookup"><span data-stu-id="83ae6-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="83ae6-229">toocollect syslog 資料，從這一版的這些發佈，hello rsyslog 精靈應該安裝和設定 tooreplace sysklog。</span><span class="sxs-lookup"><span data-stu-id="83ae6-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="83ae6-230">快速安裝</span><span class="sxs-lookup"><span data-stu-id="83ae6-230">Quick install</span></span>
<span data-ttu-id="83ae6-231">執行下列命令 toodownload hello omsagent hello、 驗證 hello 總和檢查碼，然後安裝和上架 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="83ae6-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="83ae6-232">命令是針對 64 位元。</span><span class="sxs-lookup"><span data-stu-id="83ae6-232">Commands are for 64-bit.</span></span> <span data-ttu-id="83ae6-233">hello 工作區識別碼及主索引鍵位於 hello OMS 入口網站下**設定**上 hello**連線來源** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="83ae6-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![工作區詳細資料](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="83ae6-235">有各種不同的其他方法 tooinstall hello 代理程式，並將它升級。</span><span class="sxs-lookup"><span data-stu-id="83ae6-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="83ae6-236">您可以深入資訊，請在[步驟 tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="83ae6-237">您也可以檢視 hello [Azure 影片逐步解說](https://www.youtube.com/watch?v=mF1wtHPEzT0)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="83ae6-238">選擇 Linux 資料收集方法</span><span class="sxs-lookup"><span data-stu-id="83ae6-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="83ae6-239">如何選擇 hello 就像 toocollect 取決於您是否想 toouse hello OMS 入口網站，或您想要編輯直接在 Linux 用戶端上的不同組態檔的資料類型。</span><span class="sxs-lookup"><span data-stu-id="83ae6-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="83ae6-240">如果您選擇 toouse hello 入口網站，hello 組態就會自動傳送 tooall Linux 用戶端。</span><span class="sxs-lookup"><span data-stu-id="83ae6-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="83ae6-241">如果不同 Linux 用戶端需要不同的設定，您將會個別 – 需要 tooedit 用戶端檔案，或使用替代方法，像是 PowerShell DSC、 Chef 或 Puppet。</span><span class="sxs-lookup"><span data-stu-id="83ae6-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="83ae6-242">您可以指定 hello syslog 事件和效能計數器的 toocollect hello Linux 電腦上使用組態檔。</span><span class="sxs-lookup"><span data-stu-id="83ae6-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="83ae6-243">*如果您選擇 tooconfigure 資料收集藉由編輯代理程式組態檔時，您應該停用 hello 集中式的組態。*</span><span class="sxs-lookup"><span data-stu-id="83ae6-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="83ae6-244">Tooconfigure hello 代理程式的組態檔，以及 toodisable 集中式組態的所有 OMS Agents for Linux 個別電腦中的資料收集以下提供的指示。</span><span class="sxs-lookup"><span data-stu-id="83ae6-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="83ae6-245">停用個別 Linux 電腦的 OMS 管理</span><span class="sxs-lookup"><span data-stu-id="83ae6-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="83ae6-246">集中式的資料收集組態資料已停用個別 Linux 電腦以 hello OMS_MetaConfigHelper.py 指令碼。</span><span class="sxs-lookup"><span data-stu-id="83ae6-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="83ae6-247">如果有一部分的電腦應該有特製化組態，則這十分有用。</span><span class="sxs-lookup"><span data-stu-id="83ae6-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="83ae6-248">toodisable 集中式的組態：</span><span class="sxs-lookup"><span data-stu-id="83ae6-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="83ae6-249">toore 啟用集中式的組態：</span><span class="sxs-lookup"><span data-stu-id="83ae6-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="83ae6-250">Linux 效能計數器</span><span class="sxs-lookup"><span data-stu-id="83ae6-250">Linux performance counters</span></span>
<span data-ttu-id="83ae6-251">Linux 效能計數器會類似 tooWindows 效能計數器，兩者的操作類似。</span><span class="sxs-lookup"><span data-stu-id="83ae6-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="83ae6-252">您可以使用下列程序 tooadd hello 並設定它們。</span><span class="sxs-lookup"><span data-stu-id="83ae6-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="83ae6-253">新增 tooOMS 之後，會收集資料，每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="83ae6-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="83ae6-254">tooadd 在 OMS 中的 Linux 效能計數器</span><span class="sxs-lookup"><span data-stu-id="83ae6-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="83ae6-255">tooconfigure OMS Agents for Linux 使用 hello OMS 入口網站，您可以新增 Linux 效能計數器在 hello 設定頁面上，按一下 **資料**。</span><span class="sxs-lookup"><span data-stu-id="83ae6-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="83ae6-256">在 hello**設定**頁面**資料**，按一下**Linux 效能計數器**，然後選取或類型的 hello 名稱要 tooadd 的 hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="83ae6-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="83ae6-257">![資料](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="83ae6-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="83ae6-258">如果您不知道 hello 的 hello 計數器的完整名稱，您可以開始輸入部分名稱，即會出現可用的計數器清單。</span><span class="sxs-lookup"><span data-stu-id="83ae6-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="83ae6-259">當您找到 hello 計數器您想 tooadd，按一下 [hello] 清單中的 hello 名稱，然後按一下 hello 加上圖示 tooadd hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="83ae6-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="83ae6-260">新增 hello 計數器之後，它會出現在 hello 以彩色列反白顯示的計數器清單。</span><span class="sxs-lookup"><span data-stu-id="83ae6-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="83ae6-261">根據預設，hello**套用下列組態 toomy 電腦**選取選項。</span><span class="sxs-lookup"><span data-stu-id="83ae6-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="83ae6-262">如果您想將組態資料傳送 toodisable，清除 hello 選取項目。</span><span class="sxs-lookup"><span data-stu-id="83ae6-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="83ae6-263">當您完成修改效能計數器時，在 hello hello 頁面底部按一下**儲存**toofinalize 您的變更。</span><span class="sxs-lookup"><span data-stu-id="83ae6-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="83ae6-264">您所做的 hello 組態變更便會傳送 tooall hello OMS Agents for Linux，會向 OMS 時，通常會在 5 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="83ae6-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="83ae6-265">在 OMS 中設定 Linux 效能計數器</span><span class="sxs-lookup"><span data-stu-id="83ae6-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="83ae6-266">對於 Windows 效能計數器，您可以選擇每個效能計數器的特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="83ae6-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="83ae6-267">不過，對於 Linux 效能計數器，您所選擇的計數器任何執行個體適用於 tooall 的 hello 父計數器的子系計數器。</span><span class="sxs-lookup"><span data-stu-id="83ae6-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="83ae6-268">hello 下表顯示 hello 常見執行個體可用 tooboth Linux 和 Windows 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="83ae6-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="83ae6-269">**執行個體名稱**</span><span class="sxs-lookup"><span data-stu-id="83ae6-269">**Instance name**</span></span> | <span data-ttu-id="83ae6-270">**意義**</span><span class="sxs-lookup"><span data-stu-id="83ae6-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="83ae6-271">\_總計</span><span class="sxs-lookup"><span data-stu-id="83ae6-271">\_Total</span></span> |<span data-ttu-id="83ae6-272">所有的 hello 執行個體的總數</span><span class="sxs-lookup"><span data-stu-id="83ae6-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="83ae6-273">所有執行個體</span><span class="sxs-lookup"><span data-stu-id="83ae6-273">All instances</span></span> |
| <span data-ttu-id="83ae6-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="83ae6-274">(/&#124;/var)</span></span> |<span data-ttu-id="83ae6-275">比對名為 / 或 /var 的執行個體</span><span class="sxs-lookup"><span data-stu-id="83ae6-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="83ae6-276">同樣地，hello 取樣間隔，您選擇為父計數器適用於 tooall 及其子系計數器。</span><span class="sxs-lookup"><span data-stu-id="83ae6-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="83ae6-277">換句話說，所有 hello 子系計數器取樣間隔和執行個體都連結在一起。</span><span class="sxs-lookup"><span data-stu-id="83ae6-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="83ae6-278">使用 Linux 加入和設定效能計量</span><span class="sxs-lookup"><span data-stu-id="83ae6-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="83ae6-279">效能度量 toocollect 受到 hello 組態在/等/選擇/microsoft/omsagent/&lt;工作區識別碼&gt;/conf/omsagent.conf。</span><span class="sxs-lookup"><span data-stu-id="83ae6-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="83ae6-280">請參閱[可用的效能標準](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics)可用的類別和校 hello OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="83ae6-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="83ae6-281">應為單一 hello 組態檔中定義每個物件或類別目錄的效能度量 toocollect`<source>`項目。</span><span class="sxs-lookup"><span data-stu-id="83ae6-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="83ae6-282">hello 語法遵循下列的 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="83ae6-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="83ae6-283">這個項目的 hello 可設定參數如下：</span><span class="sxs-lookup"><span data-stu-id="83ae6-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="83ae6-284">**物件\_名稱**: hello hello 集合的物件名稱。</span><span class="sxs-lookup"><span data-stu-id="83ae6-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="83ae6-285">**執行個體\_regex**:*規則運算式*定義哪些執行個體 toocollect。</span><span class="sxs-lookup"><span data-stu-id="83ae6-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="83ae6-286">hello 值：`.*`指定所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="83ae6-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="83ae6-287">toocollect 處理器校能標準只 hello\_總執行個體，您可以指定`_Total`。</span><span class="sxs-lookup"><span data-stu-id="83ae6-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="83ae6-288">toocollect 的處理序校只 hello crond 或 sshd 執行個體，您可以指定： `(crond|sshd)`。</span><span class="sxs-lookup"><span data-stu-id="83ae6-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="83ae6-289">**計數器\_名稱\_regex**:*規則運算式*定義哪些物件的計數器 （hello） toocollect。</span><span class="sxs-lookup"><span data-stu-id="83ae6-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="83ae6-290">toocollect hello 物件的所有計數器都指定： `.*`。</span><span class="sxs-lookup"><span data-stu-id="83ae6-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="83ae6-291">toocollect 只會交換空間計數器 hello 記憶體物件，您可以指定：`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="83ae6-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="83ae6-292">**間隔：**: hello 的 hello 收集物件計數器頻率。</span><span class="sxs-lookup"><span data-stu-id="83ae6-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="83ae6-293">效能標準的 hello 預設組態是：</span><span class="sxs-lookup"><span data-stu-id="83ae6-293">hello default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="83ae6-294">使用 Linux 命令啟用 MySQL 效能計數器</span><span class="sxs-lookup"><span data-stu-id="83ae6-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="83ae6-295">如果 MySQL 伺服器或 MariaDB 伺服器偵測到 hello 電腦上安裝 hello omsagent 配套時，會自動安裝的效能監視提供者的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="83ae6-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="83ae6-296">此提供者連接 toohello 本機 MySQL/MariaDB 伺服器 tooexpose 效能統計資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="83ae6-297">您需要 tooconfigure MySQL 使用者認證，讓 hello 者可以存取 MySQL 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="83ae6-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="83ae6-298">toodefine 預設使用者帳戶 hello MySQL 伺服器的 localhost，下列命令範例使用 hello 上。</span><span class="sxs-lookup"><span data-stu-id="83ae6-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="83ae6-299">hello 認證檔案必須可供 hello omsagent 帳戶讀取。</span><span class="sxs-lookup"><span data-stu-id="83ae6-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="83ae6-300">建議您以 omsgent 的身分 hello mycimprovauth 命令。</span><span class="sxs-lookup"><span data-stu-id="83ae6-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="83ae6-301">或者，您可以指定 hello 需要 MySQL 認證，在檔案中，建立 hello 檔案： /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth如需管理 MySQL 認證以便透過 hello mysql-auth 檔案進行監視的詳細資訊，請參閱[管理 MySQL 監視認證 hello 驗證檔案中的](#manage-mysql-monitoring-credentials-in-the-authentication-file)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="83ae6-302">請參閱[資料庫 MySQL 效能計數器所需的權限](#database-permissions-required-for-mysql-performance-counters)hello MySQL 使用者 toocollect MySQL 伺服器效能資料所需的物件權限的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="83ae6-303">使用 Linux 命令啟用 Apache HTTP 伺服器效能計數器</span><span class="sxs-lookup"><span data-stu-id="83ae6-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="83ae6-304">如果 Apache HTTP Server 是電腦上偵測到 hello 安裝 hello omsagent 配套時，會自動安裝的效能監視適用於 Apache HTTP Server 提供者。</span><span class="sxs-lookup"><span data-stu-id="83ae6-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="83ae6-305">此提供者依賴 Apache 「 模組 」，必須載入順序 tooaccess 效能資料中的 hello Apache HTTP Server。</span><span class="sxs-lookup"><span data-stu-id="83ae6-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="83ae6-306">您可以載入 hello 模組以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="83ae6-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="83ae6-307">toounload hello Apache 監視模組，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="83ae6-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="83ae6-308">記錄分析 tooview 效能資料</span><span class="sxs-lookup"><span data-stu-id="83ae6-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="83ae6-309">在 hello Operations Management Suite 入口網站中，按一下 hello 記錄搜尋 磚。</span><span class="sxs-lookup"><span data-stu-id="83ae6-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="83ae6-310">在 hello 搜尋列中輸入`* (Type=Perf)`tooview 所有效能計數器。</span><span class="sxs-lookup"><span data-stu-id="83ae6-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="83ae6-311">因為 OMS 也會收集 Windows 效能計數器資料，您應該將範圍縮小 hello 搜尋 tooLinux 特定資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="83ae6-312">因此，hello 下列範例會顯示效能資料特定 tooan 範例 Linux 伺服器名為 Chorizo21。</span><span class="sxs-lookup"><span data-stu-id="83ae6-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![搜尋結果中所顯示的範例伺服器](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="83ae6-314">您可以在 hello 結果中，按一下**度量**tooview hello 計數器，用來收集資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="83ae6-315">每個計數器的即時資料會顯示為圖形。</span><span class="sxs-lookup"><span data-stu-id="83ae6-315">Real-time data is shown as graphs for each counter.</span></span>

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="83ae6-317">syslog</span><span class="sxs-lookup"><span data-stu-id="83ae6-317">Syslog</span></span>
<span data-ttu-id="83ae6-318">Syslog 是事件記錄通訊協定類似 tooWindows 事件記錄檔，兩者的操作類似在 OMS 中顯示時。</span><span class="sxs-lookup"><span data-stu-id="83ae6-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="83ae6-319">tooadd 在 OMS 中新增 Linux syslog 設備</span><span class="sxs-lookup"><span data-stu-id="83ae6-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="83ae6-320">在 hello**設定**頁面**資料**，按一下  **Syslog**然後 toohello 左的 hello 加號圖示，輸入您想 tooadd hello syslog 設備 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="83ae6-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="83ae6-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="83ae6-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="83ae6-322">如果您不知道 hello 設備 hello 完整名稱，您可以開始輸入部分名稱，即會出現可用的 syslog 設備清單。</span><span class="sxs-lookup"><span data-stu-id="83ae6-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="83ae6-323">當您找到您想 tooadd，按一下 [hello] 清單中的 hello 名稱，然後按一下hello 加上圖示 tooadd hello hello syslog 設備 syslog 設備。</span><span class="sxs-lookup"><span data-stu-id="83ae6-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="83ae6-324">您新增 hello 設備，它會出現在 hello 清單之後反白顯示以彩色列。</span><span class="sxs-lookup"><span data-stu-id="83ae6-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="83ae6-325">接下來，選擇 hello 嚴重性 （syslog 設備資訊的類別） 的 toocollect。</span><span class="sxs-lookup"><span data-stu-id="83ae6-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="83ae6-326">在 hello hello 頁面底部按一下**儲存**toofinalize 您的變更。</span><span class="sxs-lookup"><span data-stu-id="83ae6-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="83ae6-327">您所做的 hello 組態變更便會傳送 tooall hello OMS Agents for Linux，會向 OMS 時，通常會在 5 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="83ae6-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="83ae6-328">在 Linux 中設定 Linux syslog 設備</span><span class="sxs-lookup"><span data-stu-id="83ae6-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="83ae6-329">Syslog 事件從 hello syslog 服務精靈傳送，例如 rsyslog 或 syslog ng、 tooa 本機連接埠的 hello 代理程式正在接聽。</span><span class="sxs-lookup"><span data-stu-id="83ae6-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="83ae6-330">連接埠預設為 25224。</span><span class="sxs-lookup"><span data-stu-id="83ae6-330">By default, port 25224.</span></span> <span data-ttu-id="83ae6-331">Hello 代理程式安裝時，會套用預設 syslog 組態。</span><span class="sxs-lookup"><span data-stu-id="83ae6-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="83ae6-332">這可以在下列項目中找到︰</span><span class="sxs-lookup"><span data-stu-id="83ae6-332">This is found at:</span></span>

<span data-ttu-id="83ae6-333">Rsyslog：/etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="83ae6-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="83ae6-334">Syslog-ng：/etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="83ae6-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="83ae6-335">hello 預設 OMS 代理程式 syslog 組態會上傳所有設備的嚴重性為警告或更高的 syslog 事件。</span><span class="sxs-lookup"><span data-stu-id="83ae6-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="83ae6-336">如果您編輯 hello syslog 設定，您必須重新啟動 hello 變更 tootake 效果 hello syslog 服務精靈。</span><span class="sxs-lookup"><span data-stu-id="83ae6-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="83ae6-337">hello 預設 syslog 組態 hello OMS Agent for Linux 的 OMS 是：</span><span class="sxs-lookup"><span data-stu-id="83ae6-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="83ae6-338">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="83ae6-338">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="83ae6-339">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="83ae6-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="83ae6-340">tooview 記錄分析的所有 Syslog 事件</span><span class="sxs-lookup"><span data-stu-id="83ae6-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="83ae6-341">在 hello Operations Management Suite 入口網站中，按一下 hello**記錄搜尋**磚。</span><span class="sxs-lookup"><span data-stu-id="83ae6-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="83ae6-342">在 hello**記錄管理**群組中選擇預先定義的 syslog 搜尋，然後選取一個 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="83ae6-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="83ae6-343">此範例示範所有 Syslog 事件。</span><span class="sxs-lookup"><span data-stu-id="83ae6-343">This example shows all Syslog events.</span></span>

![記錄檔搜尋中所顯示的 Syslog 事件](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="83ae6-345">現在，您可以切入至搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="83ae6-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="83ae6-346">Linux 警示</span><span class="sxs-lookup"><span data-stu-id="83ae6-346">Linux alerts</span></span>
<span data-ttu-id="83ae6-347">如果您使用 Nagios 或 Zabbix toomanage 您的 Linux 機器，則 OMS 可以接收來自這些工具所產生的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="83ae6-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="83ae6-348">不過，目前沒有方法 tooconfigure 傳入的警示資料使用 hello OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="83ae6-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="83ae6-349">相反地，您將需要 tooedit 組態檔案 toostart 傳送警示 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="83ae6-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="83ae6-350">收集來自 Nagios 的警示</span><span class="sxs-lookup"><span data-stu-id="83ae6-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="83ae6-351">從 Nagios 伺服器 toocollect 警示，您需要下列設定變更 toomake hello。</span><span class="sxs-lookup"><span data-stu-id="83ae6-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="83ae6-352">授與 hello 使用者**omsagent**讀取權限 toohello Nagios 記錄檔 (也就是 /var/log/nagios/nagios.log)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="83ae6-353">假設 hello nagios.log 檔案由 hello 群組擁有**nagios** ，您可以加入 hello 使用者**omsagent** toohello **nagios**群組。</span><span class="sxs-lookup"><span data-stu-id="83ae6-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="83ae6-354">修改 hello omsagent.confconfiguration 檔案 (等/選擇/microsoft/omsagent /&lt;工作區識別碼&gt;/conf/omsagent.conf)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="83ae6-355">請確定下列項目 hello 確實存在且未標成註解：</span><span class="sxs-lookup"><span data-stu-id="83ae6-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="83ae6-356">重新啟動 hello omsagent 精靈：</span><span class="sxs-lookup"><span data-stu-id="83ae6-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="83ae6-357">收集來自 Zabbix 的警示</span><span class="sxs-lookup"><span data-stu-id="83ae6-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="83ae6-358">toocollect 警示 Zabbix 伺服器，只不過您必須 toospecify 使用者和密碼，您將會如上述，Nagios 執行類似的步驟 toothose*純文字*。</span><span class="sxs-lookup"><span data-stu-id="83ae6-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="83ae6-359">這不是理想的做法，可能很快就會變更。</span><span class="sxs-lookup"><span data-stu-id="83ae6-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="83ae6-360">tooaddress 此問題，我們建議您建立 hello 使用者並授與其權限 toomonitor 只。</span><span class="sxs-lookup"><span data-stu-id="83ae6-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="83ae6-361">Hello omsagent.conf 組態檔中的範例 > 一節 (等/選擇/microsoft/omsagent /&lt;工作區識別碼&gt;/conf/omsagent.conf) 的 Zabbix 應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="83ae6-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="83ae6-362">在 Log Analytics 搜尋中檢視警示</span><span class="sxs-lookup"><span data-stu-id="83ae6-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="83ae6-363">設定 Linux 電腦 toosend 警示 tooOMS 之後，您可以使用幾個簡單的記錄搜尋查詢 tooview hello 警示。</span><span class="sxs-lookup"><span data-stu-id="83ae6-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="83ae6-364">hello 下列搜尋查詢範例會傳回所產生的所有記錄的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="83ae6-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="83ae6-365">例如，如果在您的 IT 基礎結構發生某種問題，然後對結果 hello 下列範例查詢可能表示 hello 問題可能產生的位置。</span><span class="sxs-lookup"><span data-stu-id="83ae6-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="83ae6-366">而且，您可以輕鬆地鑽研 toohello 警示中的半形的來源系統 toohelp 調查。</span><span class="sxs-lookup"><span data-stu-id="83ae6-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="83ae6-367">hello 好處是，您不一定需要 toogo toovarious 管理系統從 hello 開始，前提是您的警示傳送 tooOMS，您可以從那裡開始。</span><span class="sxs-lookup"><span data-stu-id="83ae6-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="83ae6-368">tooview 記錄分析所有的 Nagios 警示</span><span class="sxs-lookup"><span data-stu-id="83ae6-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="83ae6-369">在 hello Operations Management Suite 入口網站中，按一下 hello**記錄搜尋**磚。</span><span class="sxs-lookup"><span data-stu-id="83ae6-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="83ae6-370">在 hello 查詢列中，輸入下列搜尋查詢的 hello</span><span class="sxs-lookup"><span data-stu-id="83ae6-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![記錄檔搜尋中所顯示的 Nagios 警示](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="83ae6-372">您會看到 hello 搜尋結果之後，您可以切入其他詳細資料這類*AlertState*。</span><span class="sxs-lookup"><span data-stu-id="83ae6-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="83ae6-373">tooview 記錄分析所有的 Zabbix 警示</span><span class="sxs-lookup"><span data-stu-id="83ae6-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="83ae6-374">在 hello Operations Management Suite 入口網站中，按一下 hello**記錄搜尋**磚。</span><span class="sxs-lookup"><span data-stu-id="83ae6-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="83ae6-375">在 hello 查詢列中，輸入下列搜尋查詢的 hello</span><span class="sxs-lookup"><span data-stu-id="83ae6-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![記錄檔搜尋中所顯示的 Zabbix 警示](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="83ae6-377">您會看到 hello 搜尋結果之後，您可以切入其他詳細資料這類*AlertName*。</span><span class="sxs-lookup"><span data-stu-id="83ae6-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="83ae6-378">與 System Center Operations Manager 的相容性</span><span class="sxs-lookup"><span data-stu-id="83ae6-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="83ae6-379">hello OMS Agent for Linux 與 hello System Center Operations Manager 代理程式共用代理程式二進位檔。</span><span class="sxs-lookup"><span data-stu-id="83ae6-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="83ae6-380">升級目前由 Operations Manager 管理的系統上，安裝 hello OMS Agent for Linux hello hello 電腦 tooa 較新版本的 OMI 和 SCX 封裝。</span><span class="sxs-lookup"><span data-stu-id="83ae6-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="83ae6-381">hello OMS Agent for Linux 和 System Center 2012 R2 都相容。</span><span class="sxs-lookup"><span data-stu-id="83ae6-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="83ae6-382">不過， **System Center 2012 SP1 和較早版本目前不是相容或支援以 hello OMS Agent for Linux。**</span><span class="sxs-lookup"><span data-stu-id="83ae6-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="83ae6-383">如果 hello OMS Agent for Linux 安裝的 tooa 目前不是由 Operations Manager 管理的電腦，而且您稍後想 toomanage hello 電腦與 Operations Manager，您必須修改 hello OMI 設定才能探索 hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="83ae6-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="83ae6-384">**如果之前 hello OMS Agent for Linux 安裝 hello Operations Manager 代理程式，不需要執行此步驟。**</span><span class="sxs-lookup"><span data-stu-id="83ae6-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="83ae6-385">tooenable hello OMS Agent for Linux toocommunicate 與 Operations Manager</span><span class="sxs-lookup"><span data-stu-id="83ae6-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="83ae6-386">編輯 hello 檔案 /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="83ae6-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="83ae6-387">請確定該 hello 行首**httpsport =**定義 hello 連接埠 1270年。</span><span class="sxs-lookup"><span data-stu-id="83ae6-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="83ae6-388">例如 `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="83ae6-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="83ae6-389">重新啟動 hello OMI 伺服器：</span><span class="sxs-lookup"><span data-stu-id="83ae6-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="83ae6-390">MySQL 效能計數器所需的資料庫權限</span><span class="sxs-lookup"><span data-stu-id="83ae6-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="83ae6-391">toogrant 權限 tooa MySQL 監視使用者，hello 授與的使用者必須具有 hello 'GRANT option' 權限，以及被授與的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="83ae6-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="83ae6-392">為了讓 MySQL 使用者 hello tooreturn 效能資料 hello 使用者需要存取 toohello 下列查詢：</span><span class="sxs-lookup"><span data-stu-id="83ae6-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="83ae6-393">此外 toothese 查詢 hello MySQL 使用者也需要下列預設資料表的選取存取 toohello:</span><span class="sxs-lookup"><span data-stu-id="83ae6-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="83ae6-394">information_schema</span><span class="sxs-lookup"><span data-stu-id="83ae6-394">information_schema</span></span>
* <span data-ttu-id="83ae6-395">mysql</span><span class="sxs-lookup"><span data-stu-id="83ae6-395">mysql</span></span>

<span data-ttu-id="83ae6-396">執行下列 grant 命令 hello 可以授與這些權限。</span><span class="sxs-lookup"><span data-stu-id="83ae6-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="83ae6-397">管理 MySQL 監視認證 hello 驗證檔案中</span><span class="sxs-lookup"><span data-stu-id="83ae6-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="83ae6-398">hello 面各節協助您管理 MySQL 認證。</span><span class="sxs-lookup"><span data-stu-id="83ae6-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="83ae6-399">設定 MySQL OMI 提供者 hello</span><span class="sxs-lookup"><span data-stu-id="83ae6-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="83ae6-400">hello MySQL OMI 提供者需要預先設定的 MySQL 使用者，並安裝 MySQL 用戶端程式庫中訂單 tooquery hello 效能/健全狀況資訊從 hello MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="83ae6-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="83ae6-401">MySQL OMI 驗證檔案</span><span class="sxs-lookup"><span data-stu-id="83ae6-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="83ae6-402">MySQL OMI 提供者使用哪些繫結位址和連接埠 hello MySQL 執行個體正在接聽驗證檔案 toodetermine 和以及認證 toouse toogather 度量。</span><span class="sxs-lookup"><span data-stu-id="83ae6-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="83ae6-403">在安裝 hello MySQL OMI 提供者會掃描 MySQL my.cnf 組態檔 （預設位置） 繫結位址和連接埠和組 hello MySQL OMI 驗證檔案部分。</span><span class="sxs-lookup"><span data-stu-id="83ae6-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="83ae6-404">toocomplete 監視 MySQL 伺服器執行個體，將預先產生的 MySQL OMI 驗證檔案加入至 hello 正確的目錄。</span><span class="sxs-lookup"><span data-stu-id="83ae6-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="83ae6-405">驗證檔案格式</span><span class="sxs-lookup"><span data-stu-id="83ae6-405">Authentication file format</span></span>
<span data-ttu-id="83ae6-406">hello MySQL OMI 驗證檔案是文字檔，其中包含有關的資訊：</span><span class="sxs-lookup"><span data-stu-id="83ae6-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="83ae6-407">Port</span><span class="sxs-lookup"><span data-stu-id="83ae6-407">Port</span></span>
* <span data-ttu-id="83ae6-408">繫結位址</span><span class="sxs-lookup"><span data-stu-id="83ae6-408">Bind-Address</span></span>
* <span data-ttu-id="83ae6-409">MySQL 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="83ae6-409">MySQL username</span></span>
* <span data-ttu-id="83ae6-410">Base64 編碼的密碼</span><span class="sxs-lookup"><span data-stu-id="83ae6-410">Base64 encoded password</span></span>

<span data-ttu-id="83ae6-411">hello MySQL OMI 驗證檔案只授與產生它的讀取/寫入 toohello Linux 使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="83ae6-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="83ae6-412">預設 MySQL OMI 驗證檔案包含預設執行個體和連接埠號碼，視何種資訊可用且剖析從 hello 找到 MySQL 組態檔。</span><span class="sxs-lookup"><span data-stu-id="83ae6-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="83ae6-413">hello 預設執行個體管理較為簡單，一部 Linux 主機上的多個 MySQL 執行個體表示 toomake 且由 hello 與連接埠 0 的執行個體所表示。</span><span class="sxs-lookup"><span data-stu-id="83ae6-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="83ae6-414">所有新增的執行個體將會繼承 hello 預設執行個體設定的內容。</span><span class="sxs-lookup"><span data-stu-id="83ae6-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="83ae6-415">例如，如果新增接聽通訊埠 '3308' 的 MySQL 執行個體，hello 預設執行個體的繫結位址、 使用者名稱和 Base64 編碼的密碼將會使用的 tootry 並監視 hello 接聽 3308 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="83ae6-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="83ae6-416">如果 3308 上的 hello 執行個體是繫結 tooanother 位址使用 hello 相同的 MySQL 使用者名稱和密碼組僅 hello hello 重新指定需要繫結位址，而且 hello 其他屬性會被繼承。</span><span class="sxs-lookup"><span data-stu-id="83ae6-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="83ae6-417">Hello 驗證檔案的範例如下 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="83ae6-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="83ae6-418">預設執行個體與連接埠為 3308 的執行個體：</span><span class="sxs-lookup"><span data-stu-id="83ae6-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="83ae6-419">預設執行個體與連接埠為 3308 的執行個體 + 不同 Base64 編碼的密碼：</span><span class="sxs-lookup"><span data-stu-id="83ae6-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="83ae6-420">**屬性**</span><span class="sxs-lookup"><span data-stu-id="83ae6-420">**Property**</span></span> | <span data-ttu-id="83ae6-421">**說明**</span><span class="sxs-lookup"><span data-stu-id="83ae6-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="83ae6-422">Port</span><span class="sxs-lookup"><span data-stu-id="83ae6-422">Port</span></span> |<span data-ttu-id="83ae6-423">連接埠代表目前的連接埠 hello hello MySQL 執行個體正在接聽。</span><span class="sxs-lookup"><span data-stu-id="83ae6-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="83ae6-424">hello 連接埠 0 表示預設執行個體，會使用下列的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="83ae6-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="83ae6-425">繫結位址</span><span class="sxs-lookup"><span data-stu-id="83ae6-425">Bind-Address</span></span> |<span data-ttu-id="83ae6-426">hello 繫結位址是 hello 目前的 MySQL 繫結位址</span><span class="sxs-lookup"><span data-stu-id="83ae6-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="83ae6-427">username</span><span class="sxs-lookup"><span data-stu-id="83ae6-427">username</span></span> |<span data-ttu-id="83ae6-428">這個 hello 使用者的使用者名稱 hello MySQL 您希望 toouse toomonitor hello MySQL 伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="83ae6-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="83ae6-429">Base64 編碼的密碼</span><span class="sxs-lookup"><span data-stu-id="83ae6-429">Base64 encoded Password</span></span> |<span data-ttu-id="83ae6-430">這是以 Base64 編碼的 hello MySQL 監視使用者的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="83ae6-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="83ae6-431">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="83ae6-431">AutoUpdate</span></span> |<span data-ttu-id="83ae6-432">Hello MySQL OMI 提供者升級時 hello 提供者會重新掃描 hello my.cnf 檔案有變更，並覆寫 hello MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="83ae6-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="83ae6-433">設定此旗標 tootrue 或視需要的更新 toohello MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="83ae6-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="83ae6-434">驗證檔案位置</span><span class="sxs-lookup"><span data-stu-id="83ae6-434">Authentication file location</span></span>
<span data-ttu-id="83ae6-435">hello MySQL OMI 驗證檔案應該位於下列位置的 hello 和名為"mysql auth":</span><span class="sxs-lookup"><span data-stu-id="83ae6-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="83ae6-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="83ae6-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="83ae6-437">hello 檔案 （和 auth/omsagent 目錄） 應該 hello omsagent 使用者所擁有。</span><span class="sxs-lookup"><span data-stu-id="83ae6-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="83ae6-438">代理程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-438">Agent logs</span></span>
<span data-ttu-id="83ae6-439">hello hello OMS Agent for Linux 的記錄檔位於：</span><span class="sxs-lookup"><span data-stu-id="83ae6-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="83ae6-440">/var/opt/microsoft/omsagent/&lt;工作區識別碼&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="83ae6-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="83ae6-441">hello 記錄檔中的 hello OMS Agent for Linux 的 omsconfig （代理程式組態） 程式位於：</span><span class="sxs-lookup"><span data-stu-id="83ae6-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="83ae6-442">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="83ae6-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="83ae6-443">Hello OMI 和 SCX 元件 （提供效能標準資料） 的記錄檔位於：</span><span class="sxs-lookup"><span data-stu-id="83ae6-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="83ae6-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="83ae6-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="83ae6-445">疑難排解 hello OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="83ae6-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="83ae6-446">使用下列資訊 toodiagnose hello 和疑難排解常見的問題。</span><span class="sxs-lookup"><span data-stu-id="83ae6-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="83ae6-447">如果無 hello 疑難排解這一節的資訊可協助您，您也可以使用下列資源 toohelp 解析 hello 您的問題。</span><span class="sxs-lookup"><span data-stu-id="83ae6-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="83ae6-448">具有頂級支援的客戶可以透過[頂級支援](https://premier.microsoft.com/)記錄支援案例</span><span class="sxs-lookup"><span data-stu-id="83ae6-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="83ae6-449">Azure 支援合約客戶可以記錄的支援案例 hello [Azure 入口網站](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="83ae6-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="83ae6-450">將 [GitHub 問題](https://github.com/Microsoft/OMS-Agent-for-Linux/issues) 歸檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="83ae6-451">意見反應的意見和問題報告 toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="83ae6-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="83ae6-452">重要記錄檔位置</span><span class="sxs-lookup"><span data-stu-id="83ae6-452">Important log locations</span></span>
| <span data-ttu-id="83ae6-453">檔案</span><span class="sxs-lookup"><span data-stu-id="83ae6-453">File</span></span> | <span data-ttu-id="83ae6-454">路徑</span><span class="sxs-lookup"><span data-stu-id="83ae6-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="83ae6-455">OMS Agent for Linux 記錄檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="83ae6-456">OMS Agent 組態記錄檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="83ae6-457">重要組態檔案</span><span class="sxs-lookup"><span data-stu-id="83ae6-457">Important configuration files</span></span>
| <span data-ttu-id="83ae6-458">分類</span><span class="sxs-lookup"><span data-stu-id="83ae6-458">Catergory</span></span> | <span data-ttu-id="83ae6-459">檔案位置</span><span class="sxs-lookup"><span data-stu-id="83ae6-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="83ae6-460">syslog</span><span class="sxs-lookup"><span data-stu-id="83ae6-460">Syslog</span></span> |<span data-ttu-id="83ae6-461">`/etc/syslog-ng/syslog-ng.conf`、`/etc/rsyslog.conf` 或 `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="83ae6-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="83ae6-462">效能、Nagios、Zabbix、OMS 輸出和一般代理程式</span><span class="sxs-lookup"><span data-stu-id="83ae6-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="83ae6-463">其他組態</span><span class="sxs-lookup"><span data-stu-id="83ae6-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="83ae6-464">編輯效能計數器的組態檔，而若已啟用 OMS 入口網站組態，則會覆寫 syslog。</span><span class="sxs-lookup"><span data-stu-id="83ae6-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="83ae6-465">您可以停用 hello OMS 入口網站 （適用於所有節點） 中的組態或單一執行 hello 下列節點：</span><span class="sxs-lookup"><span data-stu-id="83ae6-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="83ae6-466">啟用偵錯記錄</span><span class="sxs-lookup"><span data-stu-id="83ae6-466">Enable debug logging</span></span>
<span data-ttu-id="83ae6-467">tooenable 偵錯記錄，您可以使用 hello OMS 輸出外掛程式和詳細資訊輸出。</span><span class="sxs-lookup"><span data-stu-id="83ae6-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="83ae6-468">OMS 輸出外掛程式</span><span class="sxs-lookup"><span data-stu-id="83ae6-468">OMS output plugin</span></span>
<span data-ttu-id="83ae6-469">FluentD 允許 hello 外掛程式 toospecify 輸入與輸出不同的記錄層級的記錄層級。</span><span class="sxs-lookup"><span data-stu-id="83ae6-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="83ae6-470">toospecify OMS 輸出是不同的記錄層級編輯 hello 一般的代理程式設定在 hello`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`檔案。</span><span class="sxs-lookup"><span data-stu-id="83ae6-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="83ae6-471">附近的 hello 設定檔的 hello 底部，變更 hello`log_level`屬性從`info`太`debug`。</span><span class="sxs-lookup"><span data-stu-id="83ae6-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="83ae6-472">偵錯記錄可讓您 toosee 批次上傳 toohello OMS 服務分隔型別，資料項目和 toosend 所花費時間的數目。</span><span class="sxs-lookup"><span data-stu-id="83ae6-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="83ae6-473">*啟用偵錯的記錄檔範例︰*</span><span class="sxs-lookup"><span data-stu-id="83ae6-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="83ae6-474">詳細資訊輸出</span><span class="sxs-lookup"><span data-stu-id="83ae6-474">Verbose output</span></span>
<span data-ttu-id="83ae6-475">不使用 hello OMS 輸出外掛程式，您也可以輸出資料項目直接太`stdout`，這會顯示在 hello OMS Agent for Linux 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="83ae6-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="83ae6-476">在 hello OMS 一般的代理程式組態檔中`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`，註解外 hello OMS 加入輸出外掛程式`#`前面每一行。</span><span class="sxs-lookup"><span data-stu-id="83ae6-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="83ae6-477">下面 hello 輸出外掛程式，請移除 hello 藉由移除 hello 之後 > 一節中的 hello 註解`#`每一行的 hello 開頭的符號。</span><span class="sxs-lookup"><span data-stu-id="83ae6-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="83ae6-478">轉寄的 Syslog 訊息不會出現在 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="83ae6-479">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83ae6-479">Probable causes</span></span>
* <span data-ttu-id="83ae6-480">hello 套用設定 toohello Linux 伺服器不會不允許傳送嗨設備的集合和/或記錄層級</span><span class="sxs-lookup"><span data-stu-id="83ae6-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="83ae6-481">Syslog 不是被轉送正確 toohello Linux 伺服器</span><span class="sxs-lookup"><span data-stu-id="83ae6-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="83ae6-482">每秒所轉寄的訊息的 hello 數目太大的 hello OMS Agent for Linux toohandle hello 基底組態</span><span class="sxs-lookup"><span data-stu-id="83ae6-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="83ae6-483">解決方式</span><span class="sxs-lookup"><span data-stu-id="83ae6-483">Resolutions</span></span>
* <span data-ttu-id="83ae6-484">確認 hello hello OMS 入口網站中的設定 Syslog 有所有 hello 設備和 hello 正確的記錄層級</span><span class="sxs-lookup"><span data-stu-id="83ae6-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="83ae6-485">**OMS 入口網站 > 設定 > 資料 > Syslog**</span><span class="sxs-lookup"><span data-stu-id="83ae6-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="83ae6-486">請確認該原生的 syslog 訊息精靈 (`rsyslog`， `syslog-ng`) 是可以 tooreceive hello 轉送訊息</span><span class="sxs-lookup"><span data-stu-id="83ae6-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="83ae6-487">請檢查防火牆設定 hello Syslog 伺服器 tooensure 都不會封鎖訊息</span><span class="sxs-lookup"><span data-stu-id="83ae6-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="83ae6-488">模擬使用 hello Syslog 訊息 tooOMS`logger`命令-例如：</span><span class="sxs-lookup"><span data-stu-id="83ae6-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="83ae6-489">使用 proxy 時，連線 tooOMS 問題</span><span class="sxs-lookup"><span data-stu-id="83ae6-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="83ae6-490">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83ae6-490">Probable causes</span></span>
* <span data-ttu-id="83ae6-491">hello proxy 可讓您指定安裝和設定 hello 代理程式時不正確</span><span class="sxs-lookup"><span data-stu-id="83ae6-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="83ae6-492">hello OMS 服務端點不是資料中心中 whitelistested</span><span class="sxs-lookup"><span data-stu-id="83ae6-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="83ae6-493">解決方式</span><span class="sxs-lookup"><span data-stu-id="83ae6-493">Resolutions</span></span>
* <span data-ttu-id="83ae6-494">重新 hello OMS 代理程式安裝適用於 Linux 使用下列命令以 hello 選項 hello`-v`啟用。</span><span class="sxs-lookup"><span data-stu-id="83ae6-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="83ae6-495">這可讓透過 hello proxy toohello OMS 服務的 hello 代理程式的詳細資訊輸出。</span><span class="sxs-lookup"><span data-stu-id="83ae6-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="83ae6-496">檢閱在 OMS proxy 的文件集 hello[用於 HTTP proxy 伺服器設定 hello 代理程式](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="83ae6-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="83ae6-497">請確認該 hello 遵循 OMS 服務端點會在允許清單</span><span class="sxs-lookup"><span data-stu-id="83ae6-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="83ae6-498">代理程式資源</span><span class="sxs-lookup"><span data-stu-id="83ae6-498">Agent Resource</span></span> | <span data-ttu-id="83ae6-499">連接埠</span><span class="sxs-lookup"><span data-stu-id="83ae6-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="83ae6-500">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="83ae6-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="83ae6-501">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="83ae6-501">Port 443</span></span> |
| <span data-ttu-id="83ae6-502">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="83ae6-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="83ae6-503">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="83ae6-503">Port 443</span></span> |
| <span data-ttu-id="83ae6-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="83ae6-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="83ae6-505">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="83ae6-505">Port 443</span></span> |
| <span data-ttu-id="83ae6-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="83ae6-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="83ae6-507">連接埠 443</span><span class="sxs-lookup"><span data-stu-id="83ae6-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="83ae6-508">上架時會顯示 403 錯誤</span><span class="sxs-lookup"><span data-stu-id="83ae6-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="83ae6-509">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83ae6-509">Probable causes</span></span>
* <span data-ttu-id="83ae6-510">hello 日期和時間設定不正確的 Linux 伺服器上</span><span class="sxs-lookup"><span data-stu-id="83ae6-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="83ae6-511">hello 工作區識別碼和使用的工作區金鑰不正確</span><span class="sxs-lookup"><span data-stu-id="83ae6-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="83ae6-512">解決方案</span><span class="sxs-lookup"><span data-stu-id="83ae6-512">Resolution</span></span>
* <span data-ttu-id="83ae6-513">驗證您的 Linux 伺服器 hello 與 hello 時間`date`命令。</span><span class="sxs-lookup"><span data-stu-id="83ae6-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="83ae6-514">Hello 資料大於或小於 15 分鐘從 hello 目前的時間，如果登入就會失敗。</span><span class="sxs-lookup"><span data-stu-id="83ae6-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="83ae6-515">toocorrect，更新 hello 日期及/或 Linux 伺服器的時區。</span><span class="sxs-lookup"><span data-stu-id="83ae6-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="83ae6-516">hello 最新版 hello OMS Agent for Linux 通知您，如果時間差異會造成登入失敗</span><span class="sxs-lookup"><span data-stu-id="83ae6-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="83ae6-517">重新登入使用 hello 正確的工作區識別碼和工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="83ae6-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="83ae6-518">請參閱[使用 hello 命令列的上架](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="83ae6-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="83ae6-519">500 錯誤或 404 錯誤會出現在 hello 記錄檔中登入之後</span><span class="sxs-lookup"><span data-stu-id="83ae6-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="83ae6-520">這是在 hello 第一次上傳 Linux 資料到 OMS 工作區時，就會發生的已知的問題。</span><span class="sxs-lookup"><span data-stu-id="83ae6-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="83ae6-521">這不會影響正在傳送的資料或其他問題。</span><span class="sxs-lookup"><span data-stu-id="83ae6-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="83ae6-522">您可以忽略 hello 錯誤，當第一次登入。</span><span class="sxs-lookup"><span data-stu-id="83ae6-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="83ae6-523">Nagios 資料不會出現在 hello OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="83ae6-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="83ae6-524">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83ae6-524">Probable causes</span></span>
* <span data-ttu-id="83ae6-525">hello omsagent 使用者不具有權限 tooread 從 hello Nagios 記錄檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="83ae6-526">hello Nagios 來源和篩選區段仍然註 hello omsagent.conf 檔案中</span><span class="sxs-lookup"><span data-stu-id="83ae6-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="83ae6-527">解決方式</span><span class="sxs-lookup"><span data-stu-id="83ae6-527">Resolutions</span></span>
* <span data-ttu-id="83ae6-528">加入從 hello Nagios 檔案順序 tooread hello omsagent 使用者。</span><span class="sxs-lookup"><span data-stu-id="83ae6-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="83ae6-529">如需詳細資訊，請參閱 [Nagios 警示](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="83ae6-530">在 hello OMS Agent for Linux 一般的組態檔， `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`，請確認**兩者**hello 的 Nagios 來源和篩選的區段有註解中移除，下列範例類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="83ae6-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="83ae6-531">Linux 資料不會出現在 hello OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="83ae6-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="83ae6-532">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83ae6-532">Probable causes</span></span>
* <span data-ttu-id="83ae6-533">上架 toohello OMS 服務失敗</span><span class="sxs-lookup"><span data-stu-id="83ae6-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="83ae6-534">OMS 服務會封鎖連接 toohello</span><span class="sxs-lookup"><span data-stu-id="83ae6-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="83ae6-535">hello OMS Agent for Linux 資料會備份</span><span class="sxs-lookup"><span data-stu-id="83ae6-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="83ae6-536">解決方式</span><span class="sxs-lookup"><span data-stu-id="83ae6-536">Resolutions</span></span>
* <span data-ttu-id="83ae6-537">確認該入門訓練 toohello OMS 服務已成功驗證該 hello`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`存在。</span><span class="sxs-lookup"><span data-stu-id="83ae6-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="83ae6-538">重新登入使用 hello omsadmin.sh 命令列。</span><span class="sxs-lookup"><span data-stu-id="83ae6-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="83ae6-539">請參閱[使用 hello 命令列的上架](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="83ae6-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="83ae6-540">如果使用 proxy，使用 hello proxy 疑難排解上述步驟</span><span class="sxs-lookup"><span data-stu-id="83ae6-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="83ae6-541">在某些情況下，hello 適用於 Linux 的 OMS 代理程式無法與 hello OMS 服務通訊時 hello 代理程式上的資料會是備份 toohello 已滿的緩衝區大小為 50 MB。</span><span class="sxs-lookup"><span data-stu-id="83ae6-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="83ae6-542">Hello OMS Agent for Linux 啟動執行重新啟動 hello`/opt/microsoft/omsagent/bin/service_control restart`命令。</span><span class="sxs-lookup"><span data-stu-id="83ae6-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="83ae6-543">此問題已在代理程式 1.1.0-28 版和更新版本中修正。</span><span class="sxs-lookup"><span data-stu-id="83ae6-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="83ae6-544">Syslog Linux 效能計數器組態不會套用在 hello OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="83ae6-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="83ae6-545">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83ae6-545">Probable causes</span></span>
* <span data-ttu-id="83ae6-546">在 hello OMS Agent for Linux hello 設定代理程式並未從 hello OMS 入口網站擷取 hello 最新的設定。</span><span class="sxs-lookup"><span data-stu-id="83ae6-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="83ae6-547">hello hello 入口網站中修改過的設定未套用</span><span class="sxs-lookup"><span data-stu-id="83ae6-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="83ae6-548">解決方式</span><span class="sxs-lookup"><span data-stu-id="83ae6-548">Resolutions</span></span>
<span data-ttu-id="83ae6-549">`omsconfig`是 hello 設定代理程式在 hello OMS Agent for Linux，擷取 OMS 入口網站的組態變更每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="83ae6-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="83ae6-550">此設定，然後套用的 toohello OMS Agent for Linux 設定檔位於`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`。</span><span class="sxs-lookup"><span data-stu-id="83ae6-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="83ae6-551">在某些情況下，hello OMS Agent for Linux 設定代理程式可能不能 toocommunicate 不套用最新的組態中所產生的 hello 入口網站設定服務。</span><span class="sxs-lookup"><span data-stu-id="83ae6-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="83ae6-552">請確認該 hello `omsconfig` hello 下列已安裝的代理程式：</span><span class="sxs-lookup"><span data-stu-id="83ae6-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="83ae6-553">`dpkg --list omsconfig` 或 `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="83ae6-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="83ae6-554">如果未安裝，重新安裝 hello 最新版 hello OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="83ae6-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="83ae6-555">請確認該 hello`omsconfig`代理程式可以與 hello OMS 服務通訊</span><span class="sxs-lookup"><span data-stu-id="83ae6-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="83ae6-556">執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`命令</span><span class="sxs-lookup"><span data-stu-id="83ae6-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="83ae6-557">hello 上述命令會傳回 hello 設定該代理程式擷取 hello 入口網站，包括 Syslog 設定、 Linux 效能計數器，以及自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="83ae6-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="83ae6-558">如果上述 hello 命令失敗，執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`命令。</span><span class="sxs-lookup"><span data-stu-id="83ae6-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="83ae6-559">此命令會強制 hello omsconfig 代理程式 toocommunicate 與 hello OMS 服務 tooretrieve hello 最新組態。</span><span class="sxs-lookup"><span data-stu-id="83ae6-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="83ae6-560">自訂的 Linux 記錄檔資料不會出現在 hello OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="83ae6-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="83ae6-561">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83ae6-561">Probable causes</span></span>
* <span data-ttu-id="83ae6-562">上架 tooOMS 服務失敗</span><span class="sxs-lookup"><span data-stu-id="83ae6-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="83ae6-563">hello**套用下列組態 toomy Linux 伺服器的 hello**不選取設定</span><span class="sxs-lookup"><span data-stu-id="83ae6-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="83ae6-564">omsconfig 不挑選 hello 最新自訂的記錄從 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="83ae6-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="83ae6-565">hello`omsagent`使用已到期，tooa 權限問題無法 tooaccess hello 自訂記錄或`omsagent`找不到。</span><span class="sxs-lookup"><span data-stu-id="83ae6-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="83ae6-566">在此情況下，您會看到下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="83ae6-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="83ae6-567">這是以 hello 競爭 hello OMS Agent for Linux 版本 1.1.0-217 中已修正的已知的問題</span><span class="sxs-lookup"><span data-stu-id="83ae6-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="83ae6-568">解決方式</span><span class="sxs-lookup"><span data-stu-id="83ae6-568">Resolutions</span></span>
* <span data-ttu-id="83ae6-569">請確認您已順利就緒、 判斷是否 hello`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`檔案是否存在。</span><span class="sxs-lookup"><span data-stu-id="83ae6-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="83ae6-570">必要時，使用 hello omsadmin.sh 命令列再次登入。</span><span class="sxs-lookup"><span data-stu-id="83ae6-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="83ae6-571">請參閱[使用 hello 命令列的上架](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="83ae6-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="83ae6-572">在 hello OMS 入口網站，在**設定**上 hello**資料**索引標籤，確定該 hello**套用下列組態 toomy Linux 伺服器的 hello**選取設定</span><span class="sxs-lookup"><span data-stu-id="83ae6-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="83ae6-573">![套用組態](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="83ae6-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="83ae6-574">請確認該 hello`omsconfig`代理程式可以與 hello OMS 服務通訊</span><span class="sxs-lookup"><span data-stu-id="83ae6-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="83ae6-575">執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`命令</span><span class="sxs-lookup"><span data-stu-id="83ae6-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="83ae6-576">hello 上述命令會傳回 hello 設定該代理程式從 hello 入口網站，包括 Syslog 設定、 Linux 效能計數器，以及自訂記錄檔中的擷取</span><span class="sxs-lookup"><span data-stu-id="83ae6-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="83ae6-577">如果上述 hello 命令失敗，執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`命令。</span><span class="sxs-lookup"><span data-stu-id="83ae6-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="83ae6-578">此命令會強制 hello omsconfig 代理程式 toocommunicate 與 OMS 服務，並擷取 hello 最新的設定。</span><span class="sxs-lookup"><span data-stu-id="83ae6-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="83ae6-579">而不是 hello OMS Agent for Linux 使用者的特殊權限的使用者身分執行`root`，hello OMS Agent for Linux 執行 hello`omsagent`使用者。</span><span class="sxs-lookup"><span data-stu-id="83ae6-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="83ae6-580">在大部分情況下，必須明確權限授與順序 tooread toohello 使用者特定的檔案。</span><span class="sxs-lookup"><span data-stu-id="83ae6-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="83ae6-581">toogrant 權限太`omsagent`使用者，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="83ae6-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="83ae6-582">新增 hello`omsagent`使用者 tooa 特定群組`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="83ae6-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="83ae6-583">授與具有通用的讀取權限 toohello 必要的檔案`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="83ae6-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="83ae6-584">沒有 hello 競爭 hello OMS Agent for Linux 版本 1.1.0-217 中已修正的已知的問題。</span><span class="sxs-lookup"><span data-stu-id="83ae6-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="83ae6-585">在更新之後 toohello 最新的代理程式，執行下列命令 tooget hello 最新版本的 hello 輸出外掛程式 hello:</span><span class="sxs-lookup"><span data-stu-id="83ae6-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="83ae6-586">已知限制</span><span class="sxs-lookup"><span data-stu-id="83ae6-586">Known limitations</span></span>
<span data-ttu-id="83ae6-587">請檢閱下列有關目前限制的 hello OMS Agent for Linux 區段 toolearn hello。</span><span class="sxs-lookup"><span data-stu-id="83ae6-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="83ae6-588">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="83ae6-588">Azure Diagnostics</span></span>
<span data-ttu-id="83ae6-589">在 Azure 中執行的 Linux 虛擬機器，額外的步驟可能需要的 tooallow 資料收集 Azure 診斷和 Operations Management Suite 的資訊。</span><span class="sxs-lookup"><span data-stu-id="83ae6-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="83ae6-590">**2.2 版**的 hello Diagnostics Extension for Linux 做是為了與 hello OMS Agent for Linux 相容性。</span><span class="sxs-lookup"><span data-stu-id="83ae6-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="83ae6-591">如需有關安裝和設定適用於 Linux 的 hello 診斷延伸模組的詳細資訊，請參閱[使用 hello Azure CLI 命令 tooenable Linux 診斷延伸模組](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="83ae6-592">**升級 hello Linux 診斷延伸模組從 2.0 too2.2 Azure CLI ASM:**</span><span class="sxs-lookup"><span data-stu-id="83ae6-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="83ae6-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="83ae6-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="83ae6-594">這些命令範例參考名為 PrivateConfig.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="83ae6-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="83ae6-595">hello 該檔案格式應該類似下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="83ae6-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="83ae6-596">不支援 Sysklog</span><span class="sxs-lookup"><span data-stu-id="83ae6-596">Sysklog is not supported</span></span>
<span data-ttu-id="83ae6-597">需要 rsyslog 或 syslog-ng 是必要的 toocollect syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="83ae6-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="83ae6-598">在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。</span><span class="sxs-lookup"><span data-stu-id="83ae6-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="83ae6-599">toocollect syslog 資料，從這一版的這些發佈，hello rsyslog 精靈應該安裝和設定 tooreplace sysklog。</span><span class="sxs-lookup"><span data-stu-id="83ae6-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="83ae6-600">如需有關以 rsyslog 取代 sysklog 的詳細資訊，請參閱[安裝 hello 新建立的 rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM)。</span><span class="sxs-lookup"><span data-stu-id="83ae6-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83ae6-601">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83ae6-601">Next Steps</span></span>
* <span data-ttu-id="83ae6-602">[新增記錄分析解決方案從 hello 解決方案資源庫](log-analytics-add-solutions.md)tooadd 功能和收集資料。</span><span class="sxs-lookup"><span data-stu-id="83ae6-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="83ae6-603">讓您熟悉[記錄搜尋](log-analytics-log-searches.md)tooview 詳細解決方案所收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="83ae6-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="83ae6-604">使用[儀表板](log-analytics-dashboards.md)toosave 並顯示您自己的自訂搜尋。</span><span class="sxs-lookup"><span data-stu-id="83ae6-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
