---
title: "在 Azure 中設定混合式 HPC Pack 叢集 | Microsoft Docs"
description: "了解如何使用 Microsoft HPC Pack 和 Azure 設定一個小型的混合式高效能運算 (HPC) 叢集"
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
ms.openlocfilehash: f6dc9657e64160be1e68a7356863b53131e9b3c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="fea7a-103">使用 Microsoft HPC Pack 和隨選 Azure 計算節點設定混合式高效能計算 (HPC) 叢集</span><span class="sxs-lookup"><span data-stu-id="fea7a-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="fea7a-104">使用 Microsoft HPC Pack 2012 R2 和 Azure 設定小型的混合式高效能運算 (HPC) 叢集。</span><span class="sxs-lookup"><span data-stu-id="fea7a-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="fea7a-105">本文中所示的叢集包含一個內部部署 HPC Pack 前端節點，以及一些您視需要部署在 Azure 雲端服務中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="fea7a-106">然後，您便可以在混合式叢集上執行計算作業。</span><span class="sxs-lookup"><span data-stu-id="fea7a-106">You can then run compute jobs on the hybrid cluster.</span></span>

![Hybrid HPC cluster][Overview] 

<span data-ttu-id="fea7a-108">本教學課程示範一個有時稱為「將量擴大到雲端」的方法，此方法使用隨選 Azure 資源來執行大量計算的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea7a-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span></span>

