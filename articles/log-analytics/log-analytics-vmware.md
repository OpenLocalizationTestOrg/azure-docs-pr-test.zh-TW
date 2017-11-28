---
title: "aaaVMware 記錄分析監控解決方案 |Microsoft 文件"
description: "深入了解如何 hello VMware 監視解決方案可協助管理記錄檔和監視 ESXi 主機。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a><span data-ttu-id="ccf53-103">Log Analytics 中的 VMware 監視 (預覽) 解決方案</span><span class="sxs-lookup"><span data-stu-id="ccf53-103">VMware Monitoring (Preview) solution in Log Analytics</span></span>

![VMware 符號](./media/log-analytics-vmware/vmware-symbol.png)

<span data-ttu-id="ccf53-105">hello VMware 監視方案中記錄分析是解決方案，可協助您建立集中式的記錄和監視大量的 VMware 記錄方法。</span><span class="sxs-lookup"><span data-stu-id="ccf53-105">hello VMware Monitoring solution in Log Analytics is a solution that helps you create a centralized logging and monitoring approach for large VMware logs.</span></span> <span data-ttu-id="ccf53-106">本文說明如何疑難排解、 擷取並管理使用 hello 方案的單一位置中的 hello ESXi 主機。</span><span class="sxs-lookup"><span data-stu-id="ccf53-106">This article describes how you can troubleshoot, capture, and manage hello ESXi hosts in a single location using hello solution.</span></span> <span data-ttu-id="ccf53-107">Hello 方案，您可以查看您所有的單一位置的 ESXi 主機詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="ccf53-107">With hello solution, you can see detailed data for all your ESXi hosts in a single location.</span></span> <span data-ttu-id="ccf53-108">您可以看到最上層的事件計數、 狀態和趨勢的 VM 和 ESXi 主機提供透過 hello ESXi 主機記錄。</span><span class="sxs-lookup"><span data-stu-id="ccf53-108">You can see top event counts, status, and trends of VM and ESXi hosts provided through hello ESXi host logs.</span></span> <span data-ttu-id="ccf53-109">您可以檢視及搜尋 ESXi 主機集中記錄檔，來進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ccf53-109">You can troubleshoot by viewing and searching centralized ESXi host logs.</span></span> <span data-ttu-id="ccf53-110">而且，您可以根據記錄檔搜尋查詢來建立警示。</span><span class="sxs-lookup"><span data-stu-id="ccf53-110">And, you can create alerts based on log search queries.</span></span>

<span data-ttu-id="ccf53-111">hello 解決方案會使用原生 syslog hello ESXi 主機 toopush 資料 tooa 目標 VM 具有 OMS 代理程式功能。</span><span class="sxs-lookup"><span data-stu-id="ccf53-111">hello solution uses native syslog functionality of hello ESXi host toopush data tooa target VM, which has OMS Agent.</span></span> <span data-ttu-id="ccf53-112">不過，hello 方案不是檔案寫入到 syslog hello 目標 VM 內。</span><span class="sxs-lookup"><span data-stu-id="ccf53-112">However, hello solution doesn't write files into syslog within hello target VM.</span></span> <span data-ttu-id="ccf53-113">開啟連接埠 1514 hello OMS 代理程式，並接聽 toothis。</span><span class="sxs-lookup"><span data-stu-id="ccf53-113">hello OMS agent opens port 1514 and listens toothis.</span></span> <span data-ttu-id="ccf53-114">在收到 hello 資料，hello OMS 代理程式會將 hello 資料推送至 OMS。</span><span class="sxs-lookup"><span data-stu-id="ccf53-114">Once it receives hello data, hello OMS agent pushes hello data into OMS.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="ccf53-115">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="ccf53-115">Installing and configuring hello solution</span></span>
<span data-ttu-id="ccf53-116">使用下列資訊 tooinstall hello 並設定 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="ccf53-116">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="ccf53-117">新增 hello VMware 監視解決方案 tooyour OMS 工作區中使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="ccf53-117">Add hello VMware Monitoring solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

#### <a name="supported-vmware-esxi-hosts"></a><span data-ttu-id="ccf53-118">支援的 VMware ESXi 主機</span><span class="sxs-lookup"><span data-stu-id="ccf53-118">Supported VMware ESXi hosts</span></span>
<span data-ttu-id="ccf53-119">vSphere ESXi 主機 5.5 和 6.0</span><span class="sxs-lookup"><span data-stu-id="ccf53-119">vSphere ESXi Host 5.5 and 6.0</span></span>

