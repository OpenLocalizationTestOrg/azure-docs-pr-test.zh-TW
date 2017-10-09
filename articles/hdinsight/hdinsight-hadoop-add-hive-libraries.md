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
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>建立 HDInsight 叢集時新增自訂 Hive 程式庫

如果您有與 HDInsight 上的登錄區經常使用的程式庫，這份文件會包含有關在叢集建立期間使用的指令碼動作 toopre 負載 hello 程式庫。 登錄區中，使用這份文件中的 hello 步驟加入的程式庫供全域使用-沒有任何需要 toouse[新增 JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload 它們。

## <a name="how-it-works"></a>運作方式

在建立叢集時，您可以選擇性地指定一個 hello 叢集節點執行指令碼，在建立時的指令碼動作。 這份文件中的 hello 指令碼會接受單一參數，這是包含預先載入的 hello （儲存為 jar 檔案） 的程式庫 toobe WASB 位置。

在叢集建立期間 hello 指令碼列舉 hello 檔案、 將其複製 toohello`/usr/lib/customhivelibs/`目錄標頭和背景工作節點，然後將它們新增 toohello`hive.aux.jars.path`屬性在 hello`core-site.xml`檔案。 在以 Linux 為基礎的叢集，它也會更新 hello `hive-env.sh` hello hello 檔案位置的檔案。

> [!NOTE]
> 使用本文章中的 hello 指令碼動作 hello 程式庫可讓在 hello 下列案例：
>
> * **以 Linux 為基礎的 HDInsight** -時使用 hello Hive 用戶端**WebHCat**，和**HiveServer2**。
> * **Windows 為基礎的 HDInsight** -時使用 hello Hive 用戶端和**WebHCat**。

## <a name="hello-script"></a>hello 指令碼

**指令碼位置**

**以 Linux 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

**以 Windows 為基礎的叢集**：[https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

**需求**

* hello 指令碼必須可套用的 tooboth hello**前端節點**和**背景工作節點**。

* （每瓶) 您希望 tooinstall 必須儲存在 Azure Blob 儲存體中的 hello**單一容器**。

* hello 包含 jar 檔案的 hello 程式庫的儲存體帳戶**必須**是建立連結的 toohello HDInsight 叢集。 它必須是 hello 預設儲存體帳戶，或透過加入帳戶__選擇性組態__。

* hello WASB 路徑 toohello 容器必須指定為參數 toohello 指令碼動作。 例如，如果 hello （每瓶） 會儲存在名為的容器**程式庫**儲存體帳戶上名為**mystorage**，hello 參數便是 **wasb://libs@mystorage.blob.core.windows.net/** 。

  > [!NOTE]
  > 本文件假設您有已建立儲存體帳戶、 blob 容器和上傳的 hello 檔案 tooit。
  >
  > 如果您尚未建立儲存體帳戶，您可以透過 hello [Azure 入口網站](https://portal.azure.com)。 然後您可以使用公用程式例如[Azure 儲存體總管](http://storageexplorer.com/)toocreate 容器中 hello 帳戶和上傳的檔案 tooit。

## <a name="create-a-cluster-using-hello-script"></a>使用 hello 指令碼建立叢集

> [!NOTE]
> hello 下列步驟建立以 Linux 為基礎的 HDInsight 叢集。 toocreate Windows 為基礎的叢集上，選取**Windows** hello 與叢集作業系統建立 hello 叢集時，並使用 hello Windows (PowerShell) 指令碼，而不是 hello bash 指令碼。
>
> 您也可以使用 Azure PowerShell 或 hello HDInsight.NET SDK toocreate 使用此指令碼的叢集。 如需使用這些方法的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

1. 開始使用中的 hello 步驟佈建叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)，但是不完成佈建。

2. 在 hello**選擇性組態**刀鋒視窗中，選取**指令碼動作**，並提供下列資訊的 hello:

   * **名稱**： 輸入 hello 指令碼動作的易記名稱。

   * **SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**：勾選此選項。

   * **WORKER**：勾選此選項。

   * **ZOOKEEPER**：將此選項保留空白。

   * **參數**： 輸入 hello WASB 位址 toohello 容器和儲存體帳戶包含 hello （每瓶）。 例如：**wasb://libs@mystorage.blob.core.windows.net/**。

3. 在 hello 底部 hello**指令碼動作**，使用 hello**選取**按鈕 toosave hello 組態。

4. 在 hello**選擇性組態**刀鋒視窗中，選取**連結儲存體帳戶**和選取 hello**新增儲存體金鑰**連結。 選取包含 hello （每瓶），hello 儲存體帳戶，然後使用 hello**選取**按鈕 toosave 設定和傳回 hello**選擇性組態**刀鋒視窗。

5. 使用 hello**選取**在 hello hello 底部的按鈕**選擇性組態**刀鋒視窗 toosave hello 選擇性的組態資訊。

6. 繼續中所述，佈建 hello 叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)。

一旦叢集建立完成時，您就可以 toouse hello （每瓶） 從 Hive 加入到此指令碼而不需要 toouse hello`ADD JAR`陳述式。

## <a name="next-steps"></a>後續步驟

如需有關使用 Hive 的詳細資訊，請參閱 [搭配使用 Hive 與 HDInsight](hdinsight-use-hive.md)
