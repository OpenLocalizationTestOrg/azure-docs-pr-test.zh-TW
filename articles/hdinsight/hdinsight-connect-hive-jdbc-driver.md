---
title: "透過 hello JDBC 驅動程式的 Azure HDInsight 的 Hive aaaQuery |Microsoft 文件"
description: "HDInsight 上使用從 Java 應用程式 toosubmit Hive 查詢 tooHadoop hello JDBC 驅動程式。 以程式設計的方式和從 hello 松鼠 SQL 用戶端連接。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="51b2e-104">Hive 查詢透過 HDInsight 中的 hello JDBC 驅動程式</span><span class="sxs-lookup"><span data-stu-id="51b2e-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="51b2e-105">了解如何從 Java 應用程式 toosubmit Hive toouse hello JDBC 驅動程式查詢 Azure HDInsight 中的 tooHadoop。</span><span class="sxs-lookup"><span data-stu-id="51b2e-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="51b2e-106">本文件中的 hello 資訊會示範如何 tooconnect 以程式設計的方式與 hello 松鼠 SQL 用戶端。</span><span class="sxs-lookup"><span data-stu-id="51b2e-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="51b2e-107">如需有關 hello Hive JDBC 介面的詳細資訊，請參閱[HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface)。</span><span class="sxs-lookup"><span data-stu-id="51b2e-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51b2e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="51b2e-108">Prerequisites</span></span>

