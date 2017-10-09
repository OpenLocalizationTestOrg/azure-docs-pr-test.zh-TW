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
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="dd1b8-104">HDInsight tooyour 在內部部署網路連線</span><span class="sxs-lookup"><span data-stu-id="dd1b8-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="dd1b8-105">了解如何 tooconnect HDInsight tooyour 內部部署網路使用 Azure 虛擬網路和 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="dd1b8-106">本文件提供下列規劃資訊：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-106">This document provides planning information on:</span></span>

* <span data-ttu-id="dd1b8-107">使用 HDInsight 連接 tooyour Azure 虛擬網路中內部網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="dd1b8-108">設定 hello 虛擬網路與內部部署網路之間的 DNS 名稱解析。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="dd1b8-109">設定網路安全性群組 toorestrict 網際網路存取 tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="dd1b8-110">HDInsight 在 hello 虛擬網路上提供的連接埠。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="dd1b8-111">建立 hello 虛擬網路組態</span><span class="sxs-lookup"><span data-stu-id="dd1b8-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd1b8-112">如果您要尋找的逐步指引連接 HDInsight tooyour 內部網路，使用 Azure 虛擬網路，請參閱 hello[連接 HDInsight tooyour 在內部部署網路](connect-on-premises-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="dd1b8-113">使用 hello 下列文件 toolearn 如何 toocreate Azure 虛擬網路的連線的 tooyour 內部網路：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="dd1b8-114">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dd1b8-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="dd1b8-115">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd1b8-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="dd1b8-116">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd1b8-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="dd1b8-117">設定名稱解析</span><span class="sxs-lookup"><span data-stu-id="dd1b8-117">Configure name resolution</span></span>

<span data-ttu-id="dd1b8-118">tooallow HDInsight 和 hello 加入網路 toocommunicate 依名稱中的資源，您必須執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="dd1b8-119">在 hello Azure 虛擬網路中建立自訂的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="dd1b8-120">Hello 虛擬網路 toouse hello 自訂 DNS 伺服器設定而非 hello 預設 Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="dd1b8-121">設定自訂 DNS 伺服器 hello 與您的內部部署 DNS 伺服器之間的轉送。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="dd1b8-122">此設定可啟用 hello 下列行為：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="dd1b8-123">要求的完整的網域名稱擁有 hello DNS 尾碼__hello 虛擬網路__轉送 toohello 自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="dd1b8-124">hello 自訂 DNS 伺服器，然後轉送這些要求 toohello Azure 遞迴解析程式，會傳回 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="dd1b8-125">所有其他要求都會轉送 toohello 在內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="dd1b8-126">公用網際網路資源，例如 microsoft.com 甚至的要求都會轉送 toohello 在內部部署 DNS 伺服器進行名稱解析。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="dd1b8-127">在下列圖表 hello，綠色行會結束 hello hello 虛擬網路的 DNS 尾碼 中的資源要求。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="dd1b8-128">藍線是要求資源 hello 在內部部署網路中或在 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![DNS 要求如何解決在使用這份文件中的 hello 組態中的圖表](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="dd1b8-130">建立自訂的 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="dd1b8-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd1b8-131">您必須建立並設定 hello DNS 伺服器，然後再安裝 HDInsight 在 hello 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="dd1b8-132">toocreate Linux VM 使用 hello[繫結](https://www.isc.org/downloads/bind/)DNS 軟體，使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="dd1b8-133">hello 下列步驟使用 hello [Azure 入口網站](https://portal.azure.com)toocreate Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="dd1b8-134">其他方式 toocreate 虛擬機器，請參閱 hello[建立的 VM-Azure CLI](../virtual-machines/linux/quick-create-cli.md)和[建立 VM 的 Azure PowerShell](../virtual-machines/linux/quick-create-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="dd1b8-135">從 hello [Azure 入口網站](https://portal.azure.com)，選取 __+__ ，__計算__，和__Ubuntu Server 16.04 LTS__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![建立 Ubuntu 虛擬機器](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="dd1b8-137">從 hello__基本概念__區段中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="dd1b8-138">__名稱__：識別此虛擬機器的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="dd1b8-139">例如，__DNSProxy__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="dd1b8-140">__使用者名稱__: hello hello SSH 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="dd1b8-141">__SSH 公開金鑰__或__密碼__: hello hello SSH 帳戶的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="dd1b8-142">我們建議使用公開金鑰，因為它們較為安全。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="dd1b8-143">如需詳細資訊，請參閱 hello[適用於 Linux Vm 建立及使用 SSH 金鑰](../virtual-machines/linux/mac-create-ssh-keys.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="dd1b8-144">__資源群組__： 選取__使用現有__，然後選取 hello 資源群組含有 hello 稍早建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="dd1b8-145">__位置__： 選取 hello 與 hello 虛擬網路相同的位置。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![虛擬機器基本設定](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="dd1b8-147">將其他項目在 hello 保留預設值，然後選取 __確定__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="dd1b8-148">從 hello__大小選擇 「__區段中，選取 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="dd1b8-149">此教學課程中，選取最小的 hello 和最低成本的選項。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="dd1b8-150">toocontinue，使用 hello__選取__ 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="dd1b8-151">從 hello__設定__區段中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="dd1b8-152">__虛擬網路__： 選取 hello 您稍早建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="dd1b8-153">__子網路__： 選取 hello hello 虛擬網路的預設子網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="dd1b8-154">請勿__不__選取 hello hello VPN 閘道使用的子網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="dd1b8-155">__診斷儲存體帳戶__：選取現有的儲存體帳戶或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![虛擬網路設定](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="dd1b8-157">將保留 hello 其他項目 hello 預設值，然後選取 __確定__toocontinue。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="dd1b8-158">從 hello__購買__區段中，選取 hello__購買__按鈕 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="dd1b8-159">一旦建立 hello 虛擬機器之後，其__概觀__區段會顯示。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="dd1b8-160">從左側 hello hello 清單中選取__屬性__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="dd1b8-161">儲存 hello__公用 IP 位址__和__私人 IP 位址__值。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="dd1b8-162">它會使用 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-162">It will be used in hello next section.</span></span>

    ![公用和私人 IP 位址](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="dd1b8-164">安裝並設定 Bind (DNS 軟體)</span><span class="sxs-lookup"><span data-stu-id="dd1b8-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="dd1b8-165">使用 SSH tooconnect toohello__公用 IP 位址__hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="dd1b8-166">下列範例中的 hello 連線 40.68.254.142 tooa 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="dd1b8-167">取代`sshuser`hello SSH 使用者帳戶與您在建立時指定 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd1b8-168">有各種不同的方式 tooobtain hello`ssh`公用程式。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="dd1b8-169">在 Linux、 Unix 及 macOS，它是依現狀 hello 作業系統的一部分。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="dd1b8-170">如果您使用 Windows 時，請考慮使用其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="dd1b8-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="dd1b8-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="dd1b8-172">在 Windows 10 上 Ubuntu 上的 Bash</span><span class="sxs-lookup"><span data-stu-id="dd1b8-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="dd1b8-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="dd1b8-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="dd1b8-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="dd1b8-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="dd1b8-175">tooinstall 繫結，請使用下列命令從 hello SSH 工作階段的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="dd1b8-176">tooconfigure 繫結 tooforward 名稱解析要求 tooyour 內部 DNS 伺服器，請使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.options`檔案：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

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
    > <span data-ttu-id="dd1b8-177">Hello 中的 hello 值取代為`goodclients`hello IP 位址範圍的 hello 虛擬網路與內部部署網路的一節。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="dd1b8-178">這個區段會定義此 DNS 伺服器接受來自要求的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="dd1b8-179">取代 hello `192.168.0.1` hello 中的項目`forwarders`hello IP 位址在內部部署 DNS 伺服器的一節。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="dd1b8-180">此項目路由 DNS 要求 tooyour 內部 DNS 伺服器進行解析。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="dd1b8-181">tooedit 此檔案，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="dd1b8-182">toosave hello 檔案，使用__Ctrl + X__， __Y__，然後__Enter__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="dd1b8-183">從 hello SSH 工作階段，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="dd1b8-184">此命令會傳回值的類似 toohello，下列文字：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="dd1b8-185">hello`icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net`文字是 hello __DNS 尾碼__為此虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="dd1b8-186">儲存這個值以便稍後使用。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="dd1b8-187">tooconfigure 繫結 tooresolve DNS 名稱 hello 虛擬網路中資源的使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.local`檔案：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="dd1b8-188">您必須取代 hello`icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net`與您先前擷取的 hello DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="dd1b8-189">tooedit 此檔案，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="dd1b8-190">toosave hello 檔案，使用__Ctrl + X__， __Y__，然後__Enter__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="dd1b8-191">toostart 繫結，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="dd1b8-192">繫結的 tooverify 可以解決 hello 資源名稱的內部部署網路中、 使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="dd1b8-193">取代`dns.mynetwork.net`與 hello 完整的網域名稱 (FQDN) 的內部部署網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="dd1b8-194">取代`10.0.0.4`以 hello__內部 IP 位址__的 hello 虛擬網路中的自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="dd1b8-195">hello 回應會顯示下列文字類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="dd1b8-196">Hello 虛擬網路 toouse hello 自訂 DNS 伺服器設定</span><span class="sxs-lookup"><span data-stu-id="dd1b8-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="dd1b8-197">tooconfigure hello 虛擬網路 toouse hello 自訂 DNS 伺服器，而非 hello Azure 遞迴解析程式，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="dd1b8-198">在 hello [Azure 入口網站](https://portal.azure.com)選取 hello 虛擬網路，然後選取__DNS 伺服器__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="dd1b8-199">選取__自訂__，然後輸入 hello__內部 IP 位址__hello 自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="dd1b8-200">最後，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-200">Finally, select __Save__.</span></span>

    ![設定 hello 自訂網路 DNS 伺服器 hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="dd1b8-202">Hello 在內部部署 DNS 伺服器設定</span><span class="sxs-lookup"><span data-stu-id="dd1b8-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="dd1b8-203">在 hello 前一個區段中，您可以設定 hello 自訂 DNS 伺服器 tooforward 要求 toohello 在內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="dd1b8-204">接下來，您必須設定 hello 在內部部署 DNS 伺服器 tooforward 要求 toohello 自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="dd1b8-205">如需有關特定步驟 tooconfigure 您的 DNS 伺服器，請洽詢您的 DNS 伺服器軟體的 hello 文件集。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="dd1b8-206">如需有關如何 hello 步驟尋找 tooconfigure__條件轉寄站__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="dd1b8-207">條件式轉寄只會轉寄特定 DNS 尾碼的要求。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="dd1b8-208">在此情況下，您必須設定的轉寄站來 hello hello 虛擬網路的 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="dd1b8-209">這個後置詞的要求應該轉送 toohello hello 自訂的 DNS 伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="dd1b8-210">hello 下列文字是範例 hello 的條件轉寄站組態**繫結**DNS 軟體：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="dd1b8-211">如需有關上使用 DNS 資訊**Windows Server 2016**，請參閱 hello[新增 DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone)文件...</span><span class="sxs-lookup"><span data-stu-id="dd1b8-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="dd1b8-212">一旦您已設定 hello 在內部部署 DNS 伺服器，您可以使用`nslookup`從 hello 在內部部署網路 tooverify 可以解析名稱 hello 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="dd1b8-213">下列範例中的 hello</span><span class="sxs-lookup"><span data-stu-id="dd1b8-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="dd1b8-214">這個範例會使用 hello 在內部部署 DNS 伺服器在 196.168.0.4 tooresolve hello hello 自訂的 DNS 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="dd1b8-215">取代 hello 在內部部署 DNS 伺服器的其中一個 hello hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="dd1b8-216">取代 hello `dnsproxy` hello hello 自訂 DNS 伺服器的完整的網域名稱與地址。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="dd1b8-217">選擇性：控制網路流量</span><span class="sxs-lookup"><span data-stu-id="dd1b8-217">Optional: Control network traffic</span></span>

<span data-ttu-id="dd1b8-218">您可以使用網路安全性群組 (NSG) 或使用者定義的路由 (UDR) toocontrol 網路流量。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="dd1b8-219">Nsg 可讓您 toofilter 輸入和輸出流量，及允許或拒絕 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="dd1b8-220">UDRs toocontrol 流量 hello 虛擬網路中的資源之間流動的方式可讓您、 hello 網際網路和 hello 與內部網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="dd1b8-221">HDInsight 需要來自特定 IP 位址在 hello Azure 雲端中，輸入的存取和不受限制的輸出存取。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="dd1b8-222">當使用 Nsg 或 UDRs toocontrol 流量，您必須執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="dd1b8-223">尋找包含您的虛擬網路的 hello 位置 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="dd1b8-224">如需依位置的必要 IP 清單，請參閱[必要的 IP 位址](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip)。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="dd1b8-225">允許輸入的流量從 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="dd1b8-226">__NSG__： 允許__輸入__連接埠的流量__443__從 hello__網際網路__。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="dd1b8-227">__UDR__： 集 hello__下個躍點__hello 路由 too__Internet__ 的類型。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="dd1b8-228">如需使用 Azure PowerShell 或 hello Azure CLI toocreate Nsg 的範例，請參閱 hello[擴充 HDInsight 的 Azure 虛擬網路](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg)文件。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="dd1b8-229">建立 hello HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dd1b8-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="dd1b8-230">您必須先安裝 HDInsight hello 虛擬網路中設定自訂 DNS 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="dd1b8-231">使用 hello 步驟 hello[建立使用 hello Azure 入口網站的 HDInsight 叢集](./hdinsight-hadoop-create-linux-clusters-portal.md)文件 toocreate 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="dd1b8-232">叢集建立期間，您必須選擇包含您的虛擬網路的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="dd1b8-233">在 hello__進階設定__部分的設定，您必須選取 hello 虛擬網路與您稍早建立的子網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="dd1b8-234">連接 tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="dd1b8-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="dd1b8-235">HDInsight 上的大部分文件假設您有存取 toohello 叢集 hello 透過網際網路。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="dd1b8-236">例如，您可以連接 https://CLUSTERNAME.azurehdinsight.net toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="dd1b8-237">這個位址會使用 hello 公用閘道，如果您已經使用 Nsg，或從 UDRs toorestrict 存取 hello 網際網路，則無法使用此。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="dd1b8-238">toodirectly tooHDInsight 連接透過 hello 虛擬網路，請使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd1b8-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="dd1b8-239">toodiscover hello 內部的完整的網域名稱的 hello HDInsight 叢集節點，使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="dd1b8-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

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

2. <span data-ttu-id="dd1b8-240">toodetermine hello 可用通訊埠的服務，請參閱 hello [HDInsight 上的 Hadoop 服務所使用的連接埠](./hdinsight-hadoop-port-settings-for-services.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="dd1b8-241">某些 hello 前端節點上裝載的服務才一次一個節點上使用中。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="dd1b8-242">如果您嘗試存取一個前端節點上的服務，它就會失敗，請切換 toohello 其他前端節點。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="dd1b8-243">例如，Ambari 一次只在一個前端節點上作用。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="dd1b8-244">如果您嘗試存取 Ambari 一個前端節點上，它會傳回 404 錯誤，其執行於 hello 其他前端節點。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd1b8-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd1b8-245">Next steps</span></span>

* <span data-ttu-id="dd1b8-246">如需在虛擬網路中使用 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](./hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="dd1b8-247">如需有關 Azure 虛擬網路的詳細資訊，請參閱 hello [Azure 虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="dd1b8-248">如需網路安全性群組的詳細資訊，請參閱[網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="dd1b8-249">如需使用者定義路由的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dd1b8-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
