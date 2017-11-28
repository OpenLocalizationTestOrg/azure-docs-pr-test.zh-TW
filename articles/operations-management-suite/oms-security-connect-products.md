---
title: "aaaConnecting 您的安全性產品 toohello Operations Management Suite (OMS) 的安全性和稽核解決方案 |Microsoft 文件"
description: "這份文件可協助您 tooconnect 您的安全性產品 tooOperations 管理套件的安全性和稽核解決方案使用通用的事件格式。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="829ab-103">連接您的安全性產品 toohello Operations Management Suite (OMS) 的安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="829ab-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="829ab-104">這份文件可協助您連接到 hello OMS 安全性和稽核解決方案的安全性產品。</span><span class="sxs-lookup"><span data-stu-id="829ab-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="829ab-105">支援下列來源的 hello:</span><span class="sxs-lookup"><span data-stu-id="829ab-105">hello following sources are supported:</span></span>

- <span data-ttu-id="829ab-106">常見事件格式 (CEF) 事件</span><span class="sxs-lookup"><span data-stu-id="829ab-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="829ab-107">Cisco ASA 事件</span><span class="sxs-lookup"><span data-stu-id="829ab-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="829ab-108">什麼是 CEF？</span><span class="sxs-lookup"><span data-stu-id="829ab-108">What is CEF?</span></span>
<span data-ttu-id="829ab-109">一般事件格式 (CEF) 是業界標準格式之上許多安全性廠商 tooallow 事件之間的互通性不同平台所使用的 Syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="829ab-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="829ab-110">OMS 安全性和稽核解決方案支援 OMS 安全性搭配使用 CEF，可讓您 tooconnect 安全性產品擷取資料。</span><span class="sxs-lookup"><span data-stu-id="829ab-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="829ab-111">藉由連接您的資料來源 tooOMS，便能 tootake hello 遵循屬於此平台的功能的優點：</span><span class="sxs-lookup"><span data-stu-id="829ab-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="829ab-112">搜尋與相互關聯</span><span class="sxs-lookup"><span data-stu-id="829ab-112">Search & Correlation</span></span>
- <span data-ttu-id="829ab-113">稽核</span><span class="sxs-lookup"><span data-stu-id="829ab-113">Auditing</span></span>
- <span data-ttu-id="829ab-114">警示</span><span class="sxs-lookup"><span data-stu-id="829ab-114">Alert</span></span>
- <span data-ttu-id="829ab-115">威脅情報</span><span class="sxs-lookup"><span data-stu-id="829ab-115">Threat Intelligence</span></span>
- <span data-ttu-id="829ab-116">值得注意的問題</span><span class="sxs-lookup"><span data-stu-id="829ab-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="829ab-117">收集安全性解決方案的記錄檔</span><span class="sxs-lookup"><span data-stu-id="829ab-117">Collection of security solution logs</span></span>

