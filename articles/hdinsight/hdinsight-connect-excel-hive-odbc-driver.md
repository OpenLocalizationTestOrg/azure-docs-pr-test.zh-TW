---
title: "使用 Hive ODBC 驅動程式將 Excel 連線到 Hadoop - Azure HDInsight | Microsoft Docs"
description: "了解如何設定和使用 Excel 的 Microsoft Hive ODBC 驅動程式，從 Microsoft Excel 查詢 HDInsight 叢集中的資料。"
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
ms.openlocfilehash: 7818093e42c34ee671a035cde783a6622fb2a798
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-excel-to-hadoop-in-azure-hdinsight-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="30bf6-104">使用 Microsoft Hive ODBC 驅動程式將 Excel 連線到 Azure HDInsight 中的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="30bf6-104">Connect Excel to Hadoop in Azure HDInsight with the Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="30bf6-105">Microsoft 巨量資料方案會將 Microsoft 商業智慧 (BI) 元件與 Azure HDInsight 所部署的 Apache Hadoop 叢集相整合。</span><span class="sxs-lookup"><span data-stu-id="30bf6-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="30bf6-106">舉例來說，此整合可讓您使用 Microsoft Hive 開放式資料庫連線能力 (ODBC) 驅動程式，將 Excel 連線到 HDInsight 中 Hadoop 叢集的 Hive 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="30bf6-106">An example of this integration is the ability to connect Excel to the Hive data warehouse of a Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="30bf6-107">您也可以從 Excel 使用 Microsoft Power Query for Excel，連接與 HDInsight 叢集和其他資料來源 (包括其他 (非 HDInsight) Hadoop 叢集) 相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="30bf6-107">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="30bf6-108">如需安裝和使用 Power Query 的相關資訊，請參閱[使用 Power Query 將 Excel 連接到 HDInsight][hdinsight-power-query]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-108">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="30bf6-109">本文中的步驟雖然可以與 Linux 或 Windows 架構的 HDInsight 叢集搭配使用，但用戶端工作站需要有 Windows。</span><span class="sxs-lookup"><span data-stu-id="30bf6-109">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="30bf6-110">**必要條件**：</span><span class="sxs-lookup"><span data-stu-id="30bf6-110">**Prerequisites**:</span></span>

