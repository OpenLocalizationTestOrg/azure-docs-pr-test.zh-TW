---
title: "aaaSet 組成的混合式 HPC Pack 叢集在 Azure 中 |Microsoft 文件"
description: "了解 Microsoft HPC Pack toouse 和 Azure tooset 向上很小，混合式高效能運算 (HPC) 叢集"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="cdaeb-103">使用 Microsoft HPC Pack 和隨選 Azure 計算節點設定混合式高效能計算 (HPC) 叢集</span><span class="sxs-lookup"><span data-stu-id="cdaeb-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="cdaeb-104">使用 Microsoft HPC Pack 2012 R2 和 Azure tooset 很小，混合式高效能運算 (HPC) 叢集上。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="cdaeb-105">本文中所顯示的 hello 叢集包含一個在內部部署 HPC Pack 前端節點和某些計算節點部署視在 Azure 中雲端服務。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="cdaeb-106">然後，您就可以 hello 混合式叢集上執行運算作業。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Hybrid HPC cluster][Overview] 

<span data-ttu-id="cdaeb-108">此教學課程會示範一個方法，有時也稱為叢集 「 高載 toohello 雲端，」 toouse 可擴充、 隨 Azure 資源 toorun 需要大量計算的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="cdaeb-109">本教學課程假設您先前沒有使用計算叢集或 HPC Pack 的經驗。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="cdaeb-110">您部署快速供示範之用的混合式計算叢集的預期只有 toohelp 它。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="cdaeb-111">如需考量和步驟 toodeploy HPC Pack 在混合式叢集更大規模生產環境中，或 toouse HPC Pack 2016，請參閱 hello[詳細指引](http://go.microsoft.com/fwlink/p/?LinkID=200493)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="cdaeb-112">如需使用 HPC Pack 的其他案例，包括 Azure 虛擬機器中的自動化叢集部署，請參閱[使用 HPC Pack 在 Azure 中建立及管理 Windows HPC 叢集的選項](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdaeb-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="cdaeb-113">Prerequisites</span></span>
* <span data-ttu-id="cdaeb-114">**Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="cdaeb-115">**執行 Windows Server 2012 R2 或 Windows Server 2012 在內部部署電腦**-使用這個電腦作為 hello hello HPC 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="cdaeb-116">如果您目前執行的不是 Windows Server，可以下載並安裝 [評估版](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="cdaeb-117">hello 電腦必須是聯結的 tooan Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="cdaeb-118">基於測試目的，您可以設定 hello 前端節點電腦做為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="cdaeb-119">tooadd hello Active Directory 網域服務伺服器角色和升級為網域控制站的 hello 前端節點電腦，請參閱 Windows Server hello 文件集。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="cdaeb-120">toosupport HPC Pack，hello 作業系統必須安裝的其中一種語言： 英文、 日文或中文 （簡體）。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="cdaeb-121">確認已安裝重要及重大更新。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="cdaeb-122">**HPC Pack 2012 R2** - [下載](http://go.microsoft.com/fwlink/p/?linkid=328024)hello hello 電量與複製 hello 檔案 toohello 前端節點電腦的可用的最新版本的安裝套件。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="cdaeb-123">選擇安裝檔案 hello 中相同的 Windows Server 安裝的語言。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="cdaeb-124">如果您想 toouse HPC Pack 2016，而不是 HPC Pack 2012 R2，需要進行其他設定。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="cdaeb-125">請參閱 hello[詳細指引](http://go.microsoft.com/fwlink/p/?LinkID=200493)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="cdaeb-126">**網域帳戶**-此帳戶必須具有本機系統管理員權限 hello 前端節點 tooinstall HPC Pack 設定。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="cdaeb-127">**連接埠 443 上的 TCP 連線**從 hello 前端節點 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="cdaeb-128">Hello 前端節點上安裝 HPC Pack</span><span class="sxs-lookup"><span data-stu-id="cdaeb-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="cdaeb-129">您必須先在執行 Windows Server 的內部部署電腦上安裝 Microsoft HPC Pack。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="cdaeb-130">此電腦會成為 hello hello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="cdaeb-131">使用具有本機系統管理員權限的網域帳戶登入 toohello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="cdaeb-132">從 hello HPC Pack 安裝檔案執行 Setup.exe，以啟動 hello HPC Pack 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="cdaeb-133">在 hello **HPC Pack 2012 R2 安裝程式**畫面上，按一下**新安裝或加入新功能 tooan 現有安裝**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![HPC Pack 2012 Setup][install_hpc1]

4. <span data-ttu-id="cdaeb-135">在 hello **Microsoft 軟體使用者協議頁面**，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="cdaeb-136">在 hello**選取安裝類型**頁面上，按一下**透過建立前端節點建立新的 HPC 叢集**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="cdaeb-137">hello 精靈會執行數個預先安裝的測試。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="cdaeb-138">按一下**下一步**上 hello**安裝規則**頁面上，如果所有測試都成功。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="cdaeb-139">否則，請檢閱 hello 所提供的資訊，並在您的環境中進行任何必要的變更。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="cdaeb-140">Hello 測試一次，或如果必要開始可再次 hello 安裝精靈，然後執行。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="cdaeb-141">在 hello **HPC 資料庫組態**頁面上，確定**前端節點**選取所有的 HPC 資料庫，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB Configuration][install_hpc4]

8. <span data-ttu-id="cdaeb-143">接受預設選取項目 hello hello 精靈的其餘的頁面。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="cdaeb-144">在 hello**安裝所需的元件**頁面上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Install][install_hpc6]

9. <span data-ttu-id="cdaeb-146">Hello 安裝完成之後，取消核取**啟動 HPC 叢集管理員**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="cdaeb-147">(您將在稍後的步驟中啟動 HPC 叢集管理員)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![完成][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="cdaeb-149">準備 hello Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cdaeb-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="cdaeb-150">執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com)您 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="cdaeb-151">完成這些步驟之後，您可以部署 Azure 節點從 hello 在內部部署前端節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="cdaeb-152">請一併記下您的 Azure 訂用帳戶識別碼，稍後需要用到。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="cdaeb-153">Hello 中找到識別碼**訂閱**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="cdaeb-154">上傳 hello 預設管理憑證</span><span class="sxs-lookup"><span data-stu-id="cdaeb-154">Upload hello default management certificate</span></span>
<span data-ttu-id="cdaeb-155">HPC Pack 安裝 hello 前端節點，稱為 hello Microsoft HPC Azure 管理憑證，您可以上傳做為 Azure 管理憑證上的自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="cdaeb-156">此憑證供測試和之間的概念證明部署 toosecure hello 連線 hello 前端節點和 Azure。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="cdaeb-157">從 hello 前端節點的電腦 中，登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="cdaeb-158">按一下 [訂用帳戶] > 您的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="cdaeb-159">按一下 [管理憑證] > [上傳]。4.</span><span class="sxs-lookup"><span data-stu-id="cdaeb-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="cdaeb-160">瀏覽的 hello 檔案 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer hello 前端節點上。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="cdaeb-161">然後，按一下 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="cdaeb-162">hello**預設 HPC Azure 管理**憑證出現在 hello 管理憑證的清單。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="cdaeb-163">建立 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="cdaeb-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="cdaeb-164">為了達到最佳效能，建立 hello 雲端服務和 hello （在後續步驟中） 的儲存體帳戶中 hello 相同地理區域。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="cdaeb-165">在 hello 入口網站中，按一下 **雲端服務 （傳統）** > **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="cdaeb-166">輸入 hello 服務的 DNS 名稱，選擇資源群組和位置，然後按**建立**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="cdaeb-167">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cdaeb-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="cdaeb-168">在 hello 入口網站中，按一下 **儲存體帳戶 （傳統）** > **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="cdaeb-169">輸入 hello 帳戶的名稱，然後選取 hello**傳統**部署模型。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="cdaeb-170">選擇資源群組和位置，並保留其他設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="cdaeb-171">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="cdaeb-172">設定 hello 前端節點</span><span class="sxs-lookup"><span data-stu-id="cdaeb-172">Configure hello head node</span></span>
<span data-ttu-id="cdaeb-173">toouse HPC 叢集管理員 toodeploy Azure 節點和 toosubmit 作業先執行一些必要的叢集設定步驟。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="cdaeb-174">Hello 前端節點上，啟動 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="cdaeb-175">如果 hello**選取前端節點**對話方塊出現時，按一下**本機電腦**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="cdaeb-176">hello**部署待辦事項清單**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="cdaeb-177">在 [必要部署工作] 底下，按一下 [設定您的網路]。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configure Network][config_hpc2]

