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
# <a name="connect-your-linux-computers-toolog-analytics"></a>連接您的 Linux 電腦 tooLog 分析
使用 Log Analytics，您可以收集和處理從 Linux 電腦所產生的資料。 加入從 Linux tooOMS 收集的資料可讓您 toomanage Linux 系統和像使用 Docker，容器解決方案，無論您的電腦位於何處，任何地點。 資料來源可能位於您的內部部署資料中心，作為實體伺服器，例如 Amazon Web Services (AWS) 或 Microsoft Azure 雲端託管服務中的虛擬電腦，或甚至 hello 您桌上的膝上型電腦。 此外，OMS 同樣也會收集來自 Windows 電腦的資料，因此支援真正混合式 IT 環境。

您可以使用單一管理入口網站，來檢視和管理來自具有 OMS 中 Log Analytics 之所有來源的資料。 這會減少 hello 需要 toomonitor 使用許多不同的系統，可讓您輕鬆 tooconsume，因此，您可以匯出您喜歡 toowhatever 商務分析解決方案或系統已經有任何資料。

本文是快速入門指南可協助您收集和管理 Linux 電腦使用 hello OMS Agent for Linux 的資料。 如需其他技術詳細資訊 (例如 Proxy 伺服器組態、CollectD 計量相關資訊，以及自訂 JSON 資料來源)，您可在 GitHub 上的 [OMS Agent for Linux 概觀 (英文)](https://github.com/Microsoft/OMS-Agent-for-Linux) 和 [OMS Agent for Linux 完整文件 (英文)](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) 中找到該資訊。

目前，您可以收集下列類型的資料從 Linux 電腦的 hello:

* 效能度量
* Syslog 事件
* 來自 Nagios 和 Zabbix 的警示
* Docker 容器效能計量、清查和記錄檔

## <a name="supported-linux-versions"></a>支援的 Linux 版本
各種 Linux 散發套件正式支援 x86 和 x64 版本。 不過，其他未列出的發佈也可能執行 OMS Agent for Linux hello。

* Amazon Linux 2012.09 到 2015.09
* CentOS Linux 5、6 和 7
* Oracle Linux 5、6 和 7
* Red Hat Enterprise Linux Server 5、6 和 7
* Debian GNU/Linux 6、7 和 8
* Ubuntu 12.04 LTS、14.04 LTS、15.04、15.10
* SUSE Linux Enterprise Server 11 和 12

## <a name="oms-agent-for-linux"></a>OMS Agent for Linux
hello Operations Management Suite Agent for Linux 包含多個套件。 hello 發行檔案包含下列套件，以執行 hello 殼層配套 hello `--extract`。

| **Package** | **版本** | **說明** |
| --- | --- | --- |
| omsagent |1.1.0 |hello Operations Management Suite Agent for Linux |
| omsconfig |1.1.1 |Hello OMS 代理程式的設定代理程式 |
| omi |1.0.8.3 |開放式管理基礎結構 (OMI) -- 輕量型 CIM 伺服器 |
| scx |1.6.2 |作業系統效能計量的 OMI CIM 提供者 |
| apache-cimprov |1.0.0 |OMI 的 Apache HTTP 伺服器效能監視提供者。 僅在偵測到 Apache HTTP 伺服器時才安裝。 |
| mysql-cimprov |1.0.0 |OMI 的 MySQL 伺服器效能監視提供者。 僅在偵測到 MySQL/MariaDB 伺服器時才安裝。 |
| docker-cimprov |0.1.0 |OMI 的 Docker 提供者。 僅在偵測到 Docker 時才安裝。 |

### <a name="additional-installation-artifacts"></a>其他安裝構件
在安裝之後 hello OMS agent for Linux 套件，hello 下列全系統設定變更會套用。 解除安裝 hello omsagent 套件時，會移除這些成品。

* 會建立名為 `omsagent` 的非特殊權限使用者。 這是 hello hello omsagent 精靈執行的帳戶為
* Sudoers 的"include"檔案建立在 /etc/sudoers.d/omsagent 這會授權 omsagent toorestart hello syslog 和 omsagent 精靈。 如果 sudo 安裝 hello 版本不支援 sudo"include"指示詞，這些項目會寫入太/等/sudoers。
* hello syslog 組態是修改的 tooforward 事件 toohello 代理程式的子集。 如需詳細資訊，請參閱 hello**設定資料收集**下一節

### <a name="linux-data-collection-details"></a>Linux 資料收集詳細資料
hello 下表顯示資料收集方法，以及如何收集資料的其他詳細資料。

| 來源 | 直接代理程式 | SCOM 代理程式 | Azure 儲存體 | SCOM 是否為必要項目？ | 透過管理群組傳送的 SCOM 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 分鐘 |
| Nagios |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |與抵達同時 |
| syslog |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |從 Azure 儲存體：10 分鐘；從代理程式：與抵達同時 |
| Linux 效能計數器 |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |依排程，最少 10 秒 |
| 變更追蹤 |![是](./media/log-analytics-linux-agents/oms-bullet-green.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |![否](./media/log-analytics-linux-agents/oms-bullet-red.png) |每小時 |

### <a name="package-requirements"></a>封裝需求
| **必要封裝** | **說明** | **最低版本** |
| --- | --- | --- |
| Glibc |GNU C 程式庫 |2.5-12 |
| Openssl |OpenSSL 程式庫 |0.9.8e 或 1.0 |
| Curl |cURL Web 用戶端 |7.15.5 |
| Python-ctypes |函數程式庫 |n/a |
| PAM |插入式驗證模組 |n/a |

> [!NOTE]
> 需要 rsyslog 或 syslog-ng 是必要的 toocollect syslog 訊息。 在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。 toocollect syslog 資料，從這一版的這些發佈，hello rsyslog 精靈應該安裝和設定 tooreplace sysklog。
>
>

## <a name="quick-install"></a>快速安裝
執行下列命令 toodownload hello omsagent hello、 驗證 hello 總和檢查碼，然後安裝和上架 hello 代理程式。 命令是針對 64 位元。 hello 工作區識別碼及主索引鍵位於 hello OMS 入口網站下**設定**上 hello**連線來源** 索引標籤。

![工作區詳細資料](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

有各種不同的其他方法 tooinstall hello 代理程式，並將它升級。 您可以深入資訊，請在[步驟 tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)。

您也可以檢視 hello [Azure 影片逐步解說](https://www.youtube.com/watch?v=mF1wtHPEzT0)。

## <a name="choose-your-linux-data-collection-method"></a>選擇 Linux 資料收集方法
如何選擇 hello 就像 toocollect 取決於您是否想 toouse hello OMS 入口網站，或您想要編輯直接在 Linux 用戶端上的不同組態檔的資料類型。 如果您選擇 toouse hello 入口網站，hello 組態就會自動傳送 tooall Linux 用戶端。 如果不同 Linux 用戶端需要不同的設定，您將會個別 – 需要 tooedit 用戶端檔案，或使用替代方法，像是 PowerShell DSC、 Chef 或 Puppet。

您可以指定 hello syslog 事件和效能計數器的 toocollect hello Linux 電腦上使用組態檔。 *如果您選擇 tooconfigure 資料收集藉由編輯代理程式組態檔時，您應該停用 hello 集中式的組態。*  Tooconfigure hello 代理程式的組態檔，以及 toodisable 集中式組態的所有 OMS Agents for Linux 個別電腦中的資料收集以下提供的指示。

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>停用個別 Linux 電腦的 OMS 管理
集中式的資料收集組態資料已停用個別 Linux 電腦以 hello OMS_MetaConfigHelper.py 指令碼。 如果有一部分的電腦應該有特製化組態，則這十分有用。

toodisable 集中式的組態：

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

toore 啟用集中式的組態：

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Linux 效能計數器
Linux 效能計數器會類似 tooWindows 效能計數器，兩者的操作類似。 您可以使用下列程序 tooadd hello 並設定它們。 新增 tooOMS 之後，會收集資料，每隔 30 秒。

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd 在 OMS 中的 Linux 效能計數器
1. tooconfigure OMS Agents for Linux 使用 hello OMS 入口網站，您可以新增 Linux 效能計數器在 hello 設定頁面上，按一下 **資料**。  
2. 在 hello**設定**頁面**資料**，按一下**Linux 效能計數器**，然後選取或類型的 hello 名稱要 tooadd 的 hello 計數器。  
    ![資料](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. 如果您不知道 hello 的 hello 計數器的完整名稱，您可以開始輸入部分名稱，即會出現可用的計數器清單。 當您找到 hello 計數器您想 tooadd，按一下 [hello] 清單中的 hello 名稱，然後按一下 hello 加上圖示 tooadd hello 計數器。
4. 新增 hello 計數器之後，它會出現在 hello 以彩色列反白顯示的計數器清單。
5. 根據預設，hello**套用下列組態 toomy 電腦**選取選項。 如果您想將組態資料傳送 toodisable，清除 hello 選取項目。
6. 當您完成修改效能計數器時，在 hello hello 頁面底部按一下**儲存**toofinalize 您的變更。 您所做的 hello 組態變更便會傳送 tooall hello OMS Agents for Linux，會向 OMS 時，通常會在 5 分鐘內。

### <a name="configure-linux-performance-counters-in-oms"></a>在 OMS 中設定 Linux 效能計數器
對於 Windows 效能計數器，您可以選擇每個效能計數器的特定執行個體。 不過，對於 Linux 效能計數器，您所選擇的計數器任何執行個體適用於 tooall 的 hello 父計數器的子系計數器。 hello 下表顯示 hello 常見執行個體可用 tooboth Linux 和 Windows 效能計數器。

| **執行個體名稱** | **意義** |
| --- | --- |
| \_總計 |所有的 hello 執行個體的總數 |
| \* |所有執行個體 |
| (/&#124;/var) |比對名為 / 或 /var 的執行個體 |

同樣地，hello 取樣間隔，您選擇為父計數器適用於 tooall 及其子系計數器。 換句話說，所有 hello 子系計數器取樣間隔和執行個體都連結在一起。

### <a name="add-and-configure-performance-metrics-with-linux"></a>使用 Linux 加入和設定效能計量
效能度量 toocollect 受到 hello 組態在/等/選擇/microsoft/omsagent/&lt;工作區識別碼&gt;/conf/omsagent.conf。 請參閱[可用的效能標準](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics)可用的類別和校 hello OMS Agent for Linux。

應為單一 hello 組態檔中定義每個物件或類別目錄的效能度量 toocollect`<source>`項目。 hello 語法遵循下列的 hello 模式。

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

這個項目的 hello 可設定參數如下：

* **物件\_名稱**: hello hello 集合的物件名稱。
* **執行個體\_regex**:*規則運算式*定義哪些執行個體 toocollect。 hello 值：`.*`指定所有執行個體。 toocollect 處理器校能標準只 hello\_總執行個體，您可以指定`_Total`。 toocollect 的處理序校只 hello crond 或 sshd 執行個體，您可以指定： `(crond|sshd)`。
* **計數器\_名稱\_regex**:*規則運算式*定義哪些物件的計數器 （hello） toocollect。 toocollect hello 物件的所有計數器都指定： `.*`。 toocollect 只會交換空間計數器 hello 記憶體物件，您可以指定：`.+Swap.+`
* **間隔：**: hello 的 hello 收集物件計數器頻率。

效能標準的 hello 預設組態是：

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>使用 Linux 命令啟用 MySQL 效能計數器
如果 MySQL 伺服器或 MariaDB 伺服器偵測到 hello 電腦上安裝 hello omsagent 配套時，會自動安裝的效能監視提供者的 MySQL 伺服器。 此提供者連接 toohello 本機 MySQL/MariaDB 伺服器 tooexpose 效能統計資料。 您需要 tooconfigure MySQL 使用者認證，讓 hello 者可以存取 MySQL 伺服器 hello。

toodefine 預設使用者帳戶 hello MySQL 伺服器的 localhost，下列命令範例使用 hello 上。

> [!NOTE]
> hello 認證檔案必須可供 hello omsagent 帳戶讀取。 建議您以 omsgent 的身分 hello mycimprovauth 命令。
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


或者，您可以指定 hello 需要 MySQL 認證，在檔案中，建立 hello 檔案： /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth如需管理 MySQL 認證以便透過 hello mysql-auth 檔案進行監視的詳細資訊，請參閱[管理 MySQL 監視認證 hello 驗證檔案中的](#manage-mysql-monitoring-credentials-in-the-authentication-file)。

請參閱[資料庫 MySQL 效能計數器所需的權限](#database-permissions-required-for-mysql-performance-counters)hello MySQL 使用者 toocollect MySQL 伺服器效能資料所需的物件權限的詳細資料。

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>使用 Linux 命令啟用 Apache HTTP 伺服器效能計數器
如果 Apache HTTP Server 是電腦上偵測到 hello 安裝 hello omsagent 配套時，會自動安裝的效能監視適用於 Apache HTTP Server 提供者。 此提供者依賴 Apache 「 模組 」，必須載入順序 tooaccess 效能資料中的 hello Apache HTTP Server。

您可以載入 hello 模組以 hello 下列命令：

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache 監視模組，執行下列命令的 hello:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>記錄分析 tooview 效能資料
1. 在 hello Operations Management Suite 入口網站中，按一下 hello 記錄搜尋 磚。
2. 在 hello 搜尋列中輸入`* (Type=Perf)`tooview 所有效能計數器。

因為 OMS 也會收集 Windows 效能計數器資料，您應該將範圍縮小 hello 搜尋 tooLinux 特定資料。 因此，hello 下列範例會顯示效能資料特定 tooan 範例 Linux 伺服器名為 Chorizo21。

```
Type=Perf Computer=chorizo*
```

![搜尋結果中所顯示的範例伺服器](./media/log-analytics-linux-agents/oms-perfsearch01.png)

您可以在 hello 結果中，按一下**度量**tooview hello 計數器，用來收集資料。 每個計數器的即時資料會顯示為圖形。

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>syslog
Syslog 是事件記錄通訊協定類似 tooWindows 事件記錄檔，兩者的操作類似在 OMS 中顯示時。

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd 在 OMS 中新增 Linux syslog 設備
1. 在 hello**設定**頁面**資料**，按一下  **Syslog**然後 toohello 左的 hello 加號圖示，輸入您想 tooadd hello syslog 設備 hello 名稱。
    ![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. 如果您不知道 hello 設備 hello 完整名稱，您可以開始輸入部分名稱，即會出現可用的 syslog 設備清單。 當您找到您想 tooadd，按一下 [hello] 清單中的 hello 名稱，然後按一下hello 加上圖示 tooadd hello hello syslog 設備 syslog 設備。
3. 您新增 hello 設備，它會出現在 hello 清單之後反白顯示以彩色列。 接下來，選擇 hello 嚴重性 （syslog 設備資訊的類別） 的 toocollect。
4. 在 hello hello 頁面底部按一下**儲存**toofinalize 您的變更。 您所做的 hello 組態變更便會傳送 tooall hello OMS Agents for Linux，會向 OMS 時，通常會在 5 分鐘內。

### <a name="configure-linux-syslog-facilities-in-linux"></a>在 Linux 中設定 Linux syslog 設備
Syslog 事件從 hello syslog 服務精靈傳送，例如 rsyslog 或 syslog ng、 tooa 本機連接埠的 hello 代理程式正在接聽。 連接埠預設為 25224。 Hello 代理程式安裝時，會套用預設 syslog 組態。 這可以在下列項目中找到︰

Rsyslog：/etc/rsyslog.d/rsyslog-oms.conf

Syslog-ng：/etc/syslog-ng/syslog-ng.conf

hello 預設 OMS 代理程式 syslog 組態會上傳所有設備的嚴重性為警告或更高的 syslog 事件。

> [!NOTE]
> 如果您編輯 hello syslog 設定，您必須重新啟動 hello 變更 tootake 效果 hello syslog 服務精靈。
>
>

hello 預設 syslog 組態 hello OMS Agent for Linux 的 OMS 是：

#### <a name="rsyslog"></a>Rsyslog
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

#### <a name="syslog-ng"></a>Syslog-ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview 記錄分析的所有 Syslog 事件
1. 在 hello Operations Management Suite 入口網站中，按一下 hello**記錄搜尋**磚。
2. 在 hello**記錄管理**群組中選擇預先定義的 syslog 搜尋，然後選取一個 toorun 它。

此範例示範所有 Syslog 事件。

![記錄檔搜尋中所顯示的 Syslog 事件](./media/log-analytics-linux-agents/oms-linux-syslog.png)

現在，您可以切入至搜尋結果。

## <a name="linux-alerts"></a>Linux 警示
如果您使用 Nagios 或 Zabbix toomanage 您的 Linux 機器，則 OMS 可以接收來自這些工具所產生的 hello 警示。 不過，目前沒有方法 tooconfigure 傳入的警示資料使用 hello OMS 入口網站。 相反地，您將需要 tooedit 組態檔案 toostart 傳送警示 tooOMS。

### <a name="collect-alerts-from-nagios"></a>收集來自 Nagios 的警示
從 Nagios 伺服器 toocollect 警示，您需要下列設定變更 toomake hello。

1. 授與 hello 使用者**omsagent**讀取權限 toohello Nagios 記錄檔 (也就是 /var/log/nagios/nagios.log)。 假設 hello nagios.log 檔案由 hello 群組擁有**nagios** ，您可以加入 hello 使用者**omsagent** toohello **nagios**群組。

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. 修改 hello omsagent.confconfiguration 檔案 (等/選擇/microsoft/omsagent /&lt;工作區識別碼&gt;/conf/omsagent.conf)。 請確定下列項目 hello 確實存在且未標成註解：

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
3. 重新啟動 hello omsagent 精靈：

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>收集來自 Zabbix 的警示
toocollect 警示 Zabbix 伺服器，只不過您必須 toospecify 使用者和密碼，您將會如上述，Nagios 執行類似的步驟 toothose*純文字*。 這不是理想的做法，可能很快就會變更。 tooaddress 此問題，我們建議您建立 hello 使用者並授與其權限 toomonitor 只。

Hello omsagent.conf 組態檔中的範例 > 一節 (等/選擇/microsoft/omsagent /&lt;工作區識別碼&gt;/conf/omsagent.conf) 的 Zabbix 應該類似下列 hello:

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

### <a name="view-alerts-in-log-analytics-search"></a>在 Log Analytics 搜尋中檢視警示
設定 Linux 電腦 toosend 警示 tooOMS 之後，您可以使用幾個簡單的記錄搜尋查詢 tooview hello 警示。 hello 下列搜尋查詢範例會傳回所產生的所有記錄的 hello 警示。 例如，如果在您的 IT 基礎結構發生某種問題，然後對結果 hello 下列範例查詢可能表示 hello 問題可能產生的位置。 而且，您可以輕鬆地鑽研 toohello 警示中的半形的來源系統 toohelp 調查。 hello 好處是，您不一定需要 toogo toovarious 管理系統從 hello 開始，前提是您的警示傳送 tooOMS，您可以從那裡開始。

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview 記錄分析所有的 Nagios 警示
1. 在 hello Operations Management Suite 入口網站中，按一下 hello**記錄搜尋**磚。
2. 在 hello 查詢列中，輸入下列搜尋查詢的 hello

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![記錄檔搜尋中所顯示的 Nagios 警示](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

您會看到 hello 搜尋結果之後，您可以切入其他詳細資料這類*AlertState*。

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview 記錄分析所有的 Zabbix 警示
1. 在 hello Operations Management Suite 入口網站中，按一下 hello**記錄搜尋**磚。
2. 在 hello 查詢列中，輸入下列搜尋查詢的 hello

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![記錄檔搜尋中所顯示的 Zabbix 警示](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

您會看到 hello 搜尋結果之後，您可以切入其他詳細資料這類*AlertName*。

## <a name="compatibility-with-system-center-operations-manager"></a>與 System Center Operations Manager 的相容性
hello OMS Agent for Linux 與 hello System Center Operations Manager 代理程式共用代理程式二進位檔。 升級目前由 Operations Manager 管理的系統上，安裝 hello OMS Agent for Linux hello hello 電腦 tooa 較新版本的 OMI 和 SCX 封裝。 hello OMS Agent for Linux 和 System Center 2012 R2 都相容。 不過， **System Center 2012 SP1 和較早版本目前不是相容或支援以 hello OMS Agent for Linux。**

> [!NOTE]
> 如果 hello OMS Agent for Linux 安裝的 tooa 目前不是由 Operations Manager 管理的電腦，而且您稍後想 toomanage hello 電腦與 Operations Manager，您必須修改 hello OMI 設定才能探索 hello 電腦。 **如果之前 hello OMS Agent for Linux 安裝 hello Operations Manager 代理程式，不需要執行此步驟。**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>tooenable hello OMS Agent for Linux toocommunicate 與 Operations Manager
1. 編輯 hello 檔案 /etc/opt/omi/conf/omiserver.conf
2. 請確定該 hello 行首**httpsport =**定義 hello 連接埠 1270年。 例如 `httpsport=1270`
3. 重新啟動 hello OMI 伺服器：

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>MySQL 效能計數器所需的資料庫權限
toogrant 權限 tooa MySQL 監視使用者，hello 授與的使用者必須具有 hello 'GRANT option' 權限，以及被授與的 hello 權限。

為了讓 MySQL 使用者 hello tooreturn 效能資料 hello 使用者需要存取 toohello 下列查詢：

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

此外 toothese 查詢 hello MySQL 使用者也需要下列預設資料表的選取存取 toohello:

* information_schema
* mysql

執行下列 grant 命令 hello 可以授與這些權限。

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>管理 MySQL 監視認證 hello 驗證檔案中
hello 面各節協助您管理 MySQL 認證。

### <a name="configure-hello-mysql-omi-provider"></a>設定 MySQL OMI 提供者 hello
hello MySQL OMI 提供者需要預先設定的 MySQL 使用者，並安裝 MySQL 用戶端程式庫中訂單 tooquery hello 效能/健全狀況資訊從 hello MySQL 執行個體。

### <a name="mysql-omi-authentication-file"></a>MySQL OMI 驗證檔案
MySQL OMI 提供者使用哪些繫結位址和連接埠 hello MySQL 執行個體正在接聽驗證檔案 toodetermine 和以及認證 toouse toogather 度量。 在安裝 hello MySQL OMI 提供者會掃描 MySQL my.cnf 組態檔 （預設位置） 繫結位址和連接埠和組 hello MySQL OMI 驗證檔案部分。

toocomplete 監視 MySQL 伺服器執行個體，將預先產生的 MySQL OMI 驗證檔案加入至 hello 正確的目錄。

### <a name="authentication-file-format"></a>驗證檔案格式
hello MySQL OMI 驗證檔案是文字檔，其中包含有關的資訊：

* Port
* 繫結位址
* MySQL 使用者名稱
* Base64 編碼的密碼

hello MySQL OMI 驗證檔案只授與產生它的讀取/寫入 toohello Linux 使用者的權限。

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

預設 MySQL OMI 驗證檔案包含預設執行個體和連接埠號碼，視何種資訊可用且剖析從 hello 找到 MySQL 組態檔。

hello 預設執行個體管理較為簡單，一部 Linux 主機上的多個 MySQL 執行個體表示 toomake 且由 hello 與連接埠 0 的執行個體所表示。 所有新增的執行個體將會繼承 hello 預設執行個體設定的內容。 例如，如果新增接聽通訊埠 '3308' 的 MySQL 執行個體，hello 預設執行個體的繫結位址、 使用者名稱和 Base64 編碼的密碼將會使用的 tootry 並監視 hello 接聽 3308 的執行個體。 如果 3308 上的 hello 執行個體是繫結 tooanother 位址使用 hello 相同的 MySQL 使用者名稱和密碼組僅 hello hello 重新指定需要繫結位址，而且 hello 其他屬性會被繼承。

Hello 驗證檔案的範例如下 hello 下列。

預設執行個體與連接埠為 3308 的執行個體：

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

預設執行個體與連接埠為 3308 的執行個體 + 不同 Base64 編碼的密碼：

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **屬性** | **說明** |
| --- | --- |
| Port |連接埠代表目前的連接埠 hello hello MySQL 執行個體正在接聽。  hello 連接埠 0 表示預設執行個體，會使用下列的 hello 內容。 |
| 繫結位址 |hello 繫結位址是 hello 目前的 MySQL 繫結位址 |
| username |這個 hello 使用者的使用者名稱 hello MySQL 您希望 toouse toomonitor hello MySQL 伺服器執行個體。 |
| Base64 編碼的密碼 |這是以 Base64 編碼的 hello MySQL 監視使用者的 hello 密碼。 |
| AutoUpdate |Hello MySQL OMI 提供者升級時 hello 提供者會重新掃描 hello my.cnf 檔案有變更，並覆寫 hello MySQL OMI 驗證檔案。 設定此旗標 tootrue 或視需要的更新 toohello MySQL OMI 驗證檔案。 |

#### <a name="authentication-file-location"></a>驗證檔案位置
hello MySQL OMI 驗證檔案應該位於下列位置的 hello 和名為"mysql auth":

/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth

hello 檔案 （和 auth/omsagent 目錄） 應該 hello omsagent 使用者所擁有。

## <a name="agent-logs"></a>代理程式記錄檔
hello hello OMS Agent for Linux 的記錄檔位於：

/var/opt/microsoft/omsagent/&lt;工作區識別碼&gt;/log/

hello 記錄檔中的 hello OMS Agent for Linux 的 omsconfig （代理程式組態） 程式位於：

/var/opt/microsoft/omsconfig/log/

Hello OMI 和 SCX 元件 （提供效能標準資料） 的記錄檔位於：

/var/opt/omi/log/ and /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>疑難排解 hello OMS Agent for Linux
使用下列資訊 toodiagnose hello 和疑難排解常見的問題。

如果無 hello 疑難排解這一節的資訊可協助您，您也可以使用下列資源 toohelp 解析 hello 您的問題。

* 具有頂級支援的客戶可以透過[頂級支援](https://premier.microsoft.com/)記錄支援案例
* Azure 支援合約客戶可以記錄的支援案例 hello [Azure 入口網站](https://manage.windowsazure.com/?getsupport=true)
* 將 [GitHub 問題](https://github.com/Microsoft/OMS-Agent-for-Linux/issues) 歸檔
* 意見反應的意見和問題報告 toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>重要記錄檔位置
| 檔案 | 路徑 |
| --- | --- |
| OMS Agent for Linux 記錄檔 |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| OMS Agent 組態記錄檔 |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>重要組態檔案
| 分類 | 檔案位置 |
| --- | --- |
| syslog |`/etc/syslog-ng/syslog-ng.conf`、`/etc/rsyslog.conf` 或 `/etc/rsyslog.d/95-omsagent.conf` |
| 效能、Nagios、Zabbix、OMS 輸出和一般代理程式 |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| 其他組態 |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> 編輯效能計數器的組態檔，而若已啟用 OMS 入口網站組態，則會覆寫 syslog。 您可以停用 hello OMS 入口網站 （適用於所有節點） 中的組態或單一執行 hello 下列節點：
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>啟用偵錯記錄
tooenable 偵錯記錄，您可以使用 hello OMS 輸出外掛程式和詳細資訊輸出。

#### <a name="oms-output-plugin"></a>OMS 輸出外掛程式
FluentD 允許 hello 外掛程式 toospecify 輸入與輸出不同的記錄層級的記錄層級。 toospecify OMS 輸出是不同的記錄層級編輯 hello 一般的代理程式設定在 hello`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`檔案。

附近的 hello 設定檔的 hello 底部，變更 hello`log_level`屬性從`info`太`debug`。

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

偵錯記錄可讓您 toosee 批次上傳 toohello OMS 服務分隔型別，資料項目和 toosend 所花費時間的數目。

*啟用偵錯的記錄檔範例︰*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>詳細資訊輸出
不使用 hello OMS 輸出外掛程式，您也可以輸出資料項目直接太`stdout`，這會顯示在 hello OMS Agent for Linux 記錄檔中。

在 hello OMS 一般的代理程式組態檔中`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`，註解外 hello OMS 加入輸出外掛程式`#`前面每一行。

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

下面 hello 輸出外掛程式，請移除 hello 藉由移除 hello 之後 > 一節中的 hello 註解`#`每一行的 hello 開頭的符號。

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>轉寄的 Syslog 訊息不會出現在 hello 記錄檔
#### <a name="probable-causes"></a>可能的原因
* hello 套用設定 toohello Linux 伺服器不會不允許傳送嗨設備的集合和/或記錄層級
* Syslog 不是被轉送正確 toohello Linux 伺服器
* 每秒所轉寄的訊息的 hello 數目太大的 hello OMS Agent for Linux toohandle hello 基底組態

#### <a name="resolutions"></a>解決方式
* 確認 hello hello OMS 入口網站中的設定 Syslog 有所有 hello 設備和 hello 正確的記錄層級
  * **OMS 入口網站 > 設定 > 資料 > Syslog**
* 請確認該原生的 syslog 訊息精靈 (`rsyslog`， `syslog-ng`) 是可以 tooreceive hello 轉送訊息
* 請檢查防火牆設定 hello Syslog 伺服器 tooensure 都不會封鎖訊息
* 模擬使用 hello Syslog 訊息 tooOMS`logger`命令-例如：
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>使用 proxy 時，連線 tooOMS 問題
#### <a name="probable-causes"></a>可能的原因
* hello proxy 可讓您指定安裝和設定 hello 代理程式時不正確
* hello OMS 服務端點不是資料中心中 whitelistested

#### <a name="resolutions"></a>解決方式
* 重新 hello OMS 代理程式安裝適用於 Linux 使用下列命令以 hello 選項 hello`-v`啟用。 這可讓透過 hello proxy toohello OMS 服務的 hello 代理程式的詳細資訊輸出。
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * 檢閱在 OMS proxy 的文件集 hello[用於 HTTP proxy 伺服器設定 hello 代理程式](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* 請確認該 hello 遵循 OMS 服務端點會在允許清單

| 代理程式資源 | 連接埠 |
| --- | --- |
| &#42;.ods.opinsights.azure.com |連接埠 443 |
| &#42;.oms.opinsights.azure.com |連接埠 443 |
| ods.systemcenteradvisor.com |連接埠 443 |
| &#42;.blob.core.windows.net/ |連接埠 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>上架時會顯示 403 錯誤
#### <a name="probable-causes"></a>可能的原因
* hello 日期和時間設定不正確的 Linux 伺服器上
* hello 工作區識別碼和使用的工作區金鑰不正確

#### <a name="resolution"></a>解決方案
* 驗證您的 Linux 伺服器 hello 與 hello 時間`date`命令。 Hello 資料大於或小於 15 分鐘從 hello 目前的時間，如果登入就會失敗。 toocorrect，更新 hello 日期及/或 Linux 伺服器的時區。
* hello 最新版 hello OMS Agent for Linux 通知您，如果時間差異會造成登入失敗
* 重新登入使用 hello 正確的工作區識別碼和工作區金鑰。 請參閱[使用 hello 命令列的上架](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)如需詳細資訊。

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>500 錯誤或 404 錯誤會出現在 hello 記錄檔中登入之後
這是在 hello 第一次上傳 Linux 資料到 OMS 工作區時，就會發生的已知的問題。 這不會影響正在傳送的資料或其他問題。 您可以忽略 hello 錯誤，當第一次登入。

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Nagios 資料不會出現在 hello OMS 入口網站
#### <a name="probable-causes"></a>可能的原因
* hello omsagent 使用者不具有權限 tooread 從 hello Nagios 記錄檔
* hello Nagios 來源和篩選區段仍然註 hello omsagent.conf 檔案中

#### <a name="resolutions"></a>解決方式
* 加入從 hello Nagios 檔案順序 tooread hello omsagent 使用者。 如需詳細資訊，請參閱 [Nagios 警示](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts)。
* 在 hello OMS Agent for Linux 一般的組態檔， `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`，請確認**兩者**hello 的 Nagios 來源和篩選的區段有註解中移除，下列範例類似 toohello。

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Linux 資料不會出現在 hello OMS 入口網站
#### <a name="probable-causes"></a>可能的原因
* 上架 toohello OMS 服務失敗
* OMS 服務會封鎖連接 toohello
* hello OMS Agent for Linux 資料會備份

#### <a name="resolutions"></a>解決方式
* 確認該入門訓練 toohello OMS 服務已成功驗證該 hello`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`存在。
* 重新登入使用 hello omsadmin.sh 命令列。 請參閱[使用 hello 命令列的上架](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)如需詳細資訊。
* 如果使用 proxy，使用 hello proxy 疑難排解上述步驟
* 在某些情況下，hello 適用於 Linux 的 OMS 代理程式無法與 hello OMS 服務通訊時 hello 代理程式上的資料會是備份 toohello 已滿的緩衝區大小為 50 MB。 Hello OMS Agent for Linux 啟動執行重新啟動 hello`/opt/microsoft/omsagent/bin/service_control restart`命令。
  >[AZURE.NOTE] 此問題已在代理程式 1.1.0-28 版和更新版本中修正。

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Syslog Linux 效能計數器組態不會套用在 hello OMS 入口網站
#### <a name="probable-causes"></a>可能的原因
* 在 hello OMS Agent for Linux hello 設定代理程式並未從 hello OMS 入口網站擷取 hello 最新的設定。
* hello hello 入口網站中修改過的設定未套用

#### <a name="resolutions"></a>解決方式
`omsconfig`是 hello 設定代理程式在 hello OMS Agent for Linux，擷取 OMS 入口網站的組態變更每隔 5 分鐘。 此設定，然後套用的 toohello OMS Agent for Linux 設定檔位於`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`。

* 在某些情況下，hello OMS Agent for Linux 設定代理程式可能不能 toocommunicate 不套用最新的組態中所產生的 hello 入口網站設定服務。
* 請確認該 hello `omsconfig` hello 下列已安裝的代理程式：

  * `dpkg --list omsconfig` 或 `rpm -qi omsconfig`
  * 如果未安裝，重新安裝 hello 最新版 hello OMS Agent for Linux
* 請確認該 hello`omsconfig`代理程式可以與 hello OMS 服務通訊

  * 執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`命令
    * hello 上述命令會傳回 hello 設定該代理程式擷取 hello 入口網站，包括 Syslog 設定、 Linux 效能計數器，以及自訂記錄檔
    * 如果上述 hello 命令失敗，執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`命令。 此命令會強制 hello omsconfig 代理程式 toocommunicate 與 hello OMS 服務 tooretrieve hello 最新組態。

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>自訂的 Linux 記錄檔資料不會出現在 hello OMS 入口網站
#### <a name="probable-causes"></a>可能的原因
* 上架 tooOMS 服務失敗
* hello**套用下列組態 toomy Linux 伺服器的 hello**不選取設定
* omsconfig 不挑選 hello 最新自訂的記錄從 hello 入口網站
* hello`omsagent`使用已到期，tooa 權限問題無法 tooaccess hello 自訂記錄或`omsagent`找不到。 在此情況下，您會看到下列輸出的 hello:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* 這是以 hello 競爭 hello OMS Agent for Linux 版本 1.1.0-217 中已修正的已知的問題

#### <a name="resolutions"></a>解決方式
* 請確認您已順利就緒、 判斷是否 hello`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`檔案是否存在。
  * 必要時，使用 hello omsadmin.sh 命令列再次登入。 請參閱[使用 hello 命令列的上架](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)如需詳細資訊。
* 在 hello OMS 入口網站，在**設定**上 hello**資料**索引標籤，確定該 hello**套用下列組態 toomy Linux 伺服器的 hello**選取設定  
  ![套用組態](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* 請確認該 hello`omsconfig`代理程式可以與 hello OMS 服務通訊

  * 執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`命令
  * hello 上述命令會傳回 hello 設定該代理程式從 hello 入口網站，包括 Syslog 設定、 Linux 效能計數器，以及自訂記錄檔中的擷取
  * 如果上述 hello 命令失敗，執行 hello`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`命令。 此命令會強制 hello omsconfig 代理程式 toocommunicate 與 OMS 服務，並擷取 hello 最新的設定。

而不是 hello OMS Agent for Linux 使用者的特殊權限的使用者身分執行`root`，hello OMS Agent for Linux 執行 hello`omsagent`使用者。 在大部分情況下，必須明確權限授與順序 tooread toohello 使用者特定的檔案。

toogrant 權限太`omsagent`使用者，執行下列命令的 hello:

1. 新增 hello`omsagent`使用者 tooa 特定群組`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. 授與具有通用的讀取權限 toohello 必要的檔案`sudo chmod -R ugo+rw <FILE DIRECTORY>`

沒有 hello 競爭 hello OMS Agent for Linux 版本 1.1.0-217 中已修正的已知的問題。 在更新之後 toohello 最新的代理程式，執行下列命令 tooget hello 最新版本的 hello 輸出外掛程式 hello:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>已知限制
請檢閱下列有關目前限制的 hello OMS Agent for Linux 區段 toolearn hello。

### <a name="azure-diagnostics"></a>Azure 診斷
在 Azure 中執行的 Linux 虛擬機器，額外的步驟可能需要的 tooallow 資料收集 Azure 診斷和 Operations Management Suite 的資訊。 **2.2 版**的 hello Diagnostics Extension for Linux 做是為了與 hello OMS Agent for Linux 相容性。

如需有關安裝和設定適用於 Linux 的 hello 診斷延伸模組的詳細資訊，請參閱[使用 hello Azure CLI 命令 tooenable Linux 診斷延伸模組](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension)。

**升級 hello Linux 診斷延伸模組從 2.0 too2.2 Azure CLI ASM:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

這些命令範例參考名為 PrivateConfig.json 的檔案。 hello 該檔案格式應該類似下列範例中的 hello。

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>不支援 Sysklog
需要 rsyslog 或 syslog-ng 是必要的 toocollect syslog 訊息。 在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。 toocollect syslog 資料，從這一版的這些發佈，hello rsyslog 精靈應該安裝和設定 tooreplace sysklog。 如需有關以 rsyslog 取代 sysklog 的詳細資訊，請參閱[安裝 hello 新建立的 rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM)。

## <a name="next-steps"></a>後續步驟
* [新增記錄分析解決方案從 hello 解決方案資源庫](log-analytics-add-solutions.md)tooadd 功能和收集資料。
* 讓您熟悉[記錄搜尋](log-analytics-log-searches.md)tooview 詳細解決方案所收集的資訊。
* 使用[儀表板](log-analytics-dashboards.md)toosave 並顯示您自己的自訂搜尋。
