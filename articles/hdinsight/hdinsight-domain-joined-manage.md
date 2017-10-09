---
title: "aaaManage 已加入網域的 HDInsight 叢集 Azure |Microsoft 文件"
description: "了解如何 toomanage 已加入網域的 HDInsight 叢集"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>管理已加入網域的 HDInsight 叢集 (預覽)
了解 hello 中使用者與 hello 角色加入網域的 HDInsight 及如何 toomanage 已加入網域的 HDInsight 叢集。

## <a name="users-of-domain-joined-hdinsight-clusters"></a>已加入網域的 HDInsight 叢集的使用者
是未加入網域的 HDInsight 叢集有兩個 hello 叢集建立期間建立的使用者帳戶：

* **Ambari 系統管理員**：此帳戶亦稱為「Hadoop 使用者」或「HTTP 使用者」。 此帳戶可以在 https:// tooAmbari 上的使用的 toolog&lt;clustername >。.azurehdinsight.net。 同時，也是使用的 toorun Ambari 檢視上的查詢、 執行外部工具 （也就是 PowerShell、 Templeton，Visual Studio），透過作業並 hello hive 控制檔的 ODBC 驅動程式與 BI 工具 （也就是 Excel、 power Bi 或 Tableau） 進行驗證。
* **SSH 使用者**︰此帳戶可以搭配 SSH 使用，執行 sudo 命令。 它擁有根權限 toohello Linux Vm。

已加入網域的 HDInsight 叢集在加法 tooAmbari Admin 和 SSH 使用者有三個新的使用者。

* **Ranger admin**： 此帳戶是 hello 本機 Apache Ranger 系統管理員帳戶。 不是 Active Directory 網域使用者。 此帳戶可以是使用的 toosetup 原則，並讓其他使用者的系統管理員或委派系統管理員 （如此這些使用者可以管理原則）。 根據預設，hello 使用者名稱為*管理員*和 hello 密碼是 hello 與 hello Ambari 管理密碼相同。 hello 密碼可以更新從廣 hello [設定] 頁面。
* **叢集系統管理員的網域使用者**： 此帳戶是指定為 hello 包括 Ambari 和廣的 Hadoop 叢集管理的 active directory 網域使用者。 您必須在叢集建立期間提供此使用者的認證。 此使用者擁有下列權限的 hello:

  * 加入機器 toohello 網域，並將它們放在 hello 您在叢集建立期間指定的 OU 內。
  * 建立 hello 您在叢集建立期間指定的 OU 中所有服務主體。
  * 建立反向 DNS 項目。

    請注意 hello 其他 AD 使用者也具備這些權限。

    有一些結束點 hello 叢集 (例如，Templeton) 內的未受廣，而因此並不安全。 這些端點已鎖定的所有使用者，除了 hello 叢集系統管理員的網域使用者。
* **一般**︰在叢集建立期間，您可以提供多個 Active Directory 群組。 這些群組中的 hello 使用者將無法同步處理的 tooRanger 和 Ambari。 這些使用者是網域使用者，而且必須存取 tooonly 廣受管理端點 (例如，Hiveserver2)。 所有 hello RBAC 原則和稽核將會適用 toothese 使用者。

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>已加入網域的 HDInsight 叢集的角色
已加入網域的 HDInsight 有下列角色的 hello:

* 叢集系統管理員
* 叢集操作員
* 服務管理員
* 服務操作員
* 叢集使用者

**這些角色 toosee hello 權限**

1. 開啟 hello Ambari 管理 UI。  請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。
2. 從 hello 左窗格中，按一下 **角色**。
3. 按一下 hello 藍色問號 toosee hello 權限：

    ![已加入網域的 HDInsight 角色權限](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>開啟 hello Ambari 管理 UI
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在刀鋒視窗中開啟您的 HDInsight 叢集。 請參閱[列出和顯示叢集](hdinsight-administer-use-management-portal.md#list-and-show-clusters)。
3. 按一下**儀表板**從 hello 上方功能表 tooopen Ambari。
4. 登入 tooAmbari 使用 hello 叢集系統管理員的網域使用者名稱和密碼。
5. 按一下 hello **Admin**從 hello 右上角，然後再按一下下拉式功能表**管理 Ambari**。

    ![已加入網域的 HDInsight 管理 Ambari](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    hello UI 看起來像：

    ![已加入網域的 HDInsight 的 Ambari 管理 UI](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>從您的 Active Directory 同步處理清單 hello 網域使用者
1. 開啟 hello Ambari 管理 UI。  請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。
2. 從 hello 左窗格中，按一下 **使用者**。 您應該會看到所有的 hello 使用者進行同步處理從 Active Directory toohello HDInsight 叢集。

    ![已加入網域的 HDInsight 的 Ambari 管理 UI 列出使用者](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>從您的 Active Directory 同步處理清單 hello 網域群組
1. 開啟 hello Ambari 管理 UI。  請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。
2. 從 hello 左窗格中，按一下 **群組**。 您應該會看到所有的 hello 群組進行同步處理從 Active Directory toohello HDInsight 叢集。

    ![已加入網域的 HDInsight 的 Ambari 管理 UI 列出群組](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>設定 Hive 檢視權限
1. 開啟 hello Ambari 管理 UI。  請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。
2. 從 hello 左窗格中，按一下 **檢視**。
3. 按一下**HIVE** tooshow hello 詳細資料。

    ![已加入網域的 HDInsight 的 Ambari 管理 UI Hive 檢視](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. 按一下 hello **Hive 檢視**連結 tooconfigure hive 控制檔的檢視。
5. 捲動 toohello**權限**> 一節。

    ![已加入網域的 HDInsight 的 Ambari 管理 UI Hive 檢視設定權限](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. 按一下**新增使用者**或**加入群組**，然後指定 hello 使用者或群組，可以使用 hive 控制檔的檢視。

## <a name="configure-users-for-hello-roles"></a>設定使用者的 hello 角色
 toosee 清單的角色和其權限，請參閱[角色的網域的 HDInsight 叢集](#roles-of-domain---joined-hdinsight-clusters)。

1. 開啟 hello Ambari 管理 UI。  請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。
2. 從 hello 左窗格中，按一下 **角色**。
3. 按一下**新增使用者**或**加入群組**tooassign toodifferent 角色的使用者和群組。

## <a name="next-steps"></a>後續步驟
* 如需設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。
* 如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。
* 若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。
