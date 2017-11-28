---
title: "使用虛擬網路連線到 Kafka - Azure HDInsight | Microsoft Docs"
description: "了解如何透過 Azure 虛擬網路，直接連線到 HDInsight 上的 Kafka。 了解如何使用 VPN 閘道從開發用戶端連線到 Kafka，或使用 VPN 閘道裝置從內部部署網路的用戶端進行連線。"
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="10625-104">透過 Azure 虛擬網路連線到 HDInsight (預覽版) 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="10625-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="10625-105">了解如何使用 Azure 虛擬網路直接連線到 HDInsight 上的 Kafka。</span><span class="sxs-lookup"><span data-stu-id="10625-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="10625-106">本文件提供使用下列設定連線到 Kafka 的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="10625-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="10625-107">從內部部署網路的資源。</span><span class="sxs-lookup"><span data-stu-id="10625-107">From resources in an on-premises network.</span></span> <span data-ttu-id="10625-108">此連線是使用您區域網路上的 VPN 裝置 (軟體或硬體) 建立的。</span><span class="sxs-lookup"><span data-stu-id="10625-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="10625-109">使用 VPN 軟體用戶端，從開發環境連線。</span><span class="sxs-lookup"><span data-stu-id="10625-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="10625-110">架構與規劃</span><span class="sxs-lookup"><span data-stu-id="10625-110">Architecture and planning</span></span>

