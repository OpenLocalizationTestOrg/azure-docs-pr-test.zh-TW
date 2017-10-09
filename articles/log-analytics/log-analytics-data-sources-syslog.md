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
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="5d7cc-104">Log Analytics 中的 Syslog 資料來源</span><span class="sxs-lookup"><span data-stu-id="5d7cc-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="5d7cc-105">Syslog 是常見的 tooLinux 的事件記錄通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="5d7cc-106">應用程式會傳送 hello 本機電腦上儲存或傳遞 tooa Syslog 收集器的訊息。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="5d7cc-107">Hello OMS Agent for Linux 安裝時，它會設定 hello 本機 Syslog 服務精靈 tooforward 訊息 toohello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="5d7cc-108">hello 代理程式接著會傳送 hello 訊息 tooLog 分析 hello OMS 儲存機制中建立對應的記錄的位置。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="5d7cc-109">記錄分析支援 rsyslog 所在 hello 預設服務精靈所 rsyslog 或 syslog-ng 週日，傳送訊息的集合。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="5d7cc-110">在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="5d7cc-111">toocollect syslog 資料，從這一版的這些發佈，hello [rsyslog 精靈](http://rsyslog.com)應該安裝和設定 tooreplace sysklog。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Syslog 收集](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="5d7cc-113">設定 Syslog</span><span class="sxs-lookup"><span data-stu-id="5d7cc-113">Configuring Syslog</span></span>
<span data-ttu-id="5d7cc-114">hello OMS Agent for Linux 只會收集 hello 設備與嚴重性其組態中指定的事件。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="5d7cc-115">您可以設定 Syslog 透過 hello OMS 入口網站或管理您的 Linux 代理程式上的組態檔。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="5d7cc-116">在 hello OMS 入口網站中設定 Syslog</span><span class="sxs-lookup"><span data-stu-id="5d7cc-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="5d7cc-117">設定 Syslog 從 hello[資料記錄分析設定 功能表](log-analytics-data-sources.md#configuring-data-sources)。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="5d7cc-118">此組態會傳遞 toohello 上每個 Linux 代理程式的組態檔。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="5d7cc-119">您可以輸入新設備的名稱，然後按一下 **+**設定 Syslog。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="5d7cc-120">每個功能，將會收集僅選取 hello 嚴重性的訊息。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="5d7cc-121">請檢查您想 toocollect hello 特定功能的 hello 嚴重性。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="5d7cc-122">您無法提供任何其他準則 toofilter 訊息。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-122">You cannot provide any additional criteria toofilter messages.</span></span>

