---
title: "Log Analytics 中的 VMware 監視解決方案 | Microsoft Docs"
description: "了解 VMware 監視解決方案如何協助您管理記錄檔和監視 ESXi 主機。"
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
ms.openlocfilehash: 17072c4b6e4fdf6e4dc2b7a6a4ded7fa9f9f6fde
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a><span data-ttu-id="49b16-103">Log Analytics 中的 VMware 監視 (預覽) 解決方案</span><span class="sxs-lookup"><span data-stu-id="49b16-103">VMware Monitoring (Preview) solution in Log Analytics</span></span>

![VMware 符號](./media/log-analytics-vmware/vmware-symbol.png)

<span data-ttu-id="49b16-105">Log Analytics 中的 VMware 監視解決方案是一個可協助您針對大型 VMware 記錄檔建立集中記錄和監視方法的解決方案。</span><span class="sxs-lookup"><span data-stu-id="49b16-105">The VMware Monitoring solution in Log Analytics is a solution that helps you create a centralized logging and monitoring approach for large VMware logs.</span></span> <span data-ttu-id="49b16-106">本文說明如何使用此解決方案在單一位置進行疑難排解、擷取和管理 ESXi 主機。</span><span class="sxs-lookup"><span data-stu-id="49b16-106">This article describes how you can troubleshoot, capture, and manage the ESXi hosts in a single location using the solution.</span></span> <span data-ttu-id="49b16-107">有了這個解決方案，您可以在單一位置查看所有 ESXi 主機的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="49b16-107">With the solution, you can see detailed data for all your ESXi hosts in a single location.</span></span> <span data-ttu-id="49b16-108">您可以看到 VM 和 ESXi 主機上前幾名的事件計數、狀態和趨勢，透過 ESXi 主機記錄檔提供。</span><span class="sxs-lookup"><span data-stu-id="49b16-108">You can see top event counts, status, and trends of VM and ESXi hosts provided through the ESXi host logs.</span></span> <span data-ttu-id="49b16-109">您可以檢視及搜尋 ESXi 主機集中記錄檔，來進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="49b16-109">You can troubleshoot by viewing and searching centralized ESXi host logs.</span></span> <span data-ttu-id="49b16-110">而且，您可以根據記錄檔搜尋查詢來建立警示。</span><span class="sxs-lookup"><span data-stu-id="49b16-110">And, you can create alerts based on log search queries.</span></span>

<span data-ttu-id="49b16-111">解決方案會使用 ESXi 主機的原生 syslog 功能來將資料推播至具有 OMS 代理程式的目標 VM。</span><span class="sxs-lookup"><span data-stu-id="49b16-111">The solution uses native syslog functionality of the ESXi host to push data to a target VM, which has OMS Agent.</span></span> <span data-ttu-id="49b16-112">但是，解決方案不會將檔案寫入目標 VM 內部的 syslog。</span><span class="sxs-lookup"><span data-stu-id="49b16-112">However, the solution doesn't write files into syslog within the target VM.</span></span> <span data-ttu-id="49b16-113">OMS 代理程式會開啟連接埠 1514 並接聽該連接埠。</span><span class="sxs-lookup"><span data-stu-id="49b16-113">The OMS agent opens port 1514 and listens to this.</span></span> <span data-ttu-id="49b16-114">OMS 代理程式在收到資料之後，就會將資料推播至 OMS 中。</span><span class="sxs-lookup"><span data-stu-id="49b16-114">Once it receives the data, the OMS agent pushes the data into OMS.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="49b16-115">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="49b16-115">Installing and configuring the solution</span></span>
<span data-ttu-id="49b16-116">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="49b16-116">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="49b16-117">使用[從方案庫加入 Log Analytics 方案](log-analytics-add-solutions.md)中的程序，將 VMware 監視解決方案新增您的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="49b16-117">Add the VMware Monitoring solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

#### <a name="supported-vmware-esxi-hosts"></a><span data-ttu-id="49b16-118">支援的 VMware ESXi 主機</span><span class="sxs-lookup"><span data-stu-id="49b16-118">Supported VMware ESXi hosts</span></span>
<span data-ttu-id="49b16-119">vSphere ESXi 主機 5.5 和 6.0</span><span class="sxs-lookup"><span data-stu-id="49b16-119">vSphere ESXi Host 5.5 and 6.0</span></span>

