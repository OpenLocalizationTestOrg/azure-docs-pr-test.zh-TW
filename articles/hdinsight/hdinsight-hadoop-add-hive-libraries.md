---
title: "aaaAdd Hive 程式庫，在 HDInsight 叢集建立-Azure |Microsoft 文件"
description: "了解如何 tooadd Hive 程式庫 （jar 檔案），tooan HDInsight 叢集在叢集建立期間。"
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
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="dda78-103">建立 HDInsight 叢集時新增自訂 Hive 程式庫</span><span class="sxs-lookup"><span data-stu-id="dda78-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="dda78-104">如果您有與 HDInsight 上的登錄區經常使用的程式庫，這份文件會包含有關在叢集建立期間使用的指令碼動作 toopre 負載 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="dda78-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="dda78-105">登錄區中，使用這份文件中的 hello 步驟加入的程式庫供全域使用-沒有任何需要 toouse[新增 JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload 它們。</span><span class="sxs-lookup"><span data-stu-id="dda78-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="dda78-106">運作方式</span><span class="sxs-lookup"><span data-stu-id="dda78-106">How it works</span></span>

<span data-ttu-id="dda78-107">在建立叢集時，您可以選擇性地指定一個 hello 叢集節點執行指令碼，在建立時的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="dda78-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="dda78-108">這份文件中的 hello 指令碼會接受單一參數，這是包含預先載入的 hello （儲存為 jar 檔案） 的程式庫 toobe WASB 位置。</span><span class="sxs-lookup"><span data-stu-id="dda78-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="dda78-109">在叢集建立期間 hello 指令碼列舉 hello 檔案、 將其複製 toohello`/usr/lib/customhivelibs/`目錄標頭和背景工作節點，然後將它們新增 toohello`hive.aux.jars.path`屬性在 hello`core-site.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="dda78-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="dda78-110">在以 Linux 為基礎的叢集，它也會更新 hello `hive-env.sh` hello hello 檔案位置的檔案。</span><span class="sxs-lookup"><span data-stu-id="dda78-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="dda78-111">使用本文章中的 hello 指令碼動作 hello 程式庫可讓在 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="dda78-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="dda78-112">**以 Linux 為基礎的 HDInsight** -時使用 hello Hive 用戶端**WebHCat**，和**HiveServer2**。</span><span class="sxs-lookup"><span data-stu-id="dda78-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="dda78-113">**Windows 為基礎的 HDInsight** -時使用 hello Hive 用戶端和**WebHCat**。</span><span class="sxs-lookup"><span data-stu-id="dda78-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="dda78-114">hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="dda78-114">hello script</span></span>

<span data-ttu-id="dda78-115">**指令碼位置**</span><span class="sxs-lookup"><span data-stu-id="dda78-115">**Script location**</span></span>

<span data-ttu-id="dda78-116">**以 Linux 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="dda78-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="dda78-117">**以 Windows 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="dda78-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dda78-118">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="dda78-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dda78-119">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="dda78-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="dda78-120">**需求**</span><span class="sxs-lookup"><span data-stu-id="dda78-120">**Requirements**</span></span>

* <span data-ttu-id="dda78-121">hello 指令碼必須可套用的 tooboth hello**前端節點**和**背景工作節點**。</span><span class="sxs-lookup"><span data-stu-id="dda78-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="dda78-122">（每瓶) 您希望 tooinstall 必須儲存在 Azure Blob 儲存體中的 hello**單一容器**。</span><span class="sxs-lookup"><span data-stu-id="dda78-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="dda78-123">hello 包含 jar 檔案的 hello 程式庫的儲存體帳戶**必須**是建立連結的 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dda78-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="dda78-124">它必須是 hello 預設儲存體帳戶，或透過加入帳戶__選擇性組態__。</span><span class="sxs-lookup"><span data-stu-id="dda78-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="dda78-125">hello WASB 路徑 toohello 容器必須指定為參數 toohello 指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="dda78-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="dda78-126">例如，如果 hello （每瓶） 會儲存在名為的容器**程式庫**儲存體帳戶上名為**mystorage**，hello 參數便是 **wasb://libs@mystorage.blob.core.windows.net/** 。</span><span class="sxs-lookup"><span data-stu-id="dda78-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="dda78-127">本文件假設您有已建立儲存體帳戶、 blob 容器和上傳的 hello 檔案 tooit。</span><span class="sxs-lookup"><span data-stu-id="dda78-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="dda78-128">如果您尚未建立儲存體帳戶，您可以透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="dda78-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dda78-129">然後您可以使用公用程式例如[Azure 儲存體總管](http://storageexplorer.com/)toocreate 容器中 hello 帳戶和上傳的檔案 tooit。</span><span class="sxs-lookup"><span data-stu-id="dda78-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="dda78-130">使用 hello 指令碼建立叢集</span><span class="sxs-lookup"><span data-stu-id="dda78-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="dda78-131">hello 下列步驟建立以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dda78-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="dda78-132">toocreate Windows 為基礎的叢集上，選取**Windows** hello 與叢集作業系統建立 hello 叢集時，並使用 hello Windows (PowerShell) 指令碼，而不是 hello bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="dda78-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="dda78-133">您也可以使用 Azure PowerShell 或 hello HDInsight.NET SDK toocreate 使用此指令碼的叢集。</span><span class="sxs-lookup"><span data-stu-id="dda78-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="dda78-134">如需使用這些方法的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="dda78-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="dda78-135">開始使用中的 hello 步驟佈建叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)，但是不完成佈建。</span><span class="sxs-lookup"><span data-stu-id="dda78-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="dda78-136">在 hello**選擇性組態**刀鋒視窗中，選取**指令碼動作**，並提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="dda78-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="dda78-137">**名稱**： 輸入 hello 指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="dda78-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="dda78-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="dda78-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="dda78-139">**HEAD**：勾選此選項。</span><span class="sxs-lookup"><span data-stu-id="dda78-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="dda78-140">**WORKER**：勾選此選項。</span><span class="sxs-lookup"><span data-stu-id="dda78-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="dda78-141">**ZOOKEEPER**：將此選項保留空白。</span><span class="sxs-lookup"><span data-stu-id="dda78-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="dda78-142">**參數**： 輸入 hello WASB 位址 toohello 容器和儲存體帳戶包含 hello （每瓶）。</span><span class="sxs-lookup"><span data-stu-id="dda78-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="dda78-143">例如：**wasb://libs@mystorage.blob.core.windows.net/**。</span><span class="sxs-lookup"><span data-stu-id="dda78-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="dda78-144">在 hello 底部 hello**指令碼動作**，使用 hello**選取**按鈕 toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="dda78-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="dda78-145">在 hello**選擇性組態**刀鋒視窗中，選取**連結儲存體帳戶**和選取 hello**新增儲存體金鑰**連結。</span><span class="sxs-lookup"><span data-stu-id="dda78-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="dda78-146">選取包含 hello （每瓶），hello 儲存體帳戶，然後使用 hello**選取**按鈕 toosave 設定和傳回 hello**選擇性組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dda78-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="dda78-147">使用 hello**選取**在 hello hello 底部的按鈕**選擇性組態**刀鋒視窗 toosave hello 選擇性的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="dda78-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="dda78-148">繼續中所述，佈建 hello 叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="dda78-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="dda78-149">一旦叢集建立完成時，您就可以 toouse hello （每瓶） 從 Hive 加入到此指令碼而不需要 toouse hello`ADD JAR`陳述式。</span><span class="sxs-lookup"><span data-stu-id="dda78-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dda78-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dda78-150">Next steps</span></span>

<span data-ttu-id="dda78-151">如需有關使用 Hive 的詳細資訊，請參閱 [搭配使用 Hive 與 HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="dda78-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
