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
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>建立 HDInsight 叢集時新增自訂 Hive 程式庫

如果您有與 HDInsight 上的 Hive 經常一起使用的程式庫，本文件包含在叢集建立期間使用指令碼動作來預先載入程式庫的詳細資訊。 使用本文件步驟新增的程式庫在 Hive 中為全域可用 - 不需要使用 [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) 載入它們。

## <a name="how-it-works"></a>運作方式

建立叢集時，您可以選擇性地指定指令碼動作，以便在建立叢集節點時在節點上執行指令碼。 本文件中的指令碼接受單一參數，也就是包含要預先載入程式庫 (儲存為 jar 檔案) 的 WASB 位置。

叢集建立期間，指令碼會列舉檔案、將它們複製到前端和背景工作節點上的 `/usr/lib/customhivelibs/` 目錄，然後將它們加入至 `core-site.xml` 檔案中的 `hive.aux.jars.path` 屬性。 在以 Linux 為基礎的叢集上，它也會以檔案的位置來更新 `hive-env.sh` 檔案。

> [!NOTE]
> 使用本文中的指令碼動作可讓程式庫在下列案例中可供使用：
>
> * **以 Linux 為基礎的 HDInsight** - 使用 Hive 用戶端、**WebHCat** 和 **HiveServer2** 時。
> * **以 Windows 為基礎的 HDInsight** - 使用 Hive 用戶端和 **WebHCat** 時。

## <a name="the-script"></a>指令碼

**指令碼位置**

**以 Linux 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

**以 Windows 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

**需求**

* 指令碼必須同時套用至**前端節點**和**背景工作節點**。

* 您想要安裝的 jar 必須儲存在**單一容器**中的 Azure Blob 儲存體。

* 包含 jar 檔案程式庫的儲存體帳戶**必須**在建立期間連結至 HDInsight 叢集。 它必須是預設的儲存體帳戶，或是透過__選擇性組態__新增的帳戶。

* 必須指定容器的 WASB 路徑做為指令碼動作的參數。 例如，如果 jar 儲存在名為 **mystorage** 的儲存體帳戶上稱為 **libs** 的容器中，則這個參數會是 **wasb://libs@mystorage.blob.core.windows.net/**。

  > [!NOTE]
  > 本文件假設您已建立儲存體帳戶、blob 容器，也已將檔案上傳給它。
  >
  > 如果您尚未建立儲存體帳戶，您可以透過 [Azure 入口網站](https://portal.azure.com)來建立。 接著，您可以使用 [Azure 儲存體 Explorer](http://storageexplorer.com/) 之類的公用程式，在帳戶中建立容器，並將檔案上傳至其中。

## <a name="create-a-cluster-using-the-script"></a>使用指令碼建立叢集

> [!NOTE]
> 下列步驟會建立以 Linux 為基礎的 HDInsight 叢集。 若要建立以 Windows 為基礎的叢集，請在建立叢集時選取 **Windows** 作為叢集作業系統，並使用 Windows (PowerShell) 指令碼，而不是 bash 指令碼。
>
> 您也可以使用 Azure PowerShell 或 HDInsight .NET SDK，以使用此指令碼建立叢集。 如需使用這些方法的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

1. 使用[在 Linux 上佈建 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的步驟開始佈建叢集，但是不完成佈建。

2. 在 [選用組態] 刀鋒視窗中，選取 [指令碼動作]，並提供下列資訊：

   * **名稱**：輸入指令碼動作的易記名稱。

   * **SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**：勾選此選項。

   * **WORKER**：勾選此選項。

   * **ZOOKEEPER**：將此選項保留空白。

   * **參數**：輸入包含 jar 的容器和儲存體帳戶的 WASB 位址。 例如：**wasb://libs@mystorage.blob.core.windows.net/**。

3. 在 [指令碼動作] 底部，使用 [選取] 按鈕以儲存組態。

4. 在 [選擇性組態] 刀鋒視窗中，選取 [連結的儲存體帳戶]，然後選取 [新增儲存體金鑰] 連結。 選取包含 jar 的儲存體帳戶，然後使用 [選取] 按鈕來儲存設定，並回到 [選擇性組態] 刀鋒視窗。

5. 使用 [選擇性組態] 刀鋒視窗底部的 [選取] 按鈕，儲存選擇性組態資訊。

6. 繼續如[在 Linux 上佈建 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)中所述佈建叢集。

建立叢集完成後，您就能夠從 Hive 使用透過此指令碼新增的 jar，而不需使用 `ADD JAR` 陳述式。

## <a name="next-steps"></a>後續步驟

如需有關使用 Hive 的詳細資訊，請參閱 [搭配使用 Hive 與 HDInsight](hdinsight-use-hive.md)