#### <a name="prepare-a-linux-server"></a><span data-ttu-id="ccf53-120">準備 Linux 伺服器</span><span class="sxs-lookup"><span data-stu-id="ccf53-120">Prepare a Linux server</span></span>
<span data-ttu-id="ccf53-121">從 hello ESXi 主機建立 Linux 作業系統的 VM tooreceive 所有 syslog 資料。</span><span class="sxs-lookup"><span data-stu-id="ccf53-121">Create a Linux operating system VM tooreceive all syslog data from hello ESXi hosts.</span></span> <span data-ttu-id="ccf53-122">hello [OMS Linux 代理程式](log-analytics-linux-agents.md)是所有的 ESXi 主機 syslog 資料 hello 集合點。</span><span class="sxs-lookup"><span data-stu-id="ccf53-122">hello [OMS Linux Agent](log-analytics-linux-agents.md) is hello collection point for all ESXi host syslog data.</span></span> <span data-ttu-id="ccf53-123">您可以使用多個 ESXi 主機 tooforward 記錄 tooa 單一 Linux 伺服器，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ccf53-123">You can use multiple ESXi hosts tooforward logs tooa single Linux server, as in hello following example.</span></span>  

   ![syslog 流程](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a><span data-ttu-id="ccf53-125">設定 syslog 收集</span><span class="sxs-lookup"><span data-stu-id="ccf53-125">Configure syslog collection</span></span>
1. <span data-ttu-id="ccf53-126">設定 VSphere 的 syslog 轉送。</span><span class="sxs-lookup"><span data-stu-id="ccf53-126">Set up syslog forwarding for VSphere.</span></span> <span data-ttu-id="ccf53-127">設定 syslog 轉送的詳細的資訊 toohelp，請參閱[ESXi 上設定 syslog 5.x 和 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322)。</span><span class="sxs-lookup"><span data-stu-id="ccf53-127">For detailed information toohelp set up syslog forwarding, see [Configuring syslog on ESXi 5.x and 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322).</span></span> <span data-ttu-id="ccf53-128">跳過**ESXi 主機組態** > **軟體** > **進階設定** > **Syslog**.</span><span class="sxs-lookup"><span data-stu-id="ccf53-128">Go too**ESXi Host Configuration** > **Software** > **Advanced Settings** > **Syslog**.</span></span>
   <span data-ttu-id="ccf53-129">![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)</span><span class="sxs-lookup"><span data-stu-id="ccf53-129">![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)</span></span>  
2. <span data-ttu-id="ccf53-130">在 hello *Syslog.global.logHost*欄位中，加入您的 Linux 伺服器和 hello 連接埠號碼*1514年*。</span><span class="sxs-lookup"><span data-stu-id="ccf53-130">In hello *Syslog.global.logHost* field, add your Linux server and hello port number *1514*.</span></span> <span data-ttu-id="ccf53-131">例如，`tcp://hostname:1514` 或 `tcp://123.456.789.101:1514`。</span><span class="sxs-lookup"><span data-stu-id="ccf53-131">For example, `tcp://hostname:1514` or `tcp://123.456.789.101:1514`</span></span>
3. <span data-ttu-id="ccf53-132">開啟 syslog hello ESXi 主機防火牆。</span><span class="sxs-lookup"><span data-stu-id="ccf53-132">Open hello ESXi host firewall for syslog.</span></span> <span data-ttu-id="ccf53-133">[ESXi 主機組態]  >  [軟體]  >  [安全性設定檔]  >  [防火牆]，然後開啟 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="ccf53-133">**ESXi Host Configuration** > **Software** > **Security Profile** > **Firewall** and open **Properties**.</span></span>  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. <span data-ttu-id="ccf53-136">請檢查該 syslog 已正確設定的 hello vSphere 主控台 tooverify。</span><span class="sxs-lookup"><span data-stu-id="ccf53-136">Check hello vSphere Console tooverify that that syslog is properly set up.</span></span> <span data-ttu-id="ccf53-137">確認 hello ESXI 主機的連接埠**1514年**設定。</span><span class="sxs-lookup"><span data-stu-id="ccf53-137">Confirm on hello ESXI host that port **1514** is configured.</span></span>
5. <span data-ttu-id="ccf53-138">下載並安裝適用於 Linux 的 OMS 代理程式 hello hello Linux 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="ccf53-138">Download and install hello OMS Agent for Linux on hello Linux server.</span></span> <span data-ttu-id="ccf53-139">如需詳細資訊，請參閱 hello [OMS agent for Linux 的文件](https://github.com/Microsoft/OMS-Agent-for-Linux)。</span><span class="sxs-lookup"><span data-stu-id="ccf53-139">For more information, see hello [Documentation for OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).</span></span>
6. <span data-ttu-id="ccf53-140">Hello OMS Agent for Linux 安裝之後，請前往 toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d 目錄複製 hello vmware_esxi.conf 檔案 toohello /etc/opt/microsoft/omsagent/conf/omsagent.d 目錄和 hello 變更 hello 擁有者/群組與 hello 檔案的權限。</span><span class="sxs-lookup"><span data-stu-id="ccf53-140">After hello OMS Agent for Linux is installed, go toohello  /etc/opt/microsoft/omsagent/sysconf/omsagent.d directory and copy hello vmware_esxi.conf file toohello /etc/opt/microsoft/omsagent/conf/omsagent.d directory and hello change hello owner/group and permissions of hello file.</span></span> <span data-ttu-id="ccf53-141">例如：</span><span class="sxs-lookup"><span data-stu-id="ccf53-141">For example:</span></span>

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. <span data-ttu-id="ccf53-142">執行來重新啟動 hello OMS Agent for Linux `sudo /opt/microsoft/omsagent/bin/service_control restart`。</span><span class="sxs-lookup"><span data-stu-id="ccf53-142">Restart hello OMS Agent for Linux by running `sudo /opt/microsoft/omsagent/bin/service_control restart`.</span></span>
8. <span data-ttu-id="ccf53-143">測試的使用 hello hello hello Linux 伺服器和 hello ESXi 主機之間的連線能力`nc`hello ESXi 主機上的命令。</span><span class="sxs-lookup"><span data-stu-id="ccf53-143">Test hello connectivity between hello Linux server and hello ESXi host by using hello `nc` command on hello ESXi Host.</span></span> <span data-ttu-id="ccf53-144">例如：</span><span class="sxs-lookup"><span data-stu-id="ccf53-144">For example:</span></span>

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. <span data-ttu-id="ccf53-145">在 hello OMS 入口網站，執行記錄檔中的搜尋`Type=VMware_CL`。</span><span class="sxs-lookup"><span data-stu-id="ccf53-145">In hello OMS Portal, perform a log search for `Type=VMware_CL`.</span></span> <span data-ttu-id="ccf53-146">當 OMS 會收集 hello syslog 資料時，它會保留 hello syslog 格式。</span><span class="sxs-lookup"><span data-stu-id="ccf53-146">When OMS collects hello syslog data, it retains hello syslog format.</span></span> <span data-ttu-id="ccf53-147">在 hello 入口網站，某些特定的欄位所擷取，例如*Hostname*和*ProcessName*。</span><span class="sxs-lookup"><span data-stu-id="ccf53-147">In hello portal, some specific fields are captured, such as *Hostname* and *ProcessName*.</span></span>  

    ![類型](./media/log-analytics-vmware/type.png)  

    <span data-ttu-id="ccf53-149">如果您檢視的記錄搜尋結果會類似上述的 toohello 映像，您要設定 toouse hello OMS VMware 監視方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="ccf53-149">If your view log search results are similar toohello image above, you're set toouse hello OMS VMware Monitoring solution dashboard.</span></span>  

## <a name="vmware-data-collection-details"></a><span data-ttu-id="ccf53-150">VMware 資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="ccf53-150">VMware data collection details</span></span>
<span data-ttu-id="ccf53-151">hello VMware 監視解決方案使用 hello OMS Agents for Linux，您已啟用的 ESXi 主機從收集各種效能度量和記錄資料。</span><span class="sxs-lookup"><span data-stu-id="ccf53-151">hello VMware Monitoring solution collects various performance metrics and log data from ESXi hosts using hello OMS Agents for Linux that you have enabled.</span></span>

<span data-ttu-id="ccf53-152">hello 下表顯示資料收集方法，以及如何收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ccf53-152">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="ccf53-153">平台</span><span class="sxs-lookup"><span data-stu-id="ccf53-153">platform</span></span> | <span data-ttu-id="ccf53-154">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="ccf53-154">OMS Agent for Linux</span></span> | <span data-ttu-id="ccf53-155">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="ccf53-155">SCOM agent</span></span> | <span data-ttu-id="ccf53-156">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="ccf53-156">Azure Storage</span></span> | <span data-ttu-id="ccf53-157">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="ccf53-157">SCOM required?</span></span> | <span data-ttu-id="ccf53-158">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="ccf53-158">SCOM agent data sent via management group</span></span> | <span data-ttu-id="ccf53-159">收集頻率</span><span class="sxs-lookup"><span data-stu-id="ccf53-159">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="ccf53-160">Linux</span><span class="sxs-lookup"><span data-stu-id="ccf53-160">Linux</span></span> |<span data-ttu-id="ccf53-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ccf53-161">&#8226;</span></span> |  |  |  |  |<span data-ttu-id="ccf53-162">每隔 3 分鐘</span><span class="sxs-lookup"><span data-stu-id="ccf53-162">every 3 minutes</span></span> |

<span data-ttu-id="ccf53-163">下表中的 hello 顯示 hello VMware 監視解決方案所收集的資料欄位的範例：</span><span class="sxs-lookup"><span data-stu-id="ccf53-163">hello following table show examples of data fields collected by hello VMware Monitoring solution:</span></span>

| <span data-ttu-id="ccf53-164">欄位名稱</span><span class="sxs-lookup"><span data-stu-id="ccf53-164">field name</span></span> | <span data-ttu-id="ccf53-165">說明</span><span class="sxs-lookup"><span data-stu-id="ccf53-165">description</span></span> |
| --- | --- |
| <span data-ttu-id="ccf53-166">Device_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-166">Device_s</span></span> |<span data-ttu-id="ccf53-167">VMware 儲存裝置</span><span class="sxs-lookup"><span data-stu-id="ccf53-167">VMware storage devices</span></span> |
| <span data-ttu-id="ccf53-168">ESXIFailure_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-168">ESXIFailure_s</span></span> |<span data-ttu-id="ccf53-169">失敗類型</span><span class="sxs-lookup"><span data-stu-id="ccf53-169">failure types</span></span> |
| <span data-ttu-id="ccf53-170">EventTime_t</span><span class="sxs-lookup"><span data-stu-id="ccf53-170">EventTime_t</span></span> |<span data-ttu-id="ccf53-171">事件發生的時間</span><span class="sxs-lookup"><span data-stu-id="ccf53-171">time when event occurred</span></span> |
| <span data-ttu-id="ccf53-172">HostName_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-172">HostName_s</span></span> |<span data-ttu-id="ccf53-173">ESXi 主機名稱</span><span class="sxs-lookup"><span data-stu-id="ccf53-173">ESXi host name</span></span> |
| <span data-ttu-id="ccf53-174">Operation_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-174">Operation_s</span></span> |<span data-ttu-id="ccf53-175">建立 VM或刪除 VM</span><span class="sxs-lookup"><span data-stu-id="ccf53-175">create VM or delete VM</span></span> |
| <span data-ttu-id="ccf53-176">ProcessName_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-176">ProcessName_s</span></span> |<span data-ttu-id="ccf53-177">事件名稱</span><span class="sxs-lookup"><span data-stu-id="ccf53-177">event name</span></span> |
| <span data-ttu-id="ccf53-178">ResourceId_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-178">ResourceId_s</span></span> |<span data-ttu-id="ccf53-179">hello VMware 主機名稱</span><span class="sxs-lookup"><span data-stu-id="ccf53-179">name of hello VMware host</span></span> |
| <span data-ttu-id="ccf53-180">ResourceLocation_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-180">ResourceLocation_s</span></span> |<span data-ttu-id="ccf53-181">VMware</span><span class="sxs-lookup"><span data-stu-id="ccf53-181">VMware</span></span> |
| <span data-ttu-id="ccf53-182">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-182">ResourceName_s</span></span> |<span data-ttu-id="ccf53-183">VMware</span><span class="sxs-lookup"><span data-stu-id="ccf53-183">VMware</span></span> |
| <span data-ttu-id="ccf53-184">ResourceType_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-184">ResourceType_s</span></span> |<span data-ttu-id="ccf53-185">Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ccf53-185">Hyper-V</span></span> |
| <span data-ttu-id="ccf53-186">SCSIStatus_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-186">SCSIStatus_s</span></span> |<span data-ttu-id="ccf53-187">VMware SCSI 的狀態</span><span class="sxs-lookup"><span data-stu-id="ccf53-187">VMware SCSI status</span></span> |
| <span data-ttu-id="ccf53-188">SyslogMessage_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-188">SyslogMessage_s</span></span> |<span data-ttu-id="ccf53-189">syslog 資料</span><span class="sxs-lookup"><span data-stu-id="ccf53-189">Syslog data</span></span> |
| <span data-ttu-id="ccf53-190">UserName_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-190">UserName_s</span></span> |<span data-ttu-id="ccf53-191">建立或刪除 VM 的使用者</span><span class="sxs-lookup"><span data-stu-id="ccf53-191">user who created or deleted VM</span></span> |
| <span data-ttu-id="ccf53-192">VMName_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-192">VMName_s</span></span> |<span data-ttu-id="ccf53-193">VM 名稱</span><span class="sxs-lookup"><span data-stu-id="ccf53-193">VM name</span></span> |
| <span data-ttu-id="ccf53-194">電腦</span><span class="sxs-lookup"><span data-stu-id="ccf53-194">Computer</span></span> |<span data-ttu-id="ccf53-195">主機電腦</span><span class="sxs-lookup"><span data-stu-id="ccf53-195">host computer</span></span> |
| <span data-ttu-id="ccf53-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ccf53-196">TimeGenerated</span></span> |<span data-ttu-id="ccf53-197">產生時間 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ccf53-197">time hello data was generated</span></span> |
| <span data-ttu-id="ccf53-198">DataCenter_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-198">DataCenter_s</span></span> |<span data-ttu-id="ccf53-199">VMware 資料中心</span><span class="sxs-lookup"><span data-stu-id="ccf53-199">VMware datacenter</span></span> |
| <span data-ttu-id="ccf53-200">StorageLatency_s</span><span class="sxs-lookup"><span data-stu-id="ccf53-200">StorageLatency_s</span></span> |<span data-ttu-id="ccf53-201">儲存體延遲 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="ccf53-201">storage latency (ms)</span></span> |

## <a name="vmware-monitoring-solution-overview"></a><span data-ttu-id="ccf53-202">VMware 監視解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="ccf53-202">VMware Monitoring solution overview</span></span>
<span data-ttu-id="ccf53-203">hello VMware 磚會出現在 hello OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ccf53-203">hello VMware tile appears in hello OMS portal.</span></span> <span data-ttu-id="ccf53-204">它提供任何失敗的高階檢視。</span><span class="sxs-lookup"><span data-stu-id="ccf53-204">It provides a high-level view of any failures.</span></span> <span data-ttu-id="ccf53-205">當您按一下 hello 磚時，您會進入儀表板檢視。</span><span class="sxs-lookup"><span data-stu-id="ccf53-205">When you click hello tile, you go into a dashboard view.</span></span>

![圖格](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a><span data-ttu-id="ccf53-207">瀏覽 hello 儀表板檢視</span><span class="sxs-lookup"><span data-stu-id="ccf53-207">Navigate hello dashboard view</span></span>
<span data-ttu-id="ccf53-208">在 [hello **VMware**儀表板] 檢視中，依組織的刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="ccf53-208">In hello **VMware** dashboard view, blades are organized by:</span></span>

* <span data-ttu-id="ccf53-209">失敗狀態計數</span><span class="sxs-lookup"><span data-stu-id="ccf53-209">Failure Status Count</span></span>
* <span data-ttu-id="ccf53-210">依事件計數的主機前幾名</span><span class="sxs-lookup"><span data-stu-id="ccf53-210">Top Host by Event Counts</span></span>
* <span data-ttu-id="ccf53-211">前幾名事件計數</span><span class="sxs-lookup"><span data-stu-id="ccf53-211">Top Event Counts</span></span>
* <span data-ttu-id="ccf53-212">虛擬機器活動</span><span class="sxs-lookup"><span data-stu-id="ccf53-212">Virtual Machine Activities</span></span>
* <span data-ttu-id="ccf53-213">ESXi 主機磁碟的事件</span><span class="sxs-lookup"><span data-stu-id="ccf53-213">ESXi Host Disk Events</span></span>

![解決方案1](./media/log-analytics-vmware/solutionview1-1.png)

![解決方案2](./media/log-analytics-vmware/solutionview1-2.png)

<span data-ttu-id="ccf53-216">按一下任何刀鋒視窗 tooopen 適合 hello 刀鋒視窗會顯示詳細的資訊的記錄分析搜尋窗格。</span><span class="sxs-lookup"><span data-stu-id="ccf53-216">Click any blade tooopen Log Analytics search pane that shows detailed information specific for hello blade.</span></span>

<span data-ttu-id="ccf53-217">您可以從這裡編輯 hello 搜尋查詢 toomodify 會針對特定項目。</span><span class="sxs-lookup"><span data-stu-id="ccf53-217">From here, you can edit hello search query toomodify it for something specific.</span></span> <span data-ttu-id="ccf53-218">如需 OMS 搜尋 hello 基本概念的教學課程，請參閱 hello [OMS 記錄搜尋教學課程。](log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="ccf53-218">For a tutorial on hello basics of OMS search, check out hello [OMS log search tutorial.](log-analytics-log-searches.md)</span></span>

#### <a name="find-esxi-host-events"></a><span data-ttu-id="ccf53-219">尋找 ESXi 主機事件</span><span class="sxs-lookup"><span data-stu-id="ccf53-219">Find ESXi host events</span></span>
<span data-ttu-id="ccf53-220">單一 ESXi 主機會產生多個記錄檔，取決於其程序。</span><span class="sxs-lookup"><span data-stu-id="ccf53-220">A single ESXi host generates multiple logs, based on their processes.</span></span> <span data-ttu-id="ccf53-221">hello VMware 監視解決方案集中管理它們，並摘要說明 hello 事件計數。</span><span class="sxs-lookup"><span data-stu-id="ccf53-221">hello VMware Monitoring solution centralizes them and summarizes hello event counts.</span></span> <span data-ttu-id="ccf53-222">這個集中式的檢視可幫助您了解哪些 ESXi 主機有大量的事件，以及在您的環境中最常發生哪些事件。</span><span class="sxs-lookup"><span data-stu-id="ccf53-222">This centralized view helps you understand which ESXi host has a high volume of events and what events occur most frequently in your environment.</span></span>

![事件](./media/log-analytics-vmware/events.png)

<span data-ttu-id="ccf53-224">您可以按一下 ESXi 主機或事件類型，進一步深入探詢。</span><span class="sxs-lookup"><span data-stu-id="ccf53-224">You can drill further by clicking an ESXi host or an event type.</span></span>

<span data-ttu-id="ccf53-225">當您按一下的 ESXi 主機名稱時，可以檢視該 ESXi 主機的資訊。</span><span class="sxs-lookup"><span data-stu-id="ccf53-225">When you click an ESXi host name, you view information from that ESXi host.</span></span> <span data-ttu-id="ccf53-226">如果您想 toonarrow 結果 hello 事件類型，新增`“ProcessName_s=EVENT TYPE”`搜尋查詢中。</span><span class="sxs-lookup"><span data-stu-id="ccf53-226">If you want toonarrow results with hello event type, add `“ProcessName_s=EVENT TYPE”` in your search query.</span></span> <span data-ttu-id="ccf53-227">您可以選取**ProcessName** hello 搜尋篩選器中。</span><span class="sxs-lookup"><span data-stu-id="ccf53-227">You can select **ProcessName** in hello search filter.</span></span> <span data-ttu-id="ccf53-228">縮小 hello 的資訊。</span><span class="sxs-lookup"><span data-stu-id="ccf53-228">That narrows hello information for you.</span></span>

![深入探詢](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a><span data-ttu-id="ccf53-230">尋找高 VM 活動</span><span class="sxs-lookup"><span data-stu-id="ccf53-230">Find high VM activities</span></span>
<span data-ttu-id="ccf53-231">在任何 ESXi 主機上皆可以建立及刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ccf53-231">A virtual machine can be created and deleted on any ESXi host.</span></span> <span data-ttu-id="ccf53-232">它可協助系統管理員 tooidentify 多少 ESXi 主機建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ccf53-232">It's helpful for an administrator tooidentify how many VMs an ESXi host creates.</span></span> <span data-ttu-id="ccf53-233">在中開啟，可協助 toounderstand 效能及容量規劃。</span><span class="sxs-lookup"><span data-stu-id="ccf53-233">That in-turn, helps toounderstand performance and capacity planning.</span></span> <span data-ttu-id="ccf53-234">管理您的環境時，持續追蹤 VM 活動事件極為重要。</span><span class="sxs-lookup"><span data-stu-id="ccf53-234">Keeping track of VM activity events is crucial when managing your environment.</span></span>

![深入探詢](./media/log-analytics-vmware/vmactivities1.png)

<span data-ttu-id="ccf53-236">如果您想要讓其他 ESXi 主機 toosee VM 建立資料，請按一下 ESXi 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="ccf53-236">If you want toosee additional ESXi host VM creation data, click an ESXi host name.</span></span>

![深入探詢](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a><span data-ttu-id="ccf53-238">常見的搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="ccf53-238">Common search queries</span></span>
<span data-ttu-id="ccf53-239">hello 解決方案包含其他有用的查詢，可協助您管理您的 ESXi 主機，例如高的儲存空間、 儲存體延遲，以及路徑失敗。</span><span class="sxs-lookup"><span data-stu-id="ccf53-239">hello solution includes other useful queries that can help you manage your ESXi hosts, such as high storage space, storage latency, and path failure.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![查詢](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a><span data-ttu-id="ccf53-241">儲存查詢</span><span class="sxs-lookup"><span data-stu-id="ccf53-241">Save queries</span></span>
<span data-ttu-id="ccf53-242">儲存搜尋查詢是 OMS 中的標準功能，可協助您保留任何您認為有用的查詢。</span><span class="sxs-lookup"><span data-stu-id="ccf53-242">Saving search queries is a standard feature in OMS and can help you keep any queries that you’ve found useful.</span></span> <span data-ttu-id="ccf53-243">您建立查詢，您有幫助之後，按一下以儲存它 hello**我的最愛**。</span><span class="sxs-lookup"><span data-stu-id="ccf53-243">After you create a query that you find useful, save it by clicking hello **Favorites**.</span></span> <span data-ttu-id="ccf53-244">已儲存的查詢可讓您輕鬆地重複使用它稍後從 hello[我的儀表板](log-analytics-dashboards.md)頁面，您可以在其中建立您自己自訂的儀表板。</span><span class="sxs-lookup"><span data-stu-id="ccf53-244">A saved query lets you easily reuse it later from hello [My Dashboard](log-analytics-dashboards.md) page where you can create your own custom dashboards.</span></span>

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a><span data-ttu-id="ccf53-246">從查詢建立警示</span><span class="sxs-lookup"><span data-stu-id="ccf53-246">Create alerts from queries</span></span>
<span data-ttu-id="ccf53-247">您已建立您的查詢之後，您可能會想 toouse hello 查詢 tooalert 您特定事件發生時。</span><span class="sxs-lookup"><span data-stu-id="ccf53-247">After you’ve created your queries, you might want toouse hello queries tooalert you when specific events occur.</span></span> <span data-ttu-id="ccf53-248">請參閱[記錄分析中的警示](log-analytics-alerts.md)如需有關資訊 toocreate 警示。</span><span class="sxs-lookup"><span data-stu-id="ccf53-248">See [Alerts in Log Analytics](log-analytics-alerts.md) for information about how toocreate alerts.</span></span> <span data-ttu-id="ccf53-249">如需警示查詢和其他查詢範例的範例，請參閱 hello[監視 VMware 使用 OMS 記錄分析](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="ccf53-249">For examples of alerting queries and other query examples, see hello [Monitor VMware using OMS Log Analytics](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) blog post.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ccf53-250">常見問題集</span><span class="sxs-lookup"><span data-stu-id="ccf53-250">Frequently asked questions</span></span>
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a><span data-ttu-id="ccf53-251">我需要設定 hello ESXi 主機上的 toodo？</span><span class="sxs-lookup"><span data-stu-id="ccf53-251">What do I need toodo on hello ESXi host setting?</span></span> <span data-ttu-id="ccf53-252">它會對我目前的環境造成什麼影響？</span><span class="sxs-lookup"><span data-stu-id="ccf53-252">What impact will it have on my current environment?</span></span>
<span data-ttu-id="ccf53-253">hello 解決方案會使用原生 ESXi 主機 Syslog 轉送機制 hello。</span><span class="sxs-lookup"><span data-stu-id="ccf53-253">hello solution uses hello native ESXi Host Syslog forwarding mechanism.</span></span> <span data-ttu-id="ccf53-254">您不需要任何額外的 Microsoft 軟體 hello ESXi 主機 toocapture hello 記錄上。</span><span class="sxs-lookup"><span data-stu-id="ccf53-254">You don't need any additional Microsoft software on hello ESXi Host toocapture hello logs.</span></span> <span data-ttu-id="ccf53-255">它應該會有影響很小 tooyour 現有環境。</span><span class="sxs-lookup"><span data-stu-id="ccf53-255">It should have a low impact tooyour existing environment.</span></span> <span data-ttu-id="ccf53-256">不過，您需要 tooset syslog 轉送 ESXI 功能。</span><span class="sxs-lookup"><span data-stu-id="ccf53-256">However, you do need tooset syslog forwarding, which is ESXI functionality.</span></span>

### <a name="do-i-need-toorestart-my-esxi-host"></a><span data-ttu-id="ccf53-257">我需要 toorestart 我的 ESXi 主機嗎？</span><span class="sxs-lookup"><span data-stu-id="ccf53-257">Do I need toorestart my ESXi host?</span></span>
<span data-ttu-id="ccf53-258">否。</span><span class="sxs-lookup"><span data-stu-id="ccf53-258">No.</span></span> <span data-ttu-id="ccf53-259">此處理序不需要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="ccf53-259">This process does not require a restart.</span></span> <span data-ttu-id="ccf53-260">有時候，vSphere 不會正確更新 hello syslog。</span><span class="sxs-lookup"><span data-stu-id="ccf53-260">Sometimes, vSphere does not properly update hello syslog.</span></span> <span data-ttu-id="ccf53-261">在這種情況下，登入 toohello ESXi 主機並重新載入 hello syslog。</span><span class="sxs-lookup"><span data-stu-id="ccf53-261">In such a case, log on toohello ESXi host and reload hello syslog.</span></span> <span data-ttu-id="ccf53-262">同樣地，您不需要 toorestart hello 主機，讓此程序未中斷 tooyour 環境。</span><span class="sxs-lookup"><span data-stu-id="ccf53-262">Again, you don't have toorestart hello host, so this process isn't disruptive tooyour environment.</span></span>

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a><span data-ttu-id="ccf53-263">我可以增加或減少記錄傳送的資料 tooOMS hello 磁碟區嗎？</span><span class="sxs-lookup"><span data-stu-id="ccf53-263">Can I increase or decrease hello volume of log data sent tooOMS?</span></span>
<span data-ttu-id="ccf53-264">是，您可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="ccf53-264">Yes you can.</span></span> <span data-ttu-id="ccf53-265">您可以在 vSphere 使用 hello ESXi 主機記錄層級設定。</span><span class="sxs-lookup"><span data-stu-id="ccf53-265">You can use hello ESXi Host Log Level settings in vSphere.</span></span> <span data-ttu-id="ccf53-266">記錄檔集合根據 hello*資訊*層級。</span><span class="sxs-lookup"><span data-stu-id="ccf53-266">Log collection is based on hello *info* level.</span></span> <span data-ttu-id="ccf53-267">因此，如果您想 tooaudit VM 建立或刪除，您需要 tookeep hello*資訊*hostd 層級。</span><span class="sxs-lookup"><span data-stu-id="ccf53-267">So, if you want tooaudit VM creation or deletion, you need tookeep hello *info* level on Hostd.</span></span> <span data-ttu-id="ccf53-268">如需詳細資訊，請參閱 hello [VMware 知識庫](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658)。</span><span class="sxs-lookup"><span data-stu-id="ccf53-268">For more information, see hello [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).</span></span>

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a><span data-ttu-id="ccf53-269">為什麼 Hostd 不提供資料 tooOMS？</span><span class="sxs-lookup"><span data-stu-id="ccf53-269">Why is Hostd not providing data tooOMS?</span></span> <span data-ttu-id="ccf53-270">My 記錄檔設定為 tooinfo。</span><span class="sxs-lookup"><span data-stu-id="ccf53-270">My log setting is set tooinfo.</span></span>
<span data-ttu-id="ccf53-271">時發生 ESXi 主機的 bug hello syslog 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ccf53-271">There was an ESXi host bug for hello syslog timestamp.</span></span> <span data-ttu-id="ccf53-272">如需詳細資訊，請參閱 hello [VMware 知識庫](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202)。</span><span class="sxs-lookup"><span data-stu-id="ccf53-272">For more information, see hello [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202).</span></span> <span data-ttu-id="ccf53-273">套用 hello 因應措施之後，Hostd 應該正常運作。</span><span class="sxs-lookup"><span data-stu-id="ccf53-273">After you apply hello workaround, Hostd should function normally.</span></span>

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a><span data-ttu-id="ccf53-274">我可以擁有多個 ESXi 主機轉送 syslog 資料 tooa 單一 VM 與 omsagent 嗎？</span><span class="sxs-lookup"><span data-stu-id="ccf53-274">Can I have multiple ESXi hosts forwarding syslog data tooa single VM with omsagent?</span></span>
<span data-ttu-id="ccf53-275">是。</span><span class="sxs-lookup"><span data-stu-id="ccf53-275">Yes.</span></span> <span data-ttu-id="ccf53-276">您可以有多個 ESXi 主機轉送 tooa omsagent 與單一 VM。</span><span class="sxs-lookup"><span data-stu-id="ccf53-276">You can have multiple ESXi hosts forwarding tooa single VM with omsagent.</span></span>

### <a name="why-dont-i-see-data-flowing-into-oms"></a><span data-ttu-id="ccf53-277">為什麼我沒有看到資料流入 OMS？</span><span class="sxs-lookup"><span data-stu-id="ccf53-277">Why don't I see data flowing into OMS?</span></span>
<span data-ttu-id="ccf53-278">這有幾個原因：</span><span class="sxs-lookup"><span data-stu-id="ccf53-278">There can be multiple reasons:</span></span>

* <span data-ttu-id="ccf53-279">hello ESXi 主機未正確達到資料 toohello VM 執行 omsagent。</span><span class="sxs-lookup"><span data-stu-id="ccf53-279">hello ESXi host is not correctly pushing data toohello VM running omsagent.</span></span> <span data-ttu-id="ccf53-280">tootest，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ccf53-280">tootest, perform hello following steps:</span></span>

  1. <span data-ttu-id="ccf53-281">tooconfirm，登入使用 ssh toohello ESXi 主機，然後執行下列命令的 hello:`nc -z ipaddressofVM 1514`</span><span class="sxs-lookup"><span data-stu-id="ccf53-281">tooconfirm, log on toohello ESXi host using ssh and run hello following command: `nc -z ipaddressofVM 1514`</span></span>

      <span data-ttu-id="ccf53-282">如果不成功，vSphere hello 可能是進階組態設定不會更正。</span><span class="sxs-lookup"><span data-stu-id="ccf53-282">If this is not successful, vSphere settings in hello Advanced Configuration are likely not correct.</span></span> <span data-ttu-id="ccf53-283">請參閱[設定 syslog 收集](#configure-syslog-collection)如需有關如何 tooset 向上 hello ESXi 主機 syslog 轉送資訊。</span><span class="sxs-lookup"><span data-stu-id="ccf53-283">See [Configure syslog collection](#configure-syslog-collection) for information about how tooset up hello ESXi host for syslog forwarding.</span></span>
  2. <span data-ttu-id="ccf53-284">如果 syslog 連接埠連線成功，但您仍然看不到任何資料，然後重新載入 hello syslog hello ESXi 主機上的使用 ssh toorun hello 下列命令：` esxcli system syslog reload`</span><span class="sxs-lookup"><span data-stu-id="ccf53-284">If syslog port connectivity is successful, but you don't still see any data, then reload hello syslog on hello ESXi host by using ssh toorun hello following command: ` esxcli system syslog reload`</span></span>
* <span data-ttu-id="ccf53-285">hello 與 OMS Agent 的 VM 設定不正確。</span><span class="sxs-lookup"><span data-stu-id="ccf53-285">hello VM with OMS Agent is not set correctly.</span></span> <span data-ttu-id="ccf53-286">tootest，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ccf53-286">tootest this, perform hello following steps:</span></span>

  1. <span data-ttu-id="ccf53-287">OMS 會接聽 toohello 連接埠 1514年，並將資料推入 OMS。</span><span class="sxs-lookup"><span data-stu-id="ccf53-287">OMS listens toohello port 1514 and pushes data into OMS.</span></span> <span data-ttu-id="ccf53-288">tooverify，並且已開啟，執行下列命令的 hello:`netstat -a | grep 1514`</span><span class="sxs-lookup"><span data-stu-id="ccf53-288">tooverify that it is open, run hello following command: `netstat -a | grep 1514`</span></span>
  2. <span data-ttu-id="ccf53-289">您應該會看到連接埠 `1514/tcp` 已開啟。</span><span class="sxs-lookup"><span data-stu-id="ccf53-289">You should see port `1514/tcp` open.</span></span> <span data-ttu-id="ccf53-290">如果不這麼做，請確認該 hello omsagent 已正確安裝。</span><span class="sxs-lookup"><span data-stu-id="ccf53-290">If you do not, verify that hello omsagent is installed correctly.</span></span> <span data-ttu-id="ccf53-291">如果看不到 hello 連接埠資訊，則不在 hello VM 上開啟 hello syslog 連接埠。</span><span class="sxs-lookup"><span data-stu-id="ccf53-291">If you do not see hello port information, then hello syslog port is not open on hello VM.</span></span>

     1. <span data-ttu-id="ccf53-292">確認執行 OMS 代理程式時，使用該 hello `ps -ef | grep oms`。</span><span class="sxs-lookup"><span data-stu-id="ccf53-292">Verify that hello OMS Agent is running by using `ps -ef | grep oms`.</span></span> <span data-ttu-id="ccf53-293">如果未執行，請執行 hello 命令來啟動 hello 程序` sudo /opt/microsoft/omsagent/bin/service_control start`</span><span class="sxs-lookup"><span data-stu-id="ccf53-293">If it is not running, start hello process by running hello command ` sudo /opt/microsoft/omsagent/bin/service_control start`</span></span>
     2. <span data-ttu-id="ccf53-294">開啟 hello`/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf`檔案。</span><span class="sxs-lookup"><span data-stu-id="ccf53-294">Open hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` file.</span></span>

         <span data-ttu-id="ccf53-295">確認 hello 適當的使用者和群組設定有效，類似於：`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`</span><span class="sxs-lookup"><span data-stu-id="ccf53-295">Verify that hello proper user and group setting is valid, similar to: `-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`</span></span>

         <span data-ttu-id="ccf53-296">如果 hello 檔案不存在或 hello 使用者和群組設定有誤，採取更正動作[準備 Linux 伺服器](#prepare-a-linux-server)。</span><span class="sxs-lookup"><span data-stu-id="ccf53-296">If hello file does not exist or hello user and group setting is wrong, take corrective action by [Preparing a Linux server](#prepare-a-linux-server).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccf53-297">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccf53-297">Next steps</span></span>
* <span data-ttu-id="ccf53-298">使用[記錄搜尋](log-analytics-log-searches.md)中記錄分析 tooview 詳細的 VMware 主機的資料。</span><span class="sxs-lookup"><span data-stu-id="ccf53-298">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed VMware host data.</span></span>
* <span data-ttu-id="ccf53-299">[建立您自己的儀表板](log-analytics-dashboards.md)來顯示 VMware 主機的資料。</span><span class="sxs-lookup"><span data-stu-id="ccf53-299">[Create your own dashboards](log-analytics-dashboards.md) showing VMware host data.</span></span>
* <span data-ttu-id="ccf53-300">在特定的 VMware 主機事件發生時[建立警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="ccf53-300">[Create alerts](log-analytics-alerts.md) when specific VMware host events occur.</span></span>
