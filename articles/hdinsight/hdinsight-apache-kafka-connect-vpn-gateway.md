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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="b48fd-104">透過 Azure 虛擬網路連線 tooKafka 上 HDInsight （預覽）</span><span class="sxs-lookup"><span data-stu-id="b48fd-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="b48fd-105">了解如何 toodirectly 連接 tooKafka HDInsight 使用 Azure 虛擬網路上。</span><span class="sxs-lookup"><span data-stu-id="b48fd-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="b48fd-106">本文件提供有關連接 tooKafka 使用 hello 的設定：</span><span class="sxs-lookup"><span data-stu-id="b48fd-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="b48fd-107">從內部部署網路的資源。</span><span class="sxs-lookup"><span data-stu-id="b48fd-107">From resources in an on-premises network.</span></span> <span data-ttu-id="b48fd-108">此連線是使用您區域網路上的 VPN 裝置 (軟體或硬體) 建立的。</span><span class="sxs-lookup"><span data-stu-id="b48fd-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="b48fd-109">使用 VPN 軟體用戶端，從開發環境連線。</span><span class="sxs-lookup"><span data-stu-id="b48fd-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="b48fd-110">架構與規劃</span><span class="sxs-lookup"><span data-stu-id="b48fd-110">Architecture and planning</span></span>

