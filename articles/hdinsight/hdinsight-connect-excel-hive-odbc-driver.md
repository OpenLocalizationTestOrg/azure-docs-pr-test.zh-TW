---
title: "以 hello hive 控制檔的 ODBC 驅動程式的 Azure HDInsight aaaConnect Excel tooHadoop |Microsoft 文件"
description: "了解如何向上 tooset 並用 hello Excel tooquery 中的資料從 Microsoft Excel 的 HDInsight 叢集的 Microsoft Hive ODBC 驅動程式。"
keywords: hadoop excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>連接 Azure HDInsight 中的 Excel tooHadoop hello Microsoft Hive ODBC 驅動程式

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Microsoft 的巨量資料解決方案與已部署的 hello Azure HDInsight 的 Apache Hadoop 叢集整合 Microsoft 商業智慧 (BI) 元件。 這項整合的範例是 hello 能力 tooconnect Excel toohello Hive 資料倉儲中使用 hello Microsoft Hive 開放式資料庫連接 (ODBC) 驅動程式的 HDInsight Hadoop 叢集。

它也是與 HDInsight 叢集和其他資料來源相關聯的可能 tooconnect hello 資料，包括其他 (非-HDInsight) Hadoop 叢集，從 Excel 使用 hello Microsoft Power Query 增益集的 Excel。 如需安裝及使用 Power Query 的詳細資訊，請參閱[有了 Power Query 連接的 Excel tooHDInsight][hdinsight-power-query]。

> [!NOTE]
> 中的 hello 步驟時這份文件可以搭配任一 Linux 或 Windows 為基礎的 HDInsight 叢集，Windows 必須 hello 用戶端工作站。
> 
> 

**必要條件**：

在開始這份文件之前，您必須擁有 hello 下列項目：

* **HDInsight 叢集**。 toocreate 其中一個，請參閱[開始使用 Azure HDInsight][hdinsight-get-started]。
* **工作站** 。

## <a name="install-microsoft-hive-odbc-driver"></a>安裝 Microsoft Hive ODBC 驅動程式
下載並安裝 Microsoft Hive ODBC 驅動程式從 hello[下載中心][hive-odbc-driver-download]。

此驅動程式可以安裝在 32 位元或 64 位元版本的 Windows 7、Windows 8、Windows 10、Windows Server 2008 R2 和 Windows Server 2012。 hello 驅動程式會允許連接 tooAzure HDInsight （1.6 版及更新版本） 和 Azure HDInsight 模擬器 (v.1.0.0.0 和更新版本)。 您應該安裝符合 hello hello 應用程式，您可以使用 hello ODBC 驅動程式版本的 hello 版本。 此教學課程中，從 Office Excel 使用 hello 驅動程式。

## <a name="create-hive-odbc-data-source"></a>建立 Hive ODBC 資料來源
hello 下列步驟說明如何 toocreate hive 控制檔的 ODBC 資料來源。

1. 從 Windows 8 或 Windows 10 中，按 [hello Windows 金鑰 tooopen hello 開始] 畫面，然後鍵入**資料來源**。
2. 根據您的 Office 版本，按一下 [設定 ODBC 資料來源 (32 位元)] 或 [設定 ODBC 資料來源 (64 位元)]。 如果您使用 Windows 7，請從 [系統管理工具] 中選擇 [ODBC 資料來源 (32 位元)] 或 [ODBC 資料來源 (64 位元)]。 您應該會看到 hello **ODBC 資料來源管理員**對話方塊。
   
    ![OBDC 資料來源管理員](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "使用 ODBC 資料來源管理員設定 DSN")

3. 從使用者的 DNS，請按一下**新增**tooopen hello**建立新的資料來源**精靈。
4. 選取 Microsoft Hive ODBC 驅動程式，然後按一下完成。 您應該會看到 hello **Microsoft Hive ODBC 驅動程式 DNS 安裝**對話方塊。
5. 輸入或選取下列值的 hello:
   
   | 屬性 | 描述 |
   | --- | --- |
   |  資料來源名稱 |提供名稱 tooyour 資料來源 |
   |  Host |輸入 &lt;HDInsightClusterName>.azurehdinsight.net。 例如，myHDICluster.azurehdinsight.net |
   |  連接埠 |使用 <strong>443</strong> （此連接埠已變更從 563 too443）。 |
   |  資料庫 |使用<strong>預設值</strong> |
   |  機制 |選取 [Azure HDInsight 服務]<strong></strong> |
   |  使用者名稱 |輸入 HDInsight 叢集 HTTP 使用者的使用者名稱。 hello 預設使用者名稱是<strong>admin</strong>。 |
   |  密碼 |輸入 HDInsight 叢集使用者的密碼。 |
   
    </table>
   
    有一些重要參數 toobe 注意當您按一下**進階選項**:
   
   | 參數 | 說明 |
   | --- | --- |
   |  使用原生查詢 |選取時，hello ODBC 驅動程式不會嘗試 tooconvert TSQL HiveQL 到。 只有在百分之百確定您所提交的是純 HiveQL 陳述式時，才應使用此選項。 當連線 tooSQL 伺服器或 Azure SQL Database 時，您應該將未核取。 |
   |  每個區塊擷取的資料列 |當擷取大量的記錄，調整此參數可能會需要的 tooensure 最佳效能。 |
   |  預設字串資料行長度、二進位資料行長度、十進位資料行小數位數 |hello 資料類型長度和有效位數而可能會影響您如何傳回資料。 它們會導致不正確的資訊 toobe 傳回因為 tooloss 有效位數和/或截斷。 |

    ![進階選項](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "進階 DSN 設定選項")

1. 按一下**測試**tootest hello 資料來源。 當 hello 資料來源已正確設定時，它會顯示*測試成功完成 ！*。
2. 按一下**確定**tooclose hello 測試對話方塊。 hello 新的資料來源應該列在 hello **ODBC 資料來源管理員**。
3. 按一下**確定**tooexit hello 精靈。

## <a name="import-data-into-excel-from-hdinsight"></a>從 HDInsight 將資料匯入 Excel 中
hello 下列步驟描述 hello tooimport 資料方式的 Hive 資料表從 Excel 活頁簿使用您建立 hello 前一節中的 hello ODBC 資料來源。

1. 在 Excel 中開啟新的或現有的活頁簿。
2. 從 hello**資料**索引標籤上，按一下 **取得資料**，按一下 **從其他來源**，然後按一下**從 ODBC** toolaunch hello **資料連線精靈**。
   
    ![開啟資料連線精靈](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "開啟資料連線精靈")
4. 選取 hello 資料來源在 hello 最後一節中所建立的名稱，然後按一下**確定**。
5. 輸入 Hadoop 使用者名稱 （hello 預設名稱是系統管理員） hello 密碼，然後按一下**連接**。
6. 在導覽器中，依序展開 HIVE 和 default，按一下 hivesampletable，然後按一下載入。 花幾秒鐘，才能資料取得匯入的 tooExcel。

    ![HDInsight Hive ODBC 導覽器](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "開啟資料連接精靈")


## <a name="next-steps"></a>後續步驟
在本文中，您學會如何 toouse hello 到 Excel 的 Microsoft Hive ODBC 驅動程式 tooretrieve 資料從 hello HDInsight 服務。 同樣地，您可以從 hello HDInsight 服務擷取資料到 SQL 資料庫。 它也是可能 tooupload HDInsight 服務資料。 toolearn 詳細資訊，請參閱：

* [使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-data]
* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


