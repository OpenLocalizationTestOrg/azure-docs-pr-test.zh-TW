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
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>在 Log Analytics 中收集 Linux 應用程式的效能計數器 
這篇文章詳細說明如何設定 hello [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect 特定應用程式的效能計數器。  在本文中包含的 hello 應用程式可以：  

- [MySQL](#MySQL)
- [Apache HTTP Server](#apache-http-server)

## <a name="mysql"></a>MySQL
如果 MySQL 伺服器或 MariaDB 伺服器是電腦上偵測到 hello hello OMS 代理程式安裝時，會自動安裝的效能監視提供者的 MySQL 伺服器。 此提供者連接 toohello 本機 MySQL/MariaDB 伺服器 tooexpose 效能統計資料。 必須設定 MySQL 使用者認證，如此 hello 者可以存取 MySQL 伺服器 hello。

### <a name="configure-mysql-credentials"></a>設定 MySQL 認證
hello MySQL OMI 提供者需要預先設定的 MySQL 使用者，並安裝 MySQL 用戶端程式庫中順序 tooquery hello 效能和健全狀況資訊從 hello MySQL 執行個體。  這些認證會儲存在儲存在 hello Linux 代理程式的驗證檔案中。  hello 驗證檔案會指定哪些繫結位址和連接埠 hello MySQL 執行個體正在接聽，以及認證 toouse toogather 度量。  

在安裝 hello OMS Agent for Linux hello MySQL OMI 提供者會掃描 MySQL my.cnf 組態檔 （預設位置） 繫結位址和連接埠和部分組 hello MySQL OMI 驗證檔案。

hello MySQL 驗證檔案會儲存在`/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`。


### <a name="authentication-file-format"></a>驗證檔案格式
以下是 hello hello MySQL OMI 驗證檔案格式

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

下表中的 hello 說明 hello 驗證檔案中的 hello 項目。

| 屬性 | 說明 |
|:--|:--|
| Port | 表示目前的連接埠 hello hello MySQL 執行個體正在接聽。 連接埠 0 會指定下列的 hello 屬性會用於預設執行個體。 |
| 繫結位址| 目前的 MySQL 繫結位址。 |
| username| MySQL 使用者使用 toouse toomonitor hello MySQL 伺服器執行個體。 |
| Base64 編碼的密碼| 以 Base64 編碼的 hello MySQL 監視使用者的密碼。 |
| AutoUpdate| 指定是否針對 toorescan 變更在 hello my.cnf 檔案是否有與 hello MySQL OMI 提供者升級時，覆寫 hello MySQL OMI 驗證檔案。 |

### <a name="default-instance"></a>預設執行個體
預設執行個體和連接埠號碼 toomake 管理更容易的一部 Linux 主機上的多個 MySQL 執行個體，可以定義 hello MySQL OMI 驗證檔案。  以具有連接埠 0 的執行個體表示 hello 預設執行個體。 所有其他執行個體將會繼承內容從 hello 預設執行個體設定，除非他們另外指定不同的值。 例如，如果新增接聽通訊埠 '3308' 的 MySQL 執行個體，hello 預設執行個體的繫結位址、 使用者名稱和 Base64 編碼的密碼將會使用的 tootry 並監視 hello 接聽 3308 的執行個體。 如果 3308 上的 hello 執行個體繫結的 tooanother 位址並使用 hello 相同的 MySQL 使用者名稱和密碼組只有 hello 繫結位址所需的及 hello 其他屬性會被繼承。

下表中的 hello 具有範例執行個體設定 

| 說明 | 檔案 |
|:--|:--|
| 預設執行個體和連接埠為 3308 的執行個體。 | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| 預設執行個體，以及連接埠為 3308 且具有不同使用者名稱密碼的執行個體。 | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>MySQL OMI 驗證檔案程式
隨附 hello 安裝 hello MySQL OMI 提供者是 MySQL OMI 驗證檔案程式可以是使用的 tooedit hello MySQL OMI 驗證檔案。 hello 驗證檔案程式位於下列位置的 hello。

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> hello 認證檔案必須可供 hello omsagent 帳戶讀取。 建議您以 omsgent 的身分 hello mycimprovauth 命令。

hello 下表提供詳細資料 hello 語法使用 mycimprovauth。

| 作業 | 範例 | 說明
|:--|:--|:--|
| autoupdate *false\|true* | mycimprovauth autoupdate false | 設定是否將自動更新 hello 驗證檔案在重新啟動或更新。 |
| default *bind-address username password* | mycimprovauth default 127.0.0.1 root pwd | 設定 hello hello MySQL OMI 驗證檔案中的預設執行個體。<br>應以純文字輸入 hello 密碼欄位-hello MySQL OMI 驗證檔案中的 hello 密碼會是 Base 64 編碼。 |
| delete *default\|port_num* | mycimprovauth 3308 | 透過其中一個預設值或連接埠號碼，請刪除 hello 指定執行個體。 |
| help | mycimprov help | 列印命令 toouse 的清單。 |
| print | mycimprov print | 列印簡單的 tooread MySQL OMI 驗證檔案。 |
| update port_num *bind-address username password* | mycimprov update 3307 127.0.0.1 root pwd | 更新 hello 指定執行個體，或如果不存在，則將 hello 執行個體。 |

hello 下列範例命令 hello MySQL 伺服器的預設使用者帳戶在 localhost 上定義。  應以純文字輸入 hello 密碼欄位-hello MySQL OMI 驗證檔案中的 hello 密碼將會 Base 64 編碼

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>MySQL 效能計數器所需的資料庫權限
hello MySQL 使用者需要存取 toohello 遵循查詢 toocollect MySQL 伺服器效能資料。 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


hello MySQL 使用者也需要下列預設資料表的選取存取 toohello。

- information_schema
- mysql。 

執行下列 grant 命令 hello 可以授與這些權限。

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant 權限 tooa 的 MySQL 監視使用者 hello 授與使用者必須擁有 hello 'GRANT option' 權限，以及被授與的 hello 權限。

### <a name="define-performance-counters"></a>定義效能計數器

一旦您設定 hello OMS Agent for Linux toosend 資料 tooLog 分析，您必須設定 hello 效能計數器 toocollect。  使用中的 hello 程序[記錄分析中的 Windows 和 Linux 的效能資料來源](log-analytics-data-sources-windows-events.md)hello 下表中的 hello 計數器。

| 物件名稱 | 計數器名稱 |
|:--|:--|
| MySQL Database | Disk Space in Bytes |
| MySQL Database | 資料表 |
| MySQL Server | Aborted Connection Pct |
| MySQL Server | Connection Use Pct |
| MySQL Server | Disk Space in Bytes |
| MySQL Server | Full Table Scan Pct |
| MySQL Server | InnoDB Buffer Pool Hit Pct |
| MySQL Server | InnoDB Buffer Pool Use Pct |
| MySQL Server | InnoDB Buffer Pool Use Pct |
| MySQL Server | Key Cache Hit Pct |
| MySQL Server | Key Cache Use Pct |
| MySQL Server | Key Cache Write Pct |
| MySQL Server | Query Cache Hit Pct |
| MySQL Server | Query Cache Prunes Pct |
| MySQL Server | Query Cache Use Pct |
| MySQL Server | Table Cache Hit Pct |
| MySQL Server | Table Cache Use Pct |
| MySQL Server | Table Lock Contention Pct |

## <a name="apache-http-server"></a>Apache HTTP Server 
如果 Apache HTTP Server 是電腦上偵測到 hello 安裝 hello omsagent 配套時，會自動安裝的效能監視適用於 Apache HTTP Server 提供者。 此提供者依賴 Apache 模組必須載入順序 tooaccess 效能資料中的 hello Apache HTTP Server。 可以載入 hello 模組，以 hello 下列命令：
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache 監視模組，執行下列命令的 hello:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>定義效能計數器

一旦您設定 hello OMS Agent for Linux toosend 資料 tooLog 分析，您必須設定 hello 效能計數器 toocollect。  使用中的 hello 程序[記錄分析中的 Windows 和 Linux 的效能資料來源](log-analytics-data-sources-windows-events.md)hello 下表中的 hello 計數器。

| 物件名稱 | 計數器名稱 |
|:--|:--|
| Apache HTTP Server | Busy Workers |
| Apache HTTP Server | Idle Workers |
| Apache HTTP Server | Pct Busy Workers |
| Apache HTTP Server | Total Pct CPU |
| Apache Virtual Host | Errors per Minute - Client |
| Apache Virtual Host | Errors per Minute - Server |
| Apache Virtual Host | KB per Request |
| Apache Virtual Host | Requests KB per Second |
| Apache Virtual Host | Requests per Second |



## <a name="next-steps"></a>後續步驟
* 從 Linux 代理程式[收集效能計數器](log-analytics-data-sources-performance-counters.md)。
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。 
