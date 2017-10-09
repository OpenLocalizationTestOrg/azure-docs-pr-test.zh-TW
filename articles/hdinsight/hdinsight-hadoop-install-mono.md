---
title: "aaaInstall 或更新 HDInsight 的 Azure 上的 Mono |Microsoft 文件"
description: "深入了解如何 toouse Mono 與 HDInsight 叢集的特定版本。 單聲道是以 Linux 為基礎的 HDInsight 叢集上使用的 toorun.NET 應用程式。"
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="b2c75-104">在 HDInsight 上安裝或更新 Mono</span><span class="sxs-lookup"><span data-stu-id="b2c75-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="b2c75-105">深入了解如何 tooinstall 特定版本的[Mono](https://www.mono-project.com) HDInsight 3.4 或更高。</span><span class="sxs-lookup"><span data-stu-id="b2c75-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="b2c75-106">單聲道 HDInsight 3.4 及更新版本中，而且是使用的 toorun.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2c75-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="b2c75-107">如需每個 HDInsight 版本所隨附的 Mono hello 版本資訊，請參閱[HDInsight 的元件版本控制](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="b2c75-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="b2c75-108">tooinstall 您在叢集上，使用 hello 指令碼動作在此文件中的不同版本。</span><span class="sxs-lookup"><span data-stu-id="b2c75-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="b2c75-109">運作方式</span><span class="sxs-lookup"><span data-stu-id="b2c75-109">How it works</span></span>

<span data-ttu-id="b2c75-110">此指令碼接受下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c75-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="b2c75-111">__單聲道的版本號碼__: hello 單聲道 tooinstall 版本。</span><span class="sxs-lookup"><span data-stu-id="b2c75-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="b2c75-112">hello 版本必須是可從[https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/)。</span><span class="sxs-lookup"><span data-stu-id="b2c75-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="b2c75-113">hello 指令碼會安裝下列單聲道套件 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c75-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="b2c75-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="b2c75-114">__mono-complete__</span></span>

* <span data-ttu-id="b2c75-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="b2c75-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="b2c75-116">hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="b2c75-116">hello script</span></span>

<span data-ttu-id="b2c75-117">__指令碼位置__：[https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="b2c75-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="b2c75-118">__需求__：</span><span class="sxs-lookup"><span data-stu-id="b2c75-118">__Requirements__:</span></span>

* <span data-ttu-id="b2c75-119">hello 指令碼必須套用 hello__前端節點__和__背景工作節點__。</span><span class="sxs-lookup"><span data-stu-id="b2c75-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="b2c75-120">toouse hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="b2c75-120">toouse hello script</span></span>

<span data-ttu-id="b2c75-121">如需有關如何 toouse 此指令碼與 HDInsight，請參閱詳細 hello[使用指令碼動作以自訂 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)文件。</span><span class="sxs-lookup"><span data-stu-id="b2c75-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="b2c75-122">您可以使用 hello Azure 入口網站，Azure PowerShell，透過 hello 指令碼或 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="b2c75-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="b2c75-123">雖然下列 hello 指令碼動作的文件，使用下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c75-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="b2c75-124">當使用這個指令碼中設定 HDInsight，將標記為 hello 指令碼做為__Persisted__。</span><span class="sxs-lookup"><span data-stu-id="b2c75-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="b2c75-125">此設定可讓 HDInsight tooapply hello 新增透過調整作業的指令碼 tooworker 節點。</span><span class="sxs-lookup"><span data-stu-id="b2c75-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2c75-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2c75-126">Next steps</span></span>

<span data-ttu-id="b2c75-127">您已經學會如何 tooupgrade 或安裝特定版本的 Mono HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="b2c75-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="b2c75-128">如需有關搭配 Mono HDInsight 上使用.NET 應用程式的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c75-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="b2c75-129">在 HDInsight 上使用 .NET 進行串流 MapReduce</span><span class="sxs-lookup"><span data-stu-id="b2c75-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="b2c75-130">在 HDInsight 上搭配 Hive 與 Pig 使用 .NET</span><span class="sxs-lookup"><span data-stu-id="b2c75-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="b2c75-131">在 HDInsight 上使用 Storm 開發 C# 方案</span><span class="sxs-lookup"><span data-stu-id="b2c75-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="b2c75-132">將.NET 方案移轉 tooLinux 為基礎的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2c75-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="b2c75-133">如需使用指令碼動作的詳細資訊，請參閱[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="b2c75-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>