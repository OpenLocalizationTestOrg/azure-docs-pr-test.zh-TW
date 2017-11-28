---
title: "收集與分析 OMS Log Analytics 中的 Syslog 訊息 | Microsoft Docs"
description: "Syslog 是通用於 Linux 的事件記錄通訊協定。 本文說明如何在 Log Analytics 中設定收集 Syslog 訊息，以及它們在 OMS 儲存機制中建立的記錄詳細資料。"
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
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="aafc3-104">Log Analytics 中的 Syslog 資料來源</span><span class="sxs-lookup"><span data-stu-id="aafc3-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="aafc3-105">Syslog 是通用於 Linux 的事件記錄通訊協定。</span><span class="sxs-lookup"><span data-stu-id="aafc3-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="aafc3-106">應用程式將傳送的訊息可能會儲存在本機電腦上，或傳遞到 Syslog 收集器。</span><span class="sxs-lookup"><span data-stu-id="aafc3-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="aafc3-107">安裝 OMS Agent for Linux 時，它會設定本機 Syslog 精靈來將訊息轉送到代理程式。</span><span class="sxs-lookup"><span data-stu-id="aafc3-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="aafc3-108">接著，代理程式會將訊息傳送到 Log Analytics，其中對應的記錄會建立於 OMS 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="aafc3-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="aafc3-109">Log Analytics 支援收集由 rsyslog 或 syslog-ng 所傳送的訊息，其中 rsyslog 是預設精靈。</span><span class="sxs-lookup"><span data-stu-id="aafc3-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="aafc3-110">Red Hat Enterprise Linux 第 5 版、CentOS 和 Oracle Linux 版本 (sysklog) 不支援預設 syslog 精靈，進行 syslog 事件收集。</span><span class="sxs-lookup"><span data-stu-id="aafc3-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="aafc3-111">若要從這些散發套件的這個版本收集 syslog 資料，應該安裝並設定 [rsyslog 精靈](http://rsyslog.com) 來取代 sysklog。</span><span class="sxs-lookup"><span data-stu-id="aafc3-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Syslog 收集](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="aafc3-113">設定 Syslog</span><span class="sxs-lookup"><span data-stu-id="aafc3-113">Configuring Syslog</span></span>
<span data-ttu-id="aafc3-114">OMS Agent for Linux 只會收集具有其組態中指定之設備和嚴重性的事件。</span><span class="sxs-lookup"><span data-stu-id="aafc3-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="aafc3-115">您可以透過 OMS 入口網站，或藉由管理您 Linux 代理程式上的組態檔來設定 Syslog。</span><span class="sxs-lookup"><span data-stu-id="aafc3-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="aafc3-116">在 OMS 入口網站中設定 Syslog</span><span class="sxs-lookup"><span data-stu-id="aafc3-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="aafc3-117">從 [Log Analytics 設定中的 [資料] 功能表](log-analytics-data-sources.md#configuring-data-sources)設定 Syslog。</span><span class="sxs-lookup"><span data-stu-id="aafc3-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="aafc3-118">這個組態會傳遞到每個 Linux 代理程式上的組態檔。</span><span class="sxs-lookup"><span data-stu-id="aafc3-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="aafc3-119">您可以輸入新設備的名稱，然後按一下 **+**設定 Syslog。</span><span class="sxs-lookup"><span data-stu-id="aafc3-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="aafc3-120">針對每個設備，僅會收集包含所選嚴重性的訊息。</span><span class="sxs-lookup"><span data-stu-id="aafc3-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="aafc3-121">請檢查您想要收集之特定設備的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="aafc3-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="aafc3-122">您無法提供任何其他準則來篩選訊息。</span><span class="sxs-lookup"><span data-stu-id="aafc3-122">You cannot provide any additional criteria to filter messages.</span></span>

![設定 Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="aafc3-124">根據預設，所有設定變更都會自動發送給所有代理程式。</span><span class="sxs-lookup"><span data-stu-id="aafc3-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="aafc3-125">如果您想在每個 Linux 代理程式上手動設定 Syslog，則可取消核取 *[Apply below configuration to my Linux machines]* \(將下列設定套用至我的 Linux 機器) 方塊。</span><span class="sxs-lookup"><span data-stu-id="aafc3-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="aafc3-126">在 Linux 代理程式上設定 Syslog</span><span class="sxs-lookup"><span data-stu-id="aafc3-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="aafc3-127">當 [OMS 代理程式安裝於 Linux 用戶端](log-analytics-linux-agents.md)時，它會安裝預設的 syslog 組態檔，其中會定義所收集之資訊的設備和嚴重性。</span><span class="sxs-lookup"><span data-stu-id="aafc3-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="aafc3-128">您可以修改此檔案來變更組態。</span><span class="sxs-lookup"><span data-stu-id="aafc3-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="aafc3-129">組態檔會根據用戶端已安裝的 Syslog 精靈而有所不同。</span><span class="sxs-lookup"><span data-stu-id="aafc3-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="aafc3-130">如果您編輯 syslog 組態，則必須重新啟動 syslog 精靈，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="aafc3-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="aafc3-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="aafc3-131">rsyslog</span></span>
<span data-ttu-id="aafc3-132">Rsyslog 的組態檔位於 **/etc/rsyslog.d/95-omsagent.conf**。</span><span class="sxs-lookup"><span data-stu-id="aafc3-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="aafc3-133">其預設內容如下所示。</span><span class="sxs-lookup"><span data-stu-id="aafc3-133">Its default contents are shown below.</span></span>  <span data-ttu-id="aafc3-134">這會針對層級為警告或以上的所有設備收集傳送自本機代理程式的 syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="aafc3-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="aafc3-135">您可以藉由移除組態檔的設備區段來移除該設備。</span><span class="sxs-lookup"><span data-stu-id="aafc3-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="aafc3-136">您可以藉由修改特定設備的項目，來限制針對該設備所收集的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="aafc3-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="aafc3-137">例如，若要將使用者設備限制為嚴重性為錯誤或以上的訊息，您要將組態檔的那一行修改為下列內容：</span><span class="sxs-lookup"><span data-stu-id="aafc3-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="aafc3-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="aafc3-138">syslog-ng</span></span>
<span data-ttu-id="aafc3-139">Syslog-ng 的組態檔位於 **/etc/syslog-ng/syslog-ng.conf**。</span><span class="sxs-lookup"><span data-stu-id="aafc3-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="aafc3-140">其預設內容如下所示。</span><span class="sxs-lookup"><span data-stu-id="aafc3-140">Its default contents are shown below.</span></span>  <span data-ttu-id="aafc3-141">這會針對所有設備和所有嚴重性收集傳送自本機代理程式的 syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="aafc3-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="aafc3-142">您可以藉由移除組態檔的設備區段來移除該設備。</span><span class="sxs-lookup"><span data-stu-id="aafc3-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="aafc3-143">您可以限制針對特定設備收集的嚴重性，方法是從其清單中移除它們。</span><span class="sxs-lookup"><span data-stu-id="aafc3-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="aafc3-144">例如，若要將使用者設備限制為只有警示和重大訊息，您要將組態檔的那一個區段修改為下列內容：</span><span class="sxs-lookup"><span data-stu-id="aafc3-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="aafc3-145">從其他 Syslog 連接埠收集資料</span><span class="sxs-lookup"><span data-stu-id="aafc3-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="aafc3-146">OMS 代理程式會在本機用戶端的連接埠 25224 上接聽 Syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="aafc3-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="aafc3-147">安裝代理程式時，會套用預設 syslog 組態，並可在下列位置找到：</span><span class="sxs-lookup"><span data-stu-id="aafc3-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="aafc3-148">Rsyslog：`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="aafc3-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="aafc3-149">Syslog-ng：`/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="aafc3-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="aafc3-150">您可以變更連接埠號碼，方法是建立兩個組態檔：FluentD 組態檔和 rsyslog-or-syslog-ng 檔案，依您已安裝的 Syslog 精靈而定。</span><span class="sxs-lookup"><span data-stu-id="aafc3-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="aafc3-151">FluentD 組態檔應該是新的檔案，位於：`/etc/opt/microsoft/omsagent/conf/omsagent.d`，且會將**連接埠**項目中的值取代為自訂連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="aafc3-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="aafc3-152">針對 rsyslog，您應建立新的組態檔，位於：`/etc/rsyslog.d/`，並將 %SYSLOG_PORT% 值取代為您的自訂連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="aafc3-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="aafc3-153">如果您在 `95-omsagent.conf` 組態檔中修改這個值，就會在代理程式套用預設組態時將它覆寫。</span><span class="sxs-lookup"><span data-stu-id="aafc3-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="aafc3-154">應修改 syslog ng 組態，方法是複製如下所示的範例組態，並將自訂修改的設定新增至位於 `/etc/syslog-ng/` 之 syslog ng.conf 組態檔的結尾。</span><span class="sxs-lookup"><span data-stu-id="aafc3-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="aafc3-155">請**勿**使用預設標籤 **%workspace_id%_oms** 或 **%workspace_id_oms**，定義自訂標籤可協助您辨別變更。</span><span class="sxs-lookup"><span data-stu-id="aafc3-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="aafc3-156">如果您在組態檔中修改預設值，就會在代理程式套用預設組態時將它覆寫。</span><span class="sxs-lookup"><span data-stu-id="aafc3-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="aafc3-157">完成變更後，必須將 Syslog 和 OMS 代理程式服務重新啟動，才能確保組態變更生效。</span><span class="sxs-lookup"><span data-stu-id="aafc3-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="aafc3-158">Syslog 記錄屬性</span><span class="sxs-lookup"><span data-stu-id="aafc3-158">Syslog record properties</span></span>
<span data-ttu-id="aafc3-159">Syslog 記錄具有 **Syslog** 類型，以及下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="aafc3-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="aafc3-160">屬性</span><span class="sxs-lookup"><span data-stu-id="aafc3-160">Property</span></span> | <span data-ttu-id="aafc3-161">說明</span><span class="sxs-lookup"><span data-stu-id="aafc3-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="aafc3-162">電腦</span><span class="sxs-lookup"><span data-stu-id="aafc3-162">Computer</span></span> |<span data-ttu-id="aafc3-163">收集事件的來源電腦。</span><span class="sxs-lookup"><span data-stu-id="aafc3-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="aafc3-164">Facility</span><span class="sxs-lookup"><span data-stu-id="aafc3-164">Facility</span></span> |<span data-ttu-id="aafc3-165">定義產生訊息之系統的一部分。</span><span class="sxs-lookup"><span data-stu-id="aafc3-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="aafc3-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="aafc3-166">HostIP</span></span> |<span data-ttu-id="aafc3-167">傳送訊息之系統的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aafc3-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="aafc3-168">HostName</span><span class="sxs-lookup"><span data-stu-id="aafc3-168">HostName</span></span> |<span data-ttu-id="aafc3-169">傳送訊息之系統的名稱。</span><span class="sxs-lookup"><span data-stu-id="aafc3-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="aafc3-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="aafc3-170">SeverityLevel</span></span> |<span data-ttu-id="aafc3-171">事件的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="aafc3-171">Severity level of the event.</span></span> |
| <span data-ttu-id="aafc3-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="aafc3-172">SyslogMessage</span></span> |<span data-ttu-id="aafc3-173">訊息的文字。</span><span class="sxs-lookup"><span data-stu-id="aafc3-173">Text of the message.</span></span> |
| <span data-ttu-id="aafc3-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="aafc3-174">ProcessID</span></span> |<span data-ttu-id="aafc3-175">產生訊息的處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="aafc3-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="aafc3-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="aafc3-176">EventTime</span></span> |<span data-ttu-id="aafc3-177">產生事件的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="aafc3-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="aafc3-178">含有 Syslog 記錄的記錄查詢</span><span class="sxs-lookup"><span data-stu-id="aafc3-178">Log queries with Syslog records</span></span>
<span data-ttu-id="aafc3-179">下表提供擷取 Syslog 記錄的不同記錄查詢範例。</span><span class="sxs-lookup"><span data-stu-id="aafc3-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="aafc3-180">查詢</span><span class="sxs-lookup"><span data-stu-id="aafc3-180">Query</span></span> | <span data-ttu-id="aafc3-181">說明</span><span class="sxs-lookup"><span data-stu-id="aafc3-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="aafc3-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="aafc3-182">Type=Syslog</span></span> |<span data-ttu-id="aafc3-183">所有的 Syslog。</span><span class="sxs-lookup"><span data-stu-id="aafc3-183">All Syslogs.</span></span> |
| <span data-ttu-id="aafc3-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="aafc3-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="aafc3-185">嚴重性為錯誤的所有 Syslog 記錄。</span><span class="sxs-lookup"><span data-stu-id="aafc3-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="aafc3-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="aafc3-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="aafc3-187">依電腦的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="aafc3-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="aafc3-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="aafc3-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="aafc3-189">依設備的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="aafc3-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="aafc3-190">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。</span><span class="sxs-lookup"><span data-stu-id="aafc3-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="aafc3-191">查詢</span><span class="sxs-lookup"><span data-stu-id="aafc3-191">Query</span></span> | <span data-ttu-id="aafc3-192">說明</span><span class="sxs-lookup"><span data-stu-id="aafc3-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="aafc3-193">syslog</span><span class="sxs-lookup"><span data-stu-id="aafc3-193">Syslog</span></span> |<span data-ttu-id="aafc3-194">所有的 Syslog。</span><span class="sxs-lookup"><span data-stu-id="aafc3-194">All Syslogs.</span></span> |
| <span data-ttu-id="aafc3-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="aafc3-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="aafc3-196">嚴重性為錯誤的所有 Syslog 記錄。</span><span class="sxs-lookup"><span data-stu-id="aafc3-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="aafc3-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="aafc3-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="aafc3-198">依電腦的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="aafc3-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="aafc3-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="aafc3-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="aafc3-200">依設備的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="aafc3-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aafc3-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aafc3-201">Next steps</span></span>
* <span data-ttu-id="aafc3-202">了解 [記錄搜尋](log-analytics-log-searches.md) ，以分析從資料來源和解決方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="aafc3-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="aafc3-203">使用 [自訂欄位](log-analytics-custom-fields.md) ，以將來自 syslog 記錄的資料剖析至個別欄位。</span><span class="sxs-lookup"><span data-stu-id="aafc3-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="aafc3-204">[設定 Linux 代理程式](log-analytics-linux-agents.md) ，以收集其他類型的資料。</span><span class="sxs-lookup"><span data-stu-id="aafc3-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
