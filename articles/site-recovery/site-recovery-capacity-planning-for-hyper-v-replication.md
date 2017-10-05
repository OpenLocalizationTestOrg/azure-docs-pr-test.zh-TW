---
title: "執行 Site Recovery 的 Hyper-V 容量規劃工具 | Microsoft Docs"
description: "本文說明如何執行 Azure Site Recovery 的 Hyper-V 容量規劃工具"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 272b5abb5e6451164ca7900dda399b6aac65f986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-the-hyper-v-capacity-planner-tool-for-site-recovery"></a><span data-ttu-id="b4133-103">執行 Site Recovery 的 Hyper-V 容量規劃工具</span><span class="sxs-lookup"><span data-stu-id="b4133-103">Run the Hyper-V capacity planner tool for Site Recovery</span></span>

<span data-ttu-id="b4133-104">在 Azure Site Recovery 部署的過程中，您需要找出複寫和頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="b4133-104">As part of your Azure Site Recovery deployment, you need to figure out your replication and bandwidth requirements.</span></span> <span data-ttu-id="b4133-105">針對 Hyper-V 虛擬機器複寫，Site Recovery 的 Hyper-V 容量規劃工具可協助您這麼做。</span><span class="sxs-lookup"><span data-stu-id="b4133-105">The Hyper-V capacity planner tool for Site Recovery helps you to do this, for Hyper-V virtual machine replication.</span></span>

<span data-ttu-id="b4133-106">本文說明如何執行 Hyper-V 容量規劃工具。</span><span class="sxs-lookup"><span data-stu-id="b4133-106">This article describes how to run the Hyper-V capacity planner tool.</span></span> <span data-ttu-id="b4133-107">此工具應該搭配 [Site Recovery 的容量規劃](site-recovery-capacity-planner.md)中的相關資訊一起使用。</span><span class="sxs-lookup"><span data-stu-id="b4133-107">This tool should be used together with the information in [capacity planning for Site Recovery](site-recovery-capacity-planner.md).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b4133-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="b4133-108">Before you start</span></span>
<span data-ttu-id="b4133-109">您會在主要網站中的 Hyper-V 伺服器或叢集節點上執行工具。</span><span class="sxs-lookup"><span data-stu-id="b4133-109">You run the tool on a Hyper-V server or cluster node in your primary site.</span></span> <span data-ttu-id="b4133-110">若要執行 Hyper-V 主機伺服器需要的工具：</span><span class="sxs-lookup"><span data-stu-id="b4133-110">To run the tool the Hyper-V host servers needs:</span></span>

* <span data-ttu-id="b4133-111">作業系統︰Windows Server 2012 或 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b4133-111">Operating system: Windows Server 2012 or 2012 R2</span></span>
* <span data-ttu-id="b4133-112">記憶體：20 MB (最低要求)</span><span class="sxs-lookup"><span data-stu-id="b4133-112">Memory: 20 MB (minimum)</span></span>
* <span data-ttu-id="b4133-113">CPU：5% 額外負荷 (最低要求)</span><span class="sxs-lookup"><span data-stu-id="b4133-113">CPU: 5 percent overhead (minimum)</span></span>
* <span data-ttu-id="b4133-114">磁碟空間：5 MB (最低要求)</span><span class="sxs-lookup"><span data-stu-id="b4133-114">Disk space: 5 MB (minimum)</span></span>

<span data-ttu-id="b4133-115">執行工具之前，您必須準備主要網站。</span><span class="sxs-lookup"><span data-stu-id="b4133-115">Before you run the tool, you need to prepare the primary site.</span></span> <span data-ttu-id="b4133-116">如果您在兩個內部部署網站之間複寫，且想要檢查頻寬，您也必須準備複本伺服器。</span><span class="sxs-lookup"><span data-stu-id="b4133-116">If you're replicating between two on-premises sites and you want to check bandwidth, you need to prepare a replica server as well.</span></span>

## <a name="step-1-prepare-the-primary-site"></a><span data-ttu-id="b4133-117">步驟 1：準備主要網站</span><span class="sxs-lookup"><span data-stu-id="b4133-117">Step 1: Prepare the primary site</span></span>

