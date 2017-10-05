---
title: "在 HDInsight 叢集建立期間新增 Hive 程式庫 - Azure | Microsoft Docs"
description: "了解如何在叢集建立期間將 Hive 程式庫 (jar 檔案) 新增至 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 3412864384961e8820d6700c1bf22a4cae64ba4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="d498f-103">建立 HDInsight 叢集時新增自訂 Hive 程式庫</span><span class="sxs-lookup"><span data-stu-id="d498f-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="d498f-104">如果您有與 HDInsight 上的 Hive 經常一起使用的程式庫，本文件包含在叢集建立期間使用指令碼動作來預先載入程式庫的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d498f-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="d498f-105">使用本文件步驟新增的程式庫在 Hive 中為全域可用 - 不需要使用 [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) 載入它們。</span><span class="sxs-lookup"><span data-stu-id="d498f-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="d498f-106">運作方式</span><span class="sxs-lookup"><span data-stu-id="d498f-106">How it works</span></span>

<span data-ttu-id="d498f-107">建立叢集時，您可以選擇性地指定指令碼動作，以便在建立叢集節點時在節點上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d498f-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="d498f-108">本文件中的指令碼接受單一參數，也就是包含要預先載入程式庫 (儲存為 jar 檔案) 的 WASB 位置。</span><span class="sxs-lookup"><span data-stu-id="d498f-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="d498f-109">叢集建立期間，指令碼會列舉檔案、將它們複製到前端和背景工作節點上的 `/usr/lib/customhivelibs/` 目錄，然後將它們加入至 `core-site.xml` 檔案中的 `hive.aux.jars.path` 屬性。</span><span class="sxs-lookup"><span data-stu-id="d498f-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="d498f-110">在以 Linux 為基礎的叢集上，它也會以檔案的位置來更新 `hive-env.sh` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d498f-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="d498f-111">使用本文中的指令碼動作可讓程式庫在下列案例中可供使用：</span><span class="sxs-lookup"><span data-stu-id="d498f-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="d498f-112">**以 Linux 為基礎的 HDInsight** - 使用 Hive 用戶端、**WebHCat** 和 **HiveServer2** 時。</span><span class="sxs-lookup"><span data-stu-id="d498f-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="d498f-113">**以 Windows 為基礎的 HDInsight** - 使用 Hive 用戶端和 **WebHCat** 時。</span><span class="sxs-lookup"><span data-stu-id="d498f-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="d498f-114">指令碼</span><span class="sxs-lookup"><span data-stu-id="d498f-114">The script</span></span>

<span data-ttu-id="d498f-115">**指令碼位置**</span><span class="sxs-lookup"><span data-stu-id="d498f-115">**Script location**</span></span>

<span data-ttu-id="d498f-116">**以 Linux 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="d498f-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="d498f-117">**以 Windows 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="d498f-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d498f-118">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="d498f-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d498f-119">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="d498f-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d498f-120">**需求**</span><span class="sxs-lookup"><span data-stu-id="d498f-120">**Requirements**</span></span>

* <span data-ttu-id="d498f-121">指令碼必須同時套用至**前端節點**和**背景工作節點**。</span><span class="sxs-lookup"><span data-stu-id="d498f-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="d498f-122">您想要安裝的 jar 必須儲存在**單一容器**中的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d498f-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="d498f-123">包含 jar 檔案程式庫的儲存體帳戶**必須**在建立期間連結至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d498f-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="d498f-124">它必須是預設的儲存體帳戶，或是透過__選擇性組態__新增的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d498f-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="d498f-125">必須指定容器的 WASB 路徑做為指令碼動作的參數。</span><span class="sxs-lookup"><span data-stu-id="d498f-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="d498f-126">例如，如果 jar 儲存在名為 **mystorage** 的儲存體帳戶上稱為 **libs** 的容器中，則這個參數會是 **wasb://libs@mystorage.blob.core.windows.net/**。</span><span class="sxs-lookup"><span data-stu-id="d498f-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d498f-127">本文件假設您已建立儲存體帳戶、blob 容器，也已將檔案上傳給它。</span><span class="sxs-lookup"><span data-stu-id="d498f-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="d498f-128">如果您尚未建立儲存體帳戶，您可以透過 [Azure 入口網站](https://portal.azure.com)來建立。</span><span class="sxs-lookup"><span data-stu-id="d498f-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d498f-129">接著，您可以使用 [Azure 儲存體 Explorer](http://storageexplorer.com/) 之類的公用程式，在帳戶中建立容器，並將檔案上傳至其中。</span><span class="sxs-lookup"><span data-stu-id="d498f-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="d498f-130">使用指令碼建立叢集</span><span class="sxs-lookup"><span data-stu-id="d498f-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="d498f-131">下列步驟會建立以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d498f-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d498f-132">若要建立以 Windows 為基礎的叢集，請在建立叢集時選取 **Windows** 作為叢集作業系統，並使用 Windows (PowerShell) 指令碼，而不是 bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d498f-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="d498f-133">您也可以使用 Azure PowerShell 或 HDInsight .NET SDK，以使用此指令碼建立叢集。</span><span class="sxs-lookup"><span data-stu-id="d498f-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="d498f-134">如需使用這些方法的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="d498f-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="d498f-135">使用[在 Linux 上佈建 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的步驟開始佈建叢集，但是不完成佈建。</span><span class="sxs-lookup"><span data-stu-id="d498f-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="d498f-136">在 [選用組態] 刀鋒視窗中，選取 [指令碼動作]，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d498f-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="d498f-137">**名稱**：輸入指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="d498f-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="d498f-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="d498f-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="d498f-139">**HEAD**：勾選此選項。</span><span class="sxs-lookup"><span data-stu-id="d498f-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="d498f-140">**WORKER**：勾選此選項。</span><span class="sxs-lookup"><span data-stu-id="d498f-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="d498f-141">**ZOOKEEPER**：將此選項保留空白。</span><span class="sxs-lookup"><span data-stu-id="d498f-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="d498f-142">**參數**：輸入包含 jar 的容器和儲存體帳戶的 WASB 位址。</span><span class="sxs-lookup"><span data-stu-id="d498f-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="d498f-143">例如：**wasb://libs@mystorage.blob.core.windows.net/**。</span><span class="sxs-lookup"><span data-stu-id="d498f-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="d498f-144">在 [指令碼動作] 底部，使用 [選取] 按鈕以儲存組態。</span><span class="sxs-lookup"><span data-stu-id="d498f-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="d498f-145">在 [選擇性組態] 刀鋒視窗中，選取 [連結的儲存體帳戶]，然後選取 [新增儲存體金鑰] 連結。</span><span class="sxs-lookup"><span data-stu-id="d498f-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="d498f-146">選取包含 jar 的儲存體帳戶，然後使用 [選取] 按鈕來儲存設定，並回到 [選擇性組態] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d498f-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="d498f-147">使用 [選擇性組態] 刀鋒視窗底部的 [選取] 按鈕，儲存選擇性組態資訊。</span><span class="sxs-lookup"><span data-stu-id="d498f-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="d498f-148">繼續如[在 Linux 上佈建 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)中所述佈建叢集。</span><span class="sxs-lookup"><span data-stu-id="d498f-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="d498f-149">建立叢集完成後，您就能夠從 Hive 使用透過此指令碼新增的 jar，而不需使用 `ADD JAR` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d498f-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d498f-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d498f-150">Next steps</span></span>

<span data-ttu-id="d498f-151">如需有關使用 Hive 的詳細資訊，請參閱 [搭配使用 Hive 與 HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="d498f-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
