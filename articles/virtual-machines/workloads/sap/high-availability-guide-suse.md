---
title: "SAP NetWeaver 在適用於 SAP 應用程式之 SUSE Linux Enterprise Server 上的 Azure 虛擬機器高可用性 | Microsoft Docs"
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
ms.openlocfilehash: 16e09797926f29bc18cb05671c986c74f9c2d4f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="86d01-103">SAP NetWeaver 在適用於 SAP 應用程式之 SUSE Linux Enterprise Server 上的 Azure VM 高可用性</span><span class="sxs-lookup"><span data-stu-id="86d01-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="86d01-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="86d01-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="86d01-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="86d01-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="86d01-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="86d01-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="86d01-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="86d01-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="86d01-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="86d01-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="86d01-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="86d01-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="86d01-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="86d01-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="86d01-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="86d01-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="86d01-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="86d01-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="86d01-113">本文說明如何部署虛擬機器、設定虛擬機器、安裝叢集架構，以及安裝高可用性的 SAP NetWeaver 7.50 系統。</span><span class="sxs-lookup"><span data-stu-id="86d01-113">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="86d01-114">在範例組態中，安裝命令等。會使用 ASCS 執行個體號碼 00、ERS 執行個體號碼 02 和 SAP 系統識別碼 NWS。</span><span class="sxs-lookup"><span data-stu-id="86d01-114">In the example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="86d01-115">範例中資源 (例如虛擬機器、虛擬網路) 的名稱會假設您已使用[交集範本][template-converged]與 SAP 系統識別碼 NWS 來建立資源。</span><span class="sxs-lookup"><span data-stu-id="86d01-115">The names of the resources (for example virtual machines, virtual networks) in the example assume that you have used the [converged template][template-converged] with SAP system ID NWS to create the resources.</span></span>