1. <span data-ttu-id="b4133-118">在主要網站上製作您要複寫的所有 Hyper-V VM，和它們所在的 Hyper-V 主機/叢集清單。</span><span class="sxs-lookup"><span data-stu-id="b4133-118">On the primary site, make a list of all of the Hyper-V VMs you want to replicate, and the Hyper-V hosts/clusters on which they're located.</span></span> <span data-ttu-id="b4133-119">此工具可針對多個獨立主機或單一叢集執行，但是不能同時執行。</span><span class="sxs-lookup"><span data-stu-id="b4133-119">The tool can run for multiple standalone hosts, or for a single cluster, but not both together.</span></span> <span data-ttu-id="b4133-120">也必須針對每個作業系統分別執行，因此您應該收集關於 Hyper-V 伺服器的資訊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b4133-120">It also needs to run separately for each operating system, so you should gather information about Hyper-V servers as follows:</span></span>

   * <span data-ttu-id="b4133-121">Windows Server 2012 獨立伺服器</span><span class="sxs-lookup"><span data-stu-id="b4133-121">Windows Server 2012 standalone servers</span></span>
   * <span data-ttu-id="b4133-122">Windows Server 2012 叢集</span><span class="sxs-lookup"><span data-stu-id="b4133-122">Windows Server 2012 clusters</span></span>
   * <span data-ttu-id="b4133-123">Windows Server 2012 R2 獨立伺服器</span><span class="sxs-lookup"><span data-stu-id="b4133-123">Windows Server 2012 R2 standalone servers</span></span>
   * <span data-ttu-id="b4133-124">Windows Server 2012 R2 叢集</span><span class="sxs-lookup"><span data-stu-id="b4133-124">Windows Server 2012 R2 clusters</span></span>
2. <span data-ttu-id="b4133-125">在所有 Hyper-V 主機和叢集上啟用 WMI 遠端存取。</span><span class="sxs-lookup"><span data-stu-id="b4133-125">Enable remote access to WMI on all the Hyper-V hosts and clusters.</span></span> <span data-ttu-id="b4133-126">在每個伺服器/叢集上執行此命令，確定已設定防火牆規則和使用者權限：</span><span class="sxs-lookup"><span data-stu-id="b4133-126">Run this command on each server/cluster, to make sure firewall rules and user permissions are set:</span></span>

        netsh firewall set service RemoteAdmin enable
3. <span data-ttu-id="b4133-127">在伺服器和叢集上啟用效能監視，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b4133-127">Enable performance monitoring on servers and clusters, as follows:</span></span>

   * <span data-ttu-id="b4133-128">開啟 [Windows 防火牆] 與 [進階安全性] 嵌入式管理單元，然後啟用下列輸入規則：COM+ 網路存取 (DCOM-IN)，以及「遠端事件記錄檔管理」群組中的所有規則。</span><span class="sxs-lookup"><span data-stu-id="b4133-128">Open the Windows Firewall with the **Advanced Security** snapin, and then enable the following inbound rules: **COM+ Network Access (DCOM-IN)** and all rules in the **Remote Event Log Management group**.</span></span>

## <a name="step-2-prepare-a-replica-server-on-premises-to-on-premises-replication"></a><span data-ttu-id="b4133-129">步驟 2：準備複本伺服器 (內部部署至內部部署複寫)</span><span class="sxs-lookup"><span data-stu-id="b4133-129">Step 2: Prepare a replica server (on-premises to on-premises replication)</span></span>
<span data-ttu-id="b4133-130">如果您要複寫至 Azure，就不需要執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="b4133-130">You don't need to do this if you're replicating to Azure.</span></span>

<span data-ttu-id="b4133-131">我們建議您設定一部 Hyper-V 主機做為復原伺服器，以便虛擬 VM 可以複寫到這部主機以檢查頻寬。</span><span class="sxs-lookup"><span data-stu-id="b4133-131">We recommend you set up a single Hyper-V host as a recovery server, so that a dummy VM can be replicated to it to check bandwidth.</span></span>  <span data-ttu-id="b4133-132">您可以略過這個步驟，但是如果不執行這項作業，就法測量頻寬。</span><span class="sxs-lookup"><span data-stu-id="b4133-132">You can skip this, but you won't be able to measure bandwidth unless you do it.</span></span>