3. <span data-ttu-id="cdaeb-179">在 hello 網路設定精靈 中，選取 **只在企業網路上的所有節點**(拓樸 5)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="cdaeb-180">此網路設定為 hello 簡單供示範之用。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topology 5][config_hpc3]
   
4. <span data-ttu-id="cdaeb-182">按一下**下一步**tooaccept hello 剩餘 hello 精靈頁面上的預設值。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="cdaeb-183">然後，在 hello**檢閱**索引標籤上，按一下 **設定**toocomplete hello 網路組態。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="cdaeb-184">在 hello**部署待辦事項清單**，按一下 **提供安裝認證**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="cdaeb-185">在 hello**安裝認證**對話方塊中，輸入 hello 使用 HPC Pack tooinstall hello 網域帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="cdaeb-186">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-186">Then click **OK**.</span></span> 
   
    ![Installation Credentials][config_hpc6]
   
7. <span data-ttu-id="cdaeb-188">在 hello**部署待辦事項清單**，按一下 **設定新節點的命名 hello**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="cdaeb-189">在 hello**指定節點命名序列**對話方塊方塊中，接受 hello 預設命名數列，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="cdaeb-190">即使 hello 您在本教學課程中加入 Azure 節點會自動命名，請完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Node Naming][config_hpc8]
   