<span data-ttu-id="fea7a-109">本教學課程假設您先前沒有使用計算叢集或 HPC Pack 的經驗。</span><span class="sxs-lookup"><span data-stu-id="fea7a-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="fea7a-110">其只是要協助您快速部署一個示範性質的混合式計算叢集。</span><span class="sxs-lookup"><span data-stu-id="fea7a-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="fea7a-111">如需有關使用 HPC Pack 2016，或有關在生產環境中以較大規模部署混合式 HPC Pack 叢集的考量和步驟，請參閱[詳細指引 (英文)](http://go.microsoft.com/fwlink/p/?LinkID=200493)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="fea7a-112">如需使用 HPC Pack 的其他案例，包括 Azure 虛擬機器中的自動化叢集部署，請參閱[使用 HPC Pack 在 Azure 中建立及管理 Windows HPC 叢集的選項](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fea7a-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="fea7a-113">Prerequisites</span></span>
* <span data-ttu-id="fea7a-114">**Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="fea7a-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="fea7a-115">**一部執行 Windows Server 2012 R2 或 Windows Server 2012 的內部部署電腦** - 使用這部電腦作為 HPC 叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span></span> <span data-ttu-id="fea7a-116">如果您目前執行的不是 Windows Server，可以下載並安裝 [評估版](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="fea7a-117">電腦必須加入 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="fea7a-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="fea7a-118">基於測試目的，您可以將前端節點電腦設定為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="fea7a-118">For test purposes, you can configure the head node computer as a domain controller.</span></span> <span data-ttu-id="fea7a-119">若要新增 Active Directory 網域服務伺服器角色，並將前端節點電腦升級為網域控制站，請參閱 Windows Server 的文件。</span><span class="sxs-lookup"><span data-stu-id="fea7a-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span></span>
  * <span data-ttu-id="fea7a-120">為了支援 HPC Pack，作業系統必須以下列其中一種語言安裝：英文、日文或簡體中心。</span><span class="sxs-lookup"><span data-stu-id="fea7a-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="fea7a-121">確認已安裝重要及重大更新。</span><span class="sxs-lookup"><span data-stu-id="fea7a-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="fea7a-122">**HPC Pack 2012 R2** - 免費[下載](http://go.microsoft.com/fwlink/p/?linkid=328024)最新版本的安裝套件，並將檔案複製到前端節點電腦。</span><span class="sxs-lookup"><span data-stu-id="fea7a-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span></span> <span data-ttu-id="fea7a-123">選擇與安裝的 Windows Server 語言相同語言的安裝檔。</span><span class="sxs-lookup"><span data-stu-id="fea7a-123">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="fea7a-124">如果您想要使用 HPC Pack 2016 而不是 HPC Pack 2012 R2，則需要額外設定。</span><span class="sxs-lookup"><span data-stu-id="fea7a-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="fea7a-125">請參閱[詳細指引](http://go.microsoft.com/fwlink/p/?LinkID=200493)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="fea7a-126">**網域帳戶** - 必須在前端節點上以本機系統管理員權限設定此帳戶，才能安裝 HPC Pack。</span><span class="sxs-lookup"><span data-stu-id="fea7a-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="fea7a-127">**連接埠 443 上的 TCP 連線** 。</span><span class="sxs-lookup"><span data-stu-id="fea7a-127">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="fea7a-128">在前端節點安裝 HPC Pack</span><span class="sxs-lookup"><span data-stu-id="fea7a-128">Install HPC Pack on the head node</span></span>
<span data-ttu-id="fea7a-129">您必須先在執行 Windows Server 的內部部署電腦上安裝 Microsoft HPC Pack。</span><span class="sxs-lookup"><span data-stu-id="fea7a-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="fea7a-130">此電腦會成為叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-130">This computer becomes the head node of the cluster.</span></span>

1. <span data-ttu-id="fea7a-131">使用具備本機系統管理員權限的網域帳戶登入前端節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-131">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="fea7a-132">執行 HPC Pack 安裝檔中的 Setup.exe 來啟動 HPC Pack 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="fea7a-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>

3. <span data-ttu-id="fea7a-133">在 [HPC Pack 2012 R2 設定] 畫面上，按一下 [全新安裝或將新功能新增至現有安裝]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>

    ![HPC Pack 2012 Setup][install_hpc1]

4. <span data-ttu-id="fea7a-135">在 [Microsoft 軟體使用者合約] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-135">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="fea7a-136">在 [選取安裝類型] 頁面上，按一下 [藉由建立前端節點來建立新 HPC 叢集]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="fea7a-137">精靈會執行數項安裝前的測試。</span><span class="sxs-lookup"><span data-stu-id="fea7a-137">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="fea7a-138">如果所有測試皆通過，請在 [安裝規則]  on the  。</span><span class="sxs-lookup"><span data-stu-id="fea7a-138">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="fea7a-139">否則，請檢閱系統提供的資訊，並在您的環境中進行任何必要的變更。</span><span class="sxs-lookup"><span data-stu-id="fea7a-139">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="fea7a-140">然後重新執行測試，或是視需要重新啟動安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="fea7a-140">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
7. <span data-ttu-id="fea7a-141">在 [HPC DB 設定] 頁面上，確定已為所有 HPC 資料庫選取 [前端節點]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB Configuration][install_hpc4]

8. <span data-ttu-id="fea7a-143">接受精靈剩餘頁面上的預設選項。</span><span class="sxs-lookup"><span data-stu-id="fea7a-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="fea7a-144">在 [安裝必要元件] 頁面上，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Install][install_hpc6]

9. <span data-ttu-id="fea7a-146">安裝完成之後，請取消勾選 [啟動 HPC 叢集管理員]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="fea7a-147">(您將在稍後的步驟中啟動 HPC 叢集管理員)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![完成][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="fea7a-149">準備 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="fea7a-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="fea7a-150">在 [Azure 入口網站](https://portal.azure.com)中對您的 Azure 訂用帳戶執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fea7a-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="fea7a-151">完成這些步驟之後，您就可以從內部部署前端節點部署 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="fea7a-152">請一併記下您的 Azure 訂用帳戶識別碼，稍後需要用到。</span><span class="sxs-lookup"><span data-stu-id="fea7a-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="fea7a-153">您可以在入口網站的 [訂用帳戶] 中找到此識別碼。</span><span class="sxs-lookup"><span data-stu-id="fea7a-153">Find the ID in **Subscriptions** in the portal.</span></span>
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="fea7a-154">上傳預設管理憑證</span><span class="sxs-lookup"><span data-stu-id="fea7a-154">Upload the default management certificate</span></span>
<span data-ttu-id="fea7a-155">HPC Pack 會在前端節點安裝一個自我簽署憑證 (稱為 Default Microsoft HPC Azure Management 憑證)，您可以將它上傳作為 Azure 管理憑證。</span><span class="sxs-lookup"><span data-stu-id="fea7a-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="fea7a-156">這個憑證是為了方便進行測試及概念證明部署而提供，可保護前端節點與 Azure 之間的連線安全。</span><span class="sxs-lookup"><span data-stu-id="fea7a-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span></span>

1. <span data-ttu-id="fea7a-157">從前端節點電腦登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="fea7a-158">按一下 [訂用帳戶] > 您的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="fea7a-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="fea7a-159">按一下 [管理憑證] > [上傳]。4.</span><span class="sxs-lookup"><span data-stu-id="fea7a-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="fea7a-160">瀏覽前端節點以找出 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="fea7a-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="fea7a-161">然後，按一下 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="fea7a-162">[Default HPC Azure Management] \(預設 HPC Azure 管理) 憑證會顯示在管理憑證清單中。</span><span class="sxs-lookup"><span data-stu-id="fea7a-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="fea7a-163">建立 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="fea7a-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="fea7a-164">為了獲得最佳效能，請在稍後的步驟中，將雲端服務和儲存體帳戶建立在同一個地理區域中。</span><span class="sxs-lookup"><span data-stu-id="fea7a-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="fea7a-165">在入口網站中，按一下 [雲端服務 (傳統)] > [+新增]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-165">In the portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="fea7a-166">鍵入服務的 DNS 名稱，選擇資源群組和位置，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="fea7a-167">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fea7a-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="fea7a-168">在入口網站中，按一下 [儲存體帳戶 (傳統)] > [+新增]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="fea7a-169">鍵入帳戶的名稱，然後選取 [傳統] 部署模型。</span><span class="sxs-lookup"><span data-stu-id="fea7a-169">Type a name for the account, and select the **Classic** deployment model.</span></span>

3. <span data-ttu-id="fea7a-170">選擇資源群組和位置，並保留其他設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="fea7a-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="fea7a-171">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-171">Then click **Create**.</span></span>

## <a name="configure-the-head-node"></a><span data-ttu-id="fea7a-172">設定前端節點</span><span class="sxs-lookup"><span data-stu-id="fea7a-172">Configure the head node</span></span>
<span data-ttu-id="fea7a-173">若要使用 HPC 叢集管理員來部署 Azure 節點及提交工作，請先執行一些必要的叢集設定步驟。</span><span class="sxs-lookup"><span data-stu-id="fea7a-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="fea7a-174">在前端節點上，啟動 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="fea7a-174">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="fea7a-175">如果顯示 [選取前端節點] 對話方塊，請按一下 [本機電腦]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="fea7a-176">[Deployment To-do List]  隨即出現。</span><span class="sxs-lookup"><span data-stu-id="fea7a-176">The **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="fea7a-177">在 [必要部署工作] 底下，按一下 [設定您的網路]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configure Network][config_hpc2]

3. <span data-ttu-id="fea7a-179">在 [網路設定精靈] 中，選取 [All nodes only on an enterprise network]  \(拓撲 5)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="fea7a-180">這是最簡單的網路設定，僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="fea7a-180">This network configuration is the simplest for demonstration purposes.</span></span>
   
    ![Topology 5][config_hpc3]
   
4. <span data-ttu-id="fea7a-182">按 [下一步]  以接受精靈剩餘頁面上的預設值。</span><span class="sxs-lookup"><span data-stu-id="fea7a-182">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="fea7a-183">然後，在 [檢閱] 索引標籤上，按一下 [設定] 以完成網路設定。</span><span class="sxs-lookup"><span data-stu-id="fea7a-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>

5. <span data-ttu-id="fea7a-184">在 [部署待辦事項清單] 中，按一下 [提供安裝認證]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="fea7a-185">在 [Installation Credentials]  對話方塊中，輸入您用來安裝 HPC Pack 之網域帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="fea7a-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="fea7a-186">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fea7a-186">Then click **OK**.</span></span> 
   
    ![Installation Credentials][config_hpc6]
   
7. <span data-ttu-id="fea7a-188">在 [部署待辦事項清單] 中，按一下 [設定新節點的命名]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>

8. <span data-ttu-id="fea7a-189">在 [指定節點命名序列] 對話方塊中，接受預設的命名序列，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span> <span data-ttu-id="fea7a-190">請完成這個步驟，即使您在本教學課程中新增的 Azure 節點會自動命名也一樣。</span><span class="sxs-lookup"><span data-stu-id="fea7a-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Node Naming][config_hpc8]
   
9. <span data-ttu-id="fea7a-192">在 [部署待辦事項清單] 中，按一下 [建立節點範本]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-192">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="fea7a-193">在本教學課程稍後，您可以使用節點範本將 Azure 節點新增至叢集。</span><span class="sxs-lookup"><span data-stu-id="fea7a-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span></span>

10. <span data-ttu-id="fea7a-194">在 [Create Node Template Wizard] 中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="fea7a-194">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="fea7a-195">a.</span><span class="sxs-lookup"><span data-stu-id="fea7a-195">a.</span></span> <span data-ttu-id="fea7a-196">在 [選擇節點範本類型] 頁面上，按一下 [Windows Azure 節點範本]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Node Template][config_hpc10]
    
    <span data-ttu-id="fea7a-198">b.</span><span class="sxs-lookup"><span data-stu-id="fea7a-198">b.</span></span> <span data-ttu-id="fea7a-199">按 [下一步] 以接受預設範本名稱。</span><span class="sxs-lookup"><span data-stu-id="fea7a-199">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="fea7a-200">c.</span><span class="sxs-lookup"><span data-stu-id="fea7a-200">c.</span></span> <span data-ttu-id="fea7a-201">然後，在 [管理憑證]  。</span><span class="sxs-lookup"><span data-stu-id="fea7a-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="fea7a-202">然後，在 [管理憑證] 中，瀏覽 [預設 Microsoft HPC Azure 管理]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="fea7a-203">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="fea7a-203">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc12]
    
    <span data-ttu-id="fea7a-205">d.</span><span class="sxs-lookup"><span data-stu-id="fea7a-205">d.</span></span> <span data-ttu-id="fea7a-206">在 [提供服務資訊] 頁面上，選取您在先前步驟中建立的雲端服務和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fea7a-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="fea7a-207">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="fea7a-207">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc13]
    
    <span data-ttu-id="fea7a-209">e.</span><span class="sxs-lookup"><span data-stu-id="fea7a-209">e.</span></span> <span data-ttu-id="fea7a-210">按 [下一步]  以接受精靈剩餘頁面上的預設值。</span><span class="sxs-lookup"><span data-stu-id="fea7a-210">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="fea7a-211">然後，在 [檢閱] 索引標籤上，按一下 [建立] 以建立節點範本。</span><span class="sxs-lookup"><span data-stu-id="fea7a-211">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fea7a-212">根據預設，Azure 節點範本包含可讓您使用 HPC 叢集管理員手動啟動 (佈建) 和停止節點的設定。</span><span class="sxs-lookup"><span data-stu-id="fea7a-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="fea7a-213">您可以選擇性地設定排程來自動啟動和停止 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="fea7a-214">將 Azure 節點新增至叢集</span><span class="sxs-lookup"><span data-stu-id="fea7a-214">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="fea7a-215">現在使用節點範本將 Azure 節點新增至叢集。</span><span class="sxs-lookup"><span data-stu-id="fea7a-215">Now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="fea7a-216">將節點新增至叢集會儲存其設定資訊，讓您可以隨時在雲端服務中啟動 (佈建) 這些節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span></span> <span data-ttu-id="fea7a-217">在執行個體於雲端服務中執行之後，您的訂用帳戶才須為 Azure 節點付費。</span><span class="sxs-lookup"><span data-stu-id="fea7a-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span></span>

