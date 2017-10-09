---
title: "aaaAccess Hadoop YARN 應用程式登入以 Linux 為基礎的 HDInsight 的 Azure |Microsoft 文件"
description: "了解 tooaccess YARN 應用程式登入使用命令列 hello 和網頁瀏覽器以 Linux 為基礎的 HDInsight (Hadoop) 叢集的方式。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>存取以 Linux 為基礎之 HDInsight 上的 YARN 應用程式記錄

了解如何 tooaccess hello YARN （尚未另一個資源交涉器） 在 Azure HDInsight Hadoop 叢集上的應用程式記錄檔。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="YARNTimelineServer"></a>YARN Timeline Server

hello [YARN 時間表伺服器](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html)完成的應用程式與透過兩個不同介面的架構特定應用程式資訊提供一般資訊。 具體而言：

* 儲存及擷取 HDInsight 叢集上泛型應用程式資訊的功能已在版本 3.1.1.374 或更新版本上啟用。
* 無法 HDInsight 叢集上目前可用的 hello 時間表伺服器 hello 架構特定應用程式資訊的元件。

應用程式的一般資訊包含下列資料類型的 hello:

* hello 應用程式識別碼，應用程式的唯一識別碼
* 啟動 hello 應用程式的 hello 使用者
* 資訊在嘗試進行 toocomplete hello 應用程式
* 使用指定的應用程式的任何嘗試 hello 容器

## <a name="YARNAppsAndLogs"></a>YARN 應用程式和記錄檔

YARN 藉由將資源管理從應用程式排程/監視分離，支援多種程式設計模型 (MapReduce 為其中之一)。 YARN 使用全域 *ResourceManager* (RM)、每一背景工作節點 *ResourceManager* (NM) 及每一應用程式 *ResourceManager* (AM)。 hello AM 每個應用程式會交涉資源 （CPU、 記憶體、 磁碟、 網路） hello RM 中執行您的應用程式 hello RM 搭配 NMs toogrant 做為被授與這些資源*容器*。 hello AM 負責追蹤 hello RM hello 分派容器 tooit hello 進度 應用程式可能需要根據 hello 本質 hello 應用程式的許多容器。

每個應用程式都可能包含多個「應用程式嘗試」。 如果應用程式失敗，系統可能會以新的嘗試來重試它。 每個嘗試都在容器中執行。 某方面來說，容器會提供基本的 YARN 應用程式所執行的工作單位的 hello 內容。 完成 hello 內容的容器內的所有工作是在哪一個 hello 配置容器的 hello 單一背景工作節點上都執行。 請參閱 [YARN 概念][YARN-concepts]，以取得進一步的參考資料。

應用程式記錄檔 （及相關聯的 hello 容器記錄） 在中不可或缺偵錯問題的 Hadoop 應用程式。 YARN 所提供的不錯的架構，用於收集、 彙總，並儲存應用程式記錄檔以 hello[記錄彙總][ log-aggregation]功能。 hello 記錄彙總功能可讓您更具決定性存取應用程式記錄檔。 它能彙總背景工作節點上所有容器的記錄檔，並將它們依每個背景工作節點儲存成單一彙總記錄檔。 hello 記錄會儲存在 hello 預設的檔案系統上，應用程式完成之後。 您的應用程式可能會使用數百或數千個容器，但記錄檔的單一工作者節點上執行的所有容器一律彙總的 tooa 單一檔案。 因此，應用程式使用的每一背景工作節點只會有 1 個記錄。 根據預設，HDInsight 叢集 3.0 版和更新版本上會啟用記錄彙總。 彙總的記錄檔位於預設儲存體 hello 叢集。 下列路徑的 hello 是 hello HDFS 路徑 toohello 記錄檔：

    /app-logs/<user>/logs/<applicationId>

在 hello 路徑`user`hello 啟動 hello 應用程式的 hello 使用者名稱。 hello`applicationId`是 hello hello YARN RM 所指派的唯一識別碼 tooan 應用程式

hello 彙總的記錄檔並未直接讀取，它們會以撰寫[TFile][T-file]，[二進位格式][ binary-format]容器以編製索引。 使用的 hello YARN ResourceManager 記錄或 CLI 工具 tooview 這些記錄檔以純文字的應用程式或感興趣的容器。

## <a name="yarn-cli-tools"></a>YARN CLI 工具

toouse hello YARN CLI 工具 中，您必須先連接使用 SSH toohello HDInsight 叢集。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

您可以執行其中一種 hello 下列命令，以純文字檢視這些記錄檔：

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

指定 hello &lt;applicationId >，&lt;使用者-使用者-啟動-應用程式 >， &lt;containerId >，並&lt;背景工作節點位址 > 時執行這些命令的資訊。

## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager UI

hello YARN ResourceManager UI 會 hello 叢集前端節點上執行。 它是透過 hello Ambari web UI 存取。 使用下列步驟 tooview hello YARN 的 hello 記錄：

1. 在網頁瀏覽器，瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net。 CLUSTERNAME 取代 hello 的 HDInsight 叢集的名稱。
2. 從 hello hello 左側的服務清單，選取**YARN**。

    ![選取的 Yarn 服務](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. 從 hello**快速連結**下拉式清單中，選取一個 hello 叢集前端節點，然後選取**ResourceManager 記錄**。

    ![Yarn 快速連結](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    您會看到一份連結 tooYARN 記錄檔。

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