* <span data-ttu-id="51b2e-109">HDInsight 叢集上的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="51b2e-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="51b2e-110">以 Linux 或 Windows 為基礎的叢集都可運作。</span><span class="sxs-lookup"><span data-stu-id="51b2e-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="51b2e-111">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="51b2e-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="51b2e-112">如需詳細資訊，請參閱 [HDInsight 3.3 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="51b2e-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="51b2e-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/)。</span><span class="sxs-lookup"><span data-stu-id="51b2e-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="51b2e-114">SQuirreL 是 JDBC 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="51b2e-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="51b2e-115">hello [Java Developer Kit (JDK) 第 7 版](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="51b2e-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="51b2e-116">[Apache Maven](https://maven.apache.org)。</span><span class="sxs-lookup"><span data-stu-id="51b2e-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="51b2e-117">Maven 是專案建立 Java 專案由與此發行項相關聯的 hello 專案的系統。</span><span class="sxs-lookup"><span data-stu-id="51b2e-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="51b2e-118">JDBC 連接字串</span><span class="sxs-lookup"><span data-stu-id="51b2e-118">JDBC connection string</span></span>

<span data-ttu-id="51b2e-119">JDBC 連接 tooan HDInsight 叢集在 Azure 上的超過 443，會使用 SSL 來保護 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="51b2e-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="51b2e-120">hello 後面坐 hello 叢集的公用閘道重新導向 hello 流量 toohello 接聽連接埠 HiveServer2 是實際。</span><span class="sxs-lookup"><span data-stu-id="51b2e-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="51b2e-121">hello 以下是範例連接字串：</span><span class="sxs-lookup"><span data-stu-id="51b2e-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="51b2e-122">取代`CLUSTERNAME`hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="51b2e-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="51b2e-123">驗證</span><span class="sxs-lookup"><span data-stu-id="51b2e-123">Authentication</span></span>

<span data-ttu-id="51b2e-124">在建立 hello 連接時，您必須使用 hello HDInsight 叢集系統管理員名稱和密碼 tooauthenticate toohello 叢集閘道。</span><span class="sxs-lookup"><span data-stu-id="51b2e-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="51b2e-125">當從例如松鼠 SQL JDBC 用戶端連線，您必須輸入用戶端設定中的 hello 管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="51b2e-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="51b2e-126">從 Java 應用程式，您必須使用 hello 名稱和密碼建立的連接時。</span><span class="sxs-lookup"><span data-stu-id="51b2e-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="51b2e-127">例如，hello 下列 Java 程式碼會開啟新的連接使用 hello 連接字串、 管理員名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="51b2e-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="51b2e-128">使用 SQuirreL SQL 用戶端連接</span><span class="sxs-lookup"><span data-stu-id="51b2e-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="51b2e-129">松鼠 SQL 是 JDBC 用戶端可以使用的 tooremotely 執行 Hive 查詢與您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="51b2e-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="51b2e-130">hello 下列步驟假設您已安裝松鼠 SQL。</span><span class="sxs-lookup"><span data-stu-id="51b2e-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="51b2e-131">Hello Hive JDBC 驅動程式複製您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="51b2e-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="51b2e-132">如**以 Linux 為基礎的 HDInsight**，使用 hello 下列步驟 toodownload 所需的 hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="51b2e-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="51b2e-133">建立包含 hello 檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="51b2e-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="51b2e-134">例如： `mkdir hivedriver`。</span><span class="sxs-lookup"><span data-stu-id="51b2e-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="51b2e-135">從命令列使用 hello 下列命令從 hello HDInsight 叢集 toocopy hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="51b2e-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="51b2e-136">取代`USERNAME`hello 叢集 hello SSH 使用者帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="51b2e-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="51b2e-137">取代`CLUSTERNAME`與 hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="51b2e-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="51b2e-138">如**Windows 為基礎的 HDInsight**，使用 hello 下列步驟 toodownload hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="51b2e-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="51b2e-139">從 hello Azure 入口網站，選取您的 HDInsight 叢集，然後選取 hello**遠端桌面**圖示。</span><span class="sxs-lookup"><span data-stu-id="51b2e-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![遠端桌面圖示](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="51b2e-141">Hello 遠端桌面 刀鋒視窗中，使用 hello**連接**按鈕 tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="51b2e-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="51b2e-142">如果未啟用 hello 遠端桌面，使用 hello 表單 tooprovide 使用者名稱和密碼，然後選取 **啟用**hello 叢集 tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="51b2e-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![遠端桌面刀鋒視窗](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="51b2e-144">選取 [連線] 後，系統會下載 .rdp 檔案。</span><span class="sxs-lookup"><span data-stu-id="51b2e-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="51b2e-145">使用此檔案 toolaunch hello 遠端桌面用戶端。</span><span class="sxs-lookup"><span data-stu-id="51b2e-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="51b2e-146">出現提示時，使用您輸入的遠端桌面存取 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="51b2e-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="51b2e-147">一旦連接之後，複製下列檔案從 hello 遠端桌面工作階段 tooyour 本機電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="51b2e-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="51b2e-148">把它們放在名為 `hivedriver` 的本機目錄中。</span><span class="sxs-lookup"><span data-stu-id="51b2e-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="51b2e-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="51b2e-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="51b2e-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="51b2e-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="51b2e-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="51b2e-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="51b2e-152">hello hello 路徑和檔案名稱中包含的數字可能會為您的叢集不同的版本。</span><span class="sxs-lookup"><span data-stu-id="51b2e-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="51b2e-153">中斷連線 hello 遠端桌面工作階段一旦完成複製 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="51b2e-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="51b2e-154">啟動 hello 松鼠 SQL 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51b2e-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="51b2e-155">從 hello hello 視窗左邊，選取**驅動程式**。</span><span class="sxs-lookup"><span data-stu-id="51b2e-155">From hello left of hello window, select **Drivers**.</span></span>

    ![驅動程式 索引標籤上 hello 視窗左邊的 hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="51b2e-157">從頂端的 hello hello hello 圖示**驅動程式**對話方塊中，選取 hello  **+** 圖示 toocreate 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="51b2e-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![[驅動程式] 圖示](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="51b2e-159">在 [hello] 新增驅動程式對話方塊新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="51b2e-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="51b2e-160">**名稱**：Hive</span><span class="sxs-lookup"><span data-stu-id="51b2e-160">**Name**: Hive</span></span>
    * <span data-ttu-id="51b2e-161">**範例 URL**：`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="51b2e-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="51b2e-162">**額外的類別路徑**： 之前使用 hello 新增按鈕 tooadd hello jar 檔案下載</span><span class="sxs-lookup"><span data-stu-id="51b2e-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="51b2e-163">**類別名稱**：org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="51b2e-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![新增驅動程式對話方塊](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="51b2e-165">按一下**確定**toosave 這些設定。</span><span class="sxs-lookup"><span data-stu-id="51b2e-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="51b2e-166">在 hello hello 松鼠 SQL 視窗左邊，選取 **別名**。</span><span class="sxs-lookup"><span data-stu-id="51b2e-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="51b2e-167">然後按一下 hello  **+** 圖示 toocreate 連接別名。</span><span class="sxs-lookup"><span data-stu-id="51b2e-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![新增別名](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="51b2e-169">使用 hello 下列值 hello**新增別名**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="51b2e-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="51b2e-170">**名稱**：HDInsight 上的 Hive</span><span class="sxs-lookup"><span data-stu-id="51b2e-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="51b2e-171">**驅動程式**： 使用 hello 下拉式 tooselect hello **Hive**驅動程式</span><span class="sxs-lookup"><span data-stu-id="51b2e-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="51b2e-172">**URL**： jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="51b2e-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="51b2e-173">取代**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="51b2e-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="51b2e-174">**使用者名稱**: hello 您的 HDInsight 叢集的叢集登入帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="51b2e-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="51b2e-175">hello 預設值是`admin`。</span><span class="sxs-lookup"><span data-stu-id="51b2e-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="51b2e-176">**密碼**: hello hello 叢集登入帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="51b2e-176">**Password**: hello password for hello cluster login account.</span></span>

 ![[新增別名] 對話方塊](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="51b2e-178">使用 hello**測試**hello 連線可運作的按鈕 tooverify。</span><span class="sxs-lookup"><span data-stu-id="51b2e-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="51b2e-179">當**連接到： Hive HDInsight 上**對話方塊出現，請選取**連接**tooperform hello 測試。</span><span class="sxs-lookup"><span data-stu-id="51b2e-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="51b2e-180">如果 hello 測試成功，您會看到**連線成功**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="51b2e-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="51b2e-181">toosave hello 連接別名，使用 hello**確定**在 hello hello 底部的按鈕**新增別名**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="51b2e-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="51b2e-182">從 hello**連接到**松鼠 SQL 的 hello 頂端的下拉式清單中選取**Hive HDInsight 上**。</span><span class="sxs-lookup"><span data-stu-id="51b2e-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="51b2e-183">出現提示時，請選取 [連接]。</span><span class="sxs-lookup"><span data-stu-id="51b2e-183">When prompted, select **Connect**.</span></span>

    ![連接對話方塊](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="51b2e-185">一旦連接之後，輸入下列查詢 hello SQL 查詢] 對話方塊，然後選取 [hello hello**執行**圖示。</span><span class="sxs-lookup"><span data-stu-id="51b2e-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="51b2e-186">hello 結果區域應該會顯示 hello hello 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="51b2e-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![sql 查詢對話方塊，包括結果](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="51b2e-188">從範例 Java 應用程式連接</span><span class="sxs-lookup"><span data-stu-id="51b2e-188">Connect from an example Java application</span></span>

<span data-ttu-id="51b2e-189">使用 Java 用戶端 tooquery Hive HDInsight 上的範例將會位於[https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc)。</span><span class="sxs-lookup"><span data-stu-id="51b2e-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="51b2e-190">依照 hello 儲存機制 toobuild 中的 hello 指示，並執行 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="51b2e-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="51b2e-191">疑難排解</span><span class="sxs-lookup"><span data-stu-id="51b2e-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="51b2e-192">發生意外的錯誤嘗試 tooopen SQL 連線</span><span class="sxs-lookup"><span data-stu-id="51b2e-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="51b2e-193">**徵兆**： 連接時 tooan HDInsight 叢集版本 3.3 或 3.4，您可能會收到未預期的錯誤發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="51b2e-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="51b2e-194">這項錯誤的 hello 堆疊追蹤為開頭 hello 下列行：</span><span class="sxs-lookup"><span data-stu-id="51b2e-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="51b2e-195">**可能的原因**: hello hello commons codec.jar 檔案由松鼠和 hello hello hive 控制檔的 JDBC 元件所需的其中一個版本中不相符所造成這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="51b2e-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="51b2e-196">**解析**: toofix 這個錯誤，請使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="51b2e-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="51b2e-197">從您的 HDInsight 叢集下載 hello commons 轉碼器 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="51b2e-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="51b2e-198">結束松鼠，並前往 toohello 目錄松鼠系統上的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="51b2e-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="51b2e-199">在 hello 松鼠目錄中，在 hello`lib`取代 hello 現有 commons-codec.jar 以其中一個從 hello HDInsight 叢集下載的 hello 的目錄。</span><span class="sxs-lookup"><span data-stu-id="51b2e-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="51b2e-200">重新啟動 SQuirreL。</span><span class="sxs-lookup"><span data-stu-id="51b2e-200">Restart SQuirreL.</span></span> <span data-ttu-id="51b2e-201">連接 tooHive HDInsight 上的時，應該不會再發生 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="51b2e-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51b2e-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51b2e-202">Next steps</span></span>

<span data-ttu-id="51b2e-203">既然您已經學會如何使用 Hive，使用下列的 hello toouse JDBC toowork 會連結 tooexplore Azure HDInsight 以其他方式 toowork。</span><span class="sxs-lookup"><span data-stu-id="51b2e-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="51b2e-204">上傳資料 tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="51b2e-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="51b2e-205">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="51b2e-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="51b2e-206">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="51b2e-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="51b2e-207">搭配 HDInsight 使用 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="51b2e-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
