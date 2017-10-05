---
title: "透過 JDBC 驅動程式查詢 Hive - Azure HDInsight | Microsoft Docs"
description: "從 Java 應用程式使用 JDBC 驅動程式，將 Hive 查詢提交到 HDInsight 上的 Hadoop。 以程式設計方式連接和透過 SQuirrel SQL 用戶端連接。"
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
ms.openlocfilehash: f2de58c2763b2ddd0926336164738929c477c4ae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a><span data-ttu-id="323b9-104">在 HDInsight 中透過 JDBC 驅動程式查詢 Hive</span><span class="sxs-lookup"><span data-stu-id="323b9-104">Query Hive through the JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="323b9-105">了解如何從 Java 應用程式使用 JDBC 驅動程式將 Hive 查詢提交到 Azure HDInsight 中的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="323b9-105">Learn how to use the JDBC driver from a Java application to submit Hive queries to Hadoop in Azure HDInsight.</span></span> <span data-ttu-id="323b9-106">本文件中的資訊會示範如何以程式設計方式以及如何從 SQuirrel SQL 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="323b9-106">The information in this document demonstrates how to connect programmatically and from the SQuirrel SQL client.</span></span>

<span data-ttu-id="323b9-107">如需有關 Hive JDBC 介面的詳細資訊，請參閱 [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface)。</span><span class="sxs-lookup"><span data-stu-id="323b9-107">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="323b9-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="323b9-108">Prerequisites</span></span>

* <span data-ttu-id="323b9-109">HDInsight 叢集上的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="323b9-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="323b9-110">以 Linux 或 Windows 為基礎的叢集都可運作。</span><span class="sxs-lookup"><span data-stu-id="323b9-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="323b9-111">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="323b9-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="323b9-112">如需詳細資訊，請參閱 [HDInsight 3.3 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="323b9-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="323b9-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/)。</span><span class="sxs-lookup"><span data-stu-id="323b9-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="323b9-114">SQuirreL 是 JDBC 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="323b9-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="323b9-115">[Java Developer Kit (JDK) 第 7 版](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="323b9-115">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="323b9-116">[Apache Maven](https://maven.apache.org)。</span><span class="sxs-lookup"><span data-stu-id="323b9-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="323b9-117">Maven 是 Java 專案的專案建置系統，由與本文相關聯的專案所使用。</span><span class="sxs-lookup"><span data-stu-id="323b9-117">Maven is a project build system for Java projects that is used by the project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="323b9-118">JDBC 連接字串</span><span class="sxs-lookup"><span data-stu-id="323b9-118">JDBC connection string</span></span>

<span data-ttu-id="323b9-119">透過 443 在 Azure 上建立 HDInsight 叢集的 JDBC 連接，並使用 SSL 保護流量。</span><span class="sxs-lookup"><span data-stu-id="323b9-119">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span></span> <span data-ttu-id="323b9-120">背後有叢集的公用閘道器會將流量重新導向至 HiveServer2 實際接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="323b9-120">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="323b9-121">下列為範例連接字串：</span><span class="sxs-lookup"><span data-stu-id="323b9-121">The following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="323b9-122">將 `CLUSTERNAME` 替換為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="323b9-122">Replace `CLUSTERNAME` with the name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="323b9-123">驗證</span><span class="sxs-lookup"><span data-stu-id="323b9-123">Authentication</span></span>

<span data-ttu-id="323b9-124">建立連線時，您必須使用 HDInsight 叢集系統管理員名稱和密碼來通過叢集閘道器驗證。</span><span class="sxs-lookup"><span data-stu-id="323b9-124">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span></span> <span data-ttu-id="323b9-125">從 SQuirreL SQL 之類的 JDBC 用戶端連接時，您必須在用戶端設定中輸入系統管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="323b9-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span></span>

