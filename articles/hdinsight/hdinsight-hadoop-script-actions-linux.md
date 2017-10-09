---
title: "與 linux 的 HDInsight 的 Azure 開發 aaaScript 動作 |Microsoft 文件"
description: "了解如何 toouse Bash 指令碼 toocustomize 以 Linux 為基礎的 HDInsight 叢集。 HDInsight 的 hello 指令碼動作的功能可讓您 toorun 指令碼期間或之後建立叢集。 指令碼可以使用的 toochange 叢集組態設定或安裝其他軟體。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="e84fc-105">使用 HDInsight 開發指令碼動作</span><span class="sxs-lookup"><span data-stu-id="e84fc-105">Script action development with HDInsight</span></span>

<span data-ttu-id="e84fc-106">深入了解如何撞 toocustomize 您 HDInsight 叢集使用指令碼。</span><span class="sxs-lookup"><span data-stu-id="e84fc-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="e84fc-107">指令碼動作是方式 toocustomize HDInsight 期間或之後建立叢集。</span><span class="sxs-lookup"><span data-stu-id="e84fc-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e84fc-108">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e84fc-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e84fc-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="e84fc-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e84fc-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e84fc-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="e84fc-111">什麼是指令碼動作</span><span class="sxs-lookup"><span data-stu-id="e84fc-111">What are script actions</span></span>

<span data-ttu-id="e84fc-112">指令碼動作，Azure 會 hello 叢集節點 toomake 設定變更上執行 Bash 指令碼，或安裝軟體。</span><span class="sxs-lookup"><span data-stu-id="e84fc-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="e84fc-113">指令碼動作為根，會執行，而且提供的完整存取權限 toohello 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="e84fc-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="e84fc-114">您可以透過下列方法的 hello 套用指令碼動作：</span><span class="sxs-lookup"><span data-stu-id="e84fc-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="e84fc-115">使用此方法 tooapply 指令碼...</span><span class="sxs-lookup"><span data-stu-id="e84fc-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="e84fc-116">在叢集建立期間...</span><span class="sxs-lookup"><span data-stu-id="e84fc-116">During cluster creation...</span></span> | <span data-ttu-id="e84fc-117">在執行中的叢集上...</span><span class="sxs-lookup"><span data-stu-id="e84fc-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="e84fc-118">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e84fc-118">Azure portal</span></span> |<span data-ttu-id="e84fc-119">✓ </span><span class="sxs-lookup"><span data-stu-id="e84fc-119">✓</span></span> |<span data-ttu-id="e84fc-120">✓</span><span class="sxs-lookup"><span data-stu-id="e84fc-120">✓</span></span> |
| <span data-ttu-id="e84fc-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e84fc-121">Azure PowerShell</span></span> |<span data-ttu-id="e84fc-122">✓</span><span class="sxs-lookup"><span data-stu-id="e84fc-122">✓</span></span> |<span data-ttu-id="e84fc-123">✓</span><span class="sxs-lookup"><span data-stu-id="e84fc-123">✓</span></span> |
| <span data-ttu-id="e84fc-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e84fc-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="e84fc-125">✓</span><span class="sxs-lookup"><span data-stu-id="e84fc-125">✓</span></span> |
| <span data-ttu-id="e84fc-126">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e84fc-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="e84fc-127">✓</span><span class="sxs-lookup"><span data-stu-id="e84fc-127">✓</span></span> |<span data-ttu-id="e84fc-128">✓</span><span class="sxs-lookup"><span data-stu-id="e84fc-128">✓</span></span> |
| <span data-ttu-id="e84fc-129">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="e84fc-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="e84fc-130">✓ </span><span class="sxs-lookup"><span data-stu-id="e84fc-130">✓</span></span> |&nbsp; |

