---
title: "使用虛擬網路的 Azure HDInsight aaaConnect tooKafka |Microsoft 文件"
description: "了解如何 toodirectly 連接 tooKafka HDInsight 上的透過 Azure 虛擬網路。 了解 tooconnect tooKafka 從開發用戶端使用的 VPN 閘道，或從您內部部署中的用戶端使用的 VPN 閘道裝置的網路。"
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>透過 Azure 虛擬網路連線 tooKafka 上 HDInsight （預覽）

了解如何 toodirectly 連接 tooKafka HDInsight 使用 Azure 虛擬網路上。 本文件提供有關連接 tooKafka 使用 hello 的設定：

* 從內部部署網路的資源。 此連線是使用您區域網路上的 VPN 裝置 (軟體或硬體) 建立的。
* 使用 VPN 軟體用戶端，從開發環境連線。

## <a name="architecture-and-planning"></a>架構與規劃

HDInsight 不允許直接連接 tooKafka hello 透過公用網際網路。 相反地，Kafka 用戶端 （生產者和取用者） 必須使用 hello 下列連線方法的其中一個：

* 執行 hello 用戶端在 hello 與 Kafka HDInsight 上相同虛擬網路。 此設定會用於 hello [Apache Kafka （預覽） 在 HDInsight 上的開頭](hdinsight-apache-kafka-get-started.md)文件。 hello 直接用戶端執行 hello HDInsight 上的叢集節點或另一部虛擬機器上 hello 相同網路。

