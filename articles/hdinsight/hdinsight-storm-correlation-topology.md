---
title: "經過一段時間 Storm 與 HDInsight 上的 HBase aaaCorrelate 事件"
description: "深入了解如何在不同的時間到達 HDInsight 上使用 Storm 和 HBase toocorrelate 事件。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>在不同時間使用 Storm 和 HBase 抵達的事件相互關聯

搭配 Apache Store 使用永續性資料存放區，可以讓在不同時間抵達的資料項目相互關聯。 例如，持續時間 hello 工作階段如何連結登入和登出使用者工作階段 toocalculate 事件。

在本文件中，您將學習如何 toocreate 基本的 C# Storm 拓撲可為使用者工作階段，追蹤登入和登出事件，並計算 hello hello 工作階段持續時間。 hello 拓撲使用 HBase 做為永續性資料存放區。 HBase 也允許您 tooperform 批次的查詢 hello 歷程記錄資料 tooproduce 額外的見解。 例如，在特定時間週期內已開始或結束多少個使用者工作階段。

## <a name="prerequisites"></a>必要條件

* Visual Studio 和 hello HDInsight tools for Visual Studio。 如需詳細資訊，請參閱[開始使用 hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。

* Apache Storm on HDInsight 叢集 (Windows)。

  > [!WARNING]
  > 在 2016 年 10 月 28 之後建立的 linux Storm 叢集上支援 SCP.NET 拓撲，而.NET 套件總 2016 年 10 月 28 可 hello HBase SDK 不上無法正常運作以 Linux 為基礎的 HDInsight

* Apache HBase on HDInsight 叢集 (Linux 或 Windows 型)。

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* 開發環境為 [Java](https://java.com) 1.7 或更新版本。 Java 是使用的 toopackage hello 拓撲時送出的 toohello HDInsight 叢集。

  * hello **JAVA_HOME**包含 Java 的環境變數必須點 toohello 目錄。
  * hello **%JAVA_HOME%/bin**目錄必須位於 hello 路徑

## <a name="architecture"></a>架構

![透過 hello 拓撲 hello 資料流程的圖表](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

相互關聯事件需要通用識別碼 hello 事件來源。 例如，使用者識別碼、 工作階段識別碼或其他的資料，是） 唯一且 b） 中包含所有的資料傳送 tooStorm。 這個範例會使用 GUID 值 toorepresent 工作階段識別碼。

此範例包含兩個 HDInsight 叢集：

* HBase：歷程記錄資料的持續性資料存放區
* Storm： 使用 tooingest 內送資料

hello 資料 hello Storm 拓樸，隨機產生，而且包含下列項目 hello:

* 工作階段識別碼：可唯一識別每個工作階段的 GUID
* 事件：START 或 END 事件。 在此範例中，START 一律發生於 END 之前
* Hello 事件時間： hello 時間。

此資料已處理並儲存在 HBase 中。

### <a name="storm-topology"></a>Storm 拓撲

當工作階段啟動時，**啟動**事件收到 hello 拓樸和記錄 tooHBase。 當**結束**收到事件時，會擷取 hello 拓撲 hello**啟動**事件並計算 hello hello 兩個事件之間的時間。 這**持續時間**值接著會儲存在 HBase 以及 hello**結束**事件資訊。

> [!IMPORTANT]
> 雖然此拓撲會示範 hello 基本模式，生產環境方案需要 tootake 設計 hello 下列案例：
>
> * 未按順序抵達的事件
> * 重複的事件
> * 卸除的事件

hello 範例拓撲是由 hello 下列元件組成：

* Session.cs： 建立隨機的工作階段識別碼，開始時間，以及多久 hello 工作階段的持續時間來模擬使用者工作階段。

* Spout.cs： 建立 100 個工作階段、 發出的開始事件、 hello 隨機逾時等候每個工作階段，並接著發出結束事件。 然後回收結束工作階段 toogenerate 新的。

* HBaseLookupBolt.cs： 使用 hello 工作階段識別碼 toolook HBase 從工作階段資訊。 當處理結束事件時，它會尋找 hello 對應的開始事件，並計算 hello hello 工作階段持續時間。

* HBaseBolt.cs：將資訊儲存在 HBase 中。

* 類型轉換時讀取 / 寫入 tooHBase TypeHelper.cs： 幫助。

### <a name="hbase-schema"></a>HBase 結構描述

Hbase，hello 資料會儲存在資料表具有下列結構描述/設定 hello:

* 資料列索引鍵： 做為此資料表中的資料列的 hello 索引鍵使用識別碼 hello 工作階段。

* 資料欄系列： hello 系列名稱為 'cf'。 儲存在此系列中的資料行如下：

  * 事件：START 或 END。

  * 時間： hello 時間，以毫秒為單位的 hello 事件發生。

  * 持續時間： hello 開始和結束事件之間的長度。

* 版本： hello 'cf' 家族設定 tooretain 5 每個資料列版本。

  > [!NOTE]
  > 版本是針對特定資料列索引鍵儲存的先前值的記錄檔。 根據預設，HBase 只會傳回 hello hello 最新版本資料列的值。 在此情況下，hello 相同的資料列用於所有事件 （啟動，end） 資料列的每個版本由 hello 時間戳記值。 版本可提供針對特定識別碼記錄之事件的歷程記錄檢視。

## <a name="download-hello-project"></a>下載 hello 專案

您可以從下載 hello 範例專案[https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation)。

此下載項目包含下列 C# 專案中的 hello:

* CorrelationTopology：針對使用者工作階段隨機發出開始與結束事件的 C# Storm 拓撲。 每個工作階段持續 1 到 5 分鐘。

* SessionInfo: C# 主控台應用程式建立 hello HBase 資料表，並提供範例查詢 tooreturn 儲存的工作階段資料的資訊。

## <a name="create-hello-table"></a>建立 hello 資料表

1. 開啟 hello **SessionInfo** Visual Studio 專案中的。

2. 在**方案總管 中**，以滑鼠右鍵按一下 hello **SessionInfo**專案，然後選取**屬性**。

    ![已選取屬性的功能表螢幕擷取畫面](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. 選取**設定**，然後設定 hello 下列值：

   * HBaseClusterURL: hello URL tooyour HBase 叢集。 例如，https://myhbasecluster.azurehdinsight.net。

   * 針對您的叢集 HBaseClusterUserName: hello admin/HTTP 使用者帳戶

   * HBaseClusterPassword: hello hello admin/HTTP 使用者帳戶密碼

   * HBaseTableName: hello 名稱的這個範例與 hello 資料表 toouse

   * HBaseTableColumnFamily: hello 欄系列名稱

     ![設定對話方塊的影像](./media/hdinsight-storm-correlation-topology/settings.png)

4. 執行 hello 解決方案。 出現提示時，選取 hello 'c' 索引鍵 toocreate hello 資料表 HBase 叢集上。

## <a name="build-and-deploy-hello-storm-topology"></a>建置和部署 hello Storm 拓樸

1. 開啟 hello **CorrelationTopology** Visual Studio 中的方案。

2. 在**方案總管 中**，以滑鼠右鍵按一下 hello **CorrelationTopology**專案，然後選取內容。

3. 在 [hello 屬性] 視窗中選取**設定**，然後輸入 hello 組態值，這個專案。 hello 前 5 是的 hello 使用相同的值由 hello **SessionInfo**專案：

   * HBaseClusterURL: hello URL tooyour HBase 叢集。 例如，https://myhbasecluster.azurehdinsight.net。

   * HBaseClusterUserName: hello admin/HTTP 使用者帳戶用於您的叢集。

   * HBaseClusterPassword: hello hello admin/HTTP 使用者帳戶的密碼。

   * 此範例與 hello 資料表 toouse HBaseTableName: hello 名稱。 此值為 hello 相同 hello SessionInfo 專案中所使用的資料表名稱。

   * HBaseTableColumnFamily: hello 欄系列名稱。 此值為 hello 相同 hello SessionInfo 專案中所使用的資料行的系列名稱。

   > [!IMPORTANT]
   > 請勿變更 hello HBaseTableColumnNames，因為 hello 預設值是所使用的 hello 名稱**SessionInfo** tooretrieve 資料。

4. 儲存 hello 屬性，然後建置 hello 專案。

5. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。 如果出現提示，請輸入您的 Azure 訂閱 hello 認證。

   ![映像的 hello 提交 toostorm 功能表項目](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. 在 hello**提交拓撲**對話方塊中，您想要此拓撲 toodeploy 選取 hello Storm 叢集。

   > [!NOTE]
   > hello 第一次提交拓撲，可能需要幾秒鐘的時間 tooretrieve hello 您的 HDInsight 叢集名稱。

7. 一旦 hello 拓撲已上傳和提交 toohello 叢集，hello **Storm 拓撲檢視**會開啟並顯示 hello 執行拓樸。 toorefresh hello 資料選取 hello **CorrelationTopology**並用 hello 重新整理 按鈕在 hello hello 頁面的右上方。

   ![映像的 hello 拓撲檢視](./media/hdinsight-storm-correlation-topology/topologyview.png)

   當 hello 拓樸開始產生資料時，hello 中 hello 值**Emitted**資料行遞增。

   > [!NOTE]
   > 如果 hello **Storm 拓撲檢視**不會自動開啟，請使用它 hello 步驟 tooopen 下列：
   >
   > 1. 在 [方案總管] 中，展開 **Azure**，然後展開 **HDInsight**。
   > 2. Hello 拓撲以滑鼠右鍵按一下 hello Storm 叢集會在上執行，然後選取**檢視 Storm 拓撲**

## <a name="query-hello-data"></a>查詢 hello 資料

一旦已發出資料，使用下列步驟 tooquery hello 資料 hello。

1. 傳回 toohello **SessionInfo**專案。 如果不在執行中，請啟動它的新執行個體。

2. 出現提示時，選取**s** toosearch 開始事件。 您會提示的 tooenter 開始和結束時間 toodefine 時間範圍-會傳回這兩個時間之間的唯一事件。

    使用 hello 下列格式輸入 hello 開始和結束時間： hh: mm 和 'm' 或 'pm'。 例如，11:20pm。

    tooreturn 記錄事件，會使用 hello Storm 部署拓撲之前, 從開始時間和結束時間為現在。 hello 傳回的資料包含下列文字的項目類似 toohello:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

正在搜尋的結束事件 works hello 相同做為開始事件。 不過，結束事件是隨機產生的 hello 開始事件之後的 1 到 5 分鐘之間。 您可能需要一些時間範圍 toofind hello 結束事件 tootry。 結束事件也包含 hello 持續時間的 hello 工作階段-hello hello 開始事件時間和結束事件時間之間的差異。 以下是 END 事件的資料範例：

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> 雖然您輸入的 hello 時間值以本地時間，從 hello 查詢傳回的 hello 時間是使用 utc 格式。

## <a name="stop-hello-topology"></a>停止 hello 拓樸

當您準備好 toostop hello 拓撲時，傳回 toohello **CorrelationTopology** Visual Studio 專案中的。 在 hello **Storm 拓撲檢視**選取 hello 拓樸，然後使用 hello **Kill**在 hello hello 拓撲檢視頂端的按鈕。

## <a name="delete-your-cluster"></a>刪除叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>後續步驟

如需更多 Storm 範例，請參閱 [Storm on HDInsight 上的範例拓撲](hdinsight-storm-example-topology.md)。