<span data-ttu-id="b48fd-111">HDInsight 不允許直接連接 tooKafka hello 透過公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="b48fd-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="b48fd-112">相反地，Kafka 用戶端 （生產者和取用者） 必須使用 hello 下列連線方法的其中一個：</span><span class="sxs-lookup"><span data-stu-id="b48fd-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="b48fd-113">執行 hello 用戶端在 hello 與 Kafka HDInsight 上相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b48fd-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="b48fd-114">此設定會用於 hello [Apache Kafka （預覽） 在 HDInsight 上的開頭](hdinsight-apache-kafka-get-started.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b48fd-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="b48fd-115">hello 直接用戶端執行 hello HDInsight 上的叢集節點或另一部虛擬機器上 hello 相同網路。</span><span class="sxs-lookup"><span data-stu-id="b48fd-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="b48fd-116">私人網路，例如您在內部部署網路，toohello 虛擬網路連線。</span><span class="sxs-lookup"><span data-stu-id="b48fd-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="b48fd-117">此設定允許用戶端與 Kafka 將內部部署網路 toodirectly 工作。</span><span class="sxs-lookup"><span data-stu-id="b48fd-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="b48fd-118">tooenable 此組態中，執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="b48fd-119">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b48fd-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="b48fd-120">建立 VPN 閘道以使用站對站設定。</span><span class="sxs-lookup"><span data-stu-id="b48fd-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="b48fd-121">使用這份文件中的 hello 組態連接 tooa VPN 閘道裝置會在內部部署網路中。</span><span class="sxs-lookup"><span data-stu-id="b48fd-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="b48fd-122">Hello 虛擬網路中建立的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b48fd-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="b48fd-123">設定每個網路中的 hello DNS 伺服器之間的轉送。</span><span class="sxs-lookup"><span data-stu-id="b48fd-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="b48fd-124">安裝在 HDInsight 上的 Kafka 在 hello 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b48fd-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="b48fd-125">如需詳細資訊，請參閱 hello[從內部部署網路連接 tooKafka](#on-premises) > 一節。</span><span class="sxs-lookup"><span data-stu-id="b48fd-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="b48fd-126">使用 VPN 閘道與 VPN 用戶端的個別機器 toohello 虛擬網路的連線。</span><span class="sxs-lookup"><span data-stu-id="b48fd-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="b48fd-127">tooenable 此組態中，執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="b48fd-128">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b48fd-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="b48fd-129">建立 VPN 閘道以使用點對站設定。</span><span class="sxs-lookup"><span data-stu-id="b48fd-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="b48fd-130">此設定提供可安裝在 Windows 用戶端的 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b48fd-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="b48fd-131">安裝在 HDInsight 上的 Kafka 在 hello 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b48fd-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="b48fd-132">設定 Kafka 進行 IP 公告。</span><span class="sxs-lookup"><span data-stu-id="b48fd-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="b48fd-133">此設定可讓 hello 用戶端 tooconnect 使用 IP 位址而非網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b48fd-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="b48fd-134">下載並使用 hello VPN 用戶端 hello 開發系統上。</span><span class="sxs-lookup"><span data-stu-id="b48fd-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="b48fd-135">如需詳細資訊，請參閱 hello[與 VPN 用戶端連接 tooKafka](#vpnclient) > 一節。</span><span class="sxs-lookup"><span data-stu-id="b48fd-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b48fd-136">這項設定只建議用於開發用途因為 hello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="b48fd-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="b48fd-137">每個用戶端必須使用 VPN 軟體用戶端進行連線。</span><span class="sxs-lookup"><span data-stu-id="b48fd-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="b48fd-138">Azure 只會提供以 Windows 為基礎的用戶端。</span><span class="sxs-lookup"><span data-stu-id="b48fd-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="b48fd-139">hello 用戶端未通過名稱解析要求 toohello 虛擬網路，因此您必須使用 IP 位址與 Kafka toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="b48fd-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="b48fd-140">IP 通訊需要 hello Kafka 叢集上的其他組態。</span><span class="sxs-lookup"><span data-stu-id="b48fd-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="b48fd-141">如需在虛擬網路中使用 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](./hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="b48fd-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="b48fd-142"><a id="on-premises"></a>從內部部署網路連接 tooKafka</span><span class="sxs-lookup"><span data-stu-id="b48fd-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="b48fd-143">與您的內部部署網路進行通訊的 Kafka 叢集 toocreate hello 中步驟 hello[連接 HDInsight tooyour 在內部部署網路](./connect-on-premises-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b48fd-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b48fd-144">當建立 hello HDInsight 叢集，請選取 hello __Kafka__叢集類型。</span><span class="sxs-lookup"><span data-stu-id="b48fd-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="b48fd-145">這些步驟會建立 hello 下列組態：</span><span class="sxs-lookup"><span data-stu-id="b48fd-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="b48fd-146">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b48fd-146">Azure Virtual Network</span></span>
* <span data-ttu-id="b48fd-147">站對站 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="b48fd-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="b48fd-148">Azure 儲存體帳戶 (供 HDInsight 使用)</span><span class="sxs-lookup"><span data-stu-id="b48fd-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="b48fd-149">HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="b48fd-149">Kafka on HDInsight</span></span>

<span data-ttu-id="b48fd-150">tooverify Kafka 用戶端可以從內部部署，使用 hello 步驟 hello 連接 toohello 叢集[範例： Python 用戶端](#python-client)> 一節。</span><span class="sxs-lookup"><span data-stu-id="b48fd-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="b48fd-151"><a id="vpnclient"></a>使用 VPN 用戶端連接 tooKafka</span><span class="sxs-lookup"><span data-stu-id="b48fd-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="b48fd-152">使用下列組態的這個區段 toocreate hello 中 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="b48fd-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="b48fd-153">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b48fd-153">Azure Virtual Network</span></span>
* <span data-ttu-id="b48fd-154">點對站 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="b48fd-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="b48fd-155">Azure 儲存體帳戶 (供 HDInsight 使用)</span><span class="sxs-lookup"><span data-stu-id="b48fd-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="b48fd-156">HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="b48fd-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="b48fd-157">Hello 中的 hello 步驟[使用自我簽署憑證來進行點對站連線](../vpn-gateway/vpn-gateway-certificates-point-to-site.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b48fd-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="b48fd-158">這份文件建立 hello hello 閘道所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="b48fd-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="b48fd-159">開啟 PowerShell 命令提示字元，並使用下列程式碼 toolog tooyour Azure 訂用帳戶中的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="b48fd-160">使用下列程式碼 toocreate 變數包含組態資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-160">Use hello following code toocreate variables that contain configuration information:</span></span>

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

4. <span data-ttu-id="b48fd-161">使用 hello 下列程式碼 toocreate hello Azure 資源群組和虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="b48fd-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

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
    > <span data-ttu-id="b48fd-162">可能需要幾分鐘的時間此程序 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b48fd-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="b48fd-163">使用下列程式碼 toocreate hello Azure 儲存體帳戶和 blob 容器的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

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

6. <span data-ttu-id="b48fd-164">使用下列程式碼 toocreate hello HDInsight 叢集的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

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
  > <span data-ttu-id="b48fd-165">這個程序需要約 20 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b48fd-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="b48fd-166">使用下列 cmdlet tooretrieve hello URL hello Windows VPN 用戶端 hello 虛擬網路的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="b48fd-167">toodownload hello Windows VPN 用戶端使用 hello 在網頁瀏覽器中傳回 URI。</span><span class="sxs-lookup"><span data-stu-id="b48fd-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="b48fd-168">設定 Kafka 進行 IP 公告</span><span class="sxs-lookup"><span data-stu-id="b48fd-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="b48fd-169">根據預設，動物園管理員會傳回 hello Kafka broker tooclients hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b48fd-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="b48fd-170">此設定不適用於 hello VPN 軟體用戶端，因為它無法使用名稱解析 hello 虛擬網路中的實體。</span><span class="sxs-lookup"><span data-stu-id="b48fd-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="b48fd-171">此設定，請使用下列 hello 步驟 tooconfigure Kafka tooadvertise IP 位址，而不是網域名稱：</span><span class="sxs-lookup"><span data-stu-id="b48fd-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="b48fd-172">使用網頁瀏覽器，移 toohttps://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="b48fd-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="b48fd-173">取代__CLUSTERNAME__ hello 的 hello Kafka HDInsight 叢集上的名稱。</span><span class="sxs-lookup"><span data-stu-id="b48fd-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="b48fd-174">出現提示時，使用 hello 叢集 hello HTTPS 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b48fd-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="b48fd-175">會顯示 hello 叢集 hello Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="b48fd-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="b48fd-176">tooview 有關 Kafka，選取__Kafka__從 hello hello 左邊的清單。</span><span class="sxs-lookup"><span data-stu-id="b48fd-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![反白顯示 Kafka 的服務清單](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="b48fd-178">tooview Kafka 組態中，選取__Configs__從 hello 正上方。</span><span class="sxs-lookup"><span data-stu-id="b48fd-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Kafka 的 Configs (設定) 連結](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="b48fd-180">toofind hello __kafka env__組態中，輸入`kafka-env`在 hello__篩選__欄位 hello 右上方。</span><span class="sxs-lookup"><span data-stu-id="b48fd-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Kafka 組態，找出 kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="b48fd-182">tooconfigure Kafka tooadvertise IP 位址，加入下列文字 toohello 底部 hello hello __kafka env 樣板__欄位：</span><span class="sxs-lookup"><span data-stu-id="b48fd-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="b48fd-183">tooconfigure hello 介面 Kafka 接聽時，輸入`listeners`在 hello__篩選__欄位 hello 右上方。</span><span class="sxs-lookup"><span data-stu-id="b48fd-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="b48fd-184">所有網路介面，在 hello 變更 hello 值上 Kafka toolisten tooconfigure__接聽程式__欄位太`PLAINTEXT://0.0.0.0:9092`。</span><span class="sxs-lookup"><span data-stu-id="b48fd-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="b48fd-185">toosave hello 組態變更，使用 hello__儲存__ 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b48fd-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="b48fd-186">輸入描述 hello 變更的文字訊息。</span><span class="sxs-lookup"><span data-stu-id="b48fd-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="b48fd-187">選取__確定__一旦 hello 變更尚未儲存。</span><span class="sxs-lookup"><span data-stu-id="b48fd-187">Select __OK__ once hello changes have been saved.</span></span>

    ![儲存組態按鈕](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="b48fd-189">tooprevent 錯誤 Kafka，重新啟動時使用 hello__服務動作__按鈕，然後選取__上維護模式開啟__。</span><span class="sxs-lookup"><span data-stu-id="b48fd-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="b48fd-190">選取 [確定] toocomplete 這項作業。</span><span class="sxs-lookup"><span data-stu-id="b48fd-190">Select OK toocomplete this operation.</span></span>

    ![服務動作，反白顯示開啟維護](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="b48fd-192">toorestart Kafka，使用 hello__重新啟動__按鈕，然後選取__重新啟動所有受影響__。</span><span class="sxs-lookup"><span data-stu-id="b48fd-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="b48fd-193">確認 hello 重新啟動，然後再使用 hello__確定__按鈕 hello 作業完成後。</span><span class="sxs-lookup"><span data-stu-id="b48fd-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![重新啟動按鈕，反白顯示重新啟動所有受影響項目](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="b48fd-195">toodisable 維護模式，使用 hello__服務動作__按鈕，然後選取__啟動維護模式__。</span><span class="sxs-lookup"><span data-stu-id="b48fd-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="b48fd-196">選取**確定**toocomplete 這項作業。</span><span class="sxs-lookup"><span data-stu-id="b48fd-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="b48fd-197">連線 toohello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="b48fd-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="b48fd-198">從 tooconnect toohello VPN 閘道__Windows 用戶端__，使用 hello__連接 tooAzure__區段 hello[設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate)文件。</span><span class="sxs-lookup"><span data-stu-id="b48fd-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="b48fd-199"><a id="python-client"></a> 範例：Python 用戶端</span><span class="sxs-lookup"><span data-stu-id="b48fd-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="b48fd-200">toovalidate 連線 tooKafka，使用下列步驟 toocreate hello，並執行 Python 生產者和取用者：</span><span class="sxs-lookup"><span data-stu-id="b48fd-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="b48fd-201">使用其中一個 hello 完全遵循方法 tooretrieve hello 完整網域名稱 (FQDN) 和 hello 節點在 hello Kafka 叢集 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="b48fd-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="b48fd-202">此指令碼假設`$resourceGroupName`hello hello Azure 資源群組含有 hello 虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="b48fd-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="b48fd-203">儲存 hello hello 下一個步驟中傳回資訊以供使用。</span><span class="sxs-lookup"><span data-stu-id="b48fd-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="b48fd-204">使用 hello 遵循 tooinstall hello [kafka python](http://kafka-python.readthedocs.io/)用戶端：</span><span class="sxs-lookup"><span data-stu-id="b48fd-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="b48fd-205">下列 Python 程式碼使用 hello toosend 資料 tooKafka:</span><span class="sxs-lookup"><span data-stu-id="b48fd-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="b48fd-206">取代 hello`'kafka_broker'`傳回步驟 1，這一節中的 hello 位址的項目：</span><span class="sxs-lookup"><span data-stu-id="b48fd-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="b48fd-207">如果您使用__軟體 VPN 用戶端__，取代 hello `kafka_broker` hello IP 位址的背景工作角色節點的項目。</span><span class="sxs-lookup"><span data-stu-id="b48fd-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="b48fd-208">如果您有__啟用透過自訂的 DNS 伺服器的名稱解析__，取代 hello `kafka_broker` hello hello 背景工作角色節點的 FQDN 的項目。</span><span class="sxs-lookup"><span data-stu-id="b48fd-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b48fd-209">此程式碼會傳送 hello 字串`test message`toohello 主題`testtopic`。</span><span class="sxs-lookup"><span data-stu-id="b48fd-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="b48fd-210">HDInsight 上 Kafka hello 預設設定是 toocreate hello 主題，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="b48fd-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="b48fd-211">從 Kafka，tooretrieve hello 訊息，使用下列 Python 程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

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

    <span data-ttu-id="b48fd-212">取代 hello`'kafka_broker'`傳回步驟 1，這一節中的 hello 位址的項目：</span><span class="sxs-lookup"><span data-stu-id="b48fd-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="b48fd-213">如果您使用__軟體 VPN 用戶端__，取代 hello `kafka_broker` hello IP 位址的背景工作角色節點的項目。</span><span class="sxs-lookup"><span data-stu-id="b48fd-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="b48fd-214">如果您有__啟用透過自訂的 DNS 伺服器的名稱解析__，取代 hello `kafka_broker` hello hello 背景工作角色節點的 FQDN 的項目。</span><span class="sxs-lookup"><span data-stu-id="b48fd-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b48fd-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b48fd-215">Next steps</span></span>

<span data-ttu-id="b48fd-216">如需有關使用 HDInsight 與虛擬網路的詳細資訊，請參閱 hello[擴充 Azure HDInsight 的 Azure 虛擬網路](hdinsight-extend-hadoop-virtual-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b48fd-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="b48fd-217">如需使用點對站 VPN 閘道建立 Azure 虛擬網路的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="b48fd-218">設定點對站連線使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b48fd-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="b48fd-219">使用 Azure PowerShell 設定點對站連線</span><span class="sxs-lookup"><span data-stu-id="b48fd-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="b48fd-220">與 HDInsight 上 Kafka 需使用詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="b48fd-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="b48fd-221">開始使用 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="b48fd-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="b48fd-222">對 HDInsight 上的 Kafka 使用鏡像</span><span class="sxs-lookup"><span data-stu-id="b48fd-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
