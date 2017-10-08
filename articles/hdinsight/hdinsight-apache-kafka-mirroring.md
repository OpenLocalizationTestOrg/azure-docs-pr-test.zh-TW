---
title: "aaaMirror Apache Kafka 主題 Azure HDInsight |Microsoft 文件"
description: "深入了解 toouse Apache Kafka 的鏡像功能鏡像主題 tooa 次要叢集 toomaintain Kafka HDInsight 叢集上的複本。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>使用 HDInsight （預覽） 上的 Kafka MirrorMaker tooreplicate Apache Kafka 主題

了解如何 toouse Apache Kafka 的鏡像功能 tooreplicate 主題 tooa 次要叢集。 鏡像可執行做為連續的處理序或間歇性使用，做為移轉的方法資料從某個叢集 tooanother。

在此範例中，鏡像是兩個的 HDInsight 叢集之間使用的 tooreplicate 主題。 這兩個叢集會在 hello Azure 虛擬網路中相同的區域。

> [!WARNING]
> 鏡像應該不會被視為與表示 tooachieve 容錯。 hello 主題內的位移的 tooitems 之間的有所差異 hello 來源和目的地叢集，因此用戶端無法使用兩個 hello 交換使用。
>
> 如果您擔心容錯功能，您應該在您的叢集內設定 hello 主題的複寫。 如需詳細資訊，請參閱[開始使用 Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)。

## <a name="how-kafka-mirroring-works"></a>Kafka 鏡像的運作方式

鏡像的運作方式是使用 hello MirrorMaker 工具 （Apache Kafka 的一部分） tooconsume hello 來源叢集上的主題中的記錄，然後再建立 hello 目的地叢集上的 本機複本。 MirrorMaker 使用其中一個 （或以上）*取用者*hello 來源叢集上，從讀取和*生產者*寫入 toohello 本機 （目的地） 叢集。

hello 下列圖表說明 hello 鏡像處理序：

