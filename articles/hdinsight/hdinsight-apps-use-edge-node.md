---
title: "aaaUse 空 HDInsight 的 Azure 中的 Hadoop 叢集上的邊緣節點 |Microsoft 文件"
description: "如何 tooadd 空白邊緣節點 tooan HDInsight 叢集的可用做為用戶端，然後測試/主機 HDInsight 應用程式。"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>在 HDInsight 中的 Hadoop 叢集上使用空白邊緣節點

了解如何 tooadd 空白邊緣節點 tooan HDInsight 叢集。 空白邊緣節點是在 Linux 虛擬機器具有相同的用戶端工具安裝並設定與 hello headnodes hello，但 Hadoop 服務執行。 您可以使用 hello 邊緣節點存取 hello 叢集、 測試用戶端應用程式，以及裝載用戶端應用程式。 

當您建立 hello 叢集時，您可以新增空白邊緣節點 tooan 現有 HDInsight 叢集、 tooa 新叢集。 空白邊緣節點是使用 Azure Resource Manager 範本來新增。  hello 下列範例將示範如何完成使用範本：

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Hello 範例所示，您可以選擇呼叫[指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)tooperform 額外的設定，例如安裝[Apache 色調](hdinsight-hadoop-hue-linux.md)hello 邊緣節點中。 hello 指令碼動作的指令碼必須可公開存取 hello 網站上。  例如，如果 hello 指令碼儲存在 Azure 儲存體中，使用公用容器或公用 blob。

