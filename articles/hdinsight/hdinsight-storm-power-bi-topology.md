---
title: "使用 Power BI 的 Azure HDInsight Apache Storm aaaUse |Microsoft 文件"
description: "使用來自 HDInsight 中的 Apache Storm 叢集上執行的 C# 拓撲的資料建立 Power BI。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>使用 Power BI toovisualize 資料從 Apache Storm 拓樸

Power BI 可讓您 toovisually 顯示的資料與報表。 本文件提供的範例 toouse Apache Storm 的 Power BI 的 HDInsight toogenerate 資料。

> [!NOTE]
> hello 本文件中的步驟會仰賴 Windows 與 Visual Studio 開發環境。 hello 已編譯的專案可以提交的 tooa 以 Linux 為基礎的 HDInsight 叢集。 只有在 2016/10/28 之後建立的以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。
>
> toouse 以 Linux 為基礎的叢集，而更新 hello Microsoft.SCP.Net.SDK NuGet 封裝使用您的專案 tooversion 0.10.0.6 或更高版本的 C# 拓撲。 hello hello 封裝版本也必須符合安裝在 HDInsight 上的 Storm hello 主要版本。 例如，Storm on HDInsight 3.3 和 3.4 版使用 Storm 0.10.x 版，而 HDInsight 3.5 使用 Storm 1.0.x。
>
> C# 拓撲以 Linux 為基礎的叢集上必須使用.NET 4.5，並使用單聲道 toorun hello HDInsight 叢集上。 大多能正常運作。 不過，您應該檢查 hello [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/)潛在的不相容的文件。
>
> 如需此專案的 Java 版本 (可在以 Linux 或 Windows 為基礎的 HDInsight 上運作)，請參閱[使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](hdinsight-storm-develop-java-event-hub-topology.md)。

## <a name="prerequisites"></a>必要條件