1. <span data-ttu-id="b4133-133">如果您想要使用叢集節點做為複本，請設定 Hyper-V 複本代理人：</span><span class="sxs-lookup"><span data-stu-id="b4133-133">If you want to use a cluster node as the replica configure Hyper-V Replica broker:</span></span>

   * <span data-ttu-id="b4133-134">在 [伺服器管理員] 中，開啟 [容錯移轉叢集管理員]。</span><span class="sxs-lookup"><span data-stu-id="b4133-134">In **Server Manager**, open **Failover Cluster Manager**.</span></span>
   * <span data-ttu-id="b4133-135">連接到叢集，反白顯示叢集名稱，然後按一下 [動作] > [設定角色] 以開啟 [高可用性] 精靈。</span><span class="sxs-lookup"><span data-stu-id="b4133-135">Connect to the cluster, highlight the cluster name and click **Actions** > **Configure Role** to open the High Availability wizard.</span></span>
   * <span data-ttu-id="b4133-136">在 [選取角色] 中，選取 [Hyper-V 複本代理人]。</span><span class="sxs-lookup"><span data-stu-id="b4133-136">In **Select Role**, click **Hyper-V Replica Broker**.</span></span> <span data-ttu-id="b4133-137">在精靈中提供 [NetBIOS 名稱] 和 [IP 位址] 做為叢集的連接點 (稱為用戶端存取點)。</span><span class="sxs-lookup"><span data-stu-id="b4133-137">In the wizard provide a **NetBIOS name** and the **IP address** to be used as the connection point to the cluster (called a client access point).</span></span> <span data-ttu-id="b4133-138">會設定 [Hyper-V 複本代理人]  ，產生您應該記下的用戶端存取點名稱。</span><span class="sxs-lookup"><span data-stu-id="b4133-138">The **Hyper-V Replica Broker** will be configured, resulting in a client access point name that you should note.</span></span>
   * <span data-ttu-id="b4133-139">確認 Hyper-V 複本代理人角色順利連線，而且可以進行叢集所有節點之間的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b4133-139">Verify that the Hyper-V Replica Broker role comes online successfully, and can fail over between all nodes of the cluster.</span></span> <span data-ttu-id="b4133-140">若要這樣做，請以滑鼠右鍵按一下角色，指向 [移動]，然後按一下 [選取節點]。</span><span class="sxs-lookup"><span data-stu-id="b4133-140">To do this, right click the role, point to **Move**, and then click **Select Node**.</span></span> <span data-ttu-id="b4133-141">選取節點 > [確定]。</span><span class="sxs-lookup"><span data-stu-id="b4133-141">Select a node > **OK**.</span></span>
   * <span data-ttu-id="b4133-142">如果您使用憑證型驗證，請確定每個叢集節點與用戶端存取點都有安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="b4133-142">If you're using certificate-based authentication, make sure each cluster node and the client access point all have the certificate installed.</span></span>
2. <span data-ttu-id="b4133-143">啟用複本伺服器：</span><span class="sxs-lookup"><span data-stu-id="b4133-143">Enable a replica server:</span></span>

   * <span data-ttu-id="b4133-144">對於叢集開啟 [失敗叢集管理員]，連線到叢集，然後按一下 [角色] > 選取角色 > [複寫設定] > [啟用此叢集做為複本伺服器]。</span><span class="sxs-lookup"><span data-stu-id="b4133-144">For a cluster open Failure Cluster Manager, connect to the cluster and click **Roles** > select role > **Replication Settings** > **Enable this cluster as a Replica server**.</span></span> <span data-ttu-id="b4133-145">如果使用叢集做為複本，您也必須在主要網站的叢集上顯示 Hyper-V 複本代理人角色。</span><span class="sxs-lookup"><span data-stu-id="b4133-145">If you use a cluster as the replica, you need to have the Hyper-V Replica Broker role present on the cluster in the primary site as well.</span></span>
   * <span data-ttu-id="b4133-146">若是獨立伺服器，請開啟 [Hyper-V 管理員]。</span><span class="sxs-lookup"><span data-stu-id="b4133-146">For a standalone server open Hyper-V Manager.</span></span> <span data-ttu-id="b4133-147">在 [動作] 窗格中，按一下您想要啟用的伺服器的 [Hyper-V 設定]，然後在 [複寫組態] 中按一下 [啟用這台電腦做為複本伺服器]。</span><span class="sxs-lookup"><span data-stu-id="b4133-147">In the **Actions** pane, click **Hyper-V Settings** for the server you want to enable, and in **Replication Configuration** click **Enable this computer as a Replica server**.</span></span>
