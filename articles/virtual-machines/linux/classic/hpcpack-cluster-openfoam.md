---
title: "使用 HPC Pack 在 Linux VM 上執行 OpenFOAM | Microsoft Docs"
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
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="7a7fd-103">在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFoam</span><span class="sxs-lookup"><span data-stu-id="7a7fd-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="7a7fd-104">本文說明一個在 Azure 虛擬機器中執行 OpenFoam 的方式。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="7a7fd-105">在這裡，您將在 Azure 上部署一個具有 Linux 計算節點的 Microsoft HPC Pack 叢集，並使用 Intel MPI 來執行 [OpenFoam](http://openfoam.com/) 作業。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="7a7fd-106">您可以使用支援 RDMA 的 Azure VM 作為計算節點，讓計算節點能夠透過 Azure RDMA 網路進行通訊。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="7a7fd-107">其他在 Azure 中執行 OpenFoam 的選項還包括 Marketplace 中所提供已完整設定的市售映像 (例如 UberCloud 的 [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/))，以及藉由在 [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) 上執行。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7a7fd-108">OpenFOAM (代表 Open Field Operation and Manipulation) 是一個開放原始碼計算流體力學 (CFD) 軟體套件，廣泛運用在商業和學術組織的工程及科學領域中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="7a7fd-109">其中包含網格處理工具，特別是 snappyHexMesh，這是一種用於複雜 CAD 幾何的前置和後置處理的平行化網格處理器。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="7a7fd-110">幾乎所有的程序皆以平行方式執行，讓使用者能夠依其需求充分利用電腦硬體。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="7a7fd-111">Microsoft HPC Pack 提供可在 Microsoft Azure 虛擬機器叢集上執行大規模 HPC 和平行應用程式 (包括的 MPI 應用程式) 的功能。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="7a7fd-112">HPC Pack 也支援在 HPC Pack 叢集中部署的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="7a7fd-113">如需搭配 HPC Pack 使用 Linux 計算節點的簡介，請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="7a7fd-114">本文說明如何使用 HPC Pack 來執行 Linux MPI 工作負載。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="7a7fd-115">本文假設您對 Linux 系統管理及在 Linux 叢集上執行 MPI 工作負載，有某種程度的熟悉。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="7a7fd-116">如果您使用的 MPI 和 OpenFOAM 版本與本文中所顯示的版本不同，您可能必須修改一些安裝和組態步驟。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7a7fd-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a7fd-117">Prerequisites</span></span>
* <span data-ttu-id="7a7fd-118">**具有支援 RDMA 之 Linux 計算節點的 HPC Pack 叢集** - 使用 [Azure Resource Manager 範本](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)或 [Azure PowerShell 指令碼](hpcpack-cluster-powershell-script.md)，部署具有 A8、A9、H16r 或 H16rm 大小之 Linux 計算節點的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="7a7fd-119">如需了解任一選項的必要條件與步驟，請參閱 [開始使用 Azure 中 HPC Pack 叢集內的 Linux 計算節點](hpcpack-cluster.md) 。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="7a7fd-120">如果您選擇 PowerShell 指令碼部署選項，請參閱本文結尾範例檔案中的範例組態檔。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="7a7fd-121">您可以使用此組態來部署 Azure 型 HPC Pack 叢集，其中包含一個 A8 大小的 Windows Server 2012 R2 前端節點，以及兩個 A8 大小的 SUSE Linux Enterprise Server 12 計算節點。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="7a7fd-122">請將您的訂用帳戶和服務名稱取代為適當的值。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="7a7fd-123">**其他應該知道的事項**</span><span class="sxs-lookup"><span data-stu-id="7a7fd-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="7a7fd-124">如需 Azure 的 Linux RDMA 網路必要條件，請參閱[高效能運算 VM 大小](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="7a7fd-125">如果使用 PowerShell 指令碼部署選項，請將所有 Linux 計算節點部署在一個雲端服務內，以使用 RDMA 網路連線。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="7a7fd-126">部署 Linux 節點之後，請透過 SSH 進行連線來執行任何額外的系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="7a7fd-127">您可以在 Azure 入口網站中找到每個 Linux VM 的 SSH 連線詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="7a7fd-128">**Intel MPI** - 若要在 Azure 中的 SLES 12 HPC 計算節點上執行 OpenFOAM，您必須從 [Intel.com 網站](https://software.intel.com/en-us/intel-mpi-library/)安裝 Intel MPI Library 5 執行階段。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="7a7fd-129">(Intel MPI 5 已預先安裝在 CentOS 型 HPC 映像上)。在稍後的步驟中，請視需要在 Linux 計算節點上安裝 Intel MPI。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="7a7fd-130">若要為此步驟做準備，請在向 Intel 註冊之後，依循確認電子郵件中的連結前往相關的網頁。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="7a7fd-131">然後，複製適當 Intel MPI 版本之 .tgz 檔案的下載連結。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="7a7fd-132">這篇文章根據 Intel MPI 5.0.3.048 版。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="7a7fd-133">**OpenFOAM Source Pack** - 從 [OpenFOAM Foundation 網站](http://openfoam.org/download/2-3-1-source/)下載適用於 Linux 的OpenFOAM Source Pack 軟體。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="7a7fd-134">本文是依據 Source Pack 2.3.1 版 (可透過 OpenFOAM-2.3.1.tgz 的形式下載) 而撰寫的。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="7a7fd-135">請依照本文稍後的指示，在 Linux 計算節點上解壓縮並編譯 OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="7a7fd-136">**EnSight** (選擇性) - 若要查看 OpenFOAM 模擬的結果，請下載並安裝 [EnSight](https://www.ceisoftware.com/download/) 視覺效果與分析程式。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="7a7fd-137">授權和下載資訊請見 EnSight 網站。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="7a7fd-138">設定運算節點之間的相互信任</span><span class="sxs-lookup"><span data-stu-id="7a7fd-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="7a7fd-139">在多個 Linux 節點上執行跨節點作業，需要節點相互信任 (藉由 **rsh** 或 **ssh**)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="7a7fd-140">當您使用 Microsoft HPC Pack IaaS 部署指令碼建立 HPC Pack 叢集時，指令碼會自動為您指定的系統管理員帳戶設定永久相互信任。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="7a7fd-141">針對您在叢集的網域中建立的非系統管理員使用者，您必須在將工作配置給他們時，設定節點間的暫時相互信任，並且在工作完成之後終結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="7a7fd-142">若要為每位使用者建立信任，請將 HPC Pack 用於信任關係的 RSA 金鑰組提供給叢集。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="7a7fd-143">產生 RSA 金鑰組</span><span class="sxs-lookup"><span data-stu-id="7a7fd-143">Generate an RSA key pair</span></span>
<span data-ttu-id="7a7fd-144">產生 RSA 金鑰組很容易，其中包含公開金鑰和私密金鑰，方法是執行 Linux **ssh-keygen** 命令。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="7a7fd-145">登入 Linux 電腦。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="7a7fd-146">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="7a7fd-147">按 **Enter** 以使用預設設定，直到完成命令。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="7a7fd-148">請勿在這裡輸入複雜密碼；當系統提示您輸入密碼時，只要按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![產生 RSA 金鑰組][keygen]
3. <span data-ttu-id="7a7fd-150">將目錄變更為 ~/.ssh 目錄。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="7a7fd-151">私密金鑰會儲存在 id_rsa，而公開金鑰會儲存在 id_rsa.pub。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![私密和公開金鑰][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="7a7fd-153">將金鑰組新增至 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="7a7fd-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="7a7fd-154">使用您的 HPC Pack 系統管理員帳戶與您的前端節點進行遠端桌面連線 (當您執行部署指令碼時設定的系統管理員帳戶)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="7a7fd-155">您可以使用標準的 Windows Server 程序在叢集的 Active Directory 網域中建立網域使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="7a7fd-156">例如，在前端節點上使用 Active Directory 使用者和電腦工具。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="7a7fd-157">本文中的範例假設您建立名為 hpclab\hpcuser 的網域使用者。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="7a7fd-158">建立名為 C:\cred.xml 的檔案，並且將 RSA 金鑰資料複製到其中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="7a7fd-159">本文結尾有提供一個範例 cred.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="7a7fd-160">開啟命令提示字元並輸入下列命令，以設定 hpclab\hpcuser 帳戶的認證資料。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="7a7fd-161">您使用 **extendeddata** 參數來傳遞您針對金鑰資料建立之 C:\cred.xml 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="7a7fd-162">這個命令會成功完成而沒有輸出。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-162">This command completes successfully without output.</span></span> <span data-ttu-id="7a7fd-163">為您執行工作所需的使用者帳戶設定認證之後，將 cred.xml 檔案儲存在安全的位置，或將它刪除。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="7a7fd-164">如果您在其中一個 Linux 節點上產生 RSA 金鑰組，請記得在您完成使用後刪除金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="7a7fd-165">如果 HPC Pack 找到現有的 id_rsa 檔案或 id_rsa.pub 檔案，它就不會設定相互信任。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a7fd-166">我們不建議以共用叢集上的叢集系統管理員身分執行 Linux 工作，因為系統管理員提交的工作會在 Linux 節點上的根帳戶底下執行。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="7a7fd-167">不過，非系統管理員使用者所提交的作業會在具有與作業使用者相同名稱的本機 Linux 使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="7a7fd-168">在此情況下，HPC Pack 會在配置給該作業的所有節點上，為此 Linux 使用者設定相互信任。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="7a7fd-169">您可以在執行工作之前，手動在 Linux 節點上設定 Linux 使用者，否則 HPC Pack 會在工作提交時自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="7a7fd-170">如果 HPC Pack 建立使用者，HPC Pack 會在工作完成之後刪除它。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="7a7fd-171">為了降低安全性威脅，HPC Pack 會在作業完成之後移除金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="7a7fd-172">為 Linux 節點設定檔案共用</span><span class="sxs-lookup"><span data-stu-id="7a7fd-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="7a7fd-173">現在，請在前端節點的資料夾上設定一個標準 SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="7a7fd-174">若要允許 Linux 節點存取具有共用路徑的應用程式檔案，請將共用資料夾掛接在 Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="7a7fd-175">如果您想，您可以使用其他檔案共用選項 (例如 Azure 檔案共用，在許多案例中皆建議使用此選項) 或 NFS 共用。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="7a7fd-176">請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](hpcpack-cluster.md)中的檔案共用資訊和詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="7a7fd-177">在前端節點上建立資料夾，並藉由設定讀取/寫入權限與每個人共用。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="7a7fd-178">例如，在前端節點上將 C:\OpenFOAM 共用為 \\\\SUSE12RDMA-HN\OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="7a7fd-179">在這裡， *SUSE12RDMA-HN* 是前端節點的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="7a7fd-180">開啟 Windows PowerShell 視窗並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="7a7fd-181">第一個命令會在 LinuxNodes 群組中的所有節點上建立名為 /openfoam 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="7a7fd-182">第二個命令會將共用資料夾 //SUSE12RDMA-HN/OpenFOAM 掛接在 Linux 節點上，且 dir_mode 和 file_mode 位元會設為 777。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="7a7fd-183">命令中的 *username* 和 *password* 應為前端節點上使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="7a7fd-184">第二個命令中的 “\\`” 符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7a7fd-185">“\\`,” 表示 “,” (逗號) 是命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="7a7fd-186">安裝 MPI 和 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="7a7fd-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="7a7fd-187">若要在 RDMA 網路上以 MPI 工作的形式執行 OpenFOAM，您必須使用 Intel MPI Library 編譯 OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="7a7fd-188">首先，執行數個 **clusrun** 命令，以在您的 Linux 節點上安裝 Intel MPI 程式庫 (如果尚未安裝) 和 OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="7a7fd-189">請使用先前設定的前端節點共用，在 Linux 節點之間共用安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a7fd-190">這些安裝和編譯步驟是範例。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="7a7fd-191">您必須具備一些 Linux 系統管理知識，以確保正確安裝相依的編譯器和程式庫。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="7a7fd-192">您可能需要修改一些特定的環境變數，或 Intel MPI 與 OpenFOAM 版本的其他設定。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="7a7fd-193">如需詳細資料，請參閱適用於您環境的 [Intel MPI Library for Linux 安裝指南](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html)和 [OpenFOAM Source Pack 安裝](http://openfoam.org/download/2-3-1-source/)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="7a7fd-194">安裝 Intel MPI</span><span class="sxs-lookup"><span data-stu-id="7a7fd-194">Install Intel MPI</span></span>
<span data-ttu-id="7a7fd-195">將下載的 Intel MPI 安裝套件 (在此範例中為 l_mpi_p_5.0.3.048.tgz) 儲存在前端節點的 C:\OpenFoam 中，使 Linux 節點能夠從 /openfoam 存取此檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="7a7fd-196">然後，執行 **clusrun** ，以在所有 Linux 節點上安裝 Intel MPI Library。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="7a7fd-197">下列命令會複製安裝套件，並將其解壓縮到每個節點的 /opt/intel 上。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="7a7fd-198">若要以無訊息方式安裝 Intel MPI Library，請使用 silent.cfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="7a7fd-199">您可以在本文結尾處的範例檔案中找到範例。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="7a7fd-200">將此檔案放在共用資料夾 /openfoam 中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="7a7fd-201">如需 silent.cfg 檔案的詳細資訊，請參閱 [Intel MPI Library for Linux 安裝指南 - 無訊息安裝](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7a7fd-202">請確實將您的 silent.cfg 檔案儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="7a7fd-203">此步驟可確保它在 Linux 節點上正常執行。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="7a7fd-204">以無訊息模式安裝 Intel MPI Library。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="7a7fd-205">設定 MPI</span><span class="sxs-lookup"><span data-stu-id="7a7fd-205">Configure MPI</span></span>
<span data-ttu-id="7a7fd-206">若要進行測試，您應在每個 Linux 節點的 /etc/security/limits.conf 中加入以下幾行：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="7a7fd-207">更新 limits.conf 檔案之後，請重新啟動 Linux 節點。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="7a7fd-208">例如，使用下列 **clusrun** 命令：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="7a7fd-209">重新啟動之後，請確定共用資料夾已掛接為 /openfoam。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="7a7fd-210">編譯和安裝 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="7a7fd-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="7a7fd-211">將下載的 OpenFOAM Source Pack 安裝套件 (在此範例中為 OpenFOAM-2.3.1.tgz) 儲存至前端節點的 C:\OpenFoam，使 Linux 節點能夠從 /openfoam 存取此檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="7a7fd-212">然後，執行 **clusrun** 命令，以在所有 Linux 節點上編譯 OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="7a7fd-213">在每個 Linux 節點上建立資料夾 /opt/OpenFOAM、將來源封裝複製到此資料夾，並在該處加以解壓縮。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="7a7fd-214">若要使用 Intel MPI Library 編譯 OpenFOAM，請先設定 Intel MPI 和 OpenFOAM 的某些環境變數。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="7a7fd-215">請使用名為 settings.sh 的 Bash 指令碼來設定變數。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="7a7fd-216">您可以在本文結尾處的範例檔案中找到範例。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="7a7fd-217">將此檔案 (使用 Linux 行尾結束符號儲存的) 放在共用資料夾 /openfoam 中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="7a7fd-218">此檔案也包含您後續用來執行 OpenFOAM 工作的 MPI 和 OpenFOAM 執行階段的設定。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="7a7fd-219">安裝編譯 OpenFOAM 所需的相依封裝。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="7a7fd-220">根據您的 Linux 散發套件，您可能需要先新增儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="7a7fd-221">執行類似下列的 **clusrun** 命令：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="7a7fd-222">如有需要，可透過 SSH 連線到每個 Linux 節點來執行命令，以確認它們是否正常執行。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="7a7fd-223">執行下列命令以編譯 OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="7a7fd-224">編譯程序需要一些時間才能完成，並且會在標準輸出中產生大量的記錄資訊，因此，請使用 **/interleaved** 選項以便以交錯方式顯示輸出。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="7a7fd-225">命令中的 “\\`” 符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7a7fd-226">“\\`&” 表示 “&” 是命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="7a7fd-227">準備執行 OpenFOAM 工作</span><span class="sxs-lookup"><span data-stu-id="7a7fd-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="7a7fd-228">現在，請準備在兩個 Linux 節點上執行名為 sloshingTank3D 的 MPI 作業，這是其中一個 OpenFoam 範例。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="7a7fd-229">設定執行階段環境</span><span class="sxs-lookup"><span data-stu-id="7a7fd-229">Set up the runtime environment</span></span>
<span data-ttu-id="7a7fd-230">若要在 Linux 節點上設定 MPI 和 OpenFOAM 的執行階段環境，請在前端節點上的 Windows PowerShell 視窗中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="7a7fd-231">(此命令僅適用於 SUSE Linux。)</span><span class="sxs-lookup"><span data-stu-id="7a7fd-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="7a7fd-232">準備範例資料</span><span class="sxs-lookup"><span data-stu-id="7a7fd-232">Prepare sample data</span></span>
<span data-ttu-id="7a7fd-233">請使用您先前設定的前端節點共用，在 Linux 節點之間共用檔案 (掛接為 /openfoam)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="7a7fd-234">透過 SSH 連接到您其中一個 Linux 計算節點。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="7a7fd-235">執行下列命令以設定 OpenFOAM 執行階段環境 (如果您尚未執行此作業)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="7a7fd-236">將 sloshingTank3D 範例複製到共用資料夾，並瀏覽到該資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="7a7fd-237">如果您使用此範例的預設參數，其執行時間可能需要數十分鐘，因此您可能會想要修改某些參數，讓它執行得更快。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="7a7fd-238">一個簡單的選擇是修改 system/controlDict 檔案中的時間步階變數 deltaT 和 writeInterval。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="7a7fd-239">此檔案儲存了所有與控制時間以及讀取和寫入解決方案資料有關的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="7a7fd-240">例如，您可以將 deltaT 的值從 0.05 變更為 0.5，以及將 writeInterval 的值從 0.05 變更為 0.5。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![修改步階變數][step_variables]
5. <span data-ttu-id="7a7fd-242">在 system/decomposeParDict 檔案中指定所要的變數值。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="7a7fd-243">此範例使用兩個分別具有 8 個核心的 Linux 節點，因此，請將 numberOfSubdomains 設為 16，以及將 hierarchicalCoeffs 的 n 設為 (1 1 16)，這表示以 16 個處理程序平行執行 OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="7a7fd-244">如需詳細資訊，請參閱 [OpenFOAM User Guide: 3.4 Running applications in parallel (OpenFOAM 使用者指南：3.4 平行執行應用程式)](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![分解程序][decompose]
6. <span data-ttu-id="7a7fd-246">從 sloshingTank3D 目錄執行下列命令，以準備範例資料。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="7a7fd-247">在前端節點上，您應該會看到範例資料檔案複製到 C:\OpenFoam\sloshingTank3D 中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="7a7fd-248">(C:\OpenFoam 是前端節點上的共用資料夾。)</span><span class="sxs-lookup"><span data-stu-id="7a7fd-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![前端節點上的資料檔案][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="7a7fd-250">mpirun 的主機檔案</span><span class="sxs-lookup"><span data-stu-id="7a7fd-250">Host file for mpirun</span></span>
<span data-ttu-id="7a7fd-251">在此步驟中，您會建立 **mpirun** 命令所使用的主機檔案 (計算節點清單)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="7a7fd-252">在其中一個 Linux 節點上的 /openfoam 下，建立名為 hostfile 的檔案，以便在所有 Linux 節點上的 /openfoam/hostfile 都可存取此檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="7a7fd-253">將您的 Linux 節點名稱寫入此檔案中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="7a7fd-254">在此範例中，檔案會包含下列名稱：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="7a7fd-255">您也可以在前端節點的 C:\OpenFoam\hostfile 上建立此檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="7a7fd-256">如果您選擇這個選項，請將其儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="7a7fd-257">這可確保它在 Linux 節點上正常運作。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="7a7fd-258">**Bash 指令碼包裝函式**</span><span class="sxs-lookup"><span data-stu-id="7a7fd-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="7a7fd-259">如果您有許多 Linux 節點，而您想要讓您的作業只在其中一些節點上執行，則不建議使用固定的主機檔案，因為您不知道系統會將哪些節點配置給您的作業。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="7a7fd-260">在此情況下，請為 **mpirun** 撰寫 Bash 指令碼包裝函式，以自動建立主機檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="7a7fd-261">您可以在本文結尾找到名為 hpcimpirun.sh 的範例 Bash 指令碼包裝函式，並將其儲存為 /openfoam/hpcimpirun.sh。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="7a7fd-262">此範例指令碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="7a7fd-263">設定 **mpirun**的環境變數，和透過 RDMA 網路執行 MPI 工作時所使用的某些附加命令參數。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="7a7fd-264">在此範例中，它會設定下列變數：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="7a7fd-265">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="7a7fd-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="7a7fd-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="7a7fd-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="7a7fd-267">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="7a7fd-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="7a7fd-268">根據環境變數 $CCP_NODES_CORES 建立主機檔案，該變數會在工作啟動時由 HPC 前端節點設定。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="7a7fd-269">$CCP_NODES_CORES 的格式會遵循下列模式：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="7a7fd-270">其中</span><span class="sxs-lookup"><span data-stu-id="7a7fd-270">where</span></span>
      
      * <span data-ttu-id="7a7fd-271">`<Number of nodes>` - 配置給此工作的節點數目。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="7a7fd-272">`<Name of node_n_...>` - 配置給此工作的各節點名稱。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="7a7fd-273">`<Cores of node_n_...>` - 配置給此工作的節點上核心數目。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="7a7fd-274">例如，如果作業需要兩個節點才能執行，則 $CCP_NODES_CORES 會類似於：</span><span class="sxs-lookup"><span data-stu-id="7a7fd-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="7a7fd-275">呼叫 **mpirun** 命令，並將兩個參數附加到命令列。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="7a7fd-276">`--hostfile <hostfilepath>: <hostfilepath>` - 指令碼所建立的主機檔案路徑</span><span class="sxs-lookup"><span data-stu-id="7a7fd-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="7a7fd-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - HPC Pack 前端節點所設定的環境變數，會儲存配置給此工作的總核心數目。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="7a7fd-278">在此案例中，它會指定 **mpirun**的處理程序數目。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="7a7fd-279">提交 OpenFOAM 工作</span><span class="sxs-lookup"><span data-stu-id="7a7fd-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="7a7fd-280">現在，您可以在 HPC 叢集管理員中提交工作。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="7a7fd-281">您必須在命令列中，針對某些作業工作傳遞指令碼 hpcimpirun.sh。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="7a7fd-282">連接至您的叢集前端節點並且啟動 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="7a7fd-283">在 [資源管理] 中，確定 Linux 計算節點處於 [線上] 狀態。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="7a7fd-284">如果不是，請選取這些節點，然後按一下 [ **上線**]。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="7a7fd-285">在 [工作管理] 中，按一下 [新增工作]。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="7a7fd-286">輸入作業的名稱，例如 *sloshingTank3D*。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![工作詳細資料][job_details]
5. <span data-ttu-id="7a7fd-288">在 [ **工作資源**] 中，選取 [節點] 做為資源類型，並將 [最小值] 設為 2。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="7a7fd-289">在此範例中，此組態會在兩個分別具有 8 個核心的 Linux 節點上執行作業。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![工作資源][job_resources]
6. <span data-ttu-id="7a7fd-291">按一下左導覽窗格中的 [編輯工作]，然後按一下 [加入] 來將工作加入到作業中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="7a7fd-292">請使用下列命令列與設定，將四個工作新增到作業中。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7a7fd-293">執行 `source /openfoam/settings.sh` 會設定 OpenFOAM 和 MPI 執行階段環境，因此下列每個作業會在 OpenFOAM 命令之前加以呼叫。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="7a7fd-294">**工作 1**。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-294">**Task 1**.</span></span> <span data-ttu-id="7a7fd-295">執行 **decomposePar**，產生以平行方式執行 **interDyMFoam** 的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="7a7fd-296">將一個節點指派給工作</span><span class="sxs-lookup"><span data-stu-id="7a7fd-296">Assign one node to the task</span></span>
     * <span data-ttu-id="7a7fd-297">**命令列** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a7fd-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a7fd-298">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a7fd-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="7a7fd-299">請參閱下圖。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-299">See the following figure.</span></span> <span data-ttu-id="7a7fd-300">以同樣的方式設定其餘的工作。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-300">You configure the remaining tasks similarly.</span></span>
     
     ![作業 1 詳細資料][task_details1]
   * <span data-ttu-id="7a7fd-302">**工作 2**。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-302">**Task 2**.</span></span> <span data-ttu-id="7a7fd-303">以平行方式執行 **interDyMFoam** ，以計算範例。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="7a7fd-304">將兩個節點指派給工作</span><span class="sxs-lookup"><span data-stu-id="7a7fd-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="7a7fd-305">**命令列** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a7fd-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a7fd-306">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a7fd-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="7a7fd-307">**工作 3**。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-307">**Task 3**.</span></span> <span data-ttu-id="7a7fd-308">執行 **reconstructPar**，以將來自每個 processor_N_ 目錄的數組時間目錄合併成一組目錄。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="7a7fd-309">將一個節點指派給工作</span><span class="sxs-lookup"><span data-stu-id="7a7fd-309">Assign one node to the task</span></span>
     * <span data-ttu-id="7a7fd-310">**命令列** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a7fd-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a7fd-311">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a7fd-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="7a7fd-312">**工作  4**。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-312">**Task 4**.</span></span> <span data-ttu-id="7a7fd-313">以平行方式執行 **foamToEnsight** ，以將 OpenFOAM 結果檔案轉換成 EnSight 格式，並將 EnSight 檔案放在案例目錄中名為 Ensight 的目錄內。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="7a7fd-314">將兩個節點指派給工作</span><span class="sxs-lookup"><span data-stu-id="7a7fd-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="7a7fd-315">**命令列** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="7a7fd-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="7a7fd-316">**工作目錄** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="7a7fd-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="7a7fd-317">以遞增作業順序，將相依性新增至這些作業。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![作業相依性][task_dependencies]
8. <span data-ttu-id="7a7fd-319">按一下 [ **提交** ] 以執行此工作。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="7a7fd-320">根據預設，HPC Pack 會以您目前登入的使用者帳戶提交工作。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="7a7fd-321">按一下 [ **提交**] 之後可能會出現一個對話方塊，提示您輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![工作認證][creds]
   
   <span data-ttu-id="7a7fd-323">在某些情況下，HPC Pack 會記住您以前輸入的使用者資訊，而不會顯示此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="7a7fd-324">若要讓 HPC Pack 再次顯示此對話方塊，請在命令提示字元中輸入下列命令，然後提交作業。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="7a7fd-325">執行工作可能需要數十分鐘到數小時不等，視您為範例設定的參數而定。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="7a7fd-326">在熱度圖中，您會看到作業在 Linux 節點上執行。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![熱度圖][heat_map]
   
   <span data-ttu-id="7a7fd-328">在每個節點上會啟動 8 個處理程序。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-328">On each node, eight processes are started.</span></span>
   
   ![Linux 程序][linux_processes]
10. <span data-ttu-id="7a7fd-330">工作完成時，請 C:\OpenFoam\sloshingTank3D 下的資料夾中找出工作結果，記錄檔則位於 C:\OpenFoam 上。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="7a7fd-331">在 EnSight 中檢視結果</span><span class="sxs-lookup"><span data-stu-id="7a7fd-331">View results in EnSight</span></span>
<span data-ttu-id="7a7fd-332">您可以選擇性地使用 [EnSight](https://www.ceisoftware.com/) 來視覺化和分析 OpenFOAM 工作的結果。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="7a7fd-333">如需 EnSight 中的視覺效果和動畫的詳細資訊，請參閱此 [視訊指南](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html)。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="7a7fd-334">在前端節點上安裝 EnSight 之後，請加以啟動。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="7a7fd-335">開啟 C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="7a7fd-336">您會在檢視器中看見一個儲存槽。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-336">You see a tank in the viewer.</span></span>
   
   ![EnSight 中的儲存槽][tank]
3. <span data-ttu-id="7a7fd-338">從 **internalMesh** 建立 **Isosurface**，然後選擇變數 **alpha_water**。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![建立 isosurface][isosurface]
4. <span data-ttu-id="7a7fd-340">為先前的步驟中建立的 **Isosurface_part** 設定色彩。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="7a7fd-341">例如，將它設為水藍色。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-341">For example, set it to water blue.</span></span>
   
   ![編輯 isosurface 色彩][isosurface_color]
5. <span data-ttu-id="7a7fd-343">在 [組件] 面板中選取 [圖表牆]，以從 [圖表牆] 建立 **Iso-volume**，然後按一下工具列中的 **Isosurfaces** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="7a7fd-344">在對話方塊中，選取 **Isovolume** 做為 [類型]，然後將 [Isovolume 範圍] 的最小值設為 0.5。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="7a7fd-345">若要建立 isovolume，請按一下 [使用選取的組件建立] 。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="7a7fd-346">為先前的步驟中建立的 **Iso_volume_part** 設定色彩。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="7a7fd-347">例如，將它設為深藍色。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="7a7fd-348">設定 [ **圖表牆**] 的色彩。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-348">Set the color for **walls**.</span></span> <span data-ttu-id="7a7fd-349">例如，將它設為透明的白色。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="7a7fd-350">現在，按一下 [ **播放** ] 以檢視模擬的結果。</span><span class="sxs-lookup"><span data-stu-id="7a7fd-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![儲存槽結果][tank_result]

## <a name="sample-files"></a><span data-ttu-id="7a7fd-352">範例檔案</span><span class="sxs-lookup"><span data-stu-id="7a7fd-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="7a7fd-353">PowerShell 指令碼叢集部署的 XML 組態檔範例</span><span class="sxs-lookup"><span data-stu-id="7a7fd-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="7a7fd-354">範例 cred.xml 檔案</span><span class="sxs-lookup"><span data-stu-id="7a7fd-354">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="7a7fd-355">安裝 MPI 的 silent.cfg 檔案範例</span><span class="sxs-lookup"><span data-stu-id="7a7fd-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
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

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="7a7fd-356">範例 settings.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="7a7fd-356">Sample settings.sh script</span></span>
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


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="7a7fd-357">範例 hpcimpirun.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="7a7fd-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
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
