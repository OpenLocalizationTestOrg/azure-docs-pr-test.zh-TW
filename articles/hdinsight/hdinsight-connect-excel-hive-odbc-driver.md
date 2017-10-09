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
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a><span data-ttu-id="7711e-104">連接 Azure HDInsight 中的 Excel tooHadoop hello Microsoft Hive ODBC 驅動程式</span><span class="sxs-lookup"><span data-stu-id="7711e-104">Connect Excel tooHadoop in Azure HDInsight with hello Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="7711e-105">Microsoft 的巨量資料解決方案與已部署的 hello Azure HDInsight 的 Apache Hadoop 叢集整合 Microsoft 商業智慧 (BI) 元件。</span><span class="sxs-lookup"><span data-stu-id="7711e-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by hello Azure HDInsight.</span></span> <span data-ttu-id="7711e-106">這項整合的範例是 hello 能力 tooconnect Excel toohello Hive 資料倉儲中使用 hello Microsoft Hive 開放式資料庫連接 (ODBC) 驅動程式的 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="7711e-106">An example of this integration is hello ability tooconnect Excel toohello Hive data warehouse of a Hadoop cluster in HDInsight using hello Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="7711e-107">它也是與 HDInsight 叢集和其他資料來源相關聯的可能 tooconnect hello 資料，包括其他 (非-HDInsight) Hadoop 叢集，從 Excel 使用 hello Microsoft Power Query 增益集的 Excel。</span><span class="sxs-lookup"><span data-stu-id="7711e-107">It is also possible tooconnect hello data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using hello Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="7711e-108">如需安裝及使用 Power Query 的詳細資訊，請參閱[有了 Power Query 連接的 Excel tooHDInsight][hdinsight-power-query]。</span><span class="sxs-lookup"><span data-stu-id="7711e-108">For information on installing and using Power Query, see [Connect Excel tooHDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="7711e-109">中的 hello 步驟時這份文件可以搭配任一 Linux 或 Windows 為基礎的 HDInsight 叢集，Windows 必須 hello 用戶端工作站。</span><span class="sxs-lookup"><span data-stu-id="7711e-109">While hello steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for hello client workstation.</span></span>
> 
> 

<span data-ttu-id="7711e-110">**必要條件**：</span><span class="sxs-lookup"><span data-stu-id="7711e-110">**Prerequisites**:</span></span>