3. <span data-ttu-id="b4133-148">設定驗證：</span><span class="sxs-lookup"><span data-stu-id="b4133-148">Set up authentication:</span></span>

   * <span data-ttu-id="b4133-149">在 [驗證和連接埠] 中選取如何驗證主要伺服器及驗證連接埠。</span><span class="sxs-lookup"><span data-stu-id="b4133-149">In **Authentication and ports**, select how to authenticate the primary server, and the authentication ports.</span></span> <span data-ttu-id="b4133-150">如果您使用憑證，按一下 [選取憑證] 以選取其中一個。</span><span class="sxs-lookup"><span data-stu-id="b4133-150">If you use a certificate click **Select Certificate** to select one.</span></span> <span data-ttu-id="b4133-151">如果主要和復原 Hyper-V 主機都位於相同網域或信任的網域，則使用 Kerberos。</span><span class="sxs-lookup"><span data-stu-id="b4133-151">Use Kerberos if the primary and recovery Hyper-V hosts are in the same domain, or in trusted domains.</span></span> <span data-ttu-id="b4133-152">針對不同的網域或工作群組部署使用憑證。</span><span class="sxs-lookup"><span data-stu-id="b4133-152">Use certificates for different domains, or for a workgroup deployment.</span></span>
   * <span data-ttu-id="b4133-153">在 [授權與存放裝置] 區段中，允許**任何**驗證 (主要) 伺服器將複寫資料傳送到這個複本伺服器。</span><span class="sxs-lookup"><span data-stu-id="b4133-153">In **Authorization and Storage**, allow **any** authenticated (primary) server to send replication data to this replica server.</span></span>

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * <span data-ttu-id="b4133-154">執行 **netsh http show servicestate**，檢查接聽程式是否針對您指定的通訊協定/連接埠執行：</span><span class="sxs-lookup"><span data-stu-id="b4133-154">Run **netsh http show servicestate**, to check that the listener is running for the protocol/port you specified:</span></span>  
4. <span data-ttu-id="b4133-155">設定防火牆：</span><span class="sxs-lookup"><span data-stu-id="b4133-155">Set up firewalls.</span></span> <span data-ttu-id="b4133-156">Hyper-V 安裝期間會建立防火牆規則，以允許預設連接埠的流量 (443 上的 HTTPS，80 上的 Kerberos)。</span><span class="sxs-lookup"><span data-stu-id="b4133-156">During Hyper-V installation, firewall rules are created to allow traffic on the default ports (HTTPS on 443, Kerberos on 80).</span></span> <span data-ttu-id="b4133-157">啟用這些規則，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b4133-157">Enable these rules as follows:</span></span>
  - <span data-ttu-id="b4133-158">叢集 (443) 上的憑證驗證：``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``</span><span class="sxs-lookup"><span data-stu-id="b4133-158">Certificate authentication on cluster (443): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``</span></span>
  - <span data-ttu-id="b4133-159">叢集 (80) 上的 Kerberos 驗證︰``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``</span><span class="sxs-lookup"><span data-stu-id="b4133-159">Kerberos authentication on cluster (80): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``</span></span>
  - <span data-ttu-id="b4133-160">獨立伺服器上的憑證驗證︰``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``</span><span class="sxs-lookup"><span data-stu-id="b4133-160">Certificate authentication on standalone server: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``</span></span>
  - <span data-ttu-id="b4133-161">獨立伺服器上的 Kerberos 驗證︰``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``</span><span class="sxs-lookup"><span data-stu-id="b4133-161">Kerberos authentication on standalone server: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``</span></span>

