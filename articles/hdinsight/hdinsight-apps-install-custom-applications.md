---
title: "aaaInstall Azure HDInsight 上您自己自訂的 Hadoop 應用程式 |Microsoft 文件"
description: "深入了解如何在 HDInsight 應用程式上的 tooinstall HDInsight 應用程式。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>在 Azure HDInsight 上安裝自訂 Hadoop 應用程式

在本文中，您將學習如何 tooinstall Hadoop 上的應用程式 Azure HDInsight，但尚未發行 toohello Azure 入口網站。 您將會安裝在本文中的 hello 應用程式是[色調](http://gethue.com/)。

HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。  Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。  

如需其他相關文章，請參閱：

* [安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。
* [發行 HDInsight 應用程式](hdinsight-apps-publish-applications.md)： 了解如何 toopublish 您自訂的 HDInsight 應用程式 tooAzure Marketplace。
* [MSDN： 安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)： 了解如何 toodefine HDInsight 應用程式。

## <a name="prerequisites"></a>必要條件
如果您要在現有的 HDInsight 叢集上的 tooinstall HDInsight 應用程式時，您必須擁有的 HDInsight 叢集。 toocreate 其中一個，請參閱[建立叢集](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。 您也可以在建立 HDInsight 叢集時安裝 HDInsight 應用程式。

## <a name="install-hdinsight-applications"></a>安裝 HDInsight 應用程式
HDInsight 應用程式可以安裝，當您建立叢集或 tooan 現有 HDInsight 叢集。 如需定義 Azure Resource Manager 範本，請參閱 [MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)。

所需的部署此應用程式 （色調） hello 檔案：

* [azuredeploy.json](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): hello Resource Manager 範本安裝 HDInsight 應用程式。 如需開發您自己的 Resource Manager 範本，請參閱 [MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx) 。
* [色調 install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): hello hello Resource Manager 範本設定 hello 邊緣節點所呼叫的指令碼動作。
* [色調 binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hello 色調二進位檔案從 hui install_v0.sh 呼叫。
* [色調二進位檔-14 04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hello 色調二進位檔案從 hui install_v0.sh 呼叫。
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz)：從 hui-install_v0.sh 呼叫的範例 Web 應用程式 (Tomcat)。

**tooinstall 色調 tooan 現有 HDInsight 叢集**

1. 按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    這個按鈕會開啟 hello Azure 入口網站上的資源管理員範本。  hello Resource Manager 範本位於[https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue)。  toolearn 如何 toowrite 這個資源管理員範本，請參閱[MSDN: HDInsight 應用程式安裝](https://msdn.microsoft.com/library/mt706515.aspx)。
2. 從 hello**參數**刀鋒視窗中，輸入 hello 下列：

   * **ClusterName**： 輸入 hello hello 叢集名稱上您想 tooinstall hello 應用程式。 此叢集必須是現有的叢集。
3. 按一下**確定**toosave hello 參數。
4. 從 hello**自訂部署**刀鋒視窗中，輸入**資源群組**。  hello 資源群組是群組 hello 叢集、 hello 相依的儲存體帳戶和其他資源的容器。 需要 toouse hello 與 hello 叢集相同的資源群組。
5. 按一下 法律條款，然後按一下建立。
6. 確認 hello **Pin toodashboard**核取方塊已選取，然後按一下**建立**。 您可以看到 hello 與 hello 磚已釘選的 toohello 入口網站儀表板 hello 入口網站的通知 （按一下 hello hello 頂端 hello 入口網站上的鈴鐺圖示） 的安裝狀態。  花費大約 10 分鐘 tooinstall hello 應用程式。

**tooinstall 色調時建立叢集**

1. 按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    這個按鈕會開啟 hello Azure 入口網站上的資源管理員範本。  hello Resource Manager 範本位於[https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json)。  toolearn 如何 toowrite 這個資源管理員範本，請參閱[MSDN: HDInsight 應用程式安裝](https://msdn.microsoft.com/library/mt706515.aspx)。
2. 遵循 hello 指令 toocreate 叢集並安裝色調。 如需建立 HDInsight 叢集的詳細資訊，請參閱 [在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

此外 toohello Azure 入口網站，您也可以使用[Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell)和[Azure CLI](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall 資源管理員範本。

## <a name="validate-hello-installation"></a>驗證 hello 安裝
您可以檢查 hello hello Azure 入口網站 toovalidate hello 應用程式安裝的應用程式狀態。 此外，您也可以驗證所有的 HTTP 端點找出如預期般與 hello 網頁如果有一個：

**tooopen hello 色調入口網站**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**HDInsight 叢集**hello 左功能表中。  如果沒有看到該功能表，請按一下 瀏覽，然後按一下HDInsight 叢集。
3. 按一下 hello 叢集 hello 應用程式的安裝位置。
4. 從 hello**設定**刀鋒視窗中，按一下 **應用程式**下 hello**一般**類別目錄。 您應該會看到**色調**列在 hello**安裝應用程式**刀鋒視窗。
5. 按一下**色調**從 hello 清單 toolist hello 屬性。  
6. 按一下 hello 網頁連結 toovalidate hello 網站。開啟瀏覽器 toovalidate hello 色調 web UI 中，開啟 hello SSH 的端點使用 SSH hello HTTP 端點。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a name="troubleshoot-hello-installation"></a>Hello 安裝問題疑難排解
您可以檢查 hello 入口網站通知 hello 應用程式安裝狀態 （按一下 hello hello 頂端 hello 入口網站上的鈴鐺圖示）。

如果某個應用程式安裝失敗，您可以看到 hello 錯誤訊息，而偵錯資訊從 3 的地方：

* HDInsight 應用程式︰一般錯誤資訊。

    開啟 hello 叢集從 hello 入口網站，並按一下 [從 hello 設定] 刀鋒視窗的應用程式：

    ![hdinsight 應用程式的應用程式安裝錯誤](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* 編寫動作的 HDInsight: hello 指令碼動作 窗格中若 hello HDInsight 應用程式的錯誤訊息表示指令碼動作失敗，會顯示 hello 指令碼失敗詳細資訊。

    從 hello 設定 刀鋒視窗中按一下指令碼動作。 指令碼動作記錄會顯示 hello 的錯誤訊息

    ![hdinsight 應用程式的指令碼動作錯誤](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web UI: Hello 安裝指令碼已 hello hello 失敗原因，如果使用 Ambari Web UI hello 安裝指令碼的相關 toocheck 完整記錄。

    如需詳細資訊，請參閱 [疑難排解](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)。

## <a name="remove-hdinsight-applications"></a>移除 HDInsight 應用程式
有數種方式 toodelete HDInsight 應用程式。

### <a name="use-portal"></a>使用入口網站
**tooremove 使用 hello 入口網站應用程式**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**HDInsight 叢集**hello 左功能表中。  如果沒有看到該功能表，請按一下 瀏覽，然後按一下HDInsight 叢集。
3. 按一下 hello 叢集 hello 應用程式的安裝位置。
4. 從 hello**設定**刀鋒視窗中，按一下 **應用程式**下 hello**一般**類別目錄。 您應該會看到已安裝的應用程式清單。 本教學課程，**色調**列在 hello**安裝應用程式**刀鋒視窗。
5. 以滑鼠右鍵按一下您想 tooremove，，然後按一下 「 hello 」 應用程式**刪除**。
6. 按一下**是**tooconfirm。

從 hello 入口網站，您也可以刪除 hello 叢集，或刪除 hello 資源群組，其中包含 hello 應用程式。

### <a name="use-azure-powershell"></a>使用 Azure PowerShell
您可以使用 Azure PowerShell，刪除 hello 叢集或刪除 hello 資源群組。 請參閱 [使用 Azure PowerShell 刪除叢集](hdinsight-administer-use-powershell.md#delete-clusters)。

### <a name="use-azure-cli"></a>使用 Azure CLI
您可以使用 Azure CLI，刪除 hello 叢集或刪除 hello 資源群組。 請參閱 [使用 Azure CLI 刪除叢集](hdinsight-administer-use-command-line.md#delete-clusters)。

## <a name="next-steps"></a>後續步驟
* [MSDN： 安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)： 了解如何 toodevelop 資源管理員範本部署 HDInsight 應用程式。
* [安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。
* [發行 HDInsight 應用程式](hdinsight-apps-publish-applications.md)： 了解如何 toopublish 您自訂的 HDInsight 應用程式 tooAzure Marketplace。
* [自訂使用指令碼動作以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)： 了解如何 toouse 指令碼動作 tooinstall 其他應用程式。
* [使用資源管理員範本 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)： 了解如何 toocall 資源管理員範本 toocreate HDInsight 叢集。
* [使用 HDInsight 中的空白邊緣節點](hdinsight-apps-use-edge-node.md)： 了解如何 toouse 空白邊緣節點存取 HDInsight 叢集、 測試 HDInsight 應用程式，以及裝載 HDInsight 應用程式。