<span data-ttu-id="30bf6-111">開始閱讀本文之前，您必須有下列各項：</span><span class="sxs-lookup"><span data-stu-id="30bf6-111">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="30bf6-112">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="30bf6-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="30bf6-113">若要建立，請參閱[開始使用 Azure HDInsight][hdinsight-get-started]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-113">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="30bf6-114">**工作站** 。</span><span class="sxs-lookup"><span data-stu-id="30bf6-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="30bf6-115">安裝 Microsoft Hive ODBC 驅動程式</span><span class="sxs-lookup"><span data-stu-id="30bf6-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="30bf6-116">從[下載中心][hive-odbc-driver-download]下載並安裝 Microsoft Hive ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="30bf6-116">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="30bf6-117">此驅動程式可以安裝在 32 位元或 64 位元版本的 Windows 7、Windows 8、Windows 10、Windows Server 2008 R2 和 Windows Server 2012。</span><span class="sxs-lookup"><span data-stu-id="30bf6-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="30bf6-118">驅動程式可允許 Azure HDInsight (1.6 版及更新版本) 與 Azure HDInsight Emulator (1.0.0.0 版及更新版本) 的連線。</span><span class="sxs-lookup"><span data-stu-id="30bf6-118">The driver allows connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="30bf6-119">您所安裝的版本必須與您要使用 ODBC 驅動程式的應用程式版本相符。</span><span class="sxs-lookup"><span data-stu-id="30bf6-119">You shall install the version that matches the version of the application where you use the ODBC driver.</span></span> <span data-ttu-id="30bf6-120">本教學課程將會從 Office Excel 使用此驅動程式。</span><span class="sxs-lookup"><span data-stu-id="30bf6-120">For this tutorial, the driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="30bf6-121">建立 Hive ODBC 資料來源</span><span class="sxs-lookup"><span data-stu-id="30bf6-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="30bf6-122">下列步驟將說明如何建立 Hive ODBC 資料來源。</span><span class="sxs-lookup"><span data-stu-id="30bf6-122">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="30bf6-123">在 Windows 8 或 Windows 10 中，按視窗鍵以開啟 [開始] 畫面，然後輸入 **資料來源**。</span><span class="sxs-lookup"><span data-stu-id="30bf6-123">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="30bf6-124">根據您的 Office 版本，按一下 [設定 ODBC 資料來源 (32 位元)] 或 [設定 ODBC 資料來源 (64 位元)]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="30bf6-125">如果您使用 Windows 7，請從 [系統管理工具] 中選擇 [ODBC 資料來源 (32 位元)] 或 [ODBC 資料來源 (64 位元)]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="30bf6-126">您應該會看到 [ODBC 資料來源管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="30bf6-126">You shall see the **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="30bf6-127">![OBDC 資料來源管理員](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "使用 ODBC 資料來源管理員設定 DSN")</span><span class="sxs-lookup"><span data-stu-id="30bf6-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="30bf6-128">在 [使用者 DNS] 中按一下 [新增]，以開啟 [建立新資料來源] 精靈。</span><span class="sxs-lookup"><span data-stu-id="30bf6-128">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="30bf6-129">選取 [Microsoft Hive ODBC 驅動程式]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="30bf6-130">您應該會看到 [Microsoft Hive ODBC 驅動程式 DNS 設定] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="30bf6-130">You shall see the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="30bf6-131">輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="30bf6-131">Type or select the following values:</span></span>
   
   | <span data-ttu-id="30bf6-132">屬性</span><span class="sxs-lookup"><span data-stu-id="30bf6-132">Property</span></span> | <span data-ttu-id="30bf6-133">描述</span><span class="sxs-lookup"><span data-stu-id="30bf6-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="30bf6-134">資料來源名稱</span><span class="sxs-lookup"><span data-stu-id="30bf6-134">Data Source Name</span></span> |<span data-ttu-id="30bf6-135">為資料來源指定名稱</span><span class="sxs-lookup"><span data-stu-id="30bf6-135">Give a name to your data source</span></span> |
   |  <span data-ttu-id="30bf6-136">Host</span><span class="sxs-lookup"><span data-stu-id="30bf6-136">Host</span></span> |<span data-ttu-id="30bf6-137">輸入 &lt;HDInsightClusterName>.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="30bf6-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="30bf6-138">例如，myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="30bf6-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="30bf6-139">連接埠</span><span class="sxs-lookup"><span data-stu-id="30bf6-139">Port</span></span> |<span data-ttu-id="30bf6-140">使用 <strong>443</strong></span><span class="sxs-lookup"><span data-stu-id="30bf6-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="30bf6-141">(此連接埠已從 563 變更為 443)。</span><span class="sxs-lookup"><span data-stu-id="30bf6-141">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="30bf6-142">資料庫</span><span class="sxs-lookup"><span data-stu-id="30bf6-142">Database</span></span> |<span data-ttu-id="30bf6-143">使用<strong>預設值</strong></span><span class="sxs-lookup"><span data-stu-id="30bf6-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="30bf6-144">機制</span><span class="sxs-lookup"><span data-stu-id="30bf6-144">Mechanism</span></span> |<span data-ttu-id="30bf6-145">選取 [Azure HDInsight 服務]<strong></strong></span><span class="sxs-lookup"><span data-stu-id="30bf6-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="30bf6-146">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="30bf6-146">User Name</span></span> |<span data-ttu-id="30bf6-147">輸入 HDInsight 叢集 HTTP 使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="30bf6-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="30bf6-148">預設的使用者名稱為 <strong>admin</strong>。</span><span class="sxs-lookup"><span data-stu-id="30bf6-148">The default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="30bf6-149">密碼</span><span class="sxs-lookup"><span data-stu-id="30bf6-149">Password</span></span> |<span data-ttu-id="30bf6-150">輸入 HDInsight 叢集使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="30bf6-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="30bf6-151">當您按一下 [進階選項] 時，您必須留意某些重要參數：</span><span class="sxs-lookup"><span data-stu-id="30bf6-151">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="30bf6-152">參數</span><span class="sxs-lookup"><span data-stu-id="30bf6-152">Parameter</span></span> | <span data-ttu-id="30bf6-153">說明</span><span class="sxs-lookup"><span data-stu-id="30bf6-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="30bf6-154">使用原生查詢</span><span class="sxs-lookup"><span data-stu-id="30bf6-154">Use Native Query</span></span> |<span data-ttu-id="30bf6-155">選取此選項時，ODBC 驅動程式不會嘗試將 TSQL 轉換為 HiveQL。</span><span class="sxs-lookup"><span data-stu-id="30bf6-155">When it is selected, the ODBC driver does NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="30bf6-156">只有在百分之百確定您所提交的是純 HiveQL 陳述式時，才應使用此選項。</span><span class="sxs-lookup"><span data-stu-id="30bf6-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="30bf6-157">連接到 SQL Server 或 Azure SQL Database 時，您應將它保留為未勾選。</span><span class="sxs-lookup"><span data-stu-id="30bf6-157">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="30bf6-158">每個區塊擷取的資料列</span><span class="sxs-lookup"><span data-stu-id="30bf6-158">Rows fetched per block</span></span> |<span data-ttu-id="30bf6-159">在擷取大量記錄時，可能必須調整此參數，以確保最佳效能。</span><span class="sxs-lookup"><span data-stu-id="30bf6-159">When fetching a large number of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="30bf6-160">預設字串資料行長度、二進位資料行長度、十進位資料行小數位數</span><span class="sxs-lookup"><span data-stu-id="30bf6-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="30bf6-161">資料類型的長度和精確度可能會影響傳回資料的方式。</span><span class="sxs-lookup"><span data-stu-id="30bf6-161">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="30bf6-162">如果失去精確度且 (或) 發生截斷狀況，會傳回不正確的資訊。</span><span class="sxs-lookup"><span data-stu-id="30bf6-162">They cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    <span data-ttu-id="30bf6-163">![進階選項](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "進階 DSN 設定選項")</span><span class="sxs-lookup"><span data-stu-id="30bf6-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="30bf6-164">按一下 [測試]  以測試資料來源。</span><span class="sxs-lookup"><span data-stu-id="30bf6-164">Click **Test** to test the data source.</span></span> <span data-ttu-id="30bf6-165">資料來源正確設定時，會顯示 *「測試順利完成！」*。</span><span class="sxs-lookup"><span data-stu-id="30bf6-165">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="30bf6-166">按一下 [確定]  以關閉 [測試] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="30bf6-166">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="30bf6-167">新的資料來源應會列示在 [ODBC 資料來源管理員] 中。</span><span class="sxs-lookup"><span data-stu-id="30bf6-167">The new data source shall be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="30bf6-168">按一下 [確定]  以結束精靈。</span><span class="sxs-lookup"><span data-stu-id="30bf6-168">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="30bf6-169">從 HDInsight 將資料匯入 Excel 中</span><span class="sxs-lookup"><span data-stu-id="30bf6-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="30bf6-170">下列步驟將說明如何使用您在上一節中建立的 ODBC 資料來源，將資料從 Hive 資料表匯入 Excel 活頁簿中。</span><span class="sxs-lookup"><span data-stu-id="30bf6-170">The following steps describe the way to import data from a Hive table into an Excel workbook using the ODBC data source that you created in the previous section.</span></span>

1. <span data-ttu-id="30bf6-171">在 Excel 中開啟新的或現有的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="30bf6-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="30bf6-172">從 [資料] 索引標籤，依序按一下 [取得資料] 和 [從其他來源]，然後按一下 [從 ODBC] 以啟動 [資料連接精靈]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-172">From the **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** to launch the **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="30bf6-173">![開啟資料連線精靈](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "開啟資料連線精靈")</span><span class="sxs-lookup"><span data-stu-id="30bf6-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="30bf6-174">選取您在上一節中建立的資料來源名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-174">Select the data source name that you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="30bf6-175">輸入 Hadoop 使用者名稱 (預設名稱為 admin) 和密碼，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-175">Enter Hadoop user name (the default name is admin) and the password, and then click **Connect**.</span></span>
6. <span data-ttu-id="30bf6-176">在導覽器中，依序展開 [HIVE] 和 [default]，按一下 [hivesampletable]，然後按一下 [載入]。</span><span class="sxs-lookup"><span data-stu-id="30bf6-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="30bf6-177">經過數秒後，資料即會匯入至 Excel。</span><span class="sxs-lookup"><span data-stu-id="30bf6-177">It takes a few seconds before data gets imported to Excel.</span></span>

    <span data-ttu-id="30bf6-178">![HDInsight Hive ODBC 導覽器](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "開啟資料連接精靈")</span><span class="sxs-lookup"><span data-stu-id="30bf6-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="30bf6-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30bf6-179">Next steps</span></span>
<span data-ttu-id="30bf6-180">在本文中，您已了解如何使用 Microsoft Hive ODBC 驅動程式將 HDInsight 服務中的資料擷取至 Excel。</span><span class="sxs-lookup"><span data-stu-id="30bf6-180">In this article, you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="30bf6-181">同樣地，您也可以將 HDInsight 服務中的資料擷取至 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="30bf6-181">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="30bf6-182">此外也可以將資料上傳至 HDInsight 服務。</span><span class="sxs-lookup"><span data-stu-id="30bf6-182">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="30bf6-183">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="30bf6-183">To learn more, see:</span></span>

* <span data-ttu-id="30bf6-184">[使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="30bf6-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="30bf6-185">[將資料上傳至 HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="30bf6-185">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="30bf6-186">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="30bf6-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


