---
title: "aaaUse SSH 通道 tooaccess Azure HDInsight |Microsoft 文件"
description: "了解如何 toouse SSH 通道 toosecurely 瀏覽以 Linux 為基礎的 HDInsight 節點上裝載的 web 資源。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>使用 SSH 通道 tooaccess Ambari web UI、 JobHistory、 NameNode、 Oozie 和其他 web Ui

以 Linux 為基礎的 HDInsight 叢集提供透過 hello 網際網路存取 tooAmbari web UI，但 hello UI 的某些功能。 例如，hello web UI Ambari 透過其他服務。 如需完整的 hello Ambari web UI 的功能，您必須使用 SSH 通道 toohello 叢集標頭。

## <a name="why-use-an-ssh-tunnel"></a>為何要使用 SSH 通道

有幾個 Ambari hello 功能表只可透過 SSH 通道。 這些功能表依賴其他節點類型上執行的網站和服務，例如背景工作節點。 通常，這些網站並未受到保護，因此並不安全的 toodirectly 公開它們在 hello 網際網路。

下列 Web Ui 的 hello 需要 SSH 通道：

* JobHistory
* NameNode
* 執行緒堆疊
* Oozie Web UI
* HBase Master 和記錄 UI

如果您使用指令碼動作 toocustomize 您的叢集時，任何服務或公用程式安裝會公開 web UI 要求的 SSH 通道。 例如，如果您安裝使用指令碼動作色調，您必須使用 SSH 通道 tooaccess hello 色調 web UI。

> [!IMPORTANT]
> 如果您有直接存取 tooHDInsight 透過虛擬網路，您不需要 toouse SSH 通道。 如需直接存取 HDInsight 透過虛擬網路的範例，請參閱 hello[連接 HDInsight tooyour 在內部部署網路](connect-on-premises-network.md)文件。

## <a name="what-is-an-ssh-tunnel"></a>什麼是 SSH 通道

[安全殼層 (SSH) 通道](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling)tooa 連接埠傳送您的本機工作站上的流量路由傳送。 hello 流量路由傳送透過 SSH 連線 tooyour HDInsight 叢集前端節點。 hello 要求會解析，如同原始程式碼 hello 前端節點上。 hello 回應 hello 通道 tooyour 工作站透過回傳然後路由傳送。

## <a name="prerequisites"></a>必要條件

* SSH 用戶端。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

* 可以是網頁瀏覽器設定 toouse SOCKS5 proxy。

    > [!WARNING]
    > hello SOCKS proxy 支援內建於 Windows 不支援 SOCKS5，而且不適用於這份文件中的 hello 步驟。 hello 下列瀏覽器依賴 Windows proxy 設定，並目前並不是使用這份文件中的 hello 步驟：
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome 也依賴 Windows hello 的 proxy 設定。 不過，您可以安裝支援 SOCKS5 的延伸模組。 我們建議使用 [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp)。

## <a name="usessh"></a>建立使用 hello SSH 命令通道

使用 hello 下列命令 toocreate SSH 通道使用 hello`ssh`命令。 取代**USERNAME**與您的 HDInsight 叢集和取代的 SSH 使用者**CLUSTERNAME** hello 您的 HDInsight 叢集名稱：

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

此命令會建立路由流量 toolocal 連接埠 9876 toohello 叢集透過 SSH 的連接。 hello 選項如下：

* **D 9876** -hello 路由傳送流量透過 hello 通道的本機連接埠。
* **C** - 壓縮所有資料，因為網路流量大多是文字。
* **2** -force SSH tootry 通訊協定版本 2 只。
* **q** - 無訊息模式。
* **T** - 停用虛擬 tty 配置，因為我們只是轉送連接埠。
* **n** - 防止讀取 STDIN，因為我們只是轉送連接埠。
* **N** - 不執行遠端命令，因為我們只是轉送連接埠。
* **f** -hello 背景中執行。

一旦 hello 命令完成時，傳送的流量 tooport 9876 hello 本機電腦上就是路由的 toohello 叢集前端節點。

## <a name="useputty"></a>使用 PuTTY 建立通道

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) 是適用於 Windows 的圖形化 SSH 用戶端。 使用下列步驟 toocreate SSH 通道使用 PuTTY hello:

1. 開啟 PuTTY，並輸入連線資訊。 如果您不熟悉 PuTTY，請參閱 hello [PuTTY 文件 (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)。

2. 在 hello**類別**區段 toohello 方 hello 對話方塊中，展開**連接**，依序展開**SSH**，然後選取**通道**。

3. 提供下列資訊在 hello hello**選項控制 SSH 連接埠轉送**表單：
   
   * **來源連接埠**-hello 想 tooforward hello 用戶端上的連接埠。 例如， **9876**。

   * **目的地**-hello hello 以 Linux 為基礎的 HDInsight 叢集的 SSH 位址。 例如， **mycluster-ssh.azurehdinsight.net**。

   * **動態** - 啟用動態 SOCKS Proxy 路由。
     
     ![通道處理選項的影像](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. 按一下**新增**tooadd hello 設定，然後按一下**開啟**tooopen SSH 連線。

5. 出現提示時，登入 toohello 伺服器。

## <a name="use-hello-tunnel-from-your-browser"></a>使用從您的瀏覽器的 hello 通道

> [!IMPORTANT]
> hello 依這個區段使用 hello Mozilla FireFox 瀏覽器中，因為它在所有平台之間提供 hello 相同的 proxy 設定。 其他的新式瀏覽器，例如 Google Chrome，可能需要等 FoxyProxy toowork hello 通道與擴充功能。

1. 設定 hello 瀏覽器 toouse **localhost**和 hello 時使用的連接埠建立 hello 通道為**SOCKS v5** proxy。 Hello Firefox 設定看起來如下。 如果您使用不同的通訊埠，比 9876，變更您所使用的 hello 連接埠 toohello:
   
    ![Firefox 設定的影像](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > 選取**遠端 DNS**解析網域名稱系統 (DNS) 要求使用 hello HDInsight 叢集。 這項設定會解析 DNS 使用 hello hello 叢集前端節點。

2. 請確認該 hello 通道的運作方式是瀏覽網站時，例如[http://www.whatismyip.com/](http://www.whatismyip.com/)。 hello IP 傳回其中一個應由 hello Microsoft Azure 資料中心。

## <a name="verify-with-ambari-web-ui"></a>驗證 Ambari Web UI

一旦建立 hello 叢集中，使用下列步驟，您可以從 hello Ambari Web 存取服務 web Ui 的 tooverify hello:

1. 在您的瀏覽器，移 toohttp://headnodehost:8080。 hello`headnodehost`位址是透過傳送 hello 通道 toohello 叢集，然後解決 toohello 叢集前端節點上執行 Ambari。 出現提示時，輸入 hello 系統管理員使用者名稱 （管理員） 和密碼為您的叢集。 您可能會提示輸入第二次 hello Ambari web UI。 若是如此，重新輸入 hello 資訊。

   > [!NOTE]
   > 當使用 hello http://headnodehost:8080 位址 tooconnect toohello 叢集，您透過 hello 通道進行連線。 使用 hello SSH 通道，而非 HTTPS 來保護通訊。 tooconnect 超過 hello 網際網路使用 HTTPS，請使用 https://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME**是 hello hello 叢集名稱。

2. 從 hello Ambari Web UI，請從左側的 hello 頁面 hello hello 清單中選取 HDFS。

    ![選取 HDFS 的影像](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. 顯示 hello HDFS 服務資訊時，選取**快速連結**。 Hello 叢集前端節點的清單隨即出現。 選取其中一個 hello 前端節點，然後再選取**NameNode UI**。

    ![展開 hello QuickLinks 功能表的映像](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > 當您選取 [快速連結] 時，可能會出現等候指示器。 如果您的網際網路連線速度較慢，可能會發生這種情況。 等候一分鐘或收到 hello 伺服器 hello 資料 toobe 的兩個，然後再試一次 hello 清單。
   >
   > 某些項目在 hello**快速連結**功能表可能會切掉 hello hello 螢幕右側的。 如果是這樣，依序展開 [hello] 功能表，使用滑鼠，並使用 hello 向右箭號鍵 tooscroll hello 螢幕 toohello 右 toosee hello 的其餘部分 hello 功能表。

4. 會顯示下列影像頁面類似 toohello:

    ![Hello NameNode UI 的映像](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > 請注意此頁面中; hello URL它應該類似太**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/叢集**。 此 URI 使用 hello 內部完整的網域名稱 (FQDN) 的 hello 節點，而且僅可存取時使用的 SSH 通道。

## <a name="next-steps"></a>後續步驟

既然您已經學會如何 toocreate 及使用 SSH 通道，請參閱下列文件的其他方式 toouse Ambari hello:

* [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)

如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