9. <span data-ttu-id="cdaeb-192">在 hello**部署待辦事項清單**，按一下 **建立節點範本**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="cdaeb-193">稍後在 hello 教學課程中，您可以使用 hello 節點範本 tooadd Azure 節點 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="cdaeb-194">在 hello 建立節點範本精靈，請執行下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="cdaeb-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="cdaeb-195">a.</span><span class="sxs-lookup"><span data-stu-id="cdaeb-195">a.</span></span> <span data-ttu-id="cdaeb-196">在 hello**選擇節點範本類型**頁面上，按一下**Windows Azure 節點範本**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Node Template][config_hpc10]
    
    <span data-ttu-id="cdaeb-198">b.</span><span class="sxs-lookup"><span data-stu-id="cdaeb-198">b.</span></span> <span data-ttu-id="cdaeb-199">按一下**下一步**tooaccept hello 預設範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="cdaeb-200">c.</span><span class="sxs-lookup"><span data-stu-id="cdaeb-200">c.</span></span> <span data-ttu-id="cdaeb-201">在 hello**提供訂用帳戶資訊**頁面上，輸入您的 Azure 訂用帳戶 ID （適用於您的 Azure 帳戶資訊）。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="cdaeb-202">然後，在 [管理憑證] 中，瀏覽 [預設 Microsoft HPC Azure 管理]。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="cdaeb-203">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-203">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc12]
    
    <span data-ttu-id="cdaeb-205">d.</span><span class="sxs-lookup"><span data-stu-id="cdaeb-205">d.</span></span> <span data-ttu-id="cdaeb-206">在 hello**提供服務資訊**頁面、 選取 hello 雲端服務和您在上一個步驟中建立的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="cdaeb-207">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-207">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc13]
    
    <span data-ttu-id="cdaeb-209">e.</span><span class="sxs-lookup"><span data-stu-id="cdaeb-209">e.</span></span> <span data-ttu-id="cdaeb-210">按一下**下一步**tooaccept hello 剩餘 hello 精靈頁面上的預設值。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="cdaeb-211">然後，在 hello**檢閱**索引標籤上，按一下 **建立**toocreate hello 節點範本。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cdaeb-212">根據預設，hello Azure 節點範本包含設定 toostart （佈建） 和停止 hello 節點以手動方式，使用 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="cdaeb-213">您可以選擇性地設定排程 toostart 和停止自動 hello Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="cdaeb-214">新增 Azure 節點 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="cdaeb-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="cdaeb-215">現在使用 hello 節點範本 tooadd Azure 節點 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="cdaeb-216">加入 hello 節點 toohello 叢集會儲存其組態資訊，讓您可以啟動 （佈建） 這些隨時 hello 雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="cdaeb-217">您的訂用帳戶只取得支付 Azure 節點之後 hello 雲端服務中執行 hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="cdaeb-218">請遵循這些步驟 tooadd 兩個小節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="cdaeb-219">在 HPC 叢集管理員中，按一下 [節點管理] \(在最新版本的 HPC Pack 中稱為 [資源管理]) > [新增節點]。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Add Node][add_node1]