<span data-ttu-id="10625-111">HDInsight 不允許透過公用網際網路直接連線至 Kafka。</span><span class="sxs-lookup"><span data-stu-id="10625-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="10625-112">Kafka 用戶端 (生產者和取用者) 必須改用下列其中一個連線方法：</span><span class="sxs-lookup"><span data-stu-id="10625-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="10625-113">在與 HDInsight 上之 Kafka 相同的虛擬網路中執行用戶端。</span><span class="sxs-lookup"><span data-stu-id="10625-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="10625-114">[開始在 HDInsight 上使用 Apache Kafka (預覽)](hdinsight-apache-kafka-get-started.md) 文件中使用的就是此設定。</span><span class="sxs-lookup"><span data-stu-id="10625-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="10625-115">用戶端會直接在 HDInsight 叢集節點或相同網路中的另一部虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="10625-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="10625-116">將私人網路 (例如，您的內部部署網路) 連線至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="10625-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="10625-117">此設定可讓您內部部署網路中的用戶端直接使用 Kafka。</span><span class="sxs-lookup"><span data-stu-id="10625-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="10625-118">若要啟用此設定，請執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="10625-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="10625-119">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="10625-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="10625-120">建立 VPN 閘道以使用站對站設定。</span><span class="sxs-lookup"><span data-stu-id="10625-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="10625-121">本文件中使用的設定會連線到內部部署網路中的 VPN 閘道裝置。</span><span class="sxs-lookup"><span data-stu-id="10625-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="10625-122">在虛擬網路中建立 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="10625-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="10625-123">設定每個網路中 DNS 伺服器之間的轉送。</span><span class="sxs-lookup"><span data-stu-id="10625-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="10625-124">將 HDInsight 上的 Kafka 安裝到虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="10625-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="10625-125">如需詳細資訊，請參閱[從內部部署網路連線至 Kafka](#on-premises) 一節。</span><span class="sxs-lookup"><span data-stu-id="10625-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="10625-126">使用 VPN 閘道與 VPN 用戶端，將個別機器連線至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="10625-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="10625-127">若要啟用此設定，請執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="10625-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="10625-128">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="10625-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="10625-129">建立 VPN 閘道以使用點對站設定。</span><span class="sxs-lookup"><span data-stu-id="10625-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="10625-130">此設定提供可安裝在 Windows 用戶端的 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="10625-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="10625-131">將 HDInsight 上的 Kafka 安裝到虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="10625-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="10625-132">設定 Kafka 進行 IP 公告。</span><span class="sxs-lookup"><span data-stu-id="10625-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="10625-133">此設定可讓用戶端使用 IP 位址而不是網域名稱來連線。</span><span class="sxs-lookup"><span data-stu-id="10625-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="10625-134">下載 VPN 用戶端並在開發系統上使用。</span><span class="sxs-lookup"><span data-stu-id="10625-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="10625-135">如需詳細資訊，請參閱[將 VPN 用戶端連線到 Kafka](#vpnclient) 一節。</span><span class="sxs-lookup"><span data-stu-id="10625-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="10625-136">基於下列限制，建議僅將此設定用於開發用途：</span><span class="sxs-lookup"><span data-stu-id="10625-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="10625-137">每個用戶端必須使用 VPN 軟體用戶端進行連線。</span><span class="sxs-lookup"><span data-stu-id="10625-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="10625-138">Azure 只會提供以 Windows 為基礎的用戶端。</span><span class="sxs-lookup"><span data-stu-id="10625-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="10625-139">用戶端不會將名稱解析要求傳遞至虛擬網路，因此您必須使用 IP 位址來與 Kafka 通訊。</span><span class="sxs-lookup"><span data-stu-id="10625-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="10625-140">IP 通訊需要 Kafka 叢集上的其他設定。</span><span class="sxs-lookup"><span data-stu-id="10625-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="10625-141">如需在虛擬網路中使用 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](./hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="10625-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="10625-142"><a id="on-premises"></a> 從內部部署網路連線到 Kafka</span><span class="sxs-lookup"><span data-stu-id="10625-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="10625-143">若要建立 Kafka 叢集來與內部部署網路通訊，請遵循[將 HDInsight 連線至內部部署網路](./connect-on-premises-network.md)文件中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="10625-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10625-144">建立 HDInsight 叢集時，請選取 __Kafka__ 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="10625-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="10625-145">這些步驟會建立下列設定：</span><span class="sxs-lookup"><span data-stu-id="10625-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="10625-146">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="10625-146">Azure Virtual Network</span></span>
* <span data-ttu-id="10625-147">站對站 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="10625-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="10625-148">Azure 儲存體帳戶 (供 HDInsight 使用)</span><span class="sxs-lookup"><span data-stu-id="10625-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="10625-149">HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="10625-149">Kafka on HDInsight</span></span>

<span data-ttu-id="10625-150">若要確認 Kafka 用戶端可以從內部部署連線到叢集，請使用[範例：Python 用戶端](#python-client)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="10625-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="10625-151"><a id="vpnclient"></a> 使用 VPN 用戶端連線到 Kafka</span><span class="sxs-lookup"><span data-stu-id="10625-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="10625-152">使用本節中的步驟來建立下列設定：</span><span class="sxs-lookup"><span data-stu-id="10625-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="10625-153">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="10625-153">Azure Virtual Network</span></span>
* <span data-ttu-id="10625-154">點對站 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="10625-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="10625-155">Azure 儲存體帳戶 (供 HDInsight 使用)</span><span class="sxs-lookup"><span data-stu-id="10625-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="10625-156">HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="10625-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="10625-157">遵循[使用點對站連線的自我簽署憑證](../vpn-gateway/vpn-gateway-certificates-point-to-site.md)文件中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="10625-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="10625-158">這份文件會建立閘道所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="10625-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="10625-159">開啟 PowerShell 提示字元，並使用下列程式碼來登入您的 Azure 訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="10625-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="10625-160">使用下列程式碼來建立包含組態資訊的變數︰</span><span class="sxs-lookup"><span data-stu-id="10625-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="10625-161">使用下列程式碼來建立 Azure 資源群組和虛擬網路︰</span><span class="sxs-lookup"><span data-stu-id="10625-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="10625-162">此程序可能需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="10625-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="10625-163">使用下列程式碼來建立 Azure 儲存體帳戶和 Blob 容器：</span><span class="sxs-lookup"><span data-stu-id="10625-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="10625-164">使用下列程式碼來建立 HDInsight 叢集︰</span><span class="sxs-lookup"><span data-stu-id="10625-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="10625-165">此程序大約需要 20 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="10625-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="10625-166">使用下列 Cmdlet 來擷取虛擬網路之 Windows VPN 用戶端的 URL：</span><span class="sxs-lookup"><span data-stu-id="10625-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="10625-167">若要下載 Windows VPN 用戶端，請使用網頁瀏覽器中傳回的 URI。</span><span class="sxs-lookup"><span data-stu-id="10625-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="10625-168">設定 Kafka 進行 IP 公告</span><span class="sxs-lookup"><span data-stu-id="10625-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="10625-169">Zookeeper 預設會將 Kafka 代理程式的網域名稱傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="10625-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="10625-170">這個設定不會使用 VPN 軟體用戶端，因為它無法為虛擬網路中的實體使用名稱解析。</span><span class="sxs-lookup"><span data-stu-id="10625-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="10625-171">針對此設定，使用下列步驟來設定 Kafka 以公告 IP 位址而不是網域名稱：</span><span class="sxs-lookup"><span data-stu-id="10625-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="10625-172">使用網頁瀏覽器移至 https://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="10625-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="10625-173">將 __CLUSTERNAME__ 取代為 HDInsight 叢集上 Kafka 的名稱。</span><span class="sxs-lookup"><span data-stu-id="10625-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="10625-174">出現提示時，請使用叢集的 HTTPS 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="10625-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="10625-175">此時會顯示叢集的 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="10625-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="10625-176">若要檢視 Kafka 上的資訊，請從左邊的清單選取 [Kafka]。</span><span class="sxs-lookup"><span data-stu-id="10625-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![反白顯示 Kafka 的服務清單](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="10625-178">若要檢視 Kafka 組態，請從正上方選取 [Configs (設定)]。</span><span class="sxs-lookup"><span data-stu-id="10625-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Kafka 的 Configs (設定) 連結](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="10625-180">若要找出 __kafka-env__ 組態，請在右上角的 [Filter (篩選)] 欄位中輸入 `kafka-env`。</span><span class="sxs-lookup"><span data-stu-id="10625-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Kafka 組態，找出 kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="10625-182">若要設定 Kafka 公告 IP 位址，請在 [kafka-env-template] 欄位的底部加入下列文字︰</span><span class="sxs-lookup"><span data-stu-id="10625-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="10625-183">若要設定 Kafka 接聽的介面，請在右上角的 [Filter (篩選)] 欄位中輸入 `listeners`。</span><span class="sxs-lookup"><span data-stu-id="10625-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="10625-184">若要設定 Kafka 在所有網路介面上接聽，請將 [listeners (接聽程式)] 欄位的值變更為 `PLAINTEXT://0.0.0.0:9092`。</span><span class="sxs-lookup"><span data-stu-id="10625-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="10625-185">若要儲存組態變更，請使用 [Save (儲存)] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10625-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="10625-186">輸入描述變更的文字訊息。</span><span class="sxs-lookup"><span data-stu-id="10625-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="10625-187">儲存變更後，請選取 [OK (確定)]。</span><span class="sxs-lookup"><span data-stu-id="10625-187">Select __OK__ once the changes have been saved.</span></span>

    ![儲存組態按鈕](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="10625-189">若要避免重新啟動 Kafka 時發生錯誤，請使用 [Service Actions (服務動作)] 按鈕，然後選取 [Turn On Maintenance Mode (開啟維護模式)]。</span><span class="sxs-lookup"><span data-stu-id="10625-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="10625-190">選取 [OK (確定)] 以完成此作業。</span><span class="sxs-lookup"><span data-stu-id="10625-190">Select OK to complete this operation.</span></span>

    ![服務動作，反白顯示開啟維護](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="10625-192">若要重新啟動 Kafka，請使用 [Restart (重新啟動)] 按鈕，然後選取 [Restart All Affected (重新啟動所有受影響項目)]。</span><span class="sxs-lookup"><span data-stu-id="10625-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="10625-193">確認重新啟動，然後在作業完成之後使用 [OK (確定)] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10625-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![重新啟動按鈕，反白顯示重新啟動所有受影響項目](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="10625-195">若要停用維護模式，請使用 [Service Actions (服務動作)] 按鈕，然後選取 [Turn Off Maintenance Mode (關閉維護模式)]。</span><span class="sxs-lookup"><span data-stu-id="10625-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="10625-196">選取 [OK (確定)] 以完成此作業。</span><span class="sxs-lookup"><span data-stu-id="10625-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="10625-197">連線到 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="10625-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="10625-198">若要從 __Windows 用戶端__連線到 VPN 閘道，請使用[設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate)文件的＜連線到 Azure＞一節。</span><span class="sxs-lookup"><span data-stu-id="10625-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="10625-199"><a id="python-client"></a> 範例：Python 用戶端</span><span class="sxs-lookup"><span data-stu-id="10625-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="10625-200">若要驗證 Kafka 的連接能力，請使用下列步驟來建立和執行 Python 生產者和取用者：</span><span class="sxs-lookup"><span data-stu-id="10625-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="10625-201">使用下列其中一個方法來擷取 Kafka 叢集中節點的完整網域名稱 (FQDN) 與 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="10625-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="10625-202">這個指令碼假設 `$resourceGroupName` 是包含虛擬網路的 Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="10625-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="10625-203">儲存所傳回的資訊，以便在後續步驟中使用。</span><span class="sxs-lookup"><span data-stu-id="10625-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="10625-204">使用下列命令來安裝 [kafka-python](http://kafka-python.readthedocs.io/) 用戶端︰</span><span class="sxs-lookup"><span data-stu-id="10625-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="10625-205">若要將資料傳送至 Kafka，請使用下列 Python 程式碼︰</span><span class="sxs-lookup"><span data-stu-id="10625-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="10625-206">使用從本節的步驟 1 傳回的位址來取代 `'kafka_broker'` 項目：</span><span class="sxs-lookup"><span data-stu-id="10625-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="10625-207">如果您使用__軟體 VPN 用戶端__，使用背景工作節點的 IP 位址來取代 `kafka_broker` 項目。</span><span class="sxs-lookup"><span data-stu-id="10625-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="10625-208">如果您具有__透過自訂 DNS 伺服器啟用的名稱解析__，使用背景工作節點的 FQDN 來取代 `kafka_broker` 項目。</span><span class="sxs-lookup"><span data-stu-id="10625-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10625-209">此程式碼會將 `test message` 字串傳送至 `testtopic` 主題。</span><span class="sxs-lookup"><span data-stu-id="10625-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="10625-210">HDInsight 上 Kafka 的預設組態是建立主題 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="10625-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="10625-211">若要從 Kafka 擷取訊息，請使用下列 Python 程式碼︰</span><span class="sxs-lookup"><span data-stu-id="10625-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="10625-212">使用從本節的步驟 1 傳回的位址來取代 `'kafka_broker'` 項目：</span><span class="sxs-lookup"><span data-stu-id="10625-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="10625-213">如果您使用__軟體 VPN 用戶端__，使用背景工作節點的 IP 位址來取代 `kafka_broker` 項目。</span><span class="sxs-lookup"><span data-stu-id="10625-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="10625-214">如果您具有__透過自訂 DNS 伺服器啟用的名稱解析__，使用背景工作節點的 FQDN 來取代 `kafka_broker` 項目。</span><span class="sxs-lookup"><span data-stu-id="10625-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10625-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10625-215">Next steps</span></span>

<span data-ttu-id="10625-216">如需使用 HDInsight 搭配虛擬網路的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 Azure HDInsight](hdinsight-extend-hadoop-virtual-network.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="10625-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="10625-217">如需如何建立具點對站 VPN 閘道之 Azure 虛擬網路的詳細資訊，請參閱下列文件︰</span><span class="sxs-lookup"><span data-stu-id="10625-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="10625-218">使用 Azure 入口網站設定點對站連線</span><span class="sxs-lookup"><span data-stu-id="10625-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="10625-219">使用 Azure PowerShell 設定點對站連線</span><span class="sxs-lookup"><span data-stu-id="10625-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="10625-220">如需使用 HDInsight 上 Kafka 的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="10625-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="10625-221">開始使用 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="10625-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="10625-222">對 HDInsight 上的 Kafka 使用鏡像</span><span class="sxs-lookup"><span data-stu-id="10625-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
