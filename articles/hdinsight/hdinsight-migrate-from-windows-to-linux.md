---
title: "從以 Windows 為基礎的 HDInsight 移轉至以 Linux 為基礎的 HDInsight - Azure | Microsoft Docs"
description: "了解如何從以 Windows 為基礎的 HDInsight 叢集移轉至以 Linux 為基礎的 HDInsight 叢集。"
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
ms.openlocfilehash: 35e80efe27081cd43243f488fa60447b76a20c32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-to-a-linux-based-cluster"></a><span data-ttu-id="c5706-103">從以 Windows 為基礎的 HDInsight 叢集移轉至以 Linux 為基礎的叢集</span><span class="sxs-lookup"><span data-stu-id="c5706-103">Migrate from a Windows-based HDInsight cluster to a Linux-based cluster</span></span>

<span data-ttu-id="c5706-104">本文件提供 Windows 和 Linux 上 HDInsight 差異的詳細資料，以及如何將現有工作負載移轉至以 Linux 為基礎之叢集的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c5706-104">This document provides details on the differences between HDInsight on Windows and Linux, and guidance on how to migrate existing workloads to a Linux-based cluster.</span></span>

<span data-ttu-id="c5706-105">儘管以 Windows 為基礎的 HDInsight 提供一種簡單方式來使用雲端中的 Hadoop，但您可能需要移轉到以 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-105">While Windows-based HDInsight provides an easy way to use Hadoop in the cloud, you may need to migrate to a Linux-based cluster.</span></span> <span data-ttu-id="c5706-106">例如，充分利用您解決方案所需且以 Linux 為基礎的工具和技術。</span><span class="sxs-lookup"><span data-stu-id="c5706-106">For example, to take advantage of Linux-based tools and technologies that are required for your solution.</span></span> <span data-ttu-id="c5706-107">Hadoop 生態系統的許多內容都是在以 Linux 為基礎的系統上開發，因此可能無法與以 Windows 為基礎的 HDInsight 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c5706-107">Many things in the Hadoop ecosystem are developed on Linux-based systems, and may not be available for use with Windows-based HDInsight.</span></span> <span data-ttu-id="c5706-108">除此之外，許多針對 Hadoop 的書籍、影片及其他訓練材料，都會假設您正在使用 Linux 系統。</span><span class="sxs-lookup"><span data-stu-id="c5706-108">Additionally, many books, videos, and other training material assume that you are using a Linux system when working with Hadoop.</span></span>

> [!NOTE]
> <span data-ttu-id="c5706-109">HDInsight 叢集使用 Ubuntu 長期支援 (LTS) 做為叢集中節點的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c5706-109">HDInsight clusters use Ubuntu long-term support (LTS) as the operating system for the nodes in the cluster.</span></span> <span data-ttu-id="c5706-110">如需 HDInsight 中可用 Ubuntu 版本的相關資訊以及其他元件版本設定資訊，請參閱 [HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-110">For information on the version of Ubuntu available with HDInsight, along with other component versioning information, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="migration-tasks"></a><span data-ttu-id="c5706-111">移轉工作</span><span class="sxs-lookup"><span data-stu-id="c5706-111">Migration tasks</span></span>

<span data-ttu-id="c5706-112">下列為移轉的一般工作流程。</span><span class="sxs-lookup"><span data-stu-id="c5706-112">The general workflow for migration is as follows.</span></span>