<span data-ttu-id="7711e-111">在開始這份文件之前，您必須擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="7711e-111">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="7711e-112">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="7711e-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="7711e-113">toocreate 其中一個，請參閱[開始使用 Azure HDInsight][hdinsight-get-started]。</span><span class="sxs-lookup"><span data-stu-id="7711e-113">toocreate one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="7711e-114">**工作站** 。</span><span class="sxs-lookup"><span data-stu-id="7711e-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="7711e-115">安裝 Microsoft Hive ODBC 驅動程式</span><span class="sxs-lookup"><span data-stu-id="7711e-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="7711e-116">下載並安裝 Microsoft Hive ODBC 驅動程式從 hello[下載中心][hive-odbc-driver-download]。</span><span class="sxs-lookup"><span data-stu-id="7711e-116">Download and install Microsoft Hive ODBC Driver from hello [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="7711e-117">此驅動程式可以安裝在 32 位元或 64 位元版本的 Windows 7、Windows 8、Windows 10、Windows Server 2008 R2 和 Windows Server 2012。</span><span class="sxs-lookup"><span data-stu-id="7711e-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="7711e-118">hello 驅動程式會允許連接 tooAzure HDInsight （1.6 版及更新版本） 和 Azure HDInsight 模擬器 (v.1.0.0.0 和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="7711e-118">hello driver allows connection tooAzure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="7711e-119">您應該安裝符合 hello hello 應用程式，您可以使用 hello ODBC 驅動程式版本的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7711e-119">You shall install hello version that matches hello version of hello application where you use hello ODBC driver.</span></span> <span data-ttu-id="7711e-120">此教學課程中，從 Office Excel 使用 hello 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="7711e-120">For this tutorial, hello driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="7711e-121">建立 Hive ODBC 資料來源</span><span class="sxs-lookup"><span data-stu-id="7711e-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="7711e-122">hello 下列步驟說明如何 toocreate hive 控制檔的 ODBC 資料來源。</span><span class="sxs-lookup"><span data-stu-id="7711e-122">hello following steps show you how toocreate a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="7711e-123">從 Windows 8 或 Windows 10 中，按 [hello Windows 金鑰 tooopen hello 開始] 畫面，然後鍵入**資料來源**。</span><span class="sxs-lookup"><span data-stu-id="7711e-123">From Windows 8 or Windows 10, press hello Windows key tooopen hello Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="7711e-124">根據您的 Office 版本，按一下 [設定 ODBC 資料來源 (32 位元)] 或 [設定 ODBC 資料來源 (64 位元)]。</span><span class="sxs-lookup"><span data-stu-id="7711e-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="7711e-125">如果您使用 Windows 7，請從 [系統管理工具] 中選擇 [ODBC 資料來源 (32 位元)] 或 [ODBC 資料來源 (64 位元)]。</span><span class="sxs-lookup"><span data-stu-id="7711e-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="7711e-126">您應該會看到 hello **ODBC 資料來源管理員**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7711e-126">You shall see hello **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="7711e-127">![OBDC 資料來源管理員](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "使用 ODBC 資料來源管理員設定 DSN")</span><span class="sxs-lookup"><span data-stu-id="7711e-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="7711e-128">從使用者的 DNS，請按一下**新增**tooopen hello**建立新的資料來源**精靈。</span><span class="sxs-lookup"><span data-stu-id="7711e-128">From User DNS, click **Add** tooopen hello **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="7711e-129">選取 Microsoft Hive ODBC 驅動程式，然後按一下完成。</span><span class="sxs-lookup"><span data-stu-id="7711e-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="7711e-130">您應該會看到 hello **Microsoft Hive ODBC 驅動程式 DNS 安裝**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7711e-130">You shall see hello **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="7711e-131">輸入或選取下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="7711e-131">Type or select hello following values:</span></span>
   
   | <span data-ttu-id="7711e-132">屬性</span><span class="sxs-lookup"><span data-stu-id="7711e-132">Property</span></span> | <span data-ttu-id="7711e-133">描述</span><span class="sxs-lookup"><span data-stu-id="7711e-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7711e-134">資料來源名稱</span><span class="sxs-lookup"><span data-stu-id="7711e-134">Data Source Name</span></span> |<span data-ttu-id="7711e-135">提供名稱 tooyour 資料來源</span><span class="sxs-lookup"><span data-stu-id="7711e-135">Give a name tooyour data source</span></span> |
   |  <span data-ttu-id="7711e-136">Host</span><span class="sxs-lookup"><span data-stu-id="7711e-136">Host</span></span> |<span data-ttu-id="7711e-137">輸入 &lt;HDInsightClusterName>.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="7711e-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="7711e-138">例如，myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="7711e-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="7711e-139">連接埠</span><span class="sxs-lookup"><span data-stu-id="7711e-139">Port</span></span> |<span data-ttu-id="7711e-140">使用 <strong>443</strong></span><span class="sxs-lookup"><span data-stu-id="7711e-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="7711e-141">（此連接埠已變更從 563 too443）。</span><span class="sxs-lookup"><span data-stu-id="7711e-141">(This port has been changed from 563 too443.)</span></span> |
   |  <span data-ttu-id="7711e-142">資料庫</span><span class="sxs-lookup"><span data-stu-id="7711e-142">Database</span></span> |<span data-ttu-id="7711e-143">使用<strong>預設值</strong></span><span class="sxs-lookup"><span data-stu-id="7711e-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="7711e-144">機制</span><span class="sxs-lookup"><span data-stu-id="7711e-144">Mechanism</span></span> |<span data-ttu-id="7711e-145">選取 [Azure HDInsight 服務]<strong></strong></span><span class="sxs-lookup"><span data-stu-id="7711e-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="7711e-146">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="7711e-146">User Name</span></span> |<span data-ttu-id="7711e-147">輸入 HDInsight 叢集 HTTP 使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="7711e-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="7711e-148">hello 預設使用者名稱是<strong>admin</strong>。</span><span class="sxs-lookup"><span data-stu-id="7711e-148">hello default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="7711e-149">密碼</span><span class="sxs-lookup"><span data-stu-id="7711e-149">Password</span></span> |<span data-ttu-id="7711e-150">輸入 HDInsight 叢集使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="7711e-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="7711e-151">有一些重要參數 toobe 注意當您按一下**進階選項**:</span><span class="sxs-lookup"><span data-stu-id="7711e-151">There are some important parameters toobe aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="7711e-152">參數</span><span class="sxs-lookup"><span data-stu-id="7711e-152">Parameter</span></span> | <span data-ttu-id="7711e-153">說明</span><span class="sxs-lookup"><span data-stu-id="7711e-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7711e-154">使用原生查詢</span><span class="sxs-lookup"><span data-stu-id="7711e-154">Use Native Query</span></span> |<span data-ttu-id="7711e-155">選取時，hello ODBC 驅動程式不會嘗試 tooconvert TSQL HiveQL 到。</span><span class="sxs-lookup"><span data-stu-id="7711e-155">When it is selected, hello ODBC driver does NOT try tooconvert TSQL into HiveQL.</span></span> <span data-ttu-id="7711e-156">只有在百分之百確定您所提交的是純 HiveQL 陳述式時，才應使用此選項。</span><span class="sxs-lookup"><span data-stu-id="7711e-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="7711e-157">當連線 tooSQL 伺服器或 Azure SQL Database 時，您應該將未核取。</span><span class="sxs-lookup"><span data-stu-id="7711e-157">When connecting tooSQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="7711e-158">每個區塊擷取的資料列</span><span class="sxs-lookup"><span data-stu-id="7711e-158">Rows fetched per block</span></span> |<span data-ttu-id="7711e-159">當擷取大量的記錄，調整此參數可能會需要的 tooensure 最佳效能。</span><span class="sxs-lookup"><span data-stu-id="7711e-159">When fetching a large number of records, tuning this parameter may be required tooensure optimal performances.</span></span> |
   |  <span data-ttu-id="7711e-160">預設字串資料行長度、二進位資料行長度、十進位資料行小數位數</span><span class="sxs-lookup"><span data-stu-id="7711e-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="7711e-161">hello 資料類型長度和有效位數而可能會影響您如何傳回資料。</span><span class="sxs-lookup"><span data-stu-id="7711e-161">hello data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="7711e-162">它們會導致不正確的資訊 toobe 傳回因為 tooloss 有效位數和/或截斷。</span><span class="sxs-lookup"><span data-stu-id="7711e-162">They cause incorrect information toobe returned due tooloss of precision and/or truncation.</span></span> |

    <span data-ttu-id="7711e-163">![進階選項](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "進階 DSN 設定選項")</span><span class="sxs-lookup"><span data-stu-id="7711e-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="7711e-164">按一下**測試**tootest hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="7711e-164">Click **Test** tootest hello data source.</span></span> <span data-ttu-id="7711e-165">當 hello 資料來源已正確設定時，它會顯示*測試成功完成 ！*。</span><span class="sxs-lookup"><span data-stu-id="7711e-165">When hello data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="7711e-166">按一下**確定**tooclose hello 測試對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7711e-166">Click **OK** tooclose hello Test dialog.</span></span> <span data-ttu-id="7711e-167">hello 新的資料來源應該列在 hello **ODBC 資料來源管理員**。</span><span class="sxs-lookup"><span data-stu-id="7711e-167">hello new data source shall be listed on hello **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="7711e-168">按一下**確定**tooexit hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="7711e-168">Click **OK** tooexit hello wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="7711e-169">從 HDInsight 將資料匯入 Excel 中</span><span class="sxs-lookup"><span data-stu-id="7711e-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="7711e-170">hello 下列步驟描述 hello tooimport 資料方式的 Hive 資料表從 Excel 活頁簿使用您建立 hello 前一節中的 hello ODBC 資料來源。</span><span class="sxs-lookup"><span data-stu-id="7711e-170">hello following steps describe hello way tooimport data from a Hive table into an Excel workbook using hello ODBC data source that you created in hello previous section.</span></span>

1. <span data-ttu-id="7711e-171">在 Excel 中開啟新的或現有的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="7711e-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="7711e-172">從 hello**資料**索引標籤上，按一下 **取得資料**，按一下 **從其他來源**，然後按一下**從 ODBC** toolaunch hello **資料連線精靈**。</span><span class="sxs-lookup"><span data-stu-id="7711e-172">From hello **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** toolaunch hello **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="7711e-173">![開啟資料連線精靈](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "開啟資料連線精靈")</span><span class="sxs-lookup"><span data-stu-id="7711e-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="7711e-174">選取 hello 資料來源在 hello 最後一節中所建立的名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="7711e-174">Select hello data source name that you created in hello last section, and then click **OK**.</span></span>
5. <span data-ttu-id="7711e-175">輸入 Hadoop 使用者名稱 （hello 預設名稱是系統管理員） hello 密碼，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="7711e-175">Enter Hadoop user name (hello default name is admin) and hello password, and then click **Connect**.</span></span>
6. <span data-ttu-id="7711e-176">在導覽器中，依序展開 HIVE 和 default，按一下 hivesampletable，然後按一下載入。</span><span class="sxs-lookup"><span data-stu-id="7711e-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="7711e-177">花幾秒鐘，才能資料取得匯入的 tooExcel。</span><span class="sxs-lookup"><span data-stu-id="7711e-177">It takes a few seconds before data gets imported tooExcel.</span></span>

    <span data-ttu-id="7711e-178">![HDInsight Hive ODBC 導覽器](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "開啟資料連接精靈")</span><span class="sxs-lookup"><span data-stu-id="7711e-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="7711e-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7711e-179">Next steps</span></span>
<span data-ttu-id="7711e-180">在本文中，您學會如何 toouse hello 到 Excel 的 Microsoft Hive ODBC 驅動程式 tooretrieve 資料從 hello HDInsight 服務。</span><span class="sxs-lookup"><span data-stu-id="7711e-180">In this article, you learned how toouse hello Microsoft Hive ODBC driver tooretrieve data from hello HDInsight Service into Excel.</span></span> <span data-ttu-id="7711e-181">同樣地，您可以從 hello HDInsight 服務擷取資料到 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7711e-181">Similarly, you can retrieve data from hello HDInsight Service into SQL Database.</span></span> <span data-ttu-id="7711e-182">它也是可能 tooupload HDInsight 服務資料。</span><span class="sxs-lookup"><span data-stu-id="7711e-182">It is also possible tooupload data into an HDInsight Service.</span></span> <span data-ttu-id="7711e-183">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7711e-183">toolearn more, see:</span></span>

* <span data-ttu-id="7711e-184">[使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="7711e-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="7711e-185">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="7711e-185">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="7711e-186">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="7711e-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


