---
title: "aaaAccess Hadoop YARN 應用程式以程式設計方式-記錄 Azure |Microsoft 文件"
description: "在 HDInsight 中的 Hadoop 叢集上以程式設計方式存取應用程式記錄檔"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>存取以 Windows 為基礎之 HDInsight 上的 YARN 應用程式記錄
本主題說明如何 tooaccess hello 完 Azure HDInsight 中的 Windows 架構的 Hadoop 叢集的 YARN （尚未另一個資源交涉器） 應用程式記錄檔

> [!IMPORTANT]
> 本文件中的 hello 資訊適用於僅 tooWindows 為基礎的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 如需存取 Linux 之 HDInsight 叢集上 YARN 記錄檔的相關資訊，請參閱 [在 HDInsight 中的 Linux 之 Hadoop 上存取 YARN 應用程式記錄檔](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>必要條件
* Windows 型 HDInsight 叢集。  請參閱 [在 HDInsight 中建立 Windows 型 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

## <a name="yarn-timeline-server"></a>YARN Timeline Server
hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN 時間表伺服器</a>上完成的應用程式透過兩個不同的介面以及為特定架構應用程式資訊提供一般資訊。 具體而言：

* 儲存及擷取 HDInsight 叢集上泛型應用程式資訊的功能已在版本 3.1.1.374 或更新版本上啟用。
* 無法 HDInsight 叢集上目前可用的 hello 時間表伺服器 hello 架構特定應用程式資訊的元件。

應用程式的一般資訊包含下列排序的資料的 hello:

* hello 應用程式識別碼，應用程式的唯一識別碼
* 啟動 hello 應用程式的 hello 使用者
* 資訊在嘗試進行 toocomplete hello 應用程式
* 使用指定的應用程式的任何嘗試 hello 容器

在您的 HDInsight 叢集，此資訊將會儲存 hello 預設 Azure 儲存體帳戶的預設容器中的 Azure Resource Manager tooa 記錄存放區。 透過 REST API 即可抓取這項已完成之應用程式的相關泛型資料：

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>YARN 應用程式和記錄檔
YARN 藉由將資源管理從應用程式排程/監視分離，支援多種程式設計模型 (MapReduce 為其中之一)。 這是透過全域 *ResourceManager* (RM)、每一背景工作節點 *ResourceManager* (NM) 及每一應用程式 *ResourceManager* (AM) 來達成。 hello AM 每個應用程式會交涉資源 （CPU、 記憶體、 磁碟、 網路） hello RM 中執行您的應用程式 hello RM 搭配 NMs toogrant 做為被授與這些資源*容器*。 hello AM 負責追蹤 hello RM hello 分派容器 tooit hello 進度 應用程式可能需要根據 hello 本質 hello 應用程式的許多容器。

此外，每個應用程式可能包含多個*應用程式嘗試*在 hello 是否存在的當機或 toohello 遺失 AM 之間的通訊中的順序 toofinish 和 RM 因此，容器會授與應用程式的 tooa 特定嘗試。 某方面來說，容器會提供基本 YARN 應用程式所執行的工作單位的 hello 內容且完成 hello 內容的容器內的所有工作上都執行 hello 單一背景工作節點的 hello 配置容器。 請參閱 [YARN 概念][YARN-concepts]，以取得進一步的參考資料。

應用程式記錄檔 （及相關聯的 hello 容器記錄） 在中不可或缺偵錯問題的 Hadoop 應用程式。 YARN 所提供的不錯的架構，用於收集、 彙總，並儲存應用程式記錄檔以 hello[記錄彙總][ log-aggregation]功能。 hello 記錄彙總功能可讓存取的應用程式記錄檔更具決定性，因為它會彙總的背景工作節點上的所有容器的記錄檔並將它們儲存為一個彙總記錄檔每個背景工作節點 hello 預設檔案系統上，應用程式完成之後。 您的應用程式可能會使用數百或數千個容器，但在單一的背景工作節點上執行的所有容器的記錄檔就會永遠彙總的 tooa 單一檔案，導致每個應用程式所使用的背景工作節點建立一個記錄檔。 HDInsight 叢集上的預設會啟用記錄檔彙總 (3.0 版和更新版本)，並彙總的記錄檔可以找到您的叢集，在下列位置的 hello hello 預設容器中：

    wasb:///app-logs/<user>/logs/<applicationId>

在該位置，*使用者*hello hello 啟動 hello 應用程式，使用者名稱和*applicationId* hello YARN RM 指派為 hello 的應用程式的唯一識別碼

hello 彙總的記錄檔並未直接讀取，它們會以撰寫[TFile][T-file]，[二進位格式][ binary-format]容器以編製索引。 YARN 提供 CLI 工具 toodump 這些記錄檔以純文字的應用程式或感興趣的容器。 您可以執行其中一種 hello 之後直接在 hello 叢集節點上的 YARN 命令 （之後透過 RDP 連線 tooit），以純文字檢視這些記錄檔：

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager UI
hello YARN ResourceManager UI hello 叢集叢集前端節點上執行，而且可以存取透過 Azure 入口網站的儀表板 hello:

1. 登入太[Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 左窗格中，按一下 **瀏覽**，按一下  **HDInsight 叢集**，按一下您想 tooaccess hello YARN 應用程式記錄檔的 windows 叢集。
3. 在 hello 上方功能表中，按一下 **儀表板**。 您會看到有頁面在新的瀏覽器索引標籤上開啟，其名稱為 **HDInsight 查詢主控台**。
4. 在 [HDInsight 查詢主控台] 上，按一下 [Yarn UI]。

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
