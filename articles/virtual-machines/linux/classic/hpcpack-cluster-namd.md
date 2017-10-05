---
title: "Linux VM 上的 NAMD 與 Microsoft HPC Pack | Microsoft Docs"
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
ms.openlocfilehash: e31845f3d7aa08357b0e8a1b3b77d97302442ac3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="2b935-103">在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD</span><span class="sxs-lookup"><span data-stu-id="2b935-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="2b935-104">本文將說明在 Azure 虛擬機器上執行 Linux 高效能運算 (HPC) 工作負載的方法。</span><span class="sxs-lookup"><span data-stu-id="2b935-104">This article shows you one way to run a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="2b935-105">在這裡，您會在 Azure 上使用多個 Linux 計算節點設定 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) 叢集以及執行 [NAMD](http://www.ks.uiuc.edu/Research/namd/) 模擬，以計算和視覺化大型生物分子系統的結構。</span><span class="sxs-lookup"><span data-stu-id="2b935-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation to calculate and visualize the structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="2b935-106">**NAMD** (適用於奈米分子動力程式) 是專為高效能模擬大型生物分子系統而設計的平行分子動力套件，包含多達數百萬個原子。</span><span class="sxs-lookup"><span data-stu-id="2b935-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up to millions of atoms.</span></span> <span data-ttu-id="2b935-107">這些系統的範例包括病毒、儲存格結構和大型蛋白質。</span><span class="sxs-lookup"><span data-stu-id="2b935-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="2b935-108">NAMD 會針對典型模擬縮放到數百個核心，以及針對最大型的模擬縮放至超過 500,000 個核心。</span><span class="sxs-lookup"><span data-stu-id="2b935-108">NAMD scales to hundreds of cores for typical simulations and to more than 500,000 cores for the largest simulations.</span></span>
* <span data-ttu-id="2b935-109">**Microsoft HPC Pack** 提供在內部部署電腦或 Azure 虛擬機器的叢集中執行大規模 HPC 和平行應用程式 (包括的 MPI 應用程式) 的功能。</span><span class="sxs-lookup"><span data-stu-id="2b935-109">**Microsoft HPC Pack** provides features to run large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="2b935-110">HPC Pack 的開發前身為 Windows HPC 工作負載的解決方案，其現已支援於部署在 HPC Pack 叢集中的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b935-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="2b935-111">如需簡介，請參閱 [在 Azure 的 HPC Pack 叢集中開始使用 Linux 運算節點](hpcpack-cluster.md) 。</span><span class="sxs-lookup"><span data-stu-id="2b935-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="2b935-112">如需在 Azure 上執行 HPC 和批次工作負載的其他選項，請參閱[批次和高效能運算的技術資源](../../../batch/batch-hpc-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="2b935-112">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b935-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="2b935-113">Prerequisites</span></span>
* <span data-ttu-id="2b935-114">**具備 Linux 計算節點的 HPC Pack 叢集** - 使用 [Azure Resource Manager 範本](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)或 [Azure PowerShell 指令碼](hpcpack-cluster-powershell-script.md)，在 Azure 上部署具備 Linux 計算節點的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="2b935-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="2b935-115">如需了解任一選項的必要條件與步驟，請參閱 [開始使用 Azure 中 HPC Pack 叢集內的 Linux 計算節點](hpcpack-cluster.md) 。</span><span class="sxs-lookup"><span data-stu-id="2b935-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="2b935-116">如果您選擇 PowerShell 指令碼部署選項，請參閱本文結尾範例檔案中的範例組態檔。</span><span class="sxs-lookup"><span data-stu-id="2b935-116">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="2b935-117">此檔案會設定 Windows Server 2012 R2 的前端節點和四個大型 CentOS 6.6 計算節點組成之以 Azure 為基礎的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="2b935-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="2b935-118">請視環境需要自訂此檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="2b935-119">**NAMD 軟體與教學課程檔案** - 從 [NAMD](http://www.ks.uiuc.edu/Research/namd/) 網站下載 Linux 的 NAMD 軟體 (需要註冊)。</span><span class="sxs-lookup"><span data-stu-id="2b935-119">**NAMD software and tutorial files** - Download NAMD software for Linux from the [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="2b935-120">本文是以 NAMD 2.10 版為基礎，並使用 [Linux-x86_64 (64 位元 Intel/AMD 乙太網路)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) 封存。</span><span class="sxs-lookup"><span data-stu-id="2b935-120">This article is based on NAMD version 2.10, and uses the [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="2b935-121">另請下載 [NAMD 教學課程檔案](http://www.ks.uiuc.edu/Training/Tutorials/#namd)。</span><span class="sxs-lookup"><span data-stu-id="2b935-121">Also download the [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="2b935-122">下載的是 .tar 檔案，而您需要 Windows 工具以解壓縮叢集前端節點上的檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-122">The downloads are .tar files, and you need a Windows tool to extract the files on the cluster head node.</span></span> <span data-ttu-id="2b935-123">若要解壓縮檔案，請遵循本文稍後的指示。</span><span class="sxs-lookup"><span data-stu-id="2b935-123">To extract the files, follow the instructions later in this article.</span></span> 
* <span data-ttu-id="2b935-124">**VMD** (選擇性) - 若要查看 NAMD 工作的結果，請在您選擇的電腦上，下載和安裝分子視覺化程式 [VMD](http://www.ks.uiuc.edu/Research/vmd/) 。</span><span class="sxs-lookup"><span data-stu-id="2b935-124">**VMD** (optional) - To see the results of your NAMD job, download and install the molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="2b935-125">目前版本為 1.9.2。</span><span class="sxs-lookup"><span data-stu-id="2b935-125">The current version is 1.9.2.</span></span> <span data-ttu-id="2b935-126">請參閱 VMD 下載網站以開始作業。</span><span class="sxs-lookup"><span data-stu-id="2b935-126">See the VMD download site to get started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="2b935-127">設定運算節點之間的相互信任</span><span class="sxs-lookup"><span data-stu-id="2b935-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="2b935-128">在多個 Linux 節點上執行跨節點作業，需要節點相互信任 (藉由 **rsh** 或 **ssh**)。</span><span class="sxs-lookup"><span data-stu-id="2b935-128">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="2b935-129">當您使用 Microsoft HPC Pack IaaS 部署指令碼建立 HPC Pack 叢集時，指令碼會自動為您指定的系統管理員帳戶設定永久相互信任。</span><span class="sxs-lookup"><span data-stu-id="2b935-129">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="2b935-130">針對您在叢集的網域中建立的非系統管理員使用者，您必須在將工作配置給他們時，設定節點間的暫時相互信任。</span><span class="sxs-lookup"><span data-stu-id="2b935-130">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them.</span></span> <span data-ttu-id="2b935-131">然後，在工作完成之後終結關聯性。</span><span class="sxs-lookup"><span data-stu-id="2b935-131">Then, destroy the relationship after the job is complete.</span></span> <span data-ttu-id="2b935-132">若要為每個使用者執行此動作，提供 HPC Pack 用來建立信任關係的 RSA 金鑰組給叢集。</span><span class="sxs-lookup"><span data-stu-id="2b935-132">To do this for each user, provide an RSA key pair to the cluster which HPC Pack uses to establish the trust relationship.</span></span> <span data-ttu-id="2b935-133">指示如下。</span><span class="sxs-lookup"><span data-stu-id="2b935-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="2b935-134">產生 RSA 金鑰組</span><span class="sxs-lookup"><span data-stu-id="2b935-134">Generate an RSA key pair</span></span>
<span data-ttu-id="2b935-135">產生 RSA 金鑰組很容易，其中包含公開金鑰和私密金鑰，方法是執行 Linux **ssh-keygen** 命令。</span><span class="sxs-lookup"><span data-stu-id="2b935-135">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="2b935-136">登入 Linux 電腦。</span><span class="sxs-lookup"><span data-stu-id="2b935-136">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="2b935-137">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="2b935-137">Run the following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="2b935-138">按 **Enter** 以使用預設設定，直到完成命令。</span><span class="sxs-lookup"><span data-stu-id="2b935-138">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="2b935-139">請勿在這裡輸入複雜密碼；當系統提示您輸入密碼時，只要按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="2b935-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![產生 RSA 金鑰組][keygen]
3. <span data-ttu-id="2b935-141">將目錄變更為 ~/.ssh 目錄。</span><span class="sxs-lookup"><span data-stu-id="2b935-141">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="2b935-142">私密金鑰會儲存在 id_rsa，而公開金鑰會儲存在 id_rsa.pub。</span><span class="sxs-lookup"><span data-stu-id="2b935-142">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![私密和公開金鑰][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="2b935-144">將金鑰組新增至 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="2b935-144">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="2b935-145">請使用您部署叢集時所提供的網域認證 (例如，hpc\clusteradmin) [由遠端桌面連線](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)到前端節點 VM。</span><span class="sxs-lookup"><span data-stu-id="2b935-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="2b935-146">您可以從前端節點管理叢集。</span><span class="sxs-lookup"><span data-stu-id="2b935-146">You manage the cluster from the head node.</span></span>
2. <span data-ttu-id="2b935-147">您可以使用標準的 Windows Server 程序在叢集的 Active Directory 網域中建立網域使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b935-147">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="2b935-148">例如，在前端節點上使用 Active Directory 使用者和電腦工具。</span><span class="sxs-lookup"><span data-stu-id="2b935-148">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="2b935-149">本文中的範例假設您在 hpclab 網域中建立名為 hpcuser 的網域使用者 (hpclab\hpcuser)。</span><span class="sxs-lookup"><span data-stu-id="2b935-149">The examples in this article assume you create a domain user named hpcuser in the hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="2b935-150">將網域使用者以叢集使用者身分加入 HPC Pack 叢集中。</span><span class="sxs-lookup"><span data-stu-id="2b935-150">Add the domain user to the HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="2b935-151">如需指示，請參閱 [(Add or Remove Cluster Users) 新增或移除叢集使用者](https://technet.microsoft.com/library/ff919330.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b935-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="2b935-152">建立名為 C:\cred.xml 的檔案，並且將 RSA 金鑰資料複製到其中。</span><span class="sxs-lookup"><span data-stu-id="2b935-152">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="2b935-153">您可以在本文結尾處的範例檔案中找到範例。</span><span class="sxs-lookup"><span data-stu-id="2b935-153">You can find an example in the sample files at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="2b935-154">開啟命令提示字元並輸入下列命令，以設定 hpclab\hpcuser 帳戶的認證資料。</span><span class="sxs-lookup"><span data-stu-id="2b935-154">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="2b935-155">您使用 **extendeddata** 參數來傳遞您針對金鑰資料建立的 C:\cred.xml 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="2b935-155">You use the **extendeddata** parameter to pass the name of the C:\cred.xml file you created for the key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="2b935-156">這個命令會成功完成而沒有輸出。</span><span class="sxs-lookup"><span data-stu-id="2b935-156">This command completes successfully without output.</span></span> <span data-ttu-id="2b935-157">為您執行工作所需的使用者帳戶設定認證之後，將 cred.xml 檔案儲存在安全的位置，或將它刪除。</span><span class="sxs-lookup"><span data-stu-id="2b935-157">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="2b935-158">如果您在其中一個 Linux 節點上產生 RSA 金鑰組，請記得在您完成使用後刪除金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b935-158">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="2b935-159">如果 HPC Pack 找到現有的 id_rsa 檔案或 id_rsa.pub 檔案，則它不會設定相互信任。</span><span class="sxs-lookup"><span data-stu-id="2b935-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b935-160">我們不建議以共用叢集上的叢集系統管理員身分執行 Linux 工作，因為系統管理員提交的工作會在 Linux 節點上的根帳戶底下執行。</span><span class="sxs-lookup"><span data-stu-id="2b935-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="2b935-161">非系統管理員使用者所提交的作業會在具有與作業使用者相同名稱的本機 Linux 使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="2b935-161">A job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="2b935-162">在此情況下，HPC Pack 會在配置給該作業的所有節點上，為此 Linux 使用者設定相互信任。</span><span class="sxs-lookup"><span data-stu-id="2b935-162">In this case, HPC Pack sets up mutual trust for this Linux user across all the nodes allocated to the job.</span></span> <span data-ttu-id="2b935-163">您可以在執行工作之前，手動在 Linux 節點上設定 Linux 使用者，否則 HPC Pack 會在工作提交時自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="2b935-163">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="2b935-164">如果 HPC Pack 建立使用者，HPC Pack 會在工作完成之後刪除它。</span><span class="sxs-lookup"><span data-stu-id="2b935-164">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="2b935-165">若要降低安全性威脅，金鑰會在工作完成之後於節點上移除。</span><span class="sxs-lookup"><span data-stu-id="2b935-165">To reduce security threat, the keys are removed after the job completes on the nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="2b935-166">為 Linux 節點設定檔案共用</span><span class="sxs-lookup"><span data-stu-id="2b935-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="2b935-167">現在請設定 SMB 檔案共用，並在所有 Linux 節點上裝載共用資料夾，允許 Linux 節點存取具有共用路徑的 NAMD 檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-167">Now set up an SMB file share, and mount the shared folder on all Linux nodes to allow the Linux nodes to access NAMD files with a common path.</span></span> <span data-ttu-id="2b935-168">以下是在前端節點上裝載共用資料夾的步驟。</span><span class="sxs-lookup"><span data-stu-id="2b935-168">Following are steps to mount a shared folder on the head node.</span></span> <span data-ttu-id="2b935-169">建議共用分配，例如目前不支援 Azure 檔案服務的 CentOS 6.6。</span><span class="sxs-lookup"><span data-stu-id="2b935-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support the Azure File service.</span></span> <span data-ttu-id="2b935-170">如果您的 Linux 節點支援 Azure 檔案共用，請參閱[如何搭配使用 Azure 檔案儲存體與 Linux](../../../storage/files/storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="2b935-170">If your Linux nodes support an Azure File share, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="2b935-171">如需 HPC Pack 的其他檔案共用選項，請參閱 [開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點](hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="2b935-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="2b935-172">在前端節點上建立資料夾，並藉由設定讀取/寫入權限與每個人共用。</span><span class="sxs-lookup"><span data-stu-id="2b935-172">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="2b935-173">在此範例中，\\\\CentOS66HN\Namd 是資料夾的名稱，其中CentOS66HN 是前端節點的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="2b935-173">In this example, \\\\CentOS66HN\Namd is the name of the folder, where CentOS66HN is the host name of the head node.</span></span>
2. <span data-ttu-id="2b935-174">在共用資料夾中建立名為 namd2 的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="2b935-174">Create a subfolder named namd2 in the shared folder.</span></span> <span data-ttu-id="2b935-175">在 namd2 中，建立另一個名為 namdsample 的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="2b935-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="2b935-176">在資料夾中解壓縮 NAMD 檔案，方法是使用 Windows 的 **tar** 版本，或其他可以操作 .tar 封存的 Windows 公用程式。</span><span class="sxs-lookup"><span data-stu-id="2b935-176">Extract the NAMD files in the folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="2b935-177">將 NAMD tar 封存解壓縮到 \\\\CentOS66HN\Namd\namd2。</span><span class="sxs-lookup"><span data-stu-id="2b935-177">Extract the NAMD tar archive to \\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="2b935-178">解壓縮 \\\\CentOS66HN\Namd\namd2\namdsample 之下的教學課程檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-178">Extract the tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="2b935-179">開啟 Windows PowerShell 視窗並執行下列命令來將共用資料夾裝載在 Linux 節點上。</span><span class="sxs-lookup"><span data-stu-id="2b935-179">Open a Windows PowerShell window and run the following commands to mount the shared folder on the Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="2b935-180">第一個命令會在 LinuxNodes 群組中的所有節點上建立名為 /namd2 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2b935-180">The first command creates a folder named /namd2 on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="2b935-181">第二個命令會將共用資料夾 //CentOS66HN/Namd/namd2 掛接至此資料夾，其 dir_mode 和 file_mode 位元設為 777。</span><span class="sxs-lookup"><span data-stu-id="2b935-181">The second command mounts the shared folder //CentOS66HN/Namd/namd2 onto the folder with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="2b935-182">命令中的 *username* 和 *password* 應為前端節點上使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="2b935-182">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="2b935-183">第二個命令中的 “\\`” 符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="2b935-183">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="2b935-184">“\\`,” 表示 “,” (逗號) 是命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="2b935-184">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="create-a-bash-script-to-run-a-namd-job"></a><span data-ttu-id="2b935-185">建立執行 NAMD 作業的 Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="2b935-185">Create a Bash script to run a NAMD job</span></span>
<span data-ttu-id="2b935-186">您的 NAMD 作業需要 *nodelist* 檔案，如此 **charmrun** 才可決定啟動 NAMD 程序時要使用的節點數目。</span><span class="sxs-lookup"><span data-stu-id="2b935-186">Your NAMD job needs a *nodelist* file for **charmrun** to determine the number of nodes to use when starting NAMD processes.</span></span> <span data-ttu-id="2b935-187">您會使用 Bash 指令碼，產生 nodelist 檔案，並在執行 **charmrun** 搭配此 nodelist 檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-187">You use a Bash script that generates the nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="2b935-188">然後您就可以在會呼叫此指令碼的 HPC 叢集管理員中提交 NAMD 工作。</span><span class="sxs-lookup"><span data-stu-id="2b935-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="2b935-189">使用您選擇的文字編輯器，在包含 NAMD 程式檔案的 /namd2 資料夾中建立 Bash 指令碼，並將它命名為 hpccharmrun.sh。如需快速概念證明，請複製本文結尾所提供的範例 hpccharmrun.sh 指令碼並移至[提交 NAMD 工作](#submit-a-namd-job)。</span><span class="sxs-lookup"><span data-stu-id="2b935-189">Using a text editor of your choice, create a Bash script in the /namd2 folder containing the NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy the example hpccharmrun.sh script provided at the end of this article and go to [Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="2b935-190">將您的指令碼儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="2b935-191">這可確保它在 Linux 節點上正常運作。</span><span class="sxs-lookup"><span data-stu-id="2b935-191">This ensures that it runs properly on the Linux nodes.</span></span>
> 
> 

<span data-ttu-id="2b935-192">以下是這個 bash 指令碼的詳細作業內容。</span><span class="sxs-lookup"><span data-stu-id="2b935-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="2b935-193">定義一些變數。</span><span class="sxs-lookup"><span data-stu-id="2b935-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # The path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="2b935-194">從環境變數取得節點資訊。</span><span class="sxs-lookup"><span data-stu-id="2b935-194">Get node information from the environment variables.</span></span> <span data-ttu-id="2b935-195">$NODESCORES 會儲存來自 $CCP_NODES_CORES 的分割單字清單。</span><span class="sxs-lookup"><span data-stu-id="2b935-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="2b935-196">$COUNT 是 $NODESCORES 的大小。</span><span class="sxs-lookup"><span data-stu-id="2b935-196">$COUNT is the size of $NODESCORES.</span></span>
   
   ```
   # Get node information from the environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="2b935-197">$CCP_NODES_CORES 變數的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b935-197">The format for the $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="2b935-198">此變數會列出節點總數、節點名稱和配置給工作之每個節點上的核心數目。</span><span class="sxs-lookup"><span data-stu-id="2b935-198">This variable lists the total number of nodes, node names, and number of cores on each node that are allocated to the job.</span></span> <span data-ttu-id="2b935-199">例如，如果工作需要 10 個核心以執行，$CCP_NODES_CORES 的值會類似：</span><span class="sxs-lookup"><span data-stu-id="2b935-199">For example, if the job needs 10 cores to run, the value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="2b935-200">如果未設定 $CCP_NODES_CORES 變數，請直接啟動 **charmrun**。</span><span class="sxs-lookup"><span data-stu-id="2b935-200">If the $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="2b935-201">(這應該只有當您在 Linux 節點上直接執行這個指令碼時才會發生。)</span><span class="sxs-lookup"><span data-stu-id="2b935-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="2b935-202">或者為 **charmrun**建立節點清單檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create the nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write the head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into the nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="2b935-203">搭配節點清單檔案執行 **charmrun** ，取得其傳回狀態，並且在結束時移除節點清單檔案。</span><span class="sxs-lookup"><span data-stu-id="2b935-203">Run **charmrun** with the nodelist file, get its return status, and remove the nodelist file at the end.</span></span>
   
   <span data-ttu-id="2b935-204">${CCP_NUMCPUS} 是 HPC Pack 前端節點所設定的另一個環境變數。</span><span class="sxs-lookup"><span data-stu-id="2b935-204">${CCP_NUMCPUS} is another environment variable set by the HPC Pack head node.</span></span> <span data-ttu-id="2b935-205">它會儲存配置給這項工作的總核心數目。</span><span class="sxs-lookup"><span data-stu-id="2b935-205">It stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="2b935-206">我們可以用它來為 charmrun 指定處理序數目。</span><span class="sxs-lookup"><span data-stu-id="2b935-206">We use it to specify the number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="2b935-207">當 **charmrun** 傳回狀態時結束。</span><span class="sxs-lookup"><span data-stu-id="2b935-207">Exit with the **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="2b935-208">以下是指令碼產生的節點清單檔案中的資訊：</span><span class="sxs-lookup"><span data-stu-id="2b935-208">Following is the information in the nodelist file, which the script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="2b935-209">例如：</span><span class="sxs-lookup"><span data-stu-id="2b935-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="2b935-210">提交 NAMD 作業</span><span class="sxs-lookup"><span data-stu-id="2b935-210">Submit a NAMD job</span></span>
<span data-ttu-id="2b935-211">現在您已準備就緒在 HPC 叢集管理員中提交 NAMD 工作。</span><span class="sxs-lookup"><span data-stu-id="2b935-211">Now you are ready to submit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="2b935-212">連接至您的叢集前端節點並且啟動 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="2b935-212">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="2b935-213">在 [Resource Management] 中，確定 Linux 計算節點處於 [線上] 狀態。</span><span class="sxs-lookup"><span data-stu-id="2b935-213">In **Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="2b935-214">如果不是，請選取這些節點，然後按一下 [ **上線**]。</span><span class="sxs-lookup"><span data-stu-id="2b935-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="2b935-215">在 [工作管理] 中，按一下 [新增工作]。</span><span class="sxs-lookup"><span data-stu-id="2b935-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="2b935-216">輸入工作的名稱，例如 *hpccharmrun*。</span><span class="sxs-lookup"><span data-stu-id="2b935-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![新的 HPC 工作][namd_job]
5. <span data-ttu-id="2b935-218">在 [工作詳細資料] 頁面的 [工作資源] 底下，選取 [節點] 做為資源類型，並且將 [最小值] 設為 3。</span><span class="sxs-lookup"><span data-stu-id="2b935-218">On the **Job Details** page, under **Job Resources**, select the type of resource as **Node** and set the **Minimum** to 3.</span></span> <span data-ttu-id="2b935-219">，我們在三個 Linux 節點上執行工作，且每個節點都有四個核心。</span><span class="sxs-lookup"><span data-stu-id="2b935-219">, we run the job on three Linux nodes and each node has four cores.</span></span>
   
   ![工作資源][job_resources]
6. <span data-ttu-id="2b935-221">按一下左導覽窗格中的 [編輯工作]，然後按一下 [加入] 來將工作加入到作業中。</span><span class="sxs-lookup"><span data-stu-id="2b935-221">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span>    
7. <span data-ttu-id="2b935-222">在 [工作詳細資料和 I/O 重新導向] 頁面上，設定下列值：</span><span class="sxs-lookup"><span data-stu-id="2b935-222">On the **Task Details and I/O Redirection** page, set the following values:</span></span>
   
   * <span data-ttu-id="2b935-223">**命令列** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="2b935-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="2b935-224">前面的命令列是不含分行符號的單一命令。</span><span class="sxs-lookup"><span data-stu-id="2b935-224">The preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="2b935-225">它會換行以出現在**命令列**的數行之下。</span><span class="sxs-lookup"><span data-stu-id="2b935-225">It wraps to appear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="2b935-226">**工作目錄** - /namd2</span><span class="sxs-lookup"><span data-stu-id="2b935-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="2b935-227">**最小值** - 3</span><span class="sxs-lookup"><span data-stu-id="2b935-227">**Minimum** - 3</span></span>
     
     ![作業詳細資料][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="2b935-229">您在這裡設定工作目錄，因為 **charmrun** 嘗試瀏覽至每個節點上相同的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="2b935-229">You set the working directory here because **charmrun** tries to navigate to the same working directory on each node.</span></span> <span data-ttu-id="2b935-230">如果未設定工作目錄，HPC Pack 會在其中一個 Linux 節點上建立的隨機命名資料夾中啟動命令。</span><span class="sxs-lookup"><span data-stu-id="2b935-230">If the working directory isn't set, HPC Pack starts the command in a randomly named folder created on one of the Linux nodes.</span></span> <span data-ttu-id="2b935-231">這會在其他節點上導致下列錯誤：`/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` 若要避免這個問題，指定所有節點可存取為工作目錄的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="2b935-231">This causes the following error on the other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` To avoid this problem, specify a folder path that can be accessed by all nodes as the working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="2b935-232">按一下 [確定]，然後按一下 [提交] 以執行此作業。</span><span class="sxs-lookup"><span data-stu-id="2b935-232">Click **OK** and then click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="2b935-233">根據預設，HPC Pack 會以您目前登入的使用者帳戶提交工作。</span><span class="sxs-lookup"><span data-stu-id="2b935-233">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="2b935-234">對話方塊可能會在您按一下 [提交] 之後提示您輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2b935-234">A dialog box might prompt you to enter the user name and password after you click **Submit**.</span></span>
   
   ![工作認證][creds]
   
   <span data-ttu-id="2b935-236">在某些情況下，HPC Pack 會記住您以前輸入的使用者資訊，而不會顯示此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2b935-236">Under some conditions, HPC Pack remembers the user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="2b935-237">若要讓 HPC Pack 再次顯示此對話方塊，請在命令提示字元中輸入下列命令，然後提交作業。</span><span class="sxs-lookup"><span data-stu-id="2b935-237">To make HPC Pack show it again, enter the following command at a Command Prompt and then submit the job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="2b935-238">工作需要數分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="2b935-238">The job takes several minutes to finish.</span></span>
10. <span data-ttu-id="2b935-239">在 \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log 中尋找工作記錄檔，在 \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\. 中尋找輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2b935-239">Find the job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and the output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="2b935-240">選擇性啟動 VMD 以檢視您的工作結果。</span><span class="sxs-lookup"><span data-stu-id="2b935-240">Optionally, start VMD to view your job results.</span></span> <span data-ttu-id="2b935-241">用來視覺化 NAMD 輸出檔案 (在此案例中，水圈中的泛素蛋白質分子) 的步驟已超出本文的範圍。</span><span class="sxs-lookup"><span data-stu-id="2b935-241">The steps for visualizing the NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond the scope of this article.</span></span> <span data-ttu-id="2b935-242">如需詳細資訊，請參閱 [NAMD 教學課程](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) 。</span><span class="sxs-lookup"><span data-stu-id="2b935-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![工作結果][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="2b935-244">範例檔案</span><span class="sxs-lookup"><span data-stu-id="2b935-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="2b935-245">PowerShell 指令碼叢集部署的 XML 組態檔範例</span><span class="sxs-lookup"><span data-stu-id="2b935-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="2b935-246">範例 cred.xml 檔案</span><span class="sxs-lookup"><span data-stu-id="2b935-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="2b935-247">範例 hpccharmrun.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="2b935-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # If CCP_NODES_CORES is not found or is empty, just run the charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create the nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write the head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into the nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the charmrun with nodelist arg
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
