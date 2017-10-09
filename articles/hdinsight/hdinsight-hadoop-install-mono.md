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
# <a name="install-or-update-mono-on-hdinsight"></a>在 HDInsight 上安裝或更新 Mono

深入了解如何 tooinstall 特定版本的[Mono](https://www.mono-project.com) HDInsight 3.4 或更高。

單聲道 HDInsight 3.4 及更新版本中，而且是使用的 toorun.NET 應用程式。 如需每個 HDInsight 版本所隨附的 Mono hello 版本資訊，請參閱[HDInsight 的元件版本控制](hdinsight-component-versioning.md)。 tooinstall 您在叢集上，使用 hello 指令碼動作在此文件中的不同版本。 

## <a name="how-it-works"></a>運作方式

此指令碼接受下列參數的 hello:

* __單聲道的版本號碼__: hello 單聲道 tooinstall 版本。 hello 版本必須是可從[https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/)。

hello 指令碼會安裝下列單聲道套件 hello:

* __mono-complete__

* __ca-certificates-mono__

## <a name="hello-script"></a>hello 指令碼

__指令碼位置__：[https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__需求__：

* hello 指令碼必須套用 hello__前端節點__和__背景工作節點__。

## <a name="toouse-hello-script"></a>toouse hello 指令碼

如需有關如何 toouse 此指令碼與 HDInsight，請參閱詳細 hello[使用指令碼動作以自訂 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)文件。 您可以使用 hello Azure 入口網站，Azure PowerShell，透過 hello 指令碼或 hello Azure CLI。

雖然下列 hello 指令碼動作的文件，使用下列 URI 的 hello:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> 當使用這個指令碼中設定 HDInsight，將標記為 hello 指令碼做為__Persisted__。 此設定可讓 HDInsight tooapply hello 新增透過調整作業的指令碼 tooworker 節點。


## <a name="next-steps"></a>後續步驟

您已經學會如何 tooupgrade 或安裝特定版本的 Mono HDInsight 上。 如需有關搭配 Mono HDInsight 上使用.NET 應用程式的詳細資訊，請參閱下列文件的 hello:

* [在 HDInsight 上使用 .NET 進行串流 MapReduce](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [在 HDInsight 上搭配 Hive 與 Pig 使用 .NET](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [在 HDInsight 上使用 Storm 開發 C# 方案](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [將.NET 方案移轉 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

如需使用指令碼動作的詳細資訊，請參閱[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)