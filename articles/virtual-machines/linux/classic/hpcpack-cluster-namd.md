---
title: "使用 Linux Vm 上的 Microsoft HPC Pack aaaNAMD |Microsoft 文件"
description: "在 Azure 上部署 Microsoft HPC Pack 叢集，並執行在多個 Linux 運算節點上具有 charmrun 的 NAMD 模擬"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="7ea16-103">在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD</span><span class="sxs-lookup"><span data-stu-id="7ea16-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="7ea16-104">本文章將示範其中一種方式 toorun Linux 高效能運算 (HPC) 工作負載在 Azure 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="7ea16-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="7ea16-105">在這裡，您將設定[Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)叢集在 Azure 上使用 Linux 計算節點，並執行[NAMD](http://www.ks.uiuc.edu/Research/namd/)模擬 toocalculate 和視覺化大型 biomolecular 系統 hello 結構。</span><span class="sxs-lookup"><span data-stu-id="7ea16-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="7ea16-106">**NAMD** （適用於 Nanoscale 屬於分子 Dynamics 程式） 專為高效能模擬大型 biomolecular 系統的設計平行屬於分子 dynamics 封裝包含的原子 toomillions 組成。</span><span class="sxs-lookup"><span data-stu-id="7ea16-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="7ea16-107">這些系統的範例包括病毒、儲存格結構和大型蛋白質。</span><span class="sxs-lookup"><span data-stu-id="7ea16-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="7ea16-108">NAMD 縮放 toohundreds 的典型的模擬和 toomore 比的 hello 最大模擬 500,000 個核心的核心。</span><span class="sxs-lookup"><span data-stu-id="7ea16-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="7ea16-109">**Microsoft HPC Pack**提供功能 toorun 大規模 HPC 和內部部署電腦或 Azure 虛擬機器在叢集中的平行應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea16-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="7ea16-110">HPC Pack 的開發前身為 Windows HPC 工作負載的解決方案，其現已支援於部署在 HPC Pack 叢集中的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea16-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="7ea16-111">如需簡介，請參閱 [在 Azure 的 HPC Pack 叢集中開始使用 Linux 運算節點](hpcpack-cluster.md) 。</span><span class="sxs-lookup"><span data-stu-id="7ea16-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="7ea16-112">針對其他選項 toorun Linux HPC 工作負載在 Azure 中，請參閱[技術資源，批次和高效能運算](../../../batch/batch-hpc-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="7ea16-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ea16-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ea16-113">Prerequisites</span></span>
* <span data-ttu-id="7ea16-114">**具備 Linux 計算節點的 HPC Pack 叢集** - 使用 [Azure Resource Manager 範本](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)或 [Azure PowerShell 指令碼](hpcpack-cluster-powershell-script.md)，在 Azure 上部署具備 Linux 計算節點的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ea16-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="7ea16-115">請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)hello 必要條件和步驟，針對任何一個選項。</span><span class="sxs-lookup"><span data-stu-id="7ea16-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="7ea16-116">如果您選擇 hello PowerShell 指令碼部署選項，請參閱這篇文章 hello 結尾 hello 範例檔案中的 hello 範例組態檔。</span><span class="sxs-lookup"><span data-stu-id="7ea16-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="7ea16-117">此檔案會設定 Windows Server 2012 R2 的前端節點和四個大型 CentOS 6.6 計算節點組成之以 Azure 為基礎的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ea16-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="7ea16-118">請視環境需要自訂此檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="7ea16-119">**NAMD 軟體和教學課程檔案**-適用於 Linux 下載 NAMD 軟體 hello [NAMD](http://www.ks.uiuc.edu/Research/namd/)站台 （需要註冊）。</span><span class="sxs-lookup"><span data-stu-id="7ea16-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="7ea16-120">這篇文章根據 NAMD 版本 2.10，並使用 hello [Linux x86_64 (64 位元 Intel/AMD 使用乙太網路)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310)封存。</span><span class="sxs-lookup"><span data-stu-id="7ea16-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="7ea16-121">也下載 hello [NAMD 教學課程檔案](http://www.ks.uiuc.edu/Training/Tutorials/#namd)。</span><span class="sxs-lookup"><span data-stu-id="7ea16-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="7ea16-122">hello 下載包括.tar 檔案，而您需要在 hello 叢集前端節點上的 Windows 工具 tooextract hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="7ea16-123">tooextract hello 檔案，請遵循本文中稍後的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="7ea16-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="7ea16-124">**VMD** （選用）-toosee hello 結果 NAMD 工作，下載並安裝 hello 屬於分子視覺效果程式[VMD](http://www.ks.uiuc.edu/Research/vmd/)您選擇的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7ea16-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="7ea16-125">hello 目前版本是 1.9.2。</span><span class="sxs-lookup"><span data-stu-id="7ea16-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="7ea16-126">請參閱的 hello VMD 下載網站 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="7ea16-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="7ea16-127">設定運算節點之間的相互信任</span><span class="sxs-lookup"><span data-stu-id="7ea16-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="7ea16-128">多個 Linux 節點上執行跨節點的作業需要 hello 節點 tootrust 彼此 (由**rsh**或**ssh**)。</span><span class="sxs-lookup"><span data-stu-id="7ea16-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="7ea16-129">當您建立 hello HPC Pack 叢集以 hello Microsoft HPC Pack IaaS 部署指令碼時，hello 指令碼會自動設定您指定的 hello 系統管理員帳戶的永久相互信任。</span><span class="sxs-lookup"><span data-stu-id="7ea16-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="7ea16-130">Hello 叢集的網域中建立的非管理員使用者，您必須 tooset 暫存 hello 節點間的相互信任工作配置 toothem 時。</span><span class="sxs-lookup"><span data-stu-id="7ea16-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="7ea16-131">Hello 作業完成之後，然後摧毀 hello 關聯性。</span><span class="sxs-lookup"><span data-stu-id="7ea16-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="7ea16-132">toodo 這每位使用者提供的 RSA 金鑰組 toohello 叢集的 HPC Pack 會使用 tooestablish hello 信任關係。</span><span class="sxs-lookup"><span data-stu-id="7ea16-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="7ea16-133">指示如下。</span><span class="sxs-lookup"><span data-stu-id="7ea16-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="7ea16-134">產生 RSA 金鑰組</span><span class="sxs-lookup"><span data-stu-id="7ea16-134">Generate an RSA key pair</span></span>
<span data-ttu-id="7ea16-135">這是簡單 toogenerate RSA 金鑰組，其中包含公開金鑰和私密金鑰，藉由執行 hello Linux**透過像是**命令。</span><span class="sxs-lookup"><span data-stu-id="7ea16-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="7ea16-136">登入 tooa Linux 電腦。</span><span class="sxs-lookup"><span data-stu-id="7ea16-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="7ea16-137">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea16-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="7ea16-138">按**Enter** hello 命令完成之前 toouse hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="7ea16-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="7ea16-139">請勿在這裡輸入複雜密碼；當系統提示您輸入密碼時，只要按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="7ea16-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![產生 RSA 金鑰組][keygen]
3. <span data-ttu-id="7ea16-141">變更目錄 toohello ~/.ssh 目錄。</span><span class="sxs-lookup"><span data-stu-id="7ea16-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="7ea16-142">hello 私密金鑰會儲存在 id_rsa 和 hello id_rsa.pub 中的公用金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ea16-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![私密和公開金鑰][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="7ea16-144">新增 hello 金鑰組 toohello HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="7ea16-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="7ea16-145">[遠端桌面連線](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toohello 前端節點 VM 使用 hello 時部署 hello 叢集 (例如，hpc\clusteradmin) 所提供的網域認證。</span><span class="sxs-lookup"><span data-stu-id="7ea16-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="7ea16-146">您可以管理 hello 叢集從 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="7ea16-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="7ea16-147">Hello 叢集的 Active Directory 網域中使用標準的 Windows Server 程序 toocreate 網域使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ea16-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="7ea16-148">例如，使用 hello Active Directory 使用者和電腦 工具 hello 前端節點上。</span><span class="sxs-lookup"><span data-stu-id="7ea16-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="7ea16-149">本文中的 hello 範例假設您建立名為 hpcuser hello hpclab 網域 (hpclab\hpcuser) 中的網域使用者。</span><span class="sxs-lookup"><span data-stu-id="7ea16-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="7ea16-150">將 hello 網域使用者 toohello HPC Pack 叢集新增為叢集使用者。</span><span class="sxs-lookup"><span data-stu-id="7ea16-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="7ea16-151">如需指示，請參閱 [(Add or Remove Cluster Users) 新增或移除叢集使用者](https://technet.microsoft.com/library/ff919330.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea16-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="7ea16-152">建立具名 C:\cred.xml 和複製 hello RSA 索引鍵資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="7ea16-153">您可以找到範例在 hello hello 本文結尾處的範例檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="7ea16-154">開啟命令提示字元並輸入下列命令 tooset hello 認證 hello hpclab\hpcuser 帳戶資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="7ea16-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="7ea16-155">使用 hello **x**參數 toopass hello hello C:\cred.xml 檔案名稱建立 hello 索引鍵的資料。</span><span class="sxs-lookup"><span data-stu-id="7ea16-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="7ea16-156">這個命令會成功完成而沒有輸出。</span><span class="sxs-lookup"><span data-stu-id="7ea16-156">This command completes successfully without output.</span></span> <span data-ttu-id="7ea16-157">設定 hello hello 需要 toorun 作業的使用者帳戶的認證之後, hello cred.xml 檔儲存在安全的位置，或將它刪除。</span><span class="sxs-lookup"><span data-stu-id="7ea16-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="7ea16-158">如果您在其中 Linux 節點上產生 hello RSA 金鑰組，請記得 toodelete hello 索引鍵使用它們完畢之後。</span><span class="sxs-lookup"><span data-stu-id="7ea16-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="7ea16-159">如果 HPC Pack 找到現有的 id_rsa 檔案或 id_rsa.pub 檔案，則它不會設定相互信任。</span><span class="sxs-lookup"><span data-stu-id="7ea16-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ea16-160">我們不建議叢集系統管理員身分執行 Linux 作業上共用的叢集，因為系統管理員所提交的工作是 hello 根帳號底下執行 hello Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7ea16-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="7ea16-161">非系統管理員使用者所提交的工作會以 hello 作業的使用者名稱相同的 hello 與執行本機 Linux 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ea16-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="7ea16-162">在此情況下，HPC Pack 會相互信任此 Linux 使用者的所有 hello 節點配置 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="7ea16-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="7ea16-163">您可以設定 hello Linux 使用者 hello Linux 節點上手動執行 hello 作業之前或 HPC Pack hello 使用者會自動建立時送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="7ea16-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="7ea16-164">如果 HPC Pack 建立 hello 使用者，HPC Pack hello 作業完成之後刪除它。</span><span class="sxs-lookup"><span data-stu-id="7ea16-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="7ea16-165">hello hello 節點上的 hello 作業完成之後，會移除金鑰 tooreduce 安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="7ea16-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="7ea16-166">為 Linux 節點設定檔案共用</span><span class="sxs-lookup"><span data-stu-id="7ea16-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="7ea16-167">現在設定 SMB 檔案共用，然後掛接 hello 的所有 Linux 節點 tooallow hello Linux 節點 tooaccess NAMD 檔案的一般路徑上的共用的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ea16-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="7ea16-168">以下是步驟 toomount hello 前端節點上的共用資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ea16-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="7ea16-169">共用目前不支援 hello Azure 檔案服務，例如 CentOS 6.6 分佈的建議。</span><span class="sxs-lookup"><span data-stu-id="7ea16-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="7ea16-170">如果您的 Linux 節點支援的 Azure 檔案共用，請參閱[如何 toouse Linux 的 Azure 檔案儲存體](../../../storage/files/storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="7ea16-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="7ea16-171">如需 HPC Pack 的其他檔案共用選項，請參閱 [開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點](hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="7ea16-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="7ea16-172">Hello 前端節點上建立資料夾，並共用它 tooEveryone 藉由設定 讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="7ea16-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="7ea16-173">在此範例中， \\ \\CentOS66HN\Namd 是 hello CentOS66HN 所在 hello 的 hello 前端節點的主機名稱的 hello 資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="7ea16-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="7ea16-174">建立名為 namd2 hello 共用資料夾中的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ea16-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="7ea16-175">在 namd2 中，建立另一個名為 namdsample 的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ea16-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="7ea16-176">使用的 Windows 版本來擷取 hello 資料夾中的 hello NAMD 檔案**tar 檔案解壓縮**或其他.tar 保存檔運作的 Windows 公用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea16-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="7ea16-177">太解壓縮 hello NAMD tar 檔案解壓縮的封存\\\\CentOS66HN\Namd\namd2。</span><span class="sxs-lookup"><span data-stu-id="7ea16-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="7ea16-178">擷取下的 hello 教學課程檔案\\ \\CentOS66HN\Namd\namd2\namdsample。</span><span class="sxs-lookup"><span data-stu-id="7ea16-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="7ea16-179">開啟 Windows PowerShell 視窗並執行下列命令 toomount hello hello Linux 節點上的共用的資料夾的 hello。</span><span class="sxs-lookup"><span data-stu-id="7ea16-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="7ea16-180">hello 第一個命令會建立名為 /namd2 hello LinuxNodes 群組中的所有節點上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ea16-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="7ea16-181">hello 第二個命令會掛接到 dir_mode 和 file_mode 位元組 too777 hello 資料夾 hello 共用資料夾 //CentOS66HN/Namd/namd2。</span><span class="sxs-lookup"><span data-stu-id="7ea16-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="7ea16-182">hello *username*和*密碼*hello 命令應該 hello hello 前端節點上的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="7ea16-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea16-183">hello"\\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="7ea16-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7ea16-184">「\\`，"表示 hello"，"（逗號字元） 是 hello 命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ea16-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="7ea16-185">建立 Bash 指令碼 toorun NAMD 作業</span><span class="sxs-lookup"><span data-stu-id="7ea16-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="7ea16-186">NAMD 作業需要*nodelist*檔，以取得**charmrun**啟動 NAMD 處理程序時，節點 toouse toodetermine hello 數目。</span><span class="sxs-lookup"><span data-stu-id="7ea16-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="7ea16-187">使用 Bash 指令碼會產生 hello nodelist 檔案，並執行**charmrun**與此節點清單檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="7ea16-188">然後您就可以在會呼叫此指令碼的 HPC 叢集管理員中提交 NAMD 工作。</span><span class="sxs-lookup"><span data-stu-id="7ea16-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="7ea16-189">使用您選擇的文字編輯器，在包含 hello NAMD 程式檔案的 hello /namd2 資料夾中建立 Bash 指令碼，並命名 hpccharmrun.sh。快速概念證明，將在本文的 hello 結尾處提供的 hello 範例 hpccharmrun.sh 指令碼複製並移過[提交 NAMD 工作](#submit-a-namd-job)。</span><span class="sxs-lookup"><span data-stu-id="7ea16-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="7ea16-190">將您的指令碼儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="7ea16-191">這可確保正常 hello Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7ea16-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="7ea16-192">以下是這個 bash 指令碼的詳細作業內容。</span><span class="sxs-lookup"><span data-stu-id="7ea16-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="7ea16-193">定義一些變數。</span><span class="sxs-lookup"><span data-stu-id="7ea16-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="7ea16-194">收到 hello 環境變數中的節點資訊。</span><span class="sxs-lookup"><span data-stu-id="7ea16-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="7ea16-195">$NODESCORES 會儲存來自 $CCP_NODES_CORES 的分割單字清單。</span><span class="sxs-lookup"><span data-stu-id="7ea16-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="7ea16-196">$COUNT 是 $NODESCORES hello 大小。</span><span class="sxs-lookup"><span data-stu-id="7ea16-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="7ea16-197">hello hello $CCP_NODES_CORES 變數的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="7ea16-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="7ea16-198">這個變數會列出節點、 節點名稱，以及每個節點上配置 toohello 作業的核心數目的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="7ea16-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="7ea16-199">例如，如果 hello 作業需要 10 個核心 toorun，$CCP_NODES_CORES 的 hello 值就會類似：</span><span class="sxs-lookup"><span data-stu-id="7ea16-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="7ea16-200">如果未設定 hello $CCP_NODES_CORES 變數，啟動**charmrun**直接。</span><span class="sxs-lookup"><span data-stu-id="7ea16-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="7ea16-201">(這應該只有當您在 Linux 節點上直接執行這個指令碼時才會發生。)</span><span class="sxs-lookup"><span data-stu-id="7ea16-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="7ea16-202">或者為 **charmrun**建立節點清單檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="7ea16-203">執行**charmrun** hello nodelist 檔案後，收到其傳回的狀態，並移除 hello 結尾 hello nodelist 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea16-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="7ea16-204">${CCP_NUMCPUS} 是 hello HPC Pack 前端節點所設定的另一個環境變數。</span><span class="sxs-lookup"><span data-stu-id="7ea16-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="7ea16-205">它會儲存 hello 總配置 toothis 作業的核心數目。</span><span class="sxs-lookup"><span data-stu-id="7ea16-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="7ea16-206">我們將它的處理序 toospecify hello 數目用於 charmrun。</span><span class="sxs-lookup"><span data-stu-id="7ea16-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="7ea16-207">以 hello 結束**charmrun**傳回狀態。</span><span class="sxs-lookup"><span data-stu-id="7ea16-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="7ea16-208">以下是在 hello nodelist 檔案中，哪些 hello 指令碼會產生 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="7ea16-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="7ea16-209">例如：</span><span class="sxs-lookup"><span data-stu-id="7ea16-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="7ea16-210">提交 NAMD 作業</span><span class="sxs-lookup"><span data-stu-id="7ea16-210">Submit a NAMD job</span></span>
<span data-ttu-id="7ea16-211">現在您已準備好 toosubmit NAMD 作業 HPC 叢集管理員中。</span><span class="sxs-lookup"><span data-stu-id="7ea16-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="7ea16-212">連接 tooyour 叢集前端節點，並啟動 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="7ea16-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="7ea16-213">在**資源管理**，確保 hello Linux 計算節點處於 hello**線上**狀態。</span><span class="sxs-lookup"><span data-stu-id="7ea16-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="7ea16-214">如果不是，請選取這些節點，然後按一下 [ **上線**]。</span><span class="sxs-lookup"><span data-stu-id="7ea16-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="7ea16-215">在 [工作管理] 中，按一下 [新增工作]。</span><span class="sxs-lookup"><span data-stu-id="7ea16-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="7ea16-216">輸入工作的名稱，例如 *hpccharmrun*。</span><span class="sxs-lookup"><span data-stu-id="7ea16-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![新的 HPC 工作][namd_job]
5. <span data-ttu-id="7ea16-218">Hello 上**工作詳細資料**頁面的 **作業資源**，選取資源類型 hello**節點**組 hello 和**最小值**too3。</span><span class="sxs-lookup"><span data-stu-id="7ea16-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="7ea16-219">我們在三個 Linux 節點上執行 hello 工作和每個節點都有四個核心。</span><span class="sxs-lookup"><span data-stu-id="7ea16-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![工作資源][job_resources]
6. <span data-ttu-id="7ea16-221">按一下**編輯工作**在 hello 左側的瀏覽，然後按一下**新增**tooadd 工作 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="7ea16-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="7ea16-222">在 hello**工作詳細資料和 I/O 重新導向**頁面上，設定下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea16-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="7ea16-223">**命令列** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="7ea16-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="7ea16-224">hello 上述命令列是單一命令，但不含分行符號。</span><span class="sxs-lookup"><span data-stu-id="7ea16-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="7ea16-225">在下方的數行包裝 tooappear**命令列**。</span><span class="sxs-lookup"><span data-stu-id="7ea16-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="7ea16-226">**工作目錄** - /namd2</span><span class="sxs-lookup"><span data-stu-id="7ea16-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="7ea16-227">**最小值** - 3</span><span class="sxs-lookup"><span data-stu-id="7ea16-227">**Minimum** - 3</span></span>
     
     ![作業詳細資料][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="7ea16-229">Hello 工作目錄在這裡設定因為**charmrun** toonavigate toohello 會嘗試每個節點上相同的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="7ea16-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="7ea16-230">如果您未設定 hello 工作目錄，HPC Pack 會建立在其中 hello Linux 節點上的隨機命名資料夾中啟動 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="7ea16-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="7ea16-231">這會導致下列錯誤上 hello hello 其他節點： `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid 這個問題，請指定可以存取的所有節點，為 hello 工作目錄的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="7ea16-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="7ea16-232">按一下**確定**，然後按一下**送出**toorun 這項作業。</span><span class="sxs-lookup"><span data-stu-id="7ea16-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="7ea16-233">根據預設，HPC Pack 送出 hello 與您目前的登入的使用者帳戶的作業。</span><span class="sxs-lookup"><span data-stu-id="7ea16-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="7ea16-234">對話方塊可能會提示您 tooenter hello 使用者名稱和密碼之後，您按一下**送出**。</span><span class="sxs-lookup"><span data-stu-id="7ea16-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![工作認證][creds]
   
   <span data-ttu-id="7ea16-236">在某些情況下 HPC Pack 會記住您之前輸入，而不會顯示此對話方塊中的 hello 使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="7ea16-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="7ea16-237">toomake HPC Pack 會使它再次顯示中，輸入下列命令，在命令提示字元中的 hello，再提交 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="7ea16-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="7ea16-238">hello 作業已執行幾分鐘的時間 toofinish。</span><span class="sxs-lookup"><span data-stu-id="7ea16-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="7ea16-239">尋找在 hello 作業記錄\\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log 和 hello 輸出中的檔案\\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="7ea16-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="7ea16-240">（選擇性） 啟動 VMD tooview 工作結果。</span><span class="sxs-lookup"><span data-stu-id="7ea16-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="7ea16-241">hello 步驟視覺化 hello NAMD 輸出檔 （在此情況下，在水球體 ubiquitin 蛋白質分子） 已超出本文的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="7ea16-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="7ea16-242">如需詳細資訊，請參閱 [NAMD 教學課程](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) 。</span><span class="sxs-lookup"><span data-stu-id="7ea16-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![工作結果][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="7ea16-244">範例檔案</span><span class="sxs-lookup"><span data-stu-id="7ea16-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="7ea16-245">PowerShell 指令碼叢集部署的 XML 組態檔範例</span><span class="sxs-lookup"><span data-stu-id="7ea16-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="7ea16-246">範例 cred.xml 檔案</span><span class="sxs-lookup"><span data-stu-id="7ea16-246">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="7ea16-247">範例 hpccharmrun.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="7ea16-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