![移轉工作流程圖表](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. <span data-ttu-id="c5706-114">閱讀本文件的每個區段，來了解在將現有工作負載及工作等項目移轉至以 Linux 為基礎的叢集時，可能需要進行的變更。</span><span class="sxs-lookup"><span data-stu-id="c5706-114">Read each section of this document to understand changes that may be required when migrating your existing workflow, jobs, etc. to a Linux-based cluster.</span></span>

2. <span data-ttu-id="c5706-115">建立以 Linux 為基礎的叢集做為測試/品質保證環境。</span><span class="sxs-lookup"><span data-stu-id="c5706-115">Create a Linux-based cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="c5706-116">如需建立以 Linux 為基礎之叢集的詳細資訊，請參閱 [在 HDInsight 中建立以 Linux 為基礎的叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-116">For more information on creating a Linux-based cluster, see [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

3. <span data-ttu-id="c5706-117">將現有的作業、資料來源與接收複製到新的環境。</span><span class="sxs-lookup"><span data-stu-id="c5706-117">Copy existing jobs, data sources, and sinks to the new environment.</span></span>

4. <span data-ttu-id="c5706-118">執行驗證測試以確保您的工作在新叢集上會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="c5706-118">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>

<span data-ttu-id="c5706-119">當您已驗證一切都會如預期般運作之後，請為移轉排定停機時間。</span><span class="sxs-lookup"><span data-stu-id="c5706-119">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="c5706-120">在停機期間，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c5706-120">During this downtime, perform the following actions:</span></span>

1. <span data-ttu-id="c5706-121">備份所有儲存在本機叢集節點上的暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="c5706-121">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="c5706-122">例如，如果您的資料是直接儲存在前端節點上。</span><span class="sxs-lookup"><span data-stu-id="c5706-122">For example, if you have data stored directly on a head node.</span></span>

2. <span data-ttu-id="c5706-123">刪除以 Windows 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-123">Delete the Windows-based cluster.</span></span>

3. <span data-ttu-id="c5706-124">使用和以 Windows 為基礎之叢集所使用的相同預設資料存放區，建立以 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-124">Create a Linux-based cluster using the same default data store that the Windows-based cluster used.</span></span> <span data-ttu-id="c5706-125">以 Linux 為基礎的叢集可以針對現有的生產資料繼續運作。</span><span class="sxs-lookup"><span data-stu-id="c5706-125">The Linux-based cluster can continue working against your existing production data.</span></span>

4. <span data-ttu-id="c5706-126">匯入任何已備份的暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="c5706-126">Import any transient data you backed up.</span></span>

5. <span data-ttu-id="c5706-127">使用新叢集啟動工作/繼續處理。</span><span class="sxs-lookup"><span data-stu-id="c5706-127">Start jobs/continue processing using the new cluster.</span></span>

### <a name="copy-data-to-the-test-environment"></a><span data-ttu-id="c5706-128">將資料複製到測試環境</span><span class="sxs-lookup"><span data-stu-id="c5706-128">Copy data to the test environment</span></span>

<span data-ttu-id="c5706-129">雖然複製資料和工作的方法有很多，但是本區段所討論的兩個方法，是將檔案直接移至測試叢集最簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="c5706-129">There are many methods to copy the data and jobs, however the two discussed in this section are the simplest methods to directly move files to a test cluster.</span></span>

#### <a name="hdfs-copy"></a><span data-ttu-id="c5706-130">HDFS 複製</span><span class="sxs-lookup"><span data-stu-id="c5706-130">HDFS copy</span></span>

<span data-ttu-id="c5706-131">使用下列步驟，將資料從生產環境叢集複製到測試叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-131">Use the following steps to copy data from the production cluster to the test cluster.</span></span> <span data-ttu-id="c5706-132">這些步驟使用 HDInsight 隨附的 `hdfs dfs` 公用程式。</span><span class="sxs-lookup"><span data-stu-id="c5706-132">These steps use the `hdfs dfs` utility that is included with HDInsight.</span></span>

1. <span data-ttu-id="c5706-133">尋找現有叢集的儲存體帳戶和預設容器資訊。</span><span class="sxs-lookup"><span data-stu-id="c5706-133">Find the storage account and default container information for your existing cluster.</span></span> <span data-ttu-id="c5706-134">下列範例使用 PowerShell 來擷取此資訊：</span><span class="sxs-lookup"><span data-stu-id="c5706-134">The following example uses PowerShell to retrieve this information:</span></span>

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. <span data-ttu-id="c5706-135">若要建立測試環境，請依照＜在 HDInsight 中建立以 Linux 為基礎的叢集＞文件中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="c5706-135">To create a test environment, follow the steps in the Create Linux-based clusters in HDInsight document.</span></span> <span data-ttu-id="c5706-136">於建立叢集之前停止遵循步驟，並改為選取 [選擇性組態] 。</span><span class="sxs-lookup"><span data-stu-id="c5706-136">Stop before creating the cluster, and instead select **Optional Configuration**.</span></span>

3. <span data-ttu-id="c5706-137">從 [選擇性組態] 刀鋒視窗中，選取 [連結的儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="c5706-137">From the Optional Configuration blade, select **Linked Storage Accounts**.</span></span>

4. <span data-ttu-id="c5706-138">選取 [新增儲存體金鑰] ，並在出現提示時，選取步驟 1 中由 PowerShell 指令碼傳回的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5706-138">Select **Add a storage key**, and when prompted, select the storage account that was returned by the PowerShell script in step 1.</span></span> <span data-ttu-id="c5706-139">在每個刀鋒視窗上按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="c5706-139">Click **Select** on each blade.</span></span> <span data-ttu-id="c5706-140">最後，建立叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-140">Finally, create the cluster.</span></span>

5. <span data-ttu-id="c5706-141">建立叢集之後，使用 **SSH** 來連線至該叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-141">Once the cluster has been created, connect to it using **SSH.**</span></span> <span data-ttu-id="c5706-142">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-142">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

6. <span data-ttu-id="c5706-143">從 SSH 工作階段中，使用下列命令來將檔案從已連結的儲存體帳戶複製到新的預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5706-143">From the SSH session, use the following command to copy files from the linked storage account to the new default storage account.</span></span> <span data-ttu-id="c5706-144">使用 PowerShell 傳回的容器資訊來取代 CONTAINER。</span><span class="sxs-lookup"><span data-stu-id="c5706-144">Replace CONTAINER with the container information returned by PowerShell.</span></span> <span data-ttu-id="c5706-145">使用帳戶名稱來取代 __ACCOUNT__。</span><span class="sxs-lookup"><span data-stu-id="c5706-145">Replace __ACCOUNT__ with the account name.</span></span> <span data-ttu-id="c5706-146">將資料路徑取代為資料檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="c5706-146">Replace the path to data with the path to a data file.</span></span>

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > <span data-ttu-id="c5706-147">如果包含資料的目錄結構不存在於測試環境，您可以使用下列命令建立它：</span><span class="sxs-lookup"><span data-stu-id="c5706-147">If the directory structure that contains the data does not exist on the test environment, you can create it using the following command:</span></span>

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    <span data-ttu-id="c5706-148">`-p` 參數可讓您在路徑中建立所有目錄。</span><span class="sxs-lookup"><span data-stu-id="c5706-148">The `-p` switch enables the creation of all directories in  the path.</span></span>

#### <a name="direct-copy-between-blobs-in-azure-storage"></a><span data-ttu-id="c5706-149">在 Azure 儲存體中的 Blob 之間直接複製</span><span class="sxs-lookup"><span data-stu-id="c5706-149">Direct copy between blobs in Azure Storage</span></span>

<span data-ttu-id="c5706-150">此外，您也可能會想要使用 `Start-AzureStorageBlobCopy` Azure PowerShell Cmdlet 在 HDInsight 之外的儲存體帳戶之間複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="c5706-150">Alternatively, you may want to use the `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet to copy blobs between storage accounts outside of HDInsight.</span></span> <span data-ttu-id="c5706-151">如需詳細資訊，請參閱＜搭配使用 Azure PowerShell 與 Azure 儲存體＞一文中的＜如何管理 Azure Blob＞一節。</span><span class="sxs-lookup"><span data-stu-id="c5706-151">For more information, see the How to manage Azure Blobs section of Using Azure PowerShell with Azure Storage.</span></span>

## <a name="client-side-technologies"></a><span data-ttu-id="c5706-152">用戶端技術</span><span class="sxs-lookup"><span data-stu-id="c5706-152">Client-side technologies</span></span>

<span data-ttu-id="c5706-153">[Azure PowerShell Cmdlet](/powershell/azureps-cmdlets-docs)、[Azure CLI](../cli-install-nodejs.md) 或 [.NET SDK for Hadoop](https://hadoopsdk.codeplex.com/) 之類的用戶端技術會繼續使用以 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-153">Client-side technologies such as [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), or the [.NET SDK for Hadoop](https://hadoopsdk.codeplex.com/) continue to work Linux-based clusters.</span></span> <span data-ttu-id="c5706-154">這些依賴 REST API 的技術在兩種叢集作業系統類型上都相同。</span><span class="sxs-lookup"><span data-stu-id="c5706-154">These technologies rely on REST APIs that are the same across both cluster OS types.</span></span>

## <a name="server-side-technologies"></a><span data-ttu-id="c5706-155">伺服器端技術</span><span class="sxs-lookup"><span data-stu-id="c5706-155">Server-side technologies</span></span>

<span data-ttu-id="c5706-156">下表提供移轉 Windows 特定之伺服器端元件的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c5706-156">The following table provides guidance on migrating server-side components that are Windows-specific.</span></span>

| <span data-ttu-id="c5706-157">如果您正在使用這項技術...</span><span class="sxs-lookup"><span data-stu-id="c5706-157">If you are using this technology...</span></span> | <span data-ttu-id="c5706-158">請執行此動作...</span><span class="sxs-lookup"><span data-stu-id="c5706-158">Take this action...</span></span> |
| --- | --- |
| <span data-ttu-id="c5706-159">**PowerShell** (伺服器端指令碼，包含於叢集建立期間使用的指令碼動作)</span><span class="sxs-lookup"><span data-stu-id="c5706-159">**PowerShell** (server-side scripts, including Script Actions used during cluster creation)</span></span> |<span data-ttu-id="c5706-160">重寫為 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c5706-160">Rewrite as Bash scripts.</span></span> <span data-ttu-id="c5706-161">針對指令碼動作，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)和[以 Linux 為基礎之 HDInsight 的指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-161">For Script Actions, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span> |
| <span data-ttu-id="c5706-162">**Azure CLI** (伺服器端指令碼)</span><span class="sxs-lookup"><span data-stu-id="c5706-162">**Azure CLI** (server-side scripts)</span></span> |<span data-ttu-id="c5706-163">雖然 Azure CLI 可在 Linux 上使用，它並沒有預先安裝在 HDInsight 叢集前端節點上。</span><span class="sxs-lookup"><span data-stu-id="c5706-163">While the Azure CLI is available on Linux, it does not come pre-installed on the HDInsight cluster head nodes.</span></span> <span data-ttu-id="c5706-164">如需有關安裝 Azure CLI 的詳細資訊，請參閱[開始使用 Azure CLI 2.0 (英文)](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="c5706-164">For more information on installing the Azure CLI, see [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span> |
| <span data-ttu-id="c5706-165">**.NET 元件**</span><span class="sxs-lookup"><span data-stu-id="c5706-165">**.NET components**</span></span> |<span data-ttu-id="c5706-166">以 Linux 為基礎的 HDInsight 透過 [Mono](https://mono-project.com) 支援 .NET。</span><span class="sxs-lookup"><span data-stu-id="c5706-166">.NET is supported on Linux-based HDInsight through [Mono](https://mono-project.com).</span></span> <span data-ttu-id="c5706-167">如需詳細資訊，請參閱[將 .NET 方案移轉至以 Linux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-167">For more information, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span> |
| <span data-ttu-id="c5706-168">**Win32 元件或其他僅限 Windows 的技術**</span><span class="sxs-lookup"><span data-stu-id="c5706-168">**Win32 components or other Windows-only technology**</span></span> |<span data-ttu-id="c5706-169">指導方針將視元件或技術而有所不同。</span><span class="sxs-lookup"><span data-stu-id="c5706-169">Guidance depends on the component or technology.</span></span> <span data-ttu-id="c5706-170">您或許能夠找到與 Linux 相容的版本，也可能需要尋找替代的解決方案，或是重寫此元件。</span><span class="sxs-lookup"><span data-stu-id="c5706-170">You may be able to find a version that is compatible with Linux, or you may need to find an alternate solution or rewrite this component.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c5706-171">HDInsight 管理 SDK 不完全相容 Mono。</span><span class="sxs-lookup"><span data-stu-id="c5706-171">The HDInsight management SDK is not fully compatible with Mono.</span></span> <span data-ttu-id="c5706-172">目前它不應該作為部署至 HDInsight 叢集方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="c5706-172">It should not be used as part of solutions deployed to the HDInsight cluster at this time.</span></span>

## <a name="cluster-creation"></a><span data-ttu-id="c5706-173">叢集建立</span><span class="sxs-lookup"><span data-stu-id="c5706-173">Cluster creation</span></span>

<span data-ttu-id="c5706-174">本節將提供叢集建立之差異的資訊。</span><span class="sxs-lookup"><span data-stu-id="c5706-174">This section provides information on differences in cluster creation.</span></span>

### <a name="ssh-user"></a><span data-ttu-id="c5706-175">SSH 使用者</span><span class="sxs-lookup"><span data-stu-id="c5706-175">SSH User</span></span>

<span data-ttu-id="c5706-176">以 Linux 為基礎的 HDInsight 是使用 **安全殼層 (SSH)** 通訊協定來為叢集節點提供遠端存取功能。</span><span class="sxs-lookup"><span data-stu-id="c5706-176">Linux-based HDInsight clusters use the **Secure Shell (SSH)** protocol to provide remote access to the cluster nodes.</span></span> <span data-ttu-id="c5706-177">不同於以 Windows 為基礎之叢集的遠端桌面，大部分的 SSH 用戶端不提供圖形化使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="c5706-177">Unlike Remote Desktop for Windows-based clusters, most SSH clients do not provide a graphical user experience.</span></span> <span data-ttu-id="c5706-178">SSH 用戶端改為提供命令列，讓您在叢集上執行命令。</span><span class="sxs-lookup"><span data-stu-id="c5706-178">Instead, SSH clients provide a command line that allows you to run commands on the cluster.</span></span> <span data-ttu-id="c5706-179">某些用戶端 (例如 [MobaXterm](http://mobaxterm.mobatek.net/)) 除了提供遠端命令列之外，也提供圖形化檔案系統瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c5706-179">Some clients (such as [MobaXterm](http://mobaxterm.mobatek.net/)) provide a graphical file system browser in addition to a remote command line.</span></span>

<span data-ttu-id="c5706-180">在叢集建立期間，您必須提供 SSH 使用者，以及**密碼**或**公開金鑰憑證**以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="c5706-180">During cluster creation, you must provide an SSH user and either a **password** or **public key certificate** for authentication.</span></span>

<span data-ttu-id="c5706-181">我們建議使用公開金鑰憑證，因為它比密碼更安全。</span><span class="sxs-lookup"><span data-stu-id="c5706-181">We recommend using Public key certificate, as it is more secure than using a password.</span></span> <span data-ttu-id="c5706-182">憑證驗證會產生已簽署的公開/私人金鑰組，然後在建立叢集時提供公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="c5706-182">Certificate authentication works by generating a signed public/private key pair, then providing the public key when creating the cluster.</span></span> <span data-ttu-id="c5706-183">使用 SSH 連線至伺服器時，用戶端上的私人金鑰將會為連線提供驗證。</span><span class="sxs-lookup"><span data-stu-id="c5706-183">When connecting to the server using SSH, the private key on the client provides authentication for the connection.</span></span>

<span data-ttu-id="c5706-184">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-184">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="cluster-customization"></a><span data-ttu-id="c5706-185">叢集自訂</span><span class="sxs-lookup"><span data-stu-id="c5706-185">Cluster customization</span></span>

<span data-ttu-id="c5706-186">**指令碼動作** 必須以 Bash 指令碼撰寫。</span><span class="sxs-lookup"><span data-stu-id="c5706-186">**Script Actions** used with Linux-based clusters must be written in Bash script.</span></span> <span data-ttu-id="c5706-187">雖然指令碼動作可在叢集建立期間使用，它們也可以用來在以 Linux 為基礎之叢集已啟動並開始執行之後進行自訂。</span><span class="sxs-lookup"><span data-stu-id="c5706-187">While Script Actions can be used during cluster creation, for Linux-based clusters they can also be used to perform customization after a cluster is up and running.</span></span> <span data-ttu-id="c5706-188">如需詳細資訊，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)和[以 Linux 為基礎之 HDInsight 的指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-188">For more information, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

<span data-ttu-id="c5706-189">另一個自訂功能是 **bootstrap**。</span><span class="sxs-lookup"><span data-stu-id="c5706-189">Another customization feature is **bootstrap**.</span></span> <span data-ttu-id="c5706-190">針對 Windows 叢集，此功能可讓您指定其他搭配 Hive 使用之程式庫的位置。</span><span class="sxs-lookup"><span data-stu-id="c5706-190">For Windows clusters, this feature allows you to specify the location of additional libraries for use with Hive.</span></span> <span data-ttu-id="c5706-191">在叢集建立之後，這些程式庫將可自動搭配 Hive 查詢使用，而不需使用 `ADD JAR`。</span><span class="sxs-lookup"><span data-stu-id="c5706-191">After cluster creation, these libraries are automatically available for use with Hive queries without the need to use `ADD JAR`.</span></span>

<span data-ttu-id="c5706-192">針對以 Linux 為基礎的叢集，Bootstrap 功能不提供此功能。</span><span class="sxs-lookup"><span data-stu-id="c5706-192">The Bootstrap feature for Linux-based clusters does not provide this functionality.</span></span> <span data-ttu-id="c5706-193">請改為使用 [在叢集建立期間新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)中所記錄的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="c5706-193">Instead, use script action documented in [Add Hive libraries during cluster creation](hdinsight-hadoop-add-hive-libraries.md).</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="c5706-194">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c5706-194">Virtual Networks</span></span>

<span data-ttu-id="c5706-195">以 Windows 為基礎的 HDInsight 僅支援傳統虛擬網路，而以 Linux 為基礎的 HDInsight 則需要資源管理員虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c5706-195">Windows-based HDInsight clusters only work with Classic Virtual Networks, while Linux-based HDInsight clusters require Resource Manager Virtual Networks.</span></span> <span data-ttu-id="c5706-196">如果資源位於傳統虛擬網路中，且以 Linux 為基礎的 HDInsight 叢集必須連接到這類資源時，請參閱 [將傳統虛擬網路連接到 Resource Manager 虛擬網路](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-196">If you have resources in a Classic Virtual Network that the Linux-HDInsight cluster must connect to, see [Connecting a Classic Virtual Network to a Resource Manager Virtual Network](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

<span data-ttu-id="c5706-197">如需搭配 HDInsight 使用 Azure 虛擬網路之設定需求的詳細資訊，請參閱 [使用虛擬網路延伸 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-197">For more information on configuration requirements for using Azure Virtual Networks with HDInsight, see [Extend HDInsight capabilities by using a Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a name="management-and-monitoring"></a><span data-ttu-id="c5706-198">管理與監視</span><span class="sxs-lookup"><span data-stu-id="c5706-198">Management and monitoring</span></span>

<span data-ttu-id="c5706-199">有許多您可能曾搭配以 Windows 為基礎之 HDInsight 使用的 Web UI (例如工作歷程記錄或 Yarn UI)，皆可透過 Ambari 使用。</span><span class="sxs-lookup"><span data-stu-id="c5706-199">Many of the web UIs you may have used with Windows-based HDInsight, such as Job History or Yarn UI, are available through Ambari.</span></span> <span data-ttu-id="c5706-200">此外，Ambari Hive 檢視能提供使用您的網頁瀏覽器執行 Hive 查詢的方法。</span><span class="sxs-lookup"><span data-stu-id="c5706-200">In addition, the Ambari Hive View provides a way to run Hive queries using your web browser.</span></span> <span data-ttu-id="c5706-201">Ambari Web UI 可以在以 Linux 為基礎的叢集上使用，位於：https://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="c5706-201">The Ambari Web UI is available on Linux-based clusters at https://CLUSTERNAME.azurehdinsight.net.</span></span>

<span data-ttu-id="c5706-202">如需使用 Ambari 的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="c5706-202">For more information on working with Ambari, see the following documents:</span></span>

* [<span data-ttu-id="c5706-203">Ambari Web</span><span class="sxs-lookup"><span data-stu-id="c5706-203">Ambari Web</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="c5706-204">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="c5706-204">Ambari REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a><span data-ttu-id="c5706-205">Ambari 警示</span><span class="sxs-lookup"><span data-stu-id="c5706-205">Ambari Alerts</span></span>

<span data-ttu-id="c5706-206">Ambari 擁有能通知您叢集潛在問題的警示系統。</span><span class="sxs-lookup"><span data-stu-id="c5706-206">Ambari has an alert system that can tell you of potential problems with the cluster.</span></span> <span data-ttu-id="c5706-207">警示將會以紅色或黃色的項目出現在 Ambari Web UI 中，您也可以透過 REST API 擷取它們。</span><span class="sxs-lookup"><span data-stu-id="c5706-207">Alerts appear as red or yellow entries in the Ambari Web UI, however you can also retrieve them through the REST API.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5706-208">Ambari 警示代表「可能有」問題，而不表示「已發生」問題。</span><span class="sxs-lookup"><span data-stu-id="c5706-208">Ambari alerts indicate that there *may* be a problem, not that there *is* a problem.</span></span> <span data-ttu-id="c5706-209">例如，您可能會收到無法存取 HiveServer2 的警示，但實際上您仍然可以正常存取它。</span><span class="sxs-lookup"><span data-stu-id="c5706-209">For example, you may receive an alert that HiveServer2 cannot be accessed, even though you can access it normally.</span></span>
>
> <span data-ttu-id="c5706-210">許多警示都是針對某項服務實作為以間隔為基礎的查詢，並會預期在特定的時間範圍內收到回應。</span><span class="sxs-lookup"><span data-stu-id="c5706-210">Many alerts are implemented as interval-based queries against a service, and expect a response within a specific time frame.</span></span> <span data-ttu-id="c5706-211">因此警示本身並不代表服務已關閉，而只是單純表示該服務沒有在預期的時間範圍內傳回結果。</span><span class="sxs-lookup"><span data-stu-id="c5706-211">So the alert doesn't necessarily mean that the service is down, just that it didn't return results within the expected time frame.</span></span>

<span data-ttu-id="c5706-212">您應先評估某個警示是否已長時間持續發生，或者是否與使用者所回報的某個問題有關，再對它採取動作。</span><span class="sxs-lookup"><span data-stu-id="c5706-212">You should evaluate whether an alert has been occurring for an extended period, or mirrors user problems that have been reported before taking action on it.</span></span>

## <a name="file-system-locations"></a><span data-ttu-id="c5706-213">檔案系統位置</span><span class="sxs-lookup"><span data-stu-id="c5706-213">File system locations</span></span>

<span data-ttu-id="c5706-214">Linux 叢集檔案系統的展開方式和以 Windows 為基礎的 HDInsight 叢集不同。</span><span class="sxs-lookup"><span data-stu-id="c5706-214">The Linux cluster file system is laid out differently than Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c5706-215">使用下列表格來尋找常用的檔案。</span><span class="sxs-lookup"><span data-stu-id="c5706-215">Use the following table to find commonly used files.</span></span>

| <span data-ttu-id="c5706-216">我需要尋找...</span><span class="sxs-lookup"><span data-stu-id="c5706-216">I need to find...</span></span> | <span data-ttu-id="c5706-217">它位於...</span><span class="sxs-lookup"><span data-stu-id="c5706-217">It is located...</span></span> |
| --- | --- |
| <span data-ttu-id="c5706-218">組態</span><span class="sxs-lookup"><span data-stu-id="c5706-218">Configuration</span></span> |<span data-ttu-id="c5706-219">`/etc`。</span><span class="sxs-lookup"><span data-stu-id="c5706-219">`/etc`.</span></span> <span data-ttu-id="c5706-220">例如， `/etc/hadoop/conf/core-site.xml`</span><span class="sxs-lookup"><span data-stu-id="c5706-220">For example, `/etc/hadoop/conf/core-site.xml`</span></span> |
| <span data-ttu-id="c5706-221">記錄檔</span><span class="sxs-lookup"><span data-stu-id="c5706-221">Log files</span></span> |`/var/logs` |
| <span data-ttu-id="c5706-222">Hortonworks Data Platform (HDP)</span><span class="sxs-lookup"><span data-stu-id="c5706-222">Hortonworks Data Platform (HDP)</span></span> |<span data-ttu-id="c5706-223">`/usr/hdp`。此處有兩個目錄，一個是目前的 HDP 版本，另一個則是 `current`。</span><span class="sxs-lookup"><span data-stu-id="c5706-223">`/usr/hdp`.There are two directories located here, one that is the current HDP version and `current`.</span></span> <span data-ttu-id="c5706-224">`current` 目錄包含位於版本號碼目錄之檔案和目錄的符號連結。</span><span class="sxs-lookup"><span data-stu-id="c5706-224">The `current` directory contains symbolic links to files and directories located in the version number directory.</span></span> <span data-ttu-id="c5706-225">`current` 目錄的用途是讓您方便存取 HDP 檔案，因為版本號碼會在更新 HDP 版本時變更。</span><span class="sxs-lookup"><span data-stu-id="c5706-225">The `current` directory is provided as a convenient way of accessing HDP files since the version number changes as the HDP version is updated.</span></span> |
| <span data-ttu-id="c5706-226">hadoop-streaming.jar</span><span class="sxs-lookup"><span data-stu-id="c5706-226">hadoop-streaming.jar</span></span> |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

<span data-ttu-id="c5706-227">通常來說，如果您知道檔案的名稱，便可以使用下列來自 SSH 工作階段的命令來尋找檔案路徑：</span><span class="sxs-lookup"><span data-stu-id="c5706-227">In general, if you know the name of the file, you can use the following command from an SSH session to find the file path:</span></span>

    find / -name FILENAME 2>/dev/null

<span data-ttu-id="c5706-228">您也可以搭配檔案名稱使用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="c5706-228">You can also use wildcards with the file name.</span></span> <span data-ttu-id="c5706-229">例如，`find / -name *streaming*.jar 2>/dev/null` 會傳回任何檔案名稱包含 'streaming' 這個字的 jar 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="c5706-229">For example, `find / -name *streaming*.jar 2>/dev/null` returns the path to any jar files that contain the word 'streaming' as part of the file name.</span></span>

## <a name="hive-pig-and-mapreduce"></a><span data-ttu-id="c5706-230">Hive、Pig 及 MapReduce</span><span class="sxs-lookup"><span data-stu-id="c5706-230">Hive, Pig, and MapReduce</span></span>

<span data-ttu-id="c5706-231">Pig 和 MapReduce 工作負載在 Linux 為基礎的叢集上很相似。</span><span class="sxs-lookup"><span data-stu-id="c5706-231">Pig and MapReduce workloads are similar on Linux-based clusters.</span></span> <span data-ttu-id="c5706-232">不過，您可以使用較新版本的 Hadoop、Hive 和 Pig 建立以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-232">However, Linux-based HDInsight clusters can be created using newer versions of Hadoop, Hive, and Pig.</span></span> <span data-ttu-id="c5706-233">這些版本的差異可能會對您現有方案的運作方式造成變更。</span><span class="sxs-lookup"><span data-stu-id="c5706-233">These version differences may introduce changes in how your existing solutions function.</span></span> <span data-ttu-id="c5706-234">如需 HDInsight 包含之元件的版本詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-234">For more information on the versions of components included with HDInsight, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="c5706-235">以 Linux 為基礎的 HDInsight 不提供遠端桌面功能。</span><span class="sxs-lookup"><span data-stu-id="c5706-235">Linux-based HDInsight does not provide remote desktop functionality.</span></span> <span data-ttu-id="c5706-236">您可以改用 SSH 來遠端連線至叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="c5706-236">Instead, you can use SSH to remotely connect to the cluster head nodes.</span></span> <span data-ttu-id="c5706-237">如需詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="c5706-237">For more information, see the following documents:</span></span>

* [<span data-ttu-id="c5706-238">搭配 SSH 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="c5706-238">Use Hive with SSH</span></span>](hdinsight-hadoop-use-hive-ssh.md)
* [<span data-ttu-id="c5706-239">搭配 SSH 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="c5706-239">Use Pig with SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md)
* [<span data-ttu-id="c5706-240">搭配 SSH 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="c5706-240">Use MapReduce with SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a><span data-ttu-id="c5706-241">Hive</span><span class="sxs-lookup"><span data-stu-id="c5706-241">Hive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5706-242">如果您使用外部 Hive 中繼存放區，您應該先備份中繼存放區，然後才將它搭配以 Linux 為基礎的 HDInsight 使用。</span><span class="sxs-lookup"><span data-stu-id="c5706-242">If you use an external Hive metastore, you should back up the metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="c5706-243">以 Linux 為基礎的 HDInsight 可搭配較新版本的 Hive 使用，但可能會與舊版建立的中繼存放區不相容。</span><span class="sxs-lookup"><span data-stu-id="c5706-243">Linux-based HDInsight is available with newer versions of Hive, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="c5706-244">下列圖表提供移轉 Hive 工作負載的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c5706-244">The following chart provides guidance on migrating your Hive workloads.</span></span>

| <span data-ttu-id="c5706-245">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="c5706-245">On Windows-based, I use...</span></span> | <span data-ttu-id="c5706-246">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="c5706-246">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c5706-247">**Hive 編輯器**</span><span class="sxs-lookup"><span data-stu-id="c5706-247">**Hive Editor**</span></span> |[<span data-ttu-id="c5706-248">Ambari 中的 Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="c5706-248">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |
| <span data-ttu-id="c5706-249">`set hive.execution.engine=tez;` 以啟用 Tez</span><span class="sxs-lookup"><span data-stu-id="c5706-249">`set hive.execution.engine=tez;` to enable Tez</span></span> |<span data-ttu-id="c5706-250">Tez 是以 Linux 為基礎之叢集的預設執行引擎，因此已不再需要 SET 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c5706-250">Tez is the default execution engine for Linux-based clusters, so the set statement is no longer needed.</span></span> |
| <span data-ttu-id="c5706-251">C# 使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="c5706-251">C# user-defined functions</span></span> | <span data-ttu-id="c5706-252">如需驗證以 Linux 為基礎之 HDInsight 的 C# 元件詳細資訊，請參閱[將 .NET 方案移轉至以 Linux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="c5706-252">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="c5706-253">伺服器上的 CMD 檔案或指令碼是做為 Hive 工作的一部分進行叫用</span><span class="sxs-lookup"><span data-stu-id="c5706-253">CMD files or scripts on the server invoked as part of a Hive job</span></span> |<span data-ttu-id="c5706-254">使用 Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="c5706-254">use Bash scripts</span></span> |
| <span data-ttu-id="c5706-255">`hive` 命令</span><span class="sxs-lookup"><span data-stu-id="c5706-255">`hive` command from remote desktop</span></span> |<span data-ttu-id="c5706-256">使用 [Beeline](hdinsight-hadoop-use-hive-beeline.md) 或是[來自 SSH 工作階段的 Hive](hdinsight-hadoop-use-hive-ssh.md)</span><span class="sxs-lookup"><span data-stu-id="c5706-256">Use [Beeline](hdinsight-hadoop-use-hive-beeline.md) or [Hive from an SSH session](hdinsight-hadoop-use-hive-ssh.md)</span></span> |

### <a name="pig"></a><span data-ttu-id="c5706-257">Pig</span><span class="sxs-lookup"><span data-stu-id="c5706-257">Pig</span></span>

| <span data-ttu-id="c5706-258">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="c5706-258">On Windows-based, I use...</span></span> | <span data-ttu-id="c5706-259">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="c5706-259">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c5706-260">C# 使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="c5706-260">C# user-defined functions</span></span> | <span data-ttu-id="c5706-261">如需驗證以 Linux 為基礎之 HDInsight 的 C# 元件詳細資訊，請參閱[將 .NET 方案移轉至以 Linux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="c5706-261">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="c5706-262">伺服器上的 CMD 檔案或指令碼是做為 Pig 作業的一部分叫用</span><span class="sxs-lookup"><span data-stu-id="c5706-262">CMD files or scripts on the server invoked as part of a Pig job</span></span> |<span data-ttu-id="c5706-263">使用 Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="c5706-263">use Bash scripts</span></span> |

### <a name="mapreduce"></a><span data-ttu-id="c5706-264">MapReduce</span><span class="sxs-lookup"><span data-stu-id="c5706-264">MapReduce</span></span>

| <span data-ttu-id="c5706-265">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="c5706-265">On Windows-based, I use...</span></span> | <span data-ttu-id="c5706-266">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="c5706-266">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c5706-267">C# 對應器和歸納器元件</span><span class="sxs-lookup"><span data-stu-id="c5706-267">C# mapper and reducer components</span></span> | <span data-ttu-id="c5706-268">如需驗證以 Linux 為基礎之 HDInsight 的 C# 元件詳細資訊，請參閱[將 .NET 方案移轉至以 Linux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="c5706-268">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="c5706-269">伺服器上的 CMD 檔案或指令碼是做為 Hive 工作的一部分進行叫用</span><span class="sxs-lookup"><span data-stu-id="c5706-269">CMD files or scripts on the server invoked as part of a Hive job</span></span> |<span data-ttu-id="c5706-270">使用 Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="c5706-270">use Bash scripts</span></span> |

## <a name="oozie"></a><span data-ttu-id="c5706-271">Oozie</span><span class="sxs-lookup"><span data-stu-id="c5706-271">Oozie</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5706-272">如果您使用外部 Oozie 中繼存放區，您應該先備份中繼存放區，然後才將它搭配以 Linux 為基礎的 HDInsight 使用。</span><span class="sxs-lookup"><span data-stu-id="c5706-272">If you use an external Oozie metastore, you should back up the metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="c5706-273">以 Linux 為基礎的 HDInsight 可搭配較新版本的 Oozie 使用，但可能會與舊版建立的中繼存放區不相容。</span><span class="sxs-lookup"><span data-stu-id="c5706-273">Linux-based HDInsight is available with newer versions of Oozie, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="c5706-274">Oozie 工作流程允許殼層動作。</span><span class="sxs-lookup"><span data-stu-id="c5706-274">Oozie workflows allow shell actions.</span></span> <span data-ttu-id="c5706-275">殼層動作會使用作業系統的預設殼層來執行命令列命令。</span><span class="sxs-lookup"><span data-stu-id="c5706-275">Shell actions use the default shell for the operating system to run command-line commands.</span></span> <span data-ttu-id="c5706-276">如果您有依賴 Windows 殼層的 Oozie 工作流程，您必須重新撰寫工作流程，以依賴 Linux 殼層環境 (Bash)。</span><span class="sxs-lookup"><span data-stu-id="c5706-276">If you have Oozie workflows that rely on the Windows shell, you must rewrite the workflows to rely on the Linux shell environment (Bash).</span></span> <span data-ttu-id="c5706-277">如需使用 Oozie 殼層動作的詳細資訊，請參閱 [Oozie 殼層動作擴充功能](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html)。</span><span class="sxs-lookup"><span data-stu-id="c5706-277">For more information on using shell actions with Oozie, see [Oozie shell action extension](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).</span></span>

<span data-ttu-id="c5706-278">如果您有依賴 C# 應用程式 (透過殼層動作叫用) 的 Oozie 工作流程，您必須在 Linux 環境中驗證這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5706-278">If you have Oozie workflows that rely on C# applications invoked through shell actions, you must validate these applications in a Linux environment.</span></span> <span data-ttu-id="c5706-279">如需詳細資訊，請參閱[將 .NET 方案移轉至以 Linux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-279">For more information, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="storm"></a><span data-ttu-id="c5706-280">Storm</span><span class="sxs-lookup"><span data-stu-id="c5706-280">Storm</span></span>

| <span data-ttu-id="c5706-281">以 Windows 為基礎時，我是使用...</span><span class="sxs-lookup"><span data-stu-id="c5706-281">On Windows-based, I use...</span></span> | <span data-ttu-id="c5706-282">以 Linux 為基礎時...</span><span class="sxs-lookup"><span data-stu-id="c5706-282">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c5706-283">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="c5706-283">Storm Dashboard</span></span> |<span data-ttu-id="c5706-284">無法使用 Storm Dashboard。</span><span class="sxs-lookup"><span data-stu-id="c5706-284">The Storm Dashboard is not available.</span></span> <span data-ttu-id="c5706-285">請參閱 [在以 Linux 為基礎的 HDInsight 上部署與管理 Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md) ，以了解提交拓撲的方法。</span><span class="sxs-lookup"><span data-stu-id="c5706-285">See [Deploy and Manage Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) for ways to submit topologies</span></span> |
| <span data-ttu-id="c5706-286">Storm UI</span><span class="sxs-lookup"><span data-stu-id="c5706-286">Storm UI</span></span> |<span data-ttu-id="c5706-287">Storm UI 可以在 https://CLUSTERNAME.azurehdinsight.net/stormui 使用</span><span class="sxs-lookup"><span data-stu-id="c5706-287">The Storm UI is available at https://CLUSTERNAME.azurehdinsight.net/stormui</span></span> |
| <span data-ttu-id="c5706-288">Visual Studio 以建立、部署及管理 C# 或混合式拓撲</span><span class="sxs-lookup"><span data-stu-id="c5706-288">Visual Studio to create, deploy, and manage C# or hybrid topologies</span></span> |<span data-ttu-id="c5706-289">在 2016/10/28 後建立之以 Linux 為基礎的 Storm on HDInsight 叢集上，可以使用 Visual Studio 來建立、部署和管理 C# (SCP.NET) 或混合式拓撲。</span><span class="sxs-lookup"><span data-stu-id="c5706-289">Visual Studio can be used to create, deploy, and manage C# (SCP.NET) or hybrid topologies on Linux-based Storm on HDInsight clusters created after 10/28/2016.</span></span> |

## <a name="hbase"></a><span data-ttu-id="c5706-290">HBase</span><span class="sxs-lookup"><span data-stu-id="c5706-290">HBase</span></span>

<span data-ttu-id="c5706-291">在以 Linux 為基礎的叢集上，HBase 的 znode 父項目為 `/hbase-unsecure`。</span><span class="sxs-lookup"><span data-stu-id="c5706-291">On Linux-based clusters, the znode parent for HBase is `/hbase-unsecure`.</span></span> <span data-ttu-id="c5706-292">針對任何使用原生 HBase Java API 的 Java 用戶端應用程式，在組態中設定此值。</span><span class="sxs-lookup"><span data-stu-id="c5706-292">Set this value in the configuration for any Java client applications that use native HBase Java API.</span></span>

<span data-ttu-id="c5706-293">如需設定此值的範例用戶端，請參閱 [建置以 Java 為基礎的 HBase 應用程式](hdinsight-hbase-build-java-maven.md) 。</span><span class="sxs-lookup"><span data-stu-id="c5706-293">See [Build a Java-based HBase application](hdinsight-hbase-build-java-maven.md) for an example client that sets this value.</span></span>

## <a name="spark"></a><span data-ttu-id="c5706-294">Spark</span><span class="sxs-lookup"><span data-stu-id="c5706-294">Spark</span></span>

<span data-ttu-id="c5706-295">Spark 叢集可以在 Windows 叢集預覽期間取得。</span><span class="sxs-lookup"><span data-stu-id="c5706-295">Spark clusters were available on Windows-clusters during preview.</span></span> <span data-ttu-id="c5706-296">Spark GA 只適用於以 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-296">Spark GA is only available with Linux-based clusters.</span></span> <span data-ttu-id="c5706-297">以 Windows 為基礎的 Spark 預覽叢集和以 Linux 為基礎的 Spark 叢集之間並沒有移轉路徑。</span><span class="sxs-lookup"><span data-stu-id="c5706-297">There is no migration path from a Windows-based Spark preview cluster to a release Linux-based Spark cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c5706-298">已知問題</span><span class="sxs-lookup"><span data-stu-id="c5706-298">Known issues</span></span>

### <a name="azure-data-factory-custom-net-activities"></a><span data-ttu-id="c5706-299">Azure Data Factory 自訂 .NET 活動</span><span class="sxs-lookup"><span data-stu-id="c5706-299">Azure Data Factory custom .NET activities</span></span>

<span data-ttu-id="c5706-300">Azure Data Factory 自訂 .NET 活動目前並不受以 Linux 為基礎的 HDInsight 叢集所支援。</span><span class="sxs-lookup"><span data-stu-id="c5706-300">Azure Data Factory custom .NET activities are not currently supported on Linux-based HDInsight clusters.</span></span> <span data-ttu-id="c5706-301">您應該改為使用下列其中一個方法，來將自訂活動實作為 ADF 管線的一部分。</span><span class="sxs-lookup"><span data-stu-id="c5706-301">Instead, you should use one of the following methods to implement custom activities as part of your ADF pipeline.</span></span>

* <span data-ttu-id="c5706-302">在 Azure Batch 集區上執行 .NET 活動。</span><span class="sxs-lookup"><span data-stu-id="c5706-302">Execute .NET activities on Azure Batch pool.</span></span> <span data-ttu-id="c5706-303">請參閱 [在 Azure Data Factory 管線中使用自訂活動](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="c5706-303">See the Use Azure Batch linked service section of [Use custom activities in an Azure Data Factory pipeline](../data-factory/data-factory-use-custom-activities.md)</span></span>
* <span data-ttu-id="c5706-304">將活動實作為 MapReduce 活動。</span><span class="sxs-lookup"><span data-stu-id="c5706-304">Implement the activity as a MapReduce activity.</span></span> <span data-ttu-id="c5706-305">如需詳細資訊，請參閱[從 Data Factory 叫用 MapReduce 程式](../data-factory/data-factory-map-reduce.md)。</span><span class="sxs-lookup"><span data-stu-id="c5706-305">For more information, see [Invoke MapReduce Programs from Data Factory](../data-factory/data-factory-map-reduce.md).</span></span>

### <a name="line-endings"></a><span data-ttu-id="c5706-306">行尾結束符號</span><span class="sxs-lookup"><span data-stu-id="c5706-306">Line endings</span></span>

<span data-ttu-id="c5706-307">通常來說，以 Windows 為基礎之系統上的行尾結束符號是使用 CRLF，而以 Linux 為基礎的系統則使用 LF。</span><span class="sxs-lookup"><span data-stu-id="c5706-307">In general, line endings on Windows-based systems use CRLF, while Linux-based systems use LF.</span></span> <span data-ttu-id="c5706-308">如果您產生或預期擁有 CRLF 行尾結束符號的資料，便可能需要修改產生者或取用者來搭配 LF 行尾結束符號運作。</span><span class="sxs-lookup"><span data-stu-id="c5706-308">If you produce, or expect, data with CRLF line endings, you may need to modify the producers or consumers to work with the LF line ending.</span></span>

<span data-ttu-id="c5706-309">例如，使用 Azure PowerShell，在以 Windows 為基礎的叢集上查詢 HDInsight，會傳回擁有 CRLF 的資料。</span><span class="sxs-lookup"><span data-stu-id="c5706-309">For example, using Azure PowerShell to query HDInsight on a Windows-based cluster returns data with CRLF.</span></span> <span data-ttu-id="c5706-310">在以 Linux 為基礎的叢集上使用相同查詢，會傳回 LF。</span><span class="sxs-lookup"><span data-stu-id="c5706-310">The same query with a Linux-based cluster returns LF.</span></span> <span data-ttu-id="c5706-311">您應該先進行測試，查看行尾結束符號否會導致您的方案發生問題，再將它移轉到以 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="c5706-311">You should test to see if the line ending causes a problem with your solutuion before migrating to a Linux-based cluster.</span></span>

<span data-ttu-id="c5706-312">如果您的指令碼會直接在 Linux 叢集節點上執行，則您應一律使用 LF 做為行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="c5706-312">If you have scripts that are executed directly on the Linux-cluster nodes, you should always use LF as the line ending.</span></span> <span data-ttu-id="c5706-313">如果您使用 CRLF，便可能會在以 Linux 為基礎的叢集上執行指令碼時遭遇到錯誤。</span><span class="sxs-lookup"><span data-stu-id="c5706-313">If you use CRLF, you may see errors when running the scripts on a Linux-based cluster.</span></span>

<span data-ttu-id="c5706-314">如果您知道指令碼並沒有包含擁有內嵌 CR 字元的字串，您可以使用下列其中一種方法來大量變更行尾結束符號：</span><span class="sxs-lookup"><span data-stu-id="c5706-314">If you know that the scripts do not contain strings with embedded CR characters, you can bulk change the line endings using one of the following methods:</span></span>

* <span data-ttu-id="c5706-315">**上傳至叢集之前**：請在將指令碼上傳至叢集之前，使用下列 PowerShell 陳述式將行尾結束符號從 CRLF 變更為 LF。</span><span class="sxs-lookup"><span data-stu-id="c5706-315">**Before uploading to the cluster**: Use the following PowerShell statements to change the line endings from CRLF to LF before uploading the script to the cluster.</span></span>

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* <span data-ttu-id="c5706-316">**上傳至叢集之後**：請從以 Linux 為基礎之叢集的 SSH 工作階段使用下列命令來修改指令碼。</span><span class="sxs-lookup"><span data-stu-id="c5706-316">**After uploading to the cluster**: Use the following command from an SSH session to the Linux-based cluster to modify the script.</span></span>

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a><span data-ttu-id="c5706-317">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5706-317">Next Steps</span></span>

* [<span data-ttu-id="c5706-318">了解如何建立 Linux 型 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="c5706-318">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="c5706-319">使用 SSH 連線到 HDInsight</span><span class="sxs-lookup"><span data-stu-id="c5706-319">Use SSH to connect to HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="c5706-320">使用 Ambari 管理 Linux 型叢集</span><span class="sxs-lookup"><span data-stu-id="c5706-320">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
