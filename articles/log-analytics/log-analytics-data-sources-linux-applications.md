---
title: "在 OMS Log Analytics 中收集 Linux 應用程式效能 | Microsoft Docs"
description: "本文詳細說明如何設定 OMS Agent for Linux，以收集 MySQL 和 Apache HTTP Server 的效能計數器。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 04ea6f728e59ec8b47e54fe45e1adc6cbbfb85ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a><span data-ttu-id="3ed16-103">在 Log Analytics 中收集 Linux 應用程式的效能計數器</span><span class="sxs-lookup"><span data-stu-id="3ed16-103">Collect performance counters for Linux applications in Log Analytics</span></span> 
<span data-ttu-id="3ed16-104">本文詳細說明如何設定 [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux)，以收集特定應用程式的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="3ed16-104">This article provides details for configuring the [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) to collect performance counters for specific applications.</span></span>  <span data-ttu-id="3ed16-105">本文包含的應用程式如下︰</span><span class="sxs-lookup"><span data-stu-id="3ed16-105">The applications included in this article are:</span></span>  

- [<span data-ttu-id="3ed16-106">MySQL</span><span class="sxs-lookup"><span data-stu-id="3ed16-106">MySQL</span></span>](#MySQL)
- [<span data-ttu-id="3ed16-107">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-107">Apache HTTP Server</span></span>](#apache-http-server)

## <a name="mysql"></a><span data-ttu-id="3ed16-108">MySQL</span><span class="sxs-lookup"><span data-stu-id="3ed16-108">MySQL</span></span>
<span data-ttu-id="3ed16-109">如果在安裝 OMS 代理程式時於電腦上偵測到 MySQL 伺服器或 MariaDB 伺服器，則會自動安裝 MySQL 伺服器的效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="3ed16-109">If MySQL Server or MariaDB Server is detected on the computer when the OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span></span> <span data-ttu-id="3ed16-110">此提供者會連接到本機 MySQL/MariaDB 伺服器，以公開效能統計資料。</span><span class="sxs-lookup"><span data-stu-id="3ed16-110">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="3ed16-111">必須設定 MySQL 使用者認證，提供者才能存取 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3ed16-111">MySQL user credentials must be configured so that the provider can access the MySQL Server.</span></span>

### <a name="configure-mysql-credentials"></a><span data-ttu-id="3ed16-112">設定 MySQL 認證</span><span class="sxs-lookup"><span data-stu-id="3ed16-112">Configure MySQL credentials</span></span>
<span data-ttu-id="3ed16-113">MySQL OMI 提供者需要預先設定的 MySQL 使用者，並已安裝 MySQL 用戶端程式庫，才能從 MySQL 執行個體查詢效能和健康情況資訊。</span><span class="sxs-lookup"><span data-stu-id="3ed16-113">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance and health information from the MySQL instance.</span></span>  <span data-ttu-id="3ed16-114">這些認證儲存在 Linux 代理程式上的驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="3ed16-114">These credentials are stored in an authentication file that's stored on the Linux agent.</span></span>  <span data-ttu-id="3ed16-115">驗證檔案指定 MySQL 執行個體所接聽的繫結位址和連接埠，以及要用來收集計量的認證。</span><span class="sxs-lookup"><span data-stu-id="3ed16-115">The authentication file specifies what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span>  

<span data-ttu-id="3ed16-116">在 OMS Agent for Linux 安裝期間，MySQL OMI 提供者將掃描繫結位址和連接埠的 MySQL my.cnf 組態檔 (預設位置)，並局部設定 MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="3ed16-116">During installation of the OMS Agent for Linux the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="3ed16-117">MySQL 驗證檔案儲存在 `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`。</span><span class="sxs-lookup"><span data-stu-id="3ed16-117">The MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span></span>


### <a name="authentication-file-format"></a><span data-ttu-id="3ed16-118">驗證檔案格式</span><span class="sxs-lookup"><span data-stu-id="3ed16-118">Authentication file format</span></span>
<span data-ttu-id="3ed16-119">以下是 MySQL OMI 驗證檔案的格式</span><span class="sxs-lookup"><span data-stu-id="3ed16-119">Following is the format for the MySQL OMI authentication file</span></span>

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

<span data-ttu-id="3ed16-120">下表說明驗證檔案中的項目。</span><span class="sxs-lookup"><span data-stu-id="3ed16-120">The entries in the authentication file are described in the following table.</span></span>

| <span data-ttu-id="3ed16-121">屬性</span><span class="sxs-lookup"><span data-stu-id="3ed16-121">Property</span></span> | <span data-ttu-id="3ed16-122">說明</span><span class="sxs-lookup"><span data-stu-id="3ed16-122">Description</span></span> |
|:--|:--|
| <span data-ttu-id="3ed16-123">連接埠</span><span class="sxs-lookup"><span data-stu-id="3ed16-123">Port</span></span> | <span data-ttu-id="3ed16-124">代表 MySQL 執行個體目前正在接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="3ed16-124">Represents the current port the MySQL instance is listening on.</span></span> <span data-ttu-id="3ed16-125">連接埠 0 指定後面的屬性用於預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-125">Port 0 specifies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="3ed16-126">繫結位址</span><span class="sxs-lookup"><span data-stu-id="3ed16-126">Bind-Address</span></span>| <span data-ttu-id="3ed16-127">目前的 MySQL 繫結位址。</span><span class="sxs-lookup"><span data-stu-id="3ed16-127">Current MySQL bind-address.</span></span> |
| <span data-ttu-id="3ed16-128">username</span><span class="sxs-lookup"><span data-stu-id="3ed16-128">username</span></span>| <span data-ttu-id="3ed16-129">用來監視 MySQL 伺服器執行個體的 MySQL 使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed16-129">MySQL user used to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="3ed16-130">Base64 編碼的密碼</span><span class="sxs-lookup"><span data-stu-id="3ed16-130">Base64 encoded Password</span></span>| <span data-ttu-id="3ed16-131">MySQL 監視使用者的密碼，以 Base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="3ed16-131">Password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="3ed16-132">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="3ed16-132">AutoUpdate</span></span>| <span data-ttu-id="3ed16-133">指定在升級 MySQL OMI 提供者時，是否重新掃描 my.cnf 檔案中的變更，並覆寫 MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="3ed16-133">Specifies whether to rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file when the MySQL OMI Provider is upgraded.</span></span> |

### <a name="default-instance"></a><span data-ttu-id="3ed16-134">預設執行個體</span><span class="sxs-lookup"><span data-stu-id="3ed16-134">Default instance</span></span>
<span data-ttu-id="3ed16-135">MySQL OMI 驗證檔案可以定義預設執行個體和連接埠號碼，讓您更輕鬆地管理一台 Linux 主機上的多個 MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-135">The MySQL OMI authentication file can define a default instance and port number to make managing multiple MySQL instances on one Linux host easier.</span></span>  <span data-ttu-id="3ed16-136">連接埠為 0 的執行個體代表預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-136">The default instance is denoted by an instance with port 0.</span></span> <span data-ttu-id="3ed16-137">所有其他執行個體除非指定不同的值，否則會繼承預設執行個體的屬性集。</span><span class="sxs-lookup"><span data-stu-id="3ed16-137">All additional instances will inherit properties set from the default instance unless they specify different values.</span></span> <span data-ttu-id="3ed16-138">例如，如果加入接聽通訊埠 '3308' 的 MySQL 執行個體，預設執行個體的繫結位址、使用者名稱和 Base64 編碼的密碼將會用來嘗試和監視接聽 3308 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-138">For example, if MySQL instance listening on port ‘3308’ is added, the default instance’s bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="3ed16-139">如果 3308 上的執行個體繫結至另一個位址，並使用相同的 MySQL 使用者名稱和密碼配對，則只需要繫結位址，其他屬性會繼承而來。</span><span class="sxs-lookup"><span data-stu-id="3ed16-139">If the instance on 3308 is bound to another address and uses the same MySQL username and password pair only the bind-address is needed, and the other properties will be inherited.</span></span>

<span data-ttu-id="3ed16-140">下表提供執行個體設定範例</span><span class="sxs-lookup"><span data-stu-id="3ed16-140">The following table has example instance settings</span></span> 

| <span data-ttu-id="3ed16-141">說明</span><span class="sxs-lookup"><span data-stu-id="3ed16-141">Description</span></span> | <span data-ttu-id="3ed16-142">檔案</span><span class="sxs-lookup"><span data-stu-id="3ed16-142">File</span></span> |
|:--|:--|
| <span data-ttu-id="3ed16-143">預設執行個體和連接埠為 3308 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-143">Default instance and instance with port 3308.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| <span data-ttu-id="3ed16-144">預設執行個體，以及連接埠為 3308 且具有不同使用者名稱密碼的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-144">Default instance and instance with port 3308 and different user name and password.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a><span data-ttu-id="3ed16-145">MySQL OMI 驗證檔案程式</span><span class="sxs-lookup"><span data-stu-id="3ed16-145">MySQL OMI Authentication File Program</span></span>
<span data-ttu-id="3ed16-146">安裝 MySQL OMI 提供者時會隨附 MySQL OMI 驗證檔案程式，可用來編輯 MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="3ed16-146">Included with the installation of the MySQL OMI provider is a MySQL OMI authentication file program which can be used to edit the MySQL OMI Authentication file.</span></span> <span data-ttu-id="3ed16-147">驗證檔案程式位於下列位置。</span><span class="sxs-lookup"><span data-stu-id="3ed16-147">The authentication file program can be found at the following location.</span></span>

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> <span data-ttu-id="3ed16-148">omsagent 帳戶必須可讀取認證檔案。</span><span class="sxs-lookup"><span data-stu-id="3ed16-148">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="3ed16-149">建議以 omsgent 身分執行 mycimprovauth 命令。</span><span class="sxs-lookup"><span data-stu-id="3ed16-149">Running the mycimprovauth command as omsgent is recommended.</span></span>

<span data-ttu-id="3ed16-150">下表提供使用 mycimprovauth 語法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3ed16-150">The following table provides details on the syntax for using mycimprovauth.</span></span>

| <span data-ttu-id="3ed16-151">作業</span><span class="sxs-lookup"><span data-stu-id="3ed16-151">Operation</span></span> | <span data-ttu-id="3ed16-152">範例</span><span class="sxs-lookup"><span data-stu-id="3ed16-152">Example</span></span> | <span data-ttu-id="3ed16-153">說明</span><span class="sxs-lookup"><span data-stu-id="3ed16-153">Description</span></span>
|:--|:--|:--|
| <span data-ttu-id="3ed16-154">autoupdate *false\\</span><span class="sxs-lookup"><span data-stu-id="3ed16-154">autoupdate *false\\</span></span>|<span data-ttu-id="3ed16-155">true*</span><span class="sxs-lookup"><span data-stu-id="3ed16-155">true*</span></span> | <span data-ttu-id="3ed16-156">mycimprovauth autoupdate false</span><span class="sxs-lookup"><span data-stu-id="3ed16-156">mycimprovauth autoupdate false</span></span> | <span data-ttu-id="3ed16-157">設定是否在重新啟動或更新時自動更新驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="3ed16-157">Sets whether or not the authentication file will be automatically updated on restart or update.</span></span> |
| <span data-ttu-id="3ed16-158">default *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="3ed16-158">default *bind-address username password*</span></span> | <span data-ttu-id="3ed16-159">mycimprovauth default 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="3ed16-159">mycimprovauth default 127.0.0.1 root pwd</span></span> | <span data-ttu-id="3ed16-160">在 MySQL OMI 驗證檔案中設定預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-160">Sets the default instance in the MySQL OMI authentication file.</span></span><br><span data-ttu-id="3ed16-161">應以純文字輸入 password 欄位 - MySQL OMI 驗證檔案中的密碼將會以 Base 64 編碼。</span><span class="sxs-lookup"><span data-stu-id="3ed16-161">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded.</span></span> |
| <span data-ttu-id="3ed16-162">delete *default\\</span><span class="sxs-lookup"><span data-stu-id="3ed16-162">delete *default\\</span></span>|<span data-ttu-id="3ed16-163">port_num*</span><span class="sxs-lookup"><span data-stu-id="3ed16-163">port_num*</span></span> | <span data-ttu-id="3ed16-164">mycimprovauth 3308</span><span class="sxs-lookup"><span data-stu-id="3ed16-164">mycimprovauth 3308</span></span> | <span data-ttu-id="3ed16-165">依預設值或依連接埠號碼刪除指定的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-165">Deletes the specified instance by either default or by port number.</span></span> |
| <span data-ttu-id="3ed16-166">help</span><span class="sxs-lookup"><span data-stu-id="3ed16-166">help</span></span> | <span data-ttu-id="3ed16-167">mycimprov help</span><span class="sxs-lookup"><span data-stu-id="3ed16-167">mycimprov help</span></span> | <span data-ttu-id="3ed16-168">印出可使用的命令清單。</span><span class="sxs-lookup"><span data-stu-id="3ed16-168">Prints out a list of commands to use.</span></span> |
| <span data-ttu-id="3ed16-169">print</span><span class="sxs-lookup"><span data-stu-id="3ed16-169">print</span></span> | <span data-ttu-id="3ed16-170">mycimprov print</span><span class="sxs-lookup"><span data-stu-id="3ed16-170">mycimprov print</span></span> | <span data-ttu-id="3ed16-171">印出方便閱讀的 MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="3ed16-171">Prints out an easy to read MySQL OMI authentication file.</span></span> |
| <span data-ttu-id="3ed16-172">update port_num *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="3ed16-172">update port_num *bind-address username password*</span></span> | <span data-ttu-id="3ed16-173">mycimprov update 3307 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="3ed16-173">mycimprov update 3307 127.0.0.1 root pwd</span></span> | <span data-ttu-id="3ed16-174">更新指定的執行個體，而如果不存在，則新增執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ed16-174">Updates the specified instance or adds the instance if it does not exist.</span></span> |

<span data-ttu-id="3ed16-175">下列命令範例會為 localhost 上的 MySQL 伺服器定義預設使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ed16-175">The following example commands define a default user account for the MySQL server on localhost.</span></span>  <span data-ttu-id="3ed16-176">應以純文字輸入 password 欄位 - MySQL OMI 驗證檔案中的密碼將會以 Base 64 編碼</span><span class="sxs-lookup"><span data-stu-id="3ed16-176">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded</span></span>

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="3ed16-177">MySQL 效能計數器所需的資料庫權限</span><span class="sxs-lookup"><span data-stu-id="3ed16-177">Database Permissions Required for MySQL Performance Counters</span></span>
<span data-ttu-id="3ed16-178">MySQL 使用者需要存取下列查詢，才能收集 MySQL 伺服器的效能資料。</span><span class="sxs-lookup"><span data-stu-id="3ed16-178">The MySQL User requires access to the following queries to collect MySQL Server performance data.</span></span> 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


<span data-ttu-id="3ed16-179">MySQL 使用者需要下列預設資料表的 SELECT 存取權。</span><span class="sxs-lookup"><span data-stu-id="3ed16-179">The MySQL user also requires SELECT access to the following default tables.</span></span>

- <span data-ttu-id="3ed16-180">information_schema</span><span class="sxs-lookup"><span data-stu-id="3ed16-180">information_schema</span></span>
- <span data-ttu-id="3ed16-181">mysql。</span><span class="sxs-lookup"><span data-stu-id="3ed16-181">mysql.</span></span> 

<span data-ttu-id="3ed16-182">執行下列 grant 命令，可以授與這些權限。</span><span class="sxs-lookup"><span data-stu-id="3ed16-182">These privileges can be granted by running the following grant commands.</span></span>

    GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;


> [!NOTE]
> <span data-ttu-id="3ed16-183">若要將權限授與 MySQL 監視使用者，則授與使用者必須具有 'GRANT option' 權限以及正在授與的權限。</span><span class="sxs-lookup"><span data-stu-id="3ed16-183">To grant permissions to a MySQL monitoring user the granting user must have the ‘GRANT option’ privilege as well as the privilege being granted.</span></span>

### <a name="define-performance-counters"></a><span data-ttu-id="3ed16-184">定義效能計數器</span><span class="sxs-lookup"><span data-stu-id="3ed16-184">Define performance counters</span></span>

<span data-ttu-id="3ed16-185">設定 OMS Agent for Linux 將資料傳送至 Log Analytics 之後，您必須設定要收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="3ed16-185">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="3ed16-186">使用 [Log Analytics 中的 Windows 和 Linux 效能資料來源](log-analytics-data-sources-windows-events.md)中的程序與下表中的計數器。</span><span class="sxs-lookup"><span data-stu-id="3ed16-186">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="3ed16-187">物件名稱</span><span class="sxs-lookup"><span data-stu-id="3ed16-187">Object Name</span></span> | <span data-ttu-id="3ed16-188">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="3ed16-188">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="3ed16-189">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="3ed16-189">MySQL Database</span></span> | <span data-ttu-id="3ed16-190">Disk Space in Bytes</span><span class="sxs-lookup"><span data-stu-id="3ed16-190">Disk Space in Bytes</span></span> |
| <span data-ttu-id="3ed16-191">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="3ed16-191">MySQL Database</span></span> | <span data-ttu-id="3ed16-192">資料表</span><span class="sxs-lookup"><span data-stu-id="3ed16-192">Tables</span></span> |
| <span data-ttu-id="3ed16-193">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-193">MySQL Server</span></span> | <span data-ttu-id="3ed16-194">Aborted Connection Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-194">Aborted Connection Pct</span></span> |
| <span data-ttu-id="3ed16-195">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-195">MySQL Server</span></span> | <span data-ttu-id="3ed16-196">Connection Use Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-196">Connection Use Pct</span></span> |
| <span data-ttu-id="3ed16-197">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-197">MySQL Server</span></span> | <span data-ttu-id="3ed16-198">Disk Space in Bytes</span><span class="sxs-lookup"><span data-stu-id="3ed16-198">Disk Space Use in Bytes</span></span> |
| <span data-ttu-id="3ed16-199">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-199">MySQL Server</span></span> | <span data-ttu-id="3ed16-200">Full Table Scan Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-200">Full Table Scan Pct</span></span> |
| <span data-ttu-id="3ed16-201">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-201">MySQL Server</span></span> | <span data-ttu-id="3ed16-202">InnoDB Buffer Pool Hit Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-202">InnoDB Buffer Pool Hit Pct</span></span> |
| <span data-ttu-id="3ed16-203">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-203">MySQL Server</span></span> | <span data-ttu-id="3ed16-204">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-204">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="3ed16-205">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-205">MySQL Server</span></span> | <span data-ttu-id="3ed16-206">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-206">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="3ed16-207">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-207">MySQL Server</span></span> | <span data-ttu-id="3ed16-208">Key Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-208">Key Cache Hit Pct</span></span> |
| <span data-ttu-id="3ed16-209">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-209">MySQL Server</span></span> | <span data-ttu-id="3ed16-210">Key Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-210">Key Cache Use Pct</span></span> |
| <span data-ttu-id="3ed16-211">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-211">MySQL Server</span></span> | <span data-ttu-id="3ed16-212">Key Cache Write Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-212">Key Cache Write Pct</span></span> |
| <span data-ttu-id="3ed16-213">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-213">MySQL Server</span></span> | <span data-ttu-id="3ed16-214">Query Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-214">Query Cache Hit Pct</span></span> |
| <span data-ttu-id="3ed16-215">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-215">MySQL Server</span></span> | <span data-ttu-id="3ed16-216">Query Cache Prunes Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-216">Query Cache Prunes Pct</span></span> |
| <span data-ttu-id="3ed16-217">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-217">MySQL Server</span></span> | <span data-ttu-id="3ed16-218">Query Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-218">Query Cache Use Pct</span></span> |
| <span data-ttu-id="3ed16-219">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-219">MySQL Server</span></span> | <span data-ttu-id="3ed16-220">Table Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-220">Table Cache Hit Pct</span></span> |
| <span data-ttu-id="3ed16-221">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-221">MySQL Server</span></span> | <span data-ttu-id="3ed16-222">Table Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-222">Table Cache Use Pct</span></span> |
| <span data-ttu-id="3ed16-223">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-223">MySQL Server</span></span> | <span data-ttu-id="3ed16-224">Table Lock Contention Pct</span><span class="sxs-lookup"><span data-stu-id="3ed16-224">Table Lock Contention Pct</span></span> |

## <a name="apache-http-server"></a><span data-ttu-id="3ed16-225">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-225">Apache HTTP Server</span></span> 
<span data-ttu-id="3ed16-226">如果在安裝 omsagent 組合時於電腦上偵測到 Apache HTTP Server，則會自動安裝 Apache HTTP Server 的效能監視提供者。</span><span class="sxs-lookup"><span data-stu-id="3ed16-226">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span></span> <span data-ttu-id="3ed16-227">此提供者所依賴的 Apache 模組必須載入至 Apache HTTP Server，才能存取效能資料。</span><span class="sxs-lookup"><span data-stu-id="3ed16-227">This provider relies on an Apache module that must be loaded into the Apache HTTP Server in order to access performance data.</span></span> <span data-ttu-id="3ed16-228">您可以使用下列命令載入此模組：</span><span class="sxs-lookup"><span data-stu-id="3ed16-228">The module can be loaded with the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="3ed16-229">若要卸載 Apache 監視模組，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="3ed16-229">To unload the Apache monitoring module, run the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a><span data-ttu-id="3ed16-230">定義效能計數器</span><span class="sxs-lookup"><span data-stu-id="3ed16-230">Define performance counters</span></span>

<span data-ttu-id="3ed16-231">設定 OMS Agent for Linux 將資料傳送至 Log Analytics 之後，您必須設定要收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="3ed16-231">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="3ed16-232">使用 [Log Analytics 中的 Windows 和 Linux 效能資料來源](log-analytics-data-sources-windows-events.md)中的程序與下表中的計數器。</span><span class="sxs-lookup"><span data-stu-id="3ed16-232">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="3ed16-233">物件名稱</span><span class="sxs-lookup"><span data-stu-id="3ed16-233">Object Name</span></span> | <span data-ttu-id="3ed16-234">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="3ed16-234">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="3ed16-235">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-235">Apache HTTP Server</span></span> | <span data-ttu-id="3ed16-236">Busy Workers</span><span class="sxs-lookup"><span data-stu-id="3ed16-236">Busy Workers</span></span> |
| <span data-ttu-id="3ed16-237">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-237">Apache HTTP Server</span></span> | <span data-ttu-id="3ed16-238">Idle Workers</span><span class="sxs-lookup"><span data-stu-id="3ed16-238">Idle Workers</span></span> |
| <span data-ttu-id="3ed16-239">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-239">Apache HTTP Server</span></span> | <span data-ttu-id="3ed16-240">Pct Busy Workers</span><span class="sxs-lookup"><span data-stu-id="3ed16-240">Pct Busy Workers</span></span> |
| <span data-ttu-id="3ed16-241">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-241">Apache HTTP Server</span></span> | <span data-ttu-id="3ed16-242">Total Pct CPU</span><span class="sxs-lookup"><span data-stu-id="3ed16-242">Total Pct CPU</span></span> |
| <span data-ttu-id="3ed16-243">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="3ed16-243">Apache Virtual Host</span></span> | <span data-ttu-id="3ed16-244">Errors per Minute - Client</span><span class="sxs-lookup"><span data-stu-id="3ed16-244">Errors per Minute - Client</span></span> |
| <span data-ttu-id="3ed16-245">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="3ed16-245">Apache Virtual Host</span></span> | <span data-ttu-id="3ed16-246">Errors per Minute - Server</span><span class="sxs-lookup"><span data-stu-id="3ed16-246">Errors per Minute - Server</span></span> |
| <span data-ttu-id="3ed16-247">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="3ed16-247">Apache Virtual Host</span></span> | <span data-ttu-id="3ed16-248">KB per Request</span><span class="sxs-lookup"><span data-stu-id="3ed16-248">KB per Request</span></span> |
| <span data-ttu-id="3ed16-249">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="3ed16-249">Apache Virtual Host</span></span> | <span data-ttu-id="3ed16-250">Requests KB per Second</span><span class="sxs-lookup"><span data-stu-id="3ed16-250">Requests KB per Second</span></span> |
| <span data-ttu-id="3ed16-251">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="3ed16-251">Apache Virtual Host</span></span> | <span data-ttu-id="3ed16-252">Requests per Second</span><span class="sxs-lookup"><span data-stu-id="3ed16-252">Requests per Second</span></span> |



## <a name="next-steps"></a><span data-ttu-id="3ed16-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ed16-253">Next steps</span></span>
* <span data-ttu-id="3ed16-254">從 Linux 代理程式[收集效能計數器](log-analytics-data-sources-performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="3ed16-254">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span></span>
* <span data-ttu-id="3ed16-255">了解 [記錄搜尋](log-analytics-log-searches.md) ，其可分析從資料來源和方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="3ed16-255">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 