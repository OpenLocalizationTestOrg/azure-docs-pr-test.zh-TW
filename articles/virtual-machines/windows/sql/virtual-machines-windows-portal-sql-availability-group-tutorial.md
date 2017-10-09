---
title: "aaaSQL Server 可用性群組-Azure 虛擬機器-教學課程 |Microsoft 文件"
description: "本教學課程示範如何 toocreate SQL Server Alwayson 可用性群組在 Azure 虛擬機器。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="5b903-103">在 Azure VM 中手動設定 Always On 可用性群組</span><span class="sxs-lookup"><span data-stu-id="5b903-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="5b903-104">本教學課程示範如何 toocreate SQL Server Alwayson 可用性群組在 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b903-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="5b903-105">hello 完整的教學課程與兩個 SQL 伺服器上的資料庫複本建立可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="5b903-106">**估計時間**： 滿足 hello 必要條件之後，會採用約 30 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="5b903-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="5b903-107">hello 圖表說明您在 hello 教學課程中所建置。</span><span class="sxs-lookup"><span data-stu-id="5b903-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="5b903-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b903-109">Prerequisites</span></span>

<span data-ttu-id="5b903-110">hello 教學課程假設您有基本了解 SQL Server Always On 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="5b903-111">如需詳細資訊，請參閱 [AlwaysOn 可用性群組概觀 (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b903-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="5b903-112">hello 下表列出您在開始本教學課程之前，需要 toocomplete hello 必要條件：</span><span class="sxs-lookup"><span data-stu-id="5b903-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="5b903-113">需求</span><span class="sxs-lookup"><span data-stu-id="5b903-113">Requirement</span></span> |<span data-ttu-id="5b903-114">說明</span><span class="sxs-lookup"><span data-stu-id="5b903-114">Description</span></span> |
|----- |----- |----- |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="5b903-116">兩部 SQL Server</span><span class="sxs-lookup"><span data-stu-id="5b903-116">Two SQL Servers</span></span> | <span data-ttu-id="5b903-117">- 在 Azure 可用性設定組中</span><span class="sxs-lookup"><span data-stu-id="5b903-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="5b903-118">- 在單一網域中</span><span class="sxs-lookup"><span data-stu-id="5b903-118">- In a single domain</span></span> <br/> <span data-ttu-id="5b903-119">- 已安裝「容錯移轉叢集」功能</span><span class="sxs-lookup"><span data-stu-id="5b903-119">- With Failover Clustering feature installed</span></span> |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="5b903-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="5b903-121">Windows Server</span></span> | <span data-ttu-id="5b903-122">叢集見證的檔案共用</span><span class="sxs-lookup"><span data-stu-id="5b903-122">File share for cluster witness</span></span> |  
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5b903-124">SQL Server 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="5b903-124">SQL Server service account</span></span> | <span data-ttu-id="5b903-125">網域帳戶</span><span class="sxs-lookup"><span data-stu-id="5b903-125">Domain account</span></span> |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5b903-127">SQL Server Agent 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="5b903-127">SQL Server Agent service account</span></span> | <span data-ttu-id="5b903-128">網域帳戶</span><span class="sxs-lookup"><span data-stu-id="5b903-128">Domain account</span></span> |  
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5b903-130">防火牆連接埠開啟</span><span class="sxs-lookup"><span data-stu-id="5b903-130">Firewall ports open</span></span> | <span data-ttu-id="5b903-131">- SQL Server：**1433** (用於預設執行個體)</span><span class="sxs-lookup"><span data-stu-id="5b903-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="5b903-132">- 資料庫鏡像端點：**5022** 或任何可用的連接埠</span><span class="sxs-lookup"><span data-stu-id="5b903-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="5b903-133">- Azure Load Balancer 探查：**59999** 或任何可用的連接埠</span><span class="sxs-lookup"><span data-stu-id="5b903-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5b903-135">新增容錯移轉叢集功能</span><span class="sxs-lookup"><span data-stu-id="5b903-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="5b903-136">兩部 SQL Server 都需要此功能</span><span class="sxs-lookup"><span data-stu-id="5b903-136">Both SQL Servers require this feature</span></span> |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5b903-138">安裝網域帳戶</span><span class="sxs-lookup"><span data-stu-id="5b903-138">Installation domain account</span></span> | <span data-ttu-id="5b903-139">- 每部 SQL Server 上的本機系統管理員</span><span class="sxs-lookup"><span data-stu-id="5b903-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="5b903-140">- 每個 SQL Server 執行個體之 SQL Server sysadmin 固定伺服器角色的成員</span><span class="sxs-lookup"><span data-stu-id="5b903-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="5b903-141">在開始 hello 教學課程之前，您需要太[完成建立 Azure 虛擬機器中的 Alwayson 可用性群組的必要條件](virtual-machines-windows-portal-sql-availability-group-prereq.md)。</span><span class="sxs-lookup"><span data-stu-id="5b903-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="5b903-142">如果這些必要元件都已完成之後，您可以跳過[建立叢集](#CreateCluster)。</span><span class="sxs-lookup"><span data-stu-id="5b903-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="5b903-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="5b903-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="5b903-144">Hello 完成必要條件之後, hello 第一個步驟是 toocreate Windows Server 容錯移轉叢集，其中包含兩個 SQL 伺服器和見證伺服器。</span><span class="sxs-lookup"><span data-stu-id="5b903-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="5b903-145">RDP toohello 第一個 SQL Server 使用 SQL 伺服器和 hello 見證伺服器的系統管理員的網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b903-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="5b903-146">如果您遵循 hello[先決條件的文件](virtual-machines-windows-portal-sql-availability-group-prereq.md)，建立名為帳戶**CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="5b903-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="5b903-147">請使用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b903-147">Use this account.</span></span>

2. <span data-ttu-id="5b903-148">在 hello**伺服器管理員**儀表板，選取**工具**，然後按一下**容錯移轉叢集管理員**。</span><span class="sxs-lookup"><span data-stu-id="5b903-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="5b903-149">Hello 左窗格中，以滑鼠右鍵按一下**容錯移轉叢集管理員**，然後按一下**建立叢集**。</span><span class="sxs-lookup"><span data-stu-id="5b903-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="5b903-150">![建立叢集](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="5b903-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="5b903-151">在 hello 建立叢集精靈 」 中建立單一節點叢集逐步進行 hello 頁面中的 hello 下表中的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="5b903-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="5b903-152">Page</span><span class="sxs-lookup"><span data-stu-id="5b903-152">Page</span></span> | <span data-ttu-id="5b903-153">設定</span><span class="sxs-lookup"><span data-stu-id="5b903-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="5b903-154">開始之前</span><span class="sxs-lookup"><span data-stu-id="5b903-154">Before You Begin</span></span> |<span data-ttu-id="5b903-155">使用預設值</span><span class="sxs-lookup"><span data-stu-id="5b903-155">Use defaults</span></span> |
   | <span data-ttu-id="5b903-156">選取伺服器</span><span class="sxs-lookup"><span data-stu-id="5b903-156">Select Servers</span></span> |<span data-ttu-id="5b903-157">中的第一個 SQL Server 名稱的型別 hello**輸入伺服器名稱**按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="5b903-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="5b903-158">驗證警告</span><span class="sxs-lookup"><span data-stu-id="5b903-158">Validation Warning</span></span> |<span data-ttu-id="5b903-159">選取**否。 我不需要此群集中，來自 Microsoft 的支援和不想 toorun hello 驗證測試。當我按 [下一步] 時，繼續建立 hello 叢集**。</span><span class="sxs-lookup"><span data-stu-id="5b903-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="5b903-160">用於管理 hello 叢集存取點</span><span class="sxs-lookup"><span data-stu-id="5b903-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="5b903-161">在 [叢集名稱] 中輸入叢集名稱，例如 **SQLAGCluster1**。</span><span class="sxs-lookup"><span data-stu-id="5b903-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="5b903-162">確認</span><span class="sxs-lookup"><span data-stu-id="5b903-162">Confirmation</span></span> |<span data-ttu-id="5b903-163">除非您使用的是儲存空間，否則請使用預設值。</span><span class="sxs-lookup"><span data-stu-id="5b903-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="5b903-164">請參閱本表格後的 hello 附註。</span><span class="sxs-lookup"><span data-stu-id="5b903-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="5b903-165">設定 hello 叢集 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5b903-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="5b903-166">在**容錯移轉叢集管理員**，向下捲動太**叢集核心資源**展開 hello 叢集詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5b903-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="5b903-167">您應該會看到這兩個 hello**名稱**和 hello **IP 位址**hello 中的資源**失敗**狀態。</span><span class="sxs-lookup"><span data-stu-id="5b903-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="5b903-168">hello IP 位址資源無法上線 hello 叢集指派 hello 因為 IP 位址為 hello 機器本身相同，因此它是重複的位址。</span><span class="sxs-lookup"><span data-stu-id="5b903-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="5b903-169">以滑鼠右鍵按一下失敗的 hello **IP 位址**資源，然後再按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="5b903-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![叢集屬性](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="5b903-171">選取**靜態 IP 位址**並指定從 hello SQL Server 會處於 hello 位址 文字方塊中的子網路的可用位址。</span><span class="sxs-lookup"><span data-stu-id="5b903-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="5b903-172">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="5b903-173">在 hello**叢集核心資源**區段中以滑鼠右鍵按一下叢集名稱，然後按一下**上線**。</span><span class="sxs-lookup"><span data-stu-id="5b903-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="5b903-174">然後等待兩個資源上線。</span><span class="sxs-lookup"><span data-stu-id="5b903-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="5b903-175">當 hello 叢集名稱資源上線時，它會以新的 AD 電腦帳戶更新 hello DC 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5b903-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="5b903-176">使用這個 AD 帳戶 toorun hello 稍後可用性群組的叢集服務。</span><span class="sxs-lookup"><span data-stu-id="5b903-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="5b903-177"><a name="addNode"></a>新增 hello 其他 SQL Server toocluster</span><span class="sxs-lookup"><span data-stu-id="5b903-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="5b903-178">新增 hello 其他 SQL Server toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b903-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="5b903-179">Hello 瀏覽器樹狀目錄中，以滑鼠右鍵按一下 hello 叢集，然後按一下**加入節點**。</span><span class="sxs-lookup"><span data-stu-id="5b903-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![新增節點 toohello 叢集](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="5b903-181">在 hello**新增節點精靈**，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="5b903-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="5b903-182">在 hello**選取伺服器**頁面上，新增 hello 第二個 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5b903-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="5b903-183">中的型別 hello 伺服器名稱**輸入伺服器名稱**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="5b903-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="5b903-184">完成之後，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5b903-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="5b903-185">在 hello**驗證警告**頁面上，按一下**否**（在生產案例中您應該執行 hello 驗證測試）。</span><span class="sxs-lookup"><span data-stu-id="5b903-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="5b903-186">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="5b903-187">在 hello**確認**頁面上，如果您使用儲存空間，清除 hello 核取方塊標示為**新增所有合格的存放裝置 toohello 叢集。**</span><span class="sxs-lookup"><span data-stu-id="5b903-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![新增節點確認](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="5b903-189">如果您使用儲存空間，且未取消選取**新增所有合格的存放裝置 toohello 叢集**，Windows hello 叢集程序期間中斷 hello 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="5b903-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="5b903-190">如此一來，它們沒有出現在 磁碟管理員 或 檔案總管，直到從 hello 叢集中移除 hello 儲存空間，並使用 PowerShell 將其重新附加。</span><span class="sxs-lookup"><span data-stu-id="5b903-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="5b903-191">儲存空間將 toostorage 集區中的多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="5b903-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="5b903-192">如需詳細資訊，請參閱[儲存空間](https://technet.microsoft.com/library/hh831739)。</span><span class="sxs-lookup"><span data-stu-id="5b903-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="5b903-193">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-193">Click **Next**.</span></span>

1. <span data-ttu-id="5b903-194">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-194">Click **Finish**.</span></span>

   <span data-ttu-id="5b903-195">容錯移轉叢集管理員 會顯示您的叢集有新的節點，並列出在 hello**節點**容器。</span><span class="sxs-lookup"><span data-stu-id="5b903-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="5b903-196">登出 hello 遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="5b903-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="5b903-197">新增叢集仲裁檔案共用</span><span class="sxs-lookup"><span data-stu-id="5b903-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="5b903-198">在此範例中 hello Windows 叢集會使用檔案共用 toocreate 叢集仲裁。</span><span class="sxs-lookup"><span data-stu-id="5b903-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="5b903-199">本教學課程使用「節點與檔案共用多數」仲裁。</span><span class="sxs-lookup"><span data-stu-id="5b903-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="5b903-200">如需詳細資訊，請參閱[了解容錯移轉叢集中的仲裁設定](http://technet.microsoft.com/library/cc731739.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b903-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="5b903-201">使用遠端桌面工作階段連線 toohello 檔案共用見證成員伺服器。</span><span class="sxs-lookup"><span data-stu-id="5b903-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="5b903-202">在 [伺服器管理員] 上，按一下 [工具]。</span><span class="sxs-lookup"><span data-stu-id="5b903-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="5b903-203">開啟 [電腦管理]。</span><span class="sxs-lookup"><span data-stu-id="5b903-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="5b903-204">按一下 [共用資料夾]。</span><span class="sxs-lookup"><span data-stu-id="5b903-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="5b903-205">在 共用 上按一下滑鼠右鍵，然後按一下新增共用。</span><span class="sxs-lookup"><span data-stu-id="5b903-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="5b903-207">使用**建立共用資料夾精靈**toocreate 共用。</span><span class="sxs-lookup"><span data-stu-id="5b903-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="5b903-208">在**資料夾路徑**，按一下 **瀏覽**並找出或建立 hello 共用資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="5b903-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="5b903-209">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-209">Click **Next**.</span></span>

1. <span data-ttu-id="5b903-210">在**名稱、 描述和設定**確認 hello 共用名稱和路徑。</span><span class="sxs-lookup"><span data-stu-id="5b903-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="5b903-211">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-211">Click **Next**.</span></span>

1. <span data-ttu-id="5b903-212">在 [共用資料夾權限] 上，設定 [自訂權限]。</span><span class="sxs-lookup"><span data-stu-id="5b903-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="5b903-213">按一下 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="5b903-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="5b903-214">在 [自訂權限] 上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5b903-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="5b903-215">請確定該 hello 使用帳戶 toocreate hello 叢集中擁有完整控制權。</span><span class="sxs-lookup"><span data-stu-id="5b903-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="5b903-217">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-217">Click **OK**.</span></span>

1. <span data-ttu-id="5b903-218">在 [共用資料夾權限] 中，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5b903-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="5b903-219">再次按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5b903-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="5b903-220">登出伺服器 hello</span><span class="sxs-lookup"><span data-stu-id="5b903-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="5b903-221">設定叢集仲裁</span><span class="sxs-lookup"><span data-stu-id="5b903-221">Configure cluster quorum</span></span>

<span data-ttu-id="5b903-222">接下來，設定 hello 叢集仲裁。</span><span class="sxs-lookup"><span data-stu-id="5b903-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="5b903-223">使用遠端桌面連線 toohello 第一個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="5b903-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="5b903-224">在**容錯移轉叢集管理員**hello 叢集上按一下滑鼠右鍵，指向太**其他動作**，然後按一下**設定叢集仲裁設定...**.</span><span class="sxs-lookup"><span data-stu-id="5b903-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="5b903-226">在「設定叢集仲裁精靈」中，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5b903-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="5b903-227">在**選取仲裁設定選項**，選擇**選取 hello 仲裁見證**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5b903-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="5b903-228">在 [選取仲裁見證] 上，按一下 [設定檔案共用見證]。</span><span class="sxs-lookup"><span data-stu-id="5b903-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="5b903-229">Windows Server 2016 支援雲端見證。</span><span class="sxs-lookup"><span data-stu-id="5b903-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="5b903-230">如果您選擇此類型的見證，就不需要檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="5b903-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="5b903-231">如需詳細資訊，請參閱[為容錯移轉叢集部署雲端見證 (Deploy a cloud witness for a Failover Cluster)](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)。</span><span class="sxs-lookup"><span data-stu-id="5b903-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="5b903-232">本教學課程使用檔案共用見證，這是舊版作業系統所支援的類型。</span><span class="sxs-lookup"><span data-stu-id="5b903-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="5b903-233">在**設定檔案共用見證**，您所建立的 hello 共用的型別 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="5b903-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="5b903-234">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-234">Click **Next**.</span></span>

1. <span data-ttu-id="5b903-235">在確認 hello 設定**確認**。</span><span class="sxs-lookup"><span data-stu-id="5b903-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="5b903-236">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-236">Click **Next**.</span></span>

1. <span data-ttu-id="5b903-237">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-237">Click **Finish**.</span></span>

<span data-ttu-id="5b903-238">hello 叢集核心資源設定檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="5b903-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="5b903-239">啟用可用性群組</span><span class="sxs-lookup"><span data-stu-id="5b903-239">Enable Availability Groups</span></span>

<span data-ttu-id="5b903-240">接下來，啟用 hello **AlwaysOn 可用性群組**功能。</span><span class="sxs-lookup"><span data-stu-id="5b903-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="5b903-241">在兩部 SQL Server 上執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5b903-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="5b903-242">從 hello**啟動**畫面上，啟動**SQL Server 組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="5b903-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="5b903-243">在 hello 瀏覽器樹狀目錄中，按一下  **SQL Server 服務**，然後以滑鼠右鍵按一下 hello **SQL Server (MSSQLSERVER)**服務，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="5b903-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="5b903-244">按一下 hello **AlwaysOn 高可用性**索引標籤，然後選取**啟用 AlwaysOn 可用性群組**、，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5b903-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![啟用 AlwaysOn 可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="5b903-246">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-246">Click **Apply**.</span></span> <span data-ttu-id="5b903-247">按一下**確定**hello 快顯對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="5b903-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="5b903-248">重新啟動 hello SQL Server 服務。</span><span class="sxs-lookup"><span data-stu-id="5b903-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="5b903-249">上重複這些步驟 hello 其他 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5b903-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="5b903-250">Hello 上建立資料庫第一次的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="5b903-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="5b903-251">第一個 SQL Server 的網域帳戶也就是啟動 hello RDP 檔案 toohello 屬於 sysadmin 固定伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="5b903-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="5b903-252">開啟 SQL Server Management Studio 並連接 toohello 第一個 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5b903-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="5b903-253">在 物件總管 中，於 資料庫 上按一下滑鼠右鍵，然後按一下新增資料庫。</span><span class="sxs-lookup"><span data-stu-id="5b903-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="5b903-254">在 [資料庫名稱] 中，輸入 **MyDB1**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5b903-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="5b903-255"><a name="backupshare"></a> 建立備份共用</span><span class="sxs-lookup"><span data-stu-id="5b903-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="5b903-256">在 hello 中的第一個 SQL Server**伺服器管理員**，按一下 **工具**。</span><span class="sxs-lookup"><span data-stu-id="5b903-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="5b903-257">開啟 [電腦管理]。</span><span class="sxs-lookup"><span data-stu-id="5b903-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="5b903-258">按一下 [共用資料夾]。</span><span class="sxs-lookup"><span data-stu-id="5b903-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="5b903-259">在 共用 上按一下滑鼠右鍵，然後按一下新增共用。</span><span class="sxs-lookup"><span data-stu-id="5b903-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="5b903-261">使用**建立共用資料夾精靈**toocreate 共用。</span><span class="sxs-lookup"><span data-stu-id="5b903-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="5b903-262">在**資料夾路徑**，按一下 **瀏覽**並找出或建立 hello 資料庫的備份共用資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="5b903-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="5b903-263">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-263">Click **Next**.</span></span>

1. <span data-ttu-id="5b903-264">在**名稱、 描述和設定**確認 hello 共用名稱和路徑。</span><span class="sxs-lookup"><span data-stu-id="5b903-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="5b903-265">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-265">Click **Next**.</span></span>

1. <span data-ttu-id="5b903-266">在 [共用資料夾權限] 上，設定 [自訂權限]。</span><span class="sxs-lookup"><span data-stu-id="5b903-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="5b903-267">按一下 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="5b903-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="5b903-268">在 [自訂權限] 上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5b903-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="5b903-269">請確定這兩部伺服器的 hello SQL Server 和 SQL Server Agent 服務帳戶具有完整控制權。</span><span class="sxs-lookup"><span data-stu-id="5b903-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="5b903-271">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-271">Click **OK**.</span></span>

1. <span data-ttu-id="5b903-272">在 [共用資料夾權限] 中，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5b903-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="5b903-273">再次按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5b903-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="5b903-274">進行完整備份的 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="5b903-274">Take a full backup of hello database</span></span>

<span data-ttu-id="5b903-275">您需要 tooback hello 新資料庫 tooinitialize hello 記錄鏈結。</span><span class="sxs-lookup"><span data-stu-id="5b903-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="5b903-276">如果您不會取得 hello 新資料庫的備份，則它不包含可用性群組中。</span><span class="sxs-lookup"><span data-stu-id="5b903-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="5b903-277">在**物件總管] 中**hello 資料庫上按一下滑鼠右鍵，指向太**工作...**，按一下 [ **Back Up**。</span><span class="sxs-lookup"><span data-stu-id="5b903-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="5b903-278">按一下**確定**tootake 完整備份 toohello 預設備份位置。</span><span class="sxs-lookup"><span data-stu-id="5b903-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="5b903-279">建立 hello 可用性群組</span><span class="sxs-lookup"><span data-stu-id="5b903-279">Create hello Availability Group</span></span>
<span data-ttu-id="5b903-280">現在您已經準備就緒 tooconfigure 可用性群組使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b903-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="5b903-281">Hello 上建立資料庫第一次的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5b903-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="5b903-282">完整備份和交易記錄備份的 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="5b903-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="5b903-283">完整的還原 hello 和以 hello 的第二個 SQL Server 記錄檔備份 toohello **NORECOVERY**選項</span><span class="sxs-lookup"><span data-stu-id="5b903-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="5b903-284">建立 hello 可用性群組 (**AG1**) 同步認可、 自動容錯移轉，與可讀取次要複本</span><span class="sxs-lookup"><span data-stu-id="5b903-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="5b903-285">建立 hello 可用性群組：</span><span class="sxs-lookup"><span data-stu-id="5b903-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="5b903-286">遠端桌面工作階段 toohello 上第一個 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5b903-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="5b903-287">在 SSMS 的 物件總管 中，於 AlwaysOn 高可用性 上按一下滑鼠右鍵，然後按一下新增可用性群組精靈。</span><span class="sxs-lookup"><span data-stu-id="5b903-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![啟動新增可用性群組精靈](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="5b903-289">在 hello**簡介**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5b903-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="5b903-290">在 hello**指定可用性群組名稱**頁面上，輸入 hello 可用性群組的名稱，例如**AG1**，請在**可用性群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="5b903-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="5b903-291">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-291">Click **Next**.</span></span>

    ![新增 AG 精靈：指定 AG 名稱](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="5b903-293">在 hello**選取資料庫**頁面上，選取您的資料庫，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5b903-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5b903-294">由於您已執行至少一個完整備份 hello 預定的主要複本上，hello 資料庫會符合可用性群組的 hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="5b903-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![新增 AG 精靈：選取資料庫](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="5b903-296">在 hello**指定複本**頁面上，按一下**將複本加入**。</span><span class="sxs-lookup"><span data-stu-id="5b903-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![新增 AG 精靈：指定複本](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="5b903-298">hello**連接 tooServer**的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5b903-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="5b903-299">型別中的 hello 第二部伺服器 hello 名稱**伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="5b903-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="5b903-300">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="5b903-300">Click **Connect**.</span></span>

   <span data-ttu-id="5b903-301">在 [hello**指定複本**] 頁面上，您現在應該會看到 hello 中所列的第二部伺服器**可用性複本**。</span><span class="sxs-lookup"><span data-stu-id="5b903-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="5b903-302">Hello 複本的設定，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5b903-302">Configure hello replicas as follows.</span></span>

   ![新增 AG 精靈：指定複本 (完成)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="5b903-304">按一下**端點**toosee hello 資料庫鏡像端點，這個可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="5b903-305">使用 hello 相同連接埠，使用當您設定 hello[資料庫鏡像端點的防火牆規則](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)。</span><span class="sxs-lookup"><span data-stu-id="5b903-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![新增 AG 精靈：選取初始資料同步處理](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="5b903-307">在 hello**選取初始資料同步處理**頁面上，選取**完整**和指定的共用的網路位置。</span><span class="sxs-lookup"><span data-stu-id="5b903-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="5b903-308">Hello 位置，請使用 hello[您所建立的備份共用](#backupshare)。</span><span class="sxs-lookup"><span data-stu-id="5b903-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="5b903-309">在 hello 範例中，**\\\\\<第一個 SQL Server\>\Backup\**。</span><span class="sxs-lookup"><span data-stu-id="5b903-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="5b903-310">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5b903-311">完整同步處理會採用 hello hello 第一個執行個體的 SQL Server 資料庫的完整備份，並將它還原 toohello 第二個執行個體。</span><span class="sxs-lookup"><span data-stu-id="5b903-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="5b903-312">就大型資料庫而言，不建議進行完整同步處理，因為可能費時很久。</span><span class="sxs-lookup"><span data-stu-id="5b903-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="5b903-313">您可以減少這個時間手動建立 hello 資料庫的備份及還原與`NO RECOVERY`。</span><span class="sxs-lookup"><span data-stu-id="5b903-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="5b903-314">如果使用已還原 hello 資料庫`NO RECOVERY`hello 上然後再設定 hello 可用性群組的第二個 SQL Server 中，選擇**僅聯結**。</span><span class="sxs-lookup"><span data-stu-id="5b903-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="5b903-315">如果您想 tootake hello 備份設定 hello 可用性群組之後，請選擇**略過初始資料同步處理**。</span><span class="sxs-lookup"><span data-stu-id="5b903-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![新增 AG 精靈：選取初始資料同步處理](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="5b903-317">在 hello**驗證**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5b903-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="5b903-318">此頁面應看起來類似 toohello 下列映像：</span><span class="sxs-lookup"><span data-stu-id="5b903-318">This page should look similar toohello following image:</span></span>

    ![新增 AG 精靈：驗證](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="5b903-320">沒有 hello 接聽程式設定的警告，因為您尚未設定可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5b903-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="5b903-321">因為您可以在 Azure 虛擬機器上建立 hello 接聽程式來建立 hello Azure 負載平衡器之後，您可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="5b903-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="5b903-322">在 hello**摘要**頁面上，按一下**完成**，然後稍候 hello 精靈設定 hello 新增可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="5b903-323">在 [hello**進度**] 頁面上，您可以按一下**更多詳細資料**tooview hello 詳細進度。</span><span class="sxs-lookup"><span data-stu-id="5b903-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="5b903-324">Hello 精靈完成時，檢查 hello**結果**hello 可用性群組的頁面 tooverify 已成功建立。</span><span class="sxs-lookup"><span data-stu-id="5b903-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![新增 AG 精靈：結果](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="5b903-326">按一下**關閉**tooexit hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="5b903-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="5b903-327">核取 hello 可用性群組</span><span class="sxs-lookup"><span data-stu-id="5b903-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="5b903-328">在 [物件總管] 中，展開 [AlwaysOn 高可用性]，然後展開 [可用性群組]。</span><span class="sxs-lookup"><span data-stu-id="5b903-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="5b903-329">您現在應該會看到 hello 這個容器中的新可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="5b903-330">Hello 可用性群組上按一下滑鼠右鍵，然後按一下**顯示儀表板**。</span><span class="sxs-lookup"><span data-stu-id="5b903-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![顯示 AG 儀表板](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="5b903-332">您**AlwaysOn 儀表板**看起來應該類似 toothis。</span><span class="sxs-lookup"><span data-stu-id="5b903-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![AG 儀表板](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="5b903-334">您可以看到 hello 複本，每個複本和 hello 的同步處理狀態的 hello 容錯移轉模式。</span><span class="sxs-lookup"><span data-stu-id="5b903-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="5b903-335">在 [容錯移轉叢集管理員] 中，按一下您的叢集。</span><span class="sxs-lookup"><span data-stu-id="5b903-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="5b903-336">選取 [角色]。</span><span class="sxs-lookup"><span data-stu-id="5b903-336">Select **Roles**.</span></span> <span data-ttu-id="5b903-337">您所使用的 hello 可用性群組名稱是 hello 叢集上的角色。</span><span class="sxs-lookup"><span data-stu-id="5b903-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="5b903-338">該「可用性群組」並沒有適用於用戶端連線的 IP 位址，因為您並未設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5b903-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="5b903-339">在您建立 Azure 負載平衡器之後，您將設定 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5b903-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![容錯移轉叢集管理員中的 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="5b903-341">請勿嘗試 toofail 透過 hello 容錯移轉叢集管理員中的 hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="5b903-342">所有容錯移轉作業都應在 SSMS 的 **AlwaysOn 儀表板** 中執行。</span><span class="sxs-lookup"><span data-stu-id="5b903-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="5b903-343">如需詳細資訊，請參閱[限制使用 hello 與可用性群組容錯移轉叢集管理員](https://msdn.microsoft.com/library/ff929171.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b903-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="5b903-344">此時，您擁有一個在兩個 SQL Server 執行個體上都有複本的「可用性群組」。</span><span class="sxs-lookup"><span data-stu-id="5b903-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="5b903-345">您可以在執行個體之間移動 hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="5b903-346">您無法連線 toohello 可用性群組尚未因為您沒有接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5b903-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="5b903-347">在 Azure 虛擬機器，hello 接聽程式都需要負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b903-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="5b903-348">hello 下一個步驟是在 Azure 中的 toocreate hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b903-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="5b903-349">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5b903-349">Create an Azure load balancer</span></span>

<span data-ttu-id="5b903-350">在 Azure 虛擬機器上，「SQL Server 可用性群組」需要負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b903-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="5b903-351">hello 負載平衡器會保存 hello hello 可用性群組接聽程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b903-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="5b903-352">本節摘要說明如何 toocreate hello 負載平衡器 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5b903-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="5b903-353">在 hello Azure 入口網站，移 toohello 資源群組，其中是您的 SQL 伺服器，而按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="5b903-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="5b903-354">搜尋 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="5b903-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="5b903-355">選擇 Microsoft 所發行的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b903-355">Choose hello load balancer published by Microsoft.</span></span>

   ![容錯移轉叢集管理員中的 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="5b903-357">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5b903-357">Click **Create**.</span></span>
3. <span data-ttu-id="5b903-358">設定下列參數 hello 負載平衡器的 hello。</span><span class="sxs-lookup"><span data-stu-id="5b903-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="5b903-359">設定</span><span class="sxs-lookup"><span data-stu-id="5b903-359">Setting</span></span> | <span data-ttu-id="5b903-360">欄位</span><span class="sxs-lookup"><span data-stu-id="5b903-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="5b903-361">**名稱**</span><span class="sxs-lookup"><span data-stu-id="5b903-361">**Name**</span></span> |<span data-ttu-id="5b903-362">使用文字名稱 hello 負載平衡器，例如**sqlLB**。</span><span class="sxs-lookup"><span data-stu-id="5b903-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="5b903-363">**類型**</span><span class="sxs-lookup"><span data-stu-id="5b903-363">**Type**</span></span> |<span data-ttu-id="5b903-364">內部</span><span class="sxs-lookup"><span data-stu-id="5b903-364">Internal</span></span> |
   | <span data-ttu-id="5b903-365">**虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="5b903-365">**Virtual network**</span></span> |<span data-ttu-id="5b903-366">使用 hello hello Azure 虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="5b903-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="5b903-367">**子網路**</span><span class="sxs-lookup"><span data-stu-id="5b903-367">**Subnet**</span></span> |<span data-ttu-id="5b903-368">正在使用 hello 名稱 hello hello 虛擬機器的子網路。</span><span class="sxs-lookup"><span data-stu-id="5b903-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="5b903-369">**IP 位址指派**</span><span class="sxs-lookup"><span data-stu-id="5b903-369">**IP address assignment**</span></span> |<span data-ttu-id="5b903-370">靜態</span><span class="sxs-lookup"><span data-stu-id="5b903-370">Static</span></span> |
   | <span data-ttu-id="5b903-371">**IP 位址**</span><span class="sxs-lookup"><span data-stu-id="5b903-371">**IP address**</span></span> |<span data-ttu-id="5b903-372">使用來自子網路的可用位址。</span><span class="sxs-lookup"><span data-stu-id="5b903-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="5b903-373">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="5b903-373">**Subscription**</span></span> |<span data-ttu-id="5b903-374">使用 hello 相同訂用帳戶為 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b903-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="5b903-375">**位置**</span><span class="sxs-lookup"><span data-stu-id="5b903-375">**Location**</span></span> |<span data-ttu-id="5b903-376">使用 hello 相同 hello 虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="5b903-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="5b903-377">hello Azure 入口網站的刀鋒視窗看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="5b903-377">hello Azure portal blade should look like this:</span></span>

   ![建立負載平衡器](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="5b903-379">按一下**建立**，toocreate hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b903-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="5b903-380">tooconfigure hello 負載平衡器，您需要 toocreate 後端集區、 探查，以及設定 hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="5b903-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="5b903-381">執行下列 hello Azure 入口網站中的操作。</span><span class="sxs-lookup"><span data-stu-id="5b903-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="5b903-382">新增後端集區</span><span class="sxs-lookup"><span data-stu-id="5b903-382">Add backend pool</span></span>

1. <span data-ttu-id="5b903-383">在 hello Azure 入口網站，移 tooyour 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5b903-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="5b903-384">您可能需要 toorefresh hello 檢視 toosee hello 新建立的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b903-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![在資源群組中尋找負載平衡器](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="5b903-386">按一下 hello 負載平衡器中，按一下**後端集區**，然後按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="5b903-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="5b903-387">設定 hello 後端集區，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5b903-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="5b903-388">設定</span><span class="sxs-lookup"><span data-stu-id="5b903-388">Setting</span></span> | <span data-ttu-id="5b903-389">說明</span><span class="sxs-lookup"><span data-stu-id="5b903-389">Description</span></span> | <span data-ttu-id="5b903-390">範例</span><span class="sxs-lookup"><span data-stu-id="5b903-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5b903-391">**名稱**</span><span class="sxs-lookup"><span data-stu-id="5b903-391">**Name**</span></span> | <span data-ttu-id="5b903-392">輸入文字名稱</span><span class="sxs-lookup"><span data-stu-id="5b903-392">Type a text name</span></span> | <span data-ttu-id="5b903-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="5b903-393">SQLLBBE</span></span>
   | <span data-ttu-id="5b903-394">**與下列產生關聯**</span><span class="sxs-lookup"><span data-stu-id="5b903-394">**Associated to**</span></span> | <span data-ttu-id="5b903-395">從清單中挑選</span><span class="sxs-lookup"><span data-stu-id="5b903-395">Pick from list</span></span> | <span data-ttu-id="5b903-396">可用性集合</span><span class="sxs-lookup"><span data-stu-id="5b903-396">Availability set</span></span>
   | <span data-ttu-id="5b903-397">**可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="5b903-397">**Availability set**</span></span> | <span data-ttu-id="5b903-398">使用您的 SQL Server Vm 位於 hello 可用性設定組名稱</span><span class="sxs-lookup"><span data-stu-id="5b903-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="5b903-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="5b903-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="5b903-400">**虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="5b903-400">**Virtual machines**</span></span> |<span data-ttu-id="5b903-401">hello 兩個 Azure SQL Server VM 名稱</span><span class="sxs-lookup"><span data-stu-id="5b903-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="5b903-402">sqlserver-0、sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="5b903-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="5b903-403">輸入 hello hello 後端集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="5b903-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="5b903-404">按一下 [+ 新增虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="5b903-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="5b903-405">Hello 可用性集合時，您可以選擇 hello 可用性設定組的 SQL 伺服器位於該 hello。</span><span class="sxs-lookup"><span data-stu-id="5b903-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="5b903-406">針對虛擬機器，包括這兩個 SQL 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="5b903-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="5b903-407">請勿包含 hello 檔案共用見證伺服器。</span><span class="sxs-lookup"><span data-stu-id="5b903-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="5b903-408">按一下**確定**toocreate hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="5b903-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="5b903-409">集 hello 探查</span><span class="sxs-lookup"><span data-stu-id="5b903-409">Set hello probe</span></span>

1. <span data-ttu-id="5b903-410">按一下 hello 負載平衡器中，按一下**健全狀況探查**，然後按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="5b903-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="5b903-411">設定 hello 健全狀況探查，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5b903-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="5b903-412">設定</span><span class="sxs-lookup"><span data-stu-id="5b903-412">Setting</span></span> | <span data-ttu-id="5b903-413">說明</span><span class="sxs-lookup"><span data-stu-id="5b903-413">Description</span></span> | <span data-ttu-id="5b903-414">範例</span><span class="sxs-lookup"><span data-stu-id="5b903-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5b903-415">**名稱**</span><span class="sxs-lookup"><span data-stu-id="5b903-415">**Name**</span></span> | <span data-ttu-id="5b903-416">文字</span><span class="sxs-lookup"><span data-stu-id="5b903-416">Text</span></span> | <span data-ttu-id="5b903-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5b903-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="5b903-418">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="5b903-418">**Protocol**</span></span> | <span data-ttu-id="5b903-419">選擇 [TCP]</span><span class="sxs-lookup"><span data-stu-id="5b903-419">Choose TCP</span></span> | <span data-ttu-id="5b903-420">TCP</span><span class="sxs-lookup"><span data-stu-id="5b903-420">TCP</span></span> |
   | <span data-ttu-id="5b903-421">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="5b903-421">**Port**</span></span> | <span data-ttu-id="5b903-422">任何未使用的連接埠</span><span class="sxs-lookup"><span data-stu-id="5b903-422">Any unused port</span></span> | <span data-ttu-id="5b903-423">59999</span><span class="sxs-lookup"><span data-stu-id="5b903-423">59999</span></span> |
   | <span data-ttu-id="5b903-424">**間隔**</span><span class="sxs-lookup"><span data-stu-id="5b903-424">**Interval**</span></span>  | <span data-ttu-id="5b903-425">hello 一段時間之間探查嘗試以秒為單位</span><span class="sxs-lookup"><span data-stu-id="5b903-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="5b903-426">5</span><span class="sxs-lookup"><span data-stu-id="5b903-426">5</span></span> |
   | <span data-ttu-id="5b903-427">**狀況不良臨界值**</span><span class="sxs-lookup"><span data-stu-id="5b903-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="5b903-428">hello 一定會被視為狀況不良的虛擬機器 toobe 進行連續探查失敗數目</span><span class="sxs-lookup"><span data-stu-id="5b903-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="5b903-429">2</span><span class="sxs-lookup"><span data-stu-id="5b903-429">2</span></span> |

1. <span data-ttu-id="5b903-430">按一下**確定**tooset hello 健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="5b903-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="5b903-431">設定 hello 負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="5b903-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="5b903-432">按一下 hello 負載平衡器中，按一下**負載平衡規則**，然後按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="5b903-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="5b903-433">設定 hello 負載平衡規則，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5b903-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="5b903-434">設定</span><span class="sxs-lookup"><span data-stu-id="5b903-434">Setting</span></span> | <span data-ttu-id="5b903-435">說明</span><span class="sxs-lookup"><span data-stu-id="5b903-435">Description</span></span> | <span data-ttu-id="5b903-436">範例</span><span class="sxs-lookup"><span data-stu-id="5b903-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5b903-437">**名稱**</span><span class="sxs-lookup"><span data-stu-id="5b903-437">**Name**</span></span> | <span data-ttu-id="5b903-438">文字</span><span class="sxs-lookup"><span data-stu-id="5b903-438">Text</span></span> | <span data-ttu-id="5b903-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="5b903-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="5b903-440">**前端 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="5b903-440">**Frontend IP address**</span></span> | <span data-ttu-id="5b903-441">選擇一個位址</span><span class="sxs-lookup"><span data-stu-id="5b903-441">Choose an address</span></span> |<span data-ttu-id="5b903-442">使用建立 hello 負載平衡器時的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="5b903-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="5b903-443">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="5b903-443">**Protocol**</span></span> | <span data-ttu-id="5b903-444">選擇 [TCP]</span><span class="sxs-lookup"><span data-stu-id="5b903-444">Choose TCP</span></span> |<span data-ttu-id="5b903-445">TCP</span><span class="sxs-lookup"><span data-stu-id="5b903-445">TCP</span></span> |
   | <span data-ttu-id="5b903-446">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="5b903-446">**Port**</span></span> | <span data-ttu-id="5b903-447">Hello SQL Server 執行個體使用 hello 連接埠</span><span class="sxs-lookup"><span data-stu-id="5b903-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="5b903-448">1433</span><span class="sxs-lookup"><span data-stu-id="5b903-448">1433</span></span> |
   | <span data-ttu-id="5b903-449">**後端連接埠**</span><span class="sxs-lookup"><span data-stu-id="5b903-449">**Backend Port**</span></span> | <span data-ttu-id="5b903-450">如果已為伺服器直接回傳設定「浮動 IP」，便不會使用此欄位。</span><span class="sxs-lookup"><span data-stu-id="5b903-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="5b903-451">1433</span><span class="sxs-lookup"><span data-stu-id="5b903-451">1433</span></span> |
   | <span data-ttu-id="5b903-452">**探查**</span><span class="sxs-lookup"><span data-stu-id="5b903-452">**Probe**</span></span> |<span data-ttu-id="5b903-453">您指定 hello 探查的 hello 名稱</span><span class="sxs-lookup"><span data-stu-id="5b903-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="5b903-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5b903-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="5b903-455">**工作階段持續性**</span><span class="sxs-lookup"><span data-stu-id="5b903-455">**Session Persistence**</span></span> | <span data-ttu-id="5b903-456">下拉式清單</span><span class="sxs-lookup"><span data-stu-id="5b903-456">Drop down list</span></span> | <span data-ttu-id="5b903-457">**None**</span><span class="sxs-lookup"><span data-stu-id="5b903-457">**None**</span></span> |
   | <span data-ttu-id="5b903-458">**閒置逾時**</span><span class="sxs-lookup"><span data-stu-id="5b903-458">**Idle Timeout**</span></span> | <span data-ttu-id="5b903-459">開啟 TCP 連線的分鐘 tookeep</span><span class="sxs-lookup"><span data-stu-id="5b903-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="5b903-460">4</span><span class="sxs-lookup"><span data-stu-id="5b903-460">4</span></span> |
   | <span data-ttu-id="5b903-461">**浮動 IP (伺服器直接回傳)**</span><span class="sxs-lookup"><span data-stu-id="5b903-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="5b903-462">已啟用</span><span class="sxs-lookup"><span data-stu-id="5b903-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="5b903-463">伺服器直接回傳是在建立時設定。</span><span class="sxs-lookup"><span data-stu-id="5b903-463">Direct server return is set during creation.</span></span> <span data-ttu-id="5b903-464">無法予以變更。</span><span class="sxs-lookup"><span data-stu-id="5b903-464">It cannot be changed.</span></span>

1. <span data-ttu-id="5b903-465">按一下**確定**tooset hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="5b903-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="5b903-466"><a name="configure-listener"></a>Hello 接聽程式設定</span><span class="sxs-lookup"><span data-stu-id="5b903-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="5b903-467">下一件事 toodo hello 是 tooconfigure hello 容錯移轉叢集上的可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5b903-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5b903-468">本教學課程會示範如何 toocreate 單一接聽程式-一個 ILB 的 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="5b903-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="5b903-469">toocreate 一或多個接聽程式使用一或多個 IP 位址，請參閱[建立可用性群組接聽程式與負載平衡器 |Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5b903-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="5b903-470">設定接聽程式連接埠</span><span class="sxs-lookup"><span data-stu-id="5b903-470">Set listener port</span></span>

<span data-ttu-id="5b903-471">在 SQL Server Management Studio 中，設定 hello 接聽程式通訊埠。</span><span class="sxs-lookup"><span data-stu-id="5b903-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="5b903-472">啟動 SQL Server Management Studio 並連接 toohello 主要複本。</span><span class="sxs-lookup"><span data-stu-id="5b903-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="5b903-473">瀏覽過**AlwaysOn 高可用性** | **可用性群組** | **可用性群組接聽程式**。</span><span class="sxs-lookup"><span data-stu-id="5b903-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="5b903-474">您現在應該會看到您在建立容錯移轉叢集管理員 中的 hello 接聽程式名稱。</span><span class="sxs-lookup"><span data-stu-id="5b903-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="5b903-475">以滑鼠右鍵按一下 hello 接聽程式名稱，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="5b903-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="5b903-476">在 hello**連接埠**方塊中，使用 hello $EndpointPort 您稍早所指定 hello hello 可用性群組接聽程式的通訊埠編號 （1433年是 hello 預設值），然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="5b903-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="5b903-477">現在，您在以 Resource Manager 模式執行的 Azure 虛擬機器中，已有一個「SQL Server 可用性群組」。</span><span class="sxs-lookup"><span data-stu-id="5b903-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="5b903-478">測試連接 toolistener</span><span class="sxs-lookup"><span data-stu-id="5b903-478">Test connection toolistener</span></span>

<span data-ttu-id="5b903-479">tootest hello 連線：</span><span class="sxs-lookup"><span data-stu-id="5b903-479">tootest hello connection:</span></span>

1. <span data-ttu-id="5b903-480">RDP tooa hello 中的 SQL Server 相同虛擬網路，但不會無法自己 hello 複本。</span><span class="sxs-lookup"><span data-stu-id="5b903-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="5b903-481">您可以使用 hello hello 叢集中的其他 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5b903-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="5b903-482">使用**sqlcmd**公用程式 tootest hello 連線。</span><span class="sxs-lookup"><span data-stu-id="5b903-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="5b903-483">例如，下列指令碼的 hello 建立**sqlcmd**透過 hello 接聽程式使用 Windows 驗證連接 toohello 主要複本：</span><span class="sxs-lookup"><span data-stu-id="5b903-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="5b903-484">如果 hello 接聽程式正在使用連接埠以外 hello 預設連接埠 (1433)，hello 連接字串中指定 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="5b903-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="5b903-485">例如，hello 下列 sqlcmd 命令連接埠 1435 tooa 接聽程式：</span><span class="sxs-lookup"><span data-stu-id="5b903-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="5b903-486">hello SQLCMD 連線自動連線 toowhichever SQL Server 裝載 hello 主要複本執行個體。</span><span class="sxs-lookup"><span data-stu-id="5b903-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="5b903-487">請確定您指定的 hello 通訊埠的兩個 SQL 伺服器 hello 防火牆上開啟。</span><span class="sxs-lookup"><span data-stu-id="5b903-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="5b903-488">這兩部伺服器所需 hello 您使用的 TCP 連接埠的輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="5b903-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="5b903-489">如需詳細資訊，請參閱[新增或編輯防火牆規則](http://technet.microsoft.com/library/cc753558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b903-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="5b903-490">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b903-490">Next steps</span></span>

- <span data-ttu-id="5b903-491">[新增第二個可用性群組使用 IP 位址 tooa 負載平衡器](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP)。</span><span class="sxs-lookup"><span data-stu-id="5b903-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