<span data-ttu-id="fea7a-218">請遵循下列步驟來新增兩個小型節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-218">Follow these steps to add two Small nodes.</span></span>

1. <span data-ttu-id="fea7a-219">在 HPC 叢集管理員中，按一下 [節點管理] \(在最新版本的 HPC Pack 中稱為 [資源管理]) > [新增節點]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Add Node][add_node1]

2. <span data-ttu-id="fea7a-221">在「新增節點精靈」中的 [選取部署方法] 頁面上，按一下 [新增 Windows Azure 節點]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Add Azure Node][add_node1_1]

3. <span data-ttu-id="fea7a-223">在 [指定新節點] 頁面上，選取您先前建立的 Azure 節點範本 (預設稱為 [預設 Azure 節點範本])。</span><span class="sxs-lookup"><span data-stu-id="fea7a-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="fea7a-224">接著，指定 **2** 個大小為 [小型] 的節點，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Specify Nodes][add_node2]
   
4. <span data-ttu-id="fea7a-226">在 [完成新增節點精靈] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="fea7a-227">HPC 叢集管理員中現在會出現兩個 Azure 節點，名為 **AzureCN-0001** 和 **AzureCN-0002**。</span><span class="sxs-lookup"><span data-stu-id="fea7a-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="fea7a-228">兩者皆處於 [未部署]  狀態。</span><span class="sxs-lookup"><span data-stu-id="fea7a-228">Both are in the **Not-Deployed** state.</span></span>
   
    ![Added Nodes][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="fea7a-230">啟動 Azure 節點</span><span class="sxs-lookup"><span data-stu-id="fea7a-230">Start the Azure nodes</span></span>
<span data-ttu-id="fea7a-231">當您想要使用 Azure 中的叢集資源時，請使用 HPC 叢集管理員來啟動 (佈建) Azure 節點並讓節點上線。</span><span class="sxs-lookup"><span data-stu-id="fea7a-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="fea7a-232">在 HPC 叢集管理員中，按一下 [節點管理] \(在最新版本的 HPC Pack 中稱為 [資源管理])，然後選取 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span></span>

2. <span data-ttu-id="fea7a-233">按一下 [開始]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Start Nodes][add_node4]
   
    <span data-ttu-id="fea7a-235">節點會轉換至 [正在佈建]  狀態。</span><span class="sxs-lookup"><span data-stu-id="fea7a-235">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="fea7a-236">檢視佈建記錄檔以追蹤佈建進度。</span><span class="sxs-lookup"><span data-stu-id="fea7a-236">View the provisioning log to track the provisioning progress.</span></span>
   
    ![Provision Nodes][add_node6]

