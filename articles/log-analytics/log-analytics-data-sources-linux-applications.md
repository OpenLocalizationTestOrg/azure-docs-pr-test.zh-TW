---
title: "Linux 的 OMS 記錄分析的應用程式效能 aaaCollect |Microsoft 文件"
description: "這篇文章提供設定 MySQL 和 Apache HTTP Server hello OMS Agent for Linux toocollect 效能計數器的詳細資料。"
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
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a><span data-ttu-id="ddabb-103">在 Log Analytics 中收集 Linux 應用程式的效能計數器</span><span class="sxs-lookup"><span data-stu-id="ddabb-103">Collect performance counters for Linux applications in Log Analytics</span></span> 
<span data-ttu-id="ddabb-104">這篇文章詳細說明如何設定 hello [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect 特定應用程式的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="ddabb-104">This article provides details for configuring hello [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect performance counters for specific applications.</span></span>  <span data-ttu-id="ddabb-105">在本文中包含的 hello 應用程式可以：</span><span class="sxs-lookup"><span data-stu-id="ddabb-105">hello applications included in this article are:</span></span>  

- [<span data-ttu-id="ddabb-106">MySQL</span><span class="sxs-lookup"><span data-stu-id="ddabb-106">MySQL</span></span>](#MySQL)
- [<span data-ttu-id="ddabb-107">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-107">Apache HTTP Server</span></span>](#apache-http-server)

## <a name="mysql"></a><span data-ttu-id="ddabb-108">MySQL</span><span class="sxs-lookup"><span data-stu-id="ddabb-108">MySQL</span></span>
<span data-ttu-id="ddabb-109">如果 MySQL 伺服器或 MariaDB 伺服器是電腦上偵測到 hello hello OMS 代理程式安裝時，會自動安裝的效能監視提供者的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ddabb-109">If MySQL Server or MariaDB Server is detected on hello computer when hello OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span></span> <span data-ttu-id="ddabb-110">此提供者連接 toohello 本機 MySQL/MariaDB 伺服器 tooexpose 效能統計資料。</span><span class="sxs-lookup"><span data-stu-id="ddabb-110">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="ddabb-111">必須設定 MySQL 使用者認證，如此 hello 者可以存取 MySQL 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="ddabb-111">MySQL user credentials must be configured so that hello provider can access hello MySQL Server.</span></span>

### <a name="configure-mysql-credentials"></a><span data-ttu-id="ddabb-112">設定 MySQL 認證</span><span class="sxs-lookup"><span data-stu-id="ddabb-112">Configure MySQL credentials</span></span>
<span data-ttu-id="ddabb-113">hello MySQL OMI 提供者需要預先設定的 MySQL 使用者，並安裝 MySQL 用戶端程式庫中順序 tooquery hello 效能和健全狀況資訊從 hello MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-113">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance and health information from hello MySQL instance.</span></span>  <span data-ttu-id="ddabb-114">這些認證會儲存在儲存在 hello Linux 代理程式的驗證檔案中。</span><span class="sxs-lookup"><span data-stu-id="ddabb-114">These credentials are stored in an authentication file that's stored on hello Linux agent.</span></span>  <span data-ttu-id="ddabb-115">hello 驗證檔案會指定哪些繫結位址和連接埠 hello MySQL 執行個體正在接聽，以及認證 toouse toogather 度量。</span><span class="sxs-lookup"><span data-stu-id="ddabb-115">hello authentication file specifies what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span>  

<span data-ttu-id="ddabb-116">在安裝 hello OMS Agent for Linux hello MySQL OMI 提供者會掃描 MySQL my.cnf 組態檔 （預設位置） 繫結位址和連接埠和部分組 hello MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="ddabb-116">During installation of hello OMS Agent for Linux hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="ddabb-117">hello MySQL 驗證檔案會儲存在`/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`。</span><span class="sxs-lookup"><span data-stu-id="ddabb-117">hello MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span></span>


### <a name="authentication-file-format"></a><span data-ttu-id="ddabb-118">驗證檔案格式</span><span class="sxs-lookup"><span data-stu-id="ddabb-118">Authentication file format</span></span>
<span data-ttu-id="ddabb-119">以下是 hello hello MySQL OMI 驗證檔案格式</span><span class="sxs-lookup"><span data-stu-id="ddabb-119">Following is hello format for hello MySQL OMI authentication file</span></span>

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

<span data-ttu-id="ddabb-120">下表中的 hello 說明 hello 驗證檔案中的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="ddabb-120">hello entries in hello authentication file are described in hello following table.</span></span>

| <span data-ttu-id="ddabb-121">屬性</span><span class="sxs-lookup"><span data-stu-id="ddabb-121">Property</span></span> | <span data-ttu-id="ddabb-122">說明</span><span class="sxs-lookup"><span data-stu-id="ddabb-122">Description</span></span> |
|:--|:--|
| <span data-ttu-id="ddabb-123">Port</span><span class="sxs-lookup"><span data-stu-id="ddabb-123">Port</span></span> | <span data-ttu-id="ddabb-124">表示目前的連接埠 hello hello MySQL 執行個體正在接聽。</span><span class="sxs-lookup"><span data-stu-id="ddabb-124">Represents hello current port hello MySQL instance is listening on.</span></span> <span data-ttu-id="ddabb-125">連接埠 0 會指定下列的 hello 屬性會用於預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-125">Port 0 specifies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="ddabb-126">繫結位址</span><span class="sxs-lookup"><span data-stu-id="ddabb-126">Bind-Address</span></span>| <span data-ttu-id="ddabb-127">目前的 MySQL 繫結位址。</span><span class="sxs-lookup"><span data-stu-id="ddabb-127">Current MySQL bind-address.</span></span> |
| <span data-ttu-id="ddabb-128">username</span><span class="sxs-lookup"><span data-stu-id="ddabb-128">username</span></span>| <span data-ttu-id="ddabb-129">MySQL 使用者使用 toouse toomonitor hello MySQL 伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-129">MySQL user used toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="ddabb-130">Base64 編碼的密碼</span><span class="sxs-lookup"><span data-stu-id="ddabb-130">Base64 encoded Password</span></span>| <span data-ttu-id="ddabb-131">以 Base64 編碼的 hello MySQL 監視使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="ddabb-131">Password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="ddabb-132">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="ddabb-132">AutoUpdate</span></span>| <span data-ttu-id="ddabb-133">指定是否針對 toorescan 變更在 hello my.cnf 檔案是否有與 hello MySQL OMI 提供者升級時，覆寫 hello MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="ddabb-133">Specifies whether toorescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file when hello MySQL OMI Provider is upgraded.</span></span> |

### <a name="default-instance"></a><span data-ttu-id="ddabb-134">預設執行個體</span><span class="sxs-lookup"><span data-stu-id="ddabb-134">Default instance</span></span>
<span data-ttu-id="ddabb-135">預設執行個體和連接埠號碼 toomake 管理更容易的一部 Linux 主機上的多個 MySQL 執行個體，可以定義 hello MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="ddabb-135">hello MySQL OMI authentication file can define a default instance and port number toomake managing multiple MySQL instances on one Linux host easier.</span></span>  <span data-ttu-id="ddabb-136">以具有連接埠 0 的執行個體表示 hello 預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-136">hello default instance is denoted by an instance with port 0.</span></span> <span data-ttu-id="ddabb-137">所有其他執行個體將會繼承內容從 hello 預設執行個體設定，除非他們另外指定不同的值。</span><span class="sxs-lookup"><span data-stu-id="ddabb-137">All additional instances will inherit properties set from hello default instance unless they specify different values.</span></span> <span data-ttu-id="ddabb-138">例如，如果新增接聽通訊埠 '3308' 的 MySQL 執行個體，hello 預設執行個體的繫結位址、 使用者名稱和 Base64 編碼的密碼將會使用的 tootry 並監視 hello 接聽 3308 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-138">For example, if MySQL instance listening on port ‘3308’ is added, hello default instance’s bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="ddabb-139">如果 3308 上的 hello 執行個體繫結的 tooanother 位址並使用 hello 相同的 MySQL 使用者名稱和密碼組只有 hello 繫結位址所需的及 hello 其他屬性會被繼承。</span><span class="sxs-lookup"><span data-stu-id="ddabb-139">If hello instance on 3308 is bound tooanother address and uses hello same MySQL username and password pair only hello bind-address is needed, and hello other properties will be inherited.</span></span>

<span data-ttu-id="ddabb-140">下表中的 hello 具有範例執行個體設定</span><span class="sxs-lookup"><span data-stu-id="ddabb-140">hello following table has example instance settings</span></span> 

| <span data-ttu-id="ddabb-141">說明</span><span class="sxs-lookup"><span data-stu-id="ddabb-141">Description</span></span> | <span data-ttu-id="ddabb-142">檔案</span><span class="sxs-lookup"><span data-stu-id="ddabb-142">File</span></span> |
|:--|:--|
| <span data-ttu-id="ddabb-143">預設執行個體和連接埠為 3308 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-143">Default instance and instance with port 3308.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| <span data-ttu-id="ddabb-144">預設執行個體，以及連接埠為 3308 且具有不同使用者名稱密碼的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-144">Default instance and instance with port 3308 and different user name and password.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a><span data-ttu-id="ddabb-145">MySQL OMI 驗證檔案程式</span><span class="sxs-lookup"><span data-stu-id="ddabb-145">MySQL OMI Authentication File Program</span></span>
<span data-ttu-id="ddabb-146">隨附 hello 安裝 hello MySQL OMI 提供者是 MySQL OMI 驗證檔案程式可以是使用的 tooedit hello MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="ddabb-146">Included with hello installation of hello MySQL OMI provider is a MySQL OMI authentication file program which can be used tooedit hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="ddabb-147">hello 驗證檔案程式位於下列位置的 hello。</span><span class="sxs-lookup"><span data-stu-id="ddabb-147">hello authentication file program can be found at hello following location.</span></span>

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> <span data-ttu-id="ddabb-148">hello 認證檔案必須可供 hello omsagent 帳戶讀取。</span><span class="sxs-lookup"><span data-stu-id="ddabb-148">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="ddabb-149">建議您以 omsgent 的身分 hello mycimprovauth 命令。</span><span class="sxs-lookup"><span data-stu-id="ddabb-149">Running hello mycimprovauth command as omsgent is recommended.</span></span>

<span data-ttu-id="ddabb-150">hello 下表提供詳細資料 hello 語法使用 mycimprovauth。</span><span class="sxs-lookup"><span data-stu-id="ddabb-150">hello following table provides details on hello syntax for using mycimprovauth.</span></span>

| <span data-ttu-id="ddabb-151">作業</span><span class="sxs-lookup"><span data-stu-id="ddabb-151">Operation</span></span> | <span data-ttu-id="ddabb-152">範例</span><span class="sxs-lookup"><span data-stu-id="ddabb-152">Example</span></span> | <span data-ttu-id="ddabb-153">說明</span><span class="sxs-lookup"><span data-stu-id="ddabb-153">Description</span></span>
|:--|:--|:--|
| <span data-ttu-id="ddabb-154">autoupdate *false\\</span><span class="sxs-lookup"><span data-stu-id="ddabb-154">autoupdate *false\\</span></span>|<span data-ttu-id="ddabb-155">true*</span><span class="sxs-lookup"><span data-stu-id="ddabb-155">true*</span></span> | <span data-ttu-id="ddabb-156">mycimprovauth autoupdate false</span><span class="sxs-lookup"><span data-stu-id="ddabb-156">mycimprovauth autoupdate false</span></span> | <span data-ttu-id="ddabb-157">設定是否將自動更新 hello 驗證檔案在重新啟動或更新。</span><span class="sxs-lookup"><span data-stu-id="ddabb-157">Sets whether or not hello authentication file will be automatically updated on restart or update.</span></span> |
| <span data-ttu-id="ddabb-158">default *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="ddabb-158">default *bind-address username password*</span></span> | <span data-ttu-id="ddabb-159">mycimprovauth default 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="ddabb-159">mycimprovauth default 127.0.0.1 root pwd</span></span> | <span data-ttu-id="ddabb-160">設定 hello hello MySQL OMI 驗證檔案中的預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-160">Sets hello default instance in hello MySQL OMI authentication file.</span></span><br><span data-ttu-id="ddabb-161">應以純文字輸入 hello 密碼欄位-hello MySQL OMI 驗證檔案中的 hello 密碼會是 Base 64 編碼。</span><span class="sxs-lookup"><span data-stu-id="ddabb-161">hello password field should be entered in plain text - hello password in hello MySQL OMI authentication file will be Base 64 encoded.</span></span> |
| <span data-ttu-id="ddabb-162">delete *default\\</span><span class="sxs-lookup"><span data-stu-id="ddabb-162">delete *default\\</span></span>|<span data-ttu-id="ddabb-163">port_num*</span><span class="sxs-lookup"><span data-stu-id="ddabb-163">port_num*</span></span> | <span data-ttu-id="ddabb-164">mycimprovauth 3308</span><span class="sxs-lookup"><span data-stu-id="ddabb-164">mycimprovauth 3308</span></span> | <span data-ttu-id="ddabb-165">透過其中一個預設值或連接埠號碼，請刪除 hello 指定執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-165">Deletes hello specified instance by either default or by port number.</span></span> |
| <span data-ttu-id="ddabb-166">help</span><span class="sxs-lookup"><span data-stu-id="ddabb-166">help</span></span> | <span data-ttu-id="ddabb-167">mycimprov help</span><span class="sxs-lookup"><span data-stu-id="ddabb-167">mycimprov help</span></span> | <span data-ttu-id="ddabb-168">列印命令 toouse 的清單。</span><span class="sxs-lookup"><span data-stu-id="ddabb-168">Prints out a list of commands toouse.</span></span> |
| <span data-ttu-id="ddabb-169">print</span><span class="sxs-lookup"><span data-stu-id="ddabb-169">print</span></span> | <span data-ttu-id="ddabb-170">mycimprov print</span><span class="sxs-lookup"><span data-stu-id="ddabb-170">mycimprov print</span></span> | <span data-ttu-id="ddabb-171">列印簡單的 tooread MySQL OMI 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="ddabb-171">Prints out an easy tooread MySQL OMI authentication file.</span></span> |
| <span data-ttu-id="ddabb-172">update port_num *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="ddabb-172">update port_num *bind-address username password*</span></span> | <span data-ttu-id="ddabb-173">mycimprov update 3307 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="ddabb-173">mycimprov update 3307 127.0.0.1 root pwd</span></span> | <span data-ttu-id="ddabb-174">更新 hello 指定執行個體，或如果不存在，則將 hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddabb-174">Updates hello specified instance or adds hello instance if it does not exist.</span></span> |

<span data-ttu-id="ddabb-175">hello 下列範例命令 hello MySQL 伺服器的預設使用者帳戶在 localhost 上定義。</span><span class="sxs-lookup"><span data-stu-id="ddabb-175">hello following example commands define a default user account for hello MySQL server on localhost.</span></span>  <span data-ttu-id="ddabb-176">應以純文字輸入 hello 密碼欄位-hello MySQL OMI 驗證檔案中的 hello 密碼將會 Base 64 編碼</span><span class="sxs-lookup"><span data-stu-id="ddabb-176">hello password field should be entered in plain text - hello password in hello MySQL OMI authentication file will be Base 64 encoded</span></span>

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="ddabb-177">MySQL 效能計數器所需的資料庫權限</span><span class="sxs-lookup"><span data-stu-id="ddabb-177">Database Permissions Required for MySQL Performance Counters</span></span>
<span data-ttu-id="ddabb-178">hello MySQL 使用者需要存取 toohello 遵循查詢 toocollect MySQL 伺服器效能資料。</span><span class="sxs-lookup"><span data-stu-id="ddabb-178">hello MySQL User requires access toohello following queries toocollect MySQL Server performance data.</span></span> 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


<span data-ttu-id="ddabb-179">hello MySQL 使用者也需要下列預設資料表的選取存取 toohello。</span><span class="sxs-lookup"><span data-stu-id="ddabb-179">hello MySQL user also requires SELECT access toohello following default tables.</span></span>

- <span data-ttu-id="ddabb-180">information_schema</span><span class="sxs-lookup"><span data-stu-id="ddabb-180">information_schema</span></span>
- <span data-ttu-id="ddabb-181">mysql。</span><span class="sxs-lookup"><span data-stu-id="ddabb-181">mysql.</span></span> 

<span data-ttu-id="ddabb-182">執行下列 grant 命令 hello 可以授與這些權限。</span><span class="sxs-lookup"><span data-stu-id="ddabb-182">These privileges can be granted by running hello following grant commands.</span></span>

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> <span data-ttu-id="ddabb-183">toogrant 權限 tooa 的 MySQL 監視使用者 hello 授與使用者必須擁有 hello 'GRANT option' 權限，以及被授與的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="ddabb-183">toogrant permissions tooa MySQL monitoring user hello granting user must have hello ‘GRANT option’ privilege as well as hello privilege being granted.</span></span>

### <a name="define-performance-counters"></a><span data-ttu-id="ddabb-184">定義效能計數器</span><span class="sxs-lookup"><span data-stu-id="ddabb-184">Define performance counters</span></span>

<span data-ttu-id="ddabb-185">一旦您設定 hello OMS Agent for Linux toosend 資料 tooLog 分析，您必須設定 hello 效能計數器 toocollect。</span><span class="sxs-lookup"><span data-stu-id="ddabb-185">Once you configure hello OMS Agent for Linux toosend data tooLog Analytics, you must configure hello performance counters toocollect.</span></span>  <span data-ttu-id="ddabb-186">使用中的 hello 程序[記錄分析中的 Windows 和 Linux 的效能資料來源](log-analytics-data-sources-windows-events.md)hello 下表中的 hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="ddabb-186">Use hello procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with hello counters in hello following table.</span></span>

| <span data-ttu-id="ddabb-187">物件名稱</span><span class="sxs-lookup"><span data-stu-id="ddabb-187">Object Name</span></span> | <span data-ttu-id="ddabb-188">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="ddabb-188">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="ddabb-189">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="ddabb-189">MySQL Database</span></span> | <span data-ttu-id="ddabb-190">Disk Space in Bytes</span><span class="sxs-lookup"><span data-stu-id="ddabb-190">Disk Space in Bytes</span></span> |
| <span data-ttu-id="ddabb-191">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="ddabb-191">MySQL Database</span></span> | <span data-ttu-id="ddabb-192">資料表</span><span class="sxs-lookup"><span data-stu-id="ddabb-192">Tables</span></span> |
| <span data-ttu-id="ddabb-193">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-193">MySQL Server</span></span> | <span data-ttu-id="ddabb-194">Aborted Connection Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-194">Aborted Connection Pct</span></span> |
| <span data-ttu-id="ddabb-195">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-195">MySQL Server</span></span> | <span data-ttu-id="ddabb-196">Connection Use Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-196">Connection Use Pct</span></span> |
| <span data-ttu-id="ddabb-197">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-197">MySQL Server</span></span> | <span data-ttu-id="ddabb-198">Disk Space in Bytes</span><span class="sxs-lookup"><span data-stu-id="ddabb-198">Disk Space Use in Bytes</span></span> |
| <span data-ttu-id="ddabb-199">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-199">MySQL Server</span></span> | <span data-ttu-id="ddabb-200">Full Table Scan Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-200">Full Table Scan Pct</span></span> |
| <span data-ttu-id="ddabb-201">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-201">MySQL Server</span></span> | <span data-ttu-id="ddabb-202">InnoDB Buffer Pool Hit Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-202">InnoDB Buffer Pool Hit Pct</span></span> |
| <span data-ttu-id="ddabb-203">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-203">MySQL Server</span></span> | <span data-ttu-id="ddabb-204">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-204">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="ddabb-205">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-205">MySQL Server</span></span> | <span data-ttu-id="ddabb-206">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-206">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="ddabb-207">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-207">MySQL Server</span></span> | <span data-ttu-id="ddabb-208">Key Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-208">Key Cache Hit Pct</span></span> |
| <span data-ttu-id="ddabb-209">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-209">MySQL Server</span></span> | <span data-ttu-id="ddabb-210">Key Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-210">Key Cache Use Pct</span></span> |
| <span data-ttu-id="ddabb-211">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-211">MySQL Server</span></span> | <span data-ttu-id="ddabb-212">Key Cache Write Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-212">Key Cache Write Pct</span></span> |
| <span data-ttu-id="ddabb-213">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-213">MySQL Server</span></span> | <span data-ttu-id="ddabb-214">Query Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-214">Query Cache Hit Pct</span></span> |
| <span data-ttu-id="ddabb-215">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-215">MySQL Server</span></span> | <span data-ttu-id="ddabb-216">Query Cache Prunes Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-216">Query Cache Prunes Pct</span></span> |
| <span data-ttu-id="ddabb-217">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-217">MySQL Server</span></span> | <span data-ttu-id="ddabb-218">Query Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-218">Query Cache Use Pct</span></span> |
| <span data-ttu-id="ddabb-219">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-219">MySQL Server</span></span> | <span data-ttu-id="ddabb-220">Table Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-220">Table Cache Hit Pct</span></span> |
| <span data-ttu-id="ddabb-221">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-221">MySQL Server</span></span> | <span data-ttu-id="ddabb-222">Table Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-222">Table Cache Use Pct</span></span> |
| <span data-ttu-id="ddabb-223">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-223">MySQL Server</span></span> | <span data-ttu-id="ddabb-224">Table Lock Contention Pct</span><span class="sxs-lookup"><span data-stu-id="ddabb-224">Table Lock Contention Pct</span></span> |

## <a name="apache-http-server"></a><span data-ttu-id="ddabb-225">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-225">Apache HTTP Server</span></span> 
<span data-ttu-id="ddabb-226">如果 Apache HTTP Server 是電腦上偵測到 hello 安裝 hello omsagent 配套時，會自動安裝的效能監視適用於 Apache HTTP Server 提供者。</span><span class="sxs-lookup"><span data-stu-id="ddabb-226">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span></span> <span data-ttu-id="ddabb-227">此提供者依賴 Apache 模組必須載入順序 tooaccess 效能資料中的 hello Apache HTTP Server。</span><span class="sxs-lookup"><span data-stu-id="ddabb-227">This provider relies on an Apache module that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span> <span data-ttu-id="ddabb-228">可以載入 hello 模組，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="ddabb-228">hello module can be loaded with hello following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="ddabb-229">toounload hello Apache 監視模組，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ddabb-229">toounload hello Apache monitoring module, run hello following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a><span data-ttu-id="ddabb-230">定義效能計數器</span><span class="sxs-lookup"><span data-stu-id="ddabb-230">Define performance counters</span></span>

<span data-ttu-id="ddabb-231">一旦您設定 hello OMS Agent for Linux toosend 資料 tooLog 分析，您必須設定 hello 效能計數器 toocollect。</span><span class="sxs-lookup"><span data-stu-id="ddabb-231">Once you configure hello OMS Agent for Linux toosend data tooLog Analytics, you must configure hello performance counters toocollect.</span></span>  <span data-ttu-id="ddabb-232">使用中的 hello 程序[記錄分析中的 Windows 和 Linux 的效能資料來源](log-analytics-data-sources-windows-events.md)hello 下表中的 hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="ddabb-232">Use hello procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with hello counters in hello following table.</span></span>

| <span data-ttu-id="ddabb-233">物件名稱</span><span class="sxs-lookup"><span data-stu-id="ddabb-233">Object Name</span></span> | <span data-ttu-id="ddabb-234">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="ddabb-234">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="ddabb-235">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-235">Apache HTTP Server</span></span> | <span data-ttu-id="ddabb-236">Busy Workers</span><span class="sxs-lookup"><span data-stu-id="ddabb-236">Busy Workers</span></span> |
| <span data-ttu-id="ddabb-237">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-237">Apache HTTP Server</span></span> | <span data-ttu-id="ddabb-238">Idle Workers</span><span class="sxs-lookup"><span data-stu-id="ddabb-238">Idle Workers</span></span> |
| <span data-ttu-id="ddabb-239">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-239">Apache HTTP Server</span></span> | <span data-ttu-id="ddabb-240">Pct Busy Workers</span><span class="sxs-lookup"><span data-stu-id="ddabb-240">Pct Busy Workers</span></span> |
| <span data-ttu-id="ddabb-241">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-241">Apache HTTP Server</span></span> | <span data-ttu-id="ddabb-242">Total Pct CPU</span><span class="sxs-lookup"><span data-stu-id="ddabb-242">Total Pct CPU</span></span> |
| <span data-ttu-id="ddabb-243">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="ddabb-243">Apache Virtual Host</span></span> | <span data-ttu-id="ddabb-244">Errors per Minute - Client</span><span class="sxs-lookup"><span data-stu-id="ddabb-244">Errors per Minute - Client</span></span> |
| <span data-ttu-id="ddabb-245">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="ddabb-245">Apache Virtual Host</span></span> | <span data-ttu-id="ddabb-246">Errors per Minute - Server</span><span class="sxs-lookup"><span data-stu-id="ddabb-246">Errors per Minute - Server</span></span> |
| <span data-ttu-id="ddabb-247">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="ddabb-247">Apache Virtual Host</span></span> | <span data-ttu-id="ddabb-248">KB per Request</span><span class="sxs-lookup"><span data-stu-id="ddabb-248">KB per Request</span></span> |
| <span data-ttu-id="ddabb-249">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="ddabb-249">Apache Virtual Host</span></span> | <span data-ttu-id="ddabb-250">Requests KB per Second</span><span class="sxs-lookup"><span data-stu-id="ddabb-250">Requests KB per Second</span></span> |
| <span data-ttu-id="ddabb-251">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="ddabb-251">Apache Virtual Host</span></span> | <span data-ttu-id="ddabb-252">Requests per Second</span><span class="sxs-lookup"><span data-stu-id="ddabb-252">Requests per Second</span></span> |



## <a name="next-steps"></a><span data-ttu-id="ddabb-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddabb-253">Next steps</span></span>
* <span data-ttu-id="ddabb-254">從 Linux 代理程式[收集效能計數器](log-analytics-data-sources-performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="ddabb-254">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span></span>
* <span data-ttu-id="ddabb-255">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="ddabb-255">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