<span data-ttu-id="86d01-116">請先閱讀下列 SAP Note 和文件</span><span class="sxs-lookup"><span data-stu-id="86d01-116">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="86d01-117">SAP Note [1928533]，其中包含：</span><span class="sxs-lookup"><span data-stu-id="86d01-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="86d01-118">SAP 軟體部署支援的 Azure VM 大小清單</span><span class="sxs-lookup"><span data-stu-id="86d01-118">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="86d01-119">Azure VM 大小的重要容量資訊</span><span class="sxs-lookup"><span data-stu-id="86d01-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="86d01-120">支援的 SAP 軟體，以及作業系統 (OS) 與資料庫組合</span><span class="sxs-lookup"><span data-stu-id="86d01-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="86d01-121">Microsoft Azure 上 Windows 和 Linux 所需的 SAP 核心版本</span><span class="sxs-lookup"><span data-stu-id="86d01-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="86d01-122">SAP Note [2015553] 列出 Azure 中 SAP 支援的 SAP 軟體部署先決條件。</span><span class="sxs-lookup"><span data-stu-id="86d01-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="86d01-123">SAP Note [2205917] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的建議 OS 設定</span><span class="sxs-lookup"><span data-stu-id="86d01-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="86d01-124">SAP Note [1944799] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的 SAP HANA 指導方針</span><span class="sxs-lookup"><span data-stu-id="86d01-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="86d01-125">SAP Note [2178632] 包含在 Azure 中針對 SAP 回報的所有監視計量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="86d01-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="86d01-126">SAP Note [2191498] 包含 Azure 中 Linux 所需的 SAP Host Agent 版本。</span><span class="sxs-lookup"><span data-stu-id="86d01-126">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="86d01-127">SAP Note [2243692] 包含 Azure 中 Linux 上的 SAP 授權相關資訊。</span><span class="sxs-lookup"><span data-stu-id="86d01-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="86d01-128">SAP Note [1984787] 包含 SUSE LINUX Enterprise Server 12 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="86d01-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="86d01-129">SAP Note [1999351] 包含 Azure Enhanced Monitoring Extension for SAP 的其他疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="86d01-129">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="86d01-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) 包含 Linux 所需的所有 SAP Note。</span><span class="sxs-lookup"><span data-stu-id="86d01-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="86d01-131">[適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="86d01-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="86d01-132">[適用於 SAP on Linux 的 Azure 虛擬機器部署 (本文)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="86d01-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="86d01-133">[適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="86d01-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="86d01-134">[SAP HANA SR 效能最佳化案例 (英文)][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="86d01-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="86d01-135">此指南包含設定內部部署 SAP HANA 系統複寫的所有必要資訊。</span><span class="sxs-lookup"><span data-stu-id="86d01-135">The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="86d01-136">請使用此指南做為基礎。</span><span class="sxs-lookup"><span data-stu-id="86d01-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="86d01-137">[高可用性的 NFS 儲存體搭配 DRBD 與 Pacemaker][suse-drbd-guide] 此指南包含設定高可用性的 NFS 伺服器所需的所有必要資訊。</span><span class="sxs-lookup"><span data-stu-id="86d01-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] The guide contains all required information to set up a highly available NFS server.</span></span> <span data-ttu-id="86d01-138">請使用此指南做為基礎。</span><span class="sxs-lookup"><span data-stu-id="86d01-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="86d01-139">概觀</span><span class="sxs-lookup"><span data-stu-id="86d01-139">Overview</span></span>

<span data-ttu-id="86d01-140">為了實現高可用性，SAP NetWeaver 需要使用 NFS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="86d01-140">To achieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="86d01-141">NFS 伺服器會設定於不同叢集中，並可供多個 SAP 系統使用。</span><span class="sxs-lookup"><span data-stu-id="86d01-141">The NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![SAP NetWeaver 高可用性概觀](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="86d01-143">NFS 伺服器、SAP NetWeaver ASCS、SAP NetWeaver SCS、SAP NetWeaver ERS 和 SAP HANA 資料庫會使用虛擬主機名稱和虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="86d01-143">The NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and the SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="86d01-144">在 Azure 上必須有負載平衡器才能使用虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="86d01-144">On Azure, a load balancer is required to use a virtual IP address.</span></span> <span data-ttu-id="86d01-145">下列清單顯示負載平衡器的組態。</span><span class="sxs-lookup"><span data-stu-id="86d01-145">The following list shows the configuration of the load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="86d01-146">NFS 伺服器</span><span class="sxs-lookup"><span data-stu-id="86d01-146">NFS Server</span></span>
* <span data-ttu-id="86d01-147">前端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-147">Frontend configuration</span></span>
  * <span data-ttu-id="86d01-148">IP 位址 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="86d01-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="86d01-149">後端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-149">Backend configuration</span></span>
  * <span data-ttu-id="86d01-150">連線到應該屬於 NFS 叢集一部分之所有虛擬機器的主要網路介面</span><span class="sxs-lookup"><span data-stu-id="86d01-150">Connected to primary network interfaces of all virtual machines that should be part of the NFS cluster</span></span>
* <span data-ttu-id="86d01-151">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="86d01-151">Probe Port</span></span>
  * <span data-ttu-id="86d01-152">連接埠 61000</span><span class="sxs-lookup"><span data-stu-id="86d01-152">Port 61000</span></span>
* <span data-ttu-id="86d01-153">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="86d01-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="86d01-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-154">2049 TCP</span></span> 
  * <span data-ttu-id="86d01-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="86d01-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="86d01-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="86d01-156">(A)SCS</span></span>
* <span data-ttu-id="86d01-157">前端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-157">Frontend configuration</span></span>
  * <span data-ttu-id="86d01-158">IP 位址 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="86d01-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="86d01-159">後端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-159">Backend configuration</span></span>
  * <span data-ttu-id="86d01-160">連線到應該屬於 (A)SCS/ERS 叢集一部分之所有虛擬機器的主要網路介面</span><span class="sxs-lookup"><span data-stu-id="86d01-160">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="86d01-161">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="86d01-161">Probe Port</span></span>
  * <span data-ttu-id="86d01-162">連接埠 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="86d01-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="86d01-163">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="86d01-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="86d01-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="86d01-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="86d01-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="86d01-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="86d01-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="86d01-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="86d01-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="86d01-171">ERS</span><span class="sxs-lookup"><span data-stu-id="86d01-171">ERS</span></span>
* <span data-ttu-id="86d01-172">前端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-172">Frontend configuration</span></span>
  * <span data-ttu-id="86d01-173">IP 位址 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="86d01-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="86d01-174">後端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-174">Backend configuration</span></span>
  * <span data-ttu-id="86d01-175">連線到應該屬於 (A)SCS/ERS 叢集一部分之所有虛擬機器的主要網路介面</span><span class="sxs-lookup"><span data-stu-id="86d01-175">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="86d01-176">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="86d01-176">Probe Port</span></span>
  * <span data-ttu-id="86d01-177">連接埠 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="86d01-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="86d01-178">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="86d01-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="86d01-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="86d01-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="86d01-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="86d01-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="86d01-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="86d01-183">SAP HANA</span></span>
* <span data-ttu-id="86d01-184">前端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-184">Frontend configuration</span></span>
  * <span data-ttu-id="86d01-185">IP 位址 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="86d01-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="86d01-186">後端組態</span><span class="sxs-lookup"><span data-stu-id="86d01-186">Backend configuration</span></span>
  * <span data-ttu-id="86d01-187">連線到應該屬於 HANA 叢集一部分之所有虛擬機器的主要網路介面</span><span class="sxs-lookup"><span data-stu-id="86d01-187">Connected to primary network interfaces of all virtual machines that should be part of the HANA cluster</span></span>
* <span data-ttu-id="86d01-188">探查連接埠</span><span class="sxs-lookup"><span data-stu-id="86d01-188">Probe Port</span></span>
  * <span data-ttu-id="86d01-189">連接埠 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="86d01-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="86d01-190">負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="86d01-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="86d01-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="86d01-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="86d01-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="86d01-193">設定高可用性的 NFS 伺服器</span><span class="sxs-lookup"><span data-stu-id="86d01-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="86d01-194">部署 Linux</span><span class="sxs-lookup"><span data-stu-id="86d01-194">Deploying Linux</span></span>

<span data-ttu-id="86d01-195">Azure Marketplace 包含 SUSE Linux Enterprise Server for SAP Applications 12 的映像，讓您可用來部署新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="86d01-195">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span>
<span data-ttu-id="86d01-196">您可以使用 Github 上的其中一個快速入門範本來部署所有必要資源。</span><span class="sxs-lookup"><span data-stu-id="86d01-196">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="86d01-197">範本會部署虛擬機器、負載平衡器、可用性設定組等。請遵循下列步驟來部署範本：</span><span class="sxs-lookup"><span data-stu-id="86d01-197">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="86d01-198">在 Azure 入口網站中開啟 [SAP 檔案伺服器範本][template-file-server]</span><span class="sxs-lookup"><span data-stu-id="86d01-198">Open the [SAP file server template][template-file-server] in the Azure portal</span></span>   
1. <span data-ttu-id="86d01-199">輸入下列參數</span><span class="sxs-lookup"><span data-stu-id="86d01-199">Enter the following parameters</span></span>
   1. <span data-ttu-id="86d01-200">資源前置詞</span><span class="sxs-lookup"><span data-stu-id="86d01-200">Resource Prefix</span></span>  
      <span data-ttu-id="86d01-201">輸入您想要使用的前置詞。</span><span class="sxs-lookup"><span data-stu-id="86d01-201">Enter the prefix you want to use.</span></span> <span data-ttu-id="86d01-202">該值會作為所部署之資源的前置詞。</span><span class="sxs-lookup"><span data-stu-id="86d01-202">The value is used as a prefix for the resources that are deployed.</span></span>
   2. <span data-ttu-id="86d01-203">OS 類型</span><span class="sxs-lookup"><span data-stu-id="86d01-203">Os Type</span></span>  
      <span data-ttu-id="86d01-204">選取一個 Linux 發行版本。</span><span class="sxs-lookup"><span data-stu-id="86d01-204">Select one of the Linux distributions.</span></span> <span data-ttu-id="86d01-205">在此範例中，請選取 SLES 12</span><span class="sxs-lookup"><span data-stu-id="86d01-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="86d01-206">管理員使用者名稱和管理員密碼</span><span class="sxs-lookup"><span data-stu-id="86d01-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="86d01-207">建立可用來登入電腦的新使用者。</span><span class="sxs-lookup"><span data-stu-id="86d01-207">A new user is created that can be used to log on to the machine.</span></span>
   4. <span data-ttu-id="86d01-208">子網路識別碼</span><span class="sxs-lookup"><span data-stu-id="86d01-208">Subnet Id</span></span>  
      <span data-ttu-id="86d01-209">虛擬機器應該連接的子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="86d01-209">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="86d01-210">如果您想要建立新的虛擬網路，請讓此參數保持空白，或者，您也可以選取將虛擬機器連線到內部部署網路之 VPN 或快速路由虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="86d01-210">Leave empty if you want to create a new virtual network or select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="86d01-211">識別碼通常如下所示：/subscriptions/**&lt;訂用帳戶識別碼&gt;**/resourceGroups/**&lt;資源群組名稱&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;虛擬網路名稱&gt;**/subnets/**&lt;子網路名稱&gt;**</span><span class="sxs-lookup"><span data-stu-id="86d01-211">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="86d01-212">安裝</span><span class="sxs-lookup"><span data-stu-id="86d01-212">Installation</span></span>

<span data-ttu-id="86d01-213">下列項目會加上下列其中一個前置詞：**[A]** - 適用於所有節點、**[1]** - 僅適用於節點 1 或 **[2]** - 僅適用於節點 2。</span><span class="sxs-lookup"><span data-stu-id="86d01-213">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="86d01-214">**[A]** 更新 SLES</span><span class="sxs-lookup"><span data-stu-id="86d01-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="86d01-215">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="86d01-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="86d01-216">**[2]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="86d01-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="86d01-217">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="86d01-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="86d01-218">**[A]** 安裝 HA 擴充功能</span><span class="sxs-lookup"><span data-stu-id="86d01-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="86d01-219">**[A]** 設定主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="86d01-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="86d01-220">您可以使用 DNS 伺服器，或修改所有節點上的 /etc/hosts。</span><span class="sxs-lookup"><span data-stu-id="86d01-220">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="86d01-221">這個範例示範如何使用 /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="86d01-221">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="86d01-222">取代下列命令中的 IP 位址和主機名稱</span><span class="sxs-lookup"><span data-stu-id="86d01-222">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="86d01-223">將下列幾行插入至 /etc/hosts。</span><span class="sxs-lookup"><span data-stu-id="86d01-223">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="86d01-224">變更 IP 位址和主機名稱以符合您的環境</span><span class="sxs-lookup"><span data-stu-id="86d01-224">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="86d01-225">**[1]** 安裝叢集</span><span class="sxs-lookup"><span data-stu-id="86d01-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="86d01-226">**[2]** 將節點新增至叢集</span><span class="sxs-lookup"><span data-stu-id="86d01-226">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="86d01-227">**[A]** 將 hacluster 密碼變更為同一個密碼</span><span class="sxs-lookup"><span data-stu-id="86d01-227">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="86d01-228">**[A]** 設定 corosync 以使用其他傳輸，並新增節點清單。</span><span class="sxs-lookup"><span data-stu-id="86d01-228">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="86d01-229">否則叢集將無法運作。</span><span class="sxs-lookup"><span data-stu-id="86d01-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="86d01-230">將下列粗體內容新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="86d01-230">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="86d01-231">然後重新啟動 corosync 服務</span><span class="sxs-lookup"><span data-stu-id="86d01-231">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="86d01-232">**[A]** 安裝 drbd 元件</span><span class="sxs-lookup"><span data-stu-id="86d01-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="86d01-233">**[A]** 建立 drbd 裝置的分割區</span><span class="sxs-lookup"><span data-stu-id="86d01-233">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="86d01-234">**[A]** 建立 LVM 組態</span><span class="sxs-lookup"><span data-stu-id="86d01-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="86d01-235">**[A]** 建立 NFS drbd 裝置</span><span class="sxs-lookup"><span data-stu-id="86d01-235">**[A]** Create the NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="86d01-236">插入新 drbd 裝置的組態並結束</span><span class="sxs-lookup"><span data-stu-id="86d01-236">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="86d01-237">建立 drbd 裝置並加以啟動</span><span class="sxs-lookup"><span data-stu-id="86d01-237">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="86d01-238">**[1]** 略過首次同步處理</span><span class="sxs-lookup"><span data-stu-id="86d01-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="86d01-239">**[1]** 設定主要節點</span><span class="sxs-lookup"><span data-stu-id="86d01-239">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="86d01-240">**[1]** 等候新的 drbd 裝置完成同步處理</span><span class="sxs-lookup"><span data-stu-id="86d01-240">**[1]** Wait until the new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="86d01-241">**[1]** 在 drbd 裝置上建立檔案系統</span><span class="sxs-lookup"><span data-stu-id="86d01-241">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="86d01-242">設定叢集架構</span><span class="sxs-lookup"><span data-stu-id="86d01-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="86d01-243">**[1]** 變更預設設定</span><span class="sxs-lookup"><span data-stu-id="86d01-243">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="86d01-244">**[1]** 將 NFS drbd 裝置新增至叢集組態</span><span class="sxs-lookup"><span data-stu-id="86d01-244">**[1]** Add the NFS drbd device to the cluster configuration</span></span>

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

1. <span data-ttu-id="86d01-245">**[1]** 建立 NFS 伺服器</span><span class="sxs-lookup"><span data-stu-id="86d01-245">**[1]** Create the NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="86d01-246">**[1]** 建立 NFS 檔案系統資源</span><span class="sxs-lookup"><span data-stu-id="86d01-246">**[1]** Create the NFS File System resources</span></span>

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

1. <span data-ttu-id="86d01-247">**[1]** 建立 NFS 匯出</span><span class="sxs-lookup"><span data-stu-id="86d01-247">**[1]** Create the NFS exports</span></span>

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

1. <span data-ttu-id="86d01-248">**[1]** 為內部負載平衡器建立虛擬 IP 資源和健康情況探查</span><span class="sxs-lookup"><span data-stu-id="86d01-248">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="86d01-249">建立 STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="86d01-249">Create STONITH device</span></span>

<span data-ttu-id="86d01-250">STONITH 裝置會使用服務主體來對 Microsoft Azure 授權。</span><span class="sxs-lookup"><span data-stu-id="86d01-250">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="86d01-251">請遵循下列步驟來建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="86d01-251">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="86d01-252">移至 <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="86d01-252">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="86d01-253">開啟 [Azure Active Directory] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="86d01-253">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="86d01-254">移至 [屬性]，並記下目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="86d01-254">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="86d01-255">這是**租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="86d01-255">This is the **tenant id**.</span></span>
1. <span data-ttu-id="86d01-256">按一下 [應用程式註冊]</span><span class="sxs-lookup"><span data-stu-id="86d01-256">Click App registrations</span></span>
1. <span data-ttu-id="86d01-257">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="86d01-257">Click Add</span></span>
1. <span data-ttu-id="86d01-258">輸入名稱、選取應用程式類型 [Web 應用程式/API]、輸入登入 URL (例如 http://localhost )，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="86d01-258">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="86d01-259">登入 URL 並未使用，而且可以是任何有效的 URL</span><span class="sxs-lookup"><span data-stu-id="86d01-259">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="86d01-260">選取新的應用程式，然後按一下 [設定] 索引標籤中的金鑰</span><span class="sxs-lookup"><span data-stu-id="86d01-260">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="86d01-261">輸入新金鑰的說明、選取 [永不過期]，然後按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="86d01-261">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="86d01-262">記下值。</span><span class="sxs-lookup"><span data-stu-id="86d01-262">Write down the Value.</span></span> <span data-ttu-id="86d01-263">此值會用來做為服務主體的**密碼**</span><span class="sxs-lookup"><span data-stu-id="86d01-263">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="86d01-264">記下應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="86d01-264">Write down the Application Id.</span></span> <span data-ttu-id="86d01-265">此識別碼會用來做為服務主體的使用者名稱 (以下步驟中的 **login id**)</span><span class="sxs-lookup"><span data-stu-id="86d01-265">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="86d01-266">服務主體預設沒有存取您 Azure 資源的權限。</span><span class="sxs-lookup"><span data-stu-id="86d01-266">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="86d01-267">您需要為服務主體提供權限來啟動和停止 (解除配置) 叢集的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="86d01-267">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="86d01-268">移至 https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="86d01-268">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="86d01-269">開啟 [所有資源] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="86d01-269">Open the All resources blade</span></span>
1. <span data-ttu-id="86d01-270">選取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="86d01-270">Select the virtual machine</span></span>
1. <span data-ttu-id="86d01-271">選取 [存取控制 (IAM)]</span><span class="sxs-lookup"><span data-stu-id="86d01-271">Click Access control (IAM)</span></span>
1. <span data-ttu-id="86d01-272">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="86d01-272">Click Add</span></span>
1. <span data-ttu-id="86d01-273">選取 [擁有者] 角色</span><span class="sxs-lookup"><span data-stu-id="86d01-273">Select the role Owner</span></span>
1. <span data-ttu-id="86d01-274">輸入您先前建立的應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="86d01-274">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="86d01-275">Click OK</span><span class="sxs-lookup"><span data-stu-id="86d01-275">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="86d01-276">**[1]** 建立 STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="86d01-276">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="86d01-277">當您編輯虛擬機器的權限之後，就可以在叢集中設定 STONITH 裝置。</span><span class="sxs-lookup"><span data-stu-id="86d01-277">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="86d01-278">**[1]** 啟用 STONITH 裝置的使用</span><span class="sxs-lookup"><span data-stu-id="86d01-278">**[1]** Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="86d01-279">設定 (A)SCS</span><span class="sxs-lookup"><span data-stu-id="86d01-279">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="86d01-280">部署 Linux</span><span class="sxs-lookup"><span data-stu-id="86d01-280">Deploying Linux</span></span>

<span data-ttu-id="86d01-281">Azure Marketplace 包含 SUSE Linux Enterprise Server for SAP Applications 12 的映像，讓您可用來部署新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="86d01-281">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span> <span data-ttu-id="86d01-282">Marketplace 映像包含 SAP NetWeaver 的資源代理程式。</span><span class="sxs-lookup"><span data-stu-id="86d01-282">The marketplace image contains the resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="86d01-283">您可以使用 Github 上的其中一個快速入門範本來部署所有必要資源。</span><span class="sxs-lookup"><span data-stu-id="86d01-283">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="86d01-284">範本會部署虛擬機器、負載平衡器、可用性設定組等。請遵循下列步驟來部署範本：</span><span class="sxs-lookup"><span data-stu-id="86d01-284">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="86d01-285">在 Azure 入口網站上開啟 [ASCS/SCS 多重 SID範本][template-multisid-xscs]或[交集範本][template-converged]。ASCS/SCS 範本只會建立 SAP NetWeaver ASCS/SCS 和 ERS (僅限 Linux) 執行個體的負載平衡規則，而交集範本還會建立資料庫 (例如 Microsoft SQL Server 或 SAP HANA) 的負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="86d01-285">Open the [ASCS/SCS Multi SID template][template-multisid-xscs] or the [converged template][template-converged] on the Azure portal The ASCS/SCS template only creates the load-balancing rules for the SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas the converged template also creates the load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="86d01-286">如果您打算安裝 SAP NetWeaver 架構的系統，而且也想要在同一部電腦上安裝資料庫，請使用[交集範本][template-converged]。</span><span class="sxs-lookup"><span data-stu-id="86d01-286">If you plan to install an SAP NetWeaver based system and you also want to install the database on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="86d01-287">輸入下列參數</span><span class="sxs-lookup"><span data-stu-id="86d01-287">Enter the following parameters</span></span>
   1. <span data-ttu-id="86d01-288">資源前置詞 (僅限 ASCS/SCS 多重 SID 範本)</span><span class="sxs-lookup"><span data-stu-id="86d01-288">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="86d01-289">輸入您想要使用的前置詞。</span><span class="sxs-lookup"><span data-stu-id="86d01-289">Enter the prefix you want to use.</span></span> <span data-ttu-id="86d01-290">該值會作為所部署之資源的前置詞。</span><span class="sxs-lookup"><span data-stu-id="86d01-290">The value is used as a prefix for the resources that are deployed.</span></span>
   3. <span data-ttu-id="86d01-291">Sap 系統識別碼 (僅限交集範本)</span><span class="sxs-lookup"><span data-stu-id="86d01-291">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="86d01-292">輸入您想要安裝之 SAP 系統的 SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="86d01-292">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="86d01-293">該識別碼會作為所部署之資源的前置詞。</span><span class="sxs-lookup"><span data-stu-id="86d01-293">The Id is used as a prefix for the resources that are deployed.</span></span>
   4. <span data-ttu-id="86d01-294">堆疊類型</span><span class="sxs-lookup"><span data-stu-id="86d01-294">Stack Type</span></span>  
      <span data-ttu-id="86d01-295">選取 SAP NetWeaver 堆疊類型</span><span class="sxs-lookup"><span data-stu-id="86d01-295">Select the SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="86d01-296">OS 類型</span><span class="sxs-lookup"><span data-stu-id="86d01-296">Os Type</span></span>  
      <span data-ttu-id="86d01-297">選取一個 Linux 發行版本。</span><span class="sxs-lookup"><span data-stu-id="86d01-297">Select one of the Linux distributions.</span></span> <span data-ttu-id="86d01-298">在此範例中，請選取 SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="86d01-298">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="86d01-299">DB 類型</span><span class="sxs-lookup"><span data-stu-id="86d01-299">Db Type</span></span>  
      <span data-ttu-id="86d01-300">選取 HANA</span><span class="sxs-lookup"><span data-stu-id="86d01-300">Select HANA</span></span>
   7. <span data-ttu-id="86d01-301">SAP 系統大小</span><span class="sxs-lookup"><span data-stu-id="86d01-301">Sap System Size</span></span>  
      <span data-ttu-id="86d01-302">新系統會提供的 SAP 數量。</span><span class="sxs-lookup"><span data-stu-id="86d01-302">The amount of SAPS the new system provides.</span></span> <span data-ttu-id="86d01-303">如果您不確定系統需要多少 SAP，請詢問您的 SAP 技術合作夥伴或系統整合者</span><span class="sxs-lookup"><span data-stu-id="86d01-303">If you are not sure how many SAPS the system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="86d01-304">系統可用性</span><span class="sxs-lookup"><span data-stu-id="86d01-304">System Availability</span></span>  
      <span data-ttu-id="86d01-305">選取 HA</span><span class="sxs-lookup"><span data-stu-id="86d01-305">Select HA</span></span>
   9. <span data-ttu-id="86d01-306">管理員使用者名稱和管理員密碼</span><span class="sxs-lookup"><span data-stu-id="86d01-306">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="86d01-307">建立可用來登入電腦的新使用者。</span><span class="sxs-lookup"><span data-stu-id="86d01-307">A new user is created that can be used to log on to the machine.</span></span>
   10. <span data-ttu-id="86d01-308">子網路識別碼</span><span class="sxs-lookup"><span data-stu-id="86d01-308">Subnet Id</span></span>  
   <span data-ttu-id="86d01-309">虛擬機器應該連接的子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="86d01-309">The ID of the subnet to which the virtual machines should be connected to.</span></span>  <span data-ttu-id="86d01-310">如果您想要建立新的虛擬網路，請讓此參數保持空白，或者，您也可以選取您在部署 NFS 伺服器的過程中使用或建立的同一個子網路。</span><span class="sxs-lookup"><span data-stu-id="86d01-310">Leave empty if you want to create a new virtual network or select the same subnet that you used or created as part of the NFS server deployment.</span></span> <span data-ttu-id="86d01-311">識別碼通常如下所示：/subscriptions/**&lt;訂用帳戶識別碼&gt;**/resourceGroups/**&lt;資源群組名稱&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;虛擬網路名稱&gt;**/subnets/**&lt;子網路名稱&gt;**</span><span class="sxs-lookup"><span data-stu-id="86d01-311">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="86d01-312">安裝</span><span class="sxs-lookup"><span data-stu-id="86d01-312">Installation</span></span>

<span data-ttu-id="86d01-313">下列項目會加上下列其中一個前置詞：**[A]** - 適用於所有節點、**[1]** - 僅適用於節點 1 或 **[2]** - 僅適用於節點 2。</span><span class="sxs-lookup"><span data-stu-id="86d01-313">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="86d01-314">**[A]** 更新 SLES</span><span class="sxs-lookup"><span data-stu-id="86d01-314">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="86d01-315">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="86d01-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="86d01-316">**[2]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="86d01-316">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="86d01-317">**[1]** 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="86d01-317">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="86d01-318">**[A]** 安裝 HA 擴充功能</span><span class="sxs-lookup"><span data-stu-id="86d01-318">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="86d01-319">**[A]** 更新 SAP 資源代理程式</span><span class="sxs-lookup"><span data-stu-id="86d01-319">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="86d01-320">資源代理程式套件必須有修補程式才能使用新的組態，本文會有該修補程式的說明。</span><span class="sxs-lookup"><span data-stu-id="86d01-320">A patch for the resource-agents package is required to use the new configuration, that is described in this article.</span></span> <span data-ttu-id="86d01-321">您可以查看您是否已使用下列命令安裝了修補程式</span><span class="sxs-lookup"><span data-stu-id="86d01-321">You can check, if the patch is already installed with the following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="86d01-322">輸出應該會類似</span><span class="sxs-lookup"><span data-stu-id="86d01-322">The output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="86d01-323">如果 grep 命令找不到 IS_ERS 參數，您必須安裝 [SUSE 下載頁面](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)上所列出的修補程式</span><span class="sxs-lookup"><span data-stu-id="86d01-323">If the grep command does not find the IS_ERS parameter, you need to install the patch listed on [the SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="86d01-324">**[A]** 設定主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="86d01-324">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="86d01-325">您可以使用 DNS 伺服器，或修改所有節點上的 /etc/hosts。</span><span class="sxs-lookup"><span data-stu-id="86d01-325">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="86d01-326">這個範例示範如何使用 /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="86d01-326">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="86d01-327">取代下列命令中的 IP 位址和主機名稱</span><span class="sxs-lookup"><span data-stu-id="86d01-327">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="86d01-328">將下列幾行插入至 /etc/hosts。</span><span class="sxs-lookup"><span data-stu-id="86d01-328">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="86d01-329">變更 IP 位址和主機名稱以符合您的環境</span><span class="sxs-lookup"><span data-stu-id="86d01-329">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="86d01-330">**[1]** 安裝叢集</span><span class="sxs-lookup"><span data-stu-id="86d01-330">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="86d01-331">**[2]** 將節點新增至叢集</span><span class="sxs-lookup"><span data-stu-id="86d01-331">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="86d01-332">**[A]** 將 hacluster 密碼變更為同一個密碼</span><span class="sxs-lookup"><span data-stu-id="86d01-332">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="86d01-333">**[A]** 設定 corosync 以使用其他傳輸，並新增節點清單。</span><span class="sxs-lookup"><span data-stu-id="86d01-333">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="86d01-334">否則叢集將無法運作。</span><span class="sxs-lookup"><span data-stu-id="86d01-334">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="86d01-335">將下列粗體內容新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="86d01-335">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="86d01-336">然後重新啟動 corosync 服務</span><span class="sxs-lookup"><span data-stu-id="86d01-336">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="86d01-337">**[A]** 安裝 drbd 元件</span><span class="sxs-lookup"><span data-stu-id="86d01-337">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="86d01-338">**[A]** 建立 drbd 裝置的分割區</span><span class="sxs-lookup"><span data-stu-id="86d01-338">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="86d01-339">**[A]** 建立 LVM 組態</span><span class="sxs-lookup"><span data-stu-id="86d01-339">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="86d01-340">**[A]** 建立 SCS drbd 裝置</span><span class="sxs-lookup"><span data-stu-id="86d01-340">**[A]** Create the SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="86d01-341">插入新 drbd 裝置的組態並結束</span><span class="sxs-lookup"><span data-stu-id="86d01-341">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="86d01-342">建立 drbd 裝置並加以啟動</span><span class="sxs-lookup"><span data-stu-id="86d01-342">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="86d01-343">**[A]** 建立 ERS drbd 裝置</span><span class="sxs-lookup"><span data-stu-id="86d01-343">**[A]** Create the ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="86d01-344">插入新 drbd 裝置的組態並結束</span><span class="sxs-lookup"><span data-stu-id="86d01-344">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="86d01-345">建立 drbd 裝置並加以啟動</span><span class="sxs-lookup"><span data-stu-id="86d01-345">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="86d01-346">**[1]** 略過首次同步處理</span><span class="sxs-lookup"><span data-stu-id="86d01-346">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="86d01-347">**[1]** 設定主要節點</span><span class="sxs-lookup"><span data-stu-id="86d01-347">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="86d01-348">**[1]** 等候新的 drbd 裝置完成同步處理</span><span class="sxs-lookup"><span data-stu-id="86d01-348">**[1]** Wait until the new drbd devices are synchronized</span></span>

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

1. <span data-ttu-id="86d01-349">**[1]** 在 drbd 裝置上建立檔案系統</span><span class="sxs-lookup"><span data-stu-id="86d01-349">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="86d01-350">設定叢集架構</span><span class="sxs-lookup"><span data-stu-id="86d01-350">Configure Cluster Framework</span></span>

<span data-ttu-id="86d01-351">**[1]** 變更預設設定</span><span class="sxs-lookup"><span data-stu-id="86d01-351">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="86d01-352">準備進行 SAP NetWeaver 安裝</span><span class="sxs-lookup"><span data-stu-id="86d01-352">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="86d01-353">**[A]** 建立共用目錄</span><span class="sxs-lookup"><span data-stu-id="86d01-353">**[A]** Create the shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="86d01-354">**[A]** 設定 autofs</span><span class="sxs-lookup"><span data-stu-id="86d01-354">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="86d01-355">使用下列命令建立檔案</span><span class="sxs-lookup"><span data-stu-id="86d01-355">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="86d01-356">重新啟動 autofs 來裝載新的共用</span><span class="sxs-lookup"><span data-stu-id="86d01-356">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="86d01-357">**[A]** 設定分頁檔</span><span class="sxs-lookup"><span data-stu-id="86d01-357">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="86d01-358">重新啟動代理程式以啟動變更</span><span class="sxs-lookup"><span data-stu-id="86d01-358">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="86d01-359">安裝 SAP NetWeaver ASCS/ERS</span><span class="sxs-lookup"><span data-stu-id="86d01-359">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="86d01-360">**[1]** 為內部負載平衡器建立虛擬 IP 資源和健康情況探查</span><span class="sxs-lookup"><span data-stu-id="86d01-360">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

   <span data-ttu-id="86d01-361">請確定叢集狀態正常，且所有資源皆已啟動。</span><span class="sxs-lookup"><span data-stu-id="86d01-361">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="86d01-362">資源在哪一個節點上執行並不重要。</span><span class="sxs-lookup"><span data-stu-id="86d01-362">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="86d01-363">**[1]** 安裝 SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="86d01-363">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="86d01-364">以 root 身分使用虛擬主機名稱 (對應至 ASCS 負載平衡器前端組態的 IP 位址，例如 <b>nws-ascs</b>、<b>10.0.0.10</b>) 和您用於負載平衡器探查的執行個體號碼 (例如 <b>00</b>)，在第一個節點上安裝 SAP NetWeaver ASCS。</span><span class="sxs-lookup"><span data-stu-id="86d01-364">Install SAP NetWeaver ASCS as root on the first node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and the instance number that you used for the probe of the load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="86d01-365">您可以使用 sapinst 參數 SAPINST_REMOTE_ACCESS_USER 來允許非 root 使用者連線到 sapinst。</span><span class="sxs-lookup"><span data-stu-id="86d01-365">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="86d01-366">**[1]** 為內部負載平衡器建立虛擬 IP 資源和健康情況探查</span><span class="sxs-lookup"><span data-stu-id="86d01-366">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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
   # Do you still want to commit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="86d01-367">請確定叢集狀態正常，且所有資源皆已啟動。</span><span class="sxs-lookup"><span data-stu-id="86d01-367">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="86d01-368">資源在哪一個節點上執行並不重要。</span><span class="sxs-lookup"><span data-stu-id="86d01-368">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="86d01-369">**[2]** 安裝 SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="86d01-369">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="86d01-370">以 root 身分使用虛擬主機名稱 (對應至 ERS 負載平衡器前端組態的 IP 位址，例如 <b>nws-ers</b>、<b>10.0.0.11</b>) 和您用於負載平衡器探查的執行個體號碼 (例如 <b>02</b>)，在第二個節點上安裝 SAP NetWeaver ERS。</span><span class="sxs-lookup"><span data-stu-id="86d01-370">Install SAP NetWeaver ERS as root on the second node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and the instance number that you used for the probe of the load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="86d01-371">您可以使用 sapinst 參數 SAPINST_REMOTE_ACCESS_USER 來允許非 root 使用者連線到 sapinst。</span><span class="sxs-lookup"><span data-stu-id="86d01-371">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="86d01-372">請使用 SWPM SP 20 PL 05 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="86d01-372">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="86d01-373">較低版本無法正確設定權限，因而會讓安裝失敗。</span><span class="sxs-lookup"><span data-stu-id="86d01-373">Lower versions do not set the permissions correctly and the installation will fail.</span></span>
   > 

1. <span data-ttu-id="86d01-374">**[1]** 調整 ASCS/SCS 和 ERS 執行個體設定檔</span><span class="sxs-lookup"><span data-stu-id="86d01-374">**[1]** Adapt the ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="86d01-375">ASCS/SCS 設定檔</span><span class="sxs-lookup"><span data-stu-id="86d01-375">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change the restart command to a start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add the keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="86d01-376">ERS 設定檔</span><span class="sxs-lookup"><span data-stu-id="86d01-376">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="86d01-377">**[A]** 設定保持運作</span><span class="sxs-lookup"><span data-stu-id="86d01-377">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="86d01-378">SAP NetWeaver 應用程式伺服器和 ASCS/SCS 之間的通訊是透過軟體負載平衡器來路由傳送。</span><span class="sxs-lookup"><span data-stu-id="86d01-378">The communication between the SAP NetWeaver application server and the ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="86d01-379">在逾時時間 (可設定) 過後，負載平衡器就會將非作用中的連線中斷。</span><span class="sxs-lookup"><span data-stu-id="86d01-379">The load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="86d01-380">為防止這個情況，您需要在 SAP NetWeaver ASCS/SCS 設定檔中設定參數，並變更 Linux 系統設定。</span><span class="sxs-lookup"><span data-stu-id="86d01-380">To prevent this you need to set a parameter in the SAP NetWeaver ASCS/SCS profile and change the Linux system settings.</span></span> <span data-ttu-id="86d01-381">如需詳細資訊，請閱讀 [SAP Note 1410736][1410736]。</span><span class="sxs-lookup"><span data-stu-id="86d01-381">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="86d01-382">ASCS/SCS 設定檔參數 enque/encni/set_so_keepalive 已在最後一個步驟中新增。</span><span class="sxs-lookup"><span data-stu-id="86d01-382">The ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in the last step.</span></span>

   <pre><code> 
   # Change the Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="86d01-383">**[A]** 在安裝過後設定 SAP 使用者</span><span class="sxs-lookup"><span data-stu-id="86d01-383">**[A]** Configure the SAP users after the installation</span></span>
 
   <pre><code>
   # Add sidadm to the haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="86d01-384">**[1]** 在 sapservice 檔案中新增 ASCS 和 ERS SAP 服務</span><span class="sxs-lookup"><span data-stu-id="86d01-384">**[1]** Add the ASCS and ERS SAP services to the sapservice file</span></span>

   <span data-ttu-id="86d01-385">在第二個節點中新增 ASCS 服務項目，並將 ERS 服務項目複製到第一個節點。</span><span class="sxs-lookup"><span data-stu-id="86d01-385">Add the ASCS service entry to the second node and copy the ERS service entry to the first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="86d01-386">**[1]** 建立 SAP 叢集資源</span><span class="sxs-lookup"><span data-stu-id="86d01-386">**[1]** Create the SAP cluster resources</span></span>

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

   <span data-ttu-id="86d01-387">請確定叢集狀態正常，且所有資源皆已啟動。</span><span class="sxs-lookup"><span data-stu-id="86d01-387">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="86d01-388">資源在哪一個節點上執行並不重要。</span><span class="sxs-lookup"><span data-stu-id="86d01-388">It is not important on which node the resources are running.</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="86d01-389">建立 STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="86d01-389">Create STONITH device</span></span>

<span data-ttu-id="86d01-390">STONITH 裝置會使用服務主體來對 Microsoft Azure 授權。</span><span class="sxs-lookup"><span data-stu-id="86d01-390">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="86d01-391">請遵循下列步驟來建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="86d01-391">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="86d01-392">移至 <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="86d01-392">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="86d01-393">開啟 [Azure Active Directory] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="86d01-393">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="86d01-394">移至 [屬性]，並記下目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="86d01-394">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="86d01-395">這是**租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="86d01-395">This is the **tenant id**.</span></span>
1. <span data-ttu-id="86d01-396">按一下 [應用程式註冊]</span><span class="sxs-lookup"><span data-stu-id="86d01-396">Click App registrations</span></span>
1. <span data-ttu-id="86d01-397">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="86d01-397">Click Add</span></span>
1. <span data-ttu-id="86d01-398">輸入名稱、選取應用程式類型 [Web 應用程式/API]、輸入登入 URL (例如 http://localhost )，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="86d01-398">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="86d01-399">登入 URL 並未使用，而且可以是任何有效的 URL</span><span class="sxs-lookup"><span data-stu-id="86d01-399">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="86d01-400">選取新的應用程式，然後按一下 [設定] 索引標籤中的金鑰</span><span class="sxs-lookup"><span data-stu-id="86d01-400">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="86d01-401">輸入新金鑰的說明、選取 [永不過期]，然後按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="86d01-401">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="86d01-402">記下值。</span><span class="sxs-lookup"><span data-stu-id="86d01-402">Write down the Value.</span></span> <span data-ttu-id="86d01-403">此值會用來做為服務主體的**密碼**</span><span class="sxs-lookup"><span data-stu-id="86d01-403">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="86d01-404">記下應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="86d01-404">Write down the Application Id.</span></span> <span data-ttu-id="86d01-405">此識別碼會用來做為服務主體的使用者名稱 (以下步驟中的 **login id**)</span><span class="sxs-lookup"><span data-stu-id="86d01-405">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="86d01-406">服務主體預設沒有存取您 Azure 資源的權限。</span><span class="sxs-lookup"><span data-stu-id="86d01-406">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="86d01-407">您需要為服務主體提供權限來啟動和停止 (解除配置) 叢集的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="86d01-407">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="86d01-408">移至 https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="86d01-408">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="86d01-409">開啟 [所有資源] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="86d01-409">Open the All resources blade</span></span>
1. <span data-ttu-id="86d01-410">選取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="86d01-410">Select the virtual machine</span></span>
1. <span data-ttu-id="86d01-411">選取 [存取控制 (IAM)]</span><span class="sxs-lookup"><span data-stu-id="86d01-411">Click Access control (IAM)</span></span>
1. <span data-ttu-id="86d01-412">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="86d01-412">Click Add</span></span>
1. <span data-ttu-id="86d01-413">選取 [擁有者] 角色</span><span class="sxs-lookup"><span data-stu-id="86d01-413">Select the role Owner</span></span>
1. <span data-ttu-id="86d01-414">輸入您先前建立的應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="86d01-414">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="86d01-415">Click OK</span><span class="sxs-lookup"><span data-stu-id="86d01-415">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="86d01-416">**[1]** 建立 STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="86d01-416">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="86d01-417">當您編輯虛擬機器的權限之後，就可以在叢集中設定 STONITH 裝置。</span><span class="sxs-lookup"><span data-stu-id="86d01-417">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="86d01-418">**[1]** 啟用 STONITH 裝置的使用</span><span class="sxs-lookup"><span data-stu-id="86d01-418">**[1]** Enable the use of a STONITH device</span></span>

<span data-ttu-id="86d01-419">啟用 STONITH 裝置的使用</span><span class="sxs-lookup"><span data-stu-id="86d01-419">Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="86d01-420">安裝資料庫</span><span class="sxs-lookup"><span data-stu-id="86d01-420">Install database</span></span>

<span data-ttu-id="86d01-421">此範例會安裝並設定 SAP HANA 系統複寫。</span><span class="sxs-lookup"><span data-stu-id="86d01-421">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="86d01-422">SAP HANA 會在和 SAP NetWeaver ASCS/SCS 與 ERS 相同的叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="86d01-422">SAP HANA will run in the same cluster as the SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="86d01-423">您也可以將 SAP HANA 安裝在專用叢集上。</span><span class="sxs-lookup"><span data-stu-id="86d01-423">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="86d01-424">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP HANA 高可用性][sap-hana-ha]。</span><span class="sxs-lookup"><span data-stu-id="86d01-424">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="86d01-425">準備進行 SAP HANA 安裝</span><span class="sxs-lookup"><span data-stu-id="86d01-425">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="86d01-426">我們通常建議針對儲存資料和記錄檔的磁碟區使用 LVM。</span><span class="sxs-lookup"><span data-stu-id="86d01-426">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="86d01-427">若要進行測試，您也可以選擇將資料和記錄檔直接儲存在一般磁碟上。</span><span class="sxs-lookup"><span data-stu-id="86d01-427">For testing purposes, you can also choose to store the data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="86d01-428">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="86d01-428">**[A]** LVM</span></span>  
   <span data-ttu-id="86d01-429">下列範例假設虛擬機器已連接四個資料磁碟，這些資料磁碟應該用來建立兩個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="86d01-429">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
   
   <span data-ttu-id="86d01-430">針對您想要使用的所有磁碟建立實體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="86d01-430">Create physical volumes for all disks that you want to use.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="86d01-431">建立一個適用於資料檔案的磁碟區群組、一個用於記錄檔的磁碟區群組，以及一個用於 SAP HANA 共用目錄的磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="86d01-431">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="86d01-432">建立邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="86d01-432">Create the logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="86d01-433">建立掛接目錄，並複製所有邏輯磁碟區的 UUID</span><span class="sxs-lookup"><span data-stu-id="86d01-433">Create the mount directories and copy the UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="86d01-434">針對這三個邏輯磁碟區建立 autofs 項目</span><span class="sxs-lookup"><span data-stu-id="86d01-434">Create autofs entries for the three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="86d01-435">將這一行插入 sudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="86d01-435">Insert this line to sudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="86d01-436">掛接新的磁碟區</span><span class="sxs-lookup"><span data-stu-id="86d01-436">Mount the new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="86d01-437">**[A]** 一般磁碟</span><span class="sxs-lookup"><span data-stu-id="86d01-437">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="86d01-438">針對小型或示範系統，您可以將 HANA 資料和記錄檔放在一個磁碟上。</span><span class="sxs-lookup"><span data-stu-id="86d01-438">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="86d01-439">下列命令會在 /dev/sdc 上建立磁碟分割，並使用 xfs 來將它格式化。</span><span class="sxs-lookup"><span data-stu-id="86d01-439">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down the id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="86d01-440">將這一行插入 /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="86d01-440">Insert this line to /etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="86d01-441">建立目標目錄並掛接磁碟。</span><span class="sxs-lookup"><span data-stu-id="86d01-441">Create the target directory and mount the disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="86d01-442">安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="86d01-442">Installing SAP HANA</span></span>

<span data-ttu-id="86d01-443">下列步驟的根據是用來安裝 SAP HANA 系統複寫之 [SAP HANA SR 效能最佳化案例指南 (英文)][suse-hana-ha-guide] 的第 4 章。</span><span class="sxs-lookup"><span data-stu-id="86d01-443">The following steps are based on chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span> <span data-ttu-id="86d01-444">請仔細閱讀，然後再繼續安裝。</span><span class="sxs-lookup"><span data-stu-id="86d01-444">Please read it before you continue the installation.</span></span>

1. <span data-ttu-id="86d01-445">**[A]** 從 HANA DVD 執行 hdblcm</span><span class="sxs-lookup"><span data-stu-id="86d01-445">**[A]** Run hdblcm from the HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="86d01-446">**[A]** 升級 SAP 主機代理程式</span><span class="sxs-lookup"><span data-stu-id="86d01-446">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="86d01-447">從 [SAP 軟體中心 (英文)][sap-swcenter] 下載最新的 SAP 主機代理程式封存檔，然後執行下列命令來升級代理程式。</span><span class="sxs-lookup"><span data-stu-id="86d01-447">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="86d01-448">取代封存檔的路徑以指向您所下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="86d01-448">Replace the path to the archive to point to the file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path to SAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="86d01-449">**[1]** 建立 HANA 複寫 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="86d01-449">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="86d01-450">執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="86d01-450">Run the following command.</span></span> <span data-ttu-id="86d01-451">請務必使用 SAP HANA 安裝的值來取代粗體字串 (HANA 系統識別碼 HDB 和執行個體號碼 03)。</span><span class="sxs-lookup"><span data-stu-id="86d01-451">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="86d01-452">**[A]** 建立金鑰儲存區項目 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="86d01-452">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="86d01-453">**[1]** 備份資料庫 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="86d01-453">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="86d01-454">**[1]** 切換至 HANA sapsid 使用者，並建立主要站台。</span><span class="sxs-lookup"><span data-stu-id="86d01-454">**[1]** Switch to the HANA sapsid user and create the primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="86d01-455">**[2]** 切換至 HANA sapsid 使用者，並建立次要站台。</span><span class="sxs-lookup"><span data-stu-id="86d01-455">**[2]** Switch to the HANA sapsid user and create the secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="86d01-456">**[1]** 建立 SAP HANA 叢集資源</span><span class="sxs-lookup"><span data-stu-id="86d01-456">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="86d01-457">首先，建立拓撲。</span><span class="sxs-lookup"><span data-stu-id="86d01-457">First, create the topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number and HANA system id
   
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
   
   <span data-ttu-id="86d01-458">接下來，建立 HANA 資源</span><span class="sxs-lookup"><span data-stu-id="86d01-458">Next, create the HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
    
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

   <span data-ttu-id="86d01-459">請確定叢集狀態正常，且所有資源皆已啟動。</span><span class="sxs-lookup"><span data-stu-id="86d01-459">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="86d01-460">資源在哪一個節點上執行並不重要。</span><span class="sxs-lookup"><span data-stu-id="86d01-460">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="86d01-461">**[1]** 安裝 SAP NetWeaver 資料庫執行個體</span><span class="sxs-lookup"><span data-stu-id="86d01-461">**[1]** Install the SAP NetWeaver database instance</span></span>

   <span data-ttu-id="86d01-462">以 root 身分使用虛擬主機名稱 (對應至資料庫負載平衡器前端組態的 IP 位址，例如 <b>nws-db</b> 和 <b>10.0.0.12</b>) 來安裝 SAP NetWeaver 資料庫執行個體。</span><span class="sxs-lookup"><span data-stu-id="86d01-462">Install the SAP NetWeaver database instance as root using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="86d01-463">您可以使用 sapinst 參數 SAPINST_REMOTE_ACCESS_USER 來允許非 root 使用者連線到 sapinst。</span><span class="sxs-lookup"><span data-stu-id="86d01-463">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="86d01-464">SAP NetWeaver 應用程式伺服器安裝</span><span class="sxs-lookup"><span data-stu-id="86d01-464">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="86d01-465">請遵循下列步驟來安裝 SAP 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="86d01-465">Follow these steps to install an SAP application server.</span></span> <span data-ttu-id="86d01-466">以下步驟假設您將應用程式伺服器安裝在與 ASCS/SCS 和 HANA 伺服器不同的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="86d01-466">The steps bellow assume that you install the application server on a server different from the ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="86d01-467">否則，您就不必進行以下某些步驟 (例如設定主機名稱解析)。</span><span class="sxs-lookup"><span data-stu-id="86d01-467">Otherwise some of the steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="86d01-468">設定主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="86d01-468">Setup host name resolution</span></span>    
   <span data-ttu-id="86d01-469">您可以使用 DNS 伺服器，或修改所有節點上的 /etc/hosts。</span><span class="sxs-lookup"><span data-stu-id="86d01-469">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="86d01-470">這個範例示範如何使用 /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="86d01-470">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="86d01-471">取代下列命令中的 IP 位址和主機名稱</span><span class="sxs-lookup"><span data-stu-id="86d01-471">Replace the IP address and the hostname in the following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="86d01-472">將下列幾行插入至 /etc/hosts。</span><span class="sxs-lookup"><span data-stu-id="86d01-472">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="86d01-473">變更 IP 位址和主機名稱以符合您的環境</span><span class="sxs-lookup"><span data-stu-id="86d01-473">Change the IP address and hostname to match your environment</span></span>    
    
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of the application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="86d01-474">建立 sapmnt 目錄</span><span class="sxs-lookup"><span data-stu-id="86d01-474">Create the sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="86d01-475">設定 autofs</span><span class="sxs-lookup"><span data-stu-id="86d01-475">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="86d01-476">使用下列命令建立新檔案</span><span class="sxs-lookup"><span data-stu-id="86d01-476">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="86d01-477">重新啟動 autofs 來裝載新的共用</span><span class="sxs-lookup"><span data-stu-id="86d01-477">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="86d01-478">設定分頁檔</span><span class="sxs-lookup"><span data-stu-id="86d01-478">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="86d01-479">重新啟動代理程式以啟動變更</span><span class="sxs-lookup"><span data-stu-id="86d01-479">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="86d01-480">安裝 SAP NetWeaver 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="86d01-480">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="86d01-481">安裝主要或其他的 SAP NetWeaver 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="86d01-481">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="86d01-482">您可以使用 sapinst 參數 SAPINST_REMOTE_ACCESS_USER 來允許非 root 使用者連線到 sapinst。</span><span class="sxs-lookup"><span data-stu-id="86d01-482">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="86d01-483">更新 SAP HANA 安全存放區</span><span class="sxs-lookup"><span data-stu-id="86d01-483">Update SAP HANA secure store</span></span>

   <span data-ttu-id="86d01-484">將 SAP HANA 安全存放區更新為指向 SAP HANA 系統複寫設定的虛擬名稱。</span><span class="sxs-lookup"><span data-stu-id="86d01-484">Update the SAP HANA secure store to point to the virtual name of the SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="86d01-485">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86d01-485">Next steps</span></span>
* <span data-ttu-id="86d01-486">[適用於 SAP 的 Azure 虛擬機器規劃和實作][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="86d01-486">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="86d01-487">[適用於 SAP 的 Azure 虛擬機器部署][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="86d01-487">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="86d01-488">[適用於 SAP 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="86d01-488">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="86d01-489">若要了解如何建立高可用性並為 Azure 上的 SAP HANA 規劃災害復原，請參閱 [Azure 上的 SAP HANA (大型執行個體) 高可用性和災害復原](hana-overview-high-availability-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="86d01-489">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="86d01-490">若要了解如何建立高可用性並為 Azure VM 上的 SAP HANA 規劃災害復原，請參閱 [Azure 虛擬機器 (VM) 上 SAP HANA 的高可用性][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="86d01-490">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>