![Hello 鏡像處理序的圖表](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Apache Kafka HDInsight 上不提供存取 toohello Kafka 服務 hello 透過公用網際網路。 Kafka 產生者或取用者必須在 hello 與 hello hello Kafka 叢集節點的相同 Azure 虛擬網路。 針對此範例中，hello Kafka 來源與目的地叢集位於 Azure 的虛擬網路中。 hello 下圖顯示 hello 叢集之間通訊流動的方式：

![Azure 虛擬網路中的來源和目的地 Kafka 叢集圖表](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

hello 來源和目的地叢集可以在 hello 節點與資料分割的不同，而且 hello 主題內的位移也會不同。 鏡像會維護 hello 金鑰值以用於資料分割，因此會保留每個索引鍵為基礎的記錄順序。

### <a name="mirroring-across-network-boundaries"></a>跨網路界限鏡像

如果您需要 toomirror Kafka 不同的網路中的叢集之間，有下列其他考量 hello:

* **閘道**: hello 網路必須能夠 toocommunicate 在 hello TCPIP 層級。

* **名稱解析**: hello Kafka 叢集在每個網路必須能夠 tooconnect tooeach 其他使用主機名稱。 這可能需要為每個網路中的網域名稱系統 (DNS) 伺服器設定 tooforward 要求 toohello 其他網路。

    建立 Azure 虛擬網路，而不是使用 DNS 自動提供的 hello 與 hello 網路時，您必須指定自訂 DNS 伺服器和 hello 伺服器 IP 位址 hello。 Hello 已建立虛擬網路之後, 您就必須建立 Azure 虛擬機器使用該 IP 位址，然後安裝並在其上設定 DNS 軟體。

    > [!WARNING]
    > 建立並設定自訂 DNS 伺服器 hello 再安裝 HDInsight 到 hello 虛擬網路。 沒有 HDInsight toouse hello DNS 伺服器設定為 hello 虛擬網路所需的其他設定。

如需有關如何連接兩個 Azure 虛擬網路的詳細資訊，請參閱[設定 VNet 對 VNet 連線](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)。

## <a name="create-kafka-clusters"></a>建立 Kafka 叢集

雖然您可以建立 Azure 虛擬網路和 Kafka 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。 Azure 虛擬網路和兩個 Kafka 叢集 tooyour Azure 訂用帳戶，請使用下列步驟 toodeploy hello。

1. 使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**。

    > [!WARNING]
    > HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。 此範本會建立包含三個背景工作角色節點的 Kafka 叢集。

2. 使用下列資訊 toopopulate hello 項目上 hello 的 hello**自訂部署**刀鋒視窗中：
    
    ![HDInsight 自訂部署](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **資源群組**：建立群組或選取現有的群組。 此群組包含 hello HDInsight 叢集。

    * **位置**： 選取位置的地理位置關閉 tooyou。
     
    * **基底叢集名稱**: hello Kafka 叢集 hello 基底名稱為使用此值。 例如，輸入 **hdi** 可建立名為 **source-hdi** 和 **dest-hdi** 的叢集。

    * **叢集登入使用者名稱**: hello 系統管理員使用者名稱 hello 來源與目的 Kafka 叢集。

    * **叢集登入密碼**: hello 來源與目的 hello 管理使用者的密碼 Kafka 叢集。

    * **SSH 使用者名稱**: hello SSH 使用者 toocreate hello 來源與目的 Kafka 叢集。

    * **SSH 密碼**: hello hello hello 來源和目的地的 SSH 使用者密碼 Kafka 叢集。

3. 讀取 hello**條款和條件**，然後選取**toohello 條款和條件前面所述，即表示我同意**。

4. 最後，檢查**Pin toodashboard** ，然後選取 **購買**。 它會採用約 20 分鐘 toocreate hello 叢集。

一旦已建立 hello 資源，您已重新導向的 tooa 刀鋒視窗中的 hello 資源群組含有 hello 叢集和 web 儀表板。

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> 請注意，hello hello HDInsight 叢集名稱**來源 BASENAME**和**目的地 BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。 連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。

## <a name="create-topics"></a>建立主題

1. 連接 toohello**來源**叢集使用 SSH:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    取代**sshuser** hello 建立 hello 叢集時所使用的 SSH 使用者名稱。 取代**BASENAME** hello 建立 hello 叢集時所使用的基底名稱。

    如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用 hello 下列命令 toofind hello 動物園管理員主機 hello 來源叢集：

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. 已建立下列 hello 主題的命令 tooverify 使用 hello:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    hello 回應包含`testtopic`。

4. 遵循這個 tooview hello 動物園管理員主機資訊的使用 hello (hello**來源**) 叢集：

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    這會傳回資訊的類似 toohello 下列文字：

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    請儲存此資訊。 它用於 hello 下一節。

## <a name="configure-mirroring"></a>設定鏡像功能

1. 連接 toohello**目的地**叢集使用不同的 SSH 工作階段：

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    取代**sshuser** hello 建立 hello 叢集時所使用的 SSH 使用者名稱。 取代**BASENAME** hello 建立 hello 叢集時所使用的基底名稱。

    如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用 hello 下列命令 toocreate`consumer.properties`檔案，其中描述如何以 hello toocommunicate**來源**叢集：

    ```bash
    nano consumer.properties
    ```

    使用 hello 文字之後做為 hello 內容的 hello`consumer.properties`檔案：

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    取代**SOURCE_ZKHOSTS**以 hello 動物園管理員裝載資訊從 hello**來源**叢集。

    讀取 hello 來源 Kafka 叢集時，此檔案會描述 hello 取用者資訊 toouse。 如需取用者組態詳細資訊，請參閱 kafka.apache.org 上的[取用者組態](https://kafka.apache.org/documentation#consumerconfigs)。

    toosave hello 檔案，使用**Ctrl + X**， **Y**，然後**Enter**。

3. 在設定之前進行通訊的 hello 生產者與 hello 目的地叢集，您必須尋找 hello broker 主機 hello**目的地**叢集。 使用下列命令 tooretrieve hello 這項資訊：

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    取代`$PASSWORD`與 hello 叢集 hello 登入帳戶 （管理員） 的密碼。

    取代`$CLUSTERNAME`hello hello 目的地叢集名稱。

    這些命令會傳回類似 toohello 下列資訊：

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. 使用 hello 遵循 toocreate`producer.properties`檔案，其中描述如何以 hello toocommunicate**目的地**叢集：

    ```bash
    nano producer.properties
    ```

    使用 hello 文字之後做為 hello 內容的 hello`producer.properties`檔案：

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    取代**DEST_BROKERS** hello broker hello 上一個步驟的資訊。

    如需產生者組態詳細資訊，請參閱 kafka.apache.org 上的[者組態](https://kafka.apache.org/documentation#producerconfigs)。

## <a name="start-mirrormaker"></a>啟動 MirrorMaker

1. 從 hello SSH 連線 toohello**目的地**叢集，請使用下列命令 toostart hello MirrorMaker 程序的 hello:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    此範例中使用的 hello 參數如下：

    * **-consumer.config**： 指定包含取用者屬性的 hello 檔案。 這些屬性是使用的 toocreate hello 可讀取的取用者*來源*Kafka 叢集。

    * **-producer.config**： 指定包含生產者屬性 hello 檔案。 這些屬性是使用的 toocreate 寫入 toohello 生產者*目的地*Kafka 叢集。

    * **-白名單**: MirrorMaker 複寫的 hello 來源叢集 toohello 目的地的主題清單。

    * **-num.streams**: hello 的取用者執行緒 toocreate 數目。

 在啟動時，MirrorMaker 傳回資訊的類似 toohello 下列文字：

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. 從 hello SSH 連線 toohello**來源**叢集，使用下列命令 toostart 生產者 hello 和傳送訊息 toohello 主題：

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    取代`$PASSWORD`hello 來源叢集的 hello （管理員） 登入密碼。

    取代`$CLUSTERNAME`hello hello 來源叢集名稱。

     當您抵達有游標的空白行時，請輸入一些文字訊息。 這些系統會傳送 hello toohello 主題**來源**叢集。 完成後，使用**Ctrl + C** tooend hello 生產者程序。

3. 從 hello SSH 連線 toohello**目的地**叢集，請使用**Ctrl + C** tooend hello MirrorMaker 程序。 然後使用 hello 下列命令 tooverify 該 hello`testtopic`主題建立，而且已 hello 主題中的資料已複寫的 toothis 鏡像：

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    取代`$PASSWORD`hello 目的地叢集 hello （管理員） 登入密碼。

    取代`$CLUSTERNAME`hello hello 目的地叢集名稱。

    hello 的主題清單現在包含`testtopic`，這在建立時 MirrorMaster 鏡像處理 hello 來源叢集 toohello 目的地從 hello 主題。 擷取從 hello 主題的 hello 訊息是 hello 與 hello 來源叢集上輸入相同。

## <a name="delete-hello-cluster"></a>刪除 hello 叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

因為這份文件中的 hello 步驟建立這兩者中的叢集 hello 相同的 Azure 資源群組，您可以刪除 hello hello Azure 入口網站中的資源群組。 正在刪除 hello 資源群組中移除依照此文件、 hello Azure 虛擬網路和 hello 叢集所使用的儲存體帳戶建立的所有資源。

## <a name="next-steps"></a>後續步驟

在本文件中，您學會如何 toouse MirrorMaker toocreate Kafka 複本叢集。 使用下列連結 toodiscover hello 其他方式 toowork 與 Kafka:

* [Apache Kafka MirrorMaker 文件](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) (網址為 cwiki.apache.org)。
* [開始使用 Apache Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)
* [使用 Apache Spark 搭配 Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)
* [使用 Apache Storm 搭配 HDInsight 上的 Kafka](hdinsight-apache-storm-with-kafka.md)
* [透過 Azure 虛擬網路連線 tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)