<span data-ttu-id="323b9-126">從 Java 應用程式建立連接時，您必須使用該名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="323b9-126">From a Java application, you must use the name and password when establishing a connection.</span></span> <span data-ttu-id="323b9-127">例如，下列 Java 程式碼會使用連接字串、系統管理員名稱和密碼開啟新的連接：</span><span class="sxs-lookup"><span data-stu-id="323b9-127">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="323b9-128">使用 SQuirreL SQL 用戶端連接</span><span class="sxs-lookup"><span data-stu-id="323b9-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="323b9-129">SQuirreL SQL 是可用來從遠端以 HDInsight 叢集執行 Hive 查詢的 JDBC 用戶端。</span><span class="sxs-lookup"><span data-stu-id="323b9-129">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="323b9-130">下列步驟假設您已安裝 SQuirreL SQL。</span><span class="sxs-lookup"><span data-stu-id="323b9-130">The following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="323b9-131">從 HDInsight 叢集複製 Hive JDBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="323b9-131">Copy the Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="323b9-132">對於**以 Linux 為基礎的 HDInsight**，請使用下列步驟來下載必要的 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="323b9-132">For **Linux-based HDInsight**, use the following steps to download the required jar files.</span></span>

        1. <span data-ttu-id="323b9-133">建立包含檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="323b9-133">Create a directory that contains the files.</span></span> <span data-ttu-id="323b9-134">例如： `mkdir hivedriver`。</span><span class="sxs-lookup"><span data-stu-id="323b9-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="323b9-135">從命令列中，使用下列命令從 HDInsight 叢集將檔案進行複製：</span><span class="sxs-lookup"><span data-stu-id="323b9-135">From a command line, use the following commands to copy the files from the HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="323b9-136">將 `USERNAME` 取代為叢集的 SSH 使用者帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="323b9-136">Replace `USERNAME` with the SSH user account name for the cluster.</span></span> <span data-ttu-id="323b9-137">將 `CLUSTERNAME` 取代為 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="323b9-137">Replace `CLUSTERNAME` with the HDInsight cluster name.</span></span>

    * <span data-ttu-id="323b9-138">對於**以 Windows 為基礎的 HDInsight**，請使用下列步驟來下載 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="323b9-138">For **Windows-based HDInsight**, use the following steps to download the jar files.</span></span>

        1. <span data-ttu-id="323b9-139">從 Azure 入口網站選取 HDInsight 叢集，然後選取 [遠端桌面] 圖示。</span><span class="sxs-lookup"><span data-stu-id="323b9-139">From the Azure portal, select your HDInsight cluster, and then select the **Remote Desktop** icon.</span></span>

            ![遠端桌面圖示](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="323b9-141">在 [遠端桌面] 刀鋒視窗中，使用 [連接] 按鈕來連接叢集。</span><span class="sxs-lookup"><span data-stu-id="323b9-141">On the Remote Desktop blade, use the **Connect** button to connect to the cluster.</span></span> <span data-ttu-id="323b9-142">如果未啟用遠端桌面，請使用表單來提供使用者名稱和密碼，然後選取 [啟用] 來啟用叢集的遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="323b9-142">If the Remote Desktop is not enabled, use the form to provide a user name and password, then select **Enable** to enable Remote Desktop for the cluster.</span></span>

            ![遠端桌面刀鋒視窗](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="323b9-144">選取 [連線] 後，系統會下載 .rdp 檔案。</span><span class="sxs-lookup"><span data-stu-id="323b9-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="323b9-145">請使用這個檔案來啟動遠端桌面用戶端。</span><span class="sxs-lookup"><span data-stu-id="323b9-145">Use this file to launch the Remote Desktop client.</span></span> <span data-ttu-id="323b9-146">出現提示時，請使用存取遠端桌面時輸入的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="323b9-146">When prompted, use the user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="323b9-147">連接後，請從遠端桌面工作階段將下列檔案複製到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="323b9-147">Once connected, copy the following files from the Remote Desktop session to your local machine.</span></span> <span data-ttu-id="323b9-148">把它們放在名為 `hivedriver` 的本機目錄中。</span><span class="sxs-lookup"><span data-stu-id="323b9-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="323b9-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="323b9-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="323b9-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="323b9-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="323b9-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="323b9-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="323b9-152">路徑和檔案名稱中包含的版本號碼可能會與叢集不同。</span><span class="sxs-lookup"><span data-stu-id="323b9-152">The version numbers included in the paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="323b9-153">完成檔案複製後，請中斷連接遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="323b9-153">Disconnect the Remote Desktop session once you have finished copying the files.</span></span>

2. <span data-ttu-id="323b9-154">啟動 SQuirreL SQL 應用程式。</span><span class="sxs-lookup"><span data-stu-id="323b9-154">Start the SQuirreL SQL application.</span></span> <span data-ttu-id="323b9-155">從視窗左側選取 [驅動程式]。</span><span class="sxs-lookup"><span data-stu-id="323b9-155">From the left of the window, select **Drivers**.</span></span>

    ![視窗左側的 [驅動程式] 索引標籤](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="323b9-157">從 [驅動程式] 對話方塊上方的圖示，選取 [+] 圖示以建立驅動程式。</span><span class="sxs-lookup"><span data-stu-id="323b9-157">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a driver.</span></span>

    ![[驅動程式] 圖示](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="323b9-159">在 [新增驅動程式] 對話方塊中，新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="323b9-159">In the Add Driver dialog, add the following information:</span></span>

    * <span data-ttu-id="323b9-160">**名稱**：Hive</span><span class="sxs-lookup"><span data-stu-id="323b9-160">**Name**: Hive</span></span>
    * <span data-ttu-id="323b9-161">**範例 URL**：`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="323b9-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="323b9-162">**額外類別路徑**︰使用 [新增] 按鈕來新增稍早下載的 jar 檔案</span><span class="sxs-lookup"><span data-stu-id="323b9-162">**Extra Class Path**: Use the Add button to add the jar files downloaded earlier</span></span>
    * <span data-ttu-id="323b9-163">**類別名稱**：org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="323b9-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![新增驅動程式對話方塊](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="323b9-165">按一下 [確定] 儲存這些變更。</span><span class="sxs-lookup"><span data-stu-id="323b9-165">Click **OK** to save these settings.</span></span>

5. <span data-ttu-id="323b9-166">在 SQuirreL SQL 視窗的左側選取 [別名]。</span><span class="sxs-lookup"><span data-stu-id="323b9-166">On the left of the SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="323b9-167">然後按一下 [+] 圖示來建立連線別名。</span><span class="sxs-lookup"><span data-stu-id="323b9-167">Then click the **+** icon to create a connection alias.</span></span>

    ![新增別名](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="323b9-169">在 [新增別名] 對話方塊中使用下列值。</span><span class="sxs-lookup"><span data-stu-id="323b9-169">Use the following values for the **Add Alias** dialog.</span></span>

    * <span data-ttu-id="323b9-170">**名稱**：HDInsight 上的 Hive</span><span class="sxs-lookup"><span data-stu-id="323b9-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="323b9-171">**驅動程式**︰使用下拉式清單來選取 [Hive] 驅動程式</span><span class="sxs-lookup"><span data-stu-id="323b9-171">**Driver**: Use the dropdown to select the **Hive** driver</span></span>

    * <span data-ttu-id="323b9-172">**URL**： jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="323b9-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="323b9-173">將 **CLUSTERNAME** 取代為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="323b9-173">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="323b9-174">**使用者名稱**︰HDInsight 叢集的叢集登入帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="323b9-174">**User Name**: The cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="323b9-175">預設值為 `admin`。</span><span class="sxs-lookup"><span data-stu-id="323b9-175">The default is `admin`.</span></span>

    * <span data-ttu-id="323b9-176">**密碼**︰叢集登入帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="323b9-176">**Password**: The password for the cluster login account.</span></span>

 ![[新增別名] 對話方塊](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="323b9-178">使用 [測試] 按鈕來確認連接能正常運作。</span><span class="sxs-lookup"><span data-stu-id="323b9-178">Use the **Test** button to verify that the connection works.</span></span> <span data-ttu-id="323b9-179">當 [連接到︰HDInsight 上的 Hive] 對話方塊出現時，請選取 [連接] 來執行測試。</span><span class="sxs-lookup"><span data-stu-id="323b9-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span></span> <span data-ttu-id="323b9-180">如果測試成功，您會看到 [連線成功] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="323b9-180">If the test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="323b9-181">若要儲存連線別名，請使用 [新增別名] 對話方塊底部的 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="323b9-181">To save the connection alias, use the **Ok** button at the bottom of the **Add Alias** dialog.</span></span>

7. <span data-ttu-id="323b9-182">從 SQuirreL SQL 頂端的 [連接到] 下拉式清單選取 [HDInsight 上的 Hive]。</span><span class="sxs-lookup"><span data-stu-id="323b9-182">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="323b9-183">出現提示時，請選取 [連接]。</span><span class="sxs-lookup"><span data-stu-id="323b9-183">When prompted, select **Connect**.</span></span>

    ![連接對話方塊](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="323b9-185">連接後，請在 SQL 查詢對話方塊中輸入下列查詢，然後選取 [執行] 圖示。</span><span class="sxs-lookup"><span data-stu-id="323b9-185">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span></span> <span data-ttu-id="323b9-186">結果區域應該會顯示查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="323b9-186">The results area should show the results of the query.</span></span>

        select * from hivesampletable limit 10;

    ![sql 查詢對話方塊，包括結果](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="323b9-188">從範例 Java 應用程式連接</span><span class="sxs-lookup"><span data-stu-id="323b9-188">Connect from an example Java application</span></span>

<span data-ttu-id="323b9-189">如需使用 Java 用戶端查詢「HDInsight 上的 Hive」之範例，請造訪 [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc)。</span><span class="sxs-lookup"><span data-stu-id="323b9-189">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="323b9-190">遵循儲存機制中的指示建置和執行範例。</span><span class="sxs-lookup"><span data-stu-id="323b9-190">Follow the instructions in the repository to build and run the sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="323b9-191">疑難排解</span><span class="sxs-lookup"><span data-stu-id="323b9-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a><span data-ttu-id="323b9-192">嘗試開啟 SQL 連接時，發生意外的錯誤</span><span class="sxs-lookup"><span data-stu-id="323b9-192">Unexpected Error occurred attempting to open an SQL connection</span></span>

<span data-ttu-id="323b9-193">**徵狀**︰連接到 HDInsight 叢集版本 3.3 或 3.4 時，您可能會收到發生非預期錯誤的錯誤。</span><span class="sxs-lookup"><span data-stu-id="323b9-193">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="323b9-194">此錯誤的堆疊追蹤開頭為下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="323b9-194">The stack trace for this error begins with the following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="323b9-195">**原因**︰這個錯誤起因於 SQuirreL 使用的 commons-codec.jar 檔案版本與 Hive JDBC 元件要求的不相符。</span><span class="sxs-lookup"><span data-stu-id="323b9-195">**Cause**: This error is caused by a mismatch in the version of the commons-codec.jar file used by SQuirreL and the one required by the Hive JDBC components.</span></span>

<span data-ttu-id="323b9-196">**解決方案**︰若要修正此錯誤，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="323b9-196">**Resolution**: To fix this error, use the following steps:</span></span>

1. <span data-ttu-id="323b9-197">從您的 HDInsight 叢集下載 commons-codec jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="323b9-197">Download the commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="323b9-198">結束 SQuirreL，然後前往系統上安裝 SQuirreL 的目錄。</span><span class="sxs-lookup"><span data-stu-id="323b9-198">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="323b9-199">在 SquirreL 目錄的 `lib` 目錄下，使用從 HDInsight 叢集下載的版本來取代現有的 commons-codec.jar。</span><span class="sxs-lookup"><span data-stu-id="323b9-199">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span></span>

3. <span data-ttu-id="323b9-200">重新啟動 SQuirreL。</span><span class="sxs-lookup"><span data-stu-id="323b9-200">Restart SQuirreL.</span></span> <span data-ttu-id="323b9-201">連接到 HDInsight 上的 Hive 時應該不會再出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="323b9-201">The error should no longer occur when connecting to Hive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="323b9-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="323b9-202">Next steps</span></span>

<span data-ttu-id="323b9-203">現在您已學會如何搭配 Hive 使用 JDBC，接著請使用下列連結來探索 Azure HDInsight 的其他使用方式。</span><span class="sxs-lookup"><span data-stu-id="323b9-203">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="323b9-204">將資料上傳至 HDInsight</span><span class="sxs-lookup"><span data-stu-id="323b9-204">Upload data to HDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="323b9-205">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="323b9-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="323b9-206">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="323b9-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="323b9-207">搭配 HDInsight 使用 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="323b9-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