#### <a name="prepare-a-linux-server"></a><span data-ttu-id="49b16-120">準備 Linux 伺服器</span><span class="sxs-lookup"><span data-stu-id="49b16-120">Prepare a Linux server</span></span>
<span data-ttu-id="49b16-121">建立 Linux 作業系統 VM 來接收來自 ESXi 主機的所有 syslog 資料。</span><span class="sxs-lookup"><span data-stu-id="49b16-121">Create a Linux operating system VM to receive all syslog data from the ESXi hosts.</span></span> <span data-ttu-id="49b16-122">[OMS Linux 代理程式](log-analytics-linux-agents.md)是所有 ESXi 主機 syslog 資料的收集點。</span><span class="sxs-lookup"><span data-stu-id="49b16-122">The [OMS Linux Agent](log-analytics-linux-agents.md) is the collection point for all ESXi host syslog data.</span></span> <span data-ttu-id="49b16-123">您可以使用多個 ESXi 主機將記錄檔轉送到單一 Linux 伺服器，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="49b16-123">You can use multiple ESXi hosts to forward logs to a single Linux server, as in the following example.</span></span>  

   ![syslog 流程](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a><span data-ttu-id="49b16-125">設定 syslog 收集</span><span class="sxs-lookup"><span data-stu-id="49b16-125">Configure syslog collection</span></span>
1. <span data-ttu-id="49b16-126">設定 VSphere 的 syslog 轉送。</span><span class="sxs-lookup"><span data-stu-id="49b16-126">Set up syslog forwarding for VSphere.</span></span> <span data-ttu-id="49b16-127">如需詳細資訊來協助您設定 syslog 轉送，請參閱[設定 ESXi 5.x 和 6.0 上的 syslog (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322)。</span><span class="sxs-lookup"><span data-stu-id="49b16-127">For detailed information to help set up syslog forwarding, see [Configuring syslog on ESXi 5.x and 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322).</span></span> <span data-ttu-id="49b16-128">移至 [ESXi 主機組態]  >  [軟體]  >  [進階設定]  >  [Syslog]。</span><span class="sxs-lookup"><span data-stu-id="49b16-128">Go to **ESXi Host Configuration** > **Software** > **Advanced Settings** > **Syslog**.</span></span>
   <span data-ttu-id="49b16-129">![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)</span><span class="sxs-lookup"><span data-stu-id="49b16-129">![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)</span></span>  
2. <span data-ttu-id="49b16-130">在 [Syslog.global.logHost] 欄位中，新增您的 Linux 伺服器和連接埠號碼 1514。</span><span class="sxs-lookup"><span data-stu-id="49b16-130">In the *Syslog.global.logHost* field, add your Linux server and the port number *1514*.</span></span> <span data-ttu-id="49b16-131">例如，`tcp://hostname:1514` 或 `tcp://123.456.789.101:1514`。</span><span class="sxs-lookup"><span data-stu-id="49b16-131">For example, `tcp://hostname:1514` or `tcp://123.456.789.101:1514`</span></span>
3. <span data-ttu-id="49b16-132">為 syslog 開啟 ESXi 主機防火牆。</span><span class="sxs-lookup"><span data-stu-id="49b16-132">Open the ESXi host firewall for syslog.</span></span> <span data-ttu-id="49b16-133">[ESXi 主機組態]  >  [軟體]  >  [安全性設定檔]  >  [防火牆]，然後開啟 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="49b16-133">**ESXi Host Configuration** > **Software** > **Security Profile** > **Firewall** and open **Properties**.</span></span>  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. <span data-ttu-id="49b16-136">檢查 vSphere 主控台，確認 syslog 設定正確。</span><span class="sxs-lookup"><span data-stu-id="49b16-136">Check the vSphere Console to verify that that syslog is properly set up.</span></span> <span data-ttu-id="49b16-137">確認 ESXI 主機上已設定連接埠 **1514**。</span><span class="sxs-lookup"><span data-stu-id="49b16-137">Confirm on the ESXI host that port **1514** is configured.</span></span>
5. <span data-ttu-id="49b16-138">在 Linux 伺服器上下載並安裝 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="49b16-138">Download and install the OMS Agent for Linux on the Linux server.</span></span> <span data-ttu-id="49b16-139">如需詳細資訊，請參閱 [OMS Agent for Linux 的文件](https://github.com/Microsoft/OMS-Agent-for-Linux)。</span><span class="sxs-lookup"><span data-stu-id="49b16-139">For more information, see the [Documentation for OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).</span></span>
6. <span data-ttu-id="49b16-140">安裝 OMS Agent for Linux 後，移至 /etc/opt/microsoft/omsagent/sysconf/omsagent.d 目錄，將 vmware_esxi.conf 檔複製到 /etc/opt/microsoft/omsagent/conf/omsagent.d directory 目錄，並變更檔案的擁有者/群組和權限。</span><span class="sxs-lookup"><span data-stu-id="49b16-140">After the OMS Agent for Linux is installed, go to the  /etc/opt/microsoft/omsagent/sysconf/omsagent.d directory and copy the vmware_esxi.conf file to the /etc/opt/microsoft/omsagent/conf/omsagent.d directory and the change the owner/group and permissions of the file.</span></span> <span data-ttu-id="49b16-141">例如：</span><span class="sxs-lookup"><span data-stu-id="49b16-141">For example:</span></span>

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. <span data-ttu-id="49b16-142">執行 `sudo /opt/microsoft/omsagent/bin/service_control restart` 啟動 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="49b16-142">Restart the OMS Agent for Linux by running `sudo /opt/microsoft/omsagent/bin/service_control restart`.</span></span>
8. <span data-ttu-id="49b16-143">在 ESXi 主機上使用 `nc`命令測試 Linux 伺服器和 ESXi 主機之間的連線。</span><span class="sxs-lookup"><span data-stu-id="49b16-143">Test the connectivity between the Linux server and the ESXi host by using the `nc` command on the ESXi Host.</span></span> <span data-ttu-id="49b16-144">例如：</span><span class="sxs-lookup"><span data-stu-id="49b16-144">For example:</span></span>

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection to 123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. <span data-ttu-id="49b16-145">在 OMS 入口網站中，執行 `Type=VMware_CL` 的記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="49b16-145">In the OMS Portal, perform a log search for `Type=VMware_CL`.</span></span> <span data-ttu-id="49b16-146">當 OMS 收集 syslog 時，會保留 syslog 的格式。</span><span class="sxs-lookup"><span data-stu-id="49b16-146">When OMS collects the syslog data, it retains the syslog format.</span></span> <span data-ttu-id="49b16-147">在入口網站中，會擷取某些特定欄位，例如 Hostname 和 ProcessName。</span><span class="sxs-lookup"><span data-stu-id="49b16-147">In the portal, some specific fields are captured, such as *Hostname* and *ProcessName*.</span></span>  

    ![類型](./media/log-analytics-vmware/type.png)  

    <span data-ttu-id="49b16-149">如果您的記錄檔搜尋結果類似上圖，表示您可以開始使用 OMS VMware 監視解決方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="49b16-149">If your view log search results are similar to the image above, you're set to use the OMS VMware Monitoring solution dashboard.</span></span>  

## <a name="vmware-data-collection-details"></a><span data-ttu-id="49b16-150">VMware 資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="49b16-150">VMware data collection details</span></span>
<span data-ttu-id="49b16-151">VMware 監視解決方案會使用您已啟用的 OMS Agents for Linux，從 ESXi 主機收集各種效能度量和記錄檔資料。</span><span class="sxs-lookup"><span data-stu-id="49b16-151">The VMware Monitoring solution collects various performance metrics and log data from ESXi hosts using the OMS Agents for Linux that you have enabled.</span></span>

<span data-ttu-id="49b16-152">下表顯示資料收集方法和其他資料收集方式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="49b16-152">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="49b16-153">平台</span><span class="sxs-lookup"><span data-stu-id="49b16-153">platform</span></span> | <span data-ttu-id="49b16-154">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="49b16-154">OMS Agent for Linux</span></span> | <span data-ttu-id="49b16-155">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="49b16-155">SCOM agent</span></span> | <span data-ttu-id="49b16-156">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="49b16-156">Azure Storage</span></span> | <span data-ttu-id="49b16-157">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="49b16-157">SCOM required?</span></span> | <span data-ttu-id="49b16-158">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="49b16-158">SCOM agent data sent via management group</span></span> | <span data-ttu-id="49b16-159">收集頻率</span><span class="sxs-lookup"><span data-stu-id="49b16-159">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="49b16-160">Linux</span><span class="sxs-lookup"><span data-stu-id="49b16-160">Linux</span></span> |<span data-ttu-id="49b16-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="49b16-161">&#8226;</span></span> |  |  |  |  |<span data-ttu-id="49b16-162">每隔 3 分鐘</span><span class="sxs-lookup"><span data-stu-id="49b16-162">every 3 minutes</span></span> |

<span data-ttu-id="49b16-163">下表顯示由 VMware 監視解決方案收集的資料欄位範例︰</span><span class="sxs-lookup"><span data-stu-id="49b16-163">The following table show examples of data fields collected by the VMware Monitoring solution:</span></span>

| <span data-ttu-id="49b16-164">欄位名稱</span><span class="sxs-lookup"><span data-stu-id="49b16-164">field name</span></span> | <span data-ttu-id="49b16-165">說明</span><span class="sxs-lookup"><span data-stu-id="49b16-165">description</span></span> |
| --- | --- |
| <span data-ttu-id="49b16-166">Device_s</span><span class="sxs-lookup"><span data-stu-id="49b16-166">Device_s</span></span> |<span data-ttu-id="49b16-167">VMware 儲存裝置</span><span class="sxs-lookup"><span data-stu-id="49b16-167">VMware storage devices</span></span> |
| <span data-ttu-id="49b16-168">ESXIFailure_s</span><span class="sxs-lookup"><span data-stu-id="49b16-168">ESXIFailure_s</span></span> |<span data-ttu-id="49b16-169">失敗類型</span><span class="sxs-lookup"><span data-stu-id="49b16-169">failure types</span></span> |
| <span data-ttu-id="49b16-170">EventTime_t</span><span class="sxs-lookup"><span data-stu-id="49b16-170">EventTime_t</span></span> |<span data-ttu-id="49b16-171">事件發生的時間</span><span class="sxs-lookup"><span data-stu-id="49b16-171">time when event occurred</span></span> |
| <span data-ttu-id="49b16-172">HostName_s</span><span class="sxs-lookup"><span data-stu-id="49b16-172">HostName_s</span></span> |<span data-ttu-id="49b16-173">ESXi 主機名稱</span><span class="sxs-lookup"><span data-stu-id="49b16-173">ESXi host name</span></span> |
| <span data-ttu-id="49b16-174">Operation_s</span><span class="sxs-lookup"><span data-stu-id="49b16-174">Operation_s</span></span> |<span data-ttu-id="49b16-175">建立 VM或刪除 VM</span><span class="sxs-lookup"><span data-stu-id="49b16-175">create VM or delete VM</span></span> |
| <span data-ttu-id="49b16-176">ProcessName_s</span><span class="sxs-lookup"><span data-stu-id="49b16-176">ProcessName_s</span></span> |<span data-ttu-id="49b16-177">事件名稱</span><span class="sxs-lookup"><span data-stu-id="49b16-177">event name</span></span> |
| <span data-ttu-id="49b16-178">ResourceId_s</span><span class="sxs-lookup"><span data-stu-id="49b16-178">ResourceId_s</span></span> |<span data-ttu-id="49b16-179">VMware 主機的名稱</span><span class="sxs-lookup"><span data-stu-id="49b16-179">name of the VMware host</span></span> |
| <span data-ttu-id="49b16-180">ResourceLocation_s</span><span class="sxs-lookup"><span data-stu-id="49b16-180">ResourceLocation_s</span></span> |<span data-ttu-id="49b16-181">VMware</span><span class="sxs-lookup"><span data-stu-id="49b16-181">VMware</span></span> |
| <span data-ttu-id="49b16-182">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="49b16-182">ResourceName_s</span></span> |<span data-ttu-id="49b16-183">VMware</span><span class="sxs-lookup"><span data-stu-id="49b16-183">VMware</span></span> |
| <span data-ttu-id="49b16-184">ResourceType_s</span><span class="sxs-lookup"><span data-stu-id="49b16-184">ResourceType_s</span></span> |<span data-ttu-id="49b16-185">Hyper-V</span><span class="sxs-lookup"><span data-stu-id="49b16-185">Hyper-V</span></span> |
| <span data-ttu-id="49b16-186">SCSIStatus_s</span><span class="sxs-lookup"><span data-stu-id="49b16-186">SCSIStatus_s</span></span> |<span data-ttu-id="49b16-187">VMware SCSI 的狀態</span><span class="sxs-lookup"><span data-stu-id="49b16-187">VMware SCSI status</span></span> |
| <span data-ttu-id="49b16-188">SyslogMessage_s</span><span class="sxs-lookup"><span data-stu-id="49b16-188">SyslogMessage_s</span></span> |<span data-ttu-id="49b16-189">syslog 資料</span><span class="sxs-lookup"><span data-stu-id="49b16-189">Syslog data</span></span> |
| <span data-ttu-id="49b16-190">UserName_s</span><span class="sxs-lookup"><span data-stu-id="49b16-190">UserName_s</span></span> |<span data-ttu-id="49b16-191">建立或刪除 VM 的使用者</span><span class="sxs-lookup"><span data-stu-id="49b16-191">user who created or deleted VM</span></span> |
| <span data-ttu-id="49b16-192">VMName_s</span><span class="sxs-lookup"><span data-stu-id="49b16-192">VMName_s</span></span> |<span data-ttu-id="49b16-193">VM 名稱</span><span class="sxs-lookup"><span data-stu-id="49b16-193">VM name</span></span> |
| <span data-ttu-id="49b16-194">電腦</span><span class="sxs-lookup"><span data-stu-id="49b16-194">Computer</span></span> |<span data-ttu-id="49b16-195">主機電腦</span><span class="sxs-lookup"><span data-stu-id="49b16-195">host computer</span></span> |
| <span data-ttu-id="49b16-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="49b16-196">TimeGenerated</span></span> |<span data-ttu-id="49b16-197">產生資料的時間</span><span class="sxs-lookup"><span data-stu-id="49b16-197">time the data was generated</span></span> |
| <span data-ttu-id="49b16-198">DataCenter_s</span><span class="sxs-lookup"><span data-stu-id="49b16-198">DataCenter_s</span></span> |<span data-ttu-id="49b16-199">VMware 資料中心</span><span class="sxs-lookup"><span data-stu-id="49b16-199">VMware datacenter</span></span> |
| <span data-ttu-id="49b16-200">StorageLatency_s</span><span class="sxs-lookup"><span data-stu-id="49b16-200">StorageLatency_s</span></span> |<span data-ttu-id="49b16-201">儲存體延遲 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="49b16-201">storage latency (ms)</span></span> |

## <a name="vmware-monitoring-solution-overview"></a><span data-ttu-id="49b16-202">VMware 監視解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="49b16-202">VMware Monitoring solution overview</span></span>
<span data-ttu-id="49b16-203">VMware 圖格會出現在 OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="49b16-203">The VMware tile appears in the OMS portal.</span></span> <span data-ttu-id="49b16-204">它提供任何失敗的高階檢視。</span><span class="sxs-lookup"><span data-stu-id="49b16-204">It provides a high-level view of any failures.</span></span> <span data-ttu-id="49b16-205">當您按一下圖格時，會進入儀表板檢視。</span><span class="sxs-lookup"><span data-stu-id="49b16-205">When you click the tile, you go into a dashboard view.</span></span>

![圖格](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-the-dashboard-view"></a><span data-ttu-id="49b16-207">瀏覽儀表板檢視</span><span class="sxs-lookup"><span data-stu-id="49b16-207">Navigate the dashboard view</span></span>
<span data-ttu-id="49b16-208">在 VMware 儀表板檢視中，各刀鋒視窗組織如下︰</span><span class="sxs-lookup"><span data-stu-id="49b16-208">In the **VMware** dashboard view, blades are organized by:</span></span>

* <span data-ttu-id="49b16-209">失敗狀態計數</span><span class="sxs-lookup"><span data-stu-id="49b16-209">Failure Status Count</span></span>
* <span data-ttu-id="49b16-210">依事件計數的主機前幾名</span><span class="sxs-lookup"><span data-stu-id="49b16-210">Top Host by Event Counts</span></span>
* <span data-ttu-id="49b16-211">前幾名事件計數</span><span class="sxs-lookup"><span data-stu-id="49b16-211">Top Event Counts</span></span>
* <span data-ttu-id="49b16-212">虛擬機器活動</span><span class="sxs-lookup"><span data-stu-id="49b16-212">Virtual Machine Activities</span></span>
* <span data-ttu-id="49b16-213">ESXi 主機磁碟的事件</span><span class="sxs-lookup"><span data-stu-id="49b16-213">ESXi Host Disk Events</span></span>

![解決方案1](./media/log-analytics-vmware/solutionview1-1.png)

![解決方案2](./media/log-analytics-vmware/solutionview1-2.png)

<span data-ttu-id="49b16-216">按一下任何刀鋒視窗以開啟 Log Analytics 搜尋窗格，窗格中會顯示該刀鋒視窗的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="49b16-216">Click any blade to open Log Analytics search pane that shows detailed information specific for the blade.</span></span>

<span data-ttu-id="49b16-217">您可以在此編輯搜尋查詢，修改查核來尋找特定目標。</span><span class="sxs-lookup"><span data-stu-id="49b16-217">From here, you can edit the search query to modify it for something specific.</span></span> <span data-ttu-id="49b16-218">如需 OMS 搜尋的基本概念教學，請參閱 [OMS 記錄記錄檔搜尋教學課程。](log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="49b16-218">For a tutorial on the basics of OMS search, check out the [OMS log search tutorial.](log-analytics-log-searches.md)</span></span>

#### <a name="find-esxi-host-events"></a><span data-ttu-id="49b16-219">尋找 ESXi 主機事件</span><span class="sxs-lookup"><span data-stu-id="49b16-219">Find ESXi host events</span></span>
<span data-ttu-id="49b16-220">單一 ESXi 主機會產生多個記錄檔，取決於其程序。</span><span class="sxs-lookup"><span data-stu-id="49b16-220">A single ESXi host generates multiple logs, based on their processes.</span></span> <span data-ttu-id="49b16-221">VMware 監視解決方案會將它們集中在一起，並總結事件計數。</span><span class="sxs-lookup"><span data-stu-id="49b16-221">The VMware Monitoring solution centralizes them and summarizes the event counts.</span></span> <span data-ttu-id="49b16-222">這個集中式的檢視可幫助您了解哪些 ESXi 主機有大量的事件，以及在您的環境中最常發生哪些事件。</span><span class="sxs-lookup"><span data-stu-id="49b16-222">This centralized view helps you understand which ESXi host has a high volume of events and what events occur most frequently in your environment.</span></span>

![事件](./media/log-analytics-vmware/events.png)

<span data-ttu-id="49b16-224">您可以按一下 ESXi 主機或事件類型，進一步深入探詢。</span><span class="sxs-lookup"><span data-stu-id="49b16-224">You can drill further by clicking an ESXi host or an event type.</span></span>

<span data-ttu-id="49b16-225">當您按一下的 ESXi 主機名稱時，可以檢視該 ESXi 主機的資訊。</span><span class="sxs-lookup"><span data-stu-id="49b16-225">When you click an ESXi host name, you view information from that ESXi host.</span></span> <span data-ttu-id="49b16-226">如果想要限縮事件類型的結果，在搜尋查詢中新增 `“ProcessName_s=EVENT TYPE”`。</span><span class="sxs-lookup"><span data-stu-id="49b16-226">If you want to narrow results with the event type, add `“ProcessName_s=EVENT TYPE”` in your search query.</span></span> <span data-ttu-id="49b16-227">您可以在搜尋篩選中選取 **ProcessName**。</span><span class="sxs-lookup"><span data-stu-id="49b16-227">You can select **ProcessName** in the search filter.</span></span> <span data-ttu-id="49b16-228">這會為您限縮資訊。</span><span class="sxs-lookup"><span data-stu-id="49b16-228">That narrows the information for you.</span></span>

![深入探詢](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a><span data-ttu-id="49b16-230">尋找高 VM 活動</span><span class="sxs-lookup"><span data-stu-id="49b16-230">Find high VM activities</span></span>
<span data-ttu-id="49b16-231">在任何 ESXi 主機上皆可以建立及刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="49b16-231">A virtual machine can be created and deleted on any ESXi host.</span></span> <span data-ttu-id="49b16-232">能識別 ESXi 主機建立多少個 VM，對系統管理員很有幫助，</span><span class="sxs-lookup"><span data-stu-id="49b16-232">It's helpful for an administrator to identify how many VMs an ESXi host creates.</span></span> <span data-ttu-id="49b16-233">進而幫助了解效能和容量規劃。</span><span class="sxs-lookup"><span data-stu-id="49b16-233">That in-turn, helps to understand performance and capacity planning.</span></span> <span data-ttu-id="49b16-234">管理您的環境時，持續追蹤 VM 活動事件極為重要。</span><span class="sxs-lookup"><span data-stu-id="49b16-234">Keeping track of VM activity events is crucial when managing your environment.</span></span>

![深入探詢](./media/log-analytics-vmware/vmactivities1.png)

<span data-ttu-id="49b16-236">如果您想要查看其他 ESXi 主機 VM 建立資料，按一下 ESXi 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="49b16-236">If you want to see additional ESXi host VM creation data, click an ESXi host name.</span></span>

![深入探詢](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a><span data-ttu-id="49b16-238">常見的搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="49b16-238">Common search queries</span></span>
<span data-ttu-id="49b16-239">這個解決方案包含其他實用的查詢，可協助您管理您的 ESXi 主機，例如高儲存量空間、儲存體延遲、路徑失敗。</span><span class="sxs-lookup"><span data-stu-id="49b16-239">The solution includes other useful queries that can help you manage your ESXi hosts, such as high storage space, storage latency, and path failure.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![查詢](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a><span data-ttu-id="49b16-241">儲存查詢</span><span class="sxs-lookup"><span data-stu-id="49b16-241">Save queries</span></span>
<span data-ttu-id="49b16-242">儲存搜尋查詢是 OMS 中的標準功能，可協助您保留任何您認為有用的查詢。</span><span class="sxs-lookup"><span data-stu-id="49b16-242">Saving search queries is a standard feature in OMS and can help you keep any queries that you’ve found useful.</span></span> <span data-ttu-id="49b16-243">建立您覺得有用的查詢之後，按一下 [我的最愛] 儲存它。</span><span class="sxs-lookup"><span data-stu-id="49b16-243">After you create a query that you find useful, save it by clicking the **Favorites**.</span></span> <span data-ttu-id="49b16-244">儲存的查詢讓您之後可從 [我的儀表板](log-analytics-dashboards.md) 頁面輕鬆地重複使用它們，您也可以在此建立您自己自訂的儀表板。</span><span class="sxs-lookup"><span data-stu-id="49b16-244">A saved query lets you easily reuse it later from the [My Dashboard](log-analytics-dashboards.md) page where you can create your own custom dashboards.</span></span>

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a><span data-ttu-id="49b16-246">從查詢建立警示</span><span class="sxs-lookup"><span data-stu-id="49b16-246">Create alerts from queries</span></span>
<span data-ttu-id="49b16-247">建立您的查詢後，您可能想要使用該查詢在特定事件發生時發出警示。</span><span class="sxs-lookup"><span data-stu-id="49b16-247">After you’ve created your queries, you might want to use the queries to alert you when specific events occur.</span></span> <span data-ttu-id="49b16-248">如需有關如何建立警示的資訊，請參閱 [Log Analytics 中的警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="49b16-248">See [Alerts in Log Analytics](log-analytics-alerts.md) for information about how to create alerts.</span></span> <span data-ttu-id="49b16-249">如需警示查詢和其他查詢的範例，請參閱部落格文章[使用 OMS Log Analytics 監視 VMware](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics)。</span><span class="sxs-lookup"><span data-stu-id="49b16-249">For examples of alerting queries and other query examples, see the [Monitor VMware using OMS Log Analytics](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) blog post.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="49b16-250">常見問題集</span><span class="sxs-lookup"><span data-stu-id="49b16-250">Frequently asked questions</span></span>
### <a name="what-do-i-need-to-do-on-the-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a><span data-ttu-id="49b16-251">我需要在 ESXi 主機設定上做什麼設定？</span><span class="sxs-lookup"><span data-stu-id="49b16-251">What do I need to do on the ESXi host setting?</span></span> <span data-ttu-id="49b16-252">它會對我目前的環境造成什麼影響？</span><span class="sxs-lookup"><span data-stu-id="49b16-252">What impact will it have on my current environment?</span></span>
<span data-ttu-id="49b16-253">解決方案會使用原生 ESXi 主機 Syslog 轉送機制。</span><span class="sxs-lookup"><span data-stu-id="49b16-253">The solution uses the native ESXi Host Syslog forwarding mechanism.</span></span> <span data-ttu-id="49b16-254">您在 ESXi 主機上不需要任何額外的 Microsoft 軟體就可以擷取記錄檔。</span><span class="sxs-lookup"><span data-stu-id="49b16-254">You don't need any additional Microsoft software on the ESXi Host to capture the logs.</span></span> <span data-ttu-id="49b16-255">它對您現有的環境影響不大。</span><span class="sxs-lookup"><span data-stu-id="49b16-255">It should have a low impact to your existing environment.</span></span> <span data-ttu-id="49b16-256">但是，您需要設定 syslog 轉送，這是 ESXI 功能。</span><span class="sxs-lookup"><span data-stu-id="49b16-256">However, you do need to set syslog forwarding, which is ESXI functionality.</span></span>

### <a name="do-i-need-to-restart-my-esxi-host"></a><span data-ttu-id="49b16-257">我需要重新啟動 ESXi 主機嗎？</span><span class="sxs-lookup"><span data-stu-id="49b16-257">Do I need to restart my ESXi host?</span></span>
<span data-ttu-id="49b16-258">否。</span><span class="sxs-lookup"><span data-stu-id="49b16-258">No.</span></span> <span data-ttu-id="49b16-259">此處理序不需要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="49b16-259">This process does not require a restart.</span></span> <span data-ttu-id="49b16-260">有時候，vSphere 不會正確更新 syslog。</span><span class="sxs-lookup"><span data-stu-id="49b16-260">Sometimes, vSphere does not properly update the syslog.</span></span> <span data-ttu-id="49b16-261">在這種情況下，請登入 ESXi 主機並重新載入 syslog。</span><span class="sxs-lookup"><span data-stu-id="49b16-261">In such a case, log on to the ESXi host and reload the syslog.</span></span> <span data-ttu-id="49b16-262">同樣地，您不需要重新啟動主機，所以此處理序不會干擾到您的環境。</span><span class="sxs-lookup"><span data-stu-id="49b16-262">Again, you don't have to restart the host, so this process isn't disruptive to your environment.</span></span>

### <a name="can-i-increase-or-decrease-the-volume-of-log-data-sent-to-oms"></a><span data-ttu-id="49b16-263">我可以增加或減少傳送至 OMS 的記錄資料量嗎？</span><span class="sxs-lookup"><span data-stu-id="49b16-263">Can I increase or decrease the volume of log data sent to OMS?</span></span>
<span data-ttu-id="49b16-264">是，您可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="49b16-264">Yes you can.</span></span> <span data-ttu-id="49b16-265">您可以使用 vSphere 中的 ESXi 主機記錄層級設定。</span><span class="sxs-lookup"><span data-stu-id="49b16-265">You can use the ESXi Host Log Level settings in vSphere.</span></span> <span data-ttu-id="49b16-266">記錄集合是以 *info* 層級為基礎。</span><span class="sxs-lookup"><span data-stu-id="49b16-266">Log collection is based on the *info* level.</span></span> <span data-ttu-id="49b16-267">所以，如果您想要稽核 VM 建立或刪除，您需要在 Hostd 上維持 *info* 層級。</span><span class="sxs-lookup"><span data-stu-id="49b16-267">So, if you want to audit VM creation or deletion, you need to keep the *info* level on Hostd.</span></span> <span data-ttu-id="49b16-268">如需詳細資訊，請參閱 [VMware 知識庫](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658)。</span><span class="sxs-lookup"><span data-stu-id="49b16-268">For more information, see the [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).</span></span>

### <a name="why-is-hostd-not-providing-data-to-oms-my-log-setting-is-set-to-info"></a><span data-ttu-id="49b16-269">為什麼 Hostd 沒有提供資料給 OMS？</span><span class="sxs-lookup"><span data-stu-id="49b16-269">Why is Hostd not providing data to OMS?</span></span> <span data-ttu-id="49b16-270">我的記錄檔設定是設為 info。</span><span class="sxs-lookup"><span data-stu-id="49b16-270">My log setting is set to info.</span></span>
<span data-ttu-id="49b16-271">syslog 時間戳記有一個 ESXi 主機錯誤。</span><span class="sxs-lookup"><span data-stu-id="49b16-271">There was an ESXi host bug for the syslog timestamp.</span></span> <span data-ttu-id="49b16-272">如需詳細資訊，請參閱 [VMware 知識庫](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202)。</span><span class="sxs-lookup"><span data-stu-id="49b16-272">For more information, see the [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202).</span></span> <span data-ttu-id="49b16-273">在您套用因應措施之後，Hostd 應該就能正常運作。</span><span class="sxs-lookup"><span data-stu-id="49b16-273">After you apply the workaround, Hostd should function normally.</span></span>

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-to-a-single-vm-with-omsagent"></a><span data-ttu-id="49b16-274">我可以使用 OMS 代理程式讓多部 ESXi 主機轉送 syslog 資料至單一 VM 嗎？</span><span class="sxs-lookup"><span data-stu-id="49b16-274">Can I have multiple ESXi hosts forwarding syslog data to a single VM with omsagent?</span></span>
<span data-ttu-id="49b16-275">是。</span><span class="sxs-lookup"><span data-stu-id="49b16-275">Yes.</span></span> <span data-ttu-id="49b16-276">您可以使用 OMS 代理程式讓多部 ESXi 主機轉送資料至單一 VM。</span><span class="sxs-lookup"><span data-stu-id="49b16-276">You can have multiple ESXi hosts forwarding to a single VM with omsagent.</span></span>

### <a name="why-dont-i-see-data-flowing-into-oms"></a><span data-ttu-id="49b16-277">為什麼我沒有看到資料流入 OMS？</span><span class="sxs-lookup"><span data-stu-id="49b16-277">Why don't I see data flowing into OMS?</span></span>
<span data-ttu-id="49b16-278">這有幾個原因：</span><span class="sxs-lookup"><span data-stu-id="49b16-278">There can be multiple reasons:</span></span>

* <span data-ttu-id="49b16-279">ESXi 主機目前沒有推播資料至執行 OMS 代理程式的 VM。</span><span class="sxs-lookup"><span data-stu-id="49b16-279">The ESXi host is not correctly pushing data to the VM running omsagent.</span></span> <span data-ttu-id="49b16-280">若要測試，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="49b16-280">To test, perform the following steps:</span></span>

  1. <span data-ttu-id="49b16-281">若要確認，請使用 SSH 登入 ESXi 主機並執行以下命令：`nc -z ipaddressofVM 1514`</span><span class="sxs-lookup"><span data-stu-id="49b16-281">To confirm, log on to the ESXi host using ssh and run the following command: `nc -z ipaddressofVM 1514`</span></span>

      <span data-ttu-id="49b16-282">如果這沒有成功，表示進階組態中的 vSphere 設定可能不正確。</span><span class="sxs-lookup"><span data-stu-id="49b16-282">If this is not successful, vSphere settings in the Advanced Configuration are likely not correct.</span></span> <span data-ttu-id="49b16-283">請參閱[設定 syslog 集合](#configure-syslog-collection)，以瞭解如何設定 ESXi 主機來進行 syslog 轉送的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="49b16-283">See [Configure syslog collection](#configure-syslog-collection) for information about how to set up the ESXi host for syslog forwarding.</span></span>
  2. <span data-ttu-id="49b16-284">如果 syslog 連接埠連線成功，但您還是沒有看到任何資料，請使用 ssh 並執行以下命令來於 ESXi 主機上重新載入 syslog：` esxcli system syslog reload`</span><span class="sxs-lookup"><span data-stu-id="49b16-284">If syslog port connectivity is successful, but you don't still see any data, then reload the syslog on the ESXi host by using ssh to run the following command: ` esxcli system syslog reload`</span></span>
* <span data-ttu-id="49b16-285">未正確設定具有 OMS 代理程式的 VM。</span><span class="sxs-lookup"><span data-stu-id="49b16-285">The VM with OMS Agent is not set correctly.</span></span> <span data-ttu-id="49b16-286">若要測試，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="49b16-286">To test this, perform the following steps:</span></span>

  1. <span data-ttu-id="49b16-287">OMS 會接聽連接埠 1514 並將資料推播到 OMS 中。</span><span class="sxs-lookup"><span data-stu-id="49b16-287">OMS listens to the port 1514 and pushes data into OMS.</span></span> <span data-ttu-id="49b16-288">若要確認它是否已經開啟，請執行以下命令：`netstat -a | grep 1514`</span><span class="sxs-lookup"><span data-stu-id="49b16-288">To verify that it is open, run the following command: `netstat -a | grep 1514`</span></span>
  2. <span data-ttu-id="49b16-289">您應該會看到連接埠 `1514/tcp` 已開啟。</span><span class="sxs-lookup"><span data-stu-id="49b16-289">You should see port `1514/tcp` open.</span></span> <span data-ttu-id="49b16-290">如果沒有，請確認是否已正確安裝 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="49b16-290">If you do not, verify that the omsagent is installed correctly.</span></span> <span data-ttu-id="49b16-291">如果您沒有看到連接埠資訊，表示 VM 上沒有開啟 syslog 連接埠。</span><span class="sxs-lookup"><span data-stu-id="49b16-291">If you do not see the port information, then the syslog port is not open on the VM.</span></span>

     1. <span data-ttu-id="49b16-292">請使用 `ps -ef | grep oms` 確認 OMS 代理程式是否在執行中。</span><span class="sxs-lookup"><span data-stu-id="49b16-292">Verify that the OMS Agent is running by using `ps -ef | grep oms`.</span></span> <span data-ttu-id="49b16-293">如果它沒有執行，請執行命令 ` sudo /opt/microsoft/omsagent/bin/service_control start`</span><span class="sxs-lookup"><span data-stu-id="49b16-293">If it is not running, start the process by running the command ` sudo /opt/microsoft/omsagent/bin/service_control start`</span></span>
     2. <span data-ttu-id="49b16-294">開啟 `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` 檔案。</span><span class="sxs-lookup"><span data-stu-id="49b16-294">Open the `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` file.</span></span>

         <span data-ttu-id="49b16-295">確認適當的使用者和群組設定有效，類似於：`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`</span><span class="sxs-lookup"><span data-stu-id="49b16-295">Verify that the proper user and group setting is valid, similar to: `-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`</span></span>

         <span data-ttu-id="49b16-296">如果檔案不存在或使用者和群組設定錯誤，請透過[準備 Linux 伺服器](#prepare-a-linux-server)來採取更正動作。</span><span class="sxs-lookup"><span data-stu-id="49b16-296">If the file does not exist or the user and group setting is wrong, take corrective action by [Preparing a Linux server](#prepare-a-linux-server).</span></span>

## <a name="next-steps"></a><span data-ttu-id="49b16-297">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49b16-297">Next steps</span></span>
* <span data-ttu-id="49b16-298">使用 Log Analytics 中的 [Log Analytics](log-analytics-log-searches.md) 檢視詳細的 VMware 主機資料。</span><span class="sxs-lookup"><span data-stu-id="49b16-298">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed VMware host data.</span></span>
* <span data-ttu-id="49b16-299">[建立您自己的儀表板](log-analytics-dashboards.md)來顯示 VMware 主機的資料。</span><span class="sxs-lookup"><span data-stu-id="49b16-299">[Create your own dashboards](log-analytics-dashboards.md) showing VMware host data.</span></span>
* <span data-ttu-id="49b16-300">在特定的 VMware 主機事件發生時[建立警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="49b16-300">[Create alerts](log-analytics-alerts.md) when specific VMware host events occur.</span></span>
