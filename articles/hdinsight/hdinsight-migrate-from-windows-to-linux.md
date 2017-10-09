---
title: "從 Windows 為基礎的 HDInsight aaaMigrate tooLinux 為基礎的 HDInsight 的 Azure |Microsoft 文件"
description: "了解如何從 Windows 為基礎的 HDInsight toomigrate 叢集 tooa 以 Linux 為基礎的 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a><span data-ttu-id="288dd-103">從 Windows 為基礎的 HDInsight 叢集 tooa Linux 為基礎的叢集移轉</span><span class="sxs-lookup"><span data-stu-id="288dd-103">Migrate from a Windows-based HDInsight cluster tooa Linux-based cluster</span></span>

<span data-ttu-id="288dd-104">本文件提供 Windows 和 Linux 的 HDInsight 和指引的 hello 差異的詳細資料 toomigrate 現有工作負載 tooa linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-104">This document provides details on hello differences between HDInsight on Windows and Linux, and guidance on how toomigrate existing workloads tooa Linux-based cluster.</span></span>

<span data-ttu-id="288dd-105">雖然 Windows 為基礎的 HDInsight 提供簡單的方式 toouse Hadoop hello 雲端中，您可能需要 toomigrate tooa linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-105">While Windows-based HDInsight provides an easy way toouse Hadoop in hello cloud, you may need toomigrate tooa Linux-based cluster.</span></span> <span data-ttu-id="288dd-106">例如，tootake 利用以 Linux 為基礎的工具和技術所需的方案。</span><span class="sxs-lookup"><span data-stu-id="288dd-106">For example, tootake advantage of Linux-based tools and technologies that are required for your solution.</span></span> <span data-ttu-id="288dd-107">Hello Hadoop 生態系統中的許多項目會以 Linux 為基礎的系統上開發，並可能無法使用以 Windows 為基礎的 HDInsight 的使用。</span><span class="sxs-lookup"><span data-stu-id="288dd-107">Many things in hello Hadoop ecosystem are developed on Linux-based systems, and may not be available for use with Windows-based HDInsight.</span></span> <span data-ttu-id="288dd-108">除此之外，許多針對 Hadoop 的書籍、影片及其他訓練材料，都會假設您正在使用 Linux 系統。</span><span class="sxs-lookup"><span data-stu-id="288dd-108">Additionally, many books, videos, and other training material assume that you are using a Linux system when working with Hadoop.</span></span>

> [!NOTE]
> <span data-ttu-id="288dd-109">HDInsight 叢集會使用 Ubuntu 長期支援 (LTS) 做為 hello 作業系統 hello hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="288dd-109">HDInsight clusters use Ubuntu long-term support (LTS) as hello operating system for hello nodes in hello cluster.</span></span> <span data-ttu-id="288dd-110">如需其他元件的版本控制資訊與 HDInsight，可用的 Ubuntu hello 版本資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-110">For information on hello version of Ubuntu available with HDInsight, along with other component versioning information, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="migration-tasks"></a><span data-ttu-id="288dd-111">移轉工作</span><span class="sxs-lookup"><span data-stu-id="288dd-111">Migration tasks</span></span>

<span data-ttu-id="288dd-112">如下所示為 hello 移轉的一般工作流程。</span><span class="sxs-lookup"><span data-stu-id="288dd-112">hello general workflow for migration is as follows.</span></span>

