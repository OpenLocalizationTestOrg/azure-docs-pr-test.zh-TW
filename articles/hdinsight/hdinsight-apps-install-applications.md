---
title: "Azure HDInsight 上的 aaaInstall 第三方 Hadoop 應用程式 |Microsoft 文件"
description: "深入了解如何在 Azure HDInsight 上的 tooinstall 第三方 Hadoop 應用程式。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>在 Azure HDInsight 上安裝協力廠商 Hadoop 應用程式

在本文中，您將學習如何 tooinstall Azure HDInsight 上的已發佈協力廠商 Hadoop 應用程式。 如需您自己的應用程式的安裝指示，請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)。

HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。 Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。  

目前有四個已發佈的應用程式：

* **HDInsight 上 DATAIKU DDS**: Dataiku DSS (資料科學 Studio) 是可讓資料的軟體 （資料科學家、 商務分析師、 開發人員...） 的專業人員 tooprototype 建置及部署非常特定的服務，可將轉換成原始資料影響商務預測。
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft)提供分析師的互動式方式 toodiscover，分析和視覺化 hello 巨量資料的結果。 提取額外的資料來源中輕鬆地 toodiscover 新的關聯性和您需要快速解答 hello。
* **資料收集器 Streamsets HDnsight**提供功能完整的整合式的開發環境 (IDE) 可讓您設計、 測試、 部署和管理任何-任何內嵌資料流和批次資料的 mesh 的管線，並包含各種不同的資料流中的轉換，而不需擁有 toowrite 自訂程式碼。 
* **Cask hdinsight CDAP**提供 hello 先統一縮減資料的應用程式和資料湖 hello 時間 tooproduction 80%的巨量資料的整合平台。 此應用程式僅支援 Standard HBase 3.4 叢集。
* **HDInsight (Beta) 的 H2O 人工地智慧**H2O Sparkling 上限支援下列分散式的演算法 hello: GLM、 貝氏機率分類、 分散式隨機樹系、 漸層來提升電腦，深度類神經網路、 深入了解 k-means PCA，低等級的模型、 異常偵測和 Autoencoders 一般化。
* **Kyligence Analytics Platform**：Kyligence Analytics Platform (KAP) 是由 Apache Kylin 和 Apache Hadoop 提供之符合企業需求的資料倉儲，對大規模資料集的查詢延遲不到一秒，而且可簡化企業用戶和分析師的資料分析作業。 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex HDInsight 上執行可讓客戶更快的 tooget toobusiness insights 藉由提供自助式資料擷取和從幾乎任何來源 toohello Microsoft Azure 雲端的準備平台。
* **Spark KNIME Spark 執行程式的作業伺服器**KNIME Spark 執行程式的 Spark 作業伺服器是使用的 tooconnect hello KNIME 分析平台 tooHDInsight 叢集。

