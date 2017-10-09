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
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>在已加入網域的 HDInsight (預覽) 中設定 Hive 原則
深入了解如何登錄區的 tooconfigure Apache Ranger 原則。 在本文中，您可以建立兩個 Ranger 原則 toorestrict 存取 toohello hivesampletable。 hello hivesampletable 隨附的 HDInsight 叢集。 您已設定 hello 原則之後，您可以使用 Excel 與 ODBC 驅動程式 tooconnect tooHive 資料表 HDInsight 中。

## <a name="prerequisites"></a>必要條件
* 已加入網域的 HDInsight 叢集。 請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。
* 安裝 Office 2016、Office 2013 Professional Plus、Office 365 Pro Plus、Excel 2013 Standalone 或 Office 2010 Professional Plus 的工作站。

## <a name="connect-tooapache-ranger-admin-ui"></a>連接 tooApache Ranger Admin UI
**tooconnect tooRanger Admin UI**

1. 從瀏覽器中，連接 tooRanger Admin UI。 hello URL 是 https://&lt;ClusterName >.azurehdinsight.net/Ranger/。

   > [!NOTE]
   > Ranger 會使用與 Hadoop 叢集不同的認證。 使用快取的 Hadoop 認證 tooprevent 瀏覽器使用新的 inprivate 瀏覽器視窗 tooconnect toohello Ranger Admin UI。
   >
   >
