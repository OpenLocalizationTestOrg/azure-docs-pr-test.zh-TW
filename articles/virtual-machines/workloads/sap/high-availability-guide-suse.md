---
title: "aaaAzure 虛擬機器的高可用性的 SAP NetWeaver SUSE Linux Enterprise Server 上的 SAP 應用程式 |Microsoft 文件"
description: "SAP NetWeaver 在適用於 SAP 應用程式之 SUSE Linux Enterprise Server 上的高可用性指南"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="7ad26-103">SAP NetWeaver 在適用於 SAP 應用程式之 SUSE Linux Enterprise Server 上的 Azure VM 高可用性</span><span class="sxs-lookup"><span data-stu-id="7ad26-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="7ad26-113">本文說明 toodeploy hello 虛擬機器，設定 hello 虛擬機器、 安裝 hello 叢集架構和安裝高可用性的 SAP NetWeaver 7.50 系統的方式。</span><span class="sxs-lookup"><span data-stu-id="7ad26-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="7ad26-114">在 hello 範例組態中，安裝命令等。會使用 ASCS 執行個體號碼 00、ERS 執行個體號碼 02 和 SAP 系統識別碼 NWS。</span><span class="sxs-lookup"><span data-stu-id="7ad26-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="7ad26-115">hello 名稱 hello 中的資源 （例如虛擬機器、 虛擬網路） hello 範例假設您已使用 hello[交集範本][ template-converged]與 SAP 系統識別碼 NWS toocreate hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="7ad26-116">讀取 hello 遵循 SAP 附註和白皮書</span><span class="sxs-lookup"><span data-stu-id="7ad26-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="7ad26-117">SAP Note [1928533]，其中包含：</span><span class="sxs-lookup"><span data-stu-id="7ad26-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="7ad26-118">Hello 部署 SAP 軟體所支援的 Azure VM 大小的清單</span><span class="sxs-lookup"><span data-stu-id="7ad26-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="7ad26-119">Azure VM 大小的重要容量資訊</span><span class="sxs-lookup"><span data-stu-id="7ad26-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="7ad26-120">支援的 SAP 軟體，以及作業系統 (OS) 與資料庫組合</span><span class="sxs-lookup"><span data-stu-id="7ad26-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="7ad26-121">Microsoft Azure 上 Windows 和 Linux 所需的 SAP 核心版本</span><span class="sxs-lookup"><span data-stu-id="7ad26-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="7ad26-122">SAP Note [2015553] 列出 Azure 中 SAP 支援的 SAP 軟體部署先決條件。</span><span class="sxs-lookup"><span data-stu-id="7ad26-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="7ad26-123">SAP Note [2205917] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的建議 OS 設定</span><span class="sxs-lookup"><span data-stu-id="7ad26-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="7ad26-124">SAP Note [1944799] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的 SAP HANA 指導方針</span><span class="sxs-lookup"><span data-stu-id="7ad26-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="7ad26-125">SAP Note [2178632] 包含在 Azure 中針對 SAP 回報的所有監視計量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ad26-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="7ad26-126">SAP 附註[2191498]具有 hello 必要 SAP Host Agent 版本適用於在 Azure 中的 Linux。</span><span class="sxs-lookup"><span data-stu-id="7ad26-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="7ad26-127">SAP Note [2243692] 包含 Azure 中 Linux 上的 SAP 授權相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ad26-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="7ad26-128">SAP Note [1984787] 包含 SUSE LINUX Enterprise Server 12 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="7ad26-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="7ad26-129">SAP 附註[1999351] hello Azure 強化監視功能延伸模組適用於 SAP 的其他疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="7ad26-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="7ad26-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) 包含 Linux 所需的所有 SAP Note。</span><span class="sxs-lookup"><span data-stu-id="7ad26-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="7ad26-131">[適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7ad26-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="7ad26-132">[適用於 SAP on Linux 的 Azure 虛擬機器部署 (本文)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7ad26-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="7ad26-133">[適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7ad26-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="7ad26-134">[SAP HANA SR 效能最佳化案例 (英文)][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="7ad26-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="7ad26-135">hello 指南包含所有必要的資訊 tooset SAP HANA 系統複寫在內部。</span><span class="sxs-lookup"><span data-stu-id="7ad26-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="7ad26-136">請使用此指南做為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ad26-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="7ad26-137">[高度可用 NFS 的存放裝置與 DRBD Pacemaker] [ suse-drbd-guide] hello 指南包含所有必要的資訊 tooset 高可用性的 NFS 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="7ad26-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="7ad26-138">請使用此指南做為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ad26-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="7ad26-139">概觀</span><span class="sxs-lookup"><span data-stu-id="7ad26-139">Overview</span></span>

<span data-ttu-id="7ad26-140">tooachieve 高可用性，SAP NetWeaver 需要 NFS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7ad26-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="7ad26-141">hello NFS 伺服器不同叢集中設定，並可供多個 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="7ad26-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![SAP NetWeaver 高可用性概觀](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="7ad26-143">hello NFS 伺服器，SAP NetWeaver ASCS、 SAP NetWeaver SCS、 SAP NetWeaver 端及 hello SAP HANA 資料庫使用虛擬的主機名稱和虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ad26-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="7ad26-144">在 Azure 上、 負載平衡器需要的 toouse 虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ad26-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="7ad26-145">hello 下列清單顯示 hello hello 負載平衡器組態。</span><span class="sxs-lookup"><span data-stu-id="7ad26-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="7ad26-146">NFS 伺服器</span><span class="sxs-lookup"><span data-stu-id="7ad26-146">NFS Server</span></span>
* <span data-ttu-id="7ad26-147">前端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-147">Frontend configuration</span></span>
  * <span data-ttu-id="7ad26-148">IP 位址 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="7ad26-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="7ad26-149">後端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-149">Backend configuration</span></span>
  * <span data-ttu-id="7ad26-150">連接 tooprimary 應該 hello NFS 叢集一部分的所有虛擬機器的網路介面</span><span class="sxs-lookup"><span data-stu-id="7ad26-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="7ad26-151">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="7ad26-151">Probe Port</span></span>
  * <span data-ttu-id="7ad26-152">連接埠 61000</span><span class="sxs-lookup"><span data-stu-id="7ad26-152">Port 61000</span></span>