在本文中所提供的 hello 指示使用 Azure 入口網站。 您也可以匯出 hello Azure Resource Manager 範本從 hello 入口網站或廠商，取得一份 hello Resource Manager 範本和使用 Azure PowerShell 和 Azure CLI toodeploy hello 範本。  請參閱 [使用 Resource Manager 範本在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。

## <a name="prerequisites"></a>必要條件
如果您要在現有的 HDInsight 叢集上的 tooinstall HDInsight 應用程式時，您必須擁有的 HDInsight 叢集。 toocreate 其中一個，請參閱[建立叢集](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。 您也可以在建立 HDInsight 叢集時安裝 HDInsight 應用程式。

## <a name="install-applications-tooexisting-clusters"></a>安裝應用程式 tooexisting 叢集
hello 下列程序為您示範如何 tooinstall HDInsight 應用程式 tooan 現有 HDInsight 叢集。

**tooinstall HDInsight 應用程式**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**HDInsight 叢集**hello 左功能表中。  如果沒看到該功能表，請按一下 更多服務，然後按一下HDInsight 叢集。
3. 按一下 HDInsight 叢集。  如果您沒有叢集，則必須先建立一個。  請參閱 [建立叢集](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。
4. 按一下**應用程式**下 hello**組態**類別目錄。 您可以會看到已安裝的應用程式清單。 如果找不到應用程式，這表示沒有 hello HDInsight 叢集的此版本的應用程式。
   
    ![HDInsight 應用程式入口網站功能表](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. 按一下**新增**hello 刀鋒視窗功能表。 
   
    ![HDinsight 應用程式安裝的應用程式](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    您可以看到現有 HDInsight 應用程式的清單。
   
    ![HDinsight 應用程式可用的應用程式](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. 按一下其中一個 hello 應用程式，接受 hello 法律條款，然後按**選取**。

您可以看到從 hello 入口網站通知 hello 安裝狀態 （按一下 hello hello 頂端 hello 入口網站上的鈴鐺圖示）。 Hello 應用程式安裝後，hello 應用程式會出現在 hello 安裝應用程式 刀鋒視窗。

## <a name="install-applications-during-cluster-creation"></a>在叢集建立期間安裝應用程式
當您建立叢集時，您會有 hello 選項 tooinstall HDInsight 應用程式。 在 hello 過程中，HDInsight 應用程式會安裝 hello 叢集已建立並處於執行中狀態的 hello 之後。 hello 下列程序為您示範如何 tooinstall HDInsight 應用程式時建立叢集。

**tooinstall HDInsight 應用程式**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 依序按一下 [新增]、[資料 + 分析] 及 [HDInsight]。
3. 輸入 **叢集名稱**：此名稱必須是全域唯一的。
4. 按一下**訂用帳戶**tooselect hello 用於 hello 叢集的 Azure 訂用帳戶。
5. 按一下 [選取叢集類型] ，然後選取︰
   
   * **叢集類型**： 如果您不知道哪些 toochoose，選取**Hadoop**。 它是 hello 最受歡迎的叢集類型。
   * **作業系統**：選取 [Linux]。
   * **版本**： 如果您不知道哪些 toochoose 使用 hello 預設版本。 如需詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。
   * **叢集層**: Azure HDInsight 提供 hello 巨量資料雲端供應項目兩種類型： 標準層和 Premium 層。 如需詳細資訊，請參閱 [叢集層](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)。
6. 按一下**應用程式**，按一下其中一個 hello 發行的應用程式，然後按一下**選取**。
7. 按一下**認證**，然後輸入 hello 系統管理使用者的密碼。 您也需要 tooenter **SSH 使用者名稱**和**密碼**或**公開金鑰**，這是使用的 tooauthenticate hello SSH 使用者。 使用公開金鑰為 hello 建議的方法。 按一下**選取**在 hello 底部 toosave hello 認證組態。
8. 按一下**資料來源**，選取其中一個現有的儲存體帳戶的 hello 或建立新的儲存體帳戶 toobe 作為 hello 叢集 hello 預設儲存體帳戶。
9. 按一下**資源群組**tooselect 現有的資源群組，或按一下**新增**toocreate 新的資源群組
10. 在 hello**新的 HDInsight 叢集**刀鋒視窗中，確定**Pin tooStartboard**已選取，然後按一下**建立**。 

## <a name="list-installed-hdinsight-apps-and-properties"></a>列出已安裝的 HDInsight 應用程式和屬性
hello 入口網站會顯示一份 hello 安裝 HDInsight 叢集，以及每個已安裝應用程式的 hello 屬性的應用程式。

**toolist HDInsight 應用程式] 和 [顯示屬性**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**HDInsight 叢集**hello 左功能表中。  如果沒有看到該功能表，請按一下 瀏覽，然後按一下HDInsight 叢集。
3. 按一下 HDInsight 叢集。
4. 從 hello**設定**刀鋒視窗中，按一下 **應用程式**下 hello**一般**類別目錄。 hello 安裝應用程式 刀鋒視窗會列出所有安裝的 hello 應用程式。 
   
    ![HDinsight 應用程式安裝的應用程式](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. 按一下其中一個 hello 安裝應用程式 tooshow hello 屬性。 hello 屬性刀鋒視窗會列出：
   
   * 應用程式名稱：應用程式名稱。
   * 狀態︰應用程式狀態。 
   * 網頁： hello hello web 應用程式，您已部署 toohello 邊緣節點的 URL。 hello 認證是的 hello 相同 hello HTTP 使用者認證，您已設定為 hello 叢集。
   * HTTP 端點： hello 認證為的 hello 相同 hello HTTP 使用者認證，您已設定為 hello 叢集。 
   * SSH 的端點： 您可以使用 SSH tooconnect toohello 邊緣節點。 hello 相同 hello SSH 使用者認證，您已設定為 hello 叢集所 hello 的 SSH 認證。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。
6. 應用程式，toodelete hello 應用程式，以滑鼠右鍵按一下，然後按一下**刪除**hello 操作功能表中。

## <a name="connect-toohello-edge-node"></a>Toohello 邊緣節點連接
您可以在使用 HTTP 和 SSH toohello 邊緣節點中建立連接。 hello 端點資訊可以找到 hello[入口網站](#list-installed-hdinsight-apps-and-properties)。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

hello HTTP 端點認證是 hello HTTP 使用者認證，您所設定的 hello HDInsight 叢集。hello SSH 端點認證是您所設定的 hello HDInsight 叢集的 hello SSH 認證。

## <a name="troubleshoot"></a>疑難排解
請參閱[hello 安裝問題疑難排解](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation)。

## <a name="next-steps"></a>後續步驟
* [安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 toodeploy 未發行的 HDInsight 應用程式 tooHDInsight。
* [發行 HDInsight 應用程式](hdinsight-apps-publish-applications.md)： 了解如何 toopublish 您自訂的 HDInsight 應用程式 tooAzure Marketplace。
* [MSDN： 安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)： 了解如何 toodefine HDInsight 應用程式。
* [自訂使用指令碼動作以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)： 了解如何 toouse 指令碼動作 tooinstall 其他應用程式。
* [使用資源管理員範本 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)： 了解如何 toocall 資源管理員範本 toocreate HDInsight 叢集。
* [使用 HDInsight 中的空白邊緣節點](hdinsight-apps-use-edge-node.md)： 了解如何 toouse 空白邊緣節點存取 HDInsight 叢集、 測試 HDInsight 應用程式，以及裝載 HDInsight 應用程式。