* 具備 [Power BI](https://powerbi.com) 存取權的 Azure Active Directory 使用者。
* HDInsight 叢集。 如需詳細資訊，請參閱[開始使用 Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md)。

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* Visual Studio （其中 hello 之後版本）

  * [Visual Studio 2012](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (任何版本)

* hello HDInsight Tools for Visual Studio： 請參閱[開始使用 hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)如需安裝資訊。

## <a name="how-it-works"></a>運作方式

此範例包含 C# Storm 拓撲，會隨機產生網際網路資訊服務 (IIS) 記錄資料。 接著會將這項資料寫入 tooa SQL 資料庫，而且從該處使用的 toogenerate Power BI 中的報表。

hello 遵循此範例的檔案實作 hello 主要功能：

* **SqlAzureBolt.cs**： 寫入 hello Storm 拓撲 tooSQL 資料庫中產生的資訊。
* **IISLogsTable.sql**: hello TRANSACT-SQL 陳述式使用 toogenerate hello 儲存資料庫的 hello 資料中。

> [!WARNING]
> 建立 SQL Database 中的 hello 資料表，才可以開始您的 HDInsight 叢集 hello 拓撲。

## <a name="download-hello-example"></a>下載 hello 範例

下載 hello [HDInsight C# Storm Power BI 範例](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi)。 toodownload，是分叉/複製使用[git](http://git-scm.com/)，或使用 hello**下載**連結 toodownload hello 封存的.zip。

## <a name="create-a-database"></a>建立資料庫

1. toocreate 資料庫中，使用 hello hello 步驟[SQL Database 教學課程](../sql-database/sql-database-get-started.md)文件。

2. 下列 hello 連接 toohello 資料庫步驟 hello [tooa SQL 資料庫連接使用 Visual Studio](../sql-database/sql-database-connect-query.md)文件。

3. 在 [物件總管] 中，以滑鼠右鍵按一下 hello 資料庫，然後選取**新查詢**。 貼上 hello hello 內容**IISLogsTable.sql**檔案包含在 hello hello 查詢視窗中，下載專案，然後使用 Ctrl + Shift + E tooexecute hello 查詢。 您應該會收到 hello 命令已順利完成的訊息。

## <a name="configure-hello-sample"></a>設定 hello 範例

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 SQL 資料庫。 從 hello **Essentials** hello SQL 資料庫刀鋒視窗中，選取部分**顯示資料庫的連接字串**。 從出現的 hello 清單，複製 hello **ADO.NET （SQL 驗證）**資訊。

2. 開啟 Visual Studio 中的 hello 範例。 從**方案總管 中**，開啟 hello **App.config**檔案，然後再尋找下列項目 hello:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    取代 hello **# # TOBEFILLED # #** hello 上一個步驟中複製的值與 hello 資料庫連接字串。 取代**{您\_使用者名稱}**和**{您\_密碼}** hello 使用者名稱和密碼 hello 資料庫。

3. 儲存並關閉 hello 檔案。

## <a name="deploy-hello-sample"></a>部署 hello 範例

1. 從**方案總管 中**，以滑鼠右鍵按一下 hello **StormToSQL**專案，然後選取**提交 HDInsight 上的 tooStorm**。 選取 hello HDInsight 叢集的 hello **Storm 叢集**下拉式清單中的對話方塊。

   > [!NOTE]
   > 可能需要數秒鐘，讓 hello **Storm 叢集**下拉式 toopopulate 使用伺服器名稱。
   >
   > 如果出現提示，請輸入您的 Azure 訂閱 hello 登入認證。 如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。

2. 當已送出 hello 拓樸時，hello__拓撲檢視器__隨即出現。 tooview 此拓撲，從 [hello] 清單選取 hello SqlAzureWriterTopology 項目。

    ![hello 拓撲中，使用選取的 hello 拓撲](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    您可以使用此檢視 toosee 資訊在 hello 拓撲中，或按兩下 hello 拓撲中的項目 （例如 hello SqlAzureBolt) toosee 資訊特定 tooa 元件。

3. 之後 hello 拓撲已執行幾分鐘的時間，傳回 toohello 用 toocreate hello 資料庫的 SQL 查詢視窗。 取代下列查詢的 hello hello 現有陳述式：

        select * from iislogs;

    使用 Ctrl + Shift + E tooexecute hello 查詢，而且您應該會收到下列資料的結果類似 toohello:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    此資料已寫入 hello Storm 拓撲。

## <a name="create-a-report"></a>建立報表

1. 連接 toohello [Azure SQL Database 連接器](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect)Power bi。 

2. 在 [資料庫] 內，選取 [Get]。

3. 選取 [Azure SQL Database]，然後選取 [連接]。

    > [!NOTE]
    > 您可能會要求 toodownload hello Power BI Desktop toocontinue。 若是如此，請使用下列步驟 tooconnect hello:
    >
    > 1. 開啟 Power BI Desktop 並選取 [取得資料]。
    > 2  選取 __Azure__，然後選取 __Azure SQL Database__。

4. 輸入 hello 資訊 tooconnect tooyour Azure SQL Database。 您可以找到此資訊，請瀏覽 hello [Azure 入口網站](https://portal.azure.com)，然後選取您的 SQL 資料庫。

   > [!NOTE]
   > 您也可以透過設定 hello 重新整理間隔，自訂篩選器**啟用進階選項**hello 從連接對話方塊。

5. 您已連接之後，您會看到新的資料集，以相同的名稱，做為 hello 資料庫連接到您的 hello。 選取 hello 資料集 toobegin 設計報表。

6. 從**欄位**，依序展開 hello **IISLOGS**項目。 toocreate 源自報表清單 hello URI，選取 hello 核取方塊**URISTEM**。

    ![建立報告](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. 下一步，拖曳**方法**toohello 報表。 源自 hello 報表更新 toolist hello 與 hello 對應的 HTTP 方法使用 hello HTTP 要求。

    ![將資料加入 hello 方法](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. 從 hello**視覺效果**資料行中，選取 hello**欄位**圖示，然後選取 hello 向下箭號旁太**方法**在 hello**值**> 一節。 toodisplay 存取的多少次 URI 計數後，選取**計數**。

    ![變更 tooa 計數的方法](./media/hdinsight-storm-power-bi-topology/count.png)

9. 接下來，選取 hello**堆疊直條圖**toochange hello 資訊的顯示方式。

    ![變更 tooa 堆疊的圖表](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. toosave hello 報表中，選取**儲存**，然後輸入 hello 報表的名稱。

## <a name="stop-hello-topology"></a>停止 hello 拓樸

hello 拓撲會繼續執行 toorun，直到您將它停止或刪除 hello Storm HDInsight 叢集上。 toostop hello 拓撲中，執行下列步驟的 hello:

1. 在 Visual Studio 中，傳回 toohello 拓撲檢視器，然後選取 hello 拓撲。

2. 選取 hello **Kill**按鈕 toostop hello 拓撲。

    ![Kill hello 拓樸摘要 按鈕](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>刪除叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>後續步驟

在本文件中，您學到如何 toosend 資料從 Storm 拓撲 tooSQL 資料庫，然後視覺效果顯示 hello 使用 Power BI 的資料。 如需詳細資訊與其他 Azure 技術在 HDInsight 上使用 Storm toowork，請參閱下列文件的 hello:

* [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)