3. <span data-ttu-id="fea7a-238">幾分鐘之後，Azure 節點就會完成佈建並處於 [離線]  狀態。</span><span class="sxs-lookup"><span data-stu-id="fea7a-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="fea7a-239">在此狀態下，角色執行個體已在執行，但還沒準備要接受叢集作業。</span><span class="sxs-lookup"><span data-stu-id="fea7a-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="fea7a-240">若要確認角色執行個體已在執行，請在 Azure 入口網站中按一下 [雲端服務 (傳統)] > 您的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="fea7a-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="fea7a-241">您應該看到兩個 **HpcWorkerRole** 執行個體 (節點) 已在服務中執行。</span><span class="sxs-lookup"><span data-stu-id="fea7a-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span></span> <span data-ttu-id="fea7a-242">HPC Pack 也會自動部署兩個 **HpcProxy** 執行個體 (中型大小) 以處理前端節點與 Azure 之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="fea7a-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>

   ![Running Instances][view_instances1]

5. <span data-ttu-id="fea7a-244">若要讓 Azure 節點上線以執行叢集工作，請選取節點，按一下滑鼠右鍵，然後按一下 [上線] 。</span><span class="sxs-lookup"><span data-stu-id="fea7a-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Offline Nodes][add_node7]
   
    <span data-ttu-id="fea7a-246">HPC 叢集管理員會指出節點處於 [線上]  狀態。</span><span class="sxs-lookup"><span data-stu-id="fea7a-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="fea7a-247">在叢集執行命令</span><span class="sxs-lookup"><span data-stu-id="fea7a-247">Run a command across the cluster</span></span>
