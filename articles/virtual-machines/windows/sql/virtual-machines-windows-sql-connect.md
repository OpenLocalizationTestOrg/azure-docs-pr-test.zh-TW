---
title: "aaaConnect tooa SQL Server 虛擬機器 （資源管理員） |Microsoft 文件"
description: "深入了解如何 tooconnect tooSQL 伺服器在 Azure 中的虛擬機器上執行。 本主題使用 hello 傳統部署模型。 hello 案例 hello 網路設定與 hello 用戶端 hello 位置而有所不同。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="0ab34-105">連接 tooa Azure （資源管理員） 上的 SQL Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0ab34-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ab34-106">資源管理員</span><span class="sxs-lookup"><span data-stu-id="0ab34-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="0ab34-107">傳統</span><span class="sxs-lookup"><span data-stu-id="0ab34-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="0ab34-108">概觀</span><span class="sxs-lookup"><span data-stu-id="0ab34-108">Overview</span></span>

<span data-ttu-id="0ab34-109">本主題描述如何 tooconnect tooyour SQL Server 執行個體在 Azure 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="0ab34-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="0ab34-110">其中涵蓋一些[一般連線案例](#connection-scenarios)並提供[在 Azure VM 中設定 SQL Server 連線的詳細步驟](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm)。</span><span class="sxs-lookup"><span data-stu-id="0ab34-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="0ab34-111">如需有關佈建和連線能力的完整逐步解說，請參閱 [在 Azure 上佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="0ab34-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="0ab34-112">連接案例</span><span class="sxs-lookup"><span data-stu-id="0ab34-112">Connection scenarios</span></span>

<span data-ttu-id="0ab34-113">hello 方式用戶端連接的 tooSQL 虛擬機器上執行的伺服器 hello hello 的用戶端和 hello 網路設定的位置而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0ab34-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="0ab34-114">如果您佈建 hello Azure 入口網站中的 SQL Server VM，您會有 hello 選項指定 hello 類型**SQL 連接性**。</span><span class="sxs-lookup"><span data-stu-id="0ab34-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![佈建期間的公用 SQL 連線能力選項](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="0ab34-116">連線能力的選項包括：</span><span class="sxs-lookup"><span data-stu-id="0ab34-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="0ab34-117">選項</span><span class="sxs-lookup"><span data-stu-id="0ab34-117">Option</span></span> | <span data-ttu-id="0ab34-118">說明</span><span class="sxs-lookup"><span data-stu-id="0ab34-118">Description</span></span> |
|---|---|
| <span data-ttu-id="0ab34-119">**公開**</span><span class="sxs-lookup"><span data-stu-id="0ab34-119">**Public**</span></span> | <span data-ttu-id="0ab34-120">連接 tooSQL 伺服器 hello 透過網際網路</span><span class="sxs-lookup"><span data-stu-id="0ab34-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="0ab34-121">**私用**</span><span class="sxs-lookup"><span data-stu-id="0ab34-121">**Private**</span></span> | <span data-ttu-id="0ab34-122">連接中 hello tooSQL 伺服器相同的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="0ab34-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="0ab34-123">**本機**</span><span class="sxs-lookup"><span data-stu-id="0ab34-123">**Local**</span></span> | <span data-ttu-id="0ab34-124">連接本機上 hello tooSQL 伺服器相同的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0ab34-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="0ab34-125">hello 下列各節說明 hello**公用**和**私人**更多詳細資料中的選項。</span><span class="sxs-lookup"><span data-stu-id="0ab34-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="0ab34-126">連線透過網際網路 hello tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="0ab34-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="0ab34-127">如果您想從 hello 網際網路 tooconnect tooyour SQL Server 資料庫引擎，請選取**公用**hello **SQL 連接性**hello 入口網站佈建期間中的型別。</span><span class="sxs-lookup"><span data-stu-id="0ab34-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="0ab34-128">自動 hello 入口網站未 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0ab34-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="0ab34-129">讓 SQL Server 中的 hello TCP/IP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0ab34-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="0ab34-130">設定防火牆規則 tooopen hello SQL Server TCP 連接埠 （預設值 1433年）。</span><span class="sxs-lookup"><span data-stu-id="0ab34-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="0ab34-131">可進行公用存取所需的 SQL Server 驗證。</span><span class="sxs-lookup"><span data-stu-id="0ab34-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="0ab34-132">設定網路安全性群組 hello hello hello SQL Server 連接埠上的 VM tooall TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="0ab34-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ab34-133">SQL Server Developer hello 虛擬機器映像和 Express 版本不會自動啟用 hello TCP/IP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0ab34-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="0ab34-134">開發人員和 Express 版本中，您必須用於 SQL Server 組態管理員太[手動啟用 hello TCP/IP 通訊協定](#manualtcp)之後建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="0ab34-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="0ab34-135">任何具有網際網路存取權的用戶端可以藉由指定 hello 虛擬機器的 hello 公用 IP 位址或 toothat IP 位址指定給任何 DNS 標籤連接 toohello SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0ab34-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="0ab34-136">Hello SQL Server 連接埠為 1433年，如果您不需要 toospecify hello 連接字串中。</span><span class="sxs-lookup"><span data-stu-id="0ab34-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="0ab34-137">下列連接字串 hello 與 DNS 標籤連接 tooa SQL VM 的`sqlvmlabel.eastus.cloudapp.azure.com`使用 SQL 驗證 （您也可以使用 hello 公用 IP 位址）。</span><span class="sxs-lookup"><span data-stu-id="0ab34-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="0ab34-138">雖然這會啟用連線用戶端透過 hello 網際網路，這不表示任何人都可以連線 tooyour SQL Server。</span><span class="sxs-lookup"><span data-stu-id="0ab34-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="0ab34-139">外部用戶端具備 toohello 正確的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0ab34-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="0ab34-140">不過，為了增加安全性，您可以避免 hello 已知通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="0ab34-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="0ab34-141">比方說，如果您設定 SQL Server toolisten 上通訊埠 1500年建立適當的防火牆和網路安全性群組規則，您無法藉由附加 hello 通訊埠編號 toohello 伺服器名稱連接。</span><span class="sxs-lookup"><span data-stu-id="0ab34-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="0ab34-142">hello 下列範例會改變 hello 前一個藉由加入自訂連接埠編號， **1500年**，toohello 伺服器名稱：</span><span class="sxs-lookup"><span data-stu-id="0ab34-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="0ab34-143">當您查詢在 VM 中的 SQL Server 透過 hello 網際網路，所有傳出資料從 hello Azure 資料中心是主體 toonormal[上輸出資料傳輸定價](https://azure.microsoft.com/pricing/details/data-transfers/)。</span><span class="sxs-lookup"><span data-stu-id="0ab34-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="0ab34-144">連接虛擬網路內 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="0ab34-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="0ab34-145">當您選擇**私人**hello **SQL 連接性**hello Azure 入口網站中的型別會設定大部分相同的 hello 設定太**公用**。</span><span class="sxs-lookup"><span data-stu-id="0ab34-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="0ab34-146">hello 其中一種差異是沒有任何網路安全性群組規則 tooallow 外 hello SQL Server 連接埠 （預設值 1433年） 上的流量。</span><span class="sxs-lookup"><span data-stu-id="0ab34-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ab34-147">SQL Server Developer hello 虛擬機器映像和 Express 版本不會自動啟用 hello TCP/IP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0ab34-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="0ab34-148">開發人員和 Express 版本中，您必須用於 SQL Server 組態管理員太[手動啟用 hello TCP/IP 通訊協定](#manualtcp)之後建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="0ab34-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="0ab34-149">私用連線能力通常與[虛擬網路](../../../virtual-network/virtual-networks-overview.md)搭配使用，可進行數個情節。</span><span class="sxs-lookup"><span data-stu-id="0ab34-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="0ab34-150">您可以在相同虛擬網路，即使這些 Vm 存在於不同的資源群組中的 hello 連接 Vm。</span><span class="sxs-lookup"><span data-stu-id="0ab34-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="0ab34-151">[站對站 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)可讓您建立能將 VM 連接至內部部署網路和電腦的混合式架構。</span><span class="sxs-lookup"><span data-stu-id="0ab34-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="0ab34-152">虛擬網路也可讓您 toojoin 您的 Azure Vm tooa 網域。</span><span class="sxs-lookup"><span data-stu-id="0ab34-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="0ab34-153">這是 hello 唯一方式 toouse Windows 驗證 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0ab34-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="0ab34-154">hello 其他連線案例則需要 SQL 驗證的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0ab34-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="0ab34-155">假設您已在虛擬網路中設定 DNS，您可以藉由指定 hello 連接字串中的 hello SQL Server VM 的電腦名稱連接 tooyour SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0ab34-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="0ab34-156">下列範例也 hello 假設也已經設定 Windows 驗證，且該 hello 使用者已獲得存取 toohello SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0ab34-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="0ab34-157"><a id="change"></a>變更 SQL 連線能力設定</span><span class="sxs-lookup"><span data-stu-id="0ab34-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="0ab34-158">您可以變更 hello Azure 入口網站中的 SQL Server 虛擬機器 hello 連線設定。</span><span class="sxs-lookup"><span data-stu-id="0ab34-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="0ab34-159">在 hello Azure 入口網站，選取 **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="0ab34-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="0ab34-160">選取 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="0ab34-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="0ab34-161">在 [設定] 下，按一下 [SQL Server 組態]。</span><span class="sxs-lookup"><span data-stu-id="0ab34-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="0ab34-162">變更 hello **SQL 連線層級**tooyour 所需的設定。</span><span class="sxs-lookup"><span data-stu-id="0ab34-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="0ab34-163">您可以選擇性地使用此區域 toochange hello SQL Server 連接埠或 hello SQL 驗證設定。</span><span class="sxs-lookup"><span data-stu-id="0ab34-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![變更 SQL 連線能力](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="0ab34-165">請等候幾分鐘的時間 hello 更新 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="0ab34-165">Wait several minutes for hello update toocomplete.</span></span>

   ![SQL VM 更新通知](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="0ab34-167"><a id="manualtcp"></a> 針對 Developer 和 Express 版本啟用 TCP/IP</span><span class="sxs-lookup"><span data-stu-id="0ab34-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="0ab34-168">變更 SQL Server 連線設定，Azure 不會自動啟用 hello TCP/IP 通訊協定的 SQL Server Developer edition 和 Express edition。</span><span class="sxs-lookup"><span data-stu-id="0ab34-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="0ab34-169">hello 執行下列步驟說明如何 toomanually 啟用 TCP/IP 時，讓您可以從遠端連線的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0ab34-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="0ab34-170">首先，使用遠端桌面連接 toohello SQL Server 電腦。</span><span class="sxs-lookup"><span data-stu-id="0ab34-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="0ab34-171">接下來，啟用 hello TCP/IP 通訊協定與**SQL Server 組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="0ab34-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="0ab34-172">以 SSMS 連線</span><span class="sxs-lookup"><span data-stu-id="0ab34-172">Connect with SSMS</span></span>

<span data-ttu-id="0ab34-173">hello 下列步驟顯示如何 toocreate 選擇性 DNS 加上標籤的 Azure VM，然後連接的 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="0ab34-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="0ab34-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ab34-174">Next Steps</span></span>

<span data-ttu-id="0ab34-175">toosee 佈建的指示，以及這些連線的步驟，請參閱[佈建在 Azure 上的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="0ab34-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="0ab34-176">如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0ab34-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