![設定 Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="5d7cc-124">根據預設，所有的組態變更會自動推入 tooall 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="5d7cc-125">如果您想在每個 Linux 代理程式上手動 tooconfigure Syslog，並取消核取方塊 hello*套用下列組態 toomy Linux 電腦*。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="5d7cc-126">在 Linux 代理程式上設定 Syslog</span><span class="sxs-lookup"><span data-stu-id="5d7cc-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="5d7cc-127">當 hello [Linux 用戶端上安裝 OMS 代理程式](log-analytics-linux-agents.md)、 安裝定義 hello 設備的預設 syslog 組態檔和嚴重性 hello 訊息被收集。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="5d7cc-128">您可以修改這個檔案 toochange hello 組態。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="5d7cc-129">hello 組態檔是 hello Syslog hello 用戶端的服務精靈已安裝而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="5d7cc-130">如果您編輯 hello syslog 設定，您必須重新啟動 hello 變更 tootake 效果 hello syslog 服務精靈。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="5d7cc-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="5d7cc-131">rsyslog</span></span>
<span data-ttu-id="5d7cc-132">hello rsyslog 的組態檔是位於**/etc/rsyslog.d/95-omsagent.conf**。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="5d7cc-133">其預設內容如下所示。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-133">Its default contents are shown below.</span></span>  <span data-ttu-id="5d7cc-134">這會收集從 hello 本機代理程式傳送的層級的警告或更高版本的所有設備的 syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="5d7cc-135">您可以藉由移除 hello 設定檔 > 一節移除設備。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="5d7cc-136">您可以限制收集特定功能的修改該設備項目 hello 嚴重性。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="5d7cc-137">比方說，toolimit hello 使用者或更高的錯誤嚴重性的設備 toomessages 您修改下列 hello 設定檔 toohello 該行：</span><span class="sxs-lookup"><span data-stu-id="5d7cc-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="5d7cc-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="5d7cc-138">syslog-ng</span></span>
<span data-ttu-id="5d7cc-139">syslog ng hello 組態檔是位於位置**/etc/syslog-ng/syslog-ng.conf**。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="5d7cc-140">其預設內容如下所示。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-140">Its default contents are shown below.</span></span>  <span data-ttu-id="5d7cc-141">這會收集 syslog 訊息從 hello 本機代理程式傳送的所有功能和所有的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="5d7cc-142">您可以藉由移除 hello 設定檔 > 一節移除設備。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="5d7cc-143">您可以限制從其清單中移除特定功能所收集的 hello 嚴重性。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="5d7cc-144">例如，toolimit hello 使用者設備 toojust 警示和重大訊息會修改該區段的 hello 設定檔 toohello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5d7cc-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="5d7cc-145">從其他 Syslog 連接埠收集資料</span><span class="sxs-lookup"><span data-stu-id="5d7cc-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="5d7cc-146">hello OMS 代理程式會接聽連接埠 25224 的 hello 本機用戶端上的 Syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="5d7cc-147">Hello 代理程式安裝時，是套用預設 syslog 組態，並位於下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d7cc-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="5d7cc-148">Rsyslog：`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="5d7cc-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="5d7cc-149">Syslog-ng：`/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="5d7cc-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="5d7cc-150">您可以藉由建立兩個組態檔變更 hello 連接埠號碼： FluentD 組態檔和 rsyslog-或-syslog-ng 檔案根據已安裝的 hello Syslog 服務精靈。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="5d7cc-151">hello FluentD 組態檔應該是新的檔案位於： `/etc/opt/microsoft/omsagent/conf/omsagent.d` hello hello 中的值，取代成**連接埠**與自訂連接埠號碼的項目。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="5d7cc-152">您應針對 rsyslog，建立新的組態檔位於：`/etc/rsyslog.d/`和 hello 值 %syslog_port%取代為您的自訂連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="5d7cc-153">如果您修改這個值在 hello 組態檔中的`95-omsagent.conf`，它將會覆寫 hello 代理程式會套用預設組態。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="5d7cc-154">hello syslog ng 組態應該修改複製 hello 範例組態，如下所示，並加入 hello 已修改的自訂設定 toohello 結尾 hello syslog ng.conf 組態檔位於`/etc/syslog-ng/`。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="5d7cc-155">請勿**不**使用 hello 預設標籤**%workspace_id%_oms**或**%workspace_id_oms**，定義自訂標籤 toohelp 區別您的變更。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="5d7cc-156">如果您修改 hello hello 組態檔中的預設值，它們將會覆寫 hello 代理程式會套用預設組態。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="5d7cc-157">之後完成的 hello 變更、 hello Syslog 和 hello OMS 代理程式服務必須重新啟動 toobe tooensure hello 組態變更生效。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="5d7cc-158">Syslog 記錄屬性</span><span class="sxs-lookup"><span data-stu-id="5d7cc-158">Syslog record properties</span></span>
<span data-ttu-id="5d7cc-159">Syslog 記錄都有一種**Syslog**和 hello 下表中都有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="5d7cc-160">屬性</span><span class="sxs-lookup"><span data-stu-id="5d7cc-160">Property</span></span> | <span data-ttu-id="5d7cc-161">說明</span><span class="sxs-lookup"><span data-stu-id="5d7cc-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5d7cc-162">電腦</span><span class="sxs-lookup"><span data-stu-id="5d7cc-162">Computer</span></span> |<span data-ttu-id="5d7cc-163">從收集 hello 事件的電腦。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="5d7cc-164">Facility</span><span class="sxs-lookup"><span data-stu-id="5d7cc-164">Facility</span></span> |<span data-ttu-id="5d7cc-165">定義 hello hello 系統產生 hello 訊息的一部分。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="5d7cc-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="5d7cc-166">HostIP</span></span> |<span data-ttu-id="5d7cc-167">Hello 系統傳送 hello 訊息的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="5d7cc-168">HostName</span><span class="sxs-lookup"><span data-stu-id="5d7cc-168">HostName</span></span> |<span data-ttu-id="5d7cc-169">Hello 系統傳送 hello 訊息的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="5d7cc-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="5d7cc-170">SeverityLevel</span></span> |<span data-ttu-id="5d7cc-171">Hello 事件嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="5d7cc-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="5d7cc-172">SyslogMessage</span></span> |<span data-ttu-id="5d7cc-173">Hello 訊息的文字。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-173">Text of hello message.</span></span> |
| <span data-ttu-id="5d7cc-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="5d7cc-174">ProcessID</span></span> |<span data-ttu-id="5d7cc-175">產生 hello 訊息的 hello 處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="5d7cc-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="5d7cc-176">EventTime</span></span> |<span data-ttu-id="5d7cc-177">日期和時間 hello 事件所產生。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="5d7cc-178">含有 Syslog 記錄的記錄查詢</span><span class="sxs-lookup"><span data-stu-id="5d7cc-178">Log queries with Syslog records</span></span>
<span data-ttu-id="5d7cc-179">hello 下表提供不同擷取 Syslog 記錄的記錄檔查詢的範例。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="5d7cc-180">查詢</span><span class="sxs-lookup"><span data-stu-id="5d7cc-180">Query</span></span> | <span data-ttu-id="5d7cc-181">說明</span><span class="sxs-lookup"><span data-stu-id="5d7cc-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5d7cc-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="5d7cc-182">Type=Syslog</span></span> |<span data-ttu-id="5d7cc-183">所有的 Syslog。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-183">All Syslogs.</span></span> |
| <span data-ttu-id="5d7cc-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="5d7cc-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="5d7cc-185">嚴重性為錯誤的所有 Syslog 記錄。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="5d7cc-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="5d7cc-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="5d7cc-187">依電腦的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="5d7cc-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="5d7cc-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="5d7cc-189">依設備的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="5d7cc-190">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="5d7cc-191">查詢</span><span class="sxs-lookup"><span data-stu-id="5d7cc-191">Query</span></span> | <span data-ttu-id="5d7cc-192">說明</span><span class="sxs-lookup"><span data-stu-id="5d7cc-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5d7cc-193">syslog</span><span class="sxs-lookup"><span data-stu-id="5d7cc-193">Syslog</span></span> |<span data-ttu-id="5d7cc-194">所有的 Syslog。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-194">All Syslogs.</span></span> |
| <span data-ttu-id="5d7cc-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="5d7cc-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="5d7cc-196">嚴重性為錯誤的所有 Syslog 記錄。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="5d7cc-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="5d7cc-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="5d7cc-198">依電腦的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="5d7cc-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="5d7cc-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="5d7cc-200">依設備的 Syslog 記錄計數。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d7cc-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d7cc-201">Next steps</span></span>
* <span data-ttu-id="5d7cc-202">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="5d7cc-203">使用[自訂欄位](log-analytics-custom-fields.md)tooparse syslog 記錄，到個別欄位的資料。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="5d7cc-204">[設定 Linux 代理程式](log-analytics-linux-agents.md)toocollect 其他類型的資料。</span><span class="sxs-lookup"><span data-stu-id="5d7cc-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