<span data-ttu-id="fea7a-248">若要追蹤安裝，請使用 HPC Pack **clusrun** 命令在一或多個叢集節點上執行命令或應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea7a-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="fea7a-249">其中一個簡單的範例就是使用 **clusrun** 來取得 Azure 節點的 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="fea7a-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="fea7a-250">在前端節點上，以系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="fea7a-250">On the head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="fea7a-251">輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="fea7a-251">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="fea7a-252">出現提示時，輸入您的叢集系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="fea7a-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="fea7a-253">您應該會看到如下所示的命令輸出。</span><span class="sxs-lookup"><span data-stu-id="fea7a-253">You should see command output similar to the following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="fea7a-255">執行測試工作</span><span class="sxs-lookup"><span data-stu-id="fea7a-255">Run a test job</span></span>
<span data-ttu-id="fea7a-256">現在提交一個在混合式叢集上執行的測試作業。</span><span class="sxs-lookup"><span data-stu-id="fea7a-256">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="fea7a-257">這個範例是簡單的參數式掃掠作業 (一種本質平行計算)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="fea7a-258">本例會執行使用 **set /a** 命令將整數加入自己本身的子工作。</span><span class="sxs-lookup"><span data-stu-id="fea7a-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="fea7a-259">叢集中的所有節點皆參與完成從 1 到 100 之整數的子工作。</span><span class="sxs-lookup"><span data-stu-id="fea7a-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="fea7a-260">在 HPC 叢集管理員中，按一下 [作業管理] > [New Parametric Sweep Job] \(新增參數式掃掠作業)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![New Job][test_job1]