* 私人網路，例如您在內部部署網路，toohello 虛擬網路連線。 此設定允許用戶端與 Kafka 將內部部署網路 toodirectly 工作。 tooenable 此組態中，執行下列工作的 hello:

    1. 建立虛擬網路。
    2. 建立 VPN 閘道以使用站對站設定。 使用這份文件中的 hello 組態連接 tooa VPN 閘道裝置會在內部部署網路中。
    3. Hello 虛擬網路中建立的 DNS 伺服器。
    4. 設定每個網路中的 hello DNS 伺服器之間的轉送。
    5. 安裝在 HDInsight 上的 Kafka 在 hello 的虛擬網路。

    如需詳細資訊，請參閱 hello[從內部部署網路連接 tooKafka](#on-premises) > 一節。 

* 使用 VPN 閘道與 VPN 用戶端的個別機器 toohello 虛擬網路的連線。 tooenable 此組態中，執行下列工作的 hello:

    1. 建立虛擬網路。
    2. 建立 VPN 閘道以使用點對站設定。 此設定提供可安裝在 Windows 用戶端的 VPN 用戶端。
    3. 安裝在 HDInsight 上的 Kafka 在 hello 的虛擬網路。
    4. 設定 Kafka 進行 IP 公告。 此設定可讓 hello 用戶端 tooconnect 使用 IP 位址而非網域名稱。
    5. 下載並使用 hello VPN 用戶端 hello 開發系統上。

    如需詳細資訊，請參閱 hello[與 VPN 用戶端連接 tooKafka](#vpnclient) > 一節。

    > [!WARNING]
    > 這項設定只建議用於開發用途因為 hello 下列限制：
    >
    > * 每個用戶端必須使用 VPN 軟體用戶端進行連線。 Azure 只會提供以 Windows 為基礎的用戶端。
    > * hello 用戶端未通過名稱解析要求 toohello 虛擬網路，因此您必須使用 IP 位址與 Kafka toocommunicate。 IP 通訊需要 hello Kafka 叢集上的其他組態。

如需在虛擬網路中使用 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](./hdinsight-extend-hadoop-virtual-network.md)。

## <a id="on-premises"></a>從內部部署網路連接 tooKafka

與您的內部部署網路進行通訊的 Kafka 叢集 toocreate hello 中步驟 hello[連接 HDInsight tooyour 在內部部署網路](./connect-on-premises-network.md)文件。

> [!IMPORTANT]
> 當建立 hello HDInsight 叢集，請選取 hello __Kafka__叢集類型。

這些步驟會建立 hello 下列組態：

* Azure 虛擬網路
* 站對站 VPN 閘道
* Azure 儲存體帳戶 (供 HDInsight 使用)
* HDInsight 上的 Kafka

tooverify Kafka 用戶端可以從內部部署，使用 hello 步驟 hello 連接 toohello 叢集[範例： Python 用戶端](#python-client)> 一節。

## <a id="vpnclient"></a>使用 VPN 用戶端連接 tooKafka

使用下列組態的這個區段 toocreate hello 中 hello 步驟：

* Azure 虛擬網路
* 點對站 VPN 閘道
* Azure 儲存體帳戶 (供 HDInsight 使用)
* HDInsight 上的 Kafka

1. Hello 中的 hello 步驟[使用自我簽署憑證來進行點對站連線](../vpn-gateway/vpn-gateway-certificates-point-to-site.md)文件。 這份文件建立 hello hello 閘道所需的憑證。

2. 開啟 PowerShell 命令提示字元，並使用下列程式碼 toolog tooyour Azure 訂用帳戶中的 hello:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. 使用下列程式碼 toocreate 變數包含組態資訊的 hello:

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. 使用 hello 下列程式碼 toocreate hello Azure 資源群組和虛擬網路：

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > 可能需要幾分鐘的時間此程序 toocomplete。

5. 使用下列程式碼 toocreate hello Azure 儲存體帳戶和 blob 容器的 hello:

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. 使用下列程式碼 toocreate hello HDInsight 叢集的 hello:

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > 這個程序需要約 20 分鐘 toocomplete。

8. 使用下列 cmdlet tooretrieve hello URL hello Windows VPN 用戶端 hello 虛擬網路的 hello:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    toodownload hello Windows VPN 用戶端使用 hello 在網頁瀏覽器中傳回 URI。

### <a name="configure-kafka-for-ip-advertising"></a>設定 Kafka 進行 IP 公告

根據預設，動物園管理員會傳回 hello Kafka broker tooclients hello 網域名稱。 此設定不適用於 hello VPN 軟體用戶端，因為它無法使用名稱解析 hello 虛擬網路中的實體。 此設定，請使用下列 hello 步驟 tooconfigure Kafka tooadvertise IP 位址，而不是網域名稱：

1. 使用網頁瀏覽器，移 toohttps://CLUSTERNAME.azurehdinsight.net。 取代__CLUSTERNAME__ hello 的 hello Kafka HDInsight 叢集上的名稱。

    出現提示時，使用 hello 叢集 hello HTTPS 使用者名稱和密碼。 會顯示 hello 叢集 hello Ambari Web UI。

2. tooview 有關 Kafka，選取__Kafka__從 hello hello 左邊的清單。

    ![反白顯示 Kafka 的服務清單](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. tooview Kafka 組態中，選取__Configs__從 hello 正上方。

    ![Kafka 的 Configs (設定) 連結](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. toofind hello __kafka env__組態中，輸入`kafka-env`在 hello__篩選__欄位 hello 右上方。

    ![Kafka 組態，找出 kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. tooconfigure Kafka tooadvertise IP 位址，加入下列文字 toohello 底部 hello hello __kafka env 樣板__欄位：

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. tooconfigure hello 介面 Kafka 接聽時，輸入`listeners`在 hello__篩選__欄位 hello 右上方。

7. 所有網路介面，在 hello 變更 hello 值上 Kafka toolisten tooconfigure__接聽程式__欄位太`PLAINTEXT://0.0.0.0:9092`。

8. toosave hello 組態變更，使用 hello__儲存__ 按鈕。 輸入描述 hello 變更的文字訊息。 選取__確定__一旦 hello 變更尚未儲存。

    ![儲存組態按鈕](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. tooprevent 錯誤 Kafka，重新啟動時使用 hello__服務動作__按鈕，然後選取__上維護模式開啟__。 選取 [確定] toocomplete 這項作業。

    ![服務動作，反白顯示開啟維護](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka，使用 hello__重新啟動__按鈕，然後選取__重新啟動所有受影響__。 確認 hello 重新啟動，然後再使用 hello__確定__按鈕 hello 作業完成後。

    ![重新啟動按鈕，反白顯示重新啟動所有受影響項目](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. toodisable 維護模式，使用 hello__服務動作__按鈕，然後選取__啟動維護模式__。 選取**確定**toocomplete 這項作業。

### <a name="connect-toohello-vpn-gateway"></a>連線 toohello VPN 閘道

從 tooconnect toohello VPN 閘道__Windows 用戶端__，使用 hello__連接 tooAzure__區段 hello[設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate)文件。

## <a id="python-client"></a> 範例：Python 用戶端

toovalidate 連線 tooKafka，使用下列步驟 toocreate hello，並執行 Python 生產者和取用者：

1. 使用其中一個 hello 完全遵循方法 tooretrieve hello 完整網域名稱 (FQDN) 和 hello 節點在 hello Kafka 叢集 IP 位址：

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

    此指令碼假設`$resourceGroupName`hello hello Azure 資源群組含有 hello 虛擬網路名稱。

    儲存 hello hello 下一個步驟中傳回資訊以供使用。

2. 使用 hello 遵循 tooinstall hello [kafka python](http://kafka-python.readthedocs.io/)用戶端：

        pip install kafka-python

3. 下列 Python 程式碼使用 hello toosend 資料 tooKafka:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    取代 hello`'kafka_broker'`傳回步驟 1，這一節中的 hello 位址的項目：

    * 如果您使用__軟體 VPN 用戶端__，取代 hello `kafka_broker` hello IP 位址的背景工作角色節點的項目。

    * 如果您有__啟用透過自訂的 DNS 伺服器的名稱解析__，取代 hello `kafka_broker` hello hello 背景工作角色節點的 FQDN 的項目。

    > [!NOTE]
    > 此程式碼會傳送 hello 字串`test message`toohello 主題`testtopic`。 HDInsight 上 Kafka hello 預設設定是 toocreate hello 主題，如果不存在。

4. 從 Kafka，tooretrieve hello 訊息，使用下列 Python 程式碼的 hello:

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    取代 hello`'kafka_broker'`傳回步驟 1，這一節中的 hello 位址的項目：

    * 如果您使用__軟體 VPN 用戶端__，取代 hello `kafka_broker` hello IP 位址的背景工作角色節點的項目。

    * 如果您有__啟用透過自訂的 DNS 伺服器的名稱解析__，取代 hello `kafka_broker` hello hello 背景工作角色節點的 FQDN 的項目。

## <a name="next-steps"></a>後續步驟

如需有關使用 HDInsight 與虛擬網路的詳細資訊，請參閱 hello[擴充 Azure HDInsight 的 Azure 虛擬網路](hdinsight-extend-hadoop-virtual-network.md)文件。

如需使用點對站 VPN 閘道建立 Azure 虛擬網路的詳細資訊，請參閱下列文件的 hello:

* [設定點對站連線使用 hello Azure 入口網站](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [使用 Azure PowerShell 設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

與 HDInsight 上 Kafka 需使用詳細資訊，請參閱下列文件的 hello:

* [開始使用 HDInsight 上的 Kafka](hdinsight-apache-kafka-get-started.md)
* [對 HDInsight 上的 Kafka 使用鏡像](hdinsight-apache-kafka-mirroring.md)