2. <span data-ttu-id="cdaeb-221">在新增節點精靈 的上 hello hello**選擇部署方法**頁面上，按一下**新增 Windows Azure 節點**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Add Azure Node][add_node1_1]

3. <span data-ttu-id="cdaeb-223">在 hello**指定新的節點**頁面上，選取 hello 您先前建立的 Azure 節點範本 (預設會呼叫**預設 AzureNode 範本**)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="cdaeb-224">接著，指定 **2** 個大小為 [小型] 的節點，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Specify Nodes][add_node2]
   
4. <span data-ttu-id="cdaeb-226">在 hello**完成 hello 新增節點精靈**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="cdaeb-227">HPC 叢集管理員中現在會出現兩個 Azure 節點，名為 **AzureCN-0001** 和 **AzureCN-0002**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="cdaeb-228">兩者都是在 hello**未部署**狀態。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Added Nodes][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="cdaeb-230">啟動 hello Azure 節點</span><span class="sxs-lookup"><span data-stu-id="cdaeb-230">Start hello Azure nodes</span></span>
<span data-ttu-id="cdaeb-231">當您想要在 Azure 中，使用 HPC 叢集管理員 toostart （佈建） toouse hello 叢集資源 hello Azure 節點，並且使其連線。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="cdaeb-232">HPC 叢集管理員中，按一下**節點管理**(稱為**資源管理**在目前版本的 HPC Pack)，並選取 hello Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="cdaeb-233">按一下 開始，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Start Nodes][add_node4]
   
    <span data-ttu-id="cdaeb-235">hello 節點轉換 toohello**佈建**狀態。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="cdaeb-236">檢視 hello 佈建記錄 tootrack hello 佈建進行中。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Provision Nodes][add_node6]

3. <span data-ttu-id="cdaeb-238">請稍候幾分鐘 hello Azure 節點完成佈建到且處於 hello**離線**狀態。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="cdaeb-239">處於此狀態，hello 角色執行個體正在執行，但尚無法接受叢集作業。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="cdaeb-240">執行 hello 角色執行個體的 tooconfirm，hello Azure 入口網站中，按一下**雲端服務 （傳統）** > *your_cloud_service_name*。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="cdaeb-241">您應該會看到兩個**HpcWorkerRole** hello 服務中執行執行個體 （節點）。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="cdaeb-242">HPC Pack 也會自動部署兩個**HpcProxy**執行個體 （中型大小） toohandle hello 前端節點與 Azure 之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Running Instances][view_instances1]

5. <span data-ttu-id="cdaeb-244">toobring hello Azure 節點線上 toorun 叢集作業，選取 hello 節點、 按一下滑鼠右鍵，然後按一下**上線**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Offline Nodes][add_node7]
   
    <span data-ttu-id="cdaeb-246">HPC 叢集管理員表示 hello 節點在 hello**線上**狀態。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="cdaeb-247">Hello 叢集中執行的命令</span><span class="sxs-lookup"><span data-stu-id="cdaeb-247">Run a command across hello cluster</span></span>
