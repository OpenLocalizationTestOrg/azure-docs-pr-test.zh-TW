---
title: "將 Azure SQL Server 虛擬機器設定為 IPython Notebook 伺服器 | Microsoft Docs"
description: "使用 SQL Server 和 IPython Server 來設定資料科學虛擬機器。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 8a151a6a15d4d000a774e3ec4e38bfa0e58ca33b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a><span data-ttu-id="133a0-103">將 Azure SQL Server 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用</span><span class="sxs-lookup"><span data-stu-id="133a0-103">Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics</span></span>
<span data-ttu-id="133a0-104">本主題示範如何佈建及設定 SQL Server 虛擬機器，以用來做為雲端架構資料科學環境的一部分。</span><span class="sxs-lookup"><span data-stu-id="133a0-104">This topic shows how to provision and configure an SQL Server virtual machine to be used as part of a cloud-based data science environment.</span></span> <span data-ttu-id="133a0-105">Windows 虛擬機器是使用支援工具 (例如，IPython Notebook、Azure 儲存體總管及 AzCopy)，以及其他對於資料科學專案非常實用的公用程式來設定。</span><span class="sxs-lookup"><span data-stu-id="133a0-105">The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, and AzCopy, as well as other utilities that are useful for data science projects.</span></span> <span data-ttu-id="133a0-106">例如，Azure 儲存體總管和 AzCopy 會提供便利的方法，將資料從本機電腦上傳至 Azure Blob 儲存體，或者從 Blob 儲存體將資料下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="133a0-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure blob storage from your local machine or to download it to your local machine from blob storage.</span></span>

<span data-ttu-id="133a0-107">Azure 虛擬機器組件庫涵蓋數個包含 Microsoft SQL Server 的映像。</span><span class="sxs-lookup"><span data-stu-id="133a0-107">The Azure virtual machine gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="133a0-108">選取適合您資料需求的 SQL Server VM 映像。</span><span class="sxs-lookup"><span data-stu-id="133a0-108">Select an SQL Server VM image that is suitable for your data needs.</span></span> <span data-ttu-id="133a0-109">建議的映像如下：</span><span class="sxs-lookup"><span data-stu-id="133a0-109">Recommended images are:</span></span>

* <span data-ttu-id="133a0-110">SQL Server 2012 SP2 Enterprise，適用於小型到中型的資料大小</span><span class="sxs-lookup"><span data-stu-id="133a0-110">SQL Server 2012 SP2 Enterprise for small to medium data sizes</span></span>
* <span data-ttu-id="133a0-111">SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads，適用於大型到非常大型的資料大小</span><span class="sxs-lookup"><span data-stu-id="133a0-111">SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads for large to very large data sizes</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="133a0-112">SQL Server 2012 SP2 Enterprise 的映像 **不包含資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="133a0-112">SQL Server 2012 SP2 Enterprise image **does not include a data disk**.</span></span> <span data-ttu-id="133a0-113">您必須新增和 (或) 連接一或多個虛擬硬碟來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="133a0-113">You will need to add and/or attach one or more virtual hard disks to store your data.</span></span> <span data-ttu-id="133a0-114">當您建立 Azure 虛擬機器時，它會有一個作業系統的磁碟對應至 C 磁碟機，還有一個暫存磁碟對應至 D 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="133a0-114">When you create an Azure virtual machine, it has a disk for the operating system mapped to the C drive and a temporary disk mapped to the D drive.</span></span> <span data-ttu-id="133a0-115">請勿使用 D 磁碟機來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="133a0-115">Do not use the D drive to store data.</span></span> <span data-ttu-id="133a0-116">顧名思義，它只提供暫存儲存空間。</span><span class="sxs-lookup"><span data-stu-id="133a0-116">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="133a0-117">它並不提供備援或備份，因為它不在 Azure 儲存體內。</span><span class="sxs-lookup"><span data-stu-id="133a0-117">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
  > 
  > 