<span data-ttu-id="829ab-118">OMS 安全性支援收集使用 CEF over Syslogs 的記錄檔和 [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="829ab-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="829ab-119">在此範例中，hello 來源 （會產生 hello 記錄檔的電腦） 是執行 syslog ng 精靈的 Linux 電腦且 hello 目標是 OMS 安全性。</span><span class="sxs-lookup"><span data-stu-id="829ab-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="829ab-120">您必須遵循 tooperform hello tooprepare hello Linux 電腦的工作：</span><span class="sxs-lookup"><span data-stu-id="829ab-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="829ab-121">Hello OMS Agent for Linux，版本 1.2.0-25 或下載上方。</span><span class="sxs-lookup"><span data-stu-id="829ab-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="829ab-122">請遵循 hello 區段**快速安裝指南**從[本文](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)tooinstall 和上架 hello 代理程式 tooyour 工作區。</span><span class="sxs-lookup"><span data-stu-id="829ab-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="829ab-123">一般而言，另一個在 hello 記錄產生的 hello 與不同的電腦上安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="829ab-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="829ab-124">轉送 hello 記錄 toohello 代理程式電腦通常會需要 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="829ab-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="829ab-125">設定記錄產品/機器 tooforward hello 必要的事件 toohello syslog 服務精靈 （rsyslog 或 syslog-ng） hello hello 代理程式電腦上。</span><span class="sxs-lookup"><span data-stu-id="829ab-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="829ab-126">啟用 hello 代理程式機器 tooreceive 訊息從遠端系統上的 hello syslog 服務精靈。</span><span class="sxs-lookup"><span data-stu-id="829ab-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="829ab-127">Hello 代理程式在電腦上，hello 事件需要傳送嗨 syslog 服務精靈 toolocal UDP 連接埠 25226 toobe。</span><span class="sxs-lookup"><span data-stu-id="829ab-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="829ab-128">hello 代理程式會接聽內送事件，在此連接埠。</span><span class="sxs-lookup"><span data-stu-id="829ab-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="829ab-129">hello 下列是寄 hello 本機系統 toohello 代理程式 （您可以修改 hello 組態 toofit 您的本機設定） 的所有事件的範例組態：</span><span class="sxs-lookup"><span data-stu-id="829ab-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="829ab-130">開啟 hello 終端機視窗，並移 toohello 目錄*/etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="829ab-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="829ab-131">建立新的檔案*安全性-設定-omsagent.conf*並加入下列內容的 hello: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="829ab-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="829ab-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="829ab-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="829ab-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="829ab-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="829ab-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="829ab-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="829ab-135">下載 hello 檔案*security_events.conf*然後將放在*/etc/opt/microsoft/omsagent/conf/omsagent.d/* hello OMS 代理程式的電腦中。</span><span class="sxs-lookup"><span data-stu-id="829ab-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="829ab-136">輸入 hello 命令下方 toorestart hello syslog 服務精靈：*的 syslog ng 執行：*</span><span class="sxs-lookup"><span data-stu-id="829ab-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="829ab-137">若為 rsyslog 執行︰</span><span class="sxs-lookup"><span data-stu-id="829ab-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="829ab-138">輸入 hello 下方 toorestart hello OMS 代理程式的命令：</span><span class="sxs-lookup"><span data-stu-id="829ab-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="829ab-139">*若為 syslog-ng 執行* ︰</span><span class="sxs-lookup"><span data-stu-id="829ab-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="829ab-140">若為 rsyslog 執行︰</span><span class="sxs-lookup"><span data-stu-id="829ab-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="829ab-141">輸入下方的 hello 命令，然後檢閱 hello 結果 tooconfirm hello OMS 代理程式記錄檔中沒有任何錯誤：</span><span class="sxs-lookup"><span data-stu-id="829ab-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="829ab-142">檢閱收集到的安全性事件</span><span class="sxs-lookup"><span data-stu-id="829ab-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="829ab-143">Hello 組態完成之後，hello 安全性事件將會啟動 toobe 內嵌 OMS 安全性的。</span><span class="sxs-lookup"><span data-stu-id="829ab-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="829ab-144">toovisualize 這些事件中，開啟 hello 記錄搜尋中，輸入 hello 命令*類型 = CommonSecurityLog*在 hello 搜尋欄位，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="829ab-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="829ab-145">hello 下列範例顯示 hello 結果，此命令，請注意，在此情況下 OMS 安全性已內嵌由多個廠商的安全性記錄檔：</span><span class="sxs-lookup"><span data-stu-id="829ab-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![OMS 安全性和稽核基準評估](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="829ab-147">您可以修改此搜尋一個單一的廠商，例如 toovisualize 線上 Cisco 記錄、 型別：*類型 = CommonSecurityLog DeviceVendor = Cisco*。</span><span class="sxs-lookup"><span data-stu-id="829ab-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="829ab-148">hello"CommonSecurityLog 」 具有預先定義欄位，針對任何 CEF 標頭包括 hello 基本 extensios，任何其他擴充功能時，無論是 「 自訂延伸模組 >，就會插入到 「 AdditionalExtensions 」 欄位。</span><span class="sxs-lookup"><span data-stu-id="829ab-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="829ab-149">您可以使用它從 hello 自訂欄位功能 tooget 專用欄位。</span><span class="sxs-lookup"><span data-stu-id="829ab-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="829ab-150">存取遺失基準評估的電腦</span><span class="sxs-lookup"><span data-stu-id="829ab-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="829ab-151">OMS 會支援 Windows Server 2008 R2 上總 tooWindows Server 2012 R2 hello 網域成員基準設定檔。</span><span class="sxs-lookup"><span data-stu-id="829ab-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="829ab-152">Windows Server 2016 基準尚未定案，將在發佈後盡快新增。</span><span class="sxs-lookup"><span data-stu-id="829ab-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="829ab-153">透過 OMS 安全性和稽核基準評估掃描的所有其他作業系統出現在 hello**遺失基準評估電腦**> 一節。</span><span class="sxs-lookup"><span data-stu-id="829ab-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="829ab-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="829ab-154">See also</span></span>
<span data-ttu-id="829ab-155">在本文件中，您學到如何 tooconnect 您 CEF 方案 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="829ab-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="829ab-156">toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="829ab-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="829ab-157">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="829ab-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="829ab-158">監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="829ab-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="829ab-159">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="829ab-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

