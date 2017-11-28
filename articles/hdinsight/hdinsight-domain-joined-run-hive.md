---
title: "在已加入網域的 HDInsight 中設定 Hive 原則 - Azure | Microsoft Docs"
description: "了解 ..."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="b694b-103">在已加入網域的 HDInsight (預覽) 中設定 Hive 原則</span><span class="sxs-lookup"><span data-stu-id="b694b-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="b694b-104">了解如何針對 Hive 設定 Apache Ranger 原則。</span><span class="sxs-lookup"><span data-stu-id="b694b-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="b694b-105">在本文中，您會建立兩個 Ranger 原則來限制 hivesampletable 的存取權。</span><span class="sxs-lookup"><span data-stu-id="b694b-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="b694b-106">HDInsight 叢集隨附 hivesampletable。</span><span class="sxs-lookup"><span data-stu-id="b694b-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="b694b-107">設定原則之後，您可以使用 Excel 和 ODBC 驅動程式連接到 HDInsight 中的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="b694b-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b694b-108">先決條件</span><span class="sxs-lookup"><span data-stu-id="b694b-108">Prerequisites</span></span>
* <span data-ttu-id="b694b-109">已加入網域的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b694b-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="b694b-110">請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="b694b-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="b694b-111">安裝 Office 2016、Office 2013 Professional Plus、Office 365 Pro Plus、Excel 2013 Standalone 或 Office 2010 Professional Plus 的工作站。</span><span class="sxs-lookup"><span data-stu-id="b694b-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="b694b-112">連線到 Apache Ranger 系統管理 UI</span><span class="sxs-lookup"><span data-stu-id="b694b-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="b694b-113">**到 Ranger 系統管理 UI**</span><span class="sxs-lookup"><span data-stu-id="b694b-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="b694b-114">從瀏覽器連線到 Ranger 系統管理 UI。</span><span class="sxs-lookup"><span data-stu-id="b694b-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="b694b-115">URL 是 https://&lt;ClusterName>.azurehdinsight.net/Ranger/。</span><span class="sxs-lookup"><span data-stu-id="b694b-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b694b-116">Ranger 會使用與 Hadoop 叢集不同的認證。</span><span class="sxs-lookup"><span data-stu-id="b694b-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="b694b-117">若要避免瀏覽器使用快取的 Hadoop 認證，請使用新的 InPrivate 瀏覽器視窗連接至 Ranger 系統管理 UI。</span><span class="sxs-lookup"><span data-stu-id="b694b-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="b694b-118">使用叢集系統管理員網域使用者名稱和密碼進行登入：</span><span class="sxs-lookup"><span data-stu-id="b694b-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![HDInsight 已加入網域的 Ranger 首頁](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="b694b-120">目前，Ranger 僅適用於 Yarn 和 Hive。</span><span class="sxs-lookup"><span data-stu-id="b694b-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="b694b-121">建立網域使用者</span><span class="sxs-lookup"><span data-stu-id="b694b-121">Create Domain users</span></span>
<span data-ttu-id="b694b-122">在[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)中，您已建立 hiveruser1 和 hiveuser2。</span><span class="sxs-lookup"><span data-stu-id="b694b-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="b694b-123">在本教學課程中，您將使用兩個使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b694b-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="b694b-124">建立 Ranger 原則</span><span class="sxs-lookup"><span data-stu-id="b694b-124">Create Ranger policies</span></span>
<span data-ttu-id="b694b-125">在這一節中，您將建立兩個 Ranger 原則以供存取 hivesampletable。</span><span class="sxs-lookup"><span data-stu-id="b694b-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="b694b-126">您會提供不同資料行集的選取權限。</span><span class="sxs-lookup"><span data-stu-id="b694b-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="b694b-127">兩個使用者都建立於[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)。</span><span class="sxs-lookup"><span data-stu-id="b694b-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="b694b-128">在下一節中，您將在 Excel 中測試這兩個原則。</span><span class="sxs-lookup"><span data-stu-id="b694b-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="b694b-129">**建立 Ranger 原則**</span><span class="sxs-lookup"><span data-stu-id="b694b-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="b694b-130">開啟 Ranger 系統管理 UI。</span><span class="sxs-lookup"><span data-stu-id="b694b-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="b694b-131">請參閱[連接到 Apache Ranger 系統管理 UI](#connect-to-apache-ranager-admin-ui)。</span><span class="sxs-lookup"><span data-stu-id="b694b-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="b694b-132">按一下 [Hive] 下的 **&lt;ClusterName>_hive**。</span><span class="sxs-lookup"><span data-stu-id="b694b-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="b694b-133">您會看到兩個預先設定的原則。</span><span class="sxs-lookup"><span data-stu-id="b694b-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="b694b-134">按一下 [新增原則]，然後輸入下列值︰</span><span class="sxs-lookup"><span data-stu-id="b694b-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="b694b-135">原則名稱︰read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="b694b-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="b694b-136">Hive 資料庫︰預設值</span><span class="sxs-lookup"><span data-stu-id="b694b-136">Hive Database: default</span></span>
   * <span data-ttu-id="b694b-137">資料表：hivesampletable</span><span class="sxs-lookup"><span data-stu-id="b694b-137">table: hivesampletable</span></span>
   * <span data-ttu-id="b694b-138">Hive 資料欄：*</span><span class="sxs-lookup"><span data-stu-id="b694b-138">Hive column: *</span></span>
   * <span data-ttu-id="b694b-139">選取使用者：hiveuser1</span><span class="sxs-lookup"><span data-stu-id="b694b-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="b694b-140">權限：選取</span><span class="sxs-lookup"><span data-stu-id="b694b-140">Permissions: select</span></span>

     ![HDInsight 已加入網域的 Ranger Hive 原則設定](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="b694b-142">。</span><span class="sxs-lookup"><span data-stu-id="b694b-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b694b-143">如果 [選取使用者] 中未填入網域使用者，請稍等一下讓 Ranger 與 AAD 同步處理。</span><span class="sxs-lookup"><span data-stu-id="b694b-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="b694b-144">按一下 [新增] 以儲存規則。</span><span class="sxs-lookup"><span data-stu-id="b694b-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="b694b-145">重複最後兩個步驟，使用下列屬性建立另一個原則︰</span><span class="sxs-lookup"><span data-stu-id="b694b-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="b694b-146">原則名稱︰read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="b694b-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="b694b-147">Hive 資料庫︰預設值</span><span class="sxs-lookup"><span data-stu-id="b694b-147">Hive Database: default</span></span>
   * <span data-ttu-id="b694b-148">資料表：hivesampletable</span><span class="sxs-lookup"><span data-stu-id="b694b-148">table: hivesampletable</span></span>
   * <span data-ttu-id="b694b-149">Hive 資料行︰clientid、devicemake</span><span class="sxs-lookup"><span data-stu-id="b694b-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="b694b-150">選取使用者：hiveuser2</span><span class="sxs-lookup"><span data-stu-id="b694b-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="b694b-151">權限：選取</span><span class="sxs-lookup"><span data-stu-id="b694b-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="b694b-152">建立 Hive ODBC 資料來源</span><span class="sxs-lookup"><span data-stu-id="b694b-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="b694b-153">在[建立 Hive ODBC 資料來源](hdinsight-connect-excel-hive-odbc-driver.md)中可找到相關指示。</span><span class="sxs-lookup"><span data-stu-id="b694b-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="b694b-154">屬性</span><span class="sxs-lookup"><span data-stu-id="b694b-154">Property</span></span>|<span data-ttu-id="b694b-155">描述</span><span class="sxs-lookup"><span data-stu-id="b694b-155">Description</span></span>
    ---|---
    <span data-ttu-id="b694b-156">資料來源名稱</span><span class="sxs-lookup"><span data-stu-id="b694b-156">Data Source Name</span></span>|<span data-ttu-id="b694b-157">為資料來源指定名稱</span><span class="sxs-lookup"><span data-stu-id="b694b-157">Give a name to your data source</span></span>
    <span data-ttu-id="b694b-158">Host</span><span class="sxs-lookup"><span data-stu-id="b694b-158">Host</span></span>|<span data-ttu-id="b694b-159">輸入 &lt;HDInsightClusterName>.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="b694b-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="b694b-160">例如，myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="b694b-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="b694b-161">連接埠</span><span class="sxs-lookup"><span data-stu-id="b694b-161">Port</span></span>|<span data-ttu-id="b694b-162">使用 <strong>443</strong></span><span class="sxs-lookup"><span data-stu-id="b694b-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="b694b-163">(此連接埠已從 563 變更為 443)。</span><span class="sxs-lookup"><span data-stu-id="b694b-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="b694b-164">資料庫</span><span class="sxs-lookup"><span data-stu-id="b694b-164">Database</span></span>|<span data-ttu-id="b694b-165">使用<strong>預設值</strong></span><span class="sxs-lookup"><span data-stu-id="b694b-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="b694b-166">Hive 伺服器類型</span><span class="sxs-lookup"><span data-stu-id="b694b-166">Hive Server Type</span></span>|<span data-ttu-id="b694b-167">選取 [Hive Server 2]<strong></strong></span><span class="sxs-lookup"><span data-stu-id="b694b-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="b694b-168">機制</span><span class="sxs-lookup"><span data-stu-id="b694b-168">Mechanism</span></span>|<span data-ttu-id="b694b-169">選取 [Azure HDInsight 服務]<strong></strong></span><span class="sxs-lookup"><span data-stu-id="b694b-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="b694b-170">HTTP 路徑</span><span class="sxs-lookup"><span data-stu-id="b694b-170">HTTP Path</span></span>|<span data-ttu-id="b694b-171">保留為空白。</span><span class="sxs-lookup"><span data-stu-id="b694b-171">Leave it blank.</span></span>
    <span data-ttu-id="b694b-172">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b694b-172">User Name</span></span>|<span data-ttu-id="b694b-173">輸入 hiveuser1@contoso158.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="b694b-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="b694b-174">更新網域名稱 (如果不同的話)。</span><span class="sxs-lookup"><span data-stu-id="b694b-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="b694b-175">密碼</span><span class="sxs-lookup"><span data-stu-id="b694b-175">Password</span></span>|<span data-ttu-id="b694b-176">輸入 hiveuser1 的密碼。</span><span class="sxs-lookup"><span data-stu-id="b694b-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="b694b-177">請務必先按一下 [測試]，再儲存資料來源。</span><span class="sxs-lookup"><span data-stu-id="b694b-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="b694b-178">從 HDInsight 將資料匯入 Excel 中</span><span class="sxs-lookup"><span data-stu-id="b694b-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="b694b-179">在上一節中，您已設定兩個原則。</span><span class="sxs-lookup"><span data-stu-id="b694b-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="b694b-180">hiveuser1 具有所有資料行的選取權限，而 hiveuser2 具有兩個資料行的選取權限。</span><span class="sxs-lookup"><span data-stu-id="b694b-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="b694b-181">本節中，您可以模擬兩位使用者將資料匯入 Excel 中。</span><span class="sxs-lookup"><span data-stu-id="b694b-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="b694b-182">在 Excel 中開啟新的或現有的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="b694b-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="b694b-183">在 [資料] 索引標籤上按一下 [從其他資料來源]，然後按一下 [從資料連接精靈]，以啟動 [資料連接精靈]。</span><span class="sxs-lookup"><span data-stu-id="b694b-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="b694b-184">![開啟資料連接精靈][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="b694b-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="b694b-185">選取 [ODBC DSN] 作為資料來源，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b694b-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="b694b-186">從 ODBC 資料來源中，選取您在上一個步驟中建立的資料來源名稱，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b694b-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="b694b-187">在精靈中重新輸入叢集的密碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b694b-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="b694b-188">等待 [選取資料庫及資料表]  對話方塊開啟。</span><span class="sxs-lookup"><span data-stu-id="b694b-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="b694b-189">這可能需要幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="b694b-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="b694b-190">選取 **hivesampletable**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b694b-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="b694b-191">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="b694b-191">Click **Finish**.</span></span>
8. <span data-ttu-id="b694b-192">在 [匯入資料]  對話方塊中，您可以變更或指定查詢。</span><span class="sxs-lookup"><span data-stu-id="b694b-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="b694b-193">若要執行此動作，請按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="b694b-193">To do so, click **Properties**.</span></span> <span data-ttu-id="b694b-194">這可能需要幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="b694b-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="b694b-195">按一下 [定義] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b694b-195">Click the **Definition** tab.</span></span> <span data-ttu-id="b694b-196">命令文字如下：</span><span class="sxs-lookup"><span data-stu-id="b694b-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="b694b-197">您定義的 Ranger 原則，hiveuser1 會有所有資料行的選取權限。</span><span class="sxs-lookup"><span data-stu-id="b694b-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="b694b-198">所以此查詢適用於 hiveuser1 的認證，但此查詢不適用於 hiveuser2 的認證。</span><span class="sxs-lookup"><span data-stu-id="b694b-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="b694b-199">![連接屬性][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="b694b-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="b694b-200">按一下 [確定]  以關閉 [連接屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b694b-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="b694b-201">按一下 [確定] 以關閉 [匯入資料] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b694b-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="b694b-202">重新輸入 hiveuser1 的密碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b694b-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="b694b-203">經過數秒後，資料即會匯入至 Excel。</span><span class="sxs-lookup"><span data-stu-id="b694b-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="b694b-204">完成時，您會看到 11 個資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="b694b-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="b694b-205">測試您在上一節中建立的第二個原則 (read-hivesampletable-devicemake)</span><span class="sxs-lookup"><span data-stu-id="b694b-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="b694b-206">在 Excel 中新增工作表。</span><span class="sxs-lookup"><span data-stu-id="b694b-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="b694b-207">依照上一個程序匯入資料。</span><span class="sxs-lookup"><span data-stu-id="b694b-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="b694b-208">您會進行的唯一變更是使用 hiveuser2 的認證，而非使用 hiveuser1 的認證。</span><span class="sxs-lookup"><span data-stu-id="b694b-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="b694b-209">這將會失敗，因為 hiveuser2 只有查看兩個資料行的權限。</span><span class="sxs-lookup"><span data-stu-id="b694b-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="b694b-210">您會收到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="b694b-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="b694b-211">依照相同程序匯入資料。</span><span class="sxs-lookup"><span data-stu-id="b694b-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="b694b-212">這次使用 hiveuser2 的認證，並且修改 select 陳述式，從︰</span><span class="sxs-lookup"><span data-stu-id="b694b-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="b694b-213">至：</span><span class="sxs-lookup"><span data-stu-id="b694b-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="b694b-214">完成時，您會看到已匯入 2 個資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="b694b-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b694b-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b694b-215">Next steps</span></span>
* <span data-ttu-id="b694b-216">如需設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInisight 叢集](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="b694b-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="b694b-217">如需管理已加入網域的 HDInsight 叢集，請參閱[管理已加入網域的 HDInisight 叢集](hdinsight-domain-joined-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="b694b-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="b694b-218">若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。</span><span class="sxs-lookup"><span data-stu-id="b694b-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="b694b-219">如需使用 Hive JDBC 連接 Hive，請參閱 [使用 Hive JDBC 驅動程式連接到 Azure HDInsight 上的 Hive](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="b694b-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="b694b-220">如需使用 Hive ODBC 將 Excel 連接到 Hadoop，請參閱[使用 Microsoft Hive ODBC 驅動程式將 Excel 連接到 Hadoop](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="b694b-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="b694b-221">如需使用 Power Query 將 Excel 連接到 Hadoop，請參閱[使用 Power Query 將 Excel 連接到 Hadoop](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="b694b-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