hello 邊緣節點的虛擬機器大小必須符合 hello HDInsight 叢集背景工作節點 vm 大小需求。 Hello 建議背景工作節點的 vm 大小，請參閱[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。

建立邊緣節點之後，您可以 toohello 邊緣節點使用 SSH 的連接，並在 HDInsight 中執行用戶端工具 tooaccess hello Hadoop 叢集。

> [!WARNING] 
> 搭配 HDInsight 使用空白邊緣節點目前為預覽狀態。 Hello 邊緣節點已安裝的自訂元件會從 Microsoft 接收盡商業上合理的支援。 可能可以解決您遇到的問題。 或者，您可能需要進一步的協助參照的 toocommunity 資源。 hello 以下是 hello 的一些取得大部分的作用中網站協助 hello 社群中:
>
> * [HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com)。
>
> 如果您使用 Apache 技術，您可能無法 toofind 協助 hello 透過 Apache 專案網站上的[http://apache.org](http://apache.org)，例如 hello [Hadoop](http://hadoop.apache.org/)站台。

## <a name="add-an-edge-node-tooan-existing-cluster"></a>將邊緣節點 tooan 現有叢集新增
在本節中，您可以使用資源管理員範本 tooadd 邊緣節點 tooan 現有 HDInsight 叢集。  hello Resource Manager 範本位於[GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/)。 hello Resource Manager 範本呼叫位於 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh 指令碼動作。hello 指令碼不執行任何動作。  它是 toodemonstrate Resource Manager 範本從呼叫的指令碼動作。

**tooadd 空白邊緣節點 tooan 現有叢集**

1. 如果您還沒有 HDInsight 叢集，請予以建立。  請參閱[Hadoop 教學課程：開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)。
2. 按一下下列 tooAzure 中的映像 toosign 和開啟 hello Azure Resource Manager 範本 hello Azure 入口網站中的 hello。 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. 設定下列屬性的 hello:
   
   * **訂用帳戶**： 選取用於建立 hello 叢集的 Azure 訂用帳戶。
   * **資源群組**: hello 選取資源群組用於 hello 現有 HDInsight 叢集。
   * **位置**： 選取 hello 位置 hello 現有 HDInsight 叢集。
   * **叢集名稱**： 輸入 hello 現有 HDInsight 叢集名稱。
   * **邊緣節點大小**： 選取其中一個 hello VM 大小。 hello vm 大小必須符合 hello 背景工作節點的 vm 大小需求。 Hello 建議背景工作節點的 vm 大小，請參閱[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。
   * **邊緣節點的前置詞**: hello 預設值是**新**。  使用 hello 預設值，hello 邊緣節點名稱是**新 edgenode**。  您可以自訂 hello 從 hello 入口網站的前置詞。 您也可以自訂 hello 從 hello 範本的完整名稱。

4. 請檢查**toohello 條款和條件前面所述，即表示我同意**，然後按一下**購買**toocreate hello 邊緣節點。

>[!IMPORTANT]
> 請確定現有 HDInsight 叢集 hello tooselect hello Azure 資源群組。  否則，您會收到 hello 錯誤訊息 「 無法執行要求的作業，巢狀資源上。 找不到父資源 '&lt;叢集名稱>'」。

## <a name="add-an-edge-node-when-creating-a-cluster"></a>在建立叢集時新增邊緣節點
在本節中，您可以使用 資源管理員範本 toocreate HDInsight 叢集與邊緣節點。  hello Resource Manager 範本可以在 hello [Azure 快速入門範本組件庫](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/)。 hello Resource Manager 範本呼叫位於 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh 指令碼動作。hello 指令碼不執行任何動作。  它是 toodemonstrate Resource Manager 範本從呼叫的指令碼動作。

**tooadd 空白邊緣節點 tooan 現有叢集**

1. 如果您還沒有 HDInsight 叢集，請予以建立。  請參閱[開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)。
2. 按一下下列 tooAzure 中的映像 toosign 和開啟 hello Azure Resource Manager 範本 hello Azure 入口網站中的 hello。 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. 設定下列屬性的 hello:
   
   * **訂用帳戶**： 選取用於建立 hello 叢集的 Azure 訂用帳戶。
   * **資源群組**： 建立新的資源群組，用於 hello 叢集。
   * **位置**： 選取 hello 資源群組的位置。
   * **叢集名稱**： 輸入新叢集 toocreate hello 的名稱。
   * **叢集登入使用者名稱**： 輸入 hello Hadoop HTTP 使用者名稱。  hello 預設名稱是**admin**。
   * **叢集登入密碼**： 輸入 hello Hadoop HTTP 使用者密碼。
   * **Ssh 使用者名稱**： 輸入 hello SSH 使用者名稱。 hello 預設名稱是**sshuser**。
   * **Ssh 密碼**： 輸入 hello SSH 使用者密碼。
   * **安裝指令碼動作**： 保留 hello 預設值將在本教學課程。
     
     某些屬性已被 hello 範本中的硬式編碼： 叢集類型、 叢集背景工作節點計數、 邊緣節點大小，以及邊緣節點名稱。
4. 請檢查**toohello 條款和條件前面所述，即表示我同意**，然後按一下**購買**toocreate hello 叢集與 hello 邊緣節點。

## <a name="access-an-edge-node"></a>存取邊緣節點
hello 邊緣節點 ssh 端點是&lt;EdgeNodeName >。&lt;ClusterName >-ssh.azurehdinsight.net:22。  例如，new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22。

hello 邊緣節點會顯示為 hello Azure 入口網站上的應用程式。  hello 資訊 tooaccess hello hello 入口網站可讓邊緣使用 SSH 的節點。

**tooverify hello 邊緣節點 SSH 端點**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 與邊緣節點開啟 hello HDInsight 叢集。
3. 按一下**應用程式**從 hello 叢集刀鋒視窗。 您應該會看到 hello 邊緣節點。  hello 預設名稱是**新 edgenode**。
4. 按一下 hello 邊緣節點。 您應該會看到 hello SSH 的端點。

**toouse Hive hello 邊緣節點上**

1. 使用 SSH tooconnect toohello 邊緣節點。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 您已經連接使用 SSH toohello 邊緣節點之後，使用下列命令 tooopen hello Hive 主控台中的 hello:
   
        hive
3. 執行下列命令 tooshow hello 叢集中的 Hive 資料表的 hello:
   
        show tables;

## <a name="delete-an-edge-node"></a>刪除邊緣節點
您可以從 hello Azure 入口網站來刪除邊緣節點。

**tooaccess 邊緣節點**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 與邊緣節點開啟 hello HDInsight 叢集。
3. 按一下**應用程式**從 hello 叢集刀鋒視窗。 您應該會看到邊緣節點清單。  
4. 以滑鼠右鍵按一下 hello 邊緣節點 toodelete，然後再按一下**刪除**。
5. 按一下**是**tooconfirm。

## <a name="next-steps"></a>後續步驟
在本文中，您已經學會如何 tooadd 邊緣節點和 tooaccess hello 邊緣節點的方式。 toolearn 詳細資訊，請參閱下列文章 hello:

* [安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。
* [安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 toodeploy 未發行的 HDInsight 應用程式 tooHDInsight。
* [發行 HDInsight 應用程式](hdinsight-apps-publish-applications.md)： 了解如何 toopublish 您自訂的 HDInsight 應用程式 tooAzure Marketplace。
* [MSDN： 安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)： 了解如何 toodefine HDInsight 應用程式。
* [自訂使用指令碼動作以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)： 了解如何 toouse 指令碼動作 tooinstall 其他應用程式。
* [使用資源管理員範本 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)： 了解如何 toocall 資源管理員範本 toocreate HDInsight 叢集。

