---
title: "將 HDInsight 連線到內部部署網路 - Azure HDInsight | Microsoft Docs"
description: "了解如何在 Azure 虛擬網路中建立 HDInsight 叢集，然後將它連線到您的內部部署網路。 了解如何使用自訂的 DNS 伺服器來設定 HDInsight 與內部部署網路之間的解析名稱。"
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
ms.openlocfilehash: 6fc863010cc59e20e7d86ea9344489e574be75f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-hdinsight-to-your-on-premise-network"></a><span data-ttu-id="97259-104">將 HDInsight 連線至內部部署網</span><span class="sxs-lookup"><span data-stu-id="97259-104">Connect HDInsight to your on-premise network</span></span>

<span data-ttu-id="97259-105">了解如何使用 Azure 虛擬網路和 VPN 閘道，將 HDInsight 連線到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="97259-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="97259-106">本文件提供下列規劃資訊：</span><span class="sxs-lookup"><span data-stu-id="97259-106">This document provides planning information on:</span></span>

* <span data-ttu-id="97259-107">在連線至內部部署網路的 Azure 虛擬網路中使用 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="97259-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="97259-108">設定虛擬網路與內部部署網路之間的 DNS 名稱解析。</span><span class="sxs-lookup"><span data-stu-id="97259-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="97259-109">設定網路安全性群組來限制網際網路存取 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="97259-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="97259-110">HDInsight 在虛擬網路上提供的連接埠。</span><span class="sxs-lookup"><span data-stu-id="97259-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="97259-111">建立虛擬網路設定</span><span class="sxs-lookup"><span data-stu-id="97259-111">Create the Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97259-112">如果您要尋找使用 Azure 虛擬網路將 HDInsight 連線到內部網路的逐步指引，請參閱[將 HDInsight 連線至內部部署網路](connect-on-premises-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="97259-112">If you are looking for step by step guidance on connecting HDInsight to your on-premises network using an Azure Virtual Network, see the [Connect HDInsight to your on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="97259-113">使用下列文件可了解如何建立已連線到內部部署網路的 Azure 虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="97259-113">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="97259-114">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="97259-114">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="97259-115">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="97259-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="97259-116">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="97259-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="97259-117">設定名稱解析</span><span class="sxs-lookup"><span data-stu-id="97259-117">Configure name resolution</span></span>

