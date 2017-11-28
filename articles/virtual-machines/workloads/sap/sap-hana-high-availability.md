---
title: "aaaHigh 可用性的 SAP HANA Azure 虛擬機器 (Vm) 上 |Microsoft 文件"
description: "在 Azure 虛擬機器 (VM) 上，建立 SAP HANA 的高可用性。"
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="f71ca-103">Azure 虛擬機器 (VM) 上 SAP HANA 的高可用性</span><span class="sxs-lookup"><span data-stu-id="f71ca-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="f71ca-113">內部部署，您可以使用任一 HANA 系統複寫，或使用 SAP hana 的共用存放裝置 tooestablish 高可用性。</span><span class="sxs-lookup"><span data-stu-id="f71ca-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="f71ca-114">我們目前只支援在 Azure 上設定 HANA 系統複寫。</span><span class="sxs-lookup"><span data-stu-id="f71ca-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="f71ca-115">SAP HANA 複寫是由一個主要節點以及至少一個從屬節點所組成。</span><span class="sxs-lookup"><span data-stu-id="f71ca-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="f71ca-116">變更 toohello hello 主要節點上的資料會在同步或非同步方式複寫 toohello 從屬節點。</span><span class="sxs-lookup"><span data-stu-id="f71ca-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="f71ca-117">本文說明 toodeploy hello 虛擬機器，設定 hello 虛擬機器的方式、 安裝 hello 叢集架構、 安裝和設定 SAP HANA 系統複寫。</span><span class="sxs-lookup"><span data-stu-id="f71ca-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="f71ca-118">在 hello 範例組態中，安裝命令等執行個體號碼 03 和 HANA 系統識別碼 HDB 用。</span><span class="sxs-lookup"><span data-stu-id="f71ca-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="f71ca-119">讀取 hello 遵循 SAP 附註和白皮書</span><span class="sxs-lookup"><span data-stu-id="f71ca-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="f71ca-120">SAP Note [1928533]，其中包含：</span><span class="sxs-lookup"><span data-stu-id="f71ca-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="f71ca-121">Hello 部署 SAP 軟體所支援的 Azure VM 大小的清單</span><span class="sxs-lookup"><span data-stu-id="f71ca-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="f71ca-122">Azure VM 大小的重要容量資訊</span><span class="sxs-lookup"><span data-stu-id="f71ca-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="f71ca-123">支援的 SAP 軟體，以及作業系統 (OS) 與資料庫組合</span><span class="sxs-lookup"><span data-stu-id="f71ca-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="f71ca-124">Microsoft Azure 上 Windows 和 Linux 所需的 SAP 核心版本</span><span class="sxs-lookup"><span data-stu-id="f71ca-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="f71ca-125">SAP Note [2015553] 列出 Azure 中 SAP 支援的 SAP 軟體部署先決條件。</span><span class="sxs-lookup"><span data-stu-id="f71ca-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="f71ca-126">SAP Note [2205917] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的建議 OS 設定</span><span class="sxs-lookup"><span data-stu-id="f71ca-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="f71ca-127">SAP Note [1944799] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的 SAP HANA 指導方針</span><span class="sxs-lookup"><span data-stu-id="f71ca-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="f71ca-128">SAP Note [2178632] 包含在 Azure 中針對 SAP 回報的所有監視計量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f71ca-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="f71ca-129">SAP 附註[2191498]具有 hello 必要 SAP Host Agent 版本適用於在 Azure 中的 Linux。</span><span class="sxs-lookup"><span data-stu-id="f71ca-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="f71ca-130">SAP Note [2243692] 包含 Azure 中 Linux 上的 SAP 授權相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f71ca-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="f71ca-131">SAP Note [1984787] 包含 SUSE LINUX Enterprise Server 12 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="f71ca-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="f71ca-132">SAP 附註[1999351] hello Azure 強化監視功能延伸模組適用於 SAP 的其他疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="f71ca-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="f71ca-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) 包含 Linux 所需的所有 SAP Note。</span><span class="sxs-lookup"><span data-stu-id="f71ca-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="f71ca-134">[適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="f71ca-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="f71ca-135">[適用於 SAP on Linux 的 Azure 虛擬機器部署 (本文)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="f71ca-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="f71ca-136">[適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="f71ca-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="f71ca-137">[SAP HANA SR-IOV 的效能最佳化的案例][ suse-hana-ha-guide] hello 指南包含所有必要的資訊 tooset SAP HANA 系統複寫在內部。</span><span class="sxs-lookup"><span data-stu-id="f71ca-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="f71ca-138">請使用此指南做為基礎。</span><span class="sxs-lookup"><span data-stu-id="f71ca-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="f71ca-139">部署 Linux</span><span class="sxs-lookup"><span data-stu-id="f71ca-139">Deploying Linux</span></span>

<span data-ttu-id="f71ca-140">SAP hana hello 資源代理程式包含在 SUSE Linux Enterprise Server 中的 SAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f71ca-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="f71ca-141">hello Azure Marketplace 包含 BYOS （攜帶您自己訂閱），您可以使用 toodeploy 新的虛擬機器使用的 SAP 應用程式 12 for SUSE Linux Enterprise Server 映像。</span><span class="sxs-lookup"><span data-stu-id="f71ca-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="f71ca-142">手動部署</span><span class="sxs-lookup"><span data-stu-id="f71ca-142">Manual Deployment</span></span>

1. <span data-ttu-id="f71ca-143">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="f71ca-143">Create a Resource Group</span></span>
1. <span data-ttu-id="f71ca-144">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="f71ca-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="f71ca-145">建立兩個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f71ca-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="f71ca-146">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="f71ca-146">Create an Availability Set</span></span>  
   <span data-ttu-id="f71ca-147">設定更新網域上限</span><span class="sxs-lookup"><span data-stu-id="f71ca-147">Set max update domain</span></span>
1. <span data-ttu-id="f71ca-148">建立負載平衡器 (內部)</span><span class="sxs-lookup"><span data-stu-id="f71ca-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="f71ca-149">選取上述步驟的 VNET</span><span class="sxs-lookup"><span data-stu-id="f71ca-149">Select VNET of step above</span></span>
1. <span data-ttu-id="f71ca-150">建立虛擬機器 1</span><span class="sxs-lookup"><span data-stu-id="f71ca-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="f71ca-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="f71ca-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="f71ca-152">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="f71ca-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="f71ca-153">選取儲存體帳戶 1</span><span class="sxs-lookup"><span data-stu-id="f71ca-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="f71ca-154">選取可用性設定組</span><span class="sxs-lookup"><span data-stu-id="f71ca-154">Select Availability Set</span></span>  
1. <span data-ttu-id="f71ca-155">建立虛擬機器 2</span><span class="sxs-lookup"><span data-stu-id="f71ca-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="f71ca-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="f71ca-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="f71ca-157">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="f71ca-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="f71ca-158">選取儲存體帳戶 2</span><span class="sxs-lookup"><span data-stu-id="f71ca-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="f71ca-159">選取可用性設定組</span><span class="sxs-lookup"><span data-stu-id="f71ca-159">Select Availability Set</span></span>  
1. <span data-ttu-id="f71ca-160">新增資料磁碟</span><span class="sxs-lookup"><span data-stu-id="f71ca-160">Add Data Disks</span></span>
1. <span data-ttu-id="f71ca-161">Hello 負載平衡器設定</span><span class="sxs-lookup"><span data-stu-id="f71ca-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="f71ca-162">建立前端 IP 集區</span><span class="sxs-lookup"><span data-stu-id="f71ca-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="f71ca-163">開啟 hello 負載平衡器，選取前端 IP 集區，然後按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f71ca-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="f71ca-164">輸入 hello hello 前端 IP 集區 （例如前端 hana） 名稱</span><span class="sxs-lookup"><span data-stu-id="f71ca-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="f71ca-165">Click OK</span><span class="sxs-lookup"><span data-stu-id="f71ca-165">Click OK</span></span>
        1. <span data-ttu-id="f71ca-166">建立 hello 前端 IP 集區之後，請記下其 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f71ca-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="f71ca-167">建立後端集區</span><span class="sxs-lookup"><span data-stu-id="f71ca-167">Create a backend pool</span></span>
        1. <span data-ttu-id="f71ca-168">開啟 hello 負載平衡器選取後端集區，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f71ca-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="f71ca-169">輸入 hello 名稱 hello 新後端集區 （例如 hana-後端）</span><span class="sxs-lookup"><span data-stu-id="f71ca-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="f71ca-170">按一下 [新增虛擬機器]</span><span class="sxs-lookup"><span data-stu-id="f71ca-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="f71ca-171">選取您稍早建立可用性設定組的 hello</span><span class="sxs-lookup"><span data-stu-id="f71ca-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="f71ca-172">選取 hello 的 hello SAP HANA 叢集的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f71ca-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="f71ca-173">Click OK</span><span class="sxs-lookup"><span data-stu-id="f71ca-173">Click OK</span></span>
    1. <span data-ttu-id="f71ca-174">建立健康狀態探查</span><span class="sxs-lookup"><span data-stu-id="f71ca-174">Create a health probe</span></span>
       1. <span data-ttu-id="f71ca-175">開啟 hello 負載平衡器選取健全狀況探查，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f71ca-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="f71ca-176">輸入新健全狀況探查 hello (例如 hp hana) hello 名稱</span><span class="sxs-lookup"><span data-stu-id="f71ca-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="f71ca-177">選取 TCP 當做通訊協定、連接埠 625**03**，保留間隔 5 和狀況不良閾值 2</span><span class="sxs-lookup"><span data-stu-id="f71ca-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="f71ca-178">Click OK</span><span class="sxs-lookup"><span data-stu-id="f71ca-178">Click OK</span></span>
    1. <span data-ttu-id="f71ca-179">建立負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="f71ca-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="f71ca-180">開啟 hello 負載平衡器，選取負載平衡規則並按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f71ca-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="f71ca-181">輸入 hello hello 新的負載平衡器規則名稱 (例如 hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="f71ca-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="f71ca-182">選取 hello 前端 IP 位址、 後端集區和健全狀況探查您稍早建立 （例如前端 hana）</span><span class="sxs-lookup"><span data-stu-id="f71ca-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="f71ca-183">保留通訊協定 TCP，輸入連接埠 3**03**15</span><span class="sxs-lookup"><span data-stu-id="f71ca-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="f71ca-184">增加閒置逾時 too30 分鐘數</span><span class="sxs-lookup"><span data-stu-id="f71ca-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="f71ca-185">**請確定 tooenable 浮動 IP**</span><span class="sxs-lookup"><span data-stu-id="f71ca-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="f71ca-186">Click OK</span><span class="sxs-lookup"><span data-stu-id="f71ca-186">Click OK</span></span>
        1. <span data-ttu-id="f71ca-187">重複上述步驟，hello 埠 3**03**17</span><span class="sxs-lookup"><span data-stu-id="f71ca-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="f71ca-188">透過範本進行部署</span><span class="sxs-lookup"><span data-stu-id="f71ca-188">Deploy with template</span></span>
<span data-ttu-id="f71ca-189">您可以使用其中一個 hello 快速入門範本 github toodeploy 上所有必要的資源。</span><span class="sxs-lookup"><span data-stu-id="f71ca-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="f71ca-190">hello 範本部署 hello 虛擬機器、 hello 負載平衡器、 可用性設定組等等。請遵循這些步驟 toodeploy hello 範本：</span><span class="sxs-lookup"><span data-stu-id="f71ca-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="f71ca-191">開啟 hello[資料庫範本][ template-multisid-db]或 hello[交集範本][ template-converged] hello Azure 入口網站上 hello 資料庫範本只建立 hello資料庫的負載平衡規則而 hello 交集的範本也會建立 hello 負載平衡規則 ASCS/SCS 和端 (只有 Linux) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f71ca-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="f71ca-192">如果您計劃 tooinstall SAP NetWeaver 架構系統，而且也想 tooinstall hello ASCS/SCS 執行個體上 hello 相同機器，請使用 hello[交集範本][template-converged]。</span><span class="sxs-lookup"><span data-stu-id="f71ca-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="f71ca-193">輸入下列參數的 hello</span><span class="sxs-lookup"><span data-stu-id="f71ca-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="f71ca-194">SAP 系統識別碼</span><span class="sxs-lookup"><span data-stu-id="f71ca-194">Sap System Id</span></span>  
       <span data-ttu-id="f71ca-195">輸入 hello 想 tooinstall 的 SAP 系統的 hello SAP 的系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="f71ca-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="f71ca-196">hello 識別碼將用於做為前置詞已部署的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="f71ca-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="f71ca-197">堆疊類型 （僅適用於您使用 hello 交集的範本）</span><span class="sxs-lookup"><span data-stu-id="f71ca-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="f71ca-198">選取 hello SAP NetWeaver 堆疊類型</span><span class="sxs-lookup"><span data-stu-id="f71ca-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="f71ca-199">OS 類型</span><span class="sxs-lookup"><span data-stu-id="f71ca-199">Os Type</span></span>  
       <span data-ttu-id="f71ca-200">選取其中一個 hello Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="f71ca-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="f71ca-201">在此範例中，請選取 SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="f71ca-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="f71ca-202">DB 類型</span><span class="sxs-lookup"><span data-stu-id="f71ca-202">Db Type</span></span>  
       <span data-ttu-id="f71ca-203">選取 HANA</span><span class="sxs-lookup"><span data-stu-id="f71ca-203">Select HANA</span></span>
    1. <span data-ttu-id="f71ca-204">SAP 系統大小</span><span class="sxs-lookup"><span data-stu-id="f71ca-204">Sap System Size</span></span>  
       <span data-ttu-id="f71ca-205">將提供的 SAPS hello 新系統的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="f71ca-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="f71ca-206">如果您不確定需要多少的 SAPS hello 系統，請要求您的 SAP 技術合作夥伴或系統整合者</span><span class="sxs-lookup"><span data-stu-id="f71ca-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="f71ca-207">系統可用性</span><span class="sxs-lookup"><span data-stu-id="f71ca-207">System Availability</span></span>  
       <span data-ttu-id="f71ca-208">選取 HA</span><span class="sxs-lookup"><span data-stu-id="f71ca-208">Select HA</span></span>
    1. <span data-ttu-id="f71ca-209">管理員使用者名稱和管理員密碼</span><span class="sxs-lookup"><span data-stu-id="f71ca-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="f71ca-210">會建立新的使用者，可以使用的 toolog toohello 機器上。</span><span class="sxs-lookup"><span data-stu-id="f71ca-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="f71ca-211">新的或現有的子網路</span><span class="sxs-lookup"><span data-stu-id="f71ca-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="f71ca-212">決定應該建立新的虛擬網路和子網路，或是應該使用現有子網路。</span><span class="sxs-lookup"><span data-stu-id="f71ca-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="f71ca-213">如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取現有的。</span><span class="sxs-lookup"><span data-stu-id="f71ca-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="f71ca-214">子網路識別碼</span><span class="sxs-lookup"><span data-stu-id="f71ca-214">Subnet Id</span></span>  
    <span data-ttu-id="f71ca-215">hello 識別碼 hello 子網路 toowhich hello 虛擬機器應該連接到。</span><span class="sxs-lookup"><span data-stu-id="f71ca-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="f71ca-216">選取您的 VPN 或 Express Route 虛擬網路 tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="f71ca-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="f71ca-217">hello 識別碼通常看起來像 /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="f71ca-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="f71ca-218">設定 Linux HA</span><span class="sxs-lookup"><span data-stu-id="f71ca-218">Setting up Linux HA</span></span>

<span data-ttu-id="f71ca-219">是 [A]-適用 tooall 節點、 [1]-1 或 2 僅適用於 toonode-僅適用於 toonode 2 有前置 hello 下列項目。</span><span class="sxs-lookup"><span data-stu-id="f71ca-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="f71ca-220">[A] SLES 適用於 SAP BYOS 只-註冊 SLES toobe 無法 toouse hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="f71ca-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="f71ca-221">[A] 僅限 SLES for SAP BYOS - 新增公用雲端模組</span><span class="sxs-lookup"><span data-stu-id="f71ca-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="f71ca-222">[A] 更新 SLES</span><span class="sxs-lookup"><span data-stu-id="f71ca-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="f71ca-223">[1] 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="f71ca-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="f71ca-224">[2] 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="f71ca-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="f71ca-225">[1] 啟用 SSH 存取</span><span class="sxs-lookup"><span data-stu-id="f71ca-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="f71ca-226">[A] 安裝 HA 擴充功能</span><span class="sxs-lookup"><span data-stu-id="f71ca-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="f71ca-227">[A] 設定磁碟配置</span><span class="sxs-lookup"><span data-stu-id="f71ca-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="f71ca-228">LVM</span><span class="sxs-lookup"><span data-stu-id="f71ca-228">LVM</span></span>  
    <span data-ttu-id="f71ca-229">我們通常會建議 toouse LVM 磁碟區的儲存資料和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f71ca-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="f71ca-230">以下的 hello 範例假設 hello 虛擬機器有四個資料磁碟連接是應該使用的 toocreate 兩個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f71ca-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="f71ca-231">建立您想 toouse 的所有磁碟的實體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f71ca-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="f71ca-232">建立 hello 資料檔案的磁碟區群組，一個 hello 記錄檔的磁碟區群組，一個用於 hello 共用目錄的 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f71ca-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="f71ca-233">建立 hello 邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="f71ca-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="f71ca-234">建立 hello 掛接目錄，並複製 hello 的所有邏輯磁碟區的 UUID</span><span class="sxs-lookup"><span data-stu-id="f71ca-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="f71ca-235">建立 hello fstab 項目三個邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="f71ca-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="f71ca-236">插入此線條太/等/fstab</span><span class="sxs-lookup"><span data-stu-id="f71ca-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="f71ca-237">掛接 hello 新磁碟區</span><span class="sxs-lookup"><span data-stu-id="f71ca-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="f71ca-238">一般磁碟</span><span class="sxs-lookup"><span data-stu-id="f71ca-238">Plain Disks</span></span>  
       <span data-ttu-id="f71ca-239">針對小型或示範系統，您可以將 HANA 資料和記錄檔放在一個磁碟上。</span><span class="sxs-lookup"><span data-stu-id="f71ca-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="f71ca-240">hello 下列命令 /dev/sdc 上建立資料分割並格式化與 xfs。</span><span class="sxs-lookup"><span data-stu-id="f71ca-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="f71ca-241">請記下 /dev/sdc1 hello 識別碼</span><span class="sxs-lookup"><span data-stu-id="f71ca-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="f71ca-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="f71ca-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="f71ca-243">[A] 設定適用於所有主機的主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="f71ca-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="f71ca-244">您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。</span><span class="sxs-lookup"><span data-stu-id="f71ca-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="f71ca-245">這個範例會示範如何 toouse hello /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="f71ca-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="f71ca-246">取代 hello IP 位址和下列命令的 hello hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="f71ca-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="f71ca-247">插入 hello 下列各行太/等/主機。</span><span class="sxs-lookup"><span data-stu-id="f71ca-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="f71ca-248">變更您的環境的 hello IP 位址和主機名稱 toomatch</span><span class="sxs-lookup"><span data-stu-id="f71ca-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="f71ca-249">[1] 安裝叢集</span><span class="sxs-lookup"><span data-stu-id="f71ca-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="f71ca-250">[2] 新增節點 toocluster</span><span class="sxs-lookup"><span data-stu-id="f71ca-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="f71ca-251">[A] 變更 hacluster 密碼 toohello 相同的密碼</span><span class="sxs-lookup"><span data-stu-id="f71ca-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="f71ca-252">[A] 設定 corosync toouse 其他傳輸，並加入節點清單。</span><span class="sxs-lookup"><span data-stu-id="f71ca-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="f71ca-253">否則叢集將無法運作。</span><span class="sxs-lookup"><span data-stu-id="f71ca-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="f71ca-254">新增下列內容的粗體 toohello 檔 hello。</span><span class="sxs-lookup"><span data-stu-id="f71ca-254">Add hello following bold content toohello file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="f71ca-255">然後重新啟動 hello corosync 服務</span><span class="sxs-lookup"><span data-stu-id="f71ca-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="f71ca-256">[A] 安裝 HANA HA 套件</span><span class="sxs-lookup"><span data-stu-id="f71ca-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="f71ca-257">安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f71ca-257">Installing SAP HANA</span></span>

<span data-ttu-id="f71ca-258">請依照第 4 章 hello [SAP HANA SR-IOV 的效能最佳化的案例指南][ suse-hana-ha-guide] tooinstall SAP HANA 系統複寫。</span><span class="sxs-lookup"><span data-stu-id="f71ca-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="f71ca-259">[A] 從 hello HANA DVD 執行 hdblcm</span><span class="sxs-lookup"><span data-stu-id="f71ca-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="f71ca-260">選擇安裝 -> 1</span><span class="sxs-lookup"><span data-stu-id="f71ca-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="f71ca-261">選取要安裝的其他元件 -> 1</span><span class="sxs-lookup"><span data-stu-id="f71ca-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="f71ca-262">輸入安裝路徑 [/hana/shared]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-263">輸入本機主機名稱 [..]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-264">您想 tooadd 其他主機 toohello 系統嗎？</span><span class="sxs-lookup"><span data-stu-id="f71ca-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="f71ca-265">(y/n) [n]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-266">輸入 SAP HANA 系統識別碼︰<SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="f71ca-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="f71ca-267">輸入執行個體號碼 [00]：</span><span class="sxs-lookup"><span data-stu-id="f71ca-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="f71ca-268">HANA 執行個體號碼。</span><span class="sxs-lookup"><span data-stu-id="f71ca-268">HANA Instance number.</span></span> <span data-ttu-id="f71ca-269">如果您使用 hello Azure 範本，或遵循上述的 hello 範例，使用 03</span><span class="sxs-lookup"><span data-stu-id="f71ca-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="f71ca-270">選取資料庫模式 / 輸入索引 [1]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-271">選取系統使用量 / 輸入索引 [4]：</span><span class="sxs-lookup"><span data-stu-id="f71ca-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="f71ca-272">選取 hello 系統使用量</span><span class="sxs-lookup"><span data-stu-id="f71ca-272">Select hello system Usage</span></span>
    * <span data-ttu-id="f71ca-273">輸入資料磁碟區的位置 [/hana/data/HDB]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-274">輸入記錄檔磁碟區的位置 [/hana/log/HDB]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-275">是否限制記憶體配置上限？</span><span class="sxs-lookup"><span data-stu-id="f71ca-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="f71ca-276">[n]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-277">輸入主機的憑證主機名稱 '...'[…]:]-> [ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-278">輸入 SAP 主機代理程式使用者 (sapadm) 密碼：</span><span class="sxs-lookup"><span data-stu-id="f71ca-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="f71ca-279">確認 SAP 主機代理程式使用者 (sapadm) 密碼：</span><span class="sxs-lookup"><span data-stu-id="f71ca-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="f71ca-280">輸入系統管理員 (hdbadm) 密碼：</span><span class="sxs-lookup"><span data-stu-id="f71ca-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="f71ca-281">確認系統管理員 (hdbadm) 密碼：</span><span class="sxs-lookup"><span data-stu-id="f71ca-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="f71ca-282">輸入系統管理員主目錄 [/usr/sap/HDB/home]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-283">輸入系統管理員登入殼層 [/bin/sh]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-284">輸入系統管理員使用者識別碼 [1001]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-285">輸入使用者群組 (sapsys) 的識別碼 [79]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-286">輸入資料庫使用者 (SYSTEM) 密碼：</span><span class="sxs-lookup"><span data-stu-id="f71ca-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="f71ca-287">確認資料庫使用者 (SYSTEM) 密碼：</span><span class="sxs-lookup"><span data-stu-id="f71ca-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="f71ca-288">是否在電腦重新開機後重新啟動系統？</span><span class="sxs-lookup"><span data-stu-id="f71ca-288">Restart system after machine reboot?</span></span> <span data-ttu-id="f71ca-289">[n]：-> ENTER</span><span class="sxs-lookup"><span data-stu-id="f71ca-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="f71ca-290">您想 toocontinue 嗎？</span><span class="sxs-lookup"><span data-stu-id="f71ca-290">Do you want toocontinue?</span></span> <span data-ttu-id="f71ca-291">(y/n)：</span><span class="sxs-lookup"><span data-stu-id="f71ca-291">(y/n):</span></span>  
  <span data-ttu-id="f71ca-292">驗證摘要的 hello 並輸入 y toocontinue</span><span class="sxs-lookup"><span data-stu-id="f71ca-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="f71ca-293">[A] 升級 SAP 主機代理程式</span><span class="sxs-lookup"><span data-stu-id="f71ca-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="f71ca-294">Hello 從下載最新 SAP Host Agent 封存 hello [SAP Softwarecenter] [ sap-swcenter]並執行 hello 下列命令 tooupgrade hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f71ca-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="f71ca-295">取代 hello 路徑 toohello 封存 toopoint toohello 您下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="f71ca-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="f71ca-296">[1] 建立 HANA 複寫 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="f71ca-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="f71ca-297">執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="f71ca-297">Run hello following command.</span></span> <span data-ttu-id="f71ca-298">請確定 tooreplace 粗體字串 （HANA 系統識別碼 HDB 和執行個體編號 03），與 SAP HANA 安裝 hello 值。</span><span class="sxs-lookup"><span data-stu-id="f71ca-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="f71ca-299">[A] 建立金鑰儲存區項目 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="f71ca-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="f71ca-300">[1] 備份資料庫 (以 root 身分執行)</span><span class="sxs-lookup"><span data-stu-id="f71ca-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="f71ca-301">[1] 切換 toohello sapsid 使用者 (例如 hdbadm)，並建立 hello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="f71ca-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="f71ca-302">[2] 切換 toohello sapsid 使用者 (例如 hdbadm)，並建立 hello 次要站台。</span><span class="sxs-lookup"><span data-stu-id="f71ca-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="f71ca-303">設定叢集架構</span><span class="sxs-lookup"><span data-stu-id="f71ca-303">Configure Cluster Framework</span></span>

<span data-ttu-id="f71ca-304">變更 hello 預設設定</span><span class="sxs-lookup"><span data-stu-id="f71ca-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="f71ca-305">現在我們可以載入 hello 檔案 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="f71ca-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="f71ca-306">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="f71ca-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="f71ca-307">建立 STONITH 裝置</span><span class="sxs-lookup"><span data-stu-id="f71ca-307">Create STONITH device</span></span>

<span data-ttu-id="f71ca-308">hello STONITH 裝置會使用針對 Microsoft Azure 服務主體 tooauthorize。</span><span class="sxs-lookup"><span data-stu-id="f71ca-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="f71ca-309">請遵循這些步驟 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="f71ca-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="f71ca-310">跳過<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="f71ca-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="f71ca-311">開啟 hello Azure Active Directory 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="f71ca-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="f71ca-312">請移 tooProperties 並寫下 hello 目錄識別碼。這是 hello**租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="f71ca-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="f71ca-313">按一下 [應用程式註冊]</span><span class="sxs-lookup"><span data-stu-id="f71ca-313">Click App registrations</span></span>
1. <span data-ttu-id="f71ca-314">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f71ca-314">Click Add</span></span>
1. <span data-ttu-id="f71ca-315">輸入名稱、選取應用程式類型 [Web 應用程式/API]、輸入登入 URL (例如 http://localhost )，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="f71ca-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="f71ca-316">hello 登入 URL 不是，它可以是任何有效的 URL</span><span class="sxs-lookup"><span data-stu-id="f71ca-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="f71ca-317">選取 hello 新的應用程式，然後按一下 hello 設定 索引標籤中的 索引鍵</span><span class="sxs-lookup"><span data-stu-id="f71ca-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="f71ca-318">輸入新金鑰的說明、選取 [永不過期]，然後按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="f71ca-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="f71ca-319">記下 hello 值。</span><span class="sxs-lookup"><span data-stu-id="f71ca-319">Write down hello Value.</span></span> <span data-ttu-id="f71ca-320">它會當做 hello 使用**密碼**hello 服務主體</span><span class="sxs-lookup"><span data-stu-id="f71ca-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="f71ca-321">請記下 hello 應用程式識別碼。它作為 hello 使用者名稱 (**登入識別碼**hello 步驟中) 的 hello 服務主體</span><span class="sxs-lookup"><span data-stu-id="f71ca-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="f71ca-322">hello 服務主體沒有權限 tooaccess 您的 Azure 資源預設。</span><span class="sxs-lookup"><span data-stu-id="f71ca-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="f71ca-323">您需要 toogive hello 服務主體的權限 toostart 和停止 （取消配置） hello 叢集的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f71ca-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="f71ca-324">移 toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="f71ca-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="f71ca-325">開啟 hello 所有資源刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="f71ca-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="f71ca-326">選取 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f71ca-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="f71ca-327">選取 [存取控制 (IAM)]</span><span class="sxs-lookup"><span data-stu-id="f71ca-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="f71ca-328">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f71ca-328">Click Add</span></span>
1. <span data-ttu-id="f71ca-329">選取 hello 角色擁有者</span><span class="sxs-lookup"><span data-stu-id="f71ca-329">Select hello role Owner</span></span>
1. <span data-ttu-id="f71ca-330">輸入 hello hello 先前建立的應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="f71ca-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="f71ca-331">Click OK</span><span class="sxs-lookup"><span data-stu-id="f71ca-331">Click OK</span></span>

<span data-ttu-id="f71ca-332">編輯 hello hello 虛擬機器的權限之後，您可以設定 hello STONITH 裝置 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="f71ca-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="f71ca-333">現在我們可以載入 hello 檔案 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="f71ca-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="f71ca-334">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="f71ca-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="f71ca-335">建立 SAP HANA 資源</span><span class="sxs-lookup"><span data-stu-id="f71ca-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="f71ca-336">現在我們可以載入 hello 檔案 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="f71ca-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="f71ca-337">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="f71ca-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="f71ca-338">現在我們可以載入 hello 檔案 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="f71ca-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="f71ca-339">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="f71ca-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="f71ca-340">測試叢集設定</span><span class="sxs-lookup"><span data-stu-id="f71ca-340">Test cluster setup</span></span>
<span data-ttu-id="f71ca-341">hello 下列章節說明如何測試您的設定。</span><span class="sxs-lookup"><span data-stu-id="f71ca-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="f71ca-342">每一個測試會假設是根而且 hello SAP HANA 主要在 hello 虛擬機器 saphanavm1 上執行。</span><span class="sxs-lookup"><span data-stu-id="f71ca-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="f71ca-343">隔離測試</span><span class="sxs-lookup"><span data-stu-id="f71ca-343">Fencing Test</span></span>

<span data-ttu-id="f71ca-344">您可以藉由停用 hello 網路介面上節點 saphanavm1 測試 hello hello 圍欄代理程式的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="f71ca-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="f71ca-345">hello 虛擬機器應該立即取得重新啟動或停止根據您的叢集設定。</span><span class="sxs-lookup"><span data-stu-id="f71ca-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="f71ca-346">如果您設定 hello stonith 動作 toooff，hello 虛擬機器將會停止而且 hello 資源移轉的 toohello 虛擬機器中執行。</span><span class="sxs-lookup"><span data-stu-id="f71ca-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="f71ca-347">如果您設定 AUTOMATED_REGISTER 一旦再次啟動 hello 虛擬機器，hello SAP HANA 資源將會失敗為次要 toostart ="false"。</span><span class="sxs-lookup"><span data-stu-id="f71ca-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="f71ca-348">在此情況下，您需要藉由執行下列命令的 hello 做為次要 tooconfigure hello HANA 執行個體：</span><span class="sxs-lookup"><span data-stu-id="f71ca-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="f71ca-349">測試手動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f71ca-349">Testing a manual failover</span></span>

<span data-ttu-id="f71ca-350">您可以測試的手動容錯移轉節點 saphanavm1 上停止 hello pacemaker 服務。</span><span class="sxs-lookup"><span data-stu-id="f71ca-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="f71ca-351">Hello 容錯移轉之後，您可以重新啟動 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="f71ca-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="f71ca-352">hello saphanavm1 上的 SAP HANA 資源將會失敗 toostart 為次要資料庫設定 AUTOMATED_REGISTER ="false"。</span><span class="sxs-lookup"><span data-stu-id="f71ca-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="f71ca-353">在此情況下，您需要藉由執行下列命令的 hello 做為次要 tooconfigure hello HANA 執行個體：</span><span class="sxs-lookup"><span data-stu-id="f71ca-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="f71ca-354">測試移轉</span><span class="sxs-lookup"><span data-stu-id="f71ca-354">Testing a migration</span></span>

<span data-ttu-id="f71ca-355">您可以藉由執行下列命令的 hello 移轉 hello SAP HANA 主要節點</span><span class="sxs-lookup"><span data-stu-id="f71ca-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="f71ca-356">這應該移轉 hello SAP HANA 主要節點和包含 hello 虛擬 IP 位址 toosaphanavm2 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="f71ca-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="f71ca-357">hello saphanavm1 上的 SAP HANA 資源將會失敗 toostart 為次要資料庫設定 AUTOMATED_REGISTER ="false"。</span><span class="sxs-lookup"><span data-stu-id="f71ca-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="f71ca-358">在此情況下，您需要藉由執行下列命令的 hello 做為次要 tooconfigure hello HANA 執行個體：</span><span class="sxs-lookup"><span data-stu-id="f71ca-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="f71ca-359">hello 移轉會需要一次刪除 toobe 位置條件約束。</span><span class="sxs-lookup"><span data-stu-id="f71ca-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="f71ca-360">您也需要 toocleanup hello hello 次要節點資源狀態</span><span class="sxs-lookup"><span data-stu-id="f71ca-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="f71ca-361">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f71ca-361">Next steps</span></span>
* <span data-ttu-id="f71ca-362">[適用於 SAP 的 Azure 虛擬機器規劃和實作][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="f71ca-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="f71ca-363">[適用於 SAP 的 Azure 虛擬機器部署][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="f71ca-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="f71ca-364">[適用於 SAP 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="f71ca-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="f71ca-365">toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="f71ca-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