* <span data-ttu-id="7ad26-153">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="7ad26-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="7ad26-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-154">2049 TCP</span></span> 
  * <span data-ttu-id="7ad26-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="7ad26-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="7ad26-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="7ad26-156">(A)SCS</span></span>
* <span data-ttu-id="7ad26-157">前端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-157">Frontend configuration</span></span>
  * <span data-ttu-id="7ad26-158">IP 位址 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="7ad26-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="7ad26-159">後端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-159">Backend configuration</span></span>
  * <span data-ttu-id="7ad26-160">應該是 hello (A) SCS/端叢集一部分的所有虛擬機器的連線的 tooprimary 網路介面</span><span class="sxs-lookup"><span data-stu-id="7ad26-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="7ad26-161">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="7ad26-161">Probe Port</span></span>
  * <span data-ttu-id="7ad26-162">連接埠 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="7ad26-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="7ad26-163">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="7ad26-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="7ad26-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="7ad26-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="7ad26-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="7ad26-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="7ad26-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="7ad26-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="7ad26-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="7ad26-171">ERS</span><span class="sxs-lookup"><span data-stu-id="7ad26-171">ERS</span></span>
* <span data-ttu-id="7ad26-172">前端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-172">Frontend configuration</span></span>
  * <span data-ttu-id="7ad26-173">IP 位址 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="7ad26-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="7ad26-174">後端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-174">Backend configuration</span></span>
  * <span data-ttu-id="7ad26-175">應該是 hello (A) SCS/端叢集一部分的所有虛擬機器的連線的 tooprimary 網路介面</span><span class="sxs-lookup"><span data-stu-id="7ad26-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="7ad26-176">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="7ad26-176">Probe Port</span></span>
  * <span data-ttu-id="7ad26-177">連接埠 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="7ad26-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="7ad26-178">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="7ad26-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="7ad26-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="7ad26-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="7ad26-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="7ad26-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="7ad26-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7ad26-183">SAP HANA</span></span>
* <span data-ttu-id="7ad26-184">前端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-184">Frontend configuration</span></span>
  * <span data-ttu-id="7ad26-185">IP 位址 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="7ad26-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="7ad26-186">後端組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-186">Backend configuration</span></span>
  * <span data-ttu-id="7ad26-187">連接 tooprimary 應該 hello HANA 叢集一部分的所有虛擬機器的網路介面</span><span class="sxs-lookup"><span data-stu-id="7ad26-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="7ad26-188">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="7ad26-188">Probe Port</span></span>
  * <span data-ttu-id="7ad26-189">連接埠 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="7ad26-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="7ad26-190">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="7ad26-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="7ad26-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="7ad26-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="7ad26-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="7ad26-193">設定高可用性的 NFS 伺服器</span><span class="sxs-lookup"><span data-stu-id="7ad26-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="7ad26-194">部署 Linux</span><span class="sxs-lookup"><span data-stu-id="7ad26-194">Deploying Linux</span></span>