2. 使用登入 hello 叢集系統管理員的網域使用者名稱和密碼：

    ![HDInsight 已加入網域的 Ranger 首頁](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    目前，Ranger 僅適用於 Yarn 和 Hive。

## <a name="create-domain-users"></a>建立網域使用者
在[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)中，您已建立 hiveruser1 和 hiveuser2。 您將在本教學課程使用 hello 兩個使用者帳戶。

## <a name="create-ranger-policies"></a>建立 Ranger 原則
在這一節中，您將建立兩個 Ranger 原則以供存取 hivesampletable。 您會提供不同資料行集的選取權限。 兩個使用者都建立於[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)。  在 hello 下一步 區段中，您將測試在 Excel 中的 hello 兩個原則。

**toocreate Ranger 原則**

1. 開啟 Ranger 系統管理 UI。 請參閱[連接 tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui)。
2. 按一下 [Hive] 下的 **&lt;ClusterName>_hive**。 您會看到兩個預先設定的原則。
3. 按一下**新增原則**，然後輸入 hello 下列值：

   * 原則名稱︰read-hivesampletable-all
   * Hive 資料庫︰預設值
   * 資料表：hivesampletable
   * Hive 資料欄：*
   * 選取使用者：hiveuser1
   * 權限：選取

     ![HDInsight 已加入網域的 Ranger Hive 原則設定](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > 如果未在 選取使用者填入的網域使用者，請稍候片刻 Ranger toosync aad。
     >
     >
4. 按一下**新增**toosave hello 原則。
5. 重複 hello 最後兩個步驟 toocreate 另一個原則以 hello 下列屬性：

   * 原則名稱︰read-hivesampletable-devicemake
   * Hive 資料庫︰預設值
   * 資料表：hivesampletable
   * Hive 資料行︰clientid、devicemake
   * 選取使用者：hiveuser2
   * 權限：選取

## <a name="create-hive-odbc-data-source"></a>建立 Hive ODBC 資料來源
中可以找到 hello 指示[建立 hive 控制檔的 ODBC 資料來源](hdinsight-connect-excel-hive-odbc-driver.md)。  

    屬性|描述
    ---|---
    資料來源名稱|提供名稱 tooyour 資料來源
    Host|輸入 &lt;HDInsightClusterName>.azurehdinsight.net。 例如，myHDICluster.azurehdinsight.net
    連接埠|使用 <strong>443</strong> （此連接埠已變更從 563 too443）。
    資料庫|使用<strong>預設值</strong>
    Hive 伺服器類型|選取 [Hive Server 2]<strong></strong>
    機制|選取 [Azure HDInsight 服務]<strong></strong>
    HTTP 路徑|保留為空白。
    使用者名稱|輸入 hiveuser1@contoso158.onmicrosoft.com。如果不同，請更新 hello 網域名稱。
    密碼|輸入 hiveuser1 hello 密碼。
    </table>

請確定 tooclick**測試**之前儲存 hello 資料來源。

## <a name="import-data-into-excel-from-hdinsight"></a>從 HDInsight 將資料匯入 Excel 中
在 hello 最後一個區段中，您已設定兩個原則。  hiveuser1 hello 的 select 權限的所有 hello 資料行，而且 hiveuser2 hello 選取兩個資料行權限。 在本節中，您可以模擬 hello 兩位使用者 tooimport 資料到 Excel。

1. 在 Excel 中開啟新的或現有的活頁簿。
2. 從 hello**資料**索引標籤上，按一下 **從其他資料來源**，然後按一下**從資料連線精靈**toolaunch hello**資料連線精靈**.

    ![開啟資料連接精靈][img-hdi-simbahiveodbc.excel.dataconnection]
3. 選取**ODBC DSN**作為 hello 資料來源，然後按一下**下一步**。
4. 從 ODBC 資料來源選取 hello 資料來源在 hello 先前步驟中，您建立的名稱，然後按一下**下一步**。
5. 重新輸入 hello 叢集 hello 精靈中的 hello 密碼，然後按一下**確定**。 等候 hello**選取資料庫和資料表**對話方塊 tooopen。 這可能需要幾秒鐘的時間。
6. 選取 **hivesampletable**，然後按 [下一步]。
7. 按一下 [完成] 。
8. 在 [hello**匯入資料**] 對話方塊中，您可以變更，或指定 hello 查詢。 因此，按一下 toodo**屬性**。 這可能需要幾秒鐘的時間。
9. 按一下 hello**定義** 索引標籤 hello 命令文字：

       SELECT * FROM "HIVE"."default"."hivesampletable"

   由您定義 hello Ranger 原則，hiveuser1 具有 hello 的所有資料行的 select 權限。  所以此查詢適用於 hiveuser1 的認證，但此查詢不適用於 hiveuser2 的認證。

   ![連接屬性][img-hdi-simbahiveodbc-excel-connectionproperties]
10. 按一下**確定**tooclose hello 連接屬性 對話方塊。
11. 按一下**確定**tooclose hello**匯入資料**對話方塊。  
12. 重新輸入 hello hiveuser1，密碼，然後按一下**確定**。 花幾秒鐘，才能資料取得匯入的 tooExcel。 完成時，您會看到 11 個資料行的資料。

您在 hello 最後一節中建立 tootest hello 第二個原則 (讀取-hivesampletable-devicemake)

1. 在 Excel 中新增工作表。
2. 請遵循 hello 最後一個程序 tooimport hello 資料。  hello 唯一的變更，您將會是 toouse hiveuser2 認證，而不是 hiveuser1 的。 這將會失敗，因為 hiveuser2 只有權限 toosee 兩個資料行。 您應該會收到下列錯誤 hello:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. 後續 hello 相同程序 tooimport 資料。 此時，請使用 hiveuser2 的認證，以及修改 hello 從 select 陳述式：

        SELECT * FROM "HIVE"."default"."hivesampletable"

    至：

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    完成時，您會看到已匯入 2 個資料行的資料。

## <a name="next-steps"></a>後續步驟
* 如需設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInisight 叢集](hdinsight-domain-joined-configure.md)。
* 如需管理已加入網域的 HDInsight 叢集，請參閱[管理已加入網域的 HDInisight 叢集](hdinsight-domain-joined-manage.md)。
* 若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。
* 連接 hive 控制檔使用 Hive JDBC，請參閱[tooHive hello Hive JDBC 驅動程式使用 Azure HDInsight 上的連接](hdinsight-connect-hive-jdbc-driver.md)
* 使用 hive 控制檔的 ODBC 連接的 Excel tooHadoop，請參閱[連接 Excel tooHadoop 以 hello Microsoft Hive ODBC 磁碟機](hdinsight-connect-excel-hive-odbc-driver.md)
* 使用 Power Query 連接的 Excel tooHadoop，請參閱[使用 Power Query 連接的 Excel tooHadoop](hdinsight-connect-excel-power-query.md)