<span data-ttu-id="e84fc-131">如需有關使用這些方法 tooapply 指令碼動作的詳細資訊，請參閱[使用指令碼動作的自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e84fc-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="e84fc-132"><a name="bestPracticeScripting"></a>指令碼開發的最佳做法</span><span class="sxs-lookup"><span data-stu-id="e84fc-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="e84fc-133">當您開發的 HDInsight 叢集的自訂指令碼時，有數個最佳作法 tookeep 事項：</span><span class="sxs-lookup"><span data-stu-id="e84fc-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="e84fc-134">Hello Hadoop 版本為目標</span><span class="sxs-lookup"><span data-stu-id="e84fc-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="e84fc-135">目標 hello OS 版本</span><span class="sxs-lookup"><span data-stu-id="e84fc-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="e84fc-136">提供穩定連結 tooscript 資源</span><span class="sxs-lookup"><span data-stu-id="e84fc-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="e84fc-137">使用預先編譯的資源</span><span class="sxs-lookup"><span data-stu-id="e84fc-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="e84fc-138">確保 hello 叢集自訂指令碼為等冪</span><span class="sxs-lookup"><span data-stu-id="e84fc-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="e84fc-139">確保高可用性的 hello 叢集架構</span><span class="sxs-lookup"><span data-stu-id="e84fc-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="e84fc-140">設定 hello 自訂元件 toouse Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e84fc-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="e84fc-141">寫入資訊 tooSTDOUT 和 STDERR</span><span class="sxs-lookup"><span data-stu-id="e84fc-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="e84fc-142">將檔案儲存為具有 LF 行尾結束符號的 ASCII</span><span class="sxs-lookup"><span data-stu-id="e84fc-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="e84fc-143">使用從暫時性錯誤重試邏輯 toorecover</span><span class="sxs-lookup"><span data-stu-id="e84fc-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="e84fc-144">指令碼動作必須在 60 分鐘的時間內完成，或 hello 程序會失敗。</span><span class="sxs-lookup"><span data-stu-id="e84fc-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="e84fc-145">在佈建的節點，與其他安裝及設定處理程序同時執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e84fc-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="e84fc-146">競爭資源，例如 CPU 時間和網路頻寬可能會導致 hello 指令碼 tootake 長 toofinish 不同於您的開發環境。</span><span class="sxs-lookup"><span data-stu-id="e84fc-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="e84fc-147"><a name="bPS1"></a>Hello Hadoop 版本為目標</span><span class="sxs-lookup"><span data-stu-id="e84fc-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="e84fc-148">不同版本的 HDInsight 有不同版本的 Hadoop 服務和已安裝的元件。</span><span class="sxs-lookup"><span data-stu-id="e84fc-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="e84fc-149">如果您的指令碼需要特定版本的服務或元件，您應該只使用 hello 指令碼 hello 包含所需的 hello 元件的 HDInsight 版本。</span><span class="sxs-lookup"><span data-stu-id="e84fc-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="e84fc-150">您可以找到有關隨附 HDInsight 的元件版本使用 hello [HDInsight 的元件版本控制](hdinsight-component-versioning.md)文件。</span><span class="sxs-lookup"><span data-stu-id="e84fc-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="e84fc-151"><a name="bps10"></a>目標 hello OS 版本</span><span class="sxs-lookup"><span data-stu-id="e84fc-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="e84fc-152">以 Linux 為基礎的 HDInsight 根據 hello Ubuntu Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="e84fc-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="e84fc-153">不同 HDInsight 版本仰賴不同的 Ubuntu 版本，這可能會改變指令碼的運作方式。</span><span class="sxs-lookup"><span data-stu-id="e84fc-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="e84fc-154">例如，HDInsight 3.4 及更早版本所根據的是使用 Upstart 的 Ubuntu 版本。</span><span class="sxs-lookup"><span data-stu-id="e84fc-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="e84fc-155">3.5 版所根據的是 Ubuntu 16.04，其使用的是 Systemd。</span><span class="sxs-lookup"><span data-stu-id="e84fc-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="e84fc-156">Systemd 和同時依賴不同的命令，讓您的指令碼應寫入 toowork 同時使用。</span><span class="sxs-lookup"><span data-stu-id="e84fc-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="e84fc-157">HDInsight 3.4 和 3.5 之間的另一個重要的差異在於`JAVA_HOME`現在點 tooJava 8。</span><span class="sxs-lookup"><span data-stu-id="e84fc-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="e84fc-158">您可以藉由檢查 hello OS 版本`lsb_release`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="e84fc-159">hello 下列程式碼示範如何 toodetermine 如果 hello 指令碼 Ubuntu 14 或 16 上執行：</span><span class="sxs-lookup"><span data-stu-id="e84fc-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="e84fc-160">您可以找到包含這些程式碼片段在 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh hello 完整指令碼。</span><span class="sxs-lookup"><span data-stu-id="e84fc-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="e84fc-161">如需使用 HDInsight 的 Ubuntu hello 版本，請參閱 hello [HDInsight 元件版本](hdinsight-component-versioning.md)文件。</span><span class="sxs-lookup"><span data-stu-id="e84fc-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="e84fc-162">toounderstand hello Systemd 和差異同時，請參閱[同時使用者 Systemd](https://wiki.ubuntu.com/SystemdForUpstartUsers)。</span><span class="sxs-lookup"><span data-stu-id="e84fc-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="e84fc-163"><a name="bPS2"></a>提供穩定連結 tooscript 資源</span><span class="sxs-lookup"><span data-stu-id="e84fc-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="e84fc-164">hello 指令碼和相關聯的資源必須維持可在整個存留期 hello hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e84fc-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="e84fc-165">如果新節點加入叢集 toohello 縮放作業期間需要這些資源。</span><span class="sxs-lookup"><span data-stu-id="e84fc-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="e84fc-166">hello 最佳作法是 toodownload 和封存您的訂用帳戶的 Azure 儲存體帳戶中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="e84fc-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e84fc-167">使用 hello 儲存體帳戶必須是 hello 預設儲存體帳戶的 hello 叢集或公開的唯讀容器上任何其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e84fc-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="e84fc-168">例如，由 Microsoft 提供的 hello 範例會儲存在 hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/)儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e84fc-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="e84fc-169">這是由 hello HDInsight 團隊負責維護的公用、 唯讀容器。</span><span class="sxs-lookup"><span data-stu-id="e84fc-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="e84fc-170"><a name="bPS4"></a>使用預先編譯的資源</span><span class="sxs-lookup"><span data-stu-id="e84fc-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="e84fc-171">tooreduce hello 次它採用 toorun hello 指令碼時，避免編譯資源從來源程式碼的作業。</span><span class="sxs-lookup"><span data-stu-id="e84fc-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="e84fc-172">比方說，先行編譯的資源，並將其儲存在 Azure 儲存體帳戶中 blob hello 與 HDInsight 的相同資料中心。</span><span class="sxs-lookup"><span data-stu-id="e84fc-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="e84fc-173"><a name="bPS3"></a>確保 hello 叢集自訂指令碼為等冪</span><span class="sxs-lookup"><span data-stu-id="e84fc-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="e84fc-174">指令碼必須具有等冪性。</span><span class="sxs-lookup"><span data-stu-id="e84fc-174">Scripts must be idempotent.</span></span> <span data-ttu-id="e84fc-175">如果多次執行 hello 指令碼，它應該傳回 hello 叢集 toohello 相同狀態的每一次。</span><span class="sxs-lookup"><span data-stu-id="e84fc-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="e84fc-176">例如，如果一個會修改組態檔的指令碼執行多次，則不應該新增重複的項目。</span><span class="sxs-lookup"><span data-stu-id="e84fc-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="e84fc-177"><a name="bPS5"></a>確保高可用性的 hello 叢集架構</span><span class="sxs-lookup"><span data-stu-id="e84fc-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="e84fc-178">以 Linux 為基礎的 HDInsight 叢集提供 hello 叢集內的作用中的兩個前端節點和兩個節點上執行指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="e84fc-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="e84fc-179">如果您安裝的 hello 元件預期只有一個前端節點，請勿在這兩個前端節點上安裝 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="e84fc-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e84fc-180">HDInsight 中提供的服務是設計的 toofail 透過 hello 兩個前端節點之間所需。</span><span class="sxs-lookup"><span data-stu-id="e84fc-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="e84fc-181">這項功能不會延長 toocustom 安裝的元件，透過指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="e84fc-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="e84fc-182">如果自訂元件需要有高可用性時，您必須實作自己的容錯移轉機制。</span><span class="sxs-lookup"><span data-stu-id="e84fc-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="e84fc-183"><a name="bPS6"></a>設定 hello 自訂元件 toouse Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e84fc-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="e84fc-184">您在 hello 叢集安裝的元件可能必須使用 Hadoop 分散式檔案系統 (HDFS) 儲存體的預設設定。</span><span class="sxs-lookup"><span data-stu-id="e84fc-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="e84fc-185">HDInsight 使用 Azure 儲存體或資料湖存放區做為 hello 預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="e84fc-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="e84fc-186">這兩者都提供保存資料，即使已經刪除 hello 叢集的 HDFS 相容的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="e84fc-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="e84fc-187">您可能需要安裝 toouse WASB 或而不是 HDFS ADL tooconfigure 元件。</span><span class="sxs-lookup"><span data-stu-id="e84fc-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="e84fc-188">對於大部分的作業，您不需要 toospecify hello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="e84fc-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="e84fc-189">例如，下列 hello hello giraph examples.jar 會從檔案複製 hello 本機檔案系統 toocluster 儲存體：</span><span class="sxs-lookup"><span data-stu-id="e84fc-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="e84fc-190">在此範例中，hello`hdfs`命令以透明的方式使用 hello 預設叢集存放區。</span><span class="sxs-lookup"><span data-stu-id="e84fc-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="e84fc-191">對於某些運算而言，您可能需要 toospecify hello URI。</span><span class="sxs-lookup"><span data-stu-id="e84fc-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="e84fc-192">例如，Data Lake Store 的 `adl:///example/jars`，或 Azure 儲存體的 `wasb:///example/jars`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="e84fc-193"><a name="bPS7"></a>寫入資訊 tooSTDOUT 和 STDERR</span><span class="sxs-lookup"><span data-stu-id="e84fc-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="e84fc-194">HDInsight 記錄會寫入的 tooSTDOUT 和 STDERR 的指令碼輸出。</span><span class="sxs-lookup"><span data-stu-id="e84fc-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="e84fc-195">您可以檢視這項資訊使用 hello Ambari web UI。</span><span class="sxs-lookup"><span data-stu-id="e84fc-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="e84fc-196">Ambari 才可以使用已成功建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e84fc-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="e84fc-197">如果您使用指令碼動作在叢集建立，並建立動作失敗時，請參閱 < 疑難排解 > 一節的 hello[自訂 HDInsight 叢集使用指令碼動作](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)的其他方式存取登入的資訊。</span><span class="sxs-lookup"><span data-stu-id="e84fc-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="e84fc-198">大部分的公用程式和安裝封裝已經寫入資訊 tooSTDOUT 和 STDERR，不過您可能會想 tooadd 額外的記錄功能。</span><span class="sxs-lookup"><span data-stu-id="e84fc-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="e84fc-199">toosend 文字 tooSTDOUT 使用`echo`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="e84fc-200">例如：</span><span class="sxs-lookup"><span data-stu-id="e84fc-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="e84fc-201">根據預設，`echo`傳送 hello 字串 tooSTDOUT。</span><span class="sxs-lookup"><span data-stu-id="e84fc-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="e84fc-202">toodirect 它 tooSTDERR，新增`>&2`之前`echo`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="e84fc-203">例如：</span><span class="sxs-lookup"><span data-stu-id="e84fc-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="e84fc-204">這將會改寫入 tooSTDOUT tooSTDERR (2) 的資訊重新導向。</span><span class="sxs-lookup"><span data-stu-id="e84fc-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="e84fc-205">如需 IO 重新導向的詳細資訊，請參閱 [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html)。</span><span class="sxs-lookup"><span data-stu-id="e84fc-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="e84fc-206">如需檢視指令碼動作記錄之資訊的詳細資訊，請參閱 [使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="e84fc-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="e84fc-207"><a name="bps8"></a> 將檔案儲存為具有 LF 行尾結束符號的 ASCII</span><span class="sxs-lookup"><span data-stu-id="e84fc-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="e84fc-208">Bash 指令碼應該儲存為 ASCII 格式，該格式以 LF 做為行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="e84fc-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="e84fc-209">檔案儲存為 utf-8，或做為可 CRLF hello 行尾結束符號可能會因下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="e84fc-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="e84fc-210"><a name="bps9"></a>使用從暫時性錯誤重試邏輯 toorecover</span><span class="sxs-lookup"><span data-stu-id="e84fc-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="e84fc-211">當下載檔案，安裝封裝使用 apt get 或傳輸資料的其他動作 hello 網際網路，hello 動作可能失敗的原因 tootransient 網路錯誤。</span><span class="sxs-lookup"><span data-stu-id="e84fc-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="e84fc-212">例如，您通訊的 hello 遠端資源可能處於 tooa 備份節點上方 hello 程序執行失敗。</span><span class="sxs-lookup"><span data-stu-id="e84fc-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="e84fc-213">toomake 指令碼具有恢復功能 tootransient 錯誤，您可以實作重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="e84fc-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="e84fc-214">下列函式的 hello 示範如何 tooimplement 重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="e84fc-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="e84fc-215">它會重試三次失敗之前的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="e84fc-215">It retries hello operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="e84fc-216">hello 下列範例將示範如何 toouse 此函式。</span><span class="sxs-lookup"><span data-stu-id="e84fc-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="e84fc-217"><a name="helpermethods"></a>自訂指令碼的協助程式方法</span><span class="sxs-lookup"><span data-stu-id="e84fc-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="e84fc-218">指令碼動作協助程式方法是您在撰寫字訂指令碼時可以使用的公用程式。</span><span class="sxs-lookup"><span data-stu-id="e84fc-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="e84fc-219">這些方法全都在 [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="e84fc-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="e84fc-220">使用下列 toodownload hello 和使用它們做為您的指令碼的一部分：</span><span class="sxs-lookup"><span data-stu-id="e84fc-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="e84fc-221">下列 helper 可在您的指令碼中使用的 hello:</span><span class="sxs-lookup"><span data-stu-id="e84fc-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="e84fc-222">協助程式使用方式</span><span class="sxs-lookup"><span data-stu-id="e84fc-222">Helper usage</span></span> | <span data-ttu-id="e84fc-223">說明</span><span class="sxs-lookup"><span data-stu-id="e84fc-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="e84fc-224">下載檔案從 hello 來源 URI toohello 指定的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="e84fc-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="e84fc-225">根據預設，不會覆寫現有的檔案。</span><span class="sxs-lookup"><span data-stu-id="e84fc-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="e84fc-226">解壓縮 tar 檔案解壓縮檔案 (使用`-xf`) toohello 目的地目錄。</span><span class="sxs-lookup"><span data-stu-id="e84fc-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="e84fc-227">如果在叢集前端節點上執行，則會傳回 1，否則傳回 0。</span><span class="sxs-lookup"><span data-stu-id="e84fc-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="e84fc-228">如果 hello 目前節點的資料 （背景工作角色） 節點，則傳回 1;否則為 0。</span><span class="sxs-lookup"><span data-stu-id="e84fc-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="e84fc-229">如果 hello 目前節點為 hello 第一個資料 （背景工作角色） 節點 (具名 workernode0) 會傳回 1;否則為 0。</span><span class="sxs-lookup"><span data-stu-id="e84fc-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="e84fc-230">傳回 hello hello headnodes hello 叢集中的完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e84fc-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="e84fc-231">名稱會以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="e84fc-231">Names are comma delimited.</span></span> <span data-ttu-id="e84fc-232">發生錯誤時會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="e84fc-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="e84fc-233">取得 hello 的 hello 主要叢集前端節點的完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e84fc-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="e84fc-234">發生錯誤時會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="e84fc-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="e84fc-235">取得 hello 的 hello 次要叢集前端節點的完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e84fc-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="e84fc-236">發生錯誤時會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="e84fc-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="e84fc-237">取得 hello 的 hello 主要叢集前端節點的數值後置詞。</span><span class="sxs-lookup"><span data-stu-id="e84fc-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="e84fc-238">發生錯誤時會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="e84fc-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="e84fc-239">取得 hello 的 hello 次要叢集前端節點的數值後置詞。</span><span class="sxs-lookup"><span data-stu-id="e84fc-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="e84fc-240">發生錯誤時會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="e84fc-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="e84fc-241"><a name="commonusage"></a>常見使用模式</span><span class="sxs-lookup"><span data-stu-id="e84fc-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="e84fc-242">此章節提供指引實作某些 hello 常見的使用模式，您可能會遇到撰寫自訂指令碼時。</span><span class="sxs-lookup"><span data-stu-id="e84fc-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="e84fc-243">傳遞參數 tooa 指令碼</span><span class="sxs-lookup"><span data-stu-id="e84fc-243">Passing parameters tooa script</span></span>

<span data-ttu-id="e84fc-244">在某些情況下，您的指令碼可能需要參數。</span><span class="sxs-lookup"><span data-stu-id="e84fc-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="e84fc-245">例如，您可能需要 hello 系統管理員密碼 hello 叢集使用 hello Ambari REST API 時。</span><span class="sxs-lookup"><span data-stu-id="e84fc-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="e84fc-246">傳遞 toohello 指令碼參數稱為*位置參數*，以及要指派太`$1`hello 第一個參數， `$2` hello 第二個，並讓入。</span><span class="sxs-lookup"><span data-stu-id="e84fc-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="e84fc-247">`$0`包含 hello 的 hello 指令碼本身的名稱。</span><span class="sxs-lookup"><span data-stu-id="e84fc-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="e84fc-248">做為參數傳遞 toohello 指令碼的值應該放在單引號 （'）。</span><span class="sxs-lookup"><span data-stu-id="e84fc-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="e84fc-249">這麼做可確保該 hello 傳遞值視為常值。</span><span class="sxs-lookup"><span data-stu-id="e84fc-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="e84fc-250">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="e84fc-250">Setting environment variables</span></span>

<span data-ttu-id="e84fc-251">設定環境變數被執行陳述式之後的 hello:</span><span class="sxs-lookup"><span data-stu-id="e84fc-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="e84fc-252">變數名稱所在 hello hello 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="e84fc-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="e84fc-253">tooaccess hello 變數時，使用`$VARIABLENAME`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="e84fc-254">比方說，tooassign 做為環境變數的位置參數所提供的值命名為密碼，可以使用下列陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e84fc-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="e84fc-255">接著可以使用後續存取 toohello 資訊`$PASSWORD`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="e84fc-256">Hello 指令碼內設定的環境變數只存在於 hello hello 指令碼範圍內。</span><span class="sxs-lookup"><span data-stu-id="e84fc-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="e84fc-257">在某些情況下，您可能需要 tooadd 全系統環境變數會保存 hello 指令碼完成後。</span><span class="sxs-lookup"><span data-stu-id="e84fc-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="e84fc-258">tooadd 全系統環境變數，加入 hello 變數太`/etc/environment`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="e84fc-259">例如，將陳述式之後的 hello `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="e84fc-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="e84fc-260">存取的 toolocations hello 自訂指令碼的儲存位置</span><span class="sxs-lookup"><span data-stu-id="e84fc-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="e84fc-261">使用指令碼 toocustomize 叢集需要 toobe 儲存在下列位置的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="e84fc-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="e84fc-262">__Azure 儲存體帳戶__與 hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="e84fc-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="e84fc-263">__額外的儲存體帳戶__hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="e84fc-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="e84fc-264">__可公開讀取的 URI__。</span><span class="sxs-lookup"><span data-stu-id="e84fc-264">A __publicly readable URI__.</span></span> <span data-ttu-id="e84fc-265">例如，URL toodata 儲存在 OneDrive、 Dropbox 或裝載服務的其他檔案。</span><span class="sxs-lookup"><span data-stu-id="e84fc-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="e84fc-266">__Azure Data Lake Store 帳戶__與 hello HDInsight 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="e84fc-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="e84fc-267">如需使用 Azure Data Lake Store 與 HDInsight 的詳細資訊，請參閱[建立使用 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e84fc-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e84fc-268">hello 服務主體 HDInsight 使用 tooaccess 資料湖存放區必須有讀取權限 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e84fc-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="e84fc-269">Hello 指令碼所使用的資源也必須是公用的。</span><span class="sxs-lookup"><span data-stu-id="e84fc-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="e84fc-270">將 hello 檔案儲存在 Azure 儲存體帳戶或 Azure 資料湖存放區提供快速存取，同時 hello Azure 網路內。</span><span class="sxs-lookup"><span data-stu-id="e84fc-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="e84fc-271">hello URI 格式使用 tooreference hello 指令碼是根據目前使用的 hello 服務而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e84fc-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="e84fc-272">Hello HDInsight 叢集相關聯的儲存體帳戶，使用`wasb://`或`wasbs://`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="e84fc-273">若為可公開讀取的 URI，請使用 `http://` 或 `https://`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="e84fc-274">若為 Data Lake Store，請使用 `adl://`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="e84fc-275">正在檢查 hello 作業系統版本</span><span class="sxs-lookup"><span data-stu-id="e84fc-275">Checking hello operating system version</span></span>

<span data-ttu-id="e84fc-276">不同 HDInsight 版本各仰賴特定的 Ubuntu 版本。</span><span class="sxs-lookup"><span data-stu-id="e84fc-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="e84fc-277">您在指令碼中必須檢查的 OS 版本之間可能會有差異。</span><span class="sxs-lookup"><span data-stu-id="e84fc-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="e84fc-278">例如，您可能需要 tooinstall Ubuntu 繫結的 toohello 版本的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="e84fc-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="e84fc-279">toocheck hello OS 版本，使用`lsb_release`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="e84fc-280">例如，下列指令碼的 hello 示範根據 hello OS 版本 tooreference 特定 tar 檔案解壓縮檔案的方式：</span><span class="sxs-lookup"><span data-stu-id="e84fc-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="e84fc-281"><a name="deployScript"></a>指令碼動作的部署檢查清單</span><span class="sxs-lookup"><span data-stu-id="e84fc-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="e84fc-282">準備 toodeploy 這些指令碼時，我們採用的 hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="e84fc-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="e84fc-283">將包含 hello 自訂指令碼可在部署期間 hello 叢集節點可存取的位置中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e84fc-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="e84fc-284">例如，hello hello 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="e84fc-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="e84fc-285">檔案也可以儲存在可公開讀取的主機服務中。</span><span class="sxs-lookup"><span data-stu-id="e84fc-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="e84fc-286">確認 impotent hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e84fc-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="e84fc-287">這樣做可讓 hello 指令碼 toobe 執行多次 hello 上相同節點。</span><span class="sxs-lookup"><span data-stu-id="e84fc-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="e84fc-288">使用暫存檔目錄 tec_rule 位於 /tmp tookeep hello 下載 hello 指令碼所使用的檔案，然後再清除它們之後執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="e84fc-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="e84fc-289">如果作業系統層級的設定或 Hadoop 服務組態檔已變更，您可能想 toorestart HDInsight 服務。</span><span class="sxs-lookup"><span data-stu-id="e84fc-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="e84fc-290"><a name="runScriptAction"></a>如何 toorun 指令碼動作</span><span class="sxs-lookup"><span data-stu-id="e84fc-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="e84fc-291">您可以使用指令碼動作 toocustomize HDInsight 叢集使用 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="e84fc-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="e84fc-292">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e84fc-292">Azure portal</span></span>
* <span data-ttu-id="e84fc-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e84fc-293">Azure PowerShell</span></span>
* <span data-ttu-id="e84fc-294">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="e84fc-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="e84fc-295">hello HDInsight.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="e84fc-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="e84fc-296">如需有關如何使用每個方法的詳細資訊，請參閱[toouse 如何編寫指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e84fc-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="e84fc-297"><a name="sampleScripts"></a>自訂指令碼範例</span><span class="sxs-lookup"><span data-stu-id="e84fc-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="e84fc-298">Microsoft 提供範例指令碼 tooinstall 元件上的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e84fc-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="e84fc-299">請參閱下列連結以取得更多的範例指令碼動作的 hello。</span><span class="sxs-lookup"><span data-stu-id="e84fc-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="e84fc-300">在 HDInsight 叢集上安裝及使用色調</span><span class="sxs-lookup"><span data-stu-id="e84fc-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="e84fc-301">在 HDInsight 叢集上安裝及使用 Solr</span><span class="sxs-lookup"><span data-stu-id="e84fc-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="e84fc-302">在 HDInsight 叢集上安裝及使用 Giraph</span><span class="sxs-lookup"><span data-stu-id="e84fc-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="e84fc-303">在 HDInsight 叢集上安裝或升級 Mono</span><span class="sxs-lookup"><span data-stu-id="e84fc-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="e84fc-304">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e84fc-304">Troubleshooting</span></span>

<span data-ttu-id="e84fc-305">hello 下面是使用您所開發的指令碼時，可能會遇到的錯誤：</span><span class="sxs-lookup"><span data-stu-id="e84fc-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="e84fc-306">**錯誤**：`$'\r': command not found`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="e84fc-307">有時候後面接續 `syntax error: unexpected end of file`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="e84fc-308">*可能的原因*： 指令碼中的 hello 行結尾 CRLF 時造成這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="e84fc-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="e84fc-309">Unix 系統預期只有 LF 為 hello 行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="e84fc-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="e84fc-310">發生此問題最常在 Windows 環境中，撰寫 hello 指令碼，則當因為 CRLF 是常見的行尾結束符號的 Windows 上的多個文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="e84fc-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="e84fc-311">*解析*： 如果您的文字編輯器中的選項，請選取 Unix 格式或 LF hello 行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="e84fc-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="e84fc-312">您也可以使用下列命令在 Unix 系統 toochange hello CRLF tooan LF hello:</span><span class="sxs-lookup"><span data-stu-id="e84fc-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="e84fc-313">hello 下列命令的建立方式大致在於應變 hello CRLF 行尾結束符號 tooLF。</span><span class="sxs-lookup"><span data-stu-id="e84fc-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="e84fc-314">選取其中一個系統上可用的 hello 公用程式為基礎。</span><span class="sxs-lookup"><span data-stu-id="e84fc-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="e84fc-315">命令</span><span class="sxs-lookup"><span data-stu-id="e84fc-315">Command</span></span> | <span data-ttu-id="e84fc-316">注意事項</span><span class="sxs-lookup"><span data-stu-id="e84fc-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="e84fc-317">hello 原始檔案會與備份。BAK 延伸模組</span><span class="sxs-lookup"><span data-stu-id="e84fc-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="e84fc-318">OUTFILE 會包含只有 LF 行尾結束符號的版本</span><span class="sxs-lookup"><span data-stu-id="e84fc-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="e84fc-319">直接修改 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="e84fc-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="e84fc-320">OUTFILE 會包含只有 LF 行尾結束符號的版本。</span><span class="sxs-lookup"><span data-stu-id="e84fc-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="e84fc-321">**錯誤**：`line 1: #!/usr/bin/env: No such file or directory`。</span><span class="sxs-lookup"><span data-stu-id="e84fc-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="e84fc-322">*可能的原因*： 時會發生此錯誤 hello 指令碼已儲存為 utf-8 與位元組順序標記 (BOM)。</span><span class="sxs-lookup"><span data-stu-id="e84fc-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="e84fc-323">*解析*： 儲存 hello 檔案以 ascii 模式，或為不具有 BOM utf-8。</span><span class="sxs-lookup"><span data-stu-id="e84fc-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="e84fc-324">您也可以使用下列命令，在 Linux 或 Unix 系統 toocreate 沒有 hello BOM 的檔案上的 hello:</span><span class="sxs-lookup"><span data-stu-id="e84fc-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="e84fc-325">取代`INFILE`hello 檔案包含 hello BOM。</span><span class="sxs-lookup"><span data-stu-id="e84fc-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="e84fc-326">`OUTFILE`應該是新的檔案名稱，其中包含不含 hello BOM hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e84fc-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="e84fc-327"><a name="seeAlso"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="e84fc-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="e84fc-328">了解如何太[使用指令碼動作的自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e84fc-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="e84fc-329">使用 hello [HDInsight.NET SDK 參考](https://msdn.microsoft.com/library/mt271028.aspx)toolearn 深入了解建立管理 HDInsight 的.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="e84fc-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="e84fc-330">使用 hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn toouse REST tooperform 管理動作，在 HDInsight 上的叢集。</span><span class="sxs-lookup"><span data-stu-id="e84fc-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
