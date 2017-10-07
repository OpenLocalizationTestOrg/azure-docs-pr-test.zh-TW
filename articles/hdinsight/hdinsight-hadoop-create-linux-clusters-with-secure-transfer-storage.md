---
title: "使用傳輸安全儲存體帳戶的 Azure HDInsight 叢集 aaaCreate Hadoop |Microsoft 文件"
description: "了解與安全傳輸 toocreate HDInsight 叢集如何啟用 Azure 儲存體帳戶。"
keywords: "hadoop 使用者入門,hadoop linux,hadoop 快速入門,安全傳輸,azure 儲存體帳戶"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>在 Azure HDInsight 中使用安全傳輸儲存體帳戶建立 Hadoop 叢集

hello[安全傳輸需要](../storage/common/storage-require-secure-transfer.md)功能增強 hello Azure 儲存體帳戶的安全性，方法是強制所有要求 tooyour 帳戶透過安全的連線。 HDInsight 叢集版本 3.6 版或更新版本才支援這個功能和 hello wasbs 配置。 

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前，您必須具備：

* **Azure 訂用帳戶**: toocreate 免費的一個月試用版帳戶，瀏覽過[azure.microsoft.com/free](https://azure.microsoft.com/free)。
* **已啟用安全傳輸的 Azure 儲存體帳戶**。 Hello 指示，請參閱[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)和[需要安全傳輸](../storage/common/storage-require-secure-transfer.md)。
* **在 hello 儲存體帳戶 Blob 容器**。 
## <a name="create-cluster"></a>建立叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


在本節中，您會在 HDInsight 中使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)建立 Hadoop 叢集。 hello 範本位於[Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/)。 進行本教學課程並不需要具備 Resource Manager 範本經驗。 適用於其他叢集建立方法，並了解本教學課程中使用的 hello 內容，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

1. 按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. 請遵循 hello 指示 toocreate hello 叢集以 hello 下列規格： 

    - 指定 HDInsight 3.6 版。  hello 預設版本為 3.5。 需要 3.6 版或更新版本。
    - 指定已啟用安全傳輸的儲存體帳戶。
    - 使用 hello 儲存體帳戶的簡短名稱。
    - 必須事先建立 hello 儲存體帳戶和 hello blob 容器。 

    Hello 指示，請參閱[建立叢集](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。 

如果您使用指令碼動作 tooprovide 您自己的組態檔，您必須使用 wasbs 在 hello 下列設定：

- fs.defaultFS (core-site)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>新增其他儲存體帳戶

有數個選項 tooadd 額外的安全傳輸啟用儲存體帳戶：

- 修改 hello 最後一節中的 hello Azure Resource Manager 範本。
- 建立叢集使用 hello [Azure 入口網站](https://portal.azure.com)並指定連結的儲存體帳戶。
- 使用指令碼動作 tooadd 額外保護傳輸中啟用儲存體帳戶 tooan 現有 HDInsight 叢集。  如需詳細資訊，請參閱[新增額外的儲存體帳戶 tooHDInsight](hdinsight-hadoop-add-storage.md)。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已經學會如何 toocreate 的 HDInsight 叢集，並啟用安全傳輸 toohello 儲存體帳戶。

toolearn 有關使用 HDInsight，分析資料的詳細資訊，請參閱下列文章 hello:

* toolearn 更多有關搭配使用 Hive 與 HDInsight，包括如何 tooperform Hive 查詢從 Visual Studio，請參閱[使用 Hive 與 HDInsight][hdinsight-use-hive]。
* 關於 Pig toolearn，使用語言 tootransform 資料，請參閱[與 HDInsight 搭配使用 Pig][hdinsight-use-pig]。
* toolearn 有關 MapReduce，方式 toowrite 程式的處理資料的 Hadoop，請參閱[與 HDInsight 的使用 MapReduce][hdinsight-use-mapreduce]。
* 請參閱有關使用 hello HDInsight Tools for Visual Studio tooanalyze 資料在 HDInsight 上 toolearn[開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md)。

深入了解 HDInsight 如何儲存資料的 toolearn 或如何 tooget 至 HDInsight 的資料，請參閱下列文章的 hello:

* 如需有關 HDInsight 如何使用 Azure 儲存體的資訊，請參閱 [搭配 HDInsight 使用 Azure 儲存體](hdinsight-hadoop-use-blob-storage.md)。
* 如需詳細資訊 tooupload 資料 tooHDInsight，請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。

toolearn 進一步了解建立或管理的 HDInsight 叢集，請參閱下列文章 hello:

* toolearn 關於管理您的 Linux 為基礎的 HDInsight 叢集，請參閱[使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。
* toolearn 進一步了解 hello 選項，您可以選取當建立 HDInsight 叢集，請參閱[建立使用自訂選項的 Linux 的 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)。
* 如果您熟悉 Linux 及 Hadoop，但是想 tooknow 特點 Hadoop hello HDInsight 上的時，請參閱[Linux 上使用 HDInsight](hdinsight-hadoop-linux-information.md)。 本文提供的資訊如下：
  
  * 裝載在 hello 叢集上，例如 Ambari 和 WebHCat 服務的 Url
  * hello 位置的 Hadoop 檔案與 hello 本機檔案系統上的範例
  * hello 使用的 Azure 儲存體 (WASB) 而不是 HDFS 做 hello 預設資料存放區

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