<span data-ttu-id="cdaeb-248">toocheck hello 安裝中，使用 hello HPC Pack **clusrun**命令 toorun 命令或一個或多個叢集節點上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="cdaeb-249">簡單舉例如下，使用**clusrun** tooget hello IP 組態 hello Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="cdaeb-250">Hello 前端節點上，系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="cdaeb-251">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="cdaeb-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="cdaeb-252">出現提示時，輸入您的叢集系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="cdaeb-253">您應該會看到命令的輸出類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-253">You should see command output similar toohello following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="cdaeb-255">執行測試工作</span><span class="sxs-lookup"><span data-stu-id="cdaeb-255">Run a test job</span></span>
<span data-ttu-id="cdaeb-256">現在您可以送出 hello 混合式叢集執行的測試工作。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="cdaeb-257">這個範例是簡單的參數式掃掠作業 (一種本質平行計算)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="cdaeb-258">這個範例會執行子工作使用 hello 新增整數 tooitself**設定/a**命令。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="cdaeb-259">Hello 叢集中的所有 hello 節點 1 too100 從都參與 toofinishing hello 子任務的整數。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="cdaeb-260">在 HPC 叢集管理員中，按一下 [作業管理] > [New Parametric Sweep Job] \(新增參數式掃掠作業)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![New Job][test_job1]

2. <span data-ttu-id="cdaeb-262">在 hello**新參數掃掠工作**對話方塊中，於**命令列**，型別`set /a *+*`（覆寫 hello 預設命令列顯示）。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="cdaeb-263">保留的 hello 剩餘的設定，預設值，然後按**送出**toosubmit hello 作業。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Parametric Sweep][param_sweep1]

3. <span data-ttu-id="cdaeb-265">Hello 作業完成時，連按兩下 hello**我掃掠工作**作業。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="cdaeb-266">按一下**檢視工作**，然後按一下任務的子工作 tooview hello 計算輸出。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Task Results][view_job361]

5. <span data-ttu-id="cdaeb-268">按一下的 toosee 哪一個節點的子工作中，執行 hello 計算**配置節點**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="cdaeb-269">(您的叢集可能會顯示不同的節點名稱。)</span><span class="sxs-lookup"><span data-stu-id="cdaeb-269">(Your cluster might show a different node name.)</span></span>
   
    ![Task Results][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="cdaeb-271">停止 hello Azure 節點</span><span class="sxs-lookup"><span data-stu-id="cdaeb-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="cdaeb-272">您嘗試 hello 叢集之後，停止 hello Azure 節點 tooavoid 不必要的費用 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="cdaeb-273">這個步驟會停止 hello 雲端服務，並移除 hello Azure 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="cdaeb-274">在 HPC 叢集管理員中，於 [節點管理] \(在舊版的 HPC Pack 中稱為 [資源管理]) 中，選取這兩個 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="cdaeb-275">然後，按一下 [停止]。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-275">Then, click **Stop**.</span></span>
   
    ![Stop Nodes][stop_node1]

2. <span data-ttu-id="cdaeb-277">在 hello**停止 Windows Azure 節點**對話方塊中，按一下 **停止**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="cdaeb-278">hello 節點轉換 toohello**停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="cdaeb-279">請稍候幾分鐘 HPC 叢集管理員會顯示 hello 節點都是**未部署**。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Not Deployed Nodes][stop_node4]

4. <span data-ttu-id="cdaeb-281">hello 角色執行個體在 Azure 中，不會再執行中的 tooconfirm hello Azure 入口網站中，按一下**雲端服務 （傳統）** > *your_cloud_service_name*。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="cdaeb-282">Hello 的實際執行環境中部署沒有任何執行個體。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="cdaeb-283">如此即完成 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdaeb-284">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdaeb-284">Next steps</span></span>
* <span data-ttu-id="cdaeb-285">瀏覽 hello 文件[HPC Pack](https://technet.microsoft.com/library/cc514029)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="cdaeb-286">tooset 組成的混合式部署 HPC Pack 叢集在更大的小數位數，請參閱[tooAzure 背景工作角色執行個體，使用 Microsoft HPC Pack 高載](http://go.microsoft.com/fwlink/p/?LinkID=200493)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="cdaeb-287">針對其他方式 toocreate 在 Azure 中的 HPC Pack 叢集，包括使用 Azure 資源管理員範本，請參閱[HPC 叢集的選項以在 Azure 中的 Microsoft HPC Pack](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cdaeb-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
