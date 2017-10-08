---
title: "aaaInstall RStudio 使用 HDInsight 的 Azure 上的 R Server |Microsoft 文件"
description: "如何 tooinstall RStudio 與 HDInsight 上的 R 伺服器。"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>在 HDInsight 上使用 R 伺服器安裝 RStudio

本文說明如何 tooinstall hello 社群 （免費） 版本的[RStudio 伺服器](https://www.rstudio.com/products/rstudio-server/)hello 邊緣使用自訂指令碼的叢集節點上。 RStudio Server 提供瀏覽器型 IDE 供遠端用戶端使用，而且在 Linux 上廣為使用。 目前有多種適用於 R 的整合式開發環境 (IDE)，包括：

- Microsoft 的 [Visual Studio R 工具](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- Walware 的 Eclipse 型 [StatET](http://www.walware.de/goto/statet)。

hello 邊緣的 HDInsight 叢集節點上安裝 RStudio 伺服器 hello 優點是，它會提供完整的 IDE 體驗 hello 開發和執行 R 指令碼與 R 伺服器 hello 叢集上。 這項設定可以大幅提高生產力，比預設 hello R 主控台使用。

> [!NOTE]
> 只有相關，如果您未選取 tooinstall RStudio Server community edition，佈建叢集時 hello 本文中所述的程序。 如果您加入期間佈建，然後它您按一下 hello tooaccess **R Server 儀表板**磚 hello Azure 入口網站項目用於您的叢集，然後在 hello **R Studio Server**磚。 

如果您偏好的 RStudio Server toouse hello 商業授權 Pro 版本，您必須遵循 hello 安裝指示，從[RStudio 伺服器](https://www.rstudio.com/products/rstudio/download-server/)。

> [!NOTE]
> 如果您使用 HDInsight 叢集的 R 已安裝使用 hello[安裝 R 指令碼動作](hdinsight-hadoop-r-scripts-linux.md)，本文件中的 hello 步驟將無法運作正確，因為它們需要 R 伺服器 hello HDInsight 叢集上。
>
> 

## <a name="prerequisites"></a>必要條件

* 具有 R 伺服器的 Azure HDInsight 叢集已安裝。 如需相關指示，請參閱[開始在 HDInsight 叢集上使用 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。
* SSH 用戶端。 對於 Linux 和 Unix 發佈或 Macintosh OS X，hello `ssh` hello 作業系統提供命令。 對於 Windows 中，我們建議[Cygwin](http://www.redhat.com/services/custom/cygwin/)以 hello [OpenSSH 選項](https://www.youtube.com/watch?v=CwYSvvGaiWU)，或[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>使用自訂指令碼的 hello 叢集上安裝 RStudio

Hello 步驟如下：

1. 識別 hello 邊緣 hello 叢集節點。 使用 R Server HDInsight 叢集，以下是 hello 前端節點和邊緣節點的命名慣例。
   * 前端節點 `CLUSTERNAME-ssh.azurehdinsight.net`
   * 邊緣節點 `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH 到 hello 邊緣節點之 hello 叢集使用步驟 1 中所提供的 hello 命名模式。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

3. 一旦連線後，會變成 hello 叢集上的根使用者。 Hello SSH 工作階段中，使用下列命令的 hello:

        sudo su -

4. 下載 hello 自訂指令碼 tooinstall RStudio。 使用下列命令的 hello:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. 變更 hello hello 自訂指令碼檔案的權限，並執行 hello 指令碼。 使用下列命令的 hello:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. 如果您使用 SSH 密碼時使用 R 伺服器建立的 HDInsight 叢集，則可以略過此步驟，並繼續 toohello 下一步。 如果您使用 SSH 金鑰改為 toocreate hello 叢集，您必須設定密碼 SSH 使用者。 連接 tooRStudio 時，您會需要此密碼。 執行下列命令的 hello:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. 當系統提示您輸入**目前的 Kerberos 密碼**時，請按 **Enter**。  請注意，您必須將 `USERNAME` 取代為您的 HDInsight 叢集的 SSH 使用者。 如果已成功設定您的密碼，您應該會看到下列訊息的 hello:

        passwd: password updated successfully

    結束 hello SSH 工作階段。

8. 建立對應的 SSH 通道 toohello 叢集`ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`上 hello HDInsight 叢集 toohello 用戶端電腦。 您必須在開啟新的瀏覽器工作階段之前，建立 SSH 通道。

   * 在 Linux 用戶端或 Windows 用戶端與[Cygwin](http://www.redhat.com/services/custom/cygwin/)，開啟終端機工作階段，並使用下列命令的 hello:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       取代**USERNAME**與您的 HDInsight 叢集和取代的 SSH 使用者**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。
       您也可以透過新增 `-i id_rsa_key` 來使用 SSH 金鑰而非密碼。        
   * 如果使用 Windows 用戶端與 PuTTY，則

     1. 開啟 PuTTY，並輸入連線資訊。
     2. 在 hello**類別**區段 toohello 方 hello 對話方塊中，展開**連接**，依序展開**SSH**，然後選取**通道**。
     3. 提供下列資訊在 hello hello**選項控制 SSH 連接埠轉送**表單：

        * **來源連接埠**-hello 想 tooforward hello 用戶端上的連接埠。 例如， **8787**。
        * **目的地**-hello 目的地必須是對應 toohello 本機用戶端電腦。 例如，**localhost:8787**。

            ![建立 SSH 通道](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "建立 SSH 通道")

     4. 按一下**新增**tooadd hello 設定，然後按一下**開啟**tooopen SSH 連線。
     5. 出現提示時，登入 toohello 伺服器 tooestablish 的 SSH 工作階段，並啟用 hello 通道。

9. 開啟網頁瀏覽器並輸入下列 URL，根據您所輸入的 hello 通道的 hello 連接埠的 hello:

        http://localhost:8787/ 

10. 您必須提示的 tooenter hello SSH 使用者名稱和密碼 tooconnect toohello 叢集。 如果您使用 SSH 金鑰建立 hello 叢集時，您必須輸入您在步驟 5 中建立的 hello 密碼。

    ![連接導覽 Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "建立 SSH 通道")

11. tootest hello RStudio 安裝是否成功，您可以執行測試指令碼 hello 叢集執行 R MapReduce 和 Spark 作業。 在 RStudio、 toodownload hello 測試指令碼 toorun 返回 toohello SSH 主控台，並輸入下列命令的 hello:

    *    如果您建立具有 R 的 Hadoop 叢集，請使用此命令：

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    如果您已建立具有 R 的 Spark 叢集，請使用此命令：

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. 在 RStudio，您會看到 hello 測試您所下載的指令碼。 按兩下 hello 檔案 tooopen，選取 hello hello 檔案內容，然後按一下**執行**。 您應該會看見 hello 中的 hello 輸出**主控台**窗格：

   ![測試 hello 安裝](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "測試 hello 安裝")

另一個選項是 tootype`source(testhdi.r)`或`source(testhdi_spark.r)`tooexecute hello 指令碼。

## <a name="see-also"></a>另請參閱

* [適用於 HDInsight 叢集上的 R 伺服器的計算內容選項](hdinsight-hadoop-r-server-compute-contexts.md)
* [適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項](hdinsight-hadoop-r-server-storage.md)

