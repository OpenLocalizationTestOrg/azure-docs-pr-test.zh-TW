---
title: "aaaCollect 和分析 OMS 記錄分析的 Syslog 訊息 |Microsoft 文件"
description: "Syslog 是常見的 tooLinux 的事件記錄通訊協定。 這篇文章描述如何記錄分析的 Syslog 訊息 tooconfigure 集合以及的 hello 記錄詳細資料它們建立 hello OMS 儲存機制中。"
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Log Analytics 中的 Syslog 資料來源
Syslog 是常見的 tooLinux 的事件記錄通訊協定。  應用程式會傳送 hello 本機電腦上儲存或傳遞 tooa Syslog 收集器的訊息。  Hello OMS Agent for Linux 安裝時，它會設定 hello 本機 Syslog 服務精靈 tooforward 訊息 toohello 代理程式。  hello 代理程式接著會傳送 hello 訊息 tooLog 分析 hello OMS 儲存機制中建立對應的記錄的位置。  

> [!NOTE]
> 記錄分析支援 rsyslog 所在 hello 預設服務精靈所 rsyslog 或 syslog-ng 週日，傳送訊息的集合。 在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。 toocollect syslog 資料，從這一版的這些發佈，hello [rsyslog 精靈](http://rsyslog.com)應該安裝和設定 tooreplace sysklog。
>
>

![Syslog 收集](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>設定 Syslog
hello OMS Agent for Linux 只會收集 hello 設備與嚴重性其組態中指定的事件。  您可以設定 Syslog 透過 hello OMS 入口網站或管理您的 Linux 代理程式上的組態檔。

### <a name="configure-syslog-in-hello-oms-portal"></a>在 hello OMS 入口網站中設定 Syslog
設定 Syslog 從 hello[資料記錄分析設定 功能表](log-analytics-data-sources.md#configuring-data-sources)。  此組態會傳遞 toohello 上每個 Linux 代理程式的組態檔。

您可以輸入新設備的名稱，然後按一下 **+**設定 Syslog。  每個功能，將會收集僅選取 hello 嚴重性的訊息。  請檢查您想 toocollect hello 特定功能的 hello 嚴重性。  您無法提供任何其他準則 toofilter 訊息。

![設定 Syslog](media/log-analytics-data-sources-syslog/configure.png)

根據預設，所有的組態變更會自動推入 tooall 代理程式。  如果您想在每個 Linux 代理程式上手動 tooconfigure Syslog，並取消核取方塊 hello*套用下列組態 toomy Linux 電腦*。

### <a name="configure-syslog-on-linux-agent"></a>在 Linux 代理程式上設定 Syslog
當 hello [Linux 用戶端上安裝 OMS 代理程式](log-analytics-linux-agents.md)、 安裝定義 hello 設備的預設 syslog 組態檔和嚴重性 hello 訊息被收集。  您可以修改這個檔案 toochange hello 組態。  hello 組態檔是 hello Syslog hello 用戶端的服務精靈已安裝而有所不同。

> [!NOTE]
> 如果您編輯 hello syslog 設定，您必須重新啟動 hello 變更 tootake 效果 hello syslog 服務精靈。
>
>

#### <a name="rsyslog"></a>rsyslog
hello rsyslog 的組態檔是位於**/etc/rsyslog.d/95-omsagent.conf**。  其預設內容如下所示。  這會收集從 hello 本機代理程式傳送的層級的警告或更高版本的所有設備的 syslog 訊息。

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

您可以藉由移除 hello 設定檔 > 一節移除設備。  您可以限制收集特定功能的修改該設備項目 hello 嚴重性。  比方說，toolimit hello 使用者或更高的錯誤嚴重性的設備 toomessages 您修改下列 hello 設定檔 toohello 該行：

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>syslog-ng
syslog ng hello 組態檔是位於位置**/etc/syslog-ng/syslog-ng.conf**。  其預設內容如下所示。  這會收集 syslog 訊息從 hello 本機代理程式傳送的所有功能和所有的嚴重性。   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

您可以藉由移除 hello 設定檔 > 一節移除設備。  您可以限制從其清單中移除特定功能所收集的 hello 嚴重性。  例如，toolimit hello 使用者設備 toojust 警示和重大訊息會修改該區段的 hello 設定檔 toohello 遵循：

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>從其他 Syslog 連接埠收集資料
hello OMS 代理程式會接聽連接埠 25224 的 hello 本機用戶端上的 Syslog 訊息。  Hello 代理程式安裝時，是套用預設 syslog 組態，並位於下列位置的 hello:

* Rsyslog：`/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng：`/etc/syslog-ng/syslog-ng.conf`

您可以藉由建立兩個組態檔變更 hello 連接埠號碼： FluentD 組態檔和 rsyslog-或-syslog-ng 檔案根據已安裝的 hello Syslog 服務精靈。  

* hello FluentD 組態檔應該是新的檔案位於： `/etc/opt/microsoft/omsagent/conf/omsagent.d` hello hello 中的值，取代成**連接埠**與自訂連接埠號碼的項目。

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* 您應針對 rsyslog，建立新的組態檔位於：`/etc/rsyslog.d/`和 hello 值 %syslog_port%取代為您的自訂連接埠號碼。  

    > [!NOTE]
    > 如果您修改這個值在 hello 組態檔中的`95-omsagent.conf`，它將會覆寫 hello 代理程式會套用預設組態。
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* hello syslog ng 組態應該修改複製 hello 範例組態，如下所示，並加入 hello 已修改的自訂設定 toohello 結尾 hello syslog ng.conf 組態檔位於`/etc/syslog-ng/`。  請勿**不**使用 hello 預設標籤**%workspace_id%_oms**或**%workspace_id_oms**，定義自訂標籤 toohelp 區別您的變更。  

    > [!NOTE]
    > 如果您修改 hello hello 組態檔中的預設值，它們將會覆寫 hello 代理程式會套用預設組態。
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

之後完成的 hello 變更、 hello Syslog 和 hello OMS 代理程式服務必須重新啟動 toobe tooensure hello 組態變更生效。   

## <a name="syslog-record-properties"></a>Syslog 記錄屬性
Syslog 記錄都有一種**Syslog**和 hello 下表中都有 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 電腦 |從收集 hello 事件的電腦。 |
| Facility |定義 hello hello 系統產生 hello 訊息的一部分。 |
| HostIP |Hello 系統傳送 hello 訊息的 IP 位址。 |
| HostName |Hello 系統傳送 hello 訊息的名稱。 |
| SeverityLevel |Hello 事件嚴重性層級。 |
| SyslogMessage |Hello 訊息的文字。 |
| ProcessID |產生 hello 訊息的 hello 處理序識別碼。 |
| EventTime |日期和時間 hello 事件所產生。 |

## <a name="log-queries-with-syslog-records"></a>含有 Syslog 記錄的記錄查詢
hello 下表提供不同擷取 Syslog 記錄的記錄檔查詢的範例。

| 查詢 | 說明 |
|:--- |:--- |
| Type=Syslog |所有的 Syslog。 |
| Type=Syslog SeverityLevel=error |嚴重性為錯誤的所有 Syslog 記錄。 |
| Type=Syslog &#124; measure count() by Computer |依電腦的 Syslog 記錄計數。 |
| Type=Syslog &#124; measure count() by Facility |依設備的 Syslog 記錄計數。 |

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。

> | 查詢 | 說明 |
|:--- |:--- |
| syslog |所有的 Syslog。 |
| Syslog &#124; where SeverityLevel == "error" |嚴重性為錯誤的所有 Syslog 記錄。 |
| Syslog &#124; summarize AggregatedValue = count() by Computer |依電腦的 Syslog 記錄計數。 |
| Syslog &#124; summarize AggregatedValue = count() by Facility |依設備的 Syslog 記錄計數。 |

## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。
* 使用[自訂欄位](log-analytics-custom-fields.md)tooparse syslog 記錄，到個別欄位的資料。
* [設定 Linux 代理程式](log-analytics-linux-agents.md)toocollect 其他類型的資料。