2. <span data-ttu-id="fea7a-262">在 [新增參數式掃掠作業] 對話方塊中，於 [命令列] 中輸入 `set /a *+*` (覆寫出現的預設命令列)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="fea7a-263">保留其餘設定的預設值，然後按一下 [提交]  提交工作。</span><span class="sxs-lookup"><span data-stu-id="fea7a-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![Parametric Sweep][param_sweep1]

3. <span data-ttu-id="fea7a-265">當工作完成時，按兩下 [My Sweep Task]  工作。</span><span class="sxs-lookup"><span data-stu-id="fea7a-265">When the job is finished, double-click the **My Sweep Task** job.</span></span>

4. <span data-ttu-id="fea7a-266">按一下 [檢視工作] ，然後按一下子工作以檢視該子工作的計算結果輸出。</span><span class="sxs-lookup"><span data-stu-id="fea7a-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![Task Results][view_job361]

5. <span data-ttu-id="fea7a-268">若要查看是哪個節點執行該子工作的計算，請按一下 [已配置的節點]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="fea7a-269">(您的叢集可能會顯示不同的節點名稱。)</span><span class="sxs-lookup"><span data-stu-id="fea7a-269">(Your cluster might show a different node name.)</span></span>
   
    ![Task Results][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="fea7a-271">停止 Azure 節點</span><span class="sxs-lookup"><span data-stu-id="fea7a-271">Stop the Azure nodes</span></span>
<span data-ttu-id="fea7a-272">試驗完叢集之後，請停止 Azure 節點，以避免給您的帳戶產生不必要的費用。</span><span class="sxs-lookup"><span data-stu-id="fea7a-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="fea7a-273">這個步驟會停止雲端服務並移除 Azure 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="fea7a-273">This step stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="fea7a-274">在 HPC 叢集管理員中，於 [節點管理] \(在舊版的 HPC Pack 中稱為 [資源管理]) 中，選取這兩個 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="fea7a-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="fea7a-275">然後，按一下 [停止]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-275">Then, click **Stop**.</span></span>
   
    ![Stop Nodes][stop_node1]

2. <span data-ttu-id="fea7a-277">在 [停止 Windows Azure 節點] 對話方塊中，按一下 [停止]。</span><span class="sxs-lookup"><span data-stu-id="fea7a-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="fea7a-278">節點會轉換至 [正在停止]  狀態。</span><span class="sxs-lookup"><span data-stu-id="fea7a-278">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="fea7a-279">幾分鐘之後，HPC 叢集管理員就會顯示這些節點為 [未部署] 狀態。</span><span class="sxs-lookup"><span data-stu-id="fea7a-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![Not Deployed Nodes][stop_node4]

4. <span data-ttu-id="fea7a-281">若要確認角色執行個體已不再於 Azure 中執行，請在 Azure 入口網站中按一下 [雲端服務 (傳統)] > 您的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="fea7a-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="fea7a-282">不會有任何執行個體部署於生產環境中。</span><span class="sxs-lookup"><span data-stu-id="fea7a-282">No instances are deployed in the production environment.</span></span> 
   
    <span data-ttu-id="fea7a-283">這樣就完成了教學課程。</span><span class="sxs-lookup"><span data-stu-id="fea7a-283">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fea7a-284">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fea7a-284">Next steps</span></span>
* <span data-ttu-id="fea7a-285">瀏覽 [HPC Pack](https://technet.microsoft.com/library/cc514029) 文件。</span><span class="sxs-lookup"><span data-stu-id="fea7a-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="fea7a-286">若要設定較大規模的混合式 HPC Pack 叢集部署，請參閱 [Burst to Azure with Microsoft HPC Pack (使用 Microsoft HPC Pack 高載至 Azure 背景工作角色執行個體)](http://go.microsoft.com/fwlink/p/?LinkID=200493)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="fea7a-287">如需在 Azure 中建立 HPC Pack 叢集的其他方式，包括使用 Azure Resource Manager 範本，請參閱[使用 HPC Pack 在 Azure 中建立及管理 Windows HPC 叢集的選項](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fea7a-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


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