## <span data-ttu-id="133a0-118"><a name="Provision"></a>連線到 Azure 傳統入口網站並佈建 SQL Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="133a0-118"><a name="Provision"></a>Connect to the Azure Classic Portal and provision an SQL Server virtual machine</span></span>
1. <span data-ttu-id="133a0-119">使用您的帳戶登入 [Azure 傳統入口網站](http://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="133a0-119">Log in to the [Azure Classic portal](http://manage.windowsazure.com/) using your account.</span></span>
   <span data-ttu-id="133a0-120">如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="133a0-120">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="133a0-121">在 Azure 傳統入口網站中，依序按一下網頁左下角的 [+新增]、[計算]、[虛擬機器] 和 [從資源庫]。</span><span class="sxs-lookup"><span data-stu-id="133a0-121">On the Azure Classic portal, at the bottom left of the web page, click **+NEW**, click **COMPUTE**, click **VIRTUAL MACHINE**, and then click **FROM GALLERY**.</span></span>
3. <span data-ttu-id="133a0-122">在「 **建立虛擬機器** 」頁面上，根據您的資料需求選取包含 SQL Server 的虛擬機器映像，然後按一下頁面右下角的 [下一步] 箭號。</span><span class="sxs-lookup"><span data-stu-id="133a0-122">On the **Create a Virtual Machine** page, select a virtual machine image containing SQL Server based on your data needs, and then click the next arrow at the bottom right of the page.</span></span> <span data-ttu-id="133a0-123">如需 Azure 支援之 SQL Server 映像的最新資訊，請參閱 [Azure 虛擬機器中的 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294719) 文件集內的[開始使用 Azure 虛擬機器中的 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294720) 主題。</span><span class="sxs-lookup"><span data-stu-id="133a0-123">For the most up-to-date information on the supported SQL Server images on Azure, see [Getting Started with SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294720) topic in the [SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294719) documentation set.</span></span>
   
   ![選取 SQL Server VM][1]
4. <span data-ttu-id="133a0-125">在第一個 [ **虛擬機器組態** ] 頁面，請提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="133a0-125">On the first **Virtual Machine Configuration** page, provide the following information:</span></span>
   
   * <span data-ttu-id="133a0-126">提供 [虛擬機器名稱] 。</span><span class="sxs-lookup"><span data-stu-id="133a0-126">Provide a **VIRTUAL MACHINE NAME**.</span></span>
   * <span data-ttu-id="133a0-127">在 [新使用者名稱]  方塊中，輸入 VM 本機系統管理員帳戶的唯一使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="133a0-127">In the **NEW USER NAME** box, type unique user name for the VM local administrator account.</span></span>
   * <span data-ttu-id="133a0-128">在 [ **新增密碼** ] 方塊中，輸入增強式密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-128">In the **NEW PASSWORD** box, type a strong password.</span></span> <span data-ttu-id="133a0-129">如需詳細資訊，請參閱 [增強式密碼](http://msdn.microsoft.com/library/ms161962.aspx)。</span><span class="sxs-lookup"><span data-stu-id="133a0-129">For more information, see [Strong Passwords](http://msdn.microsoft.com/library/ms161962.aspx).</span></span>
   * <span data-ttu-id="133a0-130">在 [ **確認密碼** ] 方塊中，重新輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-130">In the **CONFIRM PASSWORD** box, retype the password.</span></span>
   * <span data-ttu-id="133a0-131">從 [大小]  下拉式清單中選取適當的大小。</span><span class="sxs-lookup"><span data-stu-id="133a0-131">Select the appropriate **SIZE** from the drop down list.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="133a0-132">在佈建期間指定虛擬機器的大小：A2 是建議用於生產工作負載的最小大小。</span><span class="sxs-lookup"><span data-stu-id="133a0-132">The size of the virtual machine is specified during provisioning: A2 is the smallest size recommended for production workloads.</span></span> <span data-ttu-id="133a0-133">使用 SQL Server Enterprise Edition 時，虛擬機器的最小建議大小為 A3。</span><span class="sxs-lookup"><span data-stu-id="133a0-133">The minimum recommended size for a virtual machine is A3 when using SQL Server Enterprise Edition.</span></span> <span data-ttu-id="133a0-134">當您使用 SQL Server Enterprise Edition 時，請選取 A3 或以上的大小。</span><span class="sxs-lookup"><span data-stu-id="133a0-134">Select A3 or higher when using SQL Server Enterprise Edition.</span></span> <span data-ttu-id="133a0-135">使用 SQL Server 2012 或 2014 Enterprise Optimized for Transactional Workloads 映像時，請選取 A4。</span><span class="sxs-lookup"><span data-stu-id="133a0-135">Select A4 when using SQL Server 2012 or 2014 Enterprise Optimized for Transactional Workloads images.</span></span>
     > <span data-ttu-id="133a0-136">使用 SQL Server 2012 或 2014 Enterprise Optimized for Data Warehousing Workloads 映像時，請選取 A7。</span><span class="sxs-lookup"><span data-stu-id="133a0-136">Select A7 when using SQL Server 2012 or 2014 Enterprise Optimized for Data Warehousing Workloads images.</span></span> <span data-ttu-id="133a0-137">選取的大小會限制可設定的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="133a0-137">The size selected limits the number of data disks you can configure.</span></span> <span data-ttu-id="133a0-138">如需可用之虛擬機器大小和可連接至虛擬機器之資料磁碟數目的最新資訊，請參閱 [虛擬機器](http://msdn.microsoft.com/library/azure/dn197896.aspx)。</span><span class="sxs-lookup"><span data-stu-id="133a0-138">For most up-to-date information on available virtual machine sizes and the number of data disks that you can attach to a virtual machine, see [Virtual Machine Sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="133a0-139">如需定價資訊，請參閱「 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)」。</span><span class="sxs-lookup"><span data-stu-id="133a0-139">For pricing information, see [VIrtual Macines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
     > 
     > 
   
   <span data-ttu-id="133a0-140">按一下右下角的 [下一步] 箭頭以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="133a0-140">Click the next arrow on the bottom right to continue.</span></span>
   
   ![VM 組態][2]
5. <span data-ttu-id="133a0-142">在第二個 [虛擬機器組態]  頁面上，請設定網路、儲存體和可用性的資源：</span><span class="sxs-lookup"><span data-stu-id="133a0-142">On the second **Virtual machine configuration** page, configure resources for networking, storage, and availability:</span></span>
   
   * <span data-ttu-id="133a0-143">在 [雲端服務] 方塊中，選擇 [建立新的雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="133a0-143">In the **Cloud Service** box, choose **Create a new cloud service**.</span></span>
   * <span data-ttu-id="133a0-144">在 [雲端服務 DNS 名稱] 方塊中，提供選擇之 DNS 名稱的第一個部分，使其形成 **TESTNAME.cloudapp.net** 格式的名稱</span><span class="sxs-lookup"><span data-stu-id="133a0-144">In the **Cloud Service DNS Name** box, provide the first portion of a DNS name of your choice, so that it completes a name in the format **TESTNAME.cloudapp.net**</span></span>
   * <span data-ttu-id="133a0-145">在 [REGION/AFFINITY GROUP/VIRTUAL NETWORK]  方塊中，選取代管這個虛擬映像的所在區域。</span><span class="sxs-lookup"><span data-stu-id="133a0-145">In the **REGION/AFFINITY GROUP/VIRTUAL NETWORK** box, select a region where this virtual image will be hosted.</span></span>
   * <span data-ttu-id="133a0-146">在 [儲存體帳戶] 中，選取現有的儲存體帳戶或選取自動產生的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="133a0-146">In the **Storage Account**, select an existing storage account or select an automatically generated one.</span></span>
   * <span data-ttu-id="133a0-147">在 [可用性設定組] 方塊中，選取 [(無)]。</span><span class="sxs-lookup"><span data-stu-id="133a0-147">In the **AVAILABILITY SET** box, select **(none)**.</span></span>
   * <span data-ttu-id="133a0-148">閱讀並接受定價資訊。</span><span class="sxs-lookup"><span data-stu-id="133a0-148">Read and accept the pricing information.</span></span>
6. <span data-ttu-id="133a0-149">在 [端點] 區段中，按一下 [名稱] 底下的空白下拉式清單並選取 [MSSQL]，然後鍵入 Database Engine 執行個體的連接埠號碼 (預設執行個體的連接埠號碼是 **1433**)。</span><span class="sxs-lookup"><span data-stu-id="133a0-149">In the **ENDPOINTS** section, click in the empty dropdown under **NAME**, and select **MSSQL**  then type the port number of the instance of the Database Engine (**1433** for the default instance).</span></span>
7. <span data-ttu-id="133a0-150">您的 SQL Server VM 也可以用來做為 IPython Notebook 伺服器 (將在稍後步驟中設定)。</span><span class="sxs-lookup"><span data-stu-id="133a0-150">Your SQL Server VM can also serve as an IPython Notebook Server, which will be configured in a later step.</span></span>
   <span data-ttu-id="133a0-151">新增端點以指定可供 IPython Notebook 伺服器使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="133a0-151">Add a new endpoint to specify the port to use for your IPython Notebook server.</span></span> <span data-ttu-id="133a0-152">在 [名稱] 資料行中，輸入名稱，並選取您為公用連接埠選擇的連接埠號碼，然後針對私用連接埠選取 9999。</span><span class="sxs-lookup"><span data-stu-id="133a0-152">Enter a name in the **NAME** column,    select a port number of your choice for the public port, and 9999 for the private port.</span></span>
   
   <span data-ttu-id="133a0-153">按一下右下角的 [下一步] 箭頭以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="133a0-153">Click the next arrow on the bottom right to continue.</span></span>
   
   ![選取 MSSQL 和 IPython 連接埠][3]
8. <span data-ttu-id="133a0-155">接受已選取的預設 [ **安裝 VM 代理程式** ] 選項，然後按一下精靈右下角的核取記號，完成 VM 佈建程序。</span><span class="sxs-lookup"><span data-stu-id="133a0-155">Accept the default **Install VM agent** option checked and click the the check mark in the bottom right corner of the wizard to complete the VM provisioning process.</span></span>
   
   `![VM 的最後選項][4]
9. <span data-ttu-id="133a0-157">等待 Azure 準備好您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="133a0-157">Wait while Azure prepares your virtual machine.</span></span> <span data-ttu-id="133a0-158">虛擬機器應該會依序經歷以下狀態變更：</span><span class="sxs-lookup"><span data-stu-id="133a0-158">Expect the virtual machine status to proceed through:</span></span>
   
   * <span data-ttu-id="133a0-159">啟動中 (佈建中)</span><span class="sxs-lookup"><span data-stu-id="133a0-159">Starting (Provisioning)</span></span>
   * <span data-ttu-id="133a0-160">已停止</span><span class="sxs-lookup"><span data-stu-id="133a0-160">Stopped</span></span>
   * <span data-ttu-id="133a0-161">啟動中 (佈建中)</span><span class="sxs-lookup"><span data-stu-id="133a0-161">Starting (Provisioning)</span></span>
   * <span data-ttu-id="133a0-162">執行中 (佈建中)</span><span class="sxs-lookup"><span data-stu-id="133a0-162">Running (Provisioning)</span></span>
   * <span data-ttu-id="133a0-163">執行中</span><span class="sxs-lookup"><span data-stu-id="133a0-163">Running</span></span>

## <span data-ttu-id="133a0-164"><a name="RemoteDesktop"></a>使用遠端桌面開啟虛擬機器並完成設定</span><span class="sxs-lookup"><span data-stu-id="133a0-164"><a name="RemoteDesktop"></a>Open the virtual machine using Remote Desktop and complete setup</span></span>
1. <span data-ttu-id="133a0-165">佈建完成時，請按一下虛擬機器的名稱以前往 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="133a0-165">When provisioning completes, click on the name of your virtual machine to go to the DASHBOARD page.</span></span> <span data-ttu-id="133a0-166">按一下頁面底部的 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="133a0-166">At the bottom of the page, click **Connect**.</span></span>
2. <span data-ttu-id="133a0-167">選擇使用 Windows 遠端桌面程式 (`%windir%\system32\mstsc.exe`) 開啟 rpd 檔案。</span><span class="sxs-lookup"><span data-stu-id="133a0-167">Choose to open the rpd file using the Windows Remote Desktop program (`%windir%\system32\mstsc.exe`).</span></span>
3. <span data-ttu-id="133a0-168">在 [Windows 安全性] 對話方塊中，提供在先前步驟中指定的本機系統管理員帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-168">At the **Windows Security** dialog box, provide the password for the local administrator account that you specified in an earlier step.</span></span>
   <span data-ttu-id="133a0-169">(系統可能會要求您確認虛擬機器的認證。)</span><span class="sxs-lookup"><span data-stu-id="133a0-169">(You might be asked to verify the credentials of the virtual machine.)</span></span>
4. <span data-ttu-id="133a0-170">當您第一次登入這個虛擬機器時，可能需要完成數個程序，包括設定桌面、Windows Update，以及完成 Windows 初始組態工作 (sysprep)。</span><span class="sxs-lookup"><span data-stu-id="133a0-170">The first time you log on to this virtual machine, several processes may need to complete, including setup of your desktop, Windows updates, and completion of the Windows initial configuration tasks (sysprep).</span></span> <span data-ttu-id="133a0-171">待 Windows sysprep 完成後，SQL Server 安裝程式會完成組態工作。</span><span class="sxs-lookup"><span data-stu-id="133a0-171">After Windows sysprep completes, SQL Server setup completes configuration tasks.</span></span> <span data-ttu-id="133a0-172">在完成這些工作的期間，可能會造成幾分鐘的時間延遲。</span><span class="sxs-lookup"><span data-stu-id="133a0-172">These tasks may cause a delay of a few minutes while they complete.</span></span> <span data-ttu-id="133a0-173">`SELECT @@SERVERNAME` 才會傳回正確的名稱，SQL Server Management Studio 才會出現在起始畫面中。</span><span class="sxs-lookup"><span data-stu-id="133a0-173">`SELECT @@SERVERNAME` may not return the correct name until SQL Server setup completes, and SQL Server Management Studio may not be visable on the start page.</span></span>

<span data-ttu-id="133a0-174">使用 Windows 遠端桌面連接到虛擬機器之後，虛擬機器的運作方式與任何其他電腦很像。</span><span class="sxs-lookup"><span data-stu-id="133a0-174">Once you are connected to the virtual machine with Windows Remote Desktop, the virtual machine works much like any other computer.</span></span> <span data-ttu-id="133a0-175">請依照正常方法使用 SQL Server Management Studio (於虛擬機器上運作) 連接 SQL Server 的預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="133a0-175">Connect to the default instance of SQL Server with SQL Server Management Studio (running on the virtual machine) in the normal way.</span></span>

## <span data-ttu-id="133a0-176"><a name="InstallIPython"></a>安裝 IPython Notebook 和其他支援工具</span><span class="sxs-lookup"><span data-stu-id="133a0-176"><a name="InstallIPython"></a>Install IPython Notebook and other supporting tools</span></span>
<span data-ttu-id="133a0-177">若要設定新的 SQL Server VM 做為 IPython Notebook 伺服器，並安裝其他的支援工具 (例如，AzCopy、Azure 儲存體總管、實用的資料科學 Python 封裝，以及其他工具)，系統為您提供了一個特殊的自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-177">To configure your new SQL Server VM to serve as an IPython Notebook server, and install additional supporting tools such AzCopy, Azure Storage Explorer, useful Data Science Python packages, and others, a special customization script is provided to you.</span></span> <span data-ttu-id="133a0-178">若要安裝：</span><span class="sxs-lookup"><span data-stu-id="133a0-178">To install:</span></span>

1. <span data-ttu-id="133a0-179">以滑鼠右鍵按一下 Windows [開始] 圖示，然後按一下 [命令提示字元 (系統管理員)]</span><span class="sxs-lookup"><span data-stu-id="133a0-179">Right-click the **Windows Start** icon and click **Command Prompt (Admin)**</span></span>
2. <span data-ttu-id="133a0-180">複製下列命令並貼至命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="133a0-180">Copy the following commands and paste at the command prompt.</span></span>
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. <span data-ttu-id="133a0-181">出現提示時，輸入您為 IPython Notebook 伺服器選擇的密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-181">When prompted, enter a password of your choice for the IPython Notebook server.</span></span>
4. <span data-ttu-id="133a0-182">自訂指令碼會自動執行數個後續安裝程序，包括：</span><span class="sxs-lookup"><span data-stu-id="133a0-182">The customization script automates several post-install procedures, which include:</span></span>
    * <span data-ttu-id="133a0-183">安裝和設定 IPython Notebook 伺服器</span><span class="sxs-lookup"><span data-stu-id="133a0-183">Installation and setup of IPython Notebook server</span></span>
    * <span data-ttu-id="133a0-184">在稍早建立之端點的 Windows 防火牆中開啟 TCP 連接埠：</span><span class="sxs-lookup"><span data-stu-id="133a0-184">Opening TCP ports in the Windows firewall for the endpoints created earlier:</span></span>
    * <span data-ttu-id="133a0-185">適用於 SQL Server 遠端連線</span><span class="sxs-lookup"><span data-stu-id="133a0-185">For SQL Server remote connectivity</span></span>
    * <span data-ttu-id="133a0-186">適用於 IPython Notebook 伺服器遠端連線</span><span class="sxs-lookup"><span data-stu-id="133a0-186">For IPython Notebook server remote connectivity</span></span>
    * <span data-ttu-id="133a0-187">擷取 IPython Notebook 範例和 SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="133a0-187">Fetching sample IPython notebooks and SQL scripts</span></span>
    * <span data-ttu-id="133a0-188">下載並安裝實用的資料科學 Python 封裝</span><span class="sxs-lookup"><span data-stu-id="133a0-188">Downloading and installing useful Data Science Python packages</span></span>
    * <span data-ttu-id="133a0-189">下載並安裝 Azure 工具，例如 AzCopy 和 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="133a0-189">Downloading and installing Azure tools such as AzCopy and Azure Storage Explorer</span></span>  
    <br>
5. <span data-ttu-id="133a0-190">您可以使用 `https://<virtual_machine_DNS_name>:<port>`格式的 URL，從任何本機或遠端瀏覽器存取並執行 IPython Notebook，URL 格式中的 port 是您佈建虛擬機器時選取的 IPython 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="133a0-190">You may access and run IPython Notebook from any local or remote browser using a URL of the form `https://<virtual_machine_DNS_name>:<port>`, where port is the IPython public port you selected while provisioning the virtual machine.</span></span>
6. <span data-ttu-id="133a0-191">IPython Notebook 伺服器正以背景服務形式執行，而且將在您重新啟動虛擬機器時自動重新啟動。</span><span class="sxs-lookup"><span data-stu-id="133a0-191">IPython Notebook server is running as a background service and will be restarted automatically when you restart the virtual machine.</span></span>

## <span data-ttu-id="133a0-192"><a name="Optional"></a>視需要連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="133a0-192"><a name="Optional"></a>Attach data disk as needed</span></span>
<span data-ttu-id="133a0-193">如果您的 VM 映像不包含資料磁碟，亦即，磁碟不是 C 磁碟機 (作業系統磁碟) 和 D 磁碟機 (暫存磁碟)，您就需要新增一或多個資料磁碟來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="133a0-193">If your VM image does not include data disks, i.e., disks other than C drive (OS disk) and D drive (temporary disk), you need to add one or more data disks to store your data.</span></span> <span data-ttu-id="133a0-194">SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads 的 VM 映像是使用其他磁碟預先設定的，可供 SQL Server 資料和記錄檔使用。</span><span class="sxs-lookup"><span data-stu-id="133a0-194">The VM image for SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads comes pre-configured with additional disks for SQL Server data and log files.</span></span>

> [!NOTE]
> <span data-ttu-id="133a0-195">請勿使用 D 磁碟機來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="133a0-195">Do not use the D drive to store data.</span></span> <span data-ttu-id="133a0-196">顧名思義，它只提供暫存儲存空間。</span><span class="sxs-lookup"><span data-stu-id="133a0-196">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="133a0-197">它並不提供備援或備份，因為它不在 Azure 儲存體內。</span><span class="sxs-lookup"><span data-stu-id="133a0-197">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> 
> 

<span data-ttu-id="133a0-198">若要連接其他資料磁碟，請依照[如何將資料磁碟連接至 Windows 虛擬機器](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)中所述的步驟執行，這將引導您完成：</span><span class="sxs-lookup"><span data-stu-id="133a0-198">To attach additional data disks, follow the steps described in [How to Attach a Data Disk to a Windows Virtual Machine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), which will guide you through:</span></span>

1. <span data-ttu-id="133a0-199">將空磁碟連接至先前步驟中佈建的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="133a0-199">Attaching empty disk(s) to the virtual machine provisioned in earlier steps</span></span>
2. <span data-ttu-id="133a0-200">在虛擬機器中將新磁碟初始化</span><span class="sxs-lookup"><span data-stu-id="133a0-200">Initialization of the new disk(s) in the virtual machine</span></span>

## <span data-ttu-id="133a0-201"><a name="SSMS"></a>連接到 SQL Server Management Studio 並啟用混合模式驗證</span><span class="sxs-lookup"><span data-stu-id="133a0-201"><a name="SSMS"></a>Connect to SQL Server Management Studio and enable mixed mode authentication</span></span>
<span data-ttu-id="133a0-202">SQL Server Database Engine 須有網域環境才能使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="133a0-202">The SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="133a0-203">若要從另一部電腦連接 Database Engine，請設定 SQL Server 以進行混合模式驗證。</span><span class="sxs-lookup"><span data-stu-id="133a0-203">To connect to the Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="133a0-204">混合模式驗證可允許 SQL Server 驗證和 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="133a0-204">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span> <span data-ttu-id="133a0-205">需要使用 SQL 驗證模式，才能在 [Azure Machine Learning Studio](https://studio.azureml.net) 中透過「匯入資料」模組，從您的 SQL Server VM 資料庫直接擷取資料。</span><span class="sxs-lookup"><span data-stu-id="133a0-205">SQL authentication mode is required in order to ingest data directly from your SQL Server VM databases in the [Azure Machine Learning Studio](https://studio.azureml.net) using the Import Data module.</span></span>

1. <span data-ttu-id="133a0-206">使用遠端桌面連接到虛擬機器時，請在 Windows [搜尋] 窗格中輸入 **SQL Server Management Studio** (SMSS)。</span><span class="sxs-lookup"><span data-stu-id="133a0-206">While connected to the virtual machine by using Remote Desktop, use the Windows **Search** pane and type **SQL Server Management Studio** (SMSS).</span></span> <span data-ttu-id="133a0-207">按一下以啟動 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="133a0-207">Click to start the SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="133a0-208">您可能想要將捷徑新增到桌面上的 SSMS，以供日後使用。</span><span class="sxs-lookup"><span data-stu-id="133a0-208">You may want to add a shortcut to SSMS on your Desktop for future use.</span></span>
   
   ![啟動 SSMS][5]
   
   <span data-ttu-id="133a0-210">當您首次開啟 Management Studio 時，它必須建立使用者 Management Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="133a0-210">The first time you open Management Studio it must create the users Management Studio environment.</span></span> <span data-ttu-id="133a0-211">這可能需要花費幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="133a0-211">This may take a few moments.</span></span>
2. <span data-ttu-id="133a0-212">當 Management Studio 開啟時，它會顯示 [ **連接到伺服器** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="133a0-212">When opening, Management Studio presents the **Connect to Server** dialog box.</span></span> <span data-ttu-id="133a0-213">在 [ **伺服器名稱** ] 方塊中，輸入虛擬機器的名稱以利用物件總管連接 Database Engine。</span><span class="sxs-lookup"><span data-stu-id="133a0-213">In the **Server name** box, type the name of the virtual machine to connect to the Database Engine with the Object Explorer.</span></span>
   <span data-ttu-id="133a0-214">除了虛擬機器名稱之外，您還可以使用 [(本機)]，或將一個句點當做 [伺服器名稱]。</span><span class="sxs-lookup"><span data-stu-id="133a0-214">(Instead of the virtual machine name you can also use **(local)** or a single period as the **Server name**.</span></span> <span data-ttu-id="133a0-215">選取 [Windows 驗證]，並保留 [使用者名稱] 方塊中的 ***your\_VM\_name*\\your\_local\_administrator**。</span><span class="sxs-lookup"><span data-stu-id="133a0-215">Select **Windows Authentication**, and leave ***your\_VM\_name*\\your\_local\_administrator** in the **User name** box.</span></span> <span data-ttu-id="133a0-216">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="133a0-216">Click **Connect**.</span></span>
   
   ![連接到伺服器][6]
   
   <br>
   
   > [!TIP]
   > <span data-ttu-id="133a0-218">您可以使用 Windows 登錄機碼變更，或使用 SQL Server Management Studio，來變更 SQL Server 驗證模式。</span><span class="sxs-lookup"><span data-stu-id="133a0-218">You may change the SQL Server authentication mode using a Windows registry key change or using the SQL Server Management Studio.</span></span> <span data-ttu-id="133a0-219">若要使用登錄機碼變更來變更驗證模式，請啟動 [ **新增查詢** ]，然後執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="133a0-219">To change authentication mode using the registry key change, start a **New Query** and execute the following script:</span></span>
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    <span data-ttu-id="133a0-220">若要使用 SQL Server management Studio 變更驗證模式：</span><span class="sxs-lookup"><span data-stu-id="133a0-220">To change the authentication mode using SQL Server management Studio:</span></span>

1. <span data-ttu-id="133a0-221">在 **SQL Server Management Studio 物件總管**中，以滑鼠右鍵按一下 SQL Server 執行個體的名稱 (虛擬機器名稱)，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="133a0-221">In **SQL Server Management Studio Object Explorer**, right-click the name of the instance of SQL Server (the virtual machine name), and then click **Properties**.</span></span>
   
   ![伺服器屬性][7]
2. <span data-ttu-id="133a0-223">在 [安全性] 頁面的 [伺服器驗證] 下方，選取 [SQL Server 及 Windows 驗證模式]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="133a0-223">On the **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
   ![選取驗證模式][8]
3. <span data-ttu-id="133a0-225">在 [SQL Server Management Studio] 對話方塊中，按一下 [確定] 以確認重新啟動 SQL Server 的需求。</span><span class="sxs-lookup"><span data-stu-id="133a0-225">In the **SQL Server Management Studio** dialog box, click **OK** to acknowledge the requirement to restart SQL Server.</span></span>
4. <span data-ttu-id="133a0-226">在 [物件總管] 中，以滑鼠右鍵按一下伺服器，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="133a0-226">In **Object Explorer**, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="133a0-227">(如果 SQL Server Agent 處於執行狀態，您也必須將其重新啟動。)</span><span class="sxs-lookup"><span data-stu-id="133a0-227">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
   ![重新啟動][9]
5. <span data-ttu-id="133a0-229">在 [SQL Server Management Studio] 對話方塊中，按一下 [是] 以同意重新啟動 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="133a0-229">In the **SQL Server Management Studio** dialog box, click **Yes** to agree that you want to restart SQL Server.</span></span>

## <span data-ttu-id="133a0-230"><a name="Logins"></a>建立 SQL Server 驗證登入</span><span class="sxs-lookup"><span data-stu-id="133a0-230"><a name="Logins"></a>Create SQL Server authentication logins</span></span>
<span data-ttu-id="133a0-231">若要從另一部電腦連接 Database Engine，您至少必須建立一個 SQL Server 驗證登入。</span><span class="sxs-lookup"><span data-stu-id="133a0-231">To connect to the Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>  

<span data-ttu-id="133a0-232">您也可以透過程式設計方式或使用 SQL Server Management Studio，來建立新的 SQL Server 登入。</span><span class="sxs-lookup"><span data-stu-id="133a0-232">You may create new SQL Server logins programmatically or using the SQL Server Management Studio.</span></span> <span data-ttu-id="133a0-233">若要以程式設計的方式透過 SQL 驗證建立新的系統管理員使用者，請啟動 [新增查詢]  ，然後執行下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-233">To create a new sysadmin user with SQL authentication programmatically, start a **New Query** and execute the following script.</span></span> <span data-ttu-id="133a0-234">使用您選擇的「使用者名稱」和「密碼」取代 <新使用者名稱\> 和 <新密碼\>。</span><span class="sxs-lookup"><span data-stu-id="133a0-234">Replace <new user name\> and <new password\> with your choice of *user name* and *password*.</span></span> 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


<span data-ttu-id="133a0-235">視需要調整密碼原則 (程式碼範例會關閉原則檢查及密碼到期日)。</span><span class="sxs-lookup"><span data-stu-id="133a0-235">Adjust the password policy as needed (the sample code turns off policy checking and password expiration).</span></span> <span data-ttu-id="133a0-236">如需 SQL Server 登入的詳細資訊，請參閱 [建立登入](http://msdn.microsoft.com/library/aa337562.aspx)。</span><span class="sxs-lookup"><span data-stu-id="133a0-236">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>  

<span data-ttu-id="133a0-237">若要使用 SQL Server Management Studio 建立新的 SQL Server 登入：</span><span class="sxs-lookup"><span data-stu-id="133a0-237">To create new SQL Server logins using the SQL Server Management Studio:</span></span>

1. <span data-ttu-id="133a0-238">在 SQL Server Management Studio 物件總管 中，展開您要在其中建立新登入的伺服器執行個體資料夾。</span><span class="sxs-lookup"><span data-stu-id="133a0-238">In **SQL Server Management Studio Object Explorer**, expand the folder of the server instance in which you want to create the new login.</span></span>
2. <span data-ttu-id="133a0-239">以滑鼠右鍵按一下 [安全性] 資料夾，並指向 [新增]，然後選取 [登入...]。</span><span class="sxs-lookup"><span data-stu-id="133a0-239">Right-click the **Security** folder, point to **New**, and select **Login…**.</span></span>
   
   ![新增登入][10]
3. <span data-ttu-id="133a0-241">在 [登入 - 新增] 對話方塊的 [一般] 頁面中，於 [登入名稱] 方塊輸入新使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="133a0-241">In the **Login - New** dialog box, on the **General** page, enter the name of the new user in the **Login name** box.</span></span>
4. <span data-ttu-id="133a0-242">選取 [SQL Server 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="133a0-242">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="133a0-243">在 [密碼]  方塊中，輸入新使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-243">In the **Password** box, enter a password for the new user.</span></span> <span data-ttu-id="133a0-244">在 [確認密碼]  方塊中再次輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-244">Enter that password again into the **Confirm Password** box.</span></span>
6. <span data-ttu-id="133a0-245">若要強制執行複雜性和強制性密碼原則選項，請選取 [強制執行密碼原則] \(建議)。</span><span class="sxs-lookup"><span data-stu-id="133a0-245">To enforce password policy options for complexity and enforcement, select **Enforce password policy** (recommended).</span></span> <span data-ttu-id="133a0-246">此為選取 SQL Server 驗證時的預設選項。</span><span class="sxs-lookup"><span data-stu-id="133a0-246">This is a default option when SQL Server authentication is selected.</span></span>
7. <span data-ttu-id="133a0-247">若要強制執行逾期密碼原則選項，請選取 [強制執行密碼逾期] \(建議)。</span><span class="sxs-lookup"><span data-stu-id="133a0-247">To enforce password policy options for expiration, select **Enforce password expiration** (recommended).</span></span> <span data-ttu-id="133a0-248">您必須選取強制執行密碼原則才能啟用此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="133a0-248">Enforce password policy must be selected to enable this checkbox.</span></span> <span data-ttu-id="133a0-249">此為選取 SQL Server 驗證時的預設選項。</span><span class="sxs-lookup"><span data-stu-id="133a0-249">This is a default option when SQL Server authentication is selected.</span></span>
8. <span data-ttu-id="133a0-250">若要強制使用者在首次登入後建立新密碼，請選取 [使用者必須在下次登入時變更密碼]  \(如果此登入是供其他使用者使用，建議您選取此選項。</span><span class="sxs-lookup"><span data-stu-id="133a0-250">To force the user to create a new password after the first time the login is used, select **User must change password at next login** (Recommended if this login is for someone else to use.</span></span> <span data-ttu-id="133a0-251">如果此登入是供您自己使用，請勿選取此選項。)您必須選取強制執行密碼逾期才能啟用此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="133a0-251">If the login is for your own use, do not select this option.) Enforce password expiration must be selected to enable this checkbox.</span></span> <span data-ttu-id="133a0-252">此為選取 SQL Server 驗證時的預設選項。</span><span class="sxs-lookup"><span data-stu-id="133a0-252">This is a default option when SQL Server authentication is selected.</span></span>
9. <span data-ttu-id="133a0-253">在 [預設資料庫] 清單中選取登入的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="133a0-253">From the **Default database** list, select a default database for the login.</span></span> <span data-ttu-id="133a0-254">[master] 是此選項的預設值。</span><span class="sxs-lookup"><span data-stu-id="133a0-254">**master** is the default for this option.</span></span> <span data-ttu-id="133a0-255">如果您尚未建立使用者資料庫，請保留 [master] 的設定。</span><span class="sxs-lookup"><span data-stu-id="133a0-255">If you have not yet created a user database, leave this set to **master**.</span></span>
10. <span data-ttu-id="133a0-256">在 [預設語言] 清單中，保留 [default] 值。</span><span class="sxs-lookup"><span data-stu-id="133a0-256">In the **Default language** list, leave **default** as the value.</span></span>
    
    ![登入屬性][11]
11. <span data-ttu-id="133a0-258">如果您正在建立第一個登入，也許會想要將此登入指定為 SQL Server 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="133a0-258">If this is the first login you are creating, you may want to designate this login as a SQL Server administrator.</span></span> <span data-ttu-id="133a0-259">如果是的話，請在 [伺服器角色] 頁面中勾選 [系統管理員 (sysadmin)]。</span><span class="sxs-lookup"><span data-stu-id="133a0-259">If so, on the **Server Roles** page, check **sysadmin**.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="133a0-260">系統管理員 (sysadmin) 固定伺服器角色的成員擁有 Database Engine 的完整控制權限。</span><span class="sxs-lookup"><span data-stu-id="133a0-260">Members of the sysadmin fixed server role have complete control of the Database Engine.</span></span> <span data-ttu-id="133a0-261">基於安全性理由，請謹慎限制此角色的成員資格。</span><span class="sxs-lookup"><span data-stu-id="133a0-261">For security reasons, you should carefully restrict membership in this role.</span></span>
    > 
    > 
    
    ![系統管理員 (sysadmin)][12]
12. <span data-ttu-id="133a0-263">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="133a0-263">Click OK.</span></span>

## <span data-ttu-id="133a0-264"><a name="DNS"></a>決定虛擬機器的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="133a0-264"><a name="DNS"></a>Determine the DNS name of the virtual machine</span></span>
<span data-ttu-id="133a0-265">若要從另一部電腦連接 SQL Server Database Engine，您必須知道虛擬機器的網域名稱系統 (DNS) 名稱。</span><span class="sxs-lookup"><span data-stu-id="133a0-265">To connect to the SQL Server Database Engine from another computer, you must know the Domain Name System (DNS) name of the virtual machine.</span></span>

<span data-ttu-id="133a0-266">(這是網際網路用來識別虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="133a0-266">(This is the name the internet uses to identify the virtual machine.</span></span> <span data-ttu-id="133a0-267">您可以使用 IP 位址，不過當 Azure 因備援或維護而移動資源時，IP 位址可能會改變。</span><span class="sxs-lookup"><span data-stu-id="133a0-267">You can use the IP address, but the IP address might change when Azure moves resources for redundancy or maintenance.</span></span> <span data-ttu-id="133a0-268">DNS 名稱是穩定的，因為它可以重新導向新的 IP 位址。)</span><span class="sxs-lookup"><span data-stu-id="133a0-268">The DNS name will be stable because it can be redirected to a new IP address.)</span></span>

1. <span data-ttu-id="133a0-269">在 Azure 傳統入口網站 (或前一個步驟) 中選取 [虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="133a0-269">In the Azure Classic Portal (or from the previous step), select **VIRTUAL MACHINES**.</span></span>
2. <span data-ttu-id="133a0-270">在 [虛擬機器執行個體] 頁面的 [DNS 名稱] 欄中，尋找及複製外觀加上 **http://** 之虛擬機器的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="133a0-270">On the **VIRTUAL MACHINE INSTANCES** page, in the **DNS NAME** column, find and copy the DNS name for the virtual machine which appears preceded by **http://**.</span></span> <span data-ttu-id="133a0-271">(使用者介面可能無法顯示完整名稱，不過您可以在名稱上按一下滑鼠右鍵，然後選擇複製。)</span><span class="sxs-lookup"><span data-stu-id="133a0-271">(The user interface might not display the entire name, but you can right-click on it, and select copy.)</span></span>

## <span data-ttu-id="133a0-272"><a name="cde"></a>從另一台電腦連接到 Database Engine</span><span class="sxs-lookup"><span data-stu-id="133a0-272"><a name="cde"></a>Connect to the Database Engine from another computer</span></span>
1. <span data-ttu-id="133a0-273">在連接網際網路的電腦上開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="133a0-273">On a computer connected to the internet, open SQL Server Management Studio.</span></span>
2. <span data-ttu-id="133a0-274">在 [連接到伺服器] 或 [連接到 Database Engine] 對話方塊的 [伺服器名稱] 方塊中，輸入虛擬機器的 DNS 名稱 (於上一個工作中決定) 和 *DNSName,portnumber* 格式的公用端點連接埠名稱 (如 **tutorialtestVM.cloudapp.net,57500**)。</span><span class="sxs-lookup"><span data-stu-id="133a0-274">In the **Connect to Server** or **Connect to Database Engine** dialog box, in the **Server name** box, enter the DNS name of the virtual machine (determined in the previous task) and a public endpoint port number in the format of *DNSName,portnumber* such as **tutorialtestVM.cloudapp.net,57500**.</span></span>
3. <span data-ttu-id="133a0-275">在 [驗證] 方塊中，選取 [SQL Server 驗證]。</span><span class="sxs-lookup"><span data-stu-id="133a0-275">In the **Authentication** box, select **SQL Server Authentication**.</span></span>
4. <span data-ttu-id="133a0-276">在 [登入]  方塊中，輸入於先前工作中建立之登入的名稱。</span><span class="sxs-lookup"><span data-stu-id="133a0-276">In the **Login** box, type the name of a login that you created in an earlier task.</span></span>
5. <span data-ttu-id="133a0-277">在 [密碼]  方塊中，輸入於先前工作中建立之登入的密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-277">In the **Password** box, type the password of the login that you create in an earlier task.</span></span>
6. <span data-ttu-id="133a0-278">按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="133a0-278">Click **Connect**.</span></span>

## <span data-ttu-id="133a0-279"><a name="amlconnect"></a>從 Azure Machine Learning 連接 Database Engine</span><span class="sxs-lookup"><span data-stu-id="133a0-279"><a name="amlconnect"></a>Connect to the Database Engine from Azure Machine Learning</span></span>
<span data-ttu-id="133a0-280">在 Team Data Science Process 的後續階段中，您將使用 [Azure Machine Learning Studio](https://studio.azureml.net) 來建置和部署機器學習服務模型。</span><span class="sxs-lookup"><span data-stu-id="133a0-280">In later stages of the Team Data Science Process, you will use the [Azure Machine Learning Studio](https://studio.azureml.net) to build and deploy machine learning models.</span></span> <span data-ttu-id="133a0-281">若要將資料從 SQL Server VM 資料庫直接擷取到 Azure Machine Learning 以供訓練或評分使用，請在新的 [Azure Machine Learning Studio](https://studio.azureml.net) 實驗中使用「匯入資料」模組。</span><span class="sxs-lookup"><span data-stu-id="133a0-281">To ingest data from your SQL Server VM databases directly into Azure Machine Learning for training or scoring, use the **Import Data** module in a new [Azure Machine Learning Studio](https://studio.azureml.net) experiment.</span></span> <span data-ttu-id="133a0-282">您可以透過 Team Data Science Process 指南的連結，找到更多有關本主題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="133a0-282">This topic is covered in more details through the Team Data Science Process guide links.</span></span> <span data-ttu-id="133a0-283">如需簡介，請參閱「 [什麼是 Azure Machine Learning Studio？」](machine-learning-what-is-ml-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="133a0-283">For an introduction, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md).</span></span>

1. <span data-ttu-id="133a0-284">在[匯入資料模組](https://msdn.microsoft.com/library/azure/dn905997.aspx)的 [屬性] 窗格中，從 [資料來源] 下拉式清單中選取 [Azure SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="133a0-284">In the **Properties** pane of the [Import Data module](https://msdn.microsoft.com/library/azure/dn905997.aspx), select **Azure SQL Database** from the **Data Source**     dropdown list.</span></span>
2. <span data-ttu-id="133a0-285">在 [資料庫伺服器名稱] 文字方塊中，輸入 `tcp:<DNS name of your virtual machine>,1433`</span><span class="sxs-lookup"><span data-stu-id="133a0-285">In the **Database server name** text box, enter `tcp:<DNS name of your virtual machine>,1433`</span></span>
3. <span data-ttu-id="133a0-286">在 [ **伺服器使用者帳戶名稱** ] 文字方塊中輸入 SQL 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="133a0-286">Enter the SQL user name in the **Server user account name** text box.</span></span>
4. <span data-ttu-id="133a0-287">在 [ **伺服器使用者帳戶密碼** ] 文字方塊中輸入 SQL 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="133a0-287">Enter the sql user's password in the **Server user account password** text box.</span></span>
   
   ![Azure Machine Learning 匯入資料][13]

## <span data-ttu-id="133a0-289"><a name="shutdown"></a>關閉並解除配置非使用中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="133a0-289"><a name="shutdown"></a>Shutdown and deallocate virtual machine when not in use</span></span>
<span data-ttu-id="133a0-290">Azure 虛擬機器的定價策略是「 **只針對您使用的項目進行付費**」。</span><span class="sxs-lookup"><span data-stu-id="133a0-290">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="133a0-291">為了確保未使用虛擬機器時不會被計費，您必須將虛擬機器的狀態設為 [ **已停止 (已解除配置)** ]。</span><span class="sxs-lookup"><span data-stu-id="133a0-291">To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state.</span></span>

> [!NOTE]
> <span data-ttu-id="133a0-292">從 VM 內部關閉虛擬機器 (使用 Windows 電源選項) 時，雖然 VM 已停止，但仍然處於已配置狀態。</span><span class="sxs-lookup"><span data-stu-id="133a0-292">Shutting down the virtual machine from inside (using Windows power options), the VM is stopped but remains allocated.</span></span> <span data-ttu-id="133a0-293">為了確保您不會繼續被計費，請一律在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中停止虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="133a0-293">To ensure you’re not being billed, always stop virtual machines from the [Azure Classic Portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="133a0-294">您也可以藉由呼叫 ShutdownRoleOperation 搭配相當於 "StoppedDeallocated" 的 "PostShutdownAction"，透過 Powershell 來停止 VM。</span><span class="sxs-lookup"><span data-stu-id="133a0-294">You can also stop the VM through Powershell by calling ShutdownRoleOperation with "PostShutdownAction" equal to "StoppedDeallocated".</span></span>
> 
> 

<span data-ttu-id="133a0-295">關閉及解除配置虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="133a0-295">To shutdown and deallocate the virtual machine:</span></span>

1. <span data-ttu-id="133a0-296">使用您的帳戶登入 [Azure 傳統入口網站](http://manage.windowsazure.com/) 。</span><span class="sxs-lookup"><span data-stu-id="133a0-296">Log in to the [Azure Classic Portal](http://manage.windowsazure.com/) using your account.</span></span>  
2. <span data-ttu-id="133a0-297">從左側導覽列選取 [ **虛擬機器** ]。</span><span class="sxs-lookup"><span data-stu-id="133a0-297">Select **VIRTUAL MACHINES** from the left navigation bar.</span></span>
3. <span data-ttu-id="133a0-298">在虛擬機器清單中，按一下虛擬機器的名稱，然後移至 [ **儀表板** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="133a0-298">In the list of virtual machines, click on the name of your virtual machine then go to the **DASHBOARD** page.</span></span>
4. <span data-ttu-id="133a0-299">按一下頁面底部的 [ **關閉**]。</span><span class="sxs-lookup"><span data-stu-id="133a0-299">At the bottom of the page, click **SHUTDOWN**.</span></span>

![VM 關閉][15]

<span data-ttu-id="133a0-301">虛擬機器將會取消配置，但不是刪除。</span><span class="sxs-lookup"><span data-stu-id="133a0-301">The virtual machine will be deallocated but not deleted.</span></span> <span data-ttu-id="133a0-302">您隨時都可從 Azure 傳統入口網站重新啟動您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="133a0-302">You may restart your virtual machine at any time from the Azure Classic Portal.</span></span>

## <a name="your-azure-sql-server-vm-is-ready-to-use-whats-next"></a><span data-ttu-id="133a0-303">您的 Azure SQL Server VM 已準備好可供使用：下一步是什麼？</span><span class="sxs-lookup"><span data-stu-id="133a0-303">Your Azure SQL Server VM is ready to use: what's next?</span></span>
<span data-ttu-id="133a0-304">您的虛擬機器已經準備好在資料科學練習中使用。</span><span class="sxs-lookup"><span data-stu-id="133a0-304">Your virtual machine is now ready to use in your data science exercises.</span></span> <span data-ttu-id="133a0-305">虛擬機器也已經準備好用來做為 IPython Notebook 伺服器，以進行資料探索和處理，以及其他可與 Azure 機器學習服務和 Team Data Science Process (TDSP) 一起使用的工作。</span><span class="sxs-lookup"><span data-stu-id="133a0-305">The virtual machine is also ready for use as an IPython Notebook server for the exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and the Team Data Science Process (TDSP).</span></span>

<span data-ttu-id="133a0-306">[Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 中說明了資料科學程序的後續步驟，其中可能包含將資料移至 HDInsight 並在其中處理資料與取樣，做為透過 Azure Machine Learning 從資料學習的準備。</span><span class="sxs-lookup"><span data-stu-id="133a0-306">The next steps in the data science process are mapped in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

