---
title: "有了 Power Query-Azure HDInsight aaaConnect Excel tooHadoop |Microsoft 文件"
description: "了解如何 tootake 善用商業智慧元件及使用 Power Query for Excel tooaccess 資料儲存在 HDInsight 上的 Hadoop。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>使用 Power Query 連線 Excel tooHadoop
Hello Microsoft 巨量資料解決方案的關鍵功能是 hello 與在 Azure HDInsight Hadoop 叢集的 Microsoft 商業智慧 (BI) 元件整合。 主要範例是 hello 能力 tooconnect Excel toohello 包含 hello 資料使用 hello Microsoft Power Query for Excel 增益集與 Hadoop 叢集相關聯的 Azure 儲存體帳戶。 這篇文章會引導您 tooset 註冊並使用與 Hdinsight 叢集相關聯的 Power Query tooquery 資料管理與 HDInsight 的方式。

### <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列項目：

* **HDInsight 叢集**。 tooconfigure 其中一個，請參閱[開始使用 Azure HDInsight][hdinsight-get-started]。
* **工作站** 。
* **Office 2016、Office 2013 專業增強版、Office 365 專業增強版、Excel 2013 獨立版或 Office 2010 專業增強版**。

## <a name="install-power-query"></a>安裝 Power Query
Power Query 可匯入在 HDInsight 叢集上執行的 Hadoop 工作所匯出或產生的資料。

在 Excel 2016 中，Power Query 已整合至 hello 資料 功能區 hello 取得和轉換 區段下。 對於較舊的 Excel 版本中，下載 Microsoft Power Query for Excel 從 hello [Microsoft Download Center] [ powerquery-download]並安裝它。

## <a name="import-hdinsight-data-into-excel"></a>將 HDInsight 資料匯入 Excel 中
Power Query 增益集適用於 Excel 的 hello 可從您的 HDInsight 叢集到 Excel，其中 BI 工具，例如 PowerPivot 和 Power 對應可以是使用的 tooinspect、 分析和呈現 hello 資料輕鬆 tooimport 資料。

**tooimport 資料從 HDInsight 叢集**

1. 開啟 Excel。
2. 建立新的空白活頁簿。
3. 執行下列步驟以 hello Excel 版本為基礎的 hello:

    - Excel 2016

        - 按一下 hello**資料**功能表上，按一下 **取得資料**從 hello**取得與轉換資料**功能區中，按一下 **從 Azure**，然後按一下 **從 Azure HDInsight(HDFS)**。

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - 按一下 hello **Power Query**功能表上，按一下 **從 Azure**，然後按一下**從 Microsoft Azure HDInsight**。
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **注意：**如果您沒有看見 hello **Power Query**功能表上，移過**檔案** > **選項** > **增益集**，然後選取**COM 增益集**hello 下拉式清單中**管理**在 hello hello 頁面底部的方塊。 選取 hello**移...**按鈕，並確認該 hello 方塊為已核取 hello Power Query for Excel 增益集。
       
        **注意：** Power Query 也可讓您從 HDFS tooimport 資料即可**從其他來源**。
4. 如**帳戶名稱**，輸入 hello hello 與您的叢集相關聯的 Azure Blob 儲存體帳戶名稱，然後按一下**確定**。 此帳戶可以是 hello[預設儲存體帳戶](hdinsight-administer-use-management-portal.md#find-the-default-storage-account)或連結的儲存體帳戶。  hello 格式是*https://&lt;StorageAccountName >.blob.core.windows.net/*。
5. 如**帳戶金鑰**，輸入 hello hello Blob 儲存體帳戶金鑰，然後按一下**儲存**。 （您需要 tooenter hello 帳戶資訊只有 hello 存取這個存放區的第一次）。
6. 在 hello**導覽**hello 窗格左邊 hello 查詢編輯器中，按兩下 hello Blob 儲存體容器名稱。 根據預設，hello 容器名稱是 hello 相同名稱做為 hello 叢集名稱。
7. 找出**HiveSampleData.txt**在 hello**名稱**資料行 (hello 的資料夾路徑**../ hive/倉儲/hivesampletable/**)，然後按一下**二進位**左邊的 HiveSampleData.txt hello。 HiveSampleData.txt 隨附於所有 hello 叢集。 您也可以選擇使用您自己的檔案。
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. 如果您想，您可以重新命名 hello 資料行名稱。 請在準備就緒後，按一下 [關閉並載入]。  hello 資料已經載入的 tooyour 活頁簿：
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>後續步驟
在本文中，您學到如何 toouse HDInsight 到 Excel 的 Power Query tooretrieve 資料。 同樣地，您也可以將 HDInsight 中的資料擷取至 Azure SQL Database。 它也是可能 tooupload HDInsight 資料。 toolearn 詳細資訊，請參閱下列文章 hello:

* [Excel tooHDInsight 連接以 hello Microsoft Hive ODBC 驅動程式][hdinsight-ODBC]
* [上傳資料 tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