![移轉工作流程圖表](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. <span data-ttu-id="288dd-114">讀取這份文件的每個區段 toounderstand 變更時，可能會需要移轉您現有的工作流程、 作業、 等 tooa linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-114">Read each section of this document toounderstand changes that may be required when migrating your existing workflow, jobs, etc. tooa Linux-based cluster.</span></span>

2. <span data-ttu-id="288dd-115">建立以 Linux 為基礎的叢集做為測試/品質保證環境。</span><span class="sxs-lookup"><span data-stu-id="288dd-115">Create a Linux-based cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="288dd-116">如需建立以 Linux 為基礎之叢集的詳細資訊，請參閱 [在 HDInsight 中建立以 Linux 為基礎的叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-116">For more information on creating a Linux-based cluster, see [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

3. <span data-ttu-id="288dd-117">現有的作業、 資料來源和接收器 toohello 新環境的複本。</span><span class="sxs-lookup"><span data-stu-id="288dd-117">Copy existing jobs, data sources, and sinks toohello new environment.</span></span>

4. <span data-ttu-id="288dd-118">執行驗證測試 toomake 確定您作業的工作，如預期般 hello 新叢集上。</span><span class="sxs-lookup"><span data-stu-id="288dd-118">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>

<span data-ttu-id="288dd-119">一旦您已確認一切運作正常，排程 hello 移轉停機的時間。</span><span class="sxs-lookup"><span data-stu-id="288dd-119">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="288dd-120">在這個停機時間，執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="288dd-120">During this downtime, perform hello following actions:</span></span>

1. <span data-ttu-id="288dd-121">備份儲存在本機 hello 叢集節點上的任何暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="288dd-121">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="288dd-122">例如，如果您的資料是直接儲存在前端節點上。</span><span class="sxs-lookup"><span data-stu-id="288dd-122">For example, if you have data stored directly on a head node.</span></span>

2. <span data-ttu-id="288dd-123">刪除 hello windows 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-123">Delete hello Windows-based cluster.</span></span>

3. <span data-ttu-id="288dd-124">建立以 Linux 為基礎的叢集使用的 hello 相同預設 hello Windows 為基礎的叢集使用的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="288dd-124">Create a Linux-based cluster using hello same default data store that hello Windows-based cluster used.</span></span> <span data-ttu-id="288dd-125">hello Linux 架構叢集可以繼續使用現有的實際執行資料。</span><span class="sxs-lookup"><span data-stu-id="288dd-125">hello Linux-based cluster can continue working against your existing production data.</span></span>

4. <span data-ttu-id="288dd-126">匯入任何已備份的暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="288dd-126">Import any transient data you backed up.</span></span>

5. <span data-ttu-id="288dd-127">開始作業/仍會繼續處理使用 hello 新叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-127">Start jobs/continue processing using hello new cluster.</span></span>

### <a name="copy-data-toohello-test-environment"></a><span data-ttu-id="288dd-128">複製資料 toohello 測試環境</span><span class="sxs-lookup"><span data-stu-id="288dd-128">Copy data toohello test environment</span></span>

<span data-ttu-id="288dd-129">有許多方法 toocopy hello 資料和作業，兩個 hello 但是本節所討論 hello 最簡單方法 toodirectly 移動檔案 tooa 測試叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-129">There are many methods toocopy hello data and jobs, however hello two discussed in this section are hello simplest methods toodirectly move files tooa test cluster.</span></span>

#### <a name="hdfs-copy"></a><span data-ttu-id="288dd-130">HDFS 複製</span><span class="sxs-lookup"><span data-stu-id="288dd-130">HDFS copy</span></span>

<span data-ttu-id="288dd-131">使用 hello hello 實際執行叢集 toohello 測試叢集的下列步驟 toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="288dd-131">Use hello following steps toocopy data from hello production cluster toohello test cluster.</span></span> <span data-ttu-id="288dd-132">這些步驟使用 hello`hdfs dfs`隨附 HDInsight 的公用程式。</span><span class="sxs-lookup"><span data-stu-id="288dd-132">These steps use hello `hdfs dfs` utility that is included with HDInsight.</span></span>

1. <span data-ttu-id="288dd-133">尋找 hello 儲存體帳戶與預設容器資訊為您現有的叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-133">Find hello storage account and default container information for your existing cluster.</span></span> <span data-ttu-id="288dd-134">hello 下列範例會使用 PowerShell tooretrieve 這項資訊：</span><span class="sxs-lookup"><span data-stu-id="288dd-134">hello following example uses PowerShell tooretrieve this information:</span></span>

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. <span data-ttu-id="288dd-135">toocreate 測試環境中，步驟 hello HDInsight 文件中的 hello 建立 linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-135">toocreate a test environment, follow hello steps in hello Create Linux-based clusters in HDInsight document.</span></span> <span data-ttu-id="288dd-136">建立 hello 叢集之前停止，而是選取**選擇性組態**。</span><span class="sxs-lookup"><span data-stu-id="288dd-136">Stop before creating hello cluster, and instead select **Optional Configuration**.</span></span>

3. <span data-ttu-id="288dd-137">從 hello 選擇性組態刀鋒視窗中，選取**連結儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="288dd-137">From hello Optional Configuration blade, select **Linked Storage Accounts**.</span></span>

4. <span data-ttu-id="288dd-138">選取**新增儲存體金鑰**，並出現提示時，選取 hello hello 在步驟 1 中的 PowerShell 指令碼傳回的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="288dd-138">Select **Add a storage key**, and when prompted, select hello storage account that was returned by hello PowerShell script in step 1.</span></span> <span data-ttu-id="288dd-139">在每個刀鋒視窗上按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="288dd-139">Click **Select** on each blade.</span></span> <span data-ttu-id="288dd-140">最後，建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-140">Finally, create hello cluster.</span></span>

5. <span data-ttu-id="288dd-141">一旦建立 hello 叢集之後，使用 tooit 連接**SSH。**</span><span class="sxs-lookup"><span data-stu-id="288dd-141">Once hello cluster has been created, connect tooit using **SSH.**</span></span> <span data-ttu-id="288dd-142">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-142">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

6. <span data-ttu-id="288dd-143">從 hello SSH 工作階段，使用 hello hello 連結儲存體帳戶 toohello 新預設儲存體帳戶中的下列命令 toocopy 檔案。</span><span class="sxs-lookup"><span data-stu-id="288dd-143">From hello SSH session, use hello following command toocopy files from hello linked storage account toohello new default storage account.</span></span> <span data-ttu-id="288dd-144">取代 PowerShell 傳回 hello 容器資訊的容器。</span><span class="sxs-lookup"><span data-stu-id="288dd-144">Replace CONTAINER with hello container information returned by PowerShell.</span></span> <span data-ttu-id="288dd-145">取代__帳戶__hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="288dd-145">Replace __ACCOUNT__ with hello account name.</span></span> <span data-ttu-id="288dd-146">Hello 路徑 toodata 取代 hello 路徑 tooa 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="288dd-146">Replace hello path toodata with hello path tooa data file.</span></span>

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > <span data-ttu-id="288dd-147">如果 hello 目錄結構，其中包含 hello 資料不存在於 hello 測試環境中，您可以建立使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="288dd-147">If hello directory structure that contains hello data does not exist on hello test environment, you can create it using hello following command:</span></span>

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    <span data-ttu-id="288dd-148">hello`-p`參數可讓 hello 建立 hello 路徑中的所有目錄。</span><span class="sxs-lookup"><span data-stu-id="288dd-148">hello `-p` switch enables hello creation of all directories in  hello path.</span></span>

#### <a name="direct-copy-between-blobs-in-azure-storage"></a><span data-ttu-id="288dd-149">在 Azure 儲存體中的 Blob 之間直接複製</span><span class="sxs-lookup"><span data-stu-id="288dd-149">Direct copy between blobs in Azure Storage</span></span>

<span data-ttu-id="288dd-150">或者，您可能想 toouse hello`Start-AzureStorageBlobCopy`之間 HDInsight 之外的儲存體帳戶的 Azure PowerShell cmdlet toocopy blob。</span><span class="sxs-lookup"><span data-stu-id="288dd-150">Alternatively, you may want toouse hello `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet toocopy blobs between storage accounts outside of HDInsight.</span></span> <span data-ttu-id="288dd-151">如需詳細資訊，請參閱 hello 如何 toomanage 與 Azure 儲存體使用 Azure PowerShell 的 Azure Blob > 一節。</span><span class="sxs-lookup"><span data-stu-id="288dd-151">For more information, see hello How toomanage Azure Blobs section of Using Azure PowerShell with Azure Storage.</span></span>

## <a name="client-side-technologies"></a><span data-ttu-id="288dd-152">用戶端技術</span><span class="sxs-lookup"><span data-stu-id="288dd-152">Client-side technologies</span></span>

<span data-ttu-id="288dd-153">用戶端技術，例如[Azure PowerShell cmdlet](/powershell/azureps-cmdlets-docs)， [Azure CLI](../cli-install-nodejs.md)，或使用 hello [Hadoop 的.NET SDK](https://hadoopsdk.codeplex.com/)繼續 toowork linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-153">Client-side technologies such as [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), or hello [.NET SDK for Hadoop](https://hadoopsdk.codeplex.com/) continue toowork Linux-based clusters.</span></span> <span data-ttu-id="288dd-154">這些技術依賴 REST hello 相同跨兩個叢集作業系統類型的 Api。</span><span class="sxs-lookup"><span data-stu-id="288dd-154">These technologies rely on REST APIs that are hello same across both cluster OS types.</span></span>

## <a name="server-side-technologies"></a><span data-ttu-id="288dd-155">伺服器端技術</span><span class="sxs-lookup"><span data-stu-id="288dd-155">Server-side technologies</span></span>

<span data-ttu-id="288dd-156">下表中的 hello 移轉是 Windows 特定的伺服器端元件提供指引。</span><span class="sxs-lookup"><span data-stu-id="288dd-156">hello following table provides guidance on migrating server-side components that are Windows-specific.</span></span>

| <span data-ttu-id="288dd-157">如果您正在使用這項技術...</span><span class="sxs-lookup"><span data-stu-id="288dd-157">If you are using this technology...</span></span> | <span data-ttu-id="288dd-158">請執行此動作...</span><span class="sxs-lookup"><span data-stu-id="288dd-158">Take this action...</span></span> |
| --- | --- |
| <span data-ttu-id="288dd-159">**PowerShell** (伺服器端指令碼，包含於叢集建立期間使用的指令碼動作)</span><span class="sxs-lookup"><span data-stu-id="288dd-159">**PowerShell** (server-side scripts, including Script Actions used during cluster creation)</span></span> |<span data-ttu-id="288dd-160">重寫為 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="288dd-160">Rewrite as Bash scripts.</span></span> <span data-ttu-id="288dd-161">針對指令碼動作，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)和[以 Linux 為基礎之 HDInsight 的指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-161">For Script Actions, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span> |
| <span data-ttu-id="288dd-162">**Azure CLI** (伺服器端指令碼)</span><span class="sxs-lookup"><span data-stu-id="288dd-162">**Azure CLI** (server-side scripts)</span></span> |<span data-ttu-id="288dd-163">Hello Azure CLI Linux 上的可用時，它不會顯示預先安裝在 hello HDInsight 叢集前端節點上。</span><span class="sxs-lookup"><span data-stu-id="288dd-163">While hello Azure CLI is available on Linux, it does not come pre-installed on hello HDInsight cluster head nodes.</span></span> <span data-ttu-id="288dd-164">如需有關如何安裝 hello Azure CLI 的詳細資訊，請參閱[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="288dd-164">For more information on installing hello Azure CLI, see [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span> |
| <span data-ttu-id="288dd-165">**.NET 元件**</span><span class="sxs-lookup"><span data-stu-id="288dd-165">**.NET components**</span></span> |<span data-ttu-id="288dd-166">以 Linux 為基礎的 HDInsight 透過 [Mono](https://mono-project.com) 支援 .NET。</span><span class="sxs-lookup"><span data-stu-id="288dd-166">.NET is supported on Linux-based HDInsight through [Mono](https://mono-project.com).</span></span> <span data-ttu-id="288dd-167">如需詳細資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-167">For more information, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span> |
| <span data-ttu-id="288dd-168">**Win32 元件或其他僅限 Windows 的技術**</span><span class="sxs-lookup"><span data-stu-id="288dd-168">**Win32 components or other Windows-only technology**</span></span> |<span data-ttu-id="288dd-169">指引取決於 hello 元件或技術。</span><span class="sxs-lookup"><span data-stu-id="288dd-169">Guidance depends on hello component or technology.</span></span> <span data-ttu-id="288dd-170">您可能無法 toofind 與 Linux 相容的版本，或您可能需要 toofind 替代解決方案，或重寫此元件。</span><span class="sxs-lookup"><span data-stu-id="288dd-170">You may be able toofind a version that is compatible with Linux, or you may need toofind an alternate solution or rewrite this component.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="288dd-171">hello HDInsight 管理 SDK 不是與 單聲道完全相容。</span><span class="sxs-lookup"><span data-stu-id="288dd-171">hello HDInsight management SDK is not fully compatible with Mono.</span></span> <span data-ttu-id="288dd-172">它不應為方案的一部分已 toohello HDInsight 叢集部署在這個階段。</span><span class="sxs-lookup"><span data-stu-id="288dd-172">It should not be used as part of solutions deployed toohello HDInsight cluster at this time.</span></span>

## <a name="cluster-creation"></a><span data-ttu-id="288dd-173">叢集建立</span><span class="sxs-lookup"><span data-stu-id="288dd-173">Cluster creation</span></span>

<span data-ttu-id="288dd-174">本節將提供叢集建立之差異的資訊。</span><span class="sxs-lookup"><span data-stu-id="288dd-174">This section provides information on differences in cluster creation.</span></span>

### <a name="ssh-user"></a><span data-ttu-id="288dd-175">SSH 使用者</span><span class="sxs-lookup"><span data-stu-id="288dd-175">SSH User</span></span>

<span data-ttu-id="288dd-176">以 Linux 為基礎的 HDInsight 叢集使用 hello**安全殼層 (SSH)**通訊協定 tooprovide 遠端存取 toohello 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="288dd-176">Linux-based HDInsight clusters use hello **Secure Shell (SSH)** protocol tooprovide remote access toohello cluster nodes.</span></span> <span data-ttu-id="288dd-177">不同於以 Windows 為基礎之叢集的遠端桌面，大部分的 SSH 用戶端不提供圖形化使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="288dd-177">Unlike Remote Desktop for Windows-based clusters, most SSH clients do not provide a graphical user experience.</span></span> <span data-ttu-id="288dd-178">相反地，SSH 用戶端提供可讓您在 hello 叢集的 toorun 命令的命令列。</span><span class="sxs-lookup"><span data-stu-id="288dd-178">Instead, SSH clients provide a command line that allows you toorun commands on hello cluster.</span></span> <span data-ttu-id="288dd-179">某些用戶端 (例如[MobaXterm](http://mobaxterm.mobatek.net/)) 提供圖形化的檔案系統瀏覽器加法 tooa 遠端命令列中。</span><span class="sxs-lookup"><span data-stu-id="288dd-179">Some clients (such as [MobaXterm](http://mobaxterm.mobatek.net/)) provide a graphical file system browser in addition tooa remote command line.</span></span>

<span data-ttu-id="288dd-180">在叢集建立期間，您必須提供 SSH 使用者，以及**密碼**或**公開金鑰憑證**以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="288dd-180">During cluster creation, you must provide an SSH user and either a **password** or **public key certificate** for authentication.</span></span>

<span data-ttu-id="288dd-181">我們建議使用公開金鑰憑證，因為它比密碼更安全。</span><span class="sxs-lookup"><span data-stu-id="288dd-181">We recommend using Public key certificate, as it is more secure than using a password.</span></span> <span data-ttu-id="288dd-182">憑證驗證的運作方式產生帶正負號的 public/private 金鑰組，然後建立 hello 叢集時，提供 hello 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="288dd-182">Certificate authentication works by generating a signed public/private key pair, then providing hello public key when creating hello cluster.</span></span> <span data-ttu-id="288dd-183">連接時使用 SSH toohello 伺服器，hello hello 用戶端上的私用金鑰提供 hello 連線的驗證。</span><span class="sxs-lookup"><span data-stu-id="288dd-183">When connecting toohello server using SSH, hello private key on hello client provides authentication for hello connection.</span></span>

<span data-ttu-id="288dd-184">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-184">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="cluster-customization"></a><span data-ttu-id="288dd-185">叢集自訂</span><span class="sxs-lookup"><span data-stu-id="288dd-185">Cluster customization</span></span>

<span data-ttu-id="288dd-186">**指令碼動作** 必須以 Bash 指令碼撰寫。</span><span class="sxs-lookup"><span data-stu-id="288dd-186">**Script Actions** used with Linux-based clusters must be written in Bash script.</span></span> <span data-ttu-id="288dd-187">雖然您可以使用指令碼動作在叢集建立期間，以 Linux 為基礎的叢集，也可以使用的 tooperform 自訂之後叢集已啟動和執行。</span><span class="sxs-lookup"><span data-stu-id="288dd-187">While Script Actions can be used during cluster creation, for Linux-based clusters they can also be used tooperform customization after a cluster is up and running.</span></span> <span data-ttu-id="288dd-188">如需詳細資訊，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)和[以 Linux 為基礎之 HDInsight 的指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-188">For more information, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

<span data-ttu-id="288dd-189">另一個自訂功能是 **bootstrap**。</span><span class="sxs-lookup"><span data-stu-id="288dd-189">Another customization feature is **bootstrap**.</span></span> <span data-ttu-id="288dd-190">適用於 Windows 叢集，這項功能可讓您 toospecify hello 位置的登錄區搭配使用的其他程式庫。</span><span class="sxs-lookup"><span data-stu-id="288dd-190">For Windows clusters, this feature allows you toospecify hello location of additional libraries for use with Hive.</span></span> <span data-ttu-id="288dd-191">叢集建立之後，這些程式庫會自動提供用於 Hive 查詢沒有 hello 需要 toouse `ADD JAR`。</span><span class="sxs-lookup"><span data-stu-id="288dd-191">After cluster creation, these libraries are automatically available for use with Hive queries without hello need toouse `ADD JAR`.</span></span>

<span data-ttu-id="288dd-192">hello 啟動程序以 Linux 為基礎的叢集功能不提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="288dd-192">hello Bootstrap feature for Linux-based clusters does not provide this functionality.</span></span> <span data-ttu-id="288dd-193">請改為使用 [在叢集建立期間新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)中所記錄的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="288dd-193">Instead, use script action documented in [Add Hive libraries during cluster creation](hdinsight-hadoop-add-hive-libraries.md).</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="288dd-194">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="288dd-194">Virtual Networks</span></span>

<span data-ttu-id="288dd-195">以 Windows 為基礎的 HDInsight 僅支援傳統虛擬網路，而以 Linux 為基礎的 HDInsight 則需要資源管理員虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="288dd-195">Windows-based HDInsight clusters only work with Classic Virtual Networks, while Linux-based HDInsight clusters require Resource Manager Virtual Networks.</span></span> <span data-ttu-id="288dd-196">如果您在資源 hello Linux HDInsight 叢集的傳統的虛擬網路必須連接到，請參閱[連接傳統虛擬網路 tooa 資源管理員虛擬網路](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-196">If you have resources in a Classic Virtual Network that hello Linux-HDInsight cluster must connect to, see [Connecting a Classic Virtual Network tooa Resource Manager Virtual Network](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

<span data-ttu-id="288dd-197">如需搭配 HDInsight 使用 Azure 虛擬網路之設定需求的詳細資訊，請參閱 [使用虛擬網路延伸 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-197">For more information on configuration requirements for using Azure Virtual Networks with HDInsight, see [Extend HDInsight capabilities by using a Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a name="management-and-monitoring"></a><span data-ttu-id="288dd-198">管理與監視</span><span class="sxs-lookup"><span data-stu-id="288dd-198">Management and monitoring</span></span>

<span data-ttu-id="288dd-199">許多的 hello web Ui，您可能已經使用以 Windows 為基礎的 HDInsight，例如作業歷程記錄或 Yarn UI 都可透過 Ambari。</span><span class="sxs-lookup"><span data-stu-id="288dd-199">Many of hello web UIs you may have used with Windows-based HDInsight, such as Job History or Yarn UI, are available through Ambari.</span></span> <span data-ttu-id="288dd-200">此外，hello Ambari Hive 檢視提供方式 toorun 使用網頁瀏覽器的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="288dd-200">In addition, hello Ambari Hive View provides a way toorun Hive queries using your web browser.</span></span> <span data-ttu-id="288dd-201">在 https://CLUSTERNAME.azurehdinsight.net 以 Linux 為基礎的叢集上使用 hello Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="288dd-201">hello Ambari Web UI is available on Linux-based clusters at https://CLUSTERNAME.azurehdinsight.net.</span></span>

<span data-ttu-id="288dd-202">如需使用 Ambari 的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="288dd-202">For more information on working with Ambari, see hello following documents:</span></span>

* [<span data-ttu-id="288dd-203">Ambari Web</span><span class="sxs-lookup"><span data-stu-id="288dd-203">Ambari Web</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="288dd-204">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="288dd-204">Ambari REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a><span data-ttu-id="288dd-205">Ambari 警示</span><span class="sxs-lookup"><span data-stu-id="288dd-205">Ambari Alerts</span></span>

<span data-ttu-id="288dd-206">Ambari 有可以告訴您 hello 叢集中的潛在問題的警示系統。</span><span class="sxs-lookup"><span data-stu-id="288dd-206">Ambari has an alert system that can tell you of potential problems with hello cluster.</span></span> <span data-ttu-id="288dd-207">不過，您也可以擷取它們透過 hello REST API，警示會顯示為紅色或黃色中 hello Ambari Web UI 中的項目。</span><span class="sxs-lookup"><span data-stu-id="288dd-207">Alerts appear as red or yellow entries in hello Ambari Web UI, however you can also retrieve them through hello REST API.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="288dd-208">Ambari 警示代表「可能有」問題，而不表示「已發生」問題。</span><span class="sxs-lookup"><span data-stu-id="288dd-208">Ambari alerts indicate that there *may* be a problem, not that there *is* a problem.</span></span> <span data-ttu-id="288dd-209">例如，您可能會收到無法存取 HiveServer2 的警示，但實際上您仍然可以正常存取它。</span><span class="sxs-lookup"><span data-stu-id="288dd-209">For example, you may receive an alert that HiveServer2 cannot be accessed, even though you can access it normally.</span></span>
>
> <span data-ttu-id="288dd-210">許多警示都是針對某項服務實作為以間隔為基礎的查詢，並會預期在特定的時間範圍內收到回應。</span><span class="sxs-lookup"><span data-stu-id="288dd-210">Many alerts are implemented as interval-based queries against a service, and expect a response within a specific time frame.</span></span> <span data-ttu-id="288dd-211">因此 hello 警示並不一定表示 hello 服務已關閉，它未傳回預期的 hello 時間範圍內的結果。</span><span class="sxs-lookup"><span data-stu-id="288dd-211">So hello alert doesn't necessarily mean that hello service is down, just that it didn't return results within hello expected time frame.</span></span>

<span data-ttu-id="288dd-212">您應先評估某個警示是否已長時間持續發生，或者是否與使用者所回報的某個問題有關，再對它採取動作。</span><span class="sxs-lookup"><span data-stu-id="288dd-212">You should evaluate whether an alert has been occurring for an extended period, or mirrors user problems that have been reported before taking action on it.</span></span>

## <a name="file-system-locations"></a><span data-ttu-id="288dd-213">檔案系統位置</span><span class="sxs-lookup"><span data-stu-id="288dd-213">File system locations</span></span>

<span data-ttu-id="288dd-214">hello Linux 叢集檔案系統的方式不同於 Windows 為基礎的 HDInsight 叢集配置。</span><span class="sxs-lookup"><span data-stu-id="288dd-214">hello Linux cluster file system is laid out differently than Windows-based HDInsight clusters.</span></span> <span data-ttu-id="288dd-215">使用下列資料表 toofind 常用檔案 hello。</span><span class="sxs-lookup"><span data-stu-id="288dd-215">Use hello following table toofind commonly used files.</span></span>

| <span data-ttu-id="288dd-216">我需要 toofind...</span><span class="sxs-lookup"><span data-stu-id="288dd-216">I need toofind...</span></span> | <span data-ttu-id="288dd-217">它位於...</span><span class="sxs-lookup"><span data-stu-id="288dd-217">It is located...</span></span> |
| --- | --- |
| <span data-ttu-id="288dd-218">組態</span><span class="sxs-lookup"><span data-stu-id="288dd-218">Configuration</span></span> |<span data-ttu-id="288dd-219">`/etc`。</span><span class="sxs-lookup"><span data-stu-id="288dd-219">`/etc`.</span></span> <span data-ttu-id="288dd-220">例如， `/etc/hadoop/conf/core-site.xml`</span><span class="sxs-lookup"><span data-stu-id="288dd-220">For example, `/etc/hadoop/conf/core-site.xml`</span></span> |
| <span data-ttu-id="288dd-221">記錄檔</span><span class="sxs-lookup"><span data-stu-id="288dd-221">Log files</span></span> |`/var/logs` |
| <span data-ttu-id="288dd-222">Hortonworks Data Platform (HDP)</span><span class="sxs-lookup"><span data-stu-id="288dd-222">Hortonworks Data Platform (HDP)</span></span> |<span data-ttu-id="288dd-223">`/usr/hdp`.有兩個目錄位在此處，其中是目前 HDP 版本 hello 和`current`。</span><span class="sxs-lookup"><span data-stu-id="288dd-223">`/usr/hdp`.There are two directories located here, one that is hello current HDP version and `current`.</span></span> <span data-ttu-id="288dd-224">hello`current`目錄包含符號連結 toofiles 和 hello 版本號碼的目錄中的目錄。</span><span class="sxs-lookup"><span data-stu-id="288dd-224">hello `current` directory contains symbolic links toofiles and directories located in hello version number directory.</span></span> <span data-ttu-id="288dd-225">hello`current`目錄已提供作為便利的方式存取自 hello 變更版本號碼為 hello HDP HDP 檔案的版本會更新。</span><span class="sxs-lookup"><span data-stu-id="288dd-225">hello `current` directory is provided as a convenient way of accessing HDP files since hello version number changes as hello HDP version is updated.</span></span> |
| <span data-ttu-id="288dd-226">hadoop-streaming.jar</span><span class="sxs-lookup"><span data-stu-id="288dd-226">hadoop-streaming.jar</span></span> |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

<span data-ttu-id="288dd-227">一般情況下，如果您知道 hello hello 檔案名稱，您可以使用 hello SSH 工作階段 toofind hello 檔案路徑中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="288dd-227">In general, if you know hello name of hello file, you can use hello following command from an SSH session toofind hello file path:</span></span>

    find / -name FILENAME 2>/dev/null

<span data-ttu-id="288dd-228">您也可以使用萬用字元 hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="288dd-228">You can also use wildcards with hello file name.</span></span> <span data-ttu-id="288dd-229">例如，`find / -name *streaming*.jar 2>/dev/null`傳回 hello 路徑 tooany jar 檔案包含 hello 字 '串流' hello 檔案名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="288dd-229">For example, `find / -name *streaming*.jar 2>/dev/null` returns hello path tooany jar files that contain hello word 'streaming' as part of hello file name.</span></span>

## <a name="hive-pig-and-mapreduce"></a><span data-ttu-id="288dd-230">Hive、Pig 及 MapReduce</span><span class="sxs-lookup"><span data-stu-id="288dd-230">Hive, Pig, and MapReduce</span></span>

<span data-ttu-id="288dd-231">Pig 和 MapReduce 工作負載在 Linux 為基礎的叢集上很相似。</span><span class="sxs-lookup"><span data-stu-id="288dd-231">Pig and MapReduce workloads are similar on Linux-based clusters.</span></span> <span data-ttu-id="288dd-232">不過，您可以使用較新版本的 Hadoop、Hive 和 Pig 建立以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-232">However, Linux-based HDInsight clusters can be created using newer versions of Hadoop, Hive, and Pig.</span></span> <span data-ttu-id="288dd-233">這些版本的差異可能會對您現有方案的運作方式造成變更。</span><span class="sxs-lookup"><span data-stu-id="288dd-233">These version differences may introduce changes in how your existing solutions function.</span></span> <span data-ttu-id="288dd-234">Hello 版本的元件，包含在 HDInsight 上的詳細資訊，請參閱[HDInsight 的元件版本控制](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-234">For more information on hello versions of components included with HDInsight, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="288dd-235">以 Linux 為基礎的 HDInsight 不提供遠端桌面功能。</span><span class="sxs-lookup"><span data-stu-id="288dd-235">Linux-based HDInsight does not provide remote desktop functionality.</span></span> <span data-ttu-id="288dd-236">相反地，您可以使用 SSH tooremotely 連接 toohello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="288dd-236">Instead, you can use SSH tooremotely connect toohello cluster head nodes.</span></span> <span data-ttu-id="288dd-237">如需詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="288dd-237">For more information, see hello following documents:</span></span>

* [<span data-ttu-id="288dd-238">搭配 SSH 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="288dd-238">Use Hive with SSH</span></span>](hdinsight-hadoop-use-hive-ssh.md)
* [<span data-ttu-id="288dd-239">搭配 SSH 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="288dd-239">Use Pig with SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md)
* [<span data-ttu-id="288dd-240">搭配 SSH 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="288dd-240">Use MapReduce with SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a><span data-ttu-id="288dd-241">Hive</span><span class="sxs-lookup"><span data-stu-id="288dd-241">Hive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="288dd-242">如果您使用外部的 Hive 中繼存放區，您應該備份之前使用 linux 的 HDInsight hello 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="288dd-242">If you use an external Hive metastore, you should back up hello metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="288dd-243">以 Linux 為基礎的 HDInsight 可搭配較新版本的 Hive 使用，但可能會與舊版建立的中繼存放區不相容。</span><span class="sxs-lookup"><span data-stu-id="288dd-243">Linux-based HDInsight is available with newer versions of Hive, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="288dd-244">hello 下列圖表會提供有關移轉您的登錄區工作負載的指引。</span><span class="sxs-lookup"><span data-stu-id="288dd-244">hello following chart provides guidance on migrating your Hive workloads.</span></span>

| <span data-ttu-id="288dd-245">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="288dd-245">On Windows-based, I use...</span></span> | <span data-ttu-id="288dd-246">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="288dd-246">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="288dd-247">**Hive 編輯器**</span><span class="sxs-lookup"><span data-stu-id="288dd-247">**Hive Editor**</span></span> |[<span data-ttu-id="288dd-248">Ambari 中的 Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="288dd-248">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |
| <span data-ttu-id="288dd-249">`set hive.execution.engine=tez;`tooenable Tez</span><span class="sxs-lookup"><span data-stu-id="288dd-249">`set hive.execution.engine=tez;` tooenable Tez</span></span> |<span data-ttu-id="288dd-250">Tez hello linux 叢集的預設執行引擎，因此 hello 設定陳述式已不再需要。</span><span class="sxs-lookup"><span data-stu-id="288dd-250">Tez is hello default execution engine for Linux-based clusters, so hello set statement is no longer needed.</span></span> |
| <span data-ttu-id="288dd-251">C# 使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="288dd-251">C# user-defined functions</span></span> | <span data-ttu-id="288dd-252">驗證 C# 元件，以 Linux 為基礎的 HDInsight 上的資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="288dd-252">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="288dd-253">CMD 檔案或登錄區工作的一部分叫用的 hello 伺服器上的指令碼</span><span class="sxs-lookup"><span data-stu-id="288dd-253">CMD files or scripts on hello server invoked as part of a Hive job</span></span> |<span data-ttu-id="288dd-254">使用 Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="288dd-254">use Bash scripts</span></span> |
| <span data-ttu-id="288dd-255">`hive` 命令</span><span class="sxs-lookup"><span data-stu-id="288dd-255">`hive` command from remote desktop</span></span> |<span data-ttu-id="288dd-256">使用 [Beeline](hdinsight-hadoop-use-hive-beeline.md) 或是[來自 SSH 工作階段的 Hive](hdinsight-hadoop-use-hive-ssh.md)</span><span class="sxs-lookup"><span data-stu-id="288dd-256">Use [Beeline](hdinsight-hadoop-use-hive-beeline.md) or [Hive from an SSH session](hdinsight-hadoop-use-hive-ssh.md)</span></span> |

### <a name="pig"></a><span data-ttu-id="288dd-257">Pig</span><span class="sxs-lookup"><span data-stu-id="288dd-257">Pig</span></span>

| <span data-ttu-id="288dd-258">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="288dd-258">On Windows-based, I use...</span></span> | <span data-ttu-id="288dd-259">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="288dd-259">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="288dd-260">C# 使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="288dd-260">C# user-defined functions</span></span> | <span data-ttu-id="288dd-261">驗證 C# 元件，以 Linux 為基礎的 HDInsight 上的資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="288dd-261">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="288dd-262">CMD 檔案或 hello 叫用 Pig 工作的一部分的伺服器上的指令碼</span><span class="sxs-lookup"><span data-stu-id="288dd-262">CMD files or scripts on hello server invoked as part of a Pig job</span></span> |<span data-ttu-id="288dd-263">使用 Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="288dd-263">use Bash scripts</span></span> |

### <a name="mapreduce"></a><span data-ttu-id="288dd-264">MapReduce</span><span class="sxs-lookup"><span data-stu-id="288dd-264">MapReduce</span></span>

| <span data-ttu-id="288dd-265">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="288dd-265">On Windows-based, I use...</span></span> | <span data-ttu-id="288dd-266">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="288dd-266">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="288dd-267">C# 對應器和歸納器元件</span><span class="sxs-lookup"><span data-stu-id="288dd-267">C# mapper and reducer components</span></span> | <span data-ttu-id="288dd-268">驗證 C# 元件，以 Linux 為基礎的 HDInsight 上的資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="288dd-268">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="288dd-269">CMD 檔案或登錄區工作的一部分叫用的 hello 伺服器上的指令碼</span><span class="sxs-lookup"><span data-stu-id="288dd-269">CMD files or scripts on hello server invoked as part of a Hive job</span></span> |<span data-ttu-id="288dd-270">使用 Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="288dd-270">use Bash scripts</span></span> |

## <a name="oozie"></a><span data-ttu-id="288dd-271">Oozie</span><span class="sxs-lookup"><span data-stu-id="288dd-271">Oozie</span></span>

> [!IMPORTANT]
> <span data-ttu-id="288dd-272">如果您使用外部的 Oozie 中繼存放區，您應該備份之前使用 linux 的 HDInsight hello 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="288dd-272">If you use an external Oozie metastore, you should back up hello metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="288dd-273">以 Linux 為基礎的 HDInsight 可搭配較新版本的 Oozie 使用，但可能會與舊版建立的中繼存放區不相容。</span><span class="sxs-lookup"><span data-stu-id="288dd-273">Linux-based HDInsight is available with newer versions of Oozie, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="288dd-274">Oozie 工作流程允許殼層動作。</span><span class="sxs-lookup"><span data-stu-id="288dd-274">Oozie workflows allow shell actions.</span></span> <span data-ttu-id="288dd-275">殼層動作會使用 hello 預設殼層的 hello 作業系統 toorun 命令列命令。</span><span class="sxs-lookup"><span data-stu-id="288dd-275">Shell actions use hello default shell for hello operating system toorun command-line commands.</span></span> <span data-ttu-id="288dd-276">如果您擁有 hello Windows shell 所依賴的 Oozie 工作流程時，您必須重新撰寫 hello 工作流程 toorely hello Linux shell 環境 (Bash)。</span><span class="sxs-lookup"><span data-stu-id="288dd-276">If you have Oozie workflows that rely on hello Windows shell, you must rewrite hello workflows toorely on hello Linux shell environment (Bash).</span></span> <span data-ttu-id="288dd-277">如需使用 Oozie 殼層動作的詳細資訊，請參閱 [Oozie 殼層動作擴充功能](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html)。</span><span class="sxs-lookup"><span data-stu-id="288dd-277">For more information on using shell actions with Oozie, see [Oozie shell action extension](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).</span></span>

<span data-ttu-id="288dd-278">如果您有依賴 C# 應用程式 (透過殼層動作叫用) 的 Oozie 工作流程，您必須在 Linux 環境中驗證這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="288dd-278">If you have Oozie workflows that rely on C# applications invoked through shell actions, you must validate these applications in a Linux environment.</span></span> <span data-ttu-id="288dd-279">如需詳細資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-279">For more information, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="storm"></a><span data-ttu-id="288dd-280">Storm</span><span class="sxs-lookup"><span data-stu-id="288dd-280">Storm</span></span>

| <span data-ttu-id="288dd-281">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="288dd-281">On Windows-based, I use...</span></span> | <span data-ttu-id="288dd-282">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="288dd-282">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="288dd-283">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="288dd-283">Storm Dashboard</span></span> |<span data-ttu-id="288dd-284">hello Storm 儀表板就無法使用。</span><span class="sxs-lookup"><span data-stu-id="288dd-284">hello Storm Dashboard is not available.</span></span> <span data-ttu-id="288dd-285">請參閱[以 Linux 為基礎的 HDInsight 上的部署和管理 Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)方式 toosubmit 拓撲</span><span class="sxs-lookup"><span data-stu-id="288dd-285">See [Deploy and Manage Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) for ways toosubmit topologies</span></span> |
| <span data-ttu-id="288dd-286">Storm UI</span><span class="sxs-lookup"><span data-stu-id="288dd-286">Storm UI</span></span> |<span data-ttu-id="288dd-287">hello Storm UI 位於 https://CLUSTERNAME.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="288dd-287">hello Storm UI is available at https://CLUSTERNAME.azurehdinsight.net/stormui</span></span> |
| <span data-ttu-id="288dd-288">Visual Studio toocreate，部署和管理 C# 或混合式拓撲</span><span class="sxs-lookup"><span data-stu-id="288dd-288">Visual Studio toocreate, deploy, and manage C# or hybrid topologies</span></span> |<span data-ttu-id="288dd-289">Visual Studio 可以是使用的 toocreate、 部署和管理 C# (SCP.NET) 或 2016 年 10 月 28 之後建立的 HDInsight 叢集上的 linux Storm 上的混合式拓撲。</span><span class="sxs-lookup"><span data-stu-id="288dd-289">Visual Studio can be used toocreate, deploy, and manage C# (SCP.NET) or hybrid topologies on Linux-based Storm on HDInsight clusters created after 10/28/2016.</span></span> |

## <a name="hbase"></a><span data-ttu-id="288dd-290">HBase</span><span class="sxs-lookup"><span data-stu-id="288dd-290">HBase</span></span>

<span data-ttu-id="288dd-291">以 Linux 為基礎的叢集上 HBase hello znode 父系是`/hbase-unsecure`。</span><span class="sxs-lookup"><span data-stu-id="288dd-291">On Linux-based clusters, hello znode parent for HBase is `/hbase-unsecure`.</span></span> <span data-ttu-id="288dd-292">使用原生 HBase Java 應用程式開發介面的任何 Java 用戶端應用程式的 hello 組態中設定此值。</span><span class="sxs-lookup"><span data-stu-id="288dd-292">Set this value in hello configuration for any Java client applications that use native HBase Java API.</span></span>

<span data-ttu-id="288dd-293">如需設定此值的範例用戶端，請參閱 [建置以 Java 為基礎的 HBase 應用程式](hdinsight-hbase-build-java-maven.md) 。</span><span class="sxs-lookup"><span data-stu-id="288dd-293">See [Build a Java-based HBase application](hdinsight-hbase-build-java-maven.md) for an example client that sets this value.</span></span>

## <a name="spark"></a><span data-ttu-id="288dd-294">Spark</span><span class="sxs-lookup"><span data-stu-id="288dd-294">Spark</span></span>

<span data-ttu-id="288dd-295">Spark 叢集可以在 Windows 叢集預覽期間取得。</span><span class="sxs-lookup"><span data-stu-id="288dd-295">Spark clusters were available on Windows-clusters during preview.</span></span> <span data-ttu-id="288dd-296">Spark GA 只適用於以 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-296">Spark GA is only available with Linux-based clusters.</span></span> <span data-ttu-id="288dd-297">沒有從 Windows 型的 Spark 預覽叢集 tooa 版本以 Linux 為基礎的 Spark 叢集移轉路徑。</span><span class="sxs-lookup"><span data-stu-id="288dd-297">There is no migration path from a Windows-based Spark preview cluster tooa release Linux-based Spark cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="288dd-298">已知問題</span><span class="sxs-lookup"><span data-stu-id="288dd-298">Known issues</span></span>

### <a name="azure-data-factory-custom-net-activities"></a><span data-ttu-id="288dd-299">Azure Data Factory 自訂 .NET 活動</span><span class="sxs-lookup"><span data-stu-id="288dd-299">Azure Data Factory custom .NET activities</span></span>

<span data-ttu-id="288dd-300">Azure Data Factory 自訂 .NET 活動目前並不受以 Linux 為基礎的 HDInsight 叢集所支援。</span><span class="sxs-lookup"><span data-stu-id="288dd-300">Azure Data Factory custom .NET activities are not currently supported on Linux-based HDInsight clusters.</span></span> <span data-ttu-id="288dd-301">相反地，您應該使用其中一個 hello 遵循方法 tooimplement 自訂活動做為 ADF 管線的一部分。</span><span class="sxs-lookup"><span data-stu-id="288dd-301">Instead, you should use one of hello following methods tooimplement custom activities as part of your ADF pipeline.</span></span>

* <span data-ttu-id="288dd-302">在 Azure Batch 集區上執行 .NET 活動。</span><span class="sxs-lookup"><span data-stu-id="288dd-302">Execute .NET activities on Azure Batch pool.</span></span> <span data-ttu-id="288dd-303">請參閱 hello 使用 Azure Batch 連結服務區段[Azure Data Factory 管線中使用自訂活動](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="288dd-303">See hello Use Azure Batch linked service section of [Use custom activities in an Azure Data Factory pipeline](../data-factory/data-factory-use-custom-activities.md)</span></span>
* <span data-ttu-id="288dd-304">實作 MapReduce 活動與 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="288dd-304">Implement hello activity as a MapReduce activity.</span></span> <span data-ttu-id="288dd-305">如需詳細資訊，請參閱[從 Data Factory 叫用 MapReduce 程式](../data-factory/data-factory-map-reduce.md)。</span><span class="sxs-lookup"><span data-stu-id="288dd-305">For more information, see [Invoke MapReduce Programs from Data Factory](../data-factory/data-factory-map-reduce.md).</span></span>

### <a name="line-endings"></a><span data-ttu-id="288dd-306">行尾結束符號</span><span class="sxs-lookup"><span data-stu-id="288dd-306">Line endings</span></span>

<span data-ttu-id="288dd-307">通常來說，以 Windows 為基礎之系統上的行尾結束符號是使用 CRLF，而以 Linux 為基礎的系統則使用 LF。</span><span class="sxs-lookup"><span data-stu-id="288dd-307">In general, line endings on Windows-based systems use CRLF, while Linux-based systems use LF.</span></span> <span data-ttu-id="288dd-308">如果您產生，或預期的方式，與 CRLF 行尾結束符號的資料，您可能需要 toomodify hello 產生者或消費者 toowork 與 hello LF 行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="288dd-308">If you produce, or expect, data with CRLF line endings, you may need toomodify hello producers or consumers toowork with hello LF line ending.</span></span>

<span data-ttu-id="288dd-309">比方說，HDInsight 在 Windows 叢集上的使用 Azure PowerShell tooquery 傳回 CRLF 與資料。</span><span class="sxs-lookup"><span data-stu-id="288dd-309">For example, using Azure PowerShell tooquery HDInsight on a Windows-based cluster returns data with CRLF.</span></span> <span data-ttu-id="288dd-310">hello 與 linux 叢集的同一個查詢傳回 LF。</span><span class="sxs-lookup"><span data-stu-id="288dd-310">hello same query with a Linux-based cluster returns LF.</span></span> <span data-ttu-id="288dd-311">如果 hello 行尾結束符號會導致您 solutuion 問題移轉之前，您應該測試 toosee tooa linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-311">You should test toosee if hello line ending causes a problem with your solutuion before migrating tooa Linux-based cluster.</span></span>

<span data-ttu-id="288dd-312">如果您有直接在 hello Linux 叢集節點執行的指令碼，您應該一律使用 LF 為 hello 行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="288dd-312">If you have scripts that are executed directly on hello Linux-cluster nodes, you should always use LF as hello line ending.</span></span> <span data-ttu-id="288dd-313">如果您使用 CRLF，您可能以 Linux 為基礎的叢集上執行 hello 指令碼時發現錯誤。</span><span class="sxs-lookup"><span data-stu-id="288dd-313">If you use CRLF, you may see errors when running hello scripts on a Linux-based cluster.</span></span>

<span data-ttu-id="288dd-314">如果您知道 hello 指令碼不會包含具有內嵌 CR 字元的字串，您就可以大量變更 hello 行尾使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="288dd-314">If you know that hello scripts do not contain strings with embedded CR characters, you can bulk change hello line endings using one of hello following methods:</span></span>

* <span data-ttu-id="288dd-315">**上傳 toohello 叢集之前**： 使用 hello CRLF tooLF 中的下列 PowerShell 陳述式 toochange hello 行尾結束符號，再上傳 hello 指令碼 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="288dd-315">**Before uploading toohello cluster**: Use hello following PowerShell statements toochange hello line endings from CRLF tooLF before uploading hello script toohello cluster.</span></span>

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* <span data-ttu-id="288dd-316">**上傳 toohello 叢集後**： 使用 hello 下列命令從 SSH 工作階段 toohello linux 叢集 toomodify hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="288dd-316">**After uploading toohello cluster**: Use hello following command from an SSH session toohello Linux-based cluster toomodify hello script.</span></span>

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a><span data-ttu-id="288dd-317">後續步驟</span><span class="sxs-lookup"><span data-stu-id="288dd-317">Next Steps</span></span>

* [<span data-ttu-id="288dd-318">了解如何 toocreate 以 Linux 為基礎的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="288dd-318">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="288dd-319">使用 SSH tooconnect tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="288dd-319">Use SSH tooconnect tooHDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="288dd-320">使用 Ambari 管理 Linux 型叢集</span><span class="sxs-lookup"><span data-stu-id="288dd-320">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