<span data-ttu-id="97259-118">若要允許聯結網路中的 HDInsight 和資源依名稱進行通訊，您必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="97259-118">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="97259-119">在 Azure 虛擬網路中建立自訂的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97259-119">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="97259-120">將虛擬網路設定為使用自訂的 DNS 伺服器，而不使用預設的 Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="97259-120">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="97259-121">設定自訂的 DNS 伺服器與您的內部部署 DNS 伺服器之間的轉送。</span><span class="sxs-lookup"><span data-stu-id="97259-121">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="97259-122">此設定可啟用下列行為：</span><span class="sxs-lookup"><span data-stu-id="97259-122">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="97259-123">對於完整網域名稱包含__虛擬網路__之 DNS 尾碼的要求會轉寄到自訂的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97259-123">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="97259-124">然後，自訂的 DNS 伺服器會將這些要求轉寄到 Azure 遞迴解析程式，以傳回 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="97259-124">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="97259-125">所有其他要求都會轉寄到內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97259-125">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="97259-126">即使是公用網際網路資源 (例如 microsoft.com) 的要求也會轉寄到內部部署 DNS 伺服器進行名稱解析。</span><span class="sxs-lookup"><span data-stu-id="97259-126">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="97259-127">在下列圖表中，綠線表示的資源要求會以虛擬網路的 DNS 尾碼結尾。</span><span class="sxs-lookup"><span data-stu-id="97259-127">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="97259-128">藍線表示在內部部署網路或公用網際網路上的資源要求。</span><span class="sxs-lookup"><span data-stu-id="97259-128">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![圖表說明如何解決本文件所使用之設定中的 DNS 要求](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="97259-130">建立自訂的 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="97259-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97259-131">您必須先建立和設定 DNS 伺服器，然後再將 HDInsight 安裝到虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="97259-131">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="97259-132">若要建立使用[繫結](https://www.isc.org/downloads/bind/) DNS 軟體的 Linux VM，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97259-132">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="97259-133">下列步驟會使用 [Azure 入口網站](https://portal.azure.com)來建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97259-133">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="97259-134">如需其他建立虛擬機器的方式，請參閱[建立 VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) 和[建立 VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="97259-134">For other ways to create a virtual machine, see the [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="97259-135">從 [Azure 入口網站](https://portal.azure.com)，選取__+__、__Compute__ 和 __Ubuntu Server 16.04 LTS__。</span><span class="sxs-lookup"><span data-stu-id="97259-135">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![建立 Ubuntu 虛擬機器](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="97259-137">從 [基本概念] 區段中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="97259-137">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="97259-138">__名稱__：識別此虛擬機器的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="97259-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="97259-139">例如，__DNSProxy__。</span><span class="sxs-lookup"><span data-stu-id="97259-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="97259-140">__使用者名稱__︰SSH 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="97259-140">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="97259-141">__SSH 公開金鑰__或__密碼__：SSH 帳戶的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="97259-141">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="97259-142">我們建議使用公開金鑰，因為它們較為安全。</span><span class="sxs-lookup"><span data-stu-id="97259-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="97259-143">如需詳細資訊，請參閱[建立及使用適用於 Linux VM 的 SSH 金鑰](../virtual-machines/linux/mac-create-ssh-keys.md)文件。</span><span class="sxs-lookup"><span data-stu-id="97259-143">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="97259-144">__資源群組__：選取 [使用現有]，然後選取包含稍早所建立之虛擬網路的資源群組。</span><span class="sxs-lookup"><span data-stu-id="97259-144">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="97259-145">__位置__：選取與 VM 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="97259-145">__Location__: Select the same location as the virtual network.</span></span>

    ![虛擬機器基本設定](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="97259-147">將其他項目保留在預設值，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="97259-147">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="97259-148">從 [選擇大小] 區段中，選取 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="97259-148">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="97259-149">在本教學課程中，選取最小與最低的成本選項。</span><span class="sxs-lookup"><span data-stu-id="97259-149">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="97259-150">若要繼續，請使用 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="97259-150">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="97259-151">從 [設定] 區段中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="97259-151">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="97259-152">__虛擬網路__：選取您稍早建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="97259-152">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="97259-153">__子網路__：選取虛擬網路的預設子網路。</span><span class="sxs-lookup"><span data-stu-id="97259-153">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="97259-154">請__勿__選取 VPN 閘道使用的子網路。</span><span class="sxs-lookup"><span data-stu-id="97259-154">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="97259-155">__診斷儲存體帳戶__：選取現有的儲存體帳戶或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="97259-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![虛擬網路設定](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="97259-157">將其他項目保留在預設值，然後選取 [確定] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="97259-157">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="97259-158">從 [購買] 區段中，選取 [購買] 按鈕以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97259-158">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="97259-159">一旦建立虛擬機器之後，會顯示其 [概觀] 區段。</span><span class="sxs-lookup"><span data-stu-id="97259-159">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="97259-160">從左側的清單中選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="97259-160">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="97259-161">儲存 [公用 IP 位址] 和 [私人 IP 位址] 的值。</span><span class="sxs-lookup"><span data-stu-id="97259-161">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="97259-162">下一節將使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="97259-162">It will be used in the next section.</span></span>

    ![公用和私人 IP 位址](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="97259-164">安裝並設定 Bind (DNS 軟體)</span><span class="sxs-lookup"><span data-stu-id="97259-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="97259-165">使用 SSH 連線至虛擬機器的__公用 IP 位址__。</span><span class="sxs-lookup"><span data-stu-id="97259-165">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="97259-166">下列範例會連線到 40.68.254.142 的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="97259-166">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="97259-167">將 `sshuser` 取代為建立叢集時所指定的 SSH 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="97259-167">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97259-168">有多種方式可取得 `ssh` 公用程式。</span><span class="sxs-lookup"><span data-stu-id="97259-168">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="97259-169">在 Linux、Unix 及 macOS 上，它會提供作為作業系統的一部分。</span><span class="sxs-lookup"><span data-stu-id="97259-169">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="97259-170">如果您是使用 Windows，請考慮下列選項的其中之一：</span><span class="sxs-lookup"><span data-stu-id="97259-170">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="97259-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="97259-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="97259-172">在 Windows 10 上 Ubuntu 上的 Bash</span><span class="sxs-lookup"><span data-stu-id="97259-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="97259-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="97259-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="97259-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="97259-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="97259-175">若要安裝 Bind，使用下列 SSH 工作階段中的命令：</span><span class="sxs-lookup"><span data-stu-id="97259-175">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="97259-176">若要將 Bind 設定為將名稱解析要求轉寄到您的內部部署 DNS 伺服器，請使用下列文字作為 `/etc/bind/named.conf.options` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="97259-176">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="97259-177">將 `goodclients` 區段中的值取代為虛擬網路與內部部署網路的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="97259-177">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="97259-178">本章節會定義此 DNS 伺服器接受要求的來源位址。</span><span class="sxs-lookup"><span data-stu-id="97259-178">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="97259-179">將 `forwarders` 區段中的 `192.168.0.1` 項目取代為內部部署 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="97259-179">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="97259-180">此項目會將 DNS 要求路由到您的內部部署 DNS 伺服器以進行解析。</span><span class="sxs-lookup"><span data-stu-id="97259-180">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="97259-181">若要編輯這個檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="97259-181">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="97259-182">若要儲存檔案，請使用 __Ctrl+X__、__Y__ 和 __Enter__ 鍵。</span><span class="sxs-lookup"><span data-stu-id="97259-182">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="97259-183">在 SSH 工作階段中，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="97259-183">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="97259-184">此命令會傳回類似下列文字的值：</span><span class="sxs-lookup"><span data-stu-id="97259-184">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="97259-185">`icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` 文字是此虛擬網路的 __DNS 尾碼__。</span><span class="sxs-lookup"><span data-stu-id="97259-185">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="97259-186">儲存這個值以便稍後使用。</span><span class="sxs-lookup"><span data-stu-id="97259-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="97259-187">若要將 Bind 設定為解析虛擬網路內資源的 DNS 名稱，請使用下列文字作為 `/etc/bind/named.conf.local` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="97259-187">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="97259-188">您必須將 `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` 取代為您先前擷取的 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="97259-188">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="97259-189">若要編輯這個檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="97259-189">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="97259-190">若要儲存檔案，請使用 __Ctrl+X__、__Y__ 和 __Enter__ 鍵。</span><span class="sxs-lookup"><span data-stu-id="97259-190">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="97259-191">若要啟動 Bind，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="97259-191">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="97259-192">若要確認該 Bind 可以解析內部部署網路中的資源名稱，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="97259-192">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="97259-193">將 `dns.mynetwork.net` 取代為內部部署網路中的資源完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="97259-193">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="97259-194">將 `10.0.0.4` 取代為虛擬網路中自訂 DNS 伺服器的 __內部 IP 位址__。</span><span class="sxs-lookup"><span data-stu-id="97259-194">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="97259-195">回應看起來類似下列文字：</span><span class="sxs-lookup"><span data-stu-id="97259-195">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="97259-196">將虛擬網路設定為使用自訂的 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="97259-196">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="97259-197">若要將虛擬網路設定為使用自訂的 DNS 伺服器，而不使用 Azure 遞迴解析程式，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97259-197">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="97259-198">在 [Azure 入口網站](https://portal.azure.com)中，選取虛擬網路，然後選取 [DNS 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="97259-198">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="97259-199">選取 [自訂]，並輸入自訂 DNS 伺服器的__內部 IP 位址__。</span><span class="sxs-lookup"><span data-stu-id="97259-199">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="97259-200">最後，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="97259-200">Finally, select __Save__.</span></span>

    ![設定網路的自訂 DNS 伺服器](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="97259-202">設定內部部署 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="97259-202">Configure the on-premises DNS server</span></span>

<span data-ttu-id="97259-203">在上一節中，您已將自訂 DNS 伺服器設定為將要求轉寄到內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97259-203">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="97259-204">接下來，您必須將內部部署 DNS 伺服器設定為將要求轉寄到自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97259-204">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="97259-205">如需有關如何設定您 DNS 伺服器的特定步驟，請參閱您 DNS 伺服器軟體的文件。</span><span class="sxs-lookup"><span data-stu-id="97259-205">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="97259-206">尋找如何設定__條件式轉寄站__的步驟。</span><span class="sxs-lookup"><span data-stu-id="97259-206">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="97259-207">條件式轉寄只會轉寄特定 DNS 尾碼的要求。</span><span class="sxs-lookup"><span data-stu-id="97259-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="97259-208">在此情況下，您必須設定虛擬網路 DNS 尾碼的轉寄站。</span><span class="sxs-lookup"><span data-stu-id="97259-208">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="97259-209">應將這個尾碼的要求轉寄到自訂 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="97259-209">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="97259-210">下列文字是 **Bind** DNS 軟體條件式轉寄站設定的範例：</span><span class="sxs-lookup"><span data-stu-id="97259-210">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="97259-211">如需有關在 **Windows Server 2016** 上使用 DNS 的資訊，請參閱 [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) 文件...</span><span class="sxs-lookup"><span data-stu-id="97259-211">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="97259-212">一旦您設定了內部部署 DNS 伺服器後，就可以從內部部署網路使用 `nslookup`，以確認您可以解析虛擬網路中的名稱。</span><span class="sxs-lookup"><span data-stu-id="97259-212">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="97259-213">下列範例</span><span class="sxs-lookup"><span data-stu-id="97259-213">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="97259-214">這個範例會使用 196.168.0.4 的內部部署 DNS 伺服器來解析自訂 DNS 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="97259-214">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="97259-215">將 IP 位址取代為內部部署 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="97259-215">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="97259-216">將 `dnsproxy` 位址取代為自訂 DNS 伺服器的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="97259-216">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="97259-217">選擇性：控制網路流量</span><span class="sxs-lookup"><span data-stu-id="97259-217">Optional: Control network traffic</span></span>

<span data-ttu-id="97259-218">您可以使用網路安全性群組 (NSG) 或使用者定義路由 (UDR) 來控制網路流量。</span><span class="sxs-lookup"><span data-stu-id="97259-218">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="97259-219">NSG 可讓您篩選輸入和輸出流量，並允許或拒絕流量。</span><span class="sxs-lookup"><span data-stu-id="97259-219">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="97259-220">UDR 可讓您控制虛擬網路、網際網路及內部部署網路的資源之間流量流動的方式。</span><span class="sxs-lookup"><span data-stu-id="97259-220">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="97259-221">HDInsight 需要 Azure 雲端中來自特定 IP 位址的輸入存取，以及不受限制的輸出存取。</span><span class="sxs-lookup"><span data-stu-id="97259-221">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="97259-222">使用 NSG 或 UDR 來控制流量時，您必須執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97259-222">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>
>
> 1. <span data-ttu-id="97259-223">尋找包含您虛擬網路之位置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="97259-223">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="97259-224">如需依位置的必要 IP 清單，請參閱[必要的 IP 位址](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip)。</span><span class="sxs-lookup"><span data-stu-id="97259-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="97259-225">允許來自 IP 位址的輸入流量。</span><span class="sxs-lookup"><span data-stu-id="97259-225">Allow inbound traffic from the IP addresses.</span></span>
>
>    * <span data-ttu-id="97259-226">__NSG__：允許來自__網際網路__之連接埠 __443__ 上的__輸入__流量。</span><span class="sxs-lookup"><span data-stu-id="97259-226">__NSG__: Allow __inbound__ traffic on port __443__ from the __Internet__.</span></span>
>    * <span data-ttu-id="97259-227">__UDR__：將路由的__下個躍點__類型設定為__網際網路__。</span><span class="sxs-lookup"><span data-stu-id="97259-227">__UDR__: Set the __Next Hop__ type of the route to __Internet__.</span></span>

<span data-ttu-id="97259-228">如需使用 Azure PowerShell 或 Azure CLI 建立 NSG 的範例，請參閱[使用 Azure 虛擬網路擴充 HDInsight](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) 文件。</span><span class="sxs-lookup"><span data-stu-id="97259-228">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="97259-229">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="97259-229">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="97259-230">您必須先設定自訂 DNS 伺服器，然後再將 HDInsight 安裝到虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="97259-230">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="97259-231">使用[使用 Azure 入口網站建立 HDInsight 叢集](./hdinsight-hadoop-create-linux-clusters-portal.md)文件中的步驟來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="97259-231">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="97259-232">叢集建立期間，您必須選擇包含您虛擬網路的位置。</span><span class="sxs-lookup"><span data-stu-id="97259-232">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="97259-233">在設定的__進階設定__部分，您必須選取稍早建立的虛擬網路與子網路。</span><span class="sxs-lookup"><span data-stu-id="97259-233">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="97259-234">連線至 HDInsight</span><span class="sxs-lookup"><span data-stu-id="97259-234">Connecting to HDInsight</span></span>

<span data-ttu-id="97259-235">HDInsight 上大部分的文件都假設您透過網際網路擁有叢集存取權。</span><span class="sxs-lookup"><span data-stu-id="97259-235">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="97259-236">例如，您可以連線到 https://CLUSTERNAME.azurehdinsight.net 的叢集。</span><span class="sxs-lookup"><span data-stu-id="97259-236">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="97259-237">這個位址會使用公用閘道，如果您已經使用 NSG 或 UDR 來限制網際網路的存取，則無法使用。</span><span class="sxs-lookup"><span data-stu-id="97259-237">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="97259-238">若要透過虛擬網路直接連線至 HDInsight，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97259-238">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="97259-239">若要探索 HDInsight 叢集節點的內部完整網域名稱，請使用下列方法之一：</span><span class="sxs-lookup"><span data-stu-id="97259-239">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

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

2. <span data-ttu-id="97259-240">若要判斷可提供服務的連接埠，請參閱 [Hadoop 服務在 HDInsight 上所使用的連接埠](./hdinsight-hadoop-port-settings-for-services.md)文件。</span><span class="sxs-lookup"><span data-stu-id="97259-240">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="97259-241">前端節點上裝載的某些服務一次只會在一個節點上作用。</span><span class="sxs-lookup"><span data-stu-id="97259-241">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="97259-242">如果您嘗試在一個前端節點上存取服務但卻失敗，請切換至其他的前端節點。</span><span class="sxs-lookup"><span data-stu-id="97259-242">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="97259-243">例如，Ambari 一次只在一個前端節點上作用。</span><span class="sxs-lookup"><span data-stu-id="97259-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="97259-244">如果您嘗試在一個前端節點上存取 Ambari 而傳回 404 錯誤，表示它正在其他前端節點上執行中。</span><span class="sxs-lookup"><span data-stu-id="97259-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97259-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97259-245">Next steps</span></span>

* <span data-ttu-id="97259-246">如需在虛擬網路中使用 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](./hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="97259-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="97259-247">如需有關 Azure 虛擬網路的詳細資訊，請參閱 [Azure 虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="97259-247">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="97259-248">如需網路安全性群組的詳細資訊，請參閱[網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="97259-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="97259-249">如需使用者定義路由的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="97259-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
