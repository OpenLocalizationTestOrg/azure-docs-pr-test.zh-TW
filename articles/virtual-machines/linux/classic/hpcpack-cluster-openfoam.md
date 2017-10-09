---
title: "使用 Linux Vm 上的 HPC Pack OpenFOAM aaaRun |Microsoft 文件"
description: "在 Azure 上部署 Microsoft HPC Pack 叢集，並且跨 RDMA 網路在多個 Linux 計算節點上執行 OpenFOAM 工作。"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="7a939-103">在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFoam</span><span class="sxs-lookup"><span data-stu-id="7a939-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="7a939-104">本文將告訴您其中一種方式 toorun OpenFoam Azure 虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="7a939-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="7a939-105">在這裡，您將在 Azure 上部署一個具有 Linux 計算節點的 Microsoft HPC Pack 叢集，並使用 Intel MPI 來執行 [OpenFoam](http://openfoam.com/) 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="7a939-106">可用於具備 RDMA 功能的 Azure Vm hello 計算節點，以便透過 hello Azure RDMA 網路通訊 hello 計算節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="7a939-107">在 Azure 中的 OpenFoam 完全包含其他選項 toorun 設定商業映像用於 hello Marketplace，例如 UberCloud 的[OpenFoam 2.3 上 CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)，以及執行[Azure 批次](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/)。</span><span class="sxs-lookup"><span data-stu-id="7a939-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7a939-108">OpenFOAM (代表 Open Field Operation and Manipulation) 是一個開放原始碼計算流體力學 (CFD) 軟體套件，廣泛運用在商業和學術組織的工程及科學領域中。</span><span class="sxs-lookup"><span data-stu-id="7a939-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="7a939-109">其中包含網格處理工具，特別是 snappyHexMesh，這是一種用於複雜 CAD 幾何的前置和後置處理的平行化網格處理器。</span><span class="sxs-lookup"><span data-stu-id="7a939-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="7a939-110">幾乎所有處理序平行執行，讓使用者 tootake 充分利用電腦硬體可供使用。</span><span class="sxs-lookup"><span data-stu-id="7a939-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="7a939-111">Microsoft HPC Pack 提供功能 toorun 大規模 HPC 和平行應用程式，包括 MPI 應用程式，在 Microsoft Azure 虛擬機器的叢集上。</span><span class="sxs-lookup"><span data-stu-id="7a939-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="7a939-112">HPC Pack 也支援在 HPC Pack 叢集中部署的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a939-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="7a939-113">請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)簡介 toousing for Linux 計算使用 HPC Pack 的節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="7a939-114">本文將說明如何 toorun Linux MPI 工作負載使用 HPC Pack。</span><span class="sxs-lookup"><span data-stu-id="7a939-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="7a939-115">本文假設您對 Linux 系統管理及在 Linux 叢集上執行 MPI 工作負載，有某種程度的熟悉。</span><span class="sxs-lookup"><span data-stu-id="7a939-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="7a939-116">如果您使用的 MPI 和 OpenFOAM hello 本文中所顯示的不同版本，您可能必須 toomodify 一些安裝和設定步驟。</span><span class="sxs-lookup"><span data-stu-id="7a939-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7a939-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a939-117">Prerequisites</span></span>
* <span data-ttu-id="7a939-118">**具有支援 RDMA 之 Linux 計算節點的 HPC Pack 叢集** - 使用 [Azure Resource Manager 範本](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)或 [Azure PowerShell 指令碼](hpcpack-cluster-powershell-script.md)，部署具有 A8、A9、H16r 或 H16rm 大小之 Linux 計算節點的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="7a939-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="7a939-119">請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)hello 必要條件和步驟，針對任何一個選項。</span><span class="sxs-lookup"><span data-stu-id="7a939-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="7a939-120">如果您選擇 hello PowerShell 指令碼部署選項，請參閱這篇文章 hello 結尾 hello 範例檔案中的 hello 範例組態檔。</span><span class="sxs-lookup"><span data-stu-id="7a939-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="7a939-121">使用此設定以 Azure 為基礎的 toodeploy HPC Pack 叢集大小 A8 Windows Server 2012 R2 前端節點所組成，再 2 大小 A8 SUSE Linux Enterprise Server 12 計算節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="7a939-122">請將您的訂用帳戶和服務名稱取代為適當的值。</span><span class="sxs-lookup"><span data-stu-id="7a939-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="7a939-123">**其他注意事項 tooknow**</span><span class="sxs-lookup"><span data-stu-id="7a939-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="7a939-124">如需 Azure 的 Linux RDMA 網路必要條件，請參閱[高效能運算 VM 大小](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a939-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="7a939-125">如果您使用 hello Powershell 指令碼部署選項，將部署的所有 hello Linux 運算節點內一個雲端服務 toouse hello RDMA 網路連線。</span><span class="sxs-lookup"><span data-stu-id="7a939-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="7a939-126">部署之後 hello Linux 節點，透過 SSH tooperform 連接任何額外的管理工作。</span><span class="sxs-lookup"><span data-stu-id="7a939-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="7a939-127">Hello Azure 入口網站中尋找每個 Linux VM hello SSH 連線詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7a939-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="7a939-128">**Intel MPI** -toorun SLES 12 hpc OpenFOAM 計算節點在 Azure 中的，您必須從 hello tooinstall hello Intel MPI 文件庫 5 執行階段[Intel.com 網站](https://software.intel.com/en-us/intel-mpi-library/)。</span><span class="sxs-lookup"><span data-stu-id="7a939-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="7a939-129">(Intel MPI 5 已預先安裝在 CentOS 型 HPC 映像上)。在稍後的步驟中，請視需要在 Linux 計算節點上安裝 Intel MPI。</span><span class="sxs-lookup"><span data-stu-id="7a939-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="7a939-130">tooprepare 此步驟中，您向 Intel 之後, 請依照 hello 確認電子郵件 toohello 相關網頁中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="7a939-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="7a939-131">然後，複製 hello 下載 Intel MPI hello 適當版本的 hello.tgz 檔案連結。</span><span class="sxs-lookup"><span data-stu-id="7a939-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="7a939-132">這篇文章根據 Intel MPI 5.0.3.048 版。</span><span class="sxs-lookup"><span data-stu-id="7a939-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="7a939-133">**OpenFOAM 來源組件**-從 hello，下載適用於 Linux 的 hello OpenFOAM 來源組件軟體[OpenFOAM Foundation 網站](http://openfoam.org/download/2-3-1-source/)。</span><span class="sxs-lookup"><span data-stu-id="7a939-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="7a939-134">本文是依據 Source Pack 2.3.1 版 (可透過 OpenFOAM-2.3.1.tgz 的形式下載) 而撰寫的。</span><span class="sxs-lookup"><span data-stu-id="7a939-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="7a939-135">稍後在本文章 toounpack 遵循 hello 和編譯 OpenFOAM hello Linux 計算節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="7a939-136">**EnSight** （選用）-您的 OpenFOAM 模擬 toosee hello 結果下載並安裝 hello [EnSight](https://www.ceisoftware.com/download/)視覺效果與分析的程式。</span><span class="sxs-lookup"><span data-stu-id="7a939-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="7a939-137">授權和下載資訊是在 hello EnSight 站台。</span><span class="sxs-lookup"><span data-stu-id="7a939-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="7a939-138">設定運算節點之間的相互信任</span><span class="sxs-lookup"><span data-stu-id="7a939-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="7a939-139">多個 Linux 節點上執行跨節點的作業需要 hello 節點 tootrust 彼此 (由**rsh**或**ssh**)。</span><span class="sxs-lookup"><span data-stu-id="7a939-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="7a939-140">當您建立 hello HPC Pack 叢集以 hello Microsoft HPC Pack IaaS 部署指令碼時，hello 指令碼會自動設定您指定的 hello 系統管理員帳戶的永久相互信任。</span><span class="sxs-lookup"><span data-stu-id="7a939-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="7a939-141">Hello 叢集的網域中建立的非管理員使用者，您必須 tooset 暫存 hello 節點間的相互信任工作配置 toothem，和 hello 作業完成之後終結 hello 關聯性時。</span><span class="sxs-lookup"><span data-stu-id="7a939-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="7a939-142">每位使用者的 tooestablish 信任提供 HPC Pack 使用 hello 信任關係的 RSA 金鑰組 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="7a939-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="7a939-143">產生 RSA 金鑰組</span><span class="sxs-lookup"><span data-stu-id="7a939-143">Generate an RSA key pair</span></span>
<span data-ttu-id="7a939-144">這是簡單 toogenerate RSA 金鑰組，其中包含公開金鑰和私密金鑰，藉由執行 hello Linux**透過像是**命令。</span><span class="sxs-lookup"><span data-stu-id="7a939-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="7a939-145">登入 tooa Linux 電腦。</span><span class="sxs-lookup"><span data-stu-id="7a939-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="7a939-146">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a939-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="7a939-147">按**Enter** hello 命令完成之前 toouse hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="7a939-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="7a939-148">請勿在這裡輸入複雜密碼；當系統提示您輸入密碼時，只要按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="7a939-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![產生 RSA 金鑰組][keygen]
3. <span data-ttu-id="7a939-150">變更目錄 toohello ~/.ssh 目錄。</span><span class="sxs-lookup"><span data-stu-id="7a939-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="7a939-151">hello 私密金鑰會儲存在 id_rsa 和 hello id_rsa.pub 中的公用金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a939-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![私密和公開金鑰][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="7a939-153">新增 hello 金鑰組 toohello HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="7a939-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="7a939-154">請 HPC Pack 系統管理員帳戶 （您執行 hello 部署指令碼時設定 hello 系統管理員帳戶） 的遠端桌面連線 tooyour 前端節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="7a939-155">Hello 叢集的 Active Directory 網域中使用標準的 Windows Server 程序 toocreate 網域使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a939-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="7a939-156">例如，使用 hello Active Directory 使用者和電腦 工具 hello 前端節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="7a939-157">本文中的 hello 範例假設您建立名為 hpclab\hpcuser 的網域使用者。</span><span class="sxs-lookup"><span data-stu-id="7a939-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="7a939-158">建立具名 C:\cred.xml 和複製 hello RSA 索引鍵資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="7a939-159">範例 cred.xml 檔案是在 hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="7a939-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="7a939-160">開啟命令提示字元並輸入下列命令 tooset hello 認證 hello hpclab\hpcuser 帳戶資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="7a939-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="7a939-161">使用 hello **x**參數 toopass hello C:\cred.xml 您建立 hello 主要資料檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a939-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="7a939-162">這個命令會成功完成而沒有輸出。</span><span class="sxs-lookup"><span data-stu-id="7a939-162">This command completes successfully without output.</span></span> <span data-ttu-id="7a939-163">設定 hello hello 需要 toorun 作業的使用者帳戶的認證之後, hello cred.xml 檔儲存在安全的位置，或將它刪除。</span><span class="sxs-lookup"><span data-stu-id="7a939-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="7a939-164">如果您在其中 Linux 節點上產生 hello RSA 金鑰組，請記得 toodelete hello 索引鍵使用它們完畢之後。</span><span class="sxs-lookup"><span data-stu-id="7a939-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="7a939-165">如果 HPC Pack 找到現有的 id_rsa 檔案或 id_rsa.pub 檔案，它就不會設定相互信任。</span><span class="sxs-lookup"><span data-stu-id="7a939-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a939-166">我們不建議叢集系統管理員身分執行 Linux 作業上共用的叢集，因為系統管理員所提交的工作是 hello 根帳號底下執行 hello Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="7a939-167">不過，非管理員使用者所提交的工作在本機 Linux 使用者帳戶下執行以 hello 作業的使用者名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="7a939-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="7a939-168">在此情況下，HPC Pack 設定此 Linux 使用者的互信 hello 節點配置 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="7a939-169">您可以設定 hello Linux 使用者 hello Linux 節點上手動執行 hello 作業之前或 HPC Pack hello 使用者會自動建立時送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="7a939-170">如果 HPC Pack 建立 hello 使用者，HPC Pack hello 作業完成之後刪除它。</span><span class="sxs-lookup"><span data-stu-id="7a939-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="7a939-171">tooreduce 安全性威脅，HPC Pack 在作業完成之後移除 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a939-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="7a939-172">為 Linux 節點設定檔案共用</span><span class="sxs-lookup"><span data-stu-id="7a939-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="7a939-173">現在設定標準的 SMB 共用資料夾上 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="7a939-174">tooallow hello Linux 節點 tooaccess 應用程式具有通用的路徑，掛接 hello 共用檔案 hello Linux 節點上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a939-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="7a939-175">如果您想，您可以使用其他檔案共用選項 (例如 Azure 檔案共用，在許多案例中皆建議使用此選項) 或 NFS 共用。</span><span class="sxs-lookup"><span data-stu-id="7a939-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="7a939-176">請參閱 hello 檔案共用資訊和詳細的步驟，以[開始使用 Linux 在 Azure 中的 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="7a939-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="7a939-177">Hello 前端節點上建立資料夾，並共用它 tooEveryone 藉由設定 讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="7a939-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="7a939-178">例如，hello 與前端節點上的共用 C:\OpenFOAM \\ \\SUSE12RDMA HN\OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a939-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="7a939-179">在這裡， *SUSE12RDMA HN* hello 前端節點 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="7a939-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="7a939-180">開啟 Windows PowerShell 視窗並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a939-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="7a939-181">hello 第一個命令會建立名為 /openfoam hello LinuxNodes 群組中的所有節點上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a939-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="7a939-182">hello 第二個命令會掛接 hello 共用資料夾 //SUSE12RDMA-HN/OpenFOAM dir_mode 和 file_mode 位元組 too777 與 hello Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="7a939-183">hello *username*和*密碼*hello 命令應該 hello hello 前端節點上的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="7a939-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="7a939-184">hello"\\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="7a939-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7a939-185">「\\`，"表示 hello"，"（逗號字元） 是 hello 命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="7a939-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="7a939-186">安裝 MPI 和 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="7a939-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="7a939-187">toorun OpenFOAM 以 hello RDMA 網路的 MPI 工作，您需要 toocompile OpenFOAM hello Intel MPI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7a939-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="7a939-188">首先，執行數個**clusrun** tooinstall Intel MPI 程式庫 （如果尚未安裝） OpenFOAM 指令在 Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="7a939-189">設定在 hello Linux 節點之間 tooshare hello 安裝檔案的先前使用 hello 前端節點共用。</span><span class="sxs-lookup"><span data-stu-id="7a939-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a939-190">這些安裝和編譯步驟是範例。</span><span class="sxs-lookup"><span data-stu-id="7a939-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="7a939-191">您必須已正確安裝相依的編譯器和程式庫的 Linux 系統管理 tooensure 的一些知識。</span><span class="sxs-lookup"><span data-stu-id="7a939-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="7a939-192">您可能需要 toomodify 某些環境變數或其他設定您的 Intel MPI 和 OpenFOAM 版本。</span><span class="sxs-lookup"><span data-stu-id="7a939-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="7a939-193">如需詳細資料，請參閱適用於您環境的 [Intel MPI Library for Linux 安裝指南](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html)和 [OpenFOAM Source Pack 安裝](http://openfoam.org/download/2-3-1-source/)。</span><span class="sxs-lookup"><span data-stu-id="7a939-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="7a939-194">安裝 Intel MPI</span><span class="sxs-lookup"><span data-stu-id="7a939-194">Install Intel MPI</span></span>
<span data-ttu-id="7a939-195">儲存 hello 下載的安裝套件的 Intel MPI (在此範例中 l_mpi_p_5.0.3.048.tgz) 中 C:\OpenFoam hello 前端節點上，從 /openfoam hello Linux 節點均可存取此檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="7a939-196">然後執行**clusrun** tooinstall Intel MPI 所有 hello Linux 節點上的文件庫。</span><span class="sxs-lookup"><span data-stu-id="7a939-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="7a939-197">hello 以下命令 hello 安裝封裝的副本，並擷取它太/選擇/intel 每個節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="7a939-198">tooinstall Intel MPI 文件庫以無訊息方式，使用 silent.cfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="7a939-199">您可以找到範例在 hello hello 本文結尾處的範例檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="7a939-200">發生在 hello 這個檔案的共用資料夾 /openfoam。</span><span class="sxs-lookup"><span data-stu-id="7a939-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="7a939-201">如需 hello silent.cfg 檔案的詳細資訊，請參閱[Intel MPI Library for Linux 安裝指南-無訊息安裝](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall)。</span><span class="sxs-lookup"><span data-stu-id="7a939-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7a939-202">請確實將您的 silent.cfg 檔案儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="7a939-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="7a939-203">這個步驟可確保正常 hello Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="7a939-204">以無訊息模式安裝 Intel MPI Library。</span><span class="sxs-lookup"><span data-stu-id="7a939-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="7a939-205">設定 MPI</span><span class="sxs-lookup"><span data-stu-id="7a939-205">Configure MPI</span></span>
<span data-ttu-id="7a939-206">進行測試，您應該加入下列行 toohello /etc/security/limits.conf 每個 hello Linux 節點上的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a939-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="7a939-207">在更新 hello limits.conf 檔案之後，請重新啟動 hello Linux 節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="7a939-208">例如，使用 hello 下列**clusrun**命令：</span><span class="sxs-lookup"><span data-stu-id="7a939-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="7a939-209">重新啟動之後，請確定該 hello 共用的資料夾掛接為 /openfoam。</span><span class="sxs-lookup"><span data-stu-id="7a939-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="7a939-210">編譯和安裝 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="7a939-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="7a939-211">儲存 hello OpenFOAM 來源組件 (OpenFOAM-在此範例中的 2.3.1.tgz) tooC:\OpenFoam hello 下載的安裝套件 hello 前端節點上，從 /openfoam hello Linux 節點均可存取此檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="7a939-212">然後執行**clusrun** toocompile OpenFOAM 所有 hello Linux 節點的命令。</span><span class="sxs-lookup"><span data-stu-id="7a939-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="7a939-213">建立資料夾 /opt/OpenFOAM 每個 Linux 節點上，複製 hello 來源封裝 toothis 資料夾，並將它解壓縮那里。</span><span class="sxs-lookup"><span data-stu-id="7a939-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="7a939-214">以 hello Intel MPI Library，先設定環境變數，Intel MPI 和 OpenFOAM toocompile OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a939-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="7a939-215">使用 bash 指令碼呼叫 settings.sh tooset hello 變數。</span><span class="sxs-lookup"><span data-stu-id="7a939-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="7a939-216">您可以找到範例在 hello hello 本文結尾處的範例檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="7a939-217">位置中的這個檔案 （儲存在 Linux 行尾結束符號） hello 共用資料夾 /openfoam。</span><span class="sxs-lookup"><span data-stu-id="7a939-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="7a939-218">這個檔案也包含設定 hello MPI 和 OpenFOAM 執行階段，您會使用更新版本 toorun OpenFOAM 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="7a939-219">安裝所需的相依封裝 toocompile OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a939-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="7a939-220">根據您的 Linux 散發套件，您可能必須 tooadd 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7a939-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="7a939-221">執行**clusrun**命令類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="7a939-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="7a939-222">如有必要，SSH tooeach Linux 節點 toorun hello 命令 tooconfirm 它們能正常執行。</span><span class="sxs-lookup"><span data-stu-id="7a939-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="7a939-223">執行下列命令 toocompile OpenFOAM hello。</span><span class="sxs-lookup"><span data-stu-id="7a939-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="7a939-224">hello 編譯處理程序需要一些時間 toocomplete，和會產生大量的記錄檔資訊 toostandard 輸出，因此使用 hello **/ 交錯**選項交錯 toodisplay hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="7a939-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="7a939-225">hello"\\`"hello 命令中的符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="7a939-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7a939-226">「\\`（& s) 」 表示 hello"&"是 hello 命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="7a939-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="7a939-227">準備 toorun OpenFOAM 工作</span><span class="sxs-lookup"><span data-stu-id="7a939-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="7a939-228">現在取得準備 toorun MPI 工作呼叫 sloshingTank3D，也就是其中一個 hello OpenFoam 範例，兩個 Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="7a939-229">設定 hello 執行階段環境</span><span class="sxs-lookup"><span data-stu-id="7a939-229">Set up hello runtime environment</span></span>
<span data-ttu-id="7a939-230">tooset MPI 和 OpenFOAM hello Linux 節點上，執行下列 Windows PowerShell 視窗中的命令 hello 前端節點上的 hello 的 hello 執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="7a939-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="7a939-231">(此命令僅適用於 SUSE Linux。)</span><span class="sxs-lookup"><span data-stu-id="7a939-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="7a939-232">準備範例資料</span><span class="sxs-lookup"><span data-stu-id="7a939-232">Prepare sample data</span></span>
<span data-ttu-id="7a939-233">使用 hello 前端節點共用您先前設定 tooshare hello Linux 節點 （裝載為 /openfoam） 之間的檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="7a939-234">您的 Linux 的 SSH tooone 計算節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="7a939-235">如果您尚未這樣，請執行下列命令 tooset hello OpenFOAM 執行階段環境，hello。</span><span class="sxs-lookup"><span data-stu-id="7a939-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="7a939-236">複製 hello sloshingTank3D 範例 toohello 共用的資料夾，並瀏覽 tooit。</span><span class="sxs-lookup"><span data-stu-id="7a939-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="7a939-237">當您使用此範例的 hello 預設參數時，可能需要數十個分鐘 toorun，因此您可能想 toomodify 執行速度某些參數 toomake。</span><span class="sxs-lookup"><span data-stu-id="7a939-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="7a939-238">一個簡單的選擇是 toomodify hello 時間步驟變數 deltaT 和 writeInterval hello 系統/controlDict 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7a939-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="7a939-239">這個檔案會儲存所有相關的時間和讀取及寫入方案資料 toohello 控制項的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="7a939-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="7a939-240">例如，您可以變更從 0.05 too0.5 deltaT hello 值和從 0.05 too0.5 writeInterval hello 值。</span><span class="sxs-lookup"><span data-stu-id="7a939-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![修改步階變數][step_variables]
5. <span data-ttu-id="7a939-242">您可以指定想要的值為 hello 變數 hello 系統/decomposeParDict 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7a939-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="7a939-243">這個範例會使用兩個 Linux 節點每 8 個核心，因此設定 numberOfSubdomains too16 and n 的 hierarchicalCoeffs too(1 1 16)，表示與 16 的處理序平行執行 OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a939-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="7a939-244">如需詳細資訊，請參閱 [OpenFOAM User Guide: 3.4 Running applications in parallel (OpenFOAM 使用者指南：3.4 平行執行應用程式)](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)。</span><span class="sxs-lookup"><span data-stu-id="7a939-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![分解程序][decompose]
6. <span data-ttu-id="7a939-246">執行 hello hello sloshingTank3D 目錄 tooprepare hello 範例資料中的下列命令。</span><span class="sxs-lookup"><span data-stu-id="7a939-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="7a939-247">Hello 前端節點上，您應該會看到 hello 範例資料檔案複製到 C:\OpenFoam\sloshingTank3D。</span><span class="sxs-lookup"><span data-stu-id="7a939-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="7a939-248">（C:\OpenFoam 是 hello hello 前端節點上的共用的資料夾）。</span><span class="sxs-lookup"><span data-stu-id="7a939-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Hello 前端節點上的資料檔案][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="7a939-250">mpirun 的主機檔案</span><span class="sxs-lookup"><span data-stu-id="7a939-250">Host file for mpirun</span></span>
<span data-ttu-id="7a939-251">在此步驟中，您建立的主機檔案 （的運算節點的清單） 的 hello **mpirun**命令使用。</span><span class="sxs-lookup"><span data-stu-id="7a939-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="7a939-252">其中一個 hello Linux 節點上建立名為 hostfile 下 /openfoam，因此這個檔案無法到達 /openfoam/hostfile 所有 Linux 節點上的檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="7a939-253">將您的 Linux 節點名稱寫入此檔案中。</span><span class="sxs-lookup"><span data-stu-id="7a939-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="7a939-254">在此範例中，hello 檔案會包含下列名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a939-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="7a939-255">您也可以建立此檔案在 C:\OpenFoam\hostfile hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="7a939-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="7a939-256">如果您選擇這個選項，請將其儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="7a939-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="7a939-257">這可確保正常 hello Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="7a939-258">**Bash 指令碼包裝函式**</span><span class="sxs-lookup"><span data-stu-id="7a939-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="7a939-259">如果您有許多 Linux 節點，而且您想要您的工作 toorun 僅部分，它不是固定的主機檔案，最好先 toouse 因為您不知道哪些節點配置 tooyour 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="7a939-260">在此情況下，撰寫 bash 指令碼包裝函式**mpirun** toocreate 自動 hello 主機檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="7a939-261">您可以尋找範例 bash 指令碼包裝函式呼叫端的此篇文章 hello hpcimpirun.sh，並將它儲存為 /openfoam/hpcimpirun.sh。此範例指令碼未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7a939-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="7a939-262">設定環境變數 hello **mpirun**，與某些加法命令參數 toorun hello MPI 工作透過 hello RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="7a939-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="7a939-263">在此情況下，它會設定 hello 下列變數：</span><span class="sxs-lookup"><span data-stu-id="7a939-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="7a939-264">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="7a939-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="7a939-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="7a939-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="7a939-266">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="7a939-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="7a939-267">建立主機檔案，根據 toohello 環境變數 $CCP_NODES_CORES，由 hello HPC 前端節點 hello 作業啟動時設定。</span><span class="sxs-lookup"><span data-stu-id="7a939-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="7a939-268">$CCP_NODES_CORES hello 格式會遵循下列模式：</span><span class="sxs-lookup"><span data-stu-id="7a939-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="7a939-269">其中</span><span class="sxs-lookup"><span data-stu-id="7a939-269">where</span></span>
      
      * <span data-ttu-id="7a939-270">`<Number of nodes>`-節點的 hello 數目配置 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="7a939-271">`<Name of node_n_...>`-每個節點的 hello 名稱配置 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="7a939-272">`<Cores of node_n_...>`-hello hello 節點配置的 toothis 工作上的核心數目。</span><span class="sxs-lookup"><span data-stu-id="7a939-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="7a939-273">例如，如果 hello 工作需要兩個節點 toorun，$CCP_NODES_CORES 就類似</span><span class="sxs-lookup"><span data-stu-id="7a939-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="7a939-274">呼叫 hello **mpirun**命令，並將附加兩個參數 toohello 命令列。</span><span class="sxs-lookup"><span data-stu-id="7a939-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="7a939-275">`--hostfile <hostfilepath>: <hostfilepath>`-建立 hello hello 主機檔案 hello 指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="7a939-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="7a939-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-hello HPC Pack 前端節點，其中儲存 hello 總核心的數目來設定環境變數配置 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="7a939-277">在此情況下，它會指定處理序數目 hello **mpirun**。</span><span class="sxs-lookup"><span data-stu-id="7a939-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="7a939-278">提交 OpenFOAM 工作</span><span class="sxs-lookup"><span data-stu-id="7a939-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="7a939-279">現在，您可以在 HPC 叢集管理員中提交工作。</span><span class="sxs-lookup"><span data-stu-id="7a939-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="7a939-280">您需要 toopass hello 指令碼 hpcimpirun.sh hello 命令列中的某些 hello 作業 」 工作。</span><span class="sxs-lookup"><span data-stu-id="7a939-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="7a939-281">連接 tooyour 叢集前端節點，並啟動 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="7a939-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="7a939-282">**在 資源管理**，確保 hello Linux 計算節點處於 hello**線上**狀態。</span><span class="sxs-lookup"><span data-stu-id="7a939-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="7a939-283">如果不是，請選取這些節點，然後按一下 [ **上線**]。</span><span class="sxs-lookup"><span data-stu-id="7a939-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="7a939-284">在 [工作管理] 中，按一下 [新增工作]。</span><span class="sxs-lookup"><span data-stu-id="7a939-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="7a939-285">輸入作業的名稱，例如 *sloshingTank3D*。</span><span class="sxs-lookup"><span data-stu-id="7a939-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![工作詳細資料][job_details]
5. <span data-ttu-id="7a939-287">在**作業資源**、 選擇 hello 「 節點 」 資源類型，以及設定 hello 最小值 too2。</span><span class="sxs-lookup"><span data-stu-id="7a939-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="7a939-288">此設定執行 hello 工作，每一個都有 8 個核心，在此範例中的兩個 Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a939-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![工作資源][job_resources]
6. <span data-ttu-id="7a939-290">按一下**編輯工作**在 hello 左側的瀏覽，然後按一下**新增**tooadd 工作 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="7a939-291">加入四個工作 toohello 作業以 hello 下列命令列和設定。</span><span class="sxs-lookup"><span data-stu-id="7a939-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7a939-292">執行`source /openfoam/settings.sh`hello OpenFOAM 和 MPI 執行階段環境，讓每個下列工作的 hello hello OpenFOAM 命令之前呼叫，它會設定。</span><span class="sxs-lookup"><span data-stu-id="7a939-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="7a939-293">**工作 1**。</span><span class="sxs-lookup"><span data-stu-id="7a939-293">**Task 1**.</span></span> <span data-ttu-id="7a939-294">執行**decomposePar** toogenerate 資料檔案執行**interDyMFoam**以平行方式。</span><span class="sxs-lookup"><span data-stu-id="7a939-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="7a939-295">指定一個節點 toohello 工作</span><span class="sxs-lookup"><span data-stu-id="7a939-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="7a939-296">**命令列** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a939-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a939-297">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a939-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="7a939-298">請參閱下列圖 hello。</span><span class="sxs-lookup"><span data-stu-id="7a939-298">See hello following figure.</span></span> <span data-ttu-id="7a939-299">同樣地，您設定 hello 其餘的工作。</span><span class="sxs-lookup"><span data-stu-id="7a939-299">You configure hello remaining tasks similarly.</span></span>
     
     ![作業 1 詳細資料][task_details1]
   * <span data-ttu-id="7a939-301">**工作 2**。</span><span class="sxs-lookup"><span data-stu-id="7a939-301">**Task 2**.</span></span> <span data-ttu-id="7a939-302">執行**interDyMFoam**平行 toocompute hello 範例中。</span><span class="sxs-lookup"><span data-stu-id="7a939-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="7a939-303">指定兩個節點 toohello 工作</span><span class="sxs-lookup"><span data-stu-id="7a939-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="7a939-304">**命令列** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a939-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a939-305">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a939-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="7a939-306">**工作 3**。</span><span class="sxs-lookup"><span data-stu-id="7a939-306">**Task 3**.</span></span> <span data-ttu-id="7a939-307">執行**reconstructPar** toomerge hello 設定的時間目錄從每個 processor_N_ 目錄成單一集合。</span><span class="sxs-lookup"><span data-stu-id="7a939-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="7a939-308">指定一個節點 toohello 工作</span><span class="sxs-lookup"><span data-stu-id="7a939-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="7a939-309">**命令列** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a939-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a939-310">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a939-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="7a939-311">**工作  4**。</span><span class="sxs-lookup"><span data-stu-id="7a939-311">**Task 4**.</span></span> <span data-ttu-id="7a939-312">執行**foamToEnsight**中平行 tooconvert EnSight hello OpenFOAM 結果檔案格式和 hello 案例目錄中名為 Ensight 中放置 hello EnSight 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a939-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="7a939-313">指定兩個節點 toohello 工作</span><span class="sxs-lookup"><span data-stu-id="7a939-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="7a939-314">**命令列** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a939-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a939-315">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a939-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="7a939-316">以遞增的工作順序中新增相依性 toothese 工作。</span><span class="sxs-lookup"><span data-stu-id="7a939-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![作業相依性][task_dependencies]
8. <span data-ttu-id="7a939-318">按一下**送出**toorun 這項作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="7a939-319">根據預設，HPC Pack 送出 hello 與您目前的登入的使用者帳戶的作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="7a939-320">按一下 之後**送出**，您可能會看到對話方塊，提示您 tooenter hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7a939-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![工作認證][creds]
   
   <span data-ttu-id="7a939-322">在某些情況下 HPC Pack 會記住您之前輸入，而不會顯示此對話方塊中的 hello 使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="7a939-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="7a939-323">toomake HPC Pack 會使它再次顯示中，輸入下列命令，在命令提示字元中的 hello，再提交 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="7a939-324">hello 作業會從數十個分鐘 tooseveral 小時，根據您為 hello 範例 toohello 參數。</span><span class="sxs-lookup"><span data-stu-id="7a939-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="7a939-325">在 hello 熱度圖，您會看到 hello hello Linux 節點上執行的作業。</span><span class="sxs-lookup"><span data-stu-id="7a939-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![熱圖][heat_map]
   
   <span data-ttu-id="7a939-327">在每個節點上會啟動 8 個處理程序。</span><span class="sxs-lookup"><span data-stu-id="7a939-327">On each node, eight processes are started.</span></span>
   
   ![Linux 程序][linux_processes]
10. <span data-ttu-id="7a939-329">Hello 作業完成時，請 C:\OpenFoam\sloshingTank3D，與在 C:\OpenFoam hello 記錄檔 下的資料夾中找到 hello 工作結果。</span><span class="sxs-lookup"><span data-stu-id="7a939-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="7a939-330">在 EnSight 中檢視結果</span><span class="sxs-lookup"><span data-stu-id="7a939-330">View results in EnSight</span></span>
<span data-ttu-id="7a939-331">選擇性地使用[EnSight](https://www.ceisoftware.com/) toovisualize 及分析 hello 的 hello OpenFOAM 作業的結果。</span><span class="sxs-lookup"><span data-stu-id="7a939-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="7a939-332">如需 EnSight 中的視覺效果和動畫的詳細資訊，請參閱此 [視訊指南](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html)。</span><span class="sxs-lookup"><span data-stu-id="7a939-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="7a939-333">Hello 前端節點上安裝 EnSight 之後，請啟動它。</span><span class="sxs-lookup"><span data-stu-id="7a939-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="7a939-334">開啟 C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case。</span><span class="sxs-lookup"><span data-stu-id="7a939-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="7a939-335">您會看到槽 hello 檢視器中。</span><span class="sxs-lookup"><span data-stu-id="7a939-335">You see a tank in hello viewer.</span></span>
   
   ![EnSight 中的儲存槽][tank]
3. <span data-ttu-id="7a939-337">建立**Isosurface**從**internalMesh**，然後選擇 hello 變數**alpha_water**。</span><span class="sxs-lookup"><span data-stu-id="7a939-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![建立 isosurface][isosurface]
4. <span data-ttu-id="7a939-339">設定 hello 色彩**Isosurface_part** hello 先前步驟中建立。</span><span class="sxs-lookup"><span data-stu-id="7a939-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="7a939-340">例如，將它設定 toowater 藍色。</span><span class="sxs-lookup"><span data-stu-id="7a939-340">For example, set it toowater blue.</span></span>
   
   ![編輯 isosurface 色彩][isosurface_color]
5. <span data-ttu-id="7a939-342">建立**Iso 磁碟區**從**牆**選取**牆**在 hello**部分**] 面板，按一下 [hello **Isosurfaces** hello 工具列中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7a939-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="7a939-343">在 hello 對話方塊中，選取 **類型**為**Isovolume**並設定 hello 的最小值**Isovolume 範圍**too0.5。</span><span class="sxs-lookup"><span data-stu-id="7a939-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="7a939-344">toocreate hello isovolume 中，按一下**建立與所選部分**。</span><span class="sxs-lookup"><span data-stu-id="7a939-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="7a939-345">設定 hello 色彩**Iso_volume_part** hello 先前步驟中建立。</span><span class="sxs-lookup"><span data-stu-id="7a939-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="7a939-346">例如，將它設定 toodeep 上限藍色。</span><span class="sxs-lookup"><span data-stu-id="7a939-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="7a939-347">設定 hello 色彩**牆**。</span><span class="sxs-lookup"><span data-stu-id="7a939-347">Set hello color for **walls**.</span></span> <span data-ttu-id="7a939-348">例如，將它設定 tootransparent 白色。</span><span class="sxs-lookup"><span data-stu-id="7a939-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="7a939-349">現在按一下**播放**toosee hello 結果 hello 模擬。</span><span class="sxs-lookup"><span data-stu-id="7a939-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![儲存槽結果][tank_result]

## <a name="sample-files"></a><span data-ttu-id="7a939-351">範例檔案</span><span class="sxs-lookup"><span data-stu-id="7a939-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="7a939-352">PowerShell 指令碼叢集部署的 XML 組態檔範例</span><span class="sxs-lookup"><span data-stu-id="7a939-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="7a939-353">範例 cred.xml 檔案</span><span class="sxs-lookup"><span data-stu-id="7a939-353">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="7a939-354">範例 silent.cfg 檔案 tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="7a939-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="7a939-355">範例 settings.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="7a939-355">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="7a939-356">範例 hpcimpirun.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="7a939-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