## <a name="step-3-run-the-capacity-planner-tool"></a><span data-ttu-id="b4133-162">步驟 3：執行容量規劃工具</span><span class="sxs-lookup"><span data-stu-id="b4133-162">Step 3: Run the capacity planner tool</span></span>
<span data-ttu-id="b4133-163">在準備好您的主要網站並設定復原伺服器之後，就可以執行此工具。</span><span class="sxs-lookup"><span data-stu-id="b4133-163">After you've prepared your primary site, and set up a recovery server, you can run the tool.</span></span>

1. <span data-ttu-id="b4133-164">[下載](https://www.microsoft.com/download/details.aspx?id=39057) the tool from the Microsoft 下載 Center.</span><span class="sxs-lookup"><span data-stu-id="b4133-164">[Download](https://www.microsoft.com/download/details.aspx?id=39057) the tool from the Microsoft Download Center.</span></span>
2. <span data-ttu-id="b4133-165">從其中一個主要伺服器 (或主要叢集的其中一個節點) 執行工具。</span><span class="sxs-lookup"><span data-stu-id="b4133-165">Run the tool from one of the primary servers (or one of the nodes from the primary cluster).</span></span> <span data-ttu-id="b4133-166">以滑鼠右鍵按一下 .exe 檔案，然後選擇 [ **以系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="b4133-166">Right-click the .exe file, and then choose **Run as administrator**.</span></span>
3. <span data-ttu-id="b4133-167">在 [開始之前]，指定您要收集資料的時間長度。</span><span class="sxs-lookup"><span data-stu-id="b4133-167">In **Before you begin**, specify for how long you want to collect data.</span></span> <span data-ttu-id="b4133-168">建議在實際執行期間執行工具，以確保資料具有代表性。</span><span class="sxs-lookup"><span data-stu-id="b4133-168">We recommend you run the tool during production hours to ensure that data is representative.</span></span> <span data-ttu-id="b4133-169">如果您只想要驗證網路連線，可以只收集一分鐘的資料。</span><span class="sxs-lookup"><span data-stu-id="b4133-169">If you're only trying to validate network connectivity, you can collect for a minute only.</span></span>

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. <span data-ttu-id="b4133-170">在 [主要網站詳細資料] 中，針對獨立主機指定伺服器名稱或 FQDN，或針對叢集指定用戶端接受點的 FQDN、叢集名稱或叢集中的任何節點，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b4133-170">In  **Primary site details**, specify the server name or FQDN for a standalone host, or for a cluster specify the FQDN of the client accept point, cluster name, or any node in the cluster and then click **Next**.</span></span> <span data-ttu-id="b4133-171">此工具會自動偵測它執行的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="b4133-171">The tool automatically detects the name of the server it's running on.</span></span> <span data-ttu-id="b4133-172">此工具會挑選可以監視指定伺服器的 VM。</span><span class="sxs-lookup"><span data-stu-id="b4133-172">The tool picks up VMs that can be monitored for the specified servers.</span></span>

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. <span data-ttu-id="b4133-173">在 [複本網站詳細資料] 中，如果您要複寫至 Azure 或次要資料中心，且尚未設定複本伺服器，請選取 [略過複本網站的相關測試]。</span><span class="sxs-lookup"><span data-stu-id="b4133-173">In **Replica Site Details**, if you're replicating to Azure, or if you're replicating to a secondary datacenter and haven't set up a replica server, select **Skip tests involving replica site**.</span></span> <span data-ttu-id="b4133-174">如果您要複寫到次要資料中心，而且已經設定好複本，在 [伺服器名稱 (或) Hyper-V 複本代理人 CAP] 中輸入獨立伺服器的 FQDN，或叢集的用戶端存取點。</span><span class="sxs-lookup"><span data-stu-id="b4133-174">If you are replicating to a secondary datacenter and you've set up a replica type, enter FQDN of the standalone server, or the client access point for the cluster, in **Server name (or) Hyper-V Replica Broker CAP**.</span></span>

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. <span data-ttu-id="b4133-175">在 [擴充複本詳細資料] 中啟用 [略過擴充複本網站的相關測試]。</span><span class="sxs-lookup"><span data-stu-id="b4133-175">In **Extended Replica Details**, enable **Skip the tests involving Extended Replica site**.</span></span> <span data-ttu-id="b4133-176">這些測試不受 Site Recovery 支援。</span><span class="sxs-lookup"><span data-stu-id="b4133-176">These tests aren't supported by Site Recovery.</span></span>
7. <span data-ttu-id="b4133-177">在 [選擇要複寫的 VM] 中，工具會根據您在 [主要網站詳細資料] 頁面上指定的設定，連接到伺服器或叢集，並且顯示主要伺服器上執行的 VM 和磁碟。</span><span class="sxs-lookup"><span data-stu-id="b4133-177">In **Choose VMs to Replicate**, the tools connects to the server or cluster and displays VMs and disks running on the primary server, in accordance with the settings you specified on the **Primary Site Details** page.</span></span> <span data-ttu-id="b4133-178">已針對複寫啟用 VM，不會顯示未執行的項目。</span><span class="sxs-lookup"><span data-stu-id="b4133-178">VMs that are already enabled for replication, or that aren't running, won't be displayed.</span></span> <span data-ttu-id="b4133-179">選取您想要收集度量的 VM。</span><span class="sxs-lookup"><span data-stu-id="b4133-179">Select the VMs for which you want to collect metrics.</span></span> <span data-ttu-id="b4133-180">選取 VHD 也會自動收集 VM 的資料。</span><span class="sxs-lookup"><span data-stu-id="b4133-180">Selecting the VHDs automatically collects data for the VMs too.</span></span>
8. <span data-ttu-id="b4133-181">如果您已設定複本伺服器或叢集，請在 [網路資訊] 中指定您認為將會用於主要和複本網站之間的近似 WAN 頻寬，如果您已設定憑證驗證，則選取憑證。</span><span class="sxs-lookup"><span data-stu-id="b4133-181">If you've configured a replica server or cluster, in **Network information**, specify the approximate WAN bandwidth you think will be used between the primary and replica sites, and select the certificates if you've configured certificate authentication.</span></span>

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. <span data-ttu-id="b4133-182">在 [摘要] 中檢查設定，然後按 [下一步] 以開始收集度量。</span><span class="sxs-lookup"><span data-stu-id="b4133-182">In **Summary**, check the settings and click **Next** to begin collecting metrics.</span></span> <span data-ttu-id="b4133-183">工具的進度和狀態會顯示在 [計算容量] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b4133-183">Tool progress and status is displayed on the **Calculate Capacity** page.</span></span> <span data-ttu-id="b4133-184">此工具完成執行時，請按一下 [檢視報告] 以檢閱輸出。</span><span class="sxs-lookup"><span data-stu-id="b4133-184">When the tool finishes running, click **View Report** to view the output.</span></span> <span data-ttu-id="b4133-185">根據預設，報告和記錄檔會儲存在 **%systemdrive%\Users\Public\Documents\Capacity Planner**。</span><span class="sxs-lookup"><span data-stu-id="b4133-185">By default, reports and logs are stored in **%systemdrive%\Users\Public\Documents\Capacity Planner**.</span></span>

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-the-results"></a><span data-ttu-id="b4133-186">步驟 4：解譯結果</span><span class="sxs-lookup"><span data-stu-id="b4133-186">Step 4: Interpret the results</span></span>

<span data-ttu-id="b4133-187">以下是重要度量。</span><span class="sxs-lookup"><span data-stu-id="b4133-187">Here are the important metrics.</span></span> <span data-ttu-id="b4133-188">您可以忽略未列在這裡的度量。</span><span class="sxs-lookup"><span data-stu-id="b4133-188">You can ignore metrics which aren't listed here.</span></span> <span data-ttu-id="b4133-189">它們與 Site Recovery 不相關。</span><span class="sxs-lookup"><span data-stu-id="b4133-189">They're not relevant for Site Recovery.</span></span>

### <a name="on-premises-to-on-premises-replication"></a><span data-ttu-id="b4133-190">內部部署至內部部署複寫</span><span class="sxs-lookup"><span data-stu-id="b4133-190">On-premises to on-premises replication</span></span>

* <span data-ttu-id="b4133-191">主要主機計算、記憶體上複寫的影響</span><span class="sxs-lookup"><span data-stu-id="b4133-191">Impact of replication on the primary host's compute, memory</span></span>
* <span data-ttu-id="b4133-192">主要、復原主機儲存體磁碟空間、IOPS 上複寫的影響</span><span class="sxs-lookup"><span data-stu-id="b4133-192">Impact of replication on the primary, recovery hosts's storage disk space, IOPS</span></span>
* <span data-ttu-id="b4133-193">差異複寫所需的總頻寬 (Mbps)</span><span class="sxs-lookup"><span data-stu-id="b4133-193">Total bandwidth required for delta replication (Mbps)</span></span>
* <span data-ttu-id="b4133-194">主要主機和復原主機之間觀察到的網路頻寬 (Mbps)</span><span class="sxs-lookup"><span data-stu-id="b4133-194">Observed network bandwidth between the primary host and the recovery host (Mbps)</span></span>
* <span data-ttu-id="b4133-195">兩個主機/叢集之間作用中平行傳輸理想數目的建議</span><span class="sxs-lookup"><span data-stu-id="b4133-195">Suggestion for the ideal number of active parallel transfers between the two hosts/clusters</span></span>

### <a name="on-premises-to-azure-replication"></a><span data-ttu-id="b4133-196">內部部署至 Azure 複寫</span><span class="sxs-lookup"><span data-stu-id="b4133-196">On-premises to Azure replication</span></span>

* <span data-ttu-id="b4133-197">主要主機計算、記憶體上複寫的影響</span><span class="sxs-lookup"><span data-stu-id="b4133-197">Impact of replication on the primary host's compute, memory</span></span>
* <span data-ttu-id="b4133-198">主要主機儲存體磁碟空間、IOPS 上複寫的影響</span><span class="sxs-lookup"><span data-stu-id="b4133-198">Impact of replication on the primary host's storage disk space, IOPS</span></span>
* <span data-ttu-id="b4133-199">差異複寫所需的總頻寬 (Mbps)</span><span class="sxs-lookup"><span data-stu-id="b4133-199">Total bandwidth required for delta replication (Mbps)</span></span>

## <a name="more-resources"></a><span data-ttu-id="b4133-200">其他資源</span><span class="sxs-lookup"><span data-stu-id="b4133-200">More resources</span></span>
* <span data-ttu-id="b4133-201">如需工具的詳細資訊，請閱讀隨工具下載的文件。</span><span class="sxs-lookup"><span data-stu-id="b4133-201">For detailed information about the tool, read the document that accompanies the tool download.</span></span>
* <span data-ttu-id="b4133-202">觀看 Keith Mayer 的 [TechNet 部落格](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx)上的工具的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="b4133-202">Watch a walkthrough of the tool on Keith Mayer’s [TechNet blog](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).</span></span>
* <span data-ttu-id="b4133-203">[結果](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) </span><span class="sxs-lookup"><span data-stu-id="b4133-203">[Get the results](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) of our performance testing for on-premises to on-premises Hyper-V replication</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4133-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4133-204">Next steps</span></span>

<span data-ttu-id="b4133-205">容量規劃完成之後，您就可以開始部署 Site Recovery：</span><span class="sxs-lookup"><span data-stu-id="b4133-205">After you've finished capacity planning you can start deploying Site Recovery:</span></span>

* [<span data-ttu-id="b4133-206">將 VMM 雲端中的 Hyper-V VM 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="b4133-206">Replicate Hyper-V VMs in VMM clouds to Azure</span></span>](site-recovery-vmm-to-azure.md)
* [<span data-ttu-id="b4133-207">將 Hyper-V VM (不使用 VMM) 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="b4133-207">Replicate Hyper-V VMs (without VMM) to Azure</span></span>](site-recovery-hyper-v-site-to-azure.md)
* [<span data-ttu-id="b4133-208">在 VMM 站台間複寫 Hyper-V VM</span><span class="sxs-lookup"><span data-stu-id="b4133-208">Replicate Hyper-V VMs between VMM sites</span></span>](site-recovery-vmm-to-vmm.md)
