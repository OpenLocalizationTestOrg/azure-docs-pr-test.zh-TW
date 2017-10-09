---
title: "aaaConnect HDInsight tooyour 在內部部署網路 Azure HDInsight |Microsoft 文件"
description: "了解如何 toocreate 在 HDInsight 叢集的 Azure 虛擬網路，然後再連接 tooyour 在內部部署網路。 了解如何 tooconfigure 之間的名稱解析 HDInsight 與內部部署網路使用自訂的 DNS 伺服器。"
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>HDInsight tooyour 在內部部署網路連線

了解如何 tooconnect HDInsight tooyour 內部部署網路使用 Azure 虛擬網路和 VPN 閘道。 本文件提供下列規劃資訊：

* 使用 HDInsight 連接 tooyour Azure 虛擬網路中內部網路。

* 設定 hello 虛擬網路與內部部署網路之間的 DNS 名稱解析。

* 設定網路安全性群組 toorestrict 網際網路存取 tooHDInsight。

* HDInsight 在 hello 虛擬網路上提供的連接埠。

## <a name="create-hello-virtual-network-configuration"></a>建立 hello 虛擬網路組態

> [!IMPORTANT]
> 如果您要尋找的逐步指引連接 HDInsight tooyour 內部網路，使用 Azure 虛擬網路，請參閱 hello[連接 HDInsight tooyour 在內部部署網路](connect-on-premises-network.md)文件。

使用 hello 下列文件 toolearn 如何 toocreate Azure 虛擬網路的連線的 tooyour 內部網路：
    
