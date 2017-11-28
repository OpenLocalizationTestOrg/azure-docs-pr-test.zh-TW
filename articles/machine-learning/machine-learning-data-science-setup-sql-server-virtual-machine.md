---
title: "為 IPython Notebook 伺服器的 SQL Server 虛擬機器 aaaSet |Microsoft 文件"
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
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a><span data-ttu-id="2d731-103">將 Azure SQL Server 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用</span><span class="sxs-lookup"><span data-stu-id="2d731-103">Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics</span></span>
<span data-ttu-id="2d731-104">本主題說明如何 tooprovision 及設定 SQL Server 虛擬機器 toobe，做為雲端架構資料科學環境的一部分。</span><span class="sxs-lookup"><span data-stu-id="2d731-104">This topic shows how tooprovision and configure an SQL Server virtual machine toobe used as part of a cloud-based data science environment.</span></span> <span data-ttu-id="2d731-105">hello Windows 虛擬機器設定有支援 IPython 筆記型電腦、 Azure 儲存體總管 中，和 AzCopy，以及其他公用程式可用於資料科學專案之類的工具。</span><span class="sxs-lookup"><span data-stu-id="2d731-105">hello Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, and AzCopy, as well as other utilities that are useful for data science projects.</span></span> <span data-ttu-id="2d731-106">Azure 儲存體總管和 AzCopy，例如，提供方便的方式 tooupload 資料 tooAzure blob 儲存體從您的本機電腦或 toodownload 它 tooyour 從 blob 儲存體的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="2d731-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways tooupload data tooAzure blob storage from your local machine or toodownload it tooyour local machine from blob storage.</span></span>

<span data-ttu-id="2d731-107">hello Azure 虛擬機器資源庫含有包含 Microsoft SQL Server 的數個映像。</span><span class="sxs-lookup"><span data-stu-id="2d731-107">hello Azure virtual machine gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="2d731-108">選取適合您資料需求的 SQL Server VM 映像。</span><span class="sxs-lookup"><span data-stu-id="2d731-108">Select an SQL Server VM image that is suitable for your data needs.</span></span> <span data-ttu-id="2d731-109">建議的映像如下：</span><span class="sxs-lookup"><span data-stu-id="2d731-109">Recommended images are:</span></span>

* <span data-ttu-id="2d731-110">SQL Server 2012 SP2 Enterprise 的小型 toomedium 資料大小</span><span class="sxs-lookup"><span data-stu-id="2d731-110">SQL Server 2012 SP2 Enterprise for small toomedium data sizes</span></span>
* <span data-ttu-id="2d731-111">SQL Server 2012 SP2 Enterprise 針對最佳化資料倉儲工作量的大型 toovery 大型的資料大小</span><span class="sxs-lookup"><span data-stu-id="2d731-111">SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads for large toovery large data sizes</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2d731-112">SQL Server 2012 SP2 Enterprise 的映像 **不包含資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="2d731-112">SQL Server 2012 SP2 Enterprise image **does not include a data disk**.</span></span> <span data-ttu-id="2d731-113">您將需要 tooadd 及/或將一或多個虛擬硬碟 toostore 附加您的資料。</span><span class="sxs-lookup"><span data-stu-id="2d731-113">You will need tooadd and/or attach one or more virtual hard disks toostore your data.</span></span> <span data-ttu-id="2d731-114">當您建立 Azure 虛擬機器時，它擁有 hello 對應的作業系統 toohello C 磁碟機的磁碟和對應的暫存磁碟 toohello D 磁碟機的支援。</span><span class="sxs-lookup"><span data-stu-id="2d731-114">When you create an Azure virtual machine, it has a disk for hello operating system mapped toohello C drive and a temporary disk mapped toohello D drive.</span></span> <span data-ttu-id="2d731-115">請勿使用 hello D 磁碟機 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="2d731-115">Do not use hello D drive toostore data.</span></span> <span data-ttu-id="2d731-116">正如 hello 名，它會提供暫存儲存位置。</span><span class="sxs-lookup"><span data-stu-id="2d731-116">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="2d731-117">它並不提供備援或備份，因為它不在 Azure 儲存體內。</span><span class="sxs-lookup"><span data-stu-id="2d731-117">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
  > 
  > 

## <span data-ttu-id="2d731-118"><a name="Provision"></a>連接 toohello Azure 傳統入口網站並佈建 SQL Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2d731-118"><a name="Provision"></a>Connect toohello Azure Classic Portal and provision an SQL Server virtual machine</span></span>
1. <span data-ttu-id="2d731-119">登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d731-119">Log in toohello [Azure Classic portal](http://manage.windowsazure.com/) using your account.</span></span>
   <span data-ttu-id="2d731-120">如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="2d731-120">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="2d731-121">在 hello Azure 傳統入口網站，在 hello 左下方 hello 網頁上，按一下  **+ 新增**，按一下 **計算**，按一下 **虛擬機器**，然後按一下 **FROM組件庫**。</span><span class="sxs-lookup"><span data-stu-id="2d731-121">On hello Azure Classic portal, at hello bottom left of hello web page, click **+NEW**, click **COMPUTE**, click **VIRTUAL MACHINE**, and then click **FROM GALLERY**.</span></span>
3. <span data-ttu-id="2d731-122">在 hello**建立虛擬機器**頁面上，選取包含您資料的需求，為基礎的 SQL Server 的虛擬機器映像，然後按一下hello 右下方的 hello 頁面下一步箭頭。</span><span class="sxs-lookup"><span data-stu-id="2d731-122">On hello **Create a Virtual Machine** page, select a virtual machine image containing SQL Server based on your data needs, and then click hello next arrow at the bottom right of hello page.</span></span> <span data-ttu-id="2d731-123">Hello hello 上最新的資訊在 Azure 上支援 SQL Server 映像，請參閱[開始使用 Azure 虛擬機器中 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294720)主題 hello [Azure 虛擬機器中 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294719)文件集。</span><span class="sxs-lookup"><span data-stu-id="2d731-123">For hello most up-to-date information on hello supported SQL Server images on Azure, see [Getting Started with SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294720) topic in hello [SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294719) documentation set.</span></span>
   
   ![選取 SQL Server VM][1]
4. <span data-ttu-id="2d731-125">在 hello 上第一個**虛擬機器組態**頁面上，提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="2d731-125">On hello first **Virtual Machine Configuration** page, provide the following information:</span></span>
   
   * <span data-ttu-id="2d731-126">提供 [虛擬機器名稱] 。</span><span class="sxs-lookup"><span data-stu-id="2d731-126">Provide a **VIRTUAL MACHINE NAME**.</span></span>
   * <span data-ttu-id="2d731-127">在 [hello**新的使用者名稱**] 方塊中，輸入唯一的使用者名稱 hello VM 本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d731-127">In hello **NEW USER NAME** box, type unique user name for hello VM local administrator account.</span></span>
   * <span data-ttu-id="2d731-128">在 hello**新密碼**方塊中，輸入強式密碼。</span><span class="sxs-lookup"><span data-stu-id="2d731-128">In hello **NEW PASSWORD** box, type a strong password.</span></span> <span data-ttu-id="2d731-129">如需詳細資訊，請參閱 [增強式密碼](http://msdn.microsoft.com/library/ms161962.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2d731-129">For more information, see [Strong Passwords](http://msdn.microsoft.com/library/ms161962.aspx).</span></span>
   * <span data-ttu-id="2d731-130">在 hello**確認密碼**方塊中，重新輸入 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="2d731-130">In hello **CONFIRM PASSWORD** box, retype hello password.</span></span>
   * <span data-ttu-id="2d731-131">選取適當的 hello**大小**hello 從下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="2d731-131">Select hello appropriate **SIZE** from hello drop down list.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="2d731-132">在佈建期間指定 hello hello 虛擬機器大小： A2 是 hello 生產工作負載的建議的最小大小。</span><span class="sxs-lookup"><span data-stu-id="2d731-132">hello size of hello virtual machine is specified during provisioning: A2 is hello smallest size recommended for production workloads.</span></span> <span data-ttu-id="2d731-133">使用 SQL Server Enterprise Edition 時，虛擬機器的最小建議大小為 A3。</span><span class="sxs-lookup"><span data-stu-id="2d731-133">The minimum recommended size for a virtual machine is A3 when using SQL Server Enterprise Edition.</span></span> <span data-ttu-id="2d731-134">當您使用 SQL Server Enterprise Edition 時，請選取 A3 或以上的大小。</span><span class="sxs-lookup"><span data-stu-id="2d731-134">Select A3 or higher when using SQL Server Enterprise Edition.</span></span> <span data-ttu-id="2d731-135">使用 SQL Server 2012 或 2014 Enterprise Optimized for Transactional Workloads 映像時，請選取 A4。</span><span class="sxs-lookup"><span data-stu-id="2d731-135">Select A4 when using SQL Server 2012 or 2014 Enterprise Optimized for Transactional Workloads images.</span></span>
     > <span data-ttu-id="2d731-136">使用 SQL Server 2012 或 2014 Enterprise Optimized for Data Warehousing Workloads 映像時，請選取 A7。</span><span class="sxs-lookup"><span data-stu-id="2d731-136">Select A7 when using SQL Server 2012 or 2014 Enterprise Optimized for Data Warehousing Workloads images.</span></span> <span data-ttu-id="2d731-137">選取的 hello 大小限制您可以設定的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="2d731-137">hello size selected limits the number of data disks you can configure.</span></span> <span data-ttu-id="2d731-138">最新，您可以連接 tooa 虛擬機器上可用的虛擬機器大小和資料磁碟數目 hello 資訊，請參閱[的 Azure 虛擬機器大小](http://msdn.microsoft.com/library/azure/dn197896.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2d731-138">For most up-to-date information on available virtual machine sizes and hello number of data disks that you can attach tooa virtual machine, see [Virtual Machine Sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="2d731-139">如需定價資訊，請參閱「 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)」。</span><span class="sxs-lookup"><span data-stu-id="2d731-139">For pricing information, see [VIrtual Macines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
     > 
     > 
   
   <span data-ttu-id="2d731-140">按一下 下一步 hello hello 底部右 toocontinue 箭號。</span><span class="sxs-lookup"><span data-stu-id="2d731-140">Click hello next arrow on hello bottom right toocontinue.</span></span>
   
   ![VM 組態][2]
5. <span data-ttu-id="2d731-142">在 hello 第二個**虛擬機器組態**頁面上，設定網路功能、 儲存體和可用性的資源：</span><span class="sxs-lookup"><span data-stu-id="2d731-142">On hello second **Virtual machine configuration** page, configure resources for networking, storage, and availability:</span></span>
   
   * <span data-ttu-id="2d731-143">在 hello**雲端服務**方塊中，選擇**建立新的雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="2d731-143">In hello **Cloud Service** box, choose **Create a new cloud service**.</span></span>
   * <span data-ttu-id="2d731-144">在 hello**雲端服務 DNS 名稱**方塊中，提供您選擇的 DNS 名稱的 hello 第一個部分，以便完成格式名稱**TESTNAME.cloudapp.net**</span><span class="sxs-lookup"><span data-stu-id="2d731-144">In hello **Cloud Service DNS Name** box, provide hello first portion of a DNS name of your choice, so that it completes a name in the format **TESTNAME.cloudapp.net**</span></span>
   * <span data-ttu-id="2d731-145">在 hello**區域/同質群組/虛擬網路**方塊中，選取將託管這個虛擬映像的區域。</span><span class="sxs-lookup"><span data-stu-id="2d731-145">In hello **REGION/AFFINITY GROUP/VIRTUAL NETWORK** box, select a region where this virtual image will be hosted.</span></span>
   * <span data-ttu-id="2d731-146">在 hello**儲存體帳戶**，選取現有的儲存體帳戶，或選取 自動產生的一個。</span><span class="sxs-lookup"><span data-stu-id="2d731-146">In hello **Storage Account**, select an existing storage account or select an automatically generated one.</span></span>
   * <span data-ttu-id="2d731-147">在 hello**可用性設定組**方塊中，選取**（無）**。</span><span class="sxs-lookup"><span data-stu-id="2d731-147">In hello **AVAILABILITY SET** box, select **(none)**.</span></span>
   * <span data-ttu-id="2d731-148">閱讀並接受 hello 定價資訊。</span><span class="sxs-lookup"><span data-stu-id="2d731-148">Read and accept hello pricing information.</span></span>
6. <span data-ttu-id="2d731-149">在 hello**端點**區段中，在 hello 底下的空白下拉式清單中按一下**名稱**，並選取**MSSQL**然後輸入 hello hello (的DatabaseEngine執行個體的連接埠號碼**1433年**hello 預設執行個體)。</span><span class="sxs-lookup"><span data-stu-id="2d731-149">In hello **ENDPOINTS** section, click in hello empty dropdown under **NAME**, and select **MSSQL**  then type hello port number of the instance of hello Database Engine (**1433** for hello default instance).</span></span>
7. <span data-ttu-id="2d731-150">您的 SQL Server VM 也可以用來做為 IPython Notebook 伺服器 (將在稍後步驟中設定)。</span><span class="sxs-lookup"><span data-stu-id="2d731-150">Your SQL Server VM can also serve as an IPython Notebook Server, which will be configured in a later step.</span></span>
   <span data-ttu-id="2d731-151">加入新端點 toospecify hello 連接埠 toouse 您 IPython 筆記型電腦的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2d731-151">Add a new endpoint toospecify hello port toouse for your IPython Notebook server.</span></span> <span data-ttu-id="2d731-152">輸入的名稱在 hello**名稱**資料行中，選取您所選擇的 hello 公用連接埠的連接埠號碼並 9999 hello 私用連接埠。</span><span class="sxs-lookup"><span data-stu-id="2d731-152">Enter a name in hello **NAME** column,    select a port number of your choice for hello public port, and 9999 for hello private port.</span></span>
   
   <span data-ttu-id="2d731-153">按一下 下一步 hello hello 底部右 toocontinue 箭號。</span><span class="sxs-lookup"><span data-stu-id="2d731-153">Click hello next arrow on hello bottom right toocontinue.</span></span>
   
   ![選取 MSSQL 和 IPython 連接埠][3]
8. <span data-ttu-id="2d731-155">接受預設值 hello**安裝 VM 代理程式**選取，然後按一下 hello 右下角的 hello 精靈 toocomplete hello VM 佈建程序中的 hello hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="2d731-155">Accept hello default **Install VM agent** option checked and click hello hello check mark in hello bottom right corner of hello wizard toocomplete hello VM provisioning process.</span></span>
   
   `![VM 的最後選項][4]
9. <span data-ttu-id="2d731-157">等待 Azure 準備好您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d731-157">Wait while Azure prepares your virtual machine.</span></span> <span data-ttu-id="2d731-158">預期 hello 虛擬機器狀態 tooproceed 透過：</span><span class="sxs-lookup"><span data-stu-id="2d731-158">Expect hello virtual machine status tooproceed through:</span></span>
   
   * <span data-ttu-id="2d731-159">啟動中 (佈建中)</span><span class="sxs-lookup"><span data-stu-id="2d731-159">Starting (Provisioning)</span></span>
   * <span data-ttu-id="2d731-160">已停止</span><span class="sxs-lookup"><span data-stu-id="2d731-160">Stopped</span></span>
   * <span data-ttu-id="2d731-161">啟動中 (佈建中)</span><span class="sxs-lookup"><span data-stu-id="2d731-161">Starting (Provisioning)</span></span>
   * <span data-ttu-id="2d731-162">執行中 (佈建中)</span><span class="sxs-lookup"><span data-stu-id="2d731-162">Running (Provisioning)</span></span>
   * <span data-ttu-id="2d731-163">執行中</span><span class="sxs-lookup"><span data-stu-id="2d731-163">Running</span></span>

## <span data-ttu-id="2d731-164"><a name="RemoteDesktop"></a>開啟 hello 虛擬機器使用遠端桌面並完成安裝</span><span class="sxs-lookup"><span data-stu-id="2d731-164"><a name="RemoteDesktop"></a>Open hello virtual machine using Remote Desktop and complete setup</span></span>
1. <span data-ttu-id="2d731-165">佈建完成時，按一下您的虛擬機器 toogo toohello 儀表板頁面的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2d731-165">When provisioning completes, click on hello name of your virtual machine toogo toohello DASHBOARD page.</span></span> <span data-ttu-id="2d731-166">在 hello hello 頁面底部，按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="2d731-166">At hello bottom of hello page, click **Connect**.</span></span>
2. <span data-ttu-id="2d731-167">選擇使用 hello Windows 遠端桌面程式 tooopen hello rpd 檔案 (`%windir%\system32\mstsc.exe`)。</span><span class="sxs-lookup"><span data-stu-id="2d731-167">Choose tooopen hello rpd file using hello Windows Remote Desktop program (`%windir%\system32\mstsc.exe`).</span></span>
3. <span data-ttu-id="2d731-168">在 hello **Windows 安全性**對話方塊方塊中，您在前述步驟中指定的本機系統管理員帳戶提供 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="2d731-168">At hello **Windows Security** dialog box, provide hello password for the local administrator account that you specified in an earlier step.</span></span>
   <span data-ttu-id="2d731-169">（您可能會要求 hello 虛擬機器的 tooverify hello 認證。）</span><span class="sxs-lookup"><span data-stu-id="2d731-169">(You might be asked tooverify hello credentials of hello virtual machine.)</span></span>
4. <span data-ttu-id="2d731-170">hello 第一次登入 toothis 虛擬機器，數個程序可能需要 toocomplete，包括桌面、 Windows 更新和已完成的 hello Windows 初始設定工作 (sysprep) 的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="2d731-170">hello first time you log on toothis virtual machine, several processes may need toocomplete, including setup of your desktop, Windows updates, and completion of hello Windows initial configuration tasks (sysprep).</span></span> <span data-ttu-id="2d731-171">待 Windows sysprep 完成後，SQL Server 安裝程式會完成組態工作。</span><span class="sxs-lookup"><span data-stu-id="2d731-171">After Windows sysprep completes, SQL Server setup completes configuration tasks.</span></span> <span data-ttu-id="2d731-172">在完成這些工作的期間，可能會造成幾分鐘的時間延遲。</span><span class="sxs-lookup"><span data-stu-id="2d731-172">These tasks may cause a delay of a few minutes while they complete.</span></span> <span data-ttu-id="2d731-173">`SELECT @@SERVERNAME`除非 SQL Server 安裝程式完成，且 SQL Server Management Studio 可能無法在 hello 開始頁面上可見，可能傳回 hello 正確的名稱。</span><span class="sxs-lookup"><span data-stu-id="2d731-173">`SELECT @@SERVERNAME` may not return hello correct name until SQL Server setup completes, and SQL Server Management Studio may not be visable on hello start page.</span></span>

<span data-ttu-id="2d731-174">當您使用 Windows 遠端桌面連線的 toohello 虛擬機器，hello 虛擬機器的運作方式就像是任何其他電腦。</span><span class="sxs-lookup"><span data-stu-id="2d731-174">Once you are connected toohello virtual machine with Windows Remote Desktop, hello virtual machine works much like any other computer.</span></span> <span data-ttu-id="2d731-175">連接 toohello 預設執行個體的 SQL Server 與 SQL Server Management Studio （hello 虛擬機器上執行） 在 hello 一般的方式。</span><span class="sxs-lookup"><span data-stu-id="2d731-175">Connect toohello default instance of SQL Server with SQL Server Management Studio (running on hello virtual machine) in hello normal way.</span></span>

## <span data-ttu-id="2d731-176"><a name="InstallIPython"></a>安裝 IPython Notebook 和其他支援工具</span><span class="sxs-lookup"><span data-stu-id="2d731-176"><a name="InstallIPython"></a>Install IPython Notebook and other supporting tools</span></span>
<span data-ttu-id="2d731-177">tooconfigure 您新的 SQL Server VM tooserve 做為 IPython Notebook 伺服器，並安裝其他支援工具這類 AzCopy、 Azure 儲存體總管、 有用的資料科學 Python 封裝和其他人、 tooyou 提供特殊的自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="2d731-177">tooconfigure your new SQL Server VM tooserve as an IPython Notebook server, and install additional supporting tools such AzCopy, Azure Storage Explorer, useful Data Science Python packages, and others, a special customization script is provided tooyou.</span></span> <span data-ttu-id="2d731-178">tooinstall:</span><span class="sxs-lookup"><span data-stu-id="2d731-178">tooinstall:</span></span>

1. <span data-ttu-id="2d731-179">以滑鼠右鍵按一下 hello **Windows 啟動**圖示，然後按一下**命令提示字元 （管理員）**</span><span class="sxs-lookup"><span data-stu-id="2d731-179">Right-click hello **Windows Start** icon and click **Command Prompt (Admin)**</span></span>
2. <span data-ttu-id="2d731-180">複製下列命令的 hello 並貼在 hello 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="2d731-180">Copy hello following commands and paste at hello command prompt.</span></span>
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. <span data-ttu-id="2d731-181">出現提示時，輸入 hello IPython Notebook 伺服器您選擇的密碼。</span><span class="sxs-lookup"><span data-stu-id="2d731-181">When prompted, enter a password of your choice for hello IPython Notebook server.</span></span>
4. <span data-ttu-id="2d731-182">hello 自訂指令碼會自動執行數個後續安裝程序，包括：</span><span class="sxs-lookup"><span data-stu-id="2d731-182">hello customization script automates several post-install procedures, which include:</span></span>
    * <span data-ttu-id="2d731-183">安裝和設定 IPython Notebook 伺服器</span><span class="sxs-lookup"><span data-stu-id="2d731-183">Installation and setup of IPython Notebook server</span></span>
    * <span data-ttu-id="2d731-184">Hello hello 端點稍早建立的 Windows 防火牆中開啟 TCP 連接埠：</span><span class="sxs-lookup"><span data-stu-id="2d731-184">Opening TCP ports in hello Windows firewall for hello endpoints created earlier:</span></span>
    * <span data-ttu-id="2d731-185">適用於 SQL Server 遠端連線</span><span class="sxs-lookup"><span data-stu-id="2d731-185">For SQL Server remote connectivity</span></span>
    * <span data-ttu-id="2d731-186">適用於 IPython Notebook 伺服器遠端連線</span><span class="sxs-lookup"><span data-stu-id="2d731-186">For IPython Notebook server remote connectivity</span></span>
    * <span data-ttu-id="2d731-187">擷取 IPython Notebook 範例和 SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="2d731-187">Fetching sample IPython notebooks and SQL scripts</span></span>
    * <span data-ttu-id="2d731-188">下載並安裝實用的資料科學 Python 封裝</span><span class="sxs-lookup"><span data-stu-id="2d731-188">Downloading and installing useful Data Science Python packages</span></span>
    * <span data-ttu-id="2d731-189">下載並安裝 Azure 工具，例如 AzCopy 和 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="2d731-189">Downloading and installing Azure tools such as AzCopy and Azure Storage Explorer</span></span>  
    <br>
5. <span data-ttu-id="2d731-190">您可能會存取，並從使用 URL hello 表單的任何本機或遠端瀏覽器執行 IPython 筆記型電腦`https://<virtual_machine_DNS_name>:<port>`，其中連接埠是 hello IPython 公用連接埠選取佈建 hello 虛擬機器時。</span><span class="sxs-lookup"><span data-stu-id="2d731-190">You may access and run IPython Notebook from any local or remote browser using a URL of hello form `https://<virtual_machine_DNS_name>:<port>`, where port is hello IPython public port you selected while provisioning hello virtual machine.</span></span>
6. <span data-ttu-id="2d731-191">IPython 筆記型電腦伺服器做為背景服務正在執行，並重新啟動 hello 虛擬機器時自動啟動。</span><span class="sxs-lookup"><span data-stu-id="2d731-191">IPython Notebook server is running as a background service and will be restarted automatically when you restart hello virtual machine.</span></span>

## <span data-ttu-id="2d731-192"><a name="Optional"></a>視需要連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="2d731-192"><a name="Optional"></a>Attach data disk as needed</span></span>
<span data-ttu-id="2d731-193">如果您的 VM 映像不包含資料磁碟，亦即，不是 C 磁碟機 （作業系統磁碟） 和 D 磁碟機 （暫存磁碟），磁碟需要 tooadd 其中一個或多個資料磁碟 toostore 您的資料。</span><span class="sxs-lookup"><span data-stu-id="2d731-193">If your VM image does not include data disks, i.e., disks other than C drive (OS disk) and D drive (temporary disk), you need tooadd one or more data disks toostore your data.</span></span> <span data-ttu-id="2d731-194">針對 SQL Server 2012 SP2 Enterprise 針對最佳化資料倉儲工作量 hello VM 映像隨附預先設定的 SQL Server 資料和記錄檔的其他磁碟。</span><span class="sxs-lookup"><span data-stu-id="2d731-194">hello VM image for SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads comes pre-configured with additional disks for SQL Server data and log files.</span></span>

> [!NOTE]
> <span data-ttu-id="2d731-195">請勿使用 hello D 磁碟機 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="2d731-195">Do not use hello D drive toostore data.</span></span> <span data-ttu-id="2d731-196">正如 hello 名，它會提供暫存儲存位置。</span><span class="sxs-lookup"><span data-stu-id="2d731-196">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="2d731-197">它並不提供備援或備份，因為它不在 Azure 儲存體內。</span><span class="sxs-lookup"><span data-stu-id="2d731-197">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> 
> 

<span data-ttu-id="2d731-198">tooattach 額外資料磁碟，請依照下列中所述的 hello 步驟[如何 tooAttach Windows 虛擬機器的資料磁碟 tooa](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)，它將引導您完成：</span><span class="sxs-lookup"><span data-stu-id="2d731-198">tooattach additional data disks, follow hello steps described in [How tooAttach a Data Disk tooa Windows Virtual Machine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), which will guide you through:</span></span>

1. <span data-ttu-id="2d731-199">附加空磁碟 toohello 虛擬機器在先前步驟中佈建</span><span class="sxs-lookup"><span data-stu-id="2d731-199">Attaching empty disk(s) toohello virtual machine provisioned in earlier steps</span></span>
2. <span data-ttu-id="2d731-200">Hello hello 虛擬機器中的新磁碟的初始化</span><span class="sxs-lookup"><span data-stu-id="2d731-200">Initialization of hello new disk(s) in hello virtual machine</span></span>

## <span data-ttu-id="2d731-201"><a name="SSMS"></a>連接 tooSQL Server Management Studio 並啟用混合的模式驗證</span><span class="sxs-lookup"><span data-stu-id="2d731-201"><a name="SSMS"></a>Connect tooSQL Server Management Studio and enable mixed mode authentication</span></span>
<span data-ttu-id="2d731-202">hello SQL Server Database Engine 無法使用 Windows 驗證，若沒有網域環境。</span><span class="sxs-lookup"><span data-stu-id="2d731-202">hello SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="2d731-203">tooconnect toohello Database Engine 從另一部電腦，設定 SQL Server 混合的模式驗證。</span><span class="sxs-lookup"><span data-stu-id="2d731-203">tooconnect toohello Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="2d731-204">混合模式驗證可允許 SQL Server 驗證和 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="2d731-204">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span> <span data-ttu-id="2d731-205">SQL 驗證模式需要直接從您的 SQL Server VM 的資料庫中的訂單 tooingest 資料[Azure Machine Learning Studio](https://studio.azureml.net)使用 hello 資料匯入模組。</span><span class="sxs-lookup"><span data-stu-id="2d731-205">SQL authentication mode is required in order tooingest data directly from your SQL Server VM databases in the [Azure Machine Learning Studio](https://studio.azureml.net) using hello Import Data module.</span></span>

1. <span data-ttu-id="2d731-206">使用遠端桌面連線的 toohello 虛擬機器，同時使用 hello Windows**搜尋**窗格和型別**SQL Server Management Studio** (SMSS)。</span><span class="sxs-lookup"><span data-stu-id="2d731-206">While connected toohello virtual machine by using Remote Desktop, use hello Windows **Search** pane and type **SQL Server Management Studio** (SMSS).</span></span> <span data-ttu-id="2d731-207">按一下 toostart hello SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="2d731-207">Click toostart hello SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="2d731-208">您可能想在桌面上的捷徑 tooSSMS tooadd 供未來使用。</span><span class="sxs-lookup"><span data-stu-id="2d731-208">You may want tooadd a shortcut tooSSMS on your Desktop for future use.</span></span>
   
   ![啟動 SSMS][5]
   
   <span data-ttu-id="2d731-210">hello 第一次開啟 Management Studio，就必須建立 hello 使用者 Management Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="2d731-210">hello first time you open Management Studio it must create hello users Management Studio environment.</span></span> <span data-ttu-id="2d731-211">這可能需要花費幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="2d731-211">This may take a few moments.</span></span>
2. <span data-ttu-id="2d731-212">Management Studio 開啟時，顯示 hello**連接 tooServer**  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-212">When opening, Management Studio presents hello **Connect tooServer** dialog box.</span></span> <span data-ttu-id="2d731-213">在 hello**伺服器名稱** 方塊中，輸入 hello 名稱的 hello 虛擬機器 tooconnect toohello hello 物件總管 中使用 Database Engine。</span><span class="sxs-lookup"><span data-stu-id="2d731-213">In hello **Server name** box, type hello name of hello virtual machine tooconnect toohello Database Engine with hello Object Explorer.</span></span>
   <span data-ttu-id="2d731-214">(而不是 hello 虛擬機器名稱您也可以使用**（本機）**或單一句號當做 hello**伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="2d731-214">(Instead of hello virtual machine name you can also use **(local)** or a single period as hello **Server name**.</span></span> <span data-ttu-id="2d731-215">選取**Windows 驗證**，並將保留***您\_VM\_名稱*\\您\_本機\_系統管理員**在 hello**使用者名**方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-215">Select **Windows Authentication**, and leave ***your\_VM\_name*\\your\_local\_administrator** in hello **User name** box.</span></span> <span data-ttu-id="2d731-216">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="2d731-216">Click **Connect**.</span></span>
   
   ![連接 tooServer][6]
   
   <br>
   
   > [!TIP]
   > <span data-ttu-id="2d731-218">您可以變更 hello 的 SQL Server 驗證模式使用 Windows 登錄機碼變更，或使用 SQL Server Management Studio hello。</span><span class="sxs-lookup"><span data-stu-id="2d731-218">You may change hello SQL Server authentication mode using a Windows registry key change or using hello SQL Server Management Studio.</span></span> <span data-ttu-id="2d731-219">toochange 驗證模式使用 hello 登錄機碼變更，開始**新查詢**並執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="2d731-219">toochange authentication mode using hello registry key change, start a **New Query** and execute hello following script:</span></span>
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    <span data-ttu-id="2d731-220">使用 SQL Server management Studio toochange hello 驗證模式：</span><span class="sxs-lookup"><span data-stu-id="2d731-220">toochange hello authentication mode using SQL Server management Studio:</span></span>

1. <span data-ttu-id="2d731-221">在**SQL Server Management Studio 物件總管**hello 的 SQL Server （hello 虛擬機器名稱） 的執行個體名稱上按一下滑鼠右鍵，然後按**屬性**。</span><span class="sxs-lookup"><span data-stu-id="2d731-221">In **SQL Server Management Studio Object Explorer**, right-click the name of hello instance of SQL Server (hello virtual machine name), and then click **Properties**.</span></span>
   
   ![伺服器屬性][7]
2. <span data-ttu-id="2d731-223">Hello 上**安全性**頁面的 **伺服器驗證**，選取**SQL Server 及 Windows 驗證模式**，然後按一下**確定**.</span><span class="sxs-lookup"><span data-stu-id="2d731-223">On hello **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
   ![選取驗證模式][8]
3. <span data-ttu-id="2d731-225">在 hello **SQL Server Management Studio**對話方塊中，按一下 **確定**確認 hello 需求 toorestart SQL Server。</span><span class="sxs-lookup"><span data-stu-id="2d731-225">In hello **SQL Server Management Studio** dialog box, click **OK** to acknowledge hello requirement toorestart SQL Server.</span></span>
4. <span data-ttu-id="2d731-226">在 物件總管 中，以滑鼠右鍵按一下伺服器，然後按一下重新啟動。</span><span class="sxs-lookup"><span data-stu-id="2d731-226">In **Object Explorer**, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="2d731-227">(如果 SQL Server Agent 處於執行狀態，您也必須將其重新啟動。)</span><span class="sxs-lookup"><span data-stu-id="2d731-227">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
   ![重新啟動][9]
5. <span data-ttu-id="2d731-229">在 hello **SQL Server Management Studio**對話方塊中，按一下**是**同意要 toorestart SQL Server。</span><span class="sxs-lookup"><span data-stu-id="2d731-229">In hello **SQL Server Management Studio** dialog box, click **Yes** to agree that you want toorestart SQL Server.</span></span>

## <span data-ttu-id="2d731-230"><a name="Logins"></a>建立 SQL Server 驗證登入</span><span class="sxs-lookup"><span data-stu-id="2d731-230"><a name="Logins"></a>Create SQL Server authentication logins</span></span>
<span data-ttu-id="2d731-231">tooconnect toohello Database Engine 從另一部電腦，您必須建立至少一個 SQL Server 驗證登入。</span><span class="sxs-lookup"><span data-stu-id="2d731-231">tooconnect toohello Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>  

<span data-ttu-id="2d731-232">您也可以透過程式設計方式建立新的 SQL Server 登入，或使用 hello SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="2d731-232">You may create new SQL Server logins programmatically or using hello SQL Server Management Studio.</span></span> <span data-ttu-id="2d731-233">以程式設計的方式，開始使用 SQL 驗證新的系統管理員使用者 toocreate**新查詢**並執行下列指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="2d731-233">toocreate a new sysadmin user with SQL authentication programmatically, start a **New Query** and execute hello following script.</span></span> <span data-ttu-id="2d731-234">使用您選擇的「使用者名稱」和「密碼」取代 <新使用者名稱\> 和 <新密碼\>。</span><span class="sxs-lookup"><span data-stu-id="2d731-234">Replace <new user name\> and <new password\> with your choice of *user name* and *password*.</span></span> 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


<span data-ttu-id="2d731-235">視需要調整 hello 密碼原則 （hello 範例程式碼會關閉原則檢查和密碼到期日）。</span><span class="sxs-lookup"><span data-stu-id="2d731-235">Adjust hello password policy as needed (hello sample code turns off policy checking and password expiration).</span></span> <span data-ttu-id="2d731-236">如需 SQL Server 登入的詳細資訊，請參閱 [建立登入](http://msdn.microsoft.com/library/aa337562.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2d731-236">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>  

<span data-ttu-id="2d731-237">toocreate 新 SQL Server 登入使用 SQL Server Management Studio hello:</span><span class="sxs-lookup"><span data-stu-id="2d731-237">toocreate new SQL Server logins using hello SQL Server Management Studio:</span></span>

1. <span data-ttu-id="2d731-238">在**SQL Server Management Studio 物件總管**，展開您想在其中 toocreate hello 新登入的 hello 伺服器執行個體的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2d731-238">In **SQL Server Management Studio Object Explorer**, expand hello folder of hello server instance in which you want toocreate hello new login.</span></span>
2. <span data-ttu-id="2d731-239">以滑鼠右鍵按一下 hello**安全性**資料夾中，點太**新增**，然後選取**登入...**.</span><span class="sxs-lookup"><span data-stu-id="2d731-239">Right-click hello **Security** folder, point too**New**, and select **Login…**.</span></span>
   
   ![新增登入][10]
3. <span data-ttu-id="2d731-241">在 hello**登入-新增** 對話方塊上 hello**一般**頁面上，輸入 hello hello 新使用者名稱中 hello**登入名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-241">In hello **Login - New** dialog box, on hello **General** page, enter hello name of hello new user in hello **Login name** box.</span></span>
4. <span data-ttu-id="2d731-242">選取 [SQL Server 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="2d731-242">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="2d731-243">在 hello**密碼**方塊中，輸入 hello 新使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="2d731-243">In hello **Password** box, enter a password for hello new user.</span></span> <span data-ttu-id="2d731-244">該密碼一次輸入 hello**確認密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-244">Enter that password again into hello **Confirm Password** box.</span></span>
6. <span data-ttu-id="2d731-245">選取的複雜性和強制，tooenforce 密碼原則選項**強制執行密碼原則**（建議選項）。</span><span class="sxs-lookup"><span data-stu-id="2d731-245">tooenforce password policy options for complexity and enforcement, select **Enforce password policy** (recommended).</span></span> <span data-ttu-id="2d731-246">此為選取 SQL Server 驗證時的預設選項。</span><span class="sxs-lookup"><span data-stu-id="2d731-246">This is a default option when SQL Server authentication is selected.</span></span>
7. <span data-ttu-id="2d731-247">選取的到期日 tooenforce 密碼原則選項**強制執行密碼逾期**（建議選項）。</span><span class="sxs-lookup"><span data-stu-id="2d731-247">tooenforce password policy options for expiration, select **Enforce password expiration** (recommended).</span></span> <span data-ttu-id="2d731-248">強制執行密碼原則必須 tooenable 選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-248">Enforce password policy must be selected tooenable this checkbox.</span></span> <span data-ttu-id="2d731-249">此為選取 SQL Server 驗證時的預設選項。</span><span class="sxs-lookup"><span data-stu-id="2d731-249">This is a default option when SQL Server authentication is selected.</span></span>
8. <span data-ttu-id="2d731-250">選取 使用新密碼 hello 第一次登入之後，tooforce hello 使用者 toocreate**使用者必須變更密碼，在下次登入時**（建議使用此登入是否有人 else toouse。</span><span class="sxs-lookup"><span data-stu-id="2d731-250">tooforce hello user toocreate a new password after hello first time the login is used, select **User must change password at next login** (Recommended if this login is for someone else toouse.</span></span> <span data-ttu-id="2d731-251">如果 hello 登入是供自己使用，請勿選取此選項。）強制執行密碼逾期必須 tooenable 選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-251">If hello login is for your own use, do not select this option.) Enforce password expiration must be selected tooenable this checkbox.</span></span> <span data-ttu-id="2d731-252">此為選取 SQL Server 驗證時的預設選項。</span><span class="sxs-lookup"><span data-stu-id="2d731-252">This is a default option when SQL Server authentication is selected.</span></span>
9. <span data-ttu-id="2d731-253">從 hello**預設資料庫**清單中，選取 hello 登入的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d731-253">From hello **Default database** list, select a default database for hello login.</span></span> <span data-ttu-id="2d731-254">**主要**hello 預設值，這個選項。</span><span class="sxs-lookup"><span data-stu-id="2d731-254">**master** is hello default for this option.</span></span> <span data-ttu-id="2d731-255">如果您尚未建立使用者資料庫，將這個資料集太**主要**。</span><span class="sxs-lookup"><span data-stu-id="2d731-255">If you have not yet created a user database, leave this set too**master**.</span></span>
10. <span data-ttu-id="2d731-256">在 hello**預設語言**清單中，保留**預設**hello 值。</span><span class="sxs-lookup"><span data-stu-id="2d731-256">In hello **Default language** list, leave **default** as hello value.</span></span>
    
    ![登入屬性][11]
11. <span data-ttu-id="2d731-258">如果這是您要建立 hello 第一個登入，您可能想要將此登入指定為 SQL Server 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="2d731-258">If this is hello first login you are creating, you may want to designate this login as a SQL Server administrator.</span></span> <span data-ttu-id="2d731-259">如果是的話，請在 [伺服器角色] 頁面中勾選 [系統管理員 (sysadmin)]。</span><span class="sxs-lookup"><span data-stu-id="2d731-259">If so, on the **Server Roles** page, check **sysadmin**.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="2d731-260">Hello sysadmin 固定伺服器角色的成員擁有 hello Database Engine 的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="2d731-260">Members of hello sysadmin fixed server role have complete control of hello Database Engine.</span></span> <span data-ttu-id="2d731-261">基於安全性理由，請謹慎限制此角色的成員資格。</span><span class="sxs-lookup"><span data-stu-id="2d731-261">For security reasons, you should carefully restrict membership in this role.</span></span>
    > 
    > 
    
    ![系統管理員 (sysadmin)][12]
12. <span data-ttu-id="2d731-263">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d731-263">Click OK.</span></span>

## <span data-ttu-id="2d731-264"><a name="DNS"></a>判斷 hello hello 虛擬機器的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="2d731-264"><a name="DNS"></a>Determine hello DNS name of hello virtual machine</span></span>
<span data-ttu-id="2d731-265">tooconnect toohello SQL Server Database Engine 從另一部電腦，您必須知道 hello 網域名稱系統 (DNS) hello 虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="2d731-265">tooconnect toohello SQL Server Database Engine from another computer, you must know hello Domain Name System (DNS) name of hello virtual machine.</span></span>

<span data-ttu-id="2d731-266">（這是 hello 名稱 hello 網際網路使用 tooidentify hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d731-266">(This is hello name hello internet uses tooidentify hello virtual machine.</span></span> <span data-ttu-id="2d731-267">您可以使用 hello IP 位址，但當 Azure 基於冗餘或維護移動資源時，可能會變更 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2d731-267">You can use hello IP address, but hello IP address might change when Azure moves resources for redundancy or maintenance.</span></span> <span data-ttu-id="2d731-268">hello DNS 名稱將會是穩定，因為它可能會重新導向 tooa 新的 IP 位址。)</span><span class="sxs-lookup"><span data-stu-id="2d731-268">hello DNS name will be stable because it can be redirected tooa new IP address.)</span></span>

1. <span data-ttu-id="2d731-269">在 hello Azure 傳統入口網站 （或從 hello 上一個步驟），選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="2d731-269">In hello Azure Classic Portal (or from hello previous step), select **VIRTUAL MACHINES**.</span></span>
2. <span data-ttu-id="2d731-270">在 [hello**虛擬機器執行個體**] 頁面的 hello **DNS 名稱**hello 虛擬機器會出現的資料行中，尋找並複製 hello DNS 名稱前面加上**http://**。</span><span class="sxs-lookup"><span data-stu-id="2d731-270">On hello **VIRTUAL MACHINE INSTANCES** page, in hello **DNS NAME** column, find and copy hello DNS name for hello virtual machine which appears preceded by **http://**.</span></span> <span data-ttu-id="2d731-271">（hello 使用者介面可能不會顯示 hello 完整名稱，但您可以以滑鼠右鍵按一下它，然後選取 複製）。</span><span class="sxs-lookup"><span data-stu-id="2d731-271">(hello user interface might not display hello entire name, but you can right-click on it, and select copy.)</span></span>

## <span data-ttu-id="2d731-272"><a name="cde"></a>從另一部電腦連接 toohello Database Engine</span><span class="sxs-lookup"><span data-stu-id="2d731-272"><a name="cde"></a>Connect toohello Database Engine from another computer</span></span>
1. <span data-ttu-id="2d731-273">在電腦上連接 toohello 網際網路上，開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="2d731-273">On a computer connected toohello internet, open SQL Server Management Studio.</span></span>
2. <span data-ttu-id="2d731-274">在 hello**連接 tooServer**或**連接 tooDatabase 引擎**對話方塊中的，在 hello**伺服器名稱**方塊中，輸入虛擬機器 （決定 hello hello DNS 名稱前一項工作） 和公用端點連接埠號碼格式的 hello *DNSName，portnumber*例如**tutorialtestVM.cloudapp.net,57500**。</span><span class="sxs-lookup"><span data-stu-id="2d731-274">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, in hello **Server name** box, enter hello DNS name of the virtual machine (determined in hello previous task) and a public endpoint port number in hello format of *DNSName,portnumber* such as **tutorialtestVM.cloudapp.net,57500**.</span></span>
3. <span data-ttu-id="2d731-275">在 hello**驗證**方塊中，選取**SQL Server 驗證**。</span><span class="sxs-lookup"><span data-stu-id="2d731-275">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>
4. <span data-ttu-id="2d731-276">在 hello**登入**中，輸入您在稍早的工作中建立登入的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2d731-276">In hello **Login** box, type hello name of a login that you created in an earlier task.</span></span>
5. <span data-ttu-id="2d731-277">在 [hello**密碼**] 方塊中，輸入 hello 密碼 hello 登入您在稍早的工作中建立。</span><span class="sxs-lookup"><span data-stu-id="2d731-277">In hello **Password** box, type hello password of hello login that you create in an earlier task.</span></span>
6. <span data-ttu-id="2d731-278">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="2d731-278">Click **Connect**.</span></span>

## <span data-ttu-id="2d731-279"><a name="amlconnect"></a>從 Azure Machine Learning 連接 toohello Database Engine</span><span class="sxs-lookup"><span data-stu-id="2d731-279"><a name="amlconnect"></a>Connect toohello Database Engine from Azure Machine Learning</span></span>
<span data-ttu-id="2d731-280">在稍後階段 hello 小組資料科學程序，您將使用 hello [Azure Machine Learning Studio](https://studio.azureml.net) toobuild 和部署的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="2d731-280">In later stages of hello Team Data Science Process, you will use hello [Azure Machine Learning Studio](https://studio.azureml.net) toobuild and deploy machine learning models.</span></span> <span data-ttu-id="2d731-281">從您的 SQL Server VM 的資料庫直接在 Azure Machine Learning 定型或計分，tooingest 資料使用 hello**匯入資料**模組中新[Azure Machine Learning Studio](https://studio.azureml.net)實驗。</span><span class="sxs-lookup"><span data-stu-id="2d731-281">tooingest data from your SQL Server VM databases directly into Azure Machine Learning for training or scoring, use hello **Import Data** module in a new [Azure Machine Learning Studio](https://studio.azureml.net) experiment.</span></span> <span data-ttu-id="2d731-282">本主題涵蓋更多詳細資料，透過 hello 小組資料科學程序指南的連結。</span><span class="sxs-lookup"><span data-stu-id="2d731-282">This topic is covered in more details through hello Team Data Science Process guide links.</span></span> <span data-ttu-id="2d731-283">如需簡介，請參閱「 [什麼是 Azure Machine Learning Studio？」](machine-learning-what-is-ml-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="2d731-283">For an introduction, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md).</span></span>

1. <span data-ttu-id="2d731-284">在 hello**屬性**窗格中的 hello[資料匯入模組](https://msdn.microsoft.com/library/azure/dn905997.aspx)，選取**Azure SQL Database**從 hello**資料來源**下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="2d731-284">In hello **Properties** pane of hello [Import Data module](https://msdn.microsoft.com/library/azure/dn905997.aspx), select **Azure SQL Database** from hello **Data Source**     dropdown list.</span></span>
2. <span data-ttu-id="2d731-285">在 hello**資料庫伺服器名稱**文字方塊中，輸入`tcp:<DNS name of your virtual machine>,1433`</span><span class="sxs-lookup"><span data-stu-id="2d731-285">In hello **Database server name** text box, enter `tcp:<DNS name of your virtual machine>,1433`</span></span>
3. <span data-ttu-id="2d731-286">輸入 hello SQL 使用者名稱中 hello**伺服器使用者帳戶名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-286">Enter hello SQL user name in hello **Server user account name** text box.</span></span>
4. <span data-ttu-id="2d731-287">輸入 hello sql 使用者密碼在 hello**伺服器使用者帳戶密碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2d731-287">Enter hello sql user's password in hello **Server user account password** text box.</span></span>
   
   ![Azure Machine Learning 匯入資料][13]

## <span data-ttu-id="2d731-289"><a name="shutdown"></a>關閉並解除配置非使用中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2d731-289"><a name="shutdown"></a>Shutdown and deallocate virtual machine when not in use</span></span>
<span data-ttu-id="2d731-290">Azure 虛擬機器的定價策略是「 **只針對您使用的項目進行付費**」。</span><span class="sxs-lookup"><span data-stu-id="2d731-290">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="2d731-291">不會的 tooensure 時不使用虛擬機器，則需要付費，它具有 toobe 中的 hello**已停止 （取消配置）**狀態。</span><span class="sxs-lookup"><span data-stu-id="2d731-291">tooensure that you are not being billed when not using your virtual machine, it has toobe in hello **Stopped (Deallocated)** state.</span></span>

> [!NOTE]
> <span data-ttu-id="2d731-292">正在關閉 hello 虛擬機器從位於內部 （使用 Windows 電源選項），hello VM 已停止，但會維持配置。</span><span class="sxs-lookup"><span data-stu-id="2d731-292">Shutting down hello virtual machine from inside (using Windows power options), hello VM is stopped but remains allocated.</span></span> <span data-ttu-id="2d731-293">您不收費，tooensure 一律停止虛擬機器從 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2d731-293">tooensure you’re not being billed, always stop virtual machines from hello [Azure Classic Portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="2d731-294">您也可以停止 hello VM 透過 Powershell 太"PostShutdownAction 」 等呼叫 ShutdownRoleOperation"StoppedDeallocated"。</span><span class="sxs-lookup"><span data-stu-id="2d731-294">You can also stop hello VM through Powershell by calling ShutdownRoleOperation with "PostShutdownAction" equal too"StoppedDeallocated".</span></span>
> 
> 

<span data-ttu-id="2d731-295">tooshutdown 及取消配置 hello 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="2d731-295">tooshutdown and deallocate hello virtual machine:</span></span>

1. <span data-ttu-id="2d731-296">登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d731-296">Log in toohello [Azure Classic Portal](http://manage.windowsazure.com/) using your account.</span></span>  
2. <span data-ttu-id="2d731-297">選取**虛擬機器**從 hello 左側的導覽列。</span><span class="sxs-lookup"><span data-stu-id="2d731-297">Select **VIRTUAL MACHINES** from hello left navigation bar.</span></span>
3. <span data-ttu-id="2d731-298">在 hello 清單中的虛擬機器，按一下您的虛擬機器，然後移 toohello hello 名稱**儀表板**頁面。</span><span class="sxs-lookup"><span data-stu-id="2d731-298">In hello list of virtual machines, click on hello name of your virtual machine then go toohello **DASHBOARD** page.</span></span>
4. <span data-ttu-id="2d731-299">在 hello hello 頁面底部，按一下**關機**。</span><span class="sxs-lookup"><span data-stu-id="2d731-299">At hello bottom of hello page, click **SHUTDOWN**.</span></span>

![VM 關閉][15]

<span data-ttu-id="2d731-301">hello 虛擬機器將會取消配置，但是不會刪除。</span><span class="sxs-lookup"><span data-stu-id="2d731-301">hello virtual machine will be deallocated but not deleted.</span></span> <span data-ttu-id="2d731-302">您可以隨時從 hello Azure 傳統入口網站，以重新啟動您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d731-302">You may restart your virtual machine at any time from hello Azure Classic Portal.</span></span>

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a><span data-ttu-id="2d731-303">Azure SQL Server VM 已準備好 toouse： 後續步驟？</span><span class="sxs-lookup"><span data-stu-id="2d731-303">Your Azure SQL Server VM is ready toouse: what's next?</span></span>
<span data-ttu-id="2d731-304">您的虛擬機器就準備好在您的資料科學練習 toouse。</span><span class="sxs-lookup"><span data-stu-id="2d731-304">Your virtual machine is now ready toouse in your data science exercises.</span></span> <span data-ttu-id="2d731-305">也可以使用 IPython Notebook 伺服器 hello 瀏覽和處理的資料，以及其他工作搭配使用 Azure 機器學習和 hello 小組資料科學程序 (TDSP) hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d731-305">hello virtual machine is also ready for use as an IPython Notebook server for hello exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and hello Team Data Science Process (TDSP).</span></span>

<span data-ttu-id="2d731-306">hello hello 資料科學程序中的下一個步驟中的對應 hello[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)，而且可能包括將資料移入 HDInsight，程序、 範例它那里與 Azure 機器學習 hello 資料的準備步驟了解。</span><span class="sxs-lookup"><span data-stu-id="2d731-306">hello next steps in hello data science process are mapped in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

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

