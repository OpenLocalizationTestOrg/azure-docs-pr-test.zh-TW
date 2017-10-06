---
title: "在虛擬網路-Azure 中的 aaaCreate HBase 叢集 |Microsoft 文件"
description: "開始在 Azure HDInsight 中使用 HBase。 了解 Azure 虛擬網路上 toocreate HDInsight HBase 叢集的方式。"
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>在 Azure 虛擬網路的 HDInsight 上建立 HBase 叢集
了解如何 toocreate Azure HDInsight HBase 叢集[Azure 虛擬網路][1]。

與虛擬網路整合 HBase 叢集可以部署的 toohello 相同虛擬網路與您的應用程式因此應用程式可直接通訊使用 HBase。 hello 優點包括：

* 直接連線的 hello web 應用程式 toohello hello HBase 叢集節點，可讓通訊透過 HBase Java 遠端程序呼叫 (RPC) Api。
* 透過使流量不須經過多個閘道器及負載平衡器，以提升其效能。
* hello 能力 tooprocess 機密資訊以更安全的方式，而不會讓公用端點。

### <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須具備下列項目 hello:

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* **具有 Azure PowerShell 的工作站**。 請參閱 [安裝及使用 Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/)。

## <a name="create-hbase-cluster-into-virtual-network"></a>在虛擬網路上建立 HBase 叢集
在本節中，您必須建立以 Linux 為基礎的 HBase 叢集與 hello 相依 Azure 儲存體帳戶中的 Azure 虛擬網路使用[Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)。 適用於其他叢集建立方法，並了解 hello 設定，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。 如需有關使用範本 toocreate Hadoop 叢集 HDInsight 中，請參閱 <<c0> [ 建立 Hadoop 叢集 HDInsight 使用 Azure Resource Manager 範本中](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> 有些屬性是硬式編碼成 hello 範本。 例如：
>
> * **位置**：美國東部 2
> * **叢集版本**：3.5
> * **叢集背景工作節點計數**：2
> * **預設儲存體帳戶**：唯一的字串
> * **虛擬網路名稱**：&lt;叢集名稱>-vnet
> * **虛擬網路位址空間**10.0.0.0/16
> * **子網路名稱**：subnet1
> * **子網路位址範圍**：10.0.0.0/24
>
> &lt;叢集名稱 > 取代為您提供使用 hello 範本時的 hello 叢集名稱。
>
>

1. 按一下下列映像 tooopen hello 範本 hello Azure 入口網站中的 hello。 hello 範本位於[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/)。

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. 從 hello**自訂部署**刀鋒視窗中，輸入下列屬性的 hello:

   * **訂用帳戶**： 選取 使用的 Azure 訂用帳戶 toocreate hello HDInsight 叢集，hello 相依的儲存體帳戶，hello Azure 虛擬網路。
   * **資源群組**：選取 [新建] 並指定新的資源群組名稱。
   * **位置**： 選取 hello 資源群組的位置。
   * **ClusterName**： 輸入建立 hello Hadoop 叢集 toobe 的名稱。
   * **叢集登入名稱和密碼**: hello 預設登入名稱是**admin**。
   * **SSH 使用者名稱和密碼**: hello 預設使用者名稱是**sshuser**。  您可以將它重新命名。
   * **我同意 toohello 使用條款 hello 上述**: （選取）
3. 按一下 [購買]。 大約需要約 20 分鐘 toocreate 叢集。 一旦建立 hello 叢集後，您可以按一下 hello 叢集刀鋒視窗中 hello 入口 tooopen 它。

完成 hello 教學課程之後，您可能想 toodelete hello 叢集。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。 您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。 刪除叢集的 hello 指示，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站](hdinsight-administer-use-management-portal.md#delete-clusters)。

toobegin 使用新的 HBase 叢集，您可以使用 hello 程序中找到[開始透過 HDInsight 中的 Hadoop 使用 HBase](hdinsight-hbase-tutorial-get-started.md)。

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>連接使用 HBase Java RPC Api toohello HBase 叢集
1. 建立作為服務 (IaaS) 至虛擬機器的基礎結構 hello 相同 Azure 虛擬網路和 hello 相同子網路。 如需建立新的 IaaS 虛擬機器的指示，請參閱[建立執行 Windows Server 的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md)。 當遵循本文件中的 hello 步驟，您必須使用 hello hello 網路設定的值：

   * **虛擬網路**：&lt;叢集名稱>-vnet
   * **子網路**：subnet1

   > [!IMPORTANT]
   > 取代&lt;叢集名稱 > hello 名稱時所使用在先前步驟中建立 hello HDInsight 叢集。
   >
   >

   使用這些值，hello 虛擬機器會放置在 hello 相同虛擬網路和子網路與 hello HDInsight 叢集。 此設定可讓它們 toodirectly 與對方進行通訊。 沒有方法 toocreate 與空白邊緣節點的 HDInsight 叢集。 hello 邊緣節點可以是使用的 toomanage hello 叢集。  如需詳細資訊，請參閱 [Use empty edge nodes in HDInsight (在 HDInsight 中使用空白的邊緣節點)](hdinsight-apps-use-edge-node.md)。

2. 當從遠端使用 Java 應用程式 tooconnect tooHBase，您必須使用 hello 完整的網域名稱 (FQDN)。 toodetermine，您必須取得 hello HBase 叢集 hello 連線特定 DNS 尾碼。 toodo，您可以使用其中一個 hello 下列方法：

   * 使用 Web 瀏覽器 toomake Ambari 呼叫：

     瀏覽 toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / 裝載？ minimal_response = true。 它會以 hello DNS 後置字元的 JSON 檔案。
   * 使用 hello Ambari 網站：

     1. 瀏覽過 https://&lt;ClusterName >。.azurehdinsight.net。
     2. 按一下**主機**從 hello 上方的功能表。
   * 使用 Curl toomake REST 呼叫：

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     在 hello JavaScript Object Notation (JSON) 傳回的資料，尋找 hello"host_name"項目。 它包含 hello FQDN hello hello 叢集中的節點。 例如：

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     hello 部分 hello 網域名稱 hello 叢集名稱開頭是 hello DNS 尾碼。 例如，mycluster.b1.cloudapp.net。
   * 使用 Azure PowerShell

     使用下列 Azure PowerShell 指令碼 tooregister hello 的 hello **Get ClusterDetail**函式，它可以是使用的 tooreturn hello DNS 尾碼：

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     執行 hello Azure PowerShell 指令碼之後, 使用 hello 下列命令的 tooreturn hello DNS 尾碼來使用 hello **Get ClusterDetail**函式。 使用此命令時，請指定您的 HDInsight HBase 叢集名稱、管理員名稱和管理員密碼。

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     此命令會傳回 hello DNS 尾碼。 例如， **yourclustername.b4.internal.cloudapp.net**。


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

hello 虛擬機器的 tooverify 可以與 hello HBase 叢集，請使用 hello 命令`ping headnode0.<dns suffix>`從 hello 虛擬機器。 例如，ping headnode0.mycluster.b1.cloudapp.net。

toouse 這項資訊在 Java 應用程式中，您可以依照中的 hello 步驟[使用 Maven toobuild Java 應用程式與 HDInsight (Hadoop) 使用 HBase](hdinsight-hbase-build-java-maven.md) toocreate 應用程式。 toohave hello 應用程式連接 tooa 遠端 HBase 伺服器，修改 hello **hbase-site.xml**中的檔案，此範例 toouse hello FQDN 動物園管理員。 例如：

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> 如需有關名稱解析在 Azure 虛擬網路中，包括如何 toouse DNS 伺服器，請參閱[名稱解析 (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。
>
>

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學到如何 toocreate HBase 叢集。 toolearn 詳細資訊，請參閱：

* [開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [在 HDInsight 中使用空白邊緣節點](hdinsight-apps-use-edge-node.md)
* [在 HDInsight 中設定 HBase 複寫](hdinsight-hbase-replication.md)
* [在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)
* [開始在 HDInsight 中搭配使用 HBase 與 Hadoop](hdinsight-hbase-tutorial-get-started.md)
* [使用 HDInsight 中的 HBase 分析 Twitter 情緒](hdinsight-hbase-analyze-twitter-sentiment.md)
* [虛擬網路概觀][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Hello 新 HBase 叢集的佈建詳細資料"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "使用指令碼動作 toocustomize HBase 叢集"

[azure-preview-portal]: https://portal.azure.com
