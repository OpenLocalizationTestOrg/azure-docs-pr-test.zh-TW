---
title: "對網站記錄分析 Azure HDInsight 的 Hive 與 Hadoop aaaUse |Microsoft 文件"
description: "了解 toouse Hive 與 HDInsight tooanalyze 網站的記錄檔。 您將使用做為輸入到 HDInsight 資料表中，記錄檔，並使用 HiveQL tooquery hello 資料。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>使用以 Windows 為基礎的 HDInsight tooanalyze 記錄檔，從網站的登錄區
了解與 HDInsight tooanalyze toouse HiveQL 從網站的記錄檔。 網站記錄分析可使用的 toosegment 觀眾根據類似的活動，分類人口統計資料和 toofind 出 hello 他們所檢視的內容，它們來自，hello 網站以及等等的站台訪客。

> [!IMPORTANT]
> hello 中此文件僅搭配 Windows 為基礎的 HDInsight 叢集的步驟。 Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

在此範例中，您將使用 HDInsight 叢集 tooanalyze 網站記錄檔 tooget 深入了解 hello 頻率造訪 toohello 網站，從外部網站一天。 您也將產生 hello 使用者遇到的網站錯誤的摘要。 您將了解如何：

* 連接 tooa Azure Blob 儲存體，其中包含網站記錄檔。
* 建立 HIVE 資料表 tooquery 這些記錄檔。
* 建立 HIVE 查詢 tooanalyze hello 資料。
* 使用 Microsoft Excel tooconnect tooHDInsight （藉由使用開放式資料庫連接 (ODBC) tooretrieve hello 分析資料。

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>必要條件
* 您必須已在 Azure HDInsight 上佈建 Hadoop 叢集。 如需指示，請參閱 [佈建 HDInsight 叢集][hdinsight-provision]。
* 您必須已安裝 Microsoft Excel 2013 或 Excel 2010。
* 您必須擁有[Microsoft Hive ODBC 驅動程式](http://www.microsoft.com/download/details.aspx?id=40886)tooimport Hive 到 Excel 的資料。

## <a name="toorun-hello-sample"></a>toorun hello 範例
1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello （如果您釘選 hello 叢集那里） 的開始面板，按一下 要 toorun hello 範例 hello 叢集磚。
2. 從 hello 叢集刀鋒視窗中，在**快速連結**，按一下 **叢集儀表板**，然後從 hello**叢集儀表板**刀鋒視窗中，按一下  **HDInsight 叢集儀表板**。 或者，您可以使用下列 URL 的 hello 直接開啟 hello 儀表板：

         https://<clustername>.azurehdinsight.net

    出現提示時，使用 hello 系統管理員使用者名稱和佈建 hello 叢集時所使用的密碼驗證。
3. 從開啟的 hello 網頁上，按一下 [hello**快速入口圖庫**] 索引標籤，然後在 hello**解決方案的範例資料**分類中，按一下 hello**網站記錄檔分析**範例。
4. 請遵循 hello hello 網頁 toofinish hello 範例上所提供的指示。

## <a name="next-steps"></a>後續步驟
請嘗試下列範例中的 hello:[分析感應器資料使用 HDInsight 的 Hive](hdinsight-hive-analyze-sensor-data.md)。

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