* [使用 hello Azure 入口網站](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [使用 Azure PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [使用 Azure CLI](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>設定名稱解析

tooallow HDInsight 和 hello 加入網路 toocommunicate 依名稱中的資源，您必須執行下列動作的 hello:

* 在 hello Azure 虛擬網路中建立自訂的 DNS 伺服器。

* Hello 虛擬網路 toouse hello 自訂 DNS 伺服器設定而非 hello 預設 Azure 遞迴解析程式。

* 設定自訂 DNS 伺服器 hello 與您的內部部署 DNS 伺服器之間的轉送。

此設定可啟用 hello 下列行為：

* 要求的完整的網域名稱擁有 hello DNS 尾碼__hello 虛擬網路__轉送 toohello 自訂 DNS 伺服器。 hello 自訂 DNS 伺服器，然後轉送這些要求 toohello Azure 遞迴解析程式，會傳回 hello IP 位址。

* 所有其他要求都會轉送 toohello 在內部部署 DNS 伺服器。 公用網際網路資源，例如 microsoft.com 甚至的要求都會轉送 toohello 在內部部署 DNS 伺服器進行名稱解析。

在下列圖表 hello，綠色行會結束 hello hello 虛擬網路的 DNS 尾碼 中的資源要求。 藍線是要求資源 hello 在內部部署網路中或在 hello 公用網際網路。

![DNS 要求如何解決在使用這份文件中的 hello 組態中的圖表](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>建立自訂的 DNS 伺服器

> [!IMPORTANT]
> 您必須建立並設定 hello DNS 伺服器，然後再安裝 HDInsight 在 hello 的虛擬網路。

toocreate Linux VM 使用 hello[繫結](https://www.isc.org/downloads/bind/)DNS 軟體，使用 hello 下列步驟：

> [!NOTE]
> hello 下列步驟使用 hello [Azure 入口網站](https://portal.azure.com)toocreate Azure 虛擬機器。 其他方式 toocreate 虛擬機器，請參閱 hello[建立的 VM-Azure CLI](../virtual-machines/linux/quick-create-cli.md)和[建立 VM 的 Azure PowerShell](../virtual-machines/linux/quick-create-portal.md)文件。

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取 __+__ ，__計算__，和__Ubuntu Server 16.04 LTS__。

    ![建立 Ubuntu 虛擬機器](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. 從 hello__基本概念__區段中，輸入下列資訊的 hello:

    * __名稱__：識別此虛擬機器的易記名稱。 例如，__DNSProxy__。
    * __使用者名稱__: hello hello SSH 帳戶名稱。
    * __SSH 公開金鑰__或__密碼__: hello hello SSH 帳戶的驗證方法。 我們建議使用公開金鑰，因為它們較為安全。 如需詳細資訊，請參閱 hello[適用於 Linux Vm 建立及使用 SSH 金鑰](../virtual-machines/linux/mac-create-ssh-keys.md)文件。
    * __資源群組__： 選取__使用現有__，然後選取 hello 資源群組含有 hello 稍早建立的虛擬網路。
    * __位置__： 選取 hello 與 hello 虛擬網路相同的位置。

    ![虛擬機器基本設定](./media/connect-on-premises-network/vm-basics.png)

    將其他項目在 hello 保留預設值，然後選取 __確定__。

3. 從 hello__大小選擇 「__區段中，選取 hello VM 大小。 此教學課程中，選取最小的 hello 和最低成本的選項。 toocontinue，使用 hello__選取__ 按鈕。

4. 從 hello__設定__區段中，輸入下列資訊的 hello:

    * __虛擬網路__： 選取 hello 您稍早建立的虛擬網路。

    * __子網路__： 選取 hello hello 虛擬網路的預設子網路。 請勿__不__選取 hello hello VPN 閘道使用的子網路。

    * __診斷儲存體帳戶__：選取現有的儲存體帳戶或建立新的儲存體帳戶。

    ![虛擬網路設定](./media/connect-on-premises-network/virtual-network-settings.png)

    將保留 hello 其他項目 hello 預設值，然後選取 __確定__toocontinue。

5. 從 hello__購買__區段中，選取 hello__購買__按鈕 toocreate hello 虛擬機器。

6. 一旦建立 hello 虛擬機器之後，其__概觀__區段會顯示。 從左側 hello hello 清單中選取__屬性__。 儲存 hello__公用 IP 位址__和__私人 IP 位址__值。 它會使用 hello 下一節。

    ![公用和私人 IP 位址](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>安裝並設定 Bind (DNS 軟體)

1. 使用 SSH tooconnect toohello__公用 IP 位址__hello 虛擬機器。 下列範例中的 hello 連線 40.68.254.142 tooa 虛擬機器：

    ```bash
    ssh sshuser@40.68.254.142
    ```

    取代`sshuser`hello SSH 使用者帳戶與您在建立時指定 hello 叢集。

    > [!NOTE]
    > 有各種不同的方式 tooobtain hello`ssh`公用程式。 在 Linux、 Unix 及 macOS，它是依現狀 hello 作業系統的一部分。 如果您使用 Windows 時，請考慮使用其中一個 hello 下列選項：
    >
    > * [Azure Cloud Shell](../cloud-shell/quickstart.md)
    > * [在 Windows 10 上 Ubuntu 上的 Bash](https://msdn.microsoft.com/commandline/wsl/about)
    > * [Git (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall 繫結，請使用下列命令從 hello SSH 工作階段的 hello:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure 繫結 tooforward 名稱解析要求 tooyour 內部 DNS 伺服器，請使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.options`檔案：

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Hello 中的 hello 值取代為`goodclients`hello IP 位址範圍的 hello 虛擬網路與內部部署網路的一節。 這個區段會定義此 DNS 伺服器接受來自要求的 hello 位址。
    >
    > 取代 hello `192.168.0.1` hello 中的項目`forwarders`hello IP 位址在內部部署 DNS 伺服器的一節。 此項目路由 DNS 要求 tooyour 內部 DNS 伺服器進行解析。

    tooedit 此檔案，請使用下列命令的 hello:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    toosave hello 檔案，使用__Ctrl + X__， __Y__，然後__Enter__。

4. 從 hello SSH 工作階段，使用下列命令的 hello:

    ```bash
    hostname -f
    ```

    此命令會傳回值的類似 toohello，下列文字：

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    hello`icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net`文字是 hello __DNS 尾碼__為此虛擬網路。 儲存這個值以便稍後使用。

5. tooconfigure 繫結 tooresolve DNS 名稱 hello 虛擬網路中資源的使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.local`檔案：

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > 您必須取代 hello`icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net`與您先前擷取的 hello DNS 尾碼。

    tooedit 此檔案，請使用下列命令的 hello:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    toosave hello 檔案，使用__Ctrl + X__， __Y__，然後__Enter__。

6. toostart 繫結，請使用下列命令的 hello:

    ```bash
    sudo service bind9 restart
    ```

7. 繫結的 tooverify 可以解決 hello 資源名稱的內部部署網路中、 使用 hello 下列命令：

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > 取代`dns.mynetwork.net`與 hello 完整的網域名稱 (FQDN) 的內部部署網路中的資源。
    >
    > 取代`10.0.0.4`以 hello__內部 IP 位址__的 hello 虛擬網路中的自訂 DNS 伺服器。

    hello 回應會顯示下列文字類似 toohello:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Hello 虛擬網路 toouse hello 自訂 DNS 伺服器設定

tooconfigure hello 虛擬網路 toouse hello 自訂 DNS 伺服器，而非 hello Azure 遞迴解析程式，使用下列步驟的 hello:

1. 在 hello [Azure 入口網站](https://portal.azure.com)選取 hello 虛擬網路，然後選取__DNS 伺服器__。

2. 選取__自訂__，然後輸入 hello__內部 IP 位址__hello 自訂 DNS 伺服器。 最後，選取 [儲存]。

    ![設定 hello 自訂網路 DNS 伺服器 hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Hello 在內部部署 DNS 伺服器設定

在 hello 前一個區段中，您可以設定 hello 自訂 DNS 伺服器 tooforward 要求 toohello 在內部部署 DNS 伺服器。 接下來，您必須設定 hello 在內部部署 DNS 伺服器 tooforward 要求 toohello 自訂 DNS 伺服器。

如需有關特定步驟 tooconfigure 您的 DNS 伺服器，請洽詢您的 DNS 伺服器軟體的 hello 文件集。 如需有關如何 hello 步驟尋找 tooconfigure__條件轉寄站__。

條件式轉寄只會轉寄特定 DNS 尾碼的要求。 在此情況下，您必須設定的轉寄站來 hello hello 虛擬網路的 DNS 尾碼。 這個後置詞的要求應該轉送 toohello hello 自訂的 DNS 伺服器 IP 位址。 

hello 下列文字是範例 hello 的條件轉寄站組態**繫結**DNS 軟體：

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

如需有關上使用 DNS 資訊**Windows Server 2016**，請參閱 hello[新增 DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone)文件...

一旦您已設定 hello 在內部部署 DNS 伺服器，您可以使用`nslookup`從 hello 在內部部署網路 tooverify 可以解析名稱 hello 虛擬網路中。 下列範例中的 hello 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

這個範例會使用 hello 在內部部署 DNS 伺服器在 196.168.0.4 tooresolve hello hello 自訂的 DNS 伺服器名稱。 取代 hello 在內部部署 DNS 伺服器的其中一個 hello hello IP 位址。 取代 hello `dnsproxy` hello hello 自訂 DNS 伺服器的完整的網域名稱與地址。

## <a name="optional-control-network-traffic"></a>選擇性：控制網路流量

您可以使用網路安全性群組 (NSG) 或使用者定義的路由 (UDR) toocontrol 網路流量。 Nsg 可讓您 toofilter 輸入和輸出流量，及允許或拒絕 hello 流量。 UDRs toocontrol 流量 hello 虛擬網路中的資源之間流動的方式可讓您、 hello 網際網路和 hello 與內部網路。

> [!WARNING]
> HDInsight 需要來自特定 IP 位址在 hello Azure 雲端中，輸入的存取和不受限制的輸出存取。 當使用 Nsg 或 UDRs toocontrol 流量，您必須執行 hello 下列步驟：
>
> 1. 尋找包含您的虛擬網路的 hello 位置 hello IP 位址。 如需依位置的必要 IP 清單，請參閱[必要的 IP 位址](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip)。
>
> 2. 允許輸入的流量從 hello IP 位址。
>
>    * __NSG__： 允許__輸入__連接埠的流量__443__從 hello__網際網路__。
>    * __UDR__： 集 hello__下個躍點__hello 路由 too__Internet__ 的類型。

如需使用 Azure PowerShell 或 hello Azure CLI toocreate Nsg 的範例，請參閱 hello[擴充 HDInsight 的 Azure 虛擬網路](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg)文件。

## <a name="create-hello-hdinsight-cluster"></a>建立 hello HDInsight 叢集

> [!WARNING]
> 您必須先安裝 HDInsight hello 虛擬網路中設定自訂 DNS 伺服器 hello。

使用 hello 步驟 hello[建立使用 hello Azure 入口網站的 HDInsight 叢集](./hdinsight-hadoop-create-linux-clusters-portal.md)文件 toocreate 的 HDInsight 叢集。

> [!WARNING]
> * 叢集建立期間，您必須選擇包含您的虛擬網路的 hello 位置。
>
> * 在 hello__進階設定__部分的設定，您必須選取 hello 虛擬網路與您稍早建立的子網路。

## <a name="connecting-toohdinsight"></a>連接 tooHDInsight

HDInsight 上的大部分文件假設您有存取 toohello 叢集 hello 透過網際網路。 例如，您可以連接 https://CLUSTERNAME.azurehdinsight.net toohello 叢集。 這個位址會使用 hello 公用閘道，如果您已經使用 Nsg，或從 UDRs toorestrict 存取 hello 網際網路，則無法使用此。

toodirectly tooHDInsight 連接透過 hello 虛擬網路，請使用下列步驟的 hello:

1. toodiscover hello 內部的完整的網域名稱的 hello HDInsight 叢集節點，使用其中一種 hello 下列方法：

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

2. toodetermine hello 可用通訊埠的服務，請參閱 hello [HDInsight 上的 Hadoop 服務所使用的連接埠](./hdinsight-hadoop-port-settings-for-services.md)文件。

    > [!IMPORTANT]
    > 某些 hello 前端節點上裝載的服務才一次一個節點上使用中。 如果您嘗試存取一個前端節點上的服務，它就會失敗，請切換 toohello 其他前端節點。
    >
    > 例如，Ambari 一次只在一個前端節點上作用。 如果您嘗試存取 Ambari 一個前端節點上，它會傳回 404 錯誤，其執行於 hello 其他前端節點。

## <a name="next-steps"></a>後續步驟

* 如需在虛擬網路中使用 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](./hdinsight-extend-hadoop-virtual-network.md)。

* 如需有關 Azure 虛擬網路的詳細資訊，請參閱 hello [Azure 虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。

* 如需網路安全性群組的詳細資訊，請參閱[網路安全性群組](../virtual-network/virtual-networks-nsg.md)。

* 如需使用者定義路由的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。