<span data-ttu-id="7ad26-195">hello Azure Marketplace 包含您可以使用 toodeploy 新的虛擬機器的 SAP 應用程式 12 for SUSE Linux Enterprise Server 映像。</span><span class="sxs-lookup"><span data-stu-id="7ad26-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="7ad26-196">您可以使用其中一個 hello 快速入門範本 github toodeploy 上所有必要的資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="7ad26-197">hello 範本部署 hello 虛擬機器、 hello 負載平衡器、 可用性設定組等等。請遵循這些步驟 toodeploy hello 範本：</span><span class="sxs-lookup"><span data-stu-id="7ad26-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="7ad26-198">開啟 hello [SAP 檔案伺服器範本][ template-file-server] hello Azure 入口網站中</span><span class="sxs-lookup"><span data-stu-id="7ad26-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="7ad26-199">輸入下列參數的 hello</span><span class="sxs-lookup"><span data-stu-id="7ad26-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="7ad26-200">資源前置詞</span><span class="sxs-lookup"><span data-stu-id="7ad26-200">Resource Prefix</span></span>  
      <span data-ttu-id="7ad26-201">輸入您想要 toouse hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="7ad26-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="7ad26-202">hello 值用於部署的 hello 資源做為前置詞。</span><span class="sxs-lookup"><span data-stu-id="7ad26-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="7ad26-203">OS 類型</span><span class="sxs-lookup"><span data-stu-id="7ad26-203">Os Type</span></span>  
      <span data-ttu-id="7ad26-204">選取其中一個 hello Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="7ad26-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="7ad26-205">在此範例中，請選取 SLES 12</span><span class="sxs-lookup"><span data-stu-id="7ad26-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="7ad26-206">管理員使用者名稱和管理員密碼</span><span class="sxs-lookup"><span data-stu-id="7ad26-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="7ad26-207">會建立新的使用者，可以使用的 toolog toohello 機器上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="7ad26-208">子網路識別碼</span><span class="sxs-lookup"><span data-stu-id="7ad26-208">Subnet Id</span></span>  
      <span data-ttu-id="7ad26-209">hello 識別碼 hello 子網路 toowhich hello 虛擬機器應該連接到。</span><span class="sxs-lookup"><span data-stu-id="7ad26-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="7ad26-210">如果您想要 toocreate 新的虛擬網路，或選取 hello 子網路的 VPN 或 Express Route 虛擬網路 tooconnect hello 虛擬機器 tooyour 在內部部署網路將會保留空白。</span><span class="sxs-lookup"><span data-stu-id="7ad26-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="7ad26-211">hello 識別碼通常看起來像 /subscriptions/**&lt;訂用帳戶 id&gt;**/resourceGroups/**&lt;資源群組名稱&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;虛擬網路名稱&gt;**/subnets/**&lt;子網路名稱&gt;**</span><span class="sxs-lookup"><span data-stu-id="7ad26-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="7ad26-212">安裝</span><span class="sxs-lookup"><span data-stu-id="7ad26-212">Installation</span></span>

<span data-ttu-id="7ad26-213">hello 下列項目會加上  **[A]** -適用 tooall 節點**[1]** -適用 toonode 1 或**[2]** -適用 toonode 2。</span><span class="sxs-lookup"><span data-stu-id="7ad26-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="7ad26-214">**[A]** 更新 SLES</span><span class="sxs-lookup"><span data-stu-id="7ad26-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="7ad26-215">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="7ad26-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="7ad26-216">**[2]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="7ad26-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="7ad26-217">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="7ad26-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="7ad26-218">**[A]** 安裝 HA 擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ad26-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="7ad26-219">**[A]** 設定主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="7ad26-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="7ad26-220">您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="7ad26-221">這個範例會示範如何 toouse hello /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ad26-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="7ad26-222">取代 hello IP 位址和下列命令的 hello hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="7ad26-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="7ad26-223">插入 hello 下列各行太/等/主機。</span><span class="sxs-lookup"><span data-stu-id="7ad26-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="7ad26-224">變更您的環境的 hello IP 位址和主機名稱 toomatch</span><span class="sxs-lookup"><span data-stu-id="7ad26-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="7ad26-225">**[1]** 安裝叢集</span><span class="sxs-lookup"><span data-stu-id="7ad26-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="7ad26-226">**[2]**新增節點 toocluster</span><span class="sxs-lookup"><span data-stu-id="7ad26-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="7ad26-227">**[A]**變更 hacluster 密碼 toohello 相同的密碼</span><span class="sxs-lookup"><span data-stu-id="7ad26-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="7ad26-228">**[A]**設定 corosync toouse 其他傳輸，並加入節點清單。</span><span class="sxs-lookup"><span data-stu-id="7ad26-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="7ad26-229">否則叢集將無法運作。</span><span class="sxs-lookup"><span data-stu-id="7ad26-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="7ad26-230">新增下列內容的粗體 toohello 檔 hello。</span><span class="sxs-lookup"><span data-stu-id="7ad26-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="7ad26-231">然後重新啟動 hello corosync 服務</span><span class="sxs-lookup"><span data-stu-id="7ad26-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="7ad26-232">**[A]** 安裝 drbd 元件</span><span class="sxs-lookup"><span data-stu-id="7ad26-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="7ad26-233">**[A]**建立 hello drbd 裝置的資料分割</span><span class="sxs-lookup"><span data-stu-id="7ad26-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="7ad26-234">**[A]** 建立 LVM 組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="7ad26-235">**[A]**建立 hello NFS drbd 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="7ad26-236">插入新 drbd 裝置 hello 和結束的 hello 組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="7ad26-237">建立 hello drbd 裝置並啟動</span><span class="sxs-lookup"><span data-stu-id="7ad26-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="7ad26-238">**[1]** 略過首次同步處理</span><span class="sxs-lookup"><span data-stu-id="7ad26-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="7ad26-239">**[1]**組 hello 主要節點</span><span class="sxs-lookup"><span data-stu-id="7ad26-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="7ad26-240">**[1]**等候同步處理新 drbd 裝置 hello</span><span class="sxs-lookup"><span data-stu-id="7ad26-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="7ad26-241">**[1]** Drbd 裝置 hello 上建立檔案系統</span><span class="sxs-lookup"><span data-stu-id="7ad26-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="7ad26-242">設定叢集架構</span><span class="sxs-lookup"><span data-stu-id="7ad26-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="7ad26-243">**[1]**變更 hello 預設設定</span><span class="sxs-lookup"><span data-stu-id="7ad26-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="7ad26-244">**[1]**新增 hello NFS drbd 裝置 toohello 叢集設定</span><span class="sxs-lookup"><span data-stu-id="7ad26-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="7ad26-245">**[1]**建立 hello NFS 伺服器</span><span class="sxs-lookup"><span data-stu-id="7ad26-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="7ad26-246">**[1]**建立 hello NFS 檔案系統資源</span><span class="sxs-lookup"><span data-stu-id="7ad26-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="7ad26-247">**[1]**建立 hello NFS 匯出</span><span class="sxs-lookup"><span data-stu-id="7ad26-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="7ad26-248">**[1]**建立虛擬 IP 資源和 hello 內部負載平衡器的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="7ad26-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="7ad26-249">建立 STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-249">Create STONITH device</span></span>

<span data-ttu-id="7ad26-250">hello STONITH 裝置會使用針對 Microsoft Azure 服務主體 tooauthorize。</span><span class="sxs-lookup"><span data-stu-id="7ad26-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="7ad26-251">請遵循這些步驟 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="7ad26-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="7ad26-252">跳過<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="7ad26-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="7ad26-253">開啟 hello Azure Active Directory 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="7ad26-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="7ad26-254">請移 tooProperties 並寫下 hello 目錄識別碼。這是 hello**租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="7ad26-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="7ad26-255">按一下 [應用程式註冊]</span><span class="sxs-lookup"><span data-stu-id="7ad26-255">Click App registrations</span></span>
1. <span data-ttu-id="7ad26-256">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="7ad26-256">Click Add</span></span>
1. <span data-ttu-id="7ad26-257">輸入名稱、選取應用程式類型 [Web 應用程式/API]、輸入登入 URL (例如 http://localhost )，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="7ad26-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="7ad26-258">hello 登入 URL 不是，它可以是任何有效的 URL</span><span class="sxs-lookup"><span data-stu-id="7ad26-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="7ad26-259">選取 hello 新的應用程式，然後按一下 hello 設定 索引標籤中的 索引鍵</span><span class="sxs-lookup"><span data-stu-id="7ad26-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="7ad26-260">輸入新金鑰的說明、選取 [永不過期]，然後按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="7ad26-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="7ad26-261">記下 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7ad26-261">Write down hello Value.</span></span> <span data-ttu-id="7ad26-262">它會當做 hello 使用**密碼**hello 服務主體</span><span class="sxs-lookup"><span data-stu-id="7ad26-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="7ad26-263">請記下 hello 應用程式識別碼。它作為 hello 使用者名稱 (**登入識別碼**hello 步驟中) 的 hello 服務主體</span><span class="sxs-lookup"><span data-stu-id="7ad26-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="7ad26-264">hello 服務主體沒有權限 tooaccess 您的 Azure 資源預設。</span><span class="sxs-lookup"><span data-stu-id="7ad26-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="7ad26-265">您需要 toogive hello 服務主體的權限 toostart 和停止 （取消配置） hello 叢集的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7ad26-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="7ad26-266">移 toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="7ad26-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="7ad26-267">開啟 hello 所有資源刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="7ad26-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="7ad26-268">選取 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7ad26-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="7ad26-269">選取 [存取控制 (IAM)]</span><span class="sxs-lookup"><span data-stu-id="7ad26-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="7ad26-270">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="7ad26-270">Click Add</span></span>
1. <span data-ttu-id="7ad26-271">選取 hello 角色擁有者</span><span class="sxs-lookup"><span data-stu-id="7ad26-271">Select hello role Owner</span></span>
1. <span data-ttu-id="7ad26-272">輸入 hello hello 先前建立的應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="7ad26-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="7ad26-273">Click OK</span><span class="sxs-lookup"><span data-stu-id="7ad26-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="7ad26-274">**[1]**建立 hello STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="7ad26-275">編輯 hello hello 虛擬機器的權限之後，您可以設定 hello STONITH 裝置 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="7ad26-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="7ad26-276">**[1]** STONITH 裝置 hello 使用</span><span class="sxs-lookup"><span data-stu-id="7ad26-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="7ad26-277">設定 (A)SCS</span><span class="sxs-lookup"><span data-stu-id="7ad26-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="7ad26-278">部署 Linux</span><span class="sxs-lookup"><span data-stu-id="7ad26-278">Deploying Linux</span></span>

<span data-ttu-id="7ad26-279">hello Azure Marketplace 包含您可以使用 toodeploy 新的虛擬機器的 SAP 應用程式 12 for SUSE Linux Enterprise Server 映像。</span><span class="sxs-lookup"><span data-stu-id="7ad26-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="7ad26-280">hello marketplace 映像包含 SAP NetWeaver hello 資源代理的程式。</span><span class="sxs-lookup"><span data-stu-id="7ad26-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="7ad26-281">您可以使用其中一個 hello 快速入門範本 github toodeploy 上所有必要的資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="7ad26-282">hello 範本部署 hello 虛擬機器、 hello 負載平衡器、 可用性設定組等等。請遵循這些步驟 toodeploy hello 範本：</span><span class="sxs-lookup"><span data-stu-id="7ad26-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="7ad26-283">開啟 hello [ASCS/SCS 多重 SID 範本][ template-multisid-xscs]或 hello[交集範本][ template-converged]上 hello Azure 入口網站的 hello ASCS/SCS 僅限範本建立 hello 負載平衡規則的 SAP NetWeaver ASCS/SCS hello 和端 (只有 Linux) 執行個體，而 hello 交集的範本也會建立資料庫 （例如 Microsoft SQL Server 或 SAP HANA） hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="7ad26-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="7ad26-284">如果您計劃 tooinstall SAP NetWeaver 架構系統，而且也想 tooinstall hello 資料庫在 hello 相同的電腦，請使用 hello[交集範本][template-converged]。</span><span class="sxs-lookup"><span data-stu-id="7ad26-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="7ad26-285">輸入下列參數的 hello</span><span class="sxs-lookup"><span data-stu-id="7ad26-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="7ad26-286">資源前置詞 (僅限 ASCS/SCS 多重 SID 範本)</span><span class="sxs-lookup"><span data-stu-id="7ad26-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="7ad26-287">輸入您想要 toouse hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="7ad26-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="7ad26-288">hello 值用於部署的 hello 資源做為前置詞。</span><span class="sxs-lookup"><span data-stu-id="7ad26-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="7ad26-289">Sap 系統識別碼 (僅限交集範本)</span><span class="sxs-lookup"><span data-stu-id="7ad26-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="7ad26-290">輸入 hello 想 tooinstall 的 SAP 系統的 hello SAP 的系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="7ad26-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="7ad26-291">hello 識別碼用於部署的 hello 資源做為前置詞。</span><span class="sxs-lookup"><span data-stu-id="7ad26-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="7ad26-292">堆疊類型</span><span class="sxs-lookup"><span data-stu-id="7ad26-292">Stack Type</span></span>  
      <span data-ttu-id="7ad26-293">選取 hello SAP NetWeaver 堆疊類型</span><span class="sxs-lookup"><span data-stu-id="7ad26-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="7ad26-294">OS 類型</span><span class="sxs-lookup"><span data-stu-id="7ad26-294">Os Type</span></span>  
      <span data-ttu-id="7ad26-295">選取其中一個 hello Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="7ad26-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="7ad26-296">在此範例中，請選取 SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="7ad26-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="7ad26-297">DB 類型</span><span class="sxs-lookup"><span data-stu-id="7ad26-297">Db Type</span></span>  
      <span data-ttu-id="7ad26-298">選取 HANA</span><span class="sxs-lookup"><span data-stu-id="7ad26-298">Select HANA</span></span>
   7. <span data-ttu-id="7ad26-299">SAP 系統大小</span><span class="sxs-lookup"><span data-stu-id="7ad26-299">Sap System Size</span></span>  
      <span data-ttu-id="7ad26-300">提供的 SAPS hello 新系統的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="7ad26-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="7ad26-301">如果您不確定需要多少的 SAPS hello 系統，請要求您的 SAP 技術合作夥伴或系統整合者</span><span class="sxs-lookup"><span data-stu-id="7ad26-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="7ad26-302">系統可用性</span><span class="sxs-lookup"><span data-stu-id="7ad26-302">System Availability</span></span>  
      <span data-ttu-id="7ad26-303">選取 HA</span><span class="sxs-lookup"><span data-stu-id="7ad26-303">Select HA</span></span>
   9. <span data-ttu-id="7ad26-304">管理員使用者名稱和管理員密碼</span><span class="sxs-lookup"><span data-stu-id="7ad26-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="7ad26-305">會建立新的使用者，可以使用的 toolog toohello 機器上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="7ad26-306">子網路識別碼</span><span class="sxs-lookup"><span data-stu-id="7ad26-306">Subnet Id</span></span>  
   <span data-ttu-id="7ad26-307">hello 識別碼 hello 子網路 toowhich hello 虛擬機器應該連接到。</span><span class="sxs-lookup"><span data-stu-id="7ad26-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="7ad26-308">如果您想 toocreate 新的虛擬網路，或選取 hello 相同子網路，您在使用或建立為 hello NFS 伺服器部署的一部分，則會保留空白。</span><span class="sxs-lookup"><span data-stu-id="7ad26-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="7ad26-309">hello 識別碼通常看起來像 /subscriptions/**&lt;訂用帳戶 id&gt;**/resourceGroups/**&lt;資源群組名稱&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;虛擬網路名稱&gt;**/subnets/**&lt;子網路名稱&gt;**</span><span class="sxs-lookup"><span data-stu-id="7ad26-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="7ad26-310">安裝</span><span class="sxs-lookup"><span data-stu-id="7ad26-310">Installation</span></span>

<span data-ttu-id="7ad26-311">hello 下列項目會加上  **[A]** -適用 tooall 節點**[1]** -適用 toonode 1 或**[2]** -適用 toonode 2。</span><span class="sxs-lookup"><span data-stu-id="7ad26-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="7ad26-312">**[A]** 更新 SLES</span><span class="sxs-lookup"><span data-stu-id="7ad26-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="7ad26-313">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="7ad26-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="7ad26-314">**[2]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="7ad26-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="7ad26-315">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="7ad26-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="7ad26-316">**[A]** 安裝 HA 擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ad26-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="7ad26-317">**[A]** 更新 SAP 資源代理程式</span><span class="sxs-lookup"><span data-stu-id="7ad26-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="7ad26-318">修補程式 hello 資源代理程式套件是必要的 toouse hello 新的設定，這篇文章中所述。</span><span class="sxs-lookup"><span data-stu-id="7ad26-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="7ad26-319">您可以檢查，如果已經以 hello 下列命令安裝 hello 修補程式</span><span class="sxs-lookup"><span data-stu-id="7ad26-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="7ad26-320">hello 輸出應類似於</span><span class="sxs-lookup"><span data-stu-id="7ad26-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="7ad26-321">如果 hello grep 命令找不到 hello IS_ERS 參數，您需要在所列的 tooinstall hello 修補程式[hello SUSE 下載頁面](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="7ad26-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="7ad26-322">**[A]** 設定主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="7ad26-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="7ad26-323">您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="7ad26-324">這個範例會示範如何 toouse hello /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ad26-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="7ad26-325">取代 hello IP 位址和下列命令的 hello hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="7ad26-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="7ad26-326">插入 hello 下列各行太/等/主機。</span><span class="sxs-lookup"><span data-stu-id="7ad26-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="7ad26-327">變更您的環境的 hello IP 位址和主機名稱 toomatch</span><span class="sxs-lookup"><span data-stu-id="7ad26-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="7ad26-328">**[1]** 安裝叢集</span><span class="sxs-lookup"><span data-stu-id="7ad26-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="7ad26-329">**[2]**新增節點 toocluster</span><span class="sxs-lookup"><span data-stu-id="7ad26-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="7ad26-330">**[A]**變更 hacluster 密碼 toohello 相同的密碼</span><span class="sxs-lookup"><span data-stu-id="7ad26-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="7ad26-331">**[A]**設定 corosync toouse 其他傳輸，並加入節點清單。</span><span class="sxs-lookup"><span data-stu-id="7ad26-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="7ad26-332">否則叢集將無法運作。</span><span class="sxs-lookup"><span data-stu-id="7ad26-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="7ad26-333">新增下列內容的粗體 toohello 檔 hello。</span><span class="sxs-lookup"><span data-stu-id="7ad26-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="7ad26-334">然後重新啟動 hello corosync 服務</span><span class="sxs-lookup"><span data-stu-id="7ad26-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="7ad26-335">**[A]** 安裝 drbd 元件</span><span class="sxs-lookup"><span data-stu-id="7ad26-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="7ad26-336">**[A]**建立 hello drbd 裝置的資料分割</span><span class="sxs-lookup"><span data-stu-id="7ad26-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="7ad26-337">**[A]** 建立 LVM 組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="7ad26-338">**[A]**建立 hello SCS drbd 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="7ad26-339">插入新 drbd 裝置 hello 和結束的 hello 組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="7ad26-340">建立 hello drbd 裝置並啟動</span><span class="sxs-lookup"><span data-stu-id="7ad26-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="7ad26-341">**[A]**建立 hello 端 drbd 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="7ad26-342">插入新 drbd 裝置 hello 和結束的 hello 組態</span><span class="sxs-lookup"><span data-stu-id="7ad26-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="7ad26-343">建立 hello drbd 裝置並啟動</span><span class="sxs-lookup"><span data-stu-id="7ad26-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="7ad26-344">**[1]** 略過首次同步處理</span><span class="sxs-lookup"><span data-stu-id="7ad26-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="7ad26-345">**[1]**組 hello 主要節點</span><span class="sxs-lookup"><span data-stu-id="7ad26-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="7ad26-346">**[1]**等候同步處理新 drbd 裝置 hello</span><span class="sxs-lookup"><span data-stu-id="7ad26-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="7ad26-347">**[1]** Drbd 裝置 hello 上建立檔案系統</span><span class="sxs-lookup"><span data-stu-id="7ad26-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="7ad26-348">設定叢集架構</span><span class="sxs-lookup"><span data-stu-id="7ad26-348">Configure Cluster Framework</span></span>

<span data-ttu-id="7ad26-349">**[1]**變更 hello 預設設定</span><span class="sxs-lookup"><span data-stu-id="7ad26-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="7ad26-350">準備進行 SAP NetWeaver 安裝</span><span class="sxs-lookup"><span data-stu-id="7ad26-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="7ad26-351">**[A]**建立 hello 共用目錄</span><span class="sxs-lookup"><span data-stu-id="7ad26-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="7ad26-352">**[A]** 設定 autofs</span><span class="sxs-lookup"><span data-stu-id="7ad26-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="7ad26-353">使用下列命令建立檔案</span><span class="sxs-lookup"><span data-stu-id="7ad26-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="7ad26-354">重新啟動 autofs toomount hello 新的共用</span><span class="sxs-lookup"><span data-stu-id="7ad26-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="7ad26-355">**[A]** 設定分頁檔</span><span class="sxs-lookup"><span data-stu-id="7ad26-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="7ad26-356">重新啟動 hello 代理程式 tooactivate hello 變更</span><span class="sxs-lookup"><span data-stu-id="7ad26-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="7ad26-357">安裝 SAP NetWeaver ASCS/ERS</span><span class="sxs-lookup"><span data-stu-id="7ad26-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="7ad26-358">**[1]**建立虛擬 IP 資源和 hello 內部負載平衡器的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="7ad26-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="7ad26-359">請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="7ad26-360">它並不重要上執行哪些節點 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="7ad26-361">**[1]** 安裝 SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="7ad26-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="7ad26-362">為根 hello 使用虛擬的主機名稱，例如對應 hello 負載平衡器前端組態 hello ASCS toohello IP 位址的第一個節點上安裝 SAP NetWeaver ASCS <b>nws ascs</b>， <b>10.0.0.10</b>和 hello 執行個體號碼，例如用於 hello 負載平衡器的 hello 探查<b>00</b>。</span><span class="sxs-lookup"><span data-stu-id="7ad26-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="7ad26-363">您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。</span><span class="sxs-lookup"><span data-stu-id="7ad26-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="7ad26-364">**[1]**建立虛擬 IP 資源和 hello 內部負載平衡器的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="7ad26-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="7ad26-365">請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="7ad26-366">它並不重要上執行哪些節點 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="7ad26-367">**[2]** 安裝 SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="7ad26-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="7ad26-368">為根 hello 使用 toohello 的 hello 負載平衡器前端組態 hello 端的 IP 位址，例如對應虛擬主機名稱的第二個節點上安裝 SAP NetWeaver 端<b>nws 端</b>， <b>10.0.0.11</b>hello，例如用於 hello 探查的 hello 負載平衡器的執行個體號碼和<b>02</b>。</span><span class="sxs-lookup"><span data-stu-id="7ad26-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="7ad26-369">您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。</span><span class="sxs-lookup"><span data-stu-id="7ad26-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="7ad26-370">請使用 SWPM SP 20 PL 05 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="7ad26-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="7ad26-371">較低版本未正確設定 hello 權限和 hello 安裝將會失敗。</span><span class="sxs-lookup"><span data-stu-id="7ad26-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="7ad26-372">**[1]**調整 hello ASCS/SCS 和端執行個體的設定檔</span><span class="sxs-lookup"><span data-stu-id="7ad26-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="7ad26-373">ASCS/SCS 設定檔</span><span class="sxs-lookup"><span data-stu-id="7ad26-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="7ad26-374">ERS 設定檔</span><span class="sxs-lookup"><span data-stu-id="7ad26-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="7ad26-375">**[A]** 設定保持運作</span><span class="sxs-lookup"><span data-stu-id="7ad26-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="7ad26-376">透過軟體負載平衡器路由傳送 hello hello ASCS/SCS hello SAP NetWeaver 應用程式伺服器之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="7ad26-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="7ad26-377">hello 負載平衡器會中斷非作用中連線之後可設定的逾時。</span><span class="sxs-lookup"><span data-stu-id="7ad26-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="7ad26-378">tooprevent 這需要 tooset hello SAP NetWeaver ASCS/SCS 設定檔中的參數，並變更 hello Linux 系統設定。</span><span class="sxs-lookup"><span data-stu-id="7ad26-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="7ad26-379">如需詳細資訊，請閱讀 [SAP Note 1410736][1410736]。</span><span class="sxs-lookup"><span data-stu-id="7ad26-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="7ad26-380">hello ASCS/SCS 設定檔參數時/encni/set_so_keepalive 已經 hello 最後一個步驟中加入。</span><span class="sxs-lookup"><span data-stu-id="7ad26-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="7ad26-381">**[A]** Hello 安裝後設定 hello SAP 使用者</span><span class="sxs-lookup"><span data-stu-id="7ad26-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="7ad26-382">**[1]**新增 hello ASCS 和 SAP 端服務 toohello sapservice 檔案</span><span class="sxs-lookup"><span data-stu-id="7ad26-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="7ad26-383">加入 hello ASCS 服務項目 toohello 第二個節點和複製 hello 端服務項目 toohello 第一個節點。</span><span class="sxs-lookup"><span data-stu-id="7ad26-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="7ad26-384">**[1]**建立 hello SAP 叢集資源</span><span class="sxs-lookup"><span data-stu-id="7ad26-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="7ad26-385">請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="7ad26-386">它並不重要上執行哪些節點 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="7ad26-387">建立 STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-387">Create STONITH device</span></span>

<span data-ttu-id="7ad26-388">hello STONITH 裝置會使用針對 Microsoft Azure 服務主體 tooauthorize。</span><span class="sxs-lookup"><span data-stu-id="7ad26-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="7ad26-389">請遵循這些步驟 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="7ad26-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="7ad26-390">跳過<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="7ad26-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="7ad26-391">開啟 hello Azure Active Directory 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="7ad26-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="7ad26-392">請移 tooProperties 並寫下 hello 目錄識別碼。這是 hello**租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="7ad26-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="7ad26-393">按一下 [應用程式註冊]</span><span class="sxs-lookup"><span data-stu-id="7ad26-393">Click App registrations</span></span>
1. <span data-ttu-id="7ad26-394">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="7ad26-394">Click Add</span></span>
1. <span data-ttu-id="7ad26-395">輸入名稱、選取應用程式類型 [Web 應用程式/API]、輸入登入 URL (例如 http://localhost )，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="7ad26-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="7ad26-396">hello 登入 URL 不是，它可以是任何有效的 URL</span><span class="sxs-lookup"><span data-stu-id="7ad26-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="7ad26-397">選取 hello 新的應用程式，然後按一下 hello 設定 索引標籤中的 索引鍵</span><span class="sxs-lookup"><span data-stu-id="7ad26-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="7ad26-398">輸入新金鑰的說明、選取 [永不過期]，然後按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="7ad26-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="7ad26-399">記下 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7ad26-399">Write down hello Value.</span></span> <span data-ttu-id="7ad26-400">它會當做 hello 使用**密碼**hello 服務主體</span><span class="sxs-lookup"><span data-stu-id="7ad26-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="7ad26-401">請記下 hello 應用程式識別碼。它作為 hello 使用者名稱 (**登入識別碼**hello 步驟中) 的 hello 服務主體</span><span class="sxs-lookup"><span data-stu-id="7ad26-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="7ad26-402">hello 服務主體沒有權限 tooaccess 您的 Azure 資源預設。</span><span class="sxs-lookup"><span data-stu-id="7ad26-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="7ad26-403">您需要 toogive hello 服務主體的權限 toostart 和停止 （取消配置） hello 叢集的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7ad26-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="7ad26-404">移 toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="7ad26-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="7ad26-405">開啟 hello 所有資源刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="7ad26-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="7ad26-406">選取 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7ad26-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="7ad26-407">選取 [存取控制 (IAM)]</span><span class="sxs-lookup"><span data-stu-id="7ad26-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="7ad26-408">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="7ad26-408">Click Add</span></span>
1. <span data-ttu-id="7ad26-409">選取 hello 角色擁有者</span><span class="sxs-lookup"><span data-stu-id="7ad26-409">Select hello role Owner</span></span>
1. <span data-ttu-id="7ad26-410">輸入 hello hello 先前建立的應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="7ad26-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="7ad26-411">Click OK</span><span class="sxs-lookup"><span data-stu-id="7ad26-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="7ad26-412">**[1]**建立 hello STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="7ad26-413">編輯 hello hello 虛擬機器的權限之後，您可以設定 hello STONITH 裝置 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="7ad26-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="7ad26-414">**[1]** STONITH 裝置 hello 使用</span><span class="sxs-lookup"><span data-stu-id="7ad26-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="7ad26-415">啟用 hello STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="7ad26-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="7ad26-416">安裝資料庫</span><span class="sxs-lookup"><span data-stu-id="7ad26-416">Install database</span></span>

<span data-ttu-id="7ad26-417">此範例會安裝並設定 SAP HANA 系統複寫。</span><span class="sxs-lookup"><span data-stu-id="7ad26-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="7ad26-418">SAP HANA hello 相同叢集 hello SAP NetWeaver ASCS/SCS 以及端將會執行。</span><span class="sxs-lookup"><span data-stu-id="7ad26-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="7ad26-419">您也可以將 SAP HANA 安裝在專用叢集上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="7ad26-420">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP HANA 高可用性][sap-hana-ha]。</span><span class="sxs-lookup"><span data-stu-id="7ad26-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="7ad26-421">準備進行 SAP HANA 安裝</span><span class="sxs-lookup"><span data-stu-id="7ad26-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="7ad26-422">我們通常建議針對儲存資料和記錄檔的磁碟區使用 LVM。</span><span class="sxs-lookup"><span data-stu-id="7ad26-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="7ad26-423">為了測試用途，您也可以選擇 toostore hello 資料和記錄檔直接在一般的磁碟上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="7ad26-424">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="7ad26-424">**[A]** LVM</span></span>  
   <span data-ttu-id="7ad26-425">以下的 hello 範例假設 hello 虛擬機器有四個資料磁碟連接是應該使用的 toocreate 兩個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7ad26-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="7ad26-426">建立您想 toouse 的所有磁碟的實體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7ad26-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="7ad26-427">建立 hello 資料檔案的磁碟區群組，一個 hello 記錄檔的磁碟區群組，一個用於 hello 共用目錄的 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7ad26-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="7ad26-428">建立 hello 邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="7ad26-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="7ad26-429">建立 hello 掛接目錄，並複製 hello 的所有邏輯磁碟區的 UUID</span><span class="sxs-lookup"><span data-stu-id="7ad26-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="7ad26-430">建立 hello autofs 項目三個邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="7ad26-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="7ad26-431">插入此列 toosudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="7ad26-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="7ad26-432">掛接 hello 新磁碟區</span><span class="sxs-lookup"><span data-stu-id="7ad26-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="7ad26-433">**[A]** 一般磁碟</span><span class="sxs-lookup"><span data-stu-id="7ad26-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="7ad26-434">針對小型或示範系統，您可以將 HANA 資料和記錄檔放在一個磁碟上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="7ad26-435">hello 下列命令 /dev/sdc 上建立資料分割並格式化與 xfs。</span><span class="sxs-lookup"><span data-stu-id="7ad26-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="7ad26-436">插入此列 too/etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="7ad26-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="7ad26-437">建立 hello 目標目錄，並將 hello 磁碟掛接。</span><span class="sxs-lookup"><span data-stu-id="7ad26-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="7ad26-438">安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7ad26-438">Installing SAP HANA</span></span>

<span data-ttu-id="7ad26-439">hello 下列步驟為基礎的 hello 第 4 章[SAP HANA SR-IOV 的效能最佳化的案例指南][ suse-hana-ha-guide] tooinstall SAP HANA 系統複寫。</span><span class="sxs-lookup"><span data-stu-id="7ad26-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="7ad26-440">請仔細閱讀，然後再繼續 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="7ad26-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="7ad26-441">**[A]**從 hello HANA DVD 執行 hdblcm</span><span class="sxs-lookup"><span data-stu-id="7ad26-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="7ad26-442">**[A]** 升級 SAP 主機代理程式</span><span class="sxs-lookup"><span data-stu-id="7ad26-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="7ad26-443">Hello 從下載最新 SAP Host Agent 封存 hello [SAP Softwarecenter] [ sap-swcenter]並執行 hello 下列命令 tooupgrade hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="7ad26-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="7ad26-444">取代 hello 路徑 toohello 封存 toopoint toohello 您下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="7ad26-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="7ad26-445">**[1]** 建立 HANA 複寫 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="7ad26-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="7ad26-446">執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="7ad26-446">Run hello following command.</span></span> <span data-ttu-id="7ad26-447">請確定 tooreplace 粗體字串 （HANA 系統識別碼 HDB 和執行個體編號 03），與 SAP HANA 安裝 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7ad26-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="7ad26-448">**[A]** 建立金鑰儲存區項目 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="7ad26-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="7ad26-449">**[1]** 備份資料庫 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="7ad26-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="7ad26-450">**[1]**切換 toohello HANA sapsid 使用者，並建立 hello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="7ad26-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="7ad26-451">**[2]**切換 toohello HANA sapsid 使用者，並建立 hello 次要站台。</span><span class="sxs-lookup"><span data-stu-id="7ad26-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="7ad26-452">**[1]** 建立 SAP HANA 叢集資源</span><span class="sxs-lookup"><span data-stu-id="7ad26-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="7ad26-453">首先，建立 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ad26-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="7ad26-454">接下來，建立 hello HANA 資源</span><span class="sxs-lookup"><span data-stu-id="7ad26-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="7ad26-455">請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="7ad26-456">它並不重要上執行哪些節點 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7ad26-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="7ad26-457">**[1]**安裝 hello SAP NetWeaver 資料庫執行個體</span><span class="sxs-lookup"><span data-stu-id="7ad26-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="7ad26-458">安裝 hello SAP NetWeaver 資料庫執行個體做為使用虛擬的主機名稱，例如對應 hello 負載平衡器前端組態 hello 資料庫 toohello IP 位址的根目錄<b>nws db</b>和<b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="7ad26-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="7ad26-459">您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。</span><span class="sxs-lookup"><span data-stu-id="7ad26-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="7ad26-460">SAP NetWeaver 應用程式伺服器安裝</span><span class="sxs-lookup"><span data-stu-id="7ad26-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="7ad26-461">請遵循這些步驟 tooinstall SAP 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="7ad26-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="7ad26-462">hello 以下步驟假設您安裝 hello hello ASCS/SCS 從不同的伺服器上的應用程式伺服器和 HANA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7ad26-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="7ad26-463">否則某些 hello 執行下列步驟 （例如設定主機名稱解析） 不需要。</span><span class="sxs-lookup"><span data-stu-id="7ad26-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="7ad26-464">設定主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="7ad26-464">Setup host name resolution</span></span>    
   <span data-ttu-id="7ad26-465">您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。</span><span class="sxs-lookup"><span data-stu-id="7ad26-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="7ad26-466">這個範例會示範如何 toouse hello /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ad26-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="7ad26-467">取代 hello IP 位址和下列命令的 hello hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="7ad26-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="7ad26-468">插入 hello 下列各行太/等/主機。</span><span class="sxs-lookup"><span data-stu-id="7ad26-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="7ad26-469">變更您的環境的 hello IP 位址和主機名稱 toomatch</span><span class="sxs-lookup"><span data-stu-id="7ad26-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="7ad26-470">建立 hello sapmnt 目錄</span><span class="sxs-lookup"><span data-stu-id="7ad26-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="7ad26-471">設定 autofs</span><span class="sxs-lookup"><span data-stu-id="7ad26-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="7ad26-472">使用下列命令建立新檔案</span><span class="sxs-lookup"><span data-stu-id="7ad26-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="7ad26-473">重新啟動 autofs toomount hello 新的共用</span><span class="sxs-lookup"><span data-stu-id="7ad26-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="7ad26-474">設定分頁檔</span><span class="sxs-lookup"><span data-stu-id="7ad26-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="7ad26-475">重新啟動 hello 代理程式 tooactivate hello 變更</span><span class="sxs-lookup"><span data-stu-id="7ad26-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="7ad26-476">安裝 SAP NetWeaver 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="7ad26-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="7ad26-477">安裝主要或其他的 SAP NetWeaver 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="7ad26-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="7ad26-478">您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。</span><span class="sxs-lookup"><span data-stu-id="7ad26-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="7ad26-479">更新 SAP HANA 安全存放區</span><span class="sxs-lookup"><span data-stu-id="7ad26-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="7ad26-480">更新 hello SAP HANA 安全儲存 toopoint toohello 虛擬名稱 hello SAP HANA 系統複寫設定。</span><span class="sxs-lookup"><span data-stu-id="7ad26-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="7ad26-481">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ad26-481">Next steps</span></span>
* <span data-ttu-id="7ad26-482">[適用於 SAP 的 Azure 虛擬機器規劃和實作][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7ad26-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="7ad26-483">[適用於 SAP 的 Azure 虛擬機器部署][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7ad26-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="7ad26-484">[適用於 SAP 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7ad26-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="7ad26-485">toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad26-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="7ad26-486">toolearn tooestablish 高可用性和災害復原的 SAP HANA 規劃 Azure Vm 上的看到[SAP HANA 的高可用性 Azure 虛擬機器 (Vm) 上][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="7ad26-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
