---
title: "使用 Azure CLI-Azure HDInsight aaaManage Hadoop 叢集 |Microsoft 文件"
description: "了解在 Azure HDInsight toouse hello Azure 命令列介面 toomanage Hadoop 叢集的方式。 hello Azure CLI 適用於 Windows、 Mac 和 Linux。"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>管理中使用 Azure CLI hello HDInsight Hadoop 叢集
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

深入了解如何 toouse hello [Azure 命令列介面](../cli-install-nodejs.md)toomanage Hadoop Azure HDInsight 叢集。 Node.js 被實作 hello Azure CLI。 此工具可在任何支援 Node.js 的平台上使用，包括 Windows、Mac 和 Linux。

本文涵蓋只使用 HDInsight 中的 hello Azure CLI。 有關的一般指南 toouse Azure CLI，請參閱[安裝及設定 Azure CLI][azure-command-line-tools]。

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* **Azure CLI** -請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)如需安裝和組態資訊。
* **連接 tooAzure**，並使用下列命令 hello:
  
        azure login
  
    如需有關如何使用工作或學校帳戶驗證的詳細資訊，請參閱[tooan Azure 訂用帳戶連線從 hello Azure CLI](../xplat-cli-connect.md)。
* **交換器 toohello Azure Resource Manager 模式**，並使用下列命令 hello:
  
        azure config mode arm

tooget 的說明，請使用 hello **-h**切換。  例如：

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>以 hello CLI 建立叢集
請參閱[中使用 HDInsight 建立叢集 hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md)。

## <a name="list-and-show-cluster-details"></a>列出和顯示叢集詳細資料
使用下列命令 toolist hello，並顯示叢集詳細資料：

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![叢集清單的命令列檢視][image-cli-clusterlisting]

## <a name="delete-clusters"></a>刪除叢集
使用下列命令 toodelete 叢集中的 hello:

    azure hdinsight cluster delete <Cluster Name>

您也可以藉由刪除 hello 資源群組含有 hello 叢集刪除叢集。 請注意，這將刪除 hello 群組包括 hello 預設儲存體帳戶中的所有 hello 資源。

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>調整叢集
toochange hello Hadoop 叢集大小：

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>啟用/停用叢集 HTTP 存取
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>啟用/停用叢集 RDP 存取
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>後續步驟
在本文中，您已經學會如何 tooperform 不同 HDInsight 叢集系統管理工作。 toolearn 詳細資訊，請參閱下列文章 hello:

* [使用 hello Azure 入口網站來管理 HDInsight][hdinsight-admin-portal]
* [使用 Azure PowerShell 管理 HDInsight][hdinsight-admin-powershell]
* [開始使用 Azure HDInsight][hdinsight-get-started]
* [如何 toouse hello Azure CLI][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "列出和顯示叢集"
