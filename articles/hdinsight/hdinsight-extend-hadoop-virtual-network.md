---
title: "與虛擬網路的 Azure HDInsight aaaExtend |Microsoft 文件"
description: "了解如何 toouse Azure 虛擬網路 tooconnect HDInsight tooother 雲端資源或您的資料中心中的資源"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>使用 Azure 虛擬網路延伸 Azure HDInsight

深入了解如何 toouse HDInsight 與[Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。 使用 Azure 虛擬網路可讓 hello 下列案例：

* 直接從內部部署網路連接 tooHDInsight。

* 連接 HDInsight toodata 會儲存在 Azure 虛擬網路中。

* 直接存取 Hadoop 服務無法使用的公開超過 hello 網際網路。 例如，Kafka 應用程式開發介面或 hello HBase Java 應用程式開發介面。

> [!WARNING]
> 本文件中的 hello 資訊需要 TCP/IP 網路中了的解。 如果您不熟悉使用 TCP/IP 網路中，您應該與之前進行修改 tooproduction 網路的人員合作。

## <a name="planning"></a>規劃

hello 下面是 hello 規劃 tooinstall HDInsight 中的虛擬網路時，您必須回答的問題：

* 您需要 tooinstall HDInsight 到現有的虛擬網路嗎？ 或者，您要建立新的網路嗎？

    如果您使用現有的虛擬網路，您可能需要 toomodify hello 網路組態，才能安裝 HDInsight。 如需詳細資訊，請參閱 hello[新增 HDInsight tooan 現有的虛擬網路](#existingvnet)> 一節。

* 您想 tooconnect hello 虛擬網路包含 HDInsight tooanother 虛擬網路或內部部署網路嗎？

    tooeasily 工作以跨網路資源，您可能需要 toocreate 自訂 DNS，並設定 DNS 轉送。 如需詳細資訊，請參閱 hello[連接多個網路](#multinet)> 一節。

* 您想 toorestrict/重新導向輸入或輸出流量 tooHDInsight 嗎？

    HDInsight 必須具有無限制的 hello Azure 資料中心中的特定 IP 位址的通訊。 另外還有數個連接埠必須允許通過防火牆才能進行用戶端通訊。 如需詳細資訊，請參閱 hello[控制網路流量](#networktraffic)> 一節。

## <a id="existingvnet"></a>新增 HDInsight tooan 現有的虛擬網路

如何使用這個區段 toodiscover 中的 hello 步驟 tooadd 新的 HDInsight tooan，現有的 Azure 虛擬網路。

> [!NOTE]
> 您無法在虛擬網路中新增現有的 HDInsight 叢集。

1. 您使用傳統 」 或 「 資源管理員部署模型 hello 虛擬網路？

    HDInsight 3.4 和更新版本需要 Resource Manager 虛擬網路。 舊版 HDInsight 需要傳統虛擬網路。

    如果您現有的網路是傳統的虛擬網路，您必須建立資源管理員的虛擬網路，然後再連接兩個 hello。 [連接傳統 Vnet toonew Vnet](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)。

    一旦加入，HDInsight hello 資源管理員網路中安裝可以互動 hello 傳統網路中的資源。

2. 您使用強制通道嗎？ 強制通道是子網路設定，會強制檢查的傳出網際網路流量 tooa 裝置和記錄。 HDInsight 不支援強制通道。 先移除強制通道，再將 HDInsight 安裝至子網路，或建立 HDInsight 的新子網路。

3. 您使用網路安全性群組的相關、 使用者定義的路由或虛擬網路應用裝置 toorestrict 流量傳入或傳出 hello 虛擬網路？

    為受管理的服務，HDInsight 需要 hello Azure 資料中心中的無限制的存取 tooseveral IP 位址。 tooallow 通訊，這些 IP 位址，與更新的任何現有的網路安全性群組或使用者定義的路由。

    HDInsight 會裝載多個使用各種連接埠的服務。 不會封鎖流量 toothese 連接埠。 如需通過虛擬設備的防火牆連接埠 tooallow 的清單，請參閱 hello[安全性](#security)> 一節。

    toofind 您現有的安全性組態，使用下列 Azure PowerShell 或 Azure CLI 命令的 hello:

    * 網路安全性群組

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        如需詳細資訊，請參閱 hello[疑難排解網路安全性群組](../virtual-network/virtual-network-nsg-troubleshoot-portal.md)文件。

        > [!IMPORTANT]
        > 會根據規則優先順序依序套用網路安全性群組規則。 hello 符合 hello 流量模式的第一個規則會套用，且沒有其他適用於該流量。 順序從最寬鬆 tooleast 寬鬆的規則。 如需詳細資訊，請參閱 hello[篩選網路流量的網路安全性群組](../virtual-network/virtual-networks-nsg.md)文件。

    * 使用者定義的路由

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        如需詳細資訊，請參閱 hello[疑難排解路由](../virtual-network/virtual-network-routes-troubleshoot-portal.md)文件。

4. 建立 HDInsight 叢集，並在設定期間選取 hello Azure 虛擬網路。 使用下列文件 toounderstand hello 叢集建立程序的 hello 中 hello 步驟：

    * [建立 HDInsight 使用 hello Azure 入口網站](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [使用 Azure PowerShell 建立 HDInsight](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [使用 Azure CLI 1.0 建立 HDInsight](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [使用 Azure Resource Manager 範本建立 HDInsight](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > 新增 HDInsight tooa 虛擬網路是選用設定步驟。 設定 hello 叢集時，是確定 tooselect hello 虛擬網路。

## <a id="multinet"></a>連線多個網路

hello 與多個網路設定最大的挑戰是 hello 網路之間的名稱解析。

Azure 會針對安裝於虛擬網路中的 Azure 服務提供名稱解析。 此內建的名稱解析可讓 HDInsight tooconnect toohello 下列使用完整的網域名稱 (FQDN) 的資源：

* 可使用的任何資源 hello 網際網路。 例如，microsoft.com、google.com。

* 是在 hello 相同 Azure 虛擬網路，使用 hello 任何資源__內部 DNS 名稱__的 hello 資源。 例如，當使用 hello 預設名稱解析，hello 如下範例內部 DNS 名稱指派的 tooHDInsight 背景工作節點：

    * wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    這些節點可以使用內部 DNS 名稱彼此直接通訊，以及與 HDInsight 中的其他節點通訊。

hello 預設名稱解析沒有__不__內聯結的 toohello 虛擬網路的網路中允許 HDInsight tooresolve hello 資源的名稱。 比方說，是通用 toojoin 您內部網路 toohello 虛擬網路。 只有 hello 預設名稱解析，HDInsight 無法透過名稱存取 hello 與內部網路中的資源。 相反的 hello 也是為 true，在內部部署網路中的資源無法透過名稱存取 hello 虛擬網路中的資源。

> [!WARNING]
> 您必須建立 hello 自訂 DNS 伺服器，並設定 hello 虛擬網路 toouse 它之前建立 hello HDInsight 叢集。

tooenable hello 虛擬網路之間聯結的網路中的資源名稱解析，您必須執行下列動作的 hello:

1. Hello 您計劃 tooinstall HDInsight 的 Azure 虛擬網路中建立自訂的 DNS 伺服器。

2. Hello 虛擬網路 toouse hello 自訂 DNS 伺服器設定。

3. Azure 虛擬網路的 DNS 尾碼指派給的 hello 中尋找。 此值就會類似太`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`。 如需尋找 hello DNS 尾碼，請參閱 hello[範例： 自訂 DNS](#example-dns) > 一節。

4. 設定 hello DNS 伺服器之間的轉送。 遠端網路 hello 類型 hello 組態而定。

    * 如果 hello 遠端網路與內部網路，設定 DNS，如下所示：
        
        * __自訂 DNS__ （hello 虛擬網路中）：

            * 轉寄要求 hello hello 虛擬網路 toohello Azure 遞迴解析程式 (168.63.129.16) 的 DNS 尾碼。 Azure 會處理 hello 虛擬網路中的資源的要求

            * 轉寄所有其他要求 toohello 在內部部署 DNS 伺服器。 hello 內部 DNS 會處理所有其他的名稱解析要求，甚至是網際網路資源，例如 Microsoft.com 要求。

        * __在內部部署 DNS__: hello 虛擬網路的 DNS 尾碼 toohello 自訂 DNS 伺服器的要求轉送。 hello 自訂 DNS 伺服器，然後轉送 toohello Azure 遞迴解析程式。

        此組態路由要求完整網域名稱包含 hello hello 虛擬網路 toohello 自訂 DNS 伺服器的 DNS 尾碼。 Hello 在內部部署 DNS 伺服器會處理 （即使是針對公用的網際網路位址） 的所有其他要求。

    * 如果另一個 Azure 虛擬網路 hello 遠端網路，設定 DNS，如下所示：

        * 「自訂 DNS」(在每個虛擬網路中)：

            * Hello hello 虛擬網路的 DNS 尾碼的要求都會轉送 toohello 自訂 DNS 伺服器。 每個虛擬網路中的 hello DNS 會負責解析其網路內的資源。

            * 轉寄所有其他要求 toohello Azure 遞迴解析程式。 hello 遞迴解析程式負責解決本機和網際網路資源。

        每個網路的 hello DNS 伺服器會將轉送要求 toohello 其他，根據 DNS 尾碼。 其他要求會解析使用 hello Azure 遞迴解析程式。

    如需每個組態的範例，請參閱 hello[範例： 自訂 DNS](#example-dns) > 一節。

如需詳細資訊，請參閱 hello [Vm 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)文件。

## <a name="directly-connect-toohadoop-services"></a>直接連接 tooHadoop 服務

HDInsight 上的大部分文件假設您有存取 toohello 叢集 hello 透過網際網路。 例如，您可以連接 https://CLUSTERNAME.azurehdinsight.net toohello 叢集。 這個位址會使用 hello 公用閘道，如果您已經使用 Nsg，或從 UDRs toorestrict 存取 hello 網際網路，則無法使用此。

tooconnect tooAmbari 和其他網頁透過 hello 虛擬網路，使用下列步驟的 hello:

1. toodiscover hello 內部的完整的網域名稱 (FQDN) 的 hello HDInsight 叢集節點，使用其中一種 hello 下列方法：

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    在 [hello] 清單中傳回的節點，尋找 hello FQDN hello 前端節點和使用 hello Fqdn tooconnect tooAmbari 及其他 web 服務。 例如，使用`http://<headnode-fqdn>:8080`tooaccess Ambari。

    > [!IMPORTANT]
    > 某些 hello 前端節點上裝載的服務才一次一個節點上使用中。 如果您嘗試存取一個前端節點上的服務，它會傳回 404 錯誤，請切換 toohello 其他前端節點。

2. toodetermine hello 節點和可用通訊埠的服務，請參閱 hello [HDInsight 上的 Hadoop 服務所使用的連接埠](./hdinsight-hadoop-port-settings-for-services.md)文件。

## <a id="networktraffic"></a> 控制網路流量

您可以使用下列方法 hello 控制 Azure 虛擬網路中的網路流量：

* **網路安全性群組**(NSG) toofilter 輸入和輸出流量 toohello 網路可讓您。 如需詳細資訊，請參閱 hello[篩選網路流量的網路安全性群組](../virtual-network/virtual-networks-nsg.md)文件。

    > [!WARNING]
    > HDInsight 不支援限制輸出流量。

* **使用者定義的路由**(UDR) 定義流量在 hello 網路資源之間流動的方式。 如需詳細資訊，請參閱 hello[使用者定義的路由與 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)文件。

* **網路虛擬裝置**複寫 hello 功能的裝置，例如防火牆和路由器。 如需詳細資訊，請參閱 hello[網路應用裝置](https://azure.microsoft.com/solutions/network-appliances)文件。

為受管理的服務，HDInsight 需要無限制的存取 tooAzure 健全狀況和管理服務在 hello Azure 雲端中。 使用 NSG 和 UDR 時，您必須確定這些服務仍然可以與 HDInsight 進行通訊。

HDInsight 會在數個連接埠上公開服務。 時使用的虛擬設備的防火牆，您必須允許流量 hello 用於這些服務的通訊埠。 如需詳細資訊，請參閱 hello [必要的連接埠] 區段。

### <a id="hdinsight-ip"></a> 具有網路安全性群組和使用者定義路由的 HDInsight

如果您計劃使用**網路安全性群組**或**使用者定義的路由**toocontrol 網路流量，請執行下列動作，然後再安裝 HDInsight hello:

1. 識別 hello toouse 規劃 HDInsight 的 Azure 區域。

2. 識別所需的 HDInsight hello IP 位址。 如需詳細資訊，請參閱 hello [HDInsight 所需的 IP 位址](#hdinsight-ip)> 一節。

3. 建立或修改 hello 網路安全性群組或使用者定義您計劃 tooinstall HDInsight hello 子網路的路由到。

    * __網路安全性群組__： 允許__輸入__連接埠的流量__443__來自 hello IP 位址。
    * __使用者定義的路由__： 建立路由 tooeach IP 位址，以及設定 hello__下個躍點類型__too__Internet__。

如需網路安全性群組或使用者定義的路由的詳細資訊，請參閱下列文件的 hello:

* [網路安全性群組](../virtual-network/virtual-networks-nsg.md)

* [使用者定義路由](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>強制通道

強制通道是其中所有流量子網路都是強制的 tooa 特定網路或位置，例如您在內部部署網路的使用者定義的路由組態。 HDInsight「不」支援強制通道。

## <a id="hdinsight-ip"></a> 所需的 IP 位址

> [!IMPORTANT]
> hello Azure 的健全狀況並管理服務必須與 HDInsight 無法 toocommunicate。 如果您使用網路安全性群組或使用者定義的路由，允許從 hello 流量這些服務 tooreach HDInsight 的 IP 位址。
>
> 如果您不想使用網路安全性群組或使用者定義的路由 toocontrol 流量，您可以忽略此區段。

如果您使用網路安全性群組或使用者定義的路由，您必須允許來自 hello Azure 健康情況與管理服務 tooreach HDInsight 的流量。 使用下列步驟 toofind hello 允許的 IP 位址必須是 hello:

1. 您永遠必須允許來自下列 IP 位址的 hello 流量：

    | IP 位址 | 允許的連接埠 | 方向 |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | 輸入 |
    | 23.99.5.239 | 443 | 輸入 |
    | 168.61.48.131 | 443 | 輸入 |
    | 138.91.141.162 | 443 | 輸入 |

2. 如果您的 HDInsight 叢集位於 hello 下列區域的其中一個，您必須允許從 hello hello 地區列出的 IP 位址的流量：

    > [!IMPORTANT]
    > 如果未列出 hello 您使用的 Azure 區域，則只能使用步驟 1 中的 hello 四個 IP 位址。

    | 國家 (地區) | 區域 | 允許的 IP 位址 | 允許的連接埠 | 方向 |
    | ---- | ---- | ---- | ---- | ----- |
    | 亞洲 | 東亞 | 23.102.235.122</br>52.175.38.134 | 443 | 輸入 |
    | &nbsp; | 東南亞 | 13.76.245.160</br>13.76.136.249 | 443 | 輸入 |
    | 澳大利亞 | 澳洲東部 | 104.210.84.115</br>13.75.152.195 | 443 | 輸入 |
    | &nbsp; | 澳大利亞東南部 | 13.77.2.56</br>13.77.2.94 | 443 | 輸入 |
    | 巴西 | 巴西南部 | 191.235.84.104</br>191.235.87.113 | 443 | 輸入 |
    | 加拿大 | 加拿大東部 | 52.229.127.96</br>52.229.123.172 | 443 | 輸入 |
    | &nbsp; | 加拿大中部 | 52.228.37.66</br>52.228.45.222 | 443 | 輸入 |
    | 中國 | 中國北部 | 42.159.96.170</br>139.217.2.219 | 443 | 輸入 |
    | &nbsp; | 中國東部 | 42.159.198.178</br>42.159.234.157 | 443 | 輸入 |
    | 歐洲 | 北歐 | 52.164.210.96</br>13.74.153.132 | 443 | 輸入 |
    | &nbsp; | 西歐| 52.166.243.90</br>52.174.36.244 | 443 | 輸入 |
    | 德國 | 德國中部 | 51.4.146.68</br>51.4.146.80 | 443 | 輸入 |
    | &nbsp; | 德國東北部 | 51.5.150.132</br>51.5.144.101 | 443 | 輸入 |
    | 印度 | 印度中部 | 52.172.153.209</br>52.172.152.49 | 443 | 輸入 |
    | 日本 | 日本東部 | 13.78.125.90</br>13.78.89.60 | 443 | 輸入 |
    | &nbsp; | 日本西部 | 40.74.125.69</br>138.91.29.150 | 443 | 輸入 |
    | 韓國 | 韓國中部 | 52.231.39.142</br>52.231.36.209 | 433 | 輸入 |
    | &nbsp; | 韓國南部 | 52.231.203.16</br>52.231.205.214 | 443 | 輸入
    | 英國 | 英國西部 | 51.141.13.110</br>51.141.7.20 | 443 | 輸入 |
    | &nbsp; | 英國南部 | 51.140.47.39</br>51.140.52.16 | 443 | 輸入 |
    | 美國 | 美國中部 | 13.67.223.215</br>40.86.83.253 | 443 | 輸入 |
    | &nbsp; | 美國中北部 | 157.56.8.38</br>157.55.213.99 | 443 | 輸入 |
    | &nbsp; | 美國中西部 | 52.161.23.15</br>52.161.10.167 | 443 | 輸入 |
    | &nbsp; | 美國西部 2 | 52.175.211.210</br>52.175.222.222 | 443 | 輸入 |

    有關 hello IP 位址 Azure 政府 toouse，請參閱 hello [Azure 政府智慧 + 分析](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics)文件。

3. 如果您搭配使用自訂 DNS 伺服器與虛擬網路，則也必須允許從 __168.63.129.16__ 進行存取。 此位址是 Azure 遞迴解析程式。 如需詳細資訊，請參閱 hello[名稱解析的 Vm 和角色執行個體](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)文件。

如需詳細資訊，請參閱 hello[控制網路流量](#networktraffic)> 一節。

## <a id="hdinsight-ports"></a> 所需連接埠

如果您打算使用網路**虛擬設備防火牆**toosecure hello 虛擬網路，您必須在 hello 下列連接埠上允許輸出流量：

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

如需特定的服務連接埠的清單，請參閱 hello [HDInsight 上的 Hadoop 服務所使用的連接埠](hdinsight-hadoop-port-settings-for-services.md)文件。

如需有關虛擬應用程式的防火牆規則的詳細資訊，請參閱 hello[虛擬設備案例](../virtual-network/virtual-network-scenario-udr-gw-nva.md)文件。

## <a id="hdinsight-nsg"></a>範例：網路安全性群組與 HDInsight

本節中的 hello 範例示範如何 toocreate 網路安全性群組規則來允許 HDInsight toocommunicate hello 與 Azure 的管理服務。 使用 hello 範例之前，調整 hello IP 位址 toomatch hello 的 hello 您使用的 Azure 區域。 您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。

### <a name="azure-resource-management-template"></a>Azure 資源管理範本

hello 下列資源管理範本建立虛擬網路時，限制的輸入的流量，但允許來自 hello HDInsight 所需的 IP 位址的流量。 此範本也會 hello 虛擬網路中建立的 HDInsight 叢集。

* [部署安全的 Azure 虛擬網路和 HDInsight Hadoop 叢集](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> 變更用於此範例 toomatch hello 您使用的 Azure 區域中的 hello IP 位址。 您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。

### <a name="azure-powershell"></a>Azure PowerShell

使用下列 PowerShell 指令碼 toocreate 限制的輸入的流量，並允許流量從 hello hello 北歐區域的 IP 位址的虛擬網路的 hello。

> [!IMPORTANT]
> 變更用於此範例 toomatch hello 您使用的 Azure 區域中的 hello IP 位址。 您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> 此範例示範如何 tooadd 規則 tooallow 輸入 hello 所需的 IP 位址的流量。 它不包含規則 toorestrict 輸入從其他來源的存取。
>
> hello 下列範例將示範如何從 hello 網際網路存取 tooenable SSH:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Azure CLI

使用下列步驟 toocreate 限制的輸入的流量，但允許流量從 hello HDInsight 所需的 IP 位址的虛擬網路的 hello。

1. 使用下列命令 toocreate 名為新的網路安全性群組的 hello `hdisecure`。 取代**RESOURCEGROUPNAME** hello 包含 hello Azure 虛擬網路的資源群組。 取代**位置**該 hello 群組建立在與 hello 位置 （地區）。

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    一旦建立 hello 群組之後，您會收到 hello 新群組的詳細資訊。

2. 使用下列 tooadd 規則 toohello 新網路安全性群組，允許傳入的通訊連接埠 443 從 hello Azure HDInsight 健全狀況和管理服務的 hello。 取代**RESOURCEGROUPNAME** hello hello 包含 hello Azure 虛擬網路的資源群組名稱。

    > [!IMPORTANT]
    > 變更用於此範例 toomatch hello 您使用的 Azure 區域中的 hello IP 位址。 您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve hello 此網路安全性群組的唯一識別碼，請使用下列命令的 hello:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    此命令會傳回值的類似 toohello，下列文字：

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    如果沒有得到預期的 hello 結果，請使用雙引號括住識別碼 hello 命令中。

4. 使用下列命令 tooapply hello 網路安全性群組 tooa 子網路的 hello。 取代 hello __GUID__和__RESOURCEGROUPNAME__ hello 上一個步驟傳回以 hello 的值。 取代__VNETNAME__和__SUBNETNAME__ hello 虛擬網路名稱與您想要 toocreate 的子網路名稱。

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    此命令完成之後，您可以安裝 HDInsight 中 hello 虛擬網路。

> [!IMPORTANT]
> 這些步驟只會開啟存取 toohello HDInsight 健全狀況和管理服務上 hello Azure 雲端。 任何其他存取 toohello HDInsight 叢集從外部 hello 虛擬網路會被封鎖。 tooenable 存取外部 hello 虛擬網路，您必須加入額外的網路安全性群組規則。
>
> hello 下列範例將示範如何從 hello 網際網路存取 tooenable SSH:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a> 範例：DNS 設定

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>虛擬網路與已連線內部部署網路之間的名稱解析

這個範例會進行下列假設 hello:

* 您有 Azure 虛擬網路所使用的 VPN 閘道連線的 tooan 在內部部署網路。

* hello 自訂 DNS 伺服器 hello 虛擬網路中的執行的 Linux 或 Unix hello 作業系統。

* [繫結](https://www.isc.org/downloads/bind/)hello 自訂 DNS 伺服器上已安裝。

Hello 自訂 DNS 伺服器上 hello 虛擬網路中：

1. 使用 Azure PowerShell 或 Azure CLI toofind hello 的 DNS 尾碼 hello 虛擬網路：

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Hello 自訂 DNS 伺服器上 hello 虛擬網路，使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.local`檔案：

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    取代 hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello 的虛擬網路的 DNS 尾碼的值。

    此設定會路由傳送 hello hello 虛擬網路 toohello Azure 遞迴解析程式的 DNS 尾碼的所有 DNS 要求。

2. Hello 自訂 DNS 伺服器上 hello 虛擬網路，使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.options`檔案：

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * 取代 hello `10.0.0.0/16` hello IP 位址範圍，為您的虛擬網路的值。 此項目允許來自此範圍內位址的名稱解析要求。

    * 新增 hello IP 位址範圍的 hello 在內部部署網路 toohello `acl goodclients { ... }` > 一節。  項目允許 hello 與內部網路中的名稱解析要求的資源。
    
    * 取代 hello 值`192.168.0.1`hello 在內部部署 DNS 伺服器的 IP 位址。 此項目會路由傳送所有其他 DNS 要求 toohello 在內部部署 DNS 伺服器。

3. toouse hello 組態，重新啟動繫結。 例如： `sudo service bind9 restart`。

4. 加入條件式轉寄站 toohello 在內部部署 DNS 伺服器。 Hello 條件轉寄站 toosend 要求設定為從步驟 1 toohello 自訂 DNS 伺服器 hello DNS 尾碼。

    > [!NOTE]
    > 請參閱您的 DNS 軟體，如需有關的特定資訊 hello 文件 tooadd 條件轉寄站。

完成這些步驟之後，您可以連接 tooresources 使用完整的網域名稱 (FQDN) 是網路中。 您現在可以安裝 HDInsight 在 hello 的虛擬網路。

### <a name="name-resolution-between-two-connected-virtual-networks"></a>兩個已連線虛擬網路之間的名稱解析

這個範例會進行下列假設 hello:

* 您的兩個 Azure 虛擬網路是使用 VPN 閘道或對等進行連線。

* 在兩個網路 hello 自訂 DNS 伺服器正在執行 Linux 或 Unix 做為 hello 作業系統。

* [繫結](https://www.isc.org/downloads/bind/)hello 自訂 DNS 伺服器上安裝。

1. 使用 Azure PowerShell 或 Azure CLI toofind hello DNS 尾碼的這兩個虛擬網路：

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. 使用 hello 文字之後做為 hello 內容的 hello `/etc/bind/named.config.local` hello 自訂 DNS 伺服器上的檔案。 這兩個虛擬網路中 hello 自訂 DNS 伺服器上進行這項變更。

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    取代 hello`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`值且 hello DNS 尾碼為 hello__其他__虛擬網路。 此項目會將要求 hello 遠端網路 toohello hello DNS 尾碼的路由網路中的自訂 DNS。

3. Hello 自訂 DNS 伺服器上在兩個虛擬網路，使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.options`檔案：

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * 取代 hello`10.0.0.0/16`和`10.1.0.0/16`值與 hello IP 位址的虛擬網路的範圍。 此項目可讓每個網路中的資源 toomake hello DNS 伺服器的要求。

    Hello Azure 遞迴解析程式會處理 hello hello 虛擬網路 (例如，microsoft.com) 的 DNS 尾碼不是任何要求。

4. toouse hello 組態，重新啟動繫結。 例如，兩部 DNS 伺服器上的 `sudo service bind9 restart`。

完成這些步驟之後，您可以連接 tooresources hello 使用完整的網域名稱 (FQDN) 的虛擬網路中。 您現在可以安裝 HDInsight 在 hello 的虛擬網路。

## <a name="next-steps"></a>後續步驟

* 設定 HDInsight tooconnect tooan 在內部部署網路的端對端範例，請參閱[連接 HDInsight tooan 在內部部署網路](./connect-on-premises-network.md)。

* 如需有關 Azure 虛擬網路的詳細資訊，請參閱 hello [Azure 虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。

* 如需網路安全性群組的詳細資訊，請參閱[網路安全性群組](../virtual-network/virtual-networks-nsg.md)。

* 如需使用者定義路由的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。