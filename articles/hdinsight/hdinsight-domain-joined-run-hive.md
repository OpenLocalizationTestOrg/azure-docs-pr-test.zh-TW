---
title: "已加入網域的 HDInsight 的 Azure 中的 aaaConfigure Hive 原則 |Microsoft 文件"
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
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="ccd43-103">在已加入網域的 HDInsight (預覽) 中設定 Hive 原則</span><span class="sxs-lookup"><span data-stu-id="ccd43-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="ccd43-104">深入了解如何登錄區的 tooconfigure Apache Ranger 原則。</span><span class="sxs-lookup"><span data-stu-id="ccd43-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="ccd43-105">在本文中，您可以建立兩個 Ranger 原則 toorestrict 存取 toohello hivesampletable。</span><span class="sxs-lookup"><span data-stu-id="ccd43-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="ccd43-106">hello hivesampletable 隨附的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ccd43-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="ccd43-107">您已設定 hello 原則之後，您可以使用 Excel 與 ODBC 驅動程式 tooconnect tooHive 資料表 HDInsight 中。</span><span class="sxs-lookup"><span data-stu-id="ccd43-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccd43-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="ccd43-108">Prerequisites</span></span>
* <span data-ttu-id="ccd43-109">已加入網域的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ccd43-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="ccd43-110">請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ccd43-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="ccd43-111">安裝 Office 2016、Office 2013 Professional Plus、Office 365 Pro Plus、Excel 2013 Standalone 或 Office 2010 Professional Plus 的工作站。</span><span class="sxs-lookup"><span data-stu-id="ccd43-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="ccd43-112">連接 tooApache Ranger Admin UI</span><span class="sxs-lookup"><span data-stu-id="ccd43-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="ccd43-113">**tooconnect tooRanger Admin UI**</span><span class="sxs-lookup"><span data-stu-id="ccd43-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="ccd43-114">從瀏覽器中，連接 tooRanger Admin UI。</span><span class="sxs-lookup"><span data-stu-id="ccd43-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="ccd43-115">hello URL 是 https://&lt;ClusterName >.azurehdinsight.net/Ranger/。</span><span class="sxs-lookup"><span data-stu-id="ccd43-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ccd43-116">Ranger 會使用與 Hadoop 叢集不同的認證。</span><span class="sxs-lookup"><span data-stu-id="ccd43-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="ccd43-117">使用快取的 Hadoop 認證 tooprevent 瀏覽器使用新的 inprivate 瀏覽器視窗 tooconnect toohello Ranger Admin UI。</span><span class="sxs-lookup"><span data-stu-id="ccd43-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="ccd43-118">使用登入 hello 叢集系統管理員的網域使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="ccd43-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![HDInsight 已加入網域的 Ranger 首頁](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="ccd43-120">目前，Ranger 僅適用於 Yarn 和 Hive。</span><span class="sxs-lookup"><span data-stu-id="ccd43-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="ccd43-121">建立網域使用者</span><span class="sxs-lookup"><span data-stu-id="ccd43-121">Create Domain users</span></span>
<span data-ttu-id="ccd43-122">在[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)中，您已建立 hiveruser1 和 hiveuser2。</span><span class="sxs-lookup"><span data-stu-id="ccd43-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="ccd43-123">您將在本教學課程使用 hello 兩個使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccd43-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="ccd43-124">建立 Ranger 原則</span><span class="sxs-lookup"><span data-stu-id="ccd43-124">Create Ranger policies</span></span>
<span data-ttu-id="ccd43-125">在這一節中，您將建立兩個 Ranger 原則以供存取 hivesampletable。</span><span class="sxs-lookup"><span data-stu-id="ccd43-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="ccd43-126">您會提供不同資料行集的選取權限。</span><span class="sxs-lookup"><span data-stu-id="ccd43-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="ccd43-127">兩個使用者都建立於[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)。</span><span class="sxs-lookup"><span data-stu-id="ccd43-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="ccd43-128">在 hello 下一步 區段中，您將測試在 Excel 中的 hello 兩個原則。</span><span class="sxs-lookup"><span data-stu-id="ccd43-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="ccd43-129">**toocreate Ranger 原則**</span><span class="sxs-lookup"><span data-stu-id="ccd43-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="ccd43-130">開啟 Ranger 系統管理 UI。</span><span class="sxs-lookup"><span data-stu-id="ccd43-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="ccd43-131">請參閱[連接 tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui)。</span><span class="sxs-lookup"><span data-stu-id="ccd43-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="ccd43-132">按一下 [Hive] 下的 **&lt;ClusterName>_hive**。</span><span class="sxs-lookup"><span data-stu-id="ccd43-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="ccd43-133">您會看到兩個預先設定的原則。</span><span class="sxs-lookup"><span data-stu-id="ccd43-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="ccd43-134">按一下**新增原則**，然後輸入 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="ccd43-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="ccd43-135">原則名稱︰read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="ccd43-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="ccd43-136">Hive 資料庫︰預設值</span><span class="sxs-lookup"><span data-stu-id="ccd43-136">Hive Database: default</span></span>
   * <span data-ttu-id="ccd43-137">資料表：hivesampletable</span><span class="sxs-lookup"><span data-stu-id="ccd43-137">table: hivesampletable</span></span>
   * <span data-ttu-id="ccd43-138">Hive 資料欄：*</span><span class="sxs-lookup"><span data-stu-id="ccd43-138">Hive column: *</span></span>
   * <span data-ttu-id="ccd43-139">選取使用者：hiveuser1</span><span class="sxs-lookup"><span data-stu-id="ccd43-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="ccd43-140">權限：選取</span><span class="sxs-lookup"><span data-stu-id="ccd43-140">Permissions: select</span></span>

     ![HDInsight 已加入網域的 Ranger Hive 原則設定](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="ccd43-142">.</span><span class="sxs-lookup"><span data-stu-id="ccd43-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ccd43-143">如果未在 選取使用者填入的網域使用者，請稍候片刻 Ranger toosync aad。</span><span class="sxs-lookup"><span data-stu-id="ccd43-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="ccd43-144">按一下**新增**toosave hello 原則。</span><span class="sxs-lookup"><span data-stu-id="ccd43-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="ccd43-145">重複 hello 最後兩個步驟 toocreate 另一個原則以 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="ccd43-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="ccd43-146">原則名稱︰read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="ccd43-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="ccd43-147">Hive 資料庫︰預設值</span><span class="sxs-lookup"><span data-stu-id="ccd43-147">Hive Database: default</span></span>
   * <span data-ttu-id="ccd43-148">資料表：hivesampletable</span><span class="sxs-lookup"><span data-stu-id="ccd43-148">table: hivesampletable</span></span>
   * <span data-ttu-id="ccd43-149">Hive 資料行︰clientid、devicemake</span><span class="sxs-lookup"><span data-stu-id="ccd43-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="ccd43-150">選取使用者：hiveuser2</span><span class="sxs-lookup"><span data-stu-id="ccd43-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="ccd43-151">權限：選取</span><span class="sxs-lookup"><span data-stu-id="ccd43-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="ccd43-152">建立 Hive ODBC 資料來源</span><span class="sxs-lookup"><span data-stu-id="ccd43-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="ccd43-153">中可以找到 hello 指示[建立 hive 控制檔的 ODBC 資料來源](hdinsight-connect-excel-hive-odbc-driver.md)。</span><span class="sxs-lookup"><span data-stu-id="ccd43-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="ccd43-154">屬性</span><span class="sxs-lookup"><span data-stu-id="ccd43-154">Property</span></span>|<span data-ttu-id="ccd43-155">描述</span><span class="sxs-lookup"><span data-stu-id="ccd43-155">Description</span></span>
    ---|---
    <span data-ttu-id="ccd43-156">資料來源名稱</span><span class="sxs-lookup"><span data-stu-id="ccd43-156">Data Source Name</span></span>|<span data-ttu-id="ccd43-157">提供名稱 tooyour 資料來源</span><span class="sxs-lookup"><span data-stu-id="ccd43-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="ccd43-158">Host</span><span class="sxs-lookup"><span data-stu-id="ccd43-158">Host</span></span>|<span data-ttu-id="ccd43-159">輸入 &lt;HDInsightClusterName>.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="ccd43-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="ccd43-160">例如，myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="ccd43-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="ccd43-161">連接埠</span><span class="sxs-lookup"><span data-stu-id="ccd43-161">Port</span></span>|<span data-ttu-id="ccd43-162">使用 <strong>443</strong></span><span class="sxs-lookup"><span data-stu-id="ccd43-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="ccd43-163">（此連接埠已變更從 563 too443）。</span><span class="sxs-lookup"><span data-stu-id="ccd43-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="ccd43-164">資料庫</span><span class="sxs-lookup"><span data-stu-id="ccd43-164">Database</span></span>|<span data-ttu-id="ccd43-165">使用<strong>預設值</strong></span><span class="sxs-lookup"><span data-stu-id="ccd43-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="ccd43-166">Hive 伺服器類型</span><span class="sxs-lookup"><span data-stu-id="ccd43-166">Hive Server Type</span></span>|<span data-ttu-id="ccd43-167">選取 [Hive Server 2]<strong></strong></span><span class="sxs-lookup"><span data-stu-id="ccd43-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="ccd43-168">機制</span><span class="sxs-lookup"><span data-stu-id="ccd43-168">Mechanism</span></span>|<span data-ttu-id="ccd43-169">選取 [Azure HDInsight 服務]<strong></strong></span><span class="sxs-lookup"><span data-stu-id="ccd43-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="ccd43-170">HTTP 路徑</span><span class="sxs-lookup"><span data-stu-id="ccd43-170">HTTP Path</span></span>|<span data-ttu-id="ccd43-171">保留為空白。</span><span class="sxs-lookup"><span data-stu-id="ccd43-171">Leave it blank.</span></span>
    <span data-ttu-id="ccd43-172">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="ccd43-172">User Name</span></span>|<span data-ttu-id="ccd43-173">輸入 hiveuser1@contoso158.onmicrosoft.com。如果不同，請更新 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ccd43-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="ccd43-174">密碼</span><span class="sxs-lookup"><span data-stu-id="ccd43-174">Password</span></span>|<span data-ttu-id="ccd43-175">輸入 hiveuser1 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="ccd43-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="ccd43-176">請確定 tooclick**測試**之前儲存 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="ccd43-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="ccd43-177">從 HDInsight 將資料匯入 Excel 中</span><span class="sxs-lookup"><span data-stu-id="ccd43-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="ccd43-178">在 hello 最後一個區段中，您已設定兩個原則。</span><span class="sxs-lookup"><span data-stu-id="ccd43-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="ccd43-179">hiveuser1 hello 的 select 權限的所有 hello 資料行，而且 hiveuser2 hello 選取兩個資料行權限。</span><span class="sxs-lookup"><span data-stu-id="ccd43-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="ccd43-180">在本節中，您可以模擬 hello 兩位使用者 tooimport 資料到 Excel。</span><span class="sxs-lookup"><span data-stu-id="ccd43-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="ccd43-181">在 Excel 中開啟新的或現有的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="ccd43-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="ccd43-182">從 hello**資料**索引標籤上，按一下 **從其他資料來源**，然後按一下**從資料連線精靈**toolaunch hello**資料連線精靈**.</span><span class="sxs-lookup"><span data-stu-id="ccd43-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="ccd43-183">![開啟資料連接精靈][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="ccd43-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="ccd43-184">選取**ODBC DSN**作為 hello 資料來源，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ccd43-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="ccd43-185">從 ODBC 資料來源選取 hello 資料來源在 hello 先前步驟中，您建立的名稱，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ccd43-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="ccd43-186">重新輸入 hello 叢集 hello 精靈中的 hello 密碼，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="ccd43-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="ccd43-187">等候 hello**選取資料庫和資料表**對話方塊 tooopen。</span><span class="sxs-lookup"><span data-stu-id="ccd43-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="ccd43-188">這可能需要幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ccd43-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="ccd43-189">選取 **hivesampletable**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ccd43-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="ccd43-190">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="ccd43-190">Click **Finish**.</span></span>
8. <span data-ttu-id="ccd43-191">在 [hello**匯入資料**] 對話方塊中，您可以變更，或指定 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="ccd43-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="ccd43-192">因此，按一下 toodo**屬性**。</span><span class="sxs-lookup"><span data-stu-id="ccd43-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="ccd43-193">這可能需要幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ccd43-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="ccd43-194">按一下 hello**定義** 索引標籤 hello 命令文字：</span><span class="sxs-lookup"><span data-stu-id="ccd43-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="ccd43-195">由您定義 hello Ranger 原則，hiveuser1 具有 hello 的所有資料行的 select 權限。</span><span class="sxs-lookup"><span data-stu-id="ccd43-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="ccd43-196">所以此查詢適用於 hiveuser1 的認證，但此查詢不適用於 hiveuser2 的認證。</span><span class="sxs-lookup"><span data-stu-id="ccd43-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="ccd43-197">![連接屬性][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="ccd43-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="ccd43-198">按一下**確定**tooclose hello 連接屬性 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ccd43-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="ccd43-199">按一下**確定**tooclose hello**匯入資料**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ccd43-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="ccd43-200">重新輸入 hello hiveuser1，密碼，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="ccd43-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="ccd43-201">花幾秒鐘，才能資料取得匯入的 tooExcel。</span><span class="sxs-lookup"><span data-stu-id="ccd43-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="ccd43-202">完成時，您會看到 11 個資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="ccd43-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="ccd43-203">您在 hello 最後一節中建立 tootest hello 第二個原則 (讀取-hivesampletable-devicemake)</span><span class="sxs-lookup"><span data-stu-id="ccd43-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="ccd43-204">在 Excel 中新增工作表。</span><span class="sxs-lookup"><span data-stu-id="ccd43-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="ccd43-205">請遵循 hello 最後一個程序 tooimport hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ccd43-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="ccd43-206">hello 唯一的變更，您將會是 toouse hiveuser2 認證，而不是 hiveuser1 的。</span><span class="sxs-lookup"><span data-stu-id="ccd43-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="ccd43-207">這將會失敗，因為 hiveuser2 只有權限 toosee 兩個資料行。</span><span class="sxs-lookup"><span data-stu-id="ccd43-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="ccd43-208">您應該會收到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="ccd43-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="ccd43-209">後續 hello 相同程序 tooimport 資料。</span><span class="sxs-lookup"><span data-stu-id="ccd43-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="ccd43-210">此時，請使用 hiveuser2 的認證，以及修改 hello 從 select 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ccd43-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="ccd43-211">至：</span><span class="sxs-lookup"><span data-stu-id="ccd43-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="ccd43-212">完成時，您會看到已匯入 2 個資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="ccd43-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccd43-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccd43-213">Next steps</span></span>
* <span data-ttu-id="ccd43-214">如需設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInisight 叢集](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ccd43-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="ccd43-215">如需管理已加入網域的 HDInsight 叢集，請參閱[管理已加入網域的 HDInisight 叢集](hdinsight-domain-joined-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="ccd43-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="ccd43-216">若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。</span><span class="sxs-lookup"><span data-stu-id="ccd43-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="ccd43-217">連接 hive 控制檔使用 Hive JDBC，請參閱[tooHive hello Hive JDBC 驅動程式使用 Azure HDInsight 上的連接](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="ccd43-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="ccd43-218">使用 hive 控制檔的 ODBC 連接的 Excel tooHadoop，請參閱[連接 Excel tooHadoop 以 hello Microsoft Hive ODBC 磁碟機](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="ccd43-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="ccd43-219">使用 Power Query 連接的 Excel tooHadoop，請參閱[使用 Power Query 連接的 Excel tooHadoop](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="ccd43-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
