---
title: "aaaConnect tooa Azure （傳統） 上的 SQL Server 虛擬機器 |Microsoft 文件"
description: "深入了解如何 tooconnect tooSQL 伺服器在 Azure 中的虛擬機器上執行。 本主題使用 hello 傳統部署模型。 hello 案例 hello 網路設定與 hello 用戶端 hello 位置而有所不同。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a><span data-ttu-id="da891-105">連接 tooa Azure （傳統部署） 上的 SQL Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="da891-105">Connect tooa SQL Server Virtual Machine on Azure (Classic Deployment)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da891-106">資源管理員</span><span class="sxs-lookup"><span data-stu-id="da891-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="da891-107">傳統</span><span class="sxs-lookup"><span data-stu-id="da891-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="da891-108">概觀</span><span class="sxs-lookup"><span data-stu-id="da891-108">Overview</span></span>
<span data-ttu-id="da891-109">本主題描述如何 tooconnect tooyour SQL Server 執行個體在 Azure 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="da891-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="da891-110">其中涵蓋一些[一般連線案例](#connection-scenarios)並提供[在 Azure VM 中設定 SQL Server 連線的詳細步驟](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。</span><span class="sxs-lookup"><span data-stu-id="da891-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="da891-111">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="da891-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="da891-112">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="da891-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="da891-113">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="da891-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="da891-114">如果您使用資源管理員的 Vm，請參閱[連接 tooa 使用資源管理員的 Azure 上的 SQL Server 虛擬機器](../sql/virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="da891-114">If you are using Resource Manager VMs, see [Connect tooa SQL Server Virtual Machine on Azure using Resource Manager](../sql/virtual-machines-windows-sql-connect.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="da891-115">連接案例</span><span class="sxs-lookup"><span data-stu-id="da891-115">Connection scenarios</span></span>
<span data-ttu-id="da891-116">hello 方式用戶端連接的 tooSQL 虛擬機器上執行的伺服器 hello hello 的用戶端和 hello 電腦/網路組態的位置而有所不同。</span><span class="sxs-lookup"><span data-stu-id="da891-116">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello machine/networking configuration.</span></span> <span data-ttu-id="da891-117">這些案例包括：</span><span class="sxs-lookup"><span data-stu-id="da891-117">These scenarios include:</span></span>

* [<span data-ttu-id="da891-118">連接 tooSQL 伺服器 hello 在相同雲端服務</span><span class="sxs-lookup"><span data-stu-id="da891-118">Connect tooSQL Server in hello same cloud service</span></span>](#connect-to-sql-server-in-the-same-cloud-service)
* [<span data-ttu-id="da891-119">連接 tooSQL 伺服器 hello 透過網際網路</span><span class="sxs-lookup"><span data-stu-id="da891-119">Connect tooSQL Server over hello internet</span></span>](#connect-to-sql-server-over-the-internet)
* [<span data-ttu-id="da891-120">連接中 hello tooSQL 伺服器相同的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="da891-120">Connect tooSQL Server in hello same virtual network</span></span>](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> <span data-ttu-id="da891-121">在連線與任何一種方法之前，您必須遵循 hello[此發行項 tooconfigure 連接中的步驟](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。</span><span class="sxs-lookup"><span data-stu-id="da891-121">Before you connect with any of these methods, you must follow hello [steps in this article tooconfigure connectivity](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a><span data-ttu-id="da891-122">連接 tooSQL 伺服器 hello 在相同雲端服務</span><span class="sxs-lookup"><span data-stu-id="da891-122">Connect tooSQL Server in hello same cloud service</span></span>
<span data-ttu-id="da891-123">多部虛擬機器中可建立 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="da891-123">Multiple virtual machines can be created in hello same cloud service.</span></span> <span data-ttu-id="da891-124">toounderstand 此虛擬機器案例中，請參閱[如何 tooconnect 虛擬機器與虛擬網路或雲端服務](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="da891-124">toounderstand this virtual machines scenario, see [How tooconnect virtual machines with a virtual network or cloud service](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service).</span></span> <span data-ttu-id="da891-125">一部虛擬機器上的用戶端會嘗試執行 tooconnect tooSQL 伺服器時，此案例中的 hello 的另一個虛擬機器上相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="da891-125">This scenario is when a client on one virtual machine attempts tooconnect tooSQL Server running on another virtual machine in hello same cloud service.</span></span>

<span data-ttu-id="da891-126">在此案例中，您可以使用連線 hello VM**名稱**(也會顯示為**電腦名稱**或**hostname** hello 入口網站中)。</span><span class="sxs-lookup"><span data-stu-id="da891-126">In this scenario, you can connect using hello VM **Name** (also shown as **Computer Name** or **hostname** in hello portal).</span></span> <span data-ttu-id="da891-127">這是您在建立期間提供 hello VM hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="da891-127">This is hello name you provided for hello VM during creation.</span></span> <span data-ttu-id="da891-128">例如，如果您已命名為您的 SQL VM **mysqlvm**，hello 可以使用相同的雲端服務中的用戶端 VM hello 下列連接字串 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="da891-128">For example, if you named your SQL VM **mysqlvm**, a client VM in hello same cloud service could use hello following connection string tooconnect:</span></span>

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="da891-129">連線透過網際網路 hello tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="da891-129">Connect tooSQL Server over hello Internet</span></span>
<span data-ttu-id="da891-130">如果您想從 hello 網際網路 tooconnect tooyour SQL Server 資料庫引擎，您必須建立虛擬機器端點內送 TCP 通訊。</span><span class="sxs-lookup"><span data-stu-id="da891-130">If you want tooconnect tooyour SQL Server database engine from hello Internet, you must create a virtual machine endpoint for incoming TCP communication.</span></span> <span data-ttu-id="da891-131">這個 Azure 組態步驟，指示內送 TCP 連接埠流量 tooa TCP 通訊埠是可存取 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="da891-131">This Azure configuration step, directs incoming TCP port traffic tooa TCP port that is accessible toohello virtual machine.</span></span>

<span data-ttu-id="da891-132">透過 tooconnect hello 網際網路，您必須使用 hello VM 的 DNS 名稱和 hello VM 端點連接埠號碼 （本文中稍後設定）。</span><span class="sxs-lookup"><span data-stu-id="da891-132">tooconnect over hello internet, you must use hello VM's DNS name and hello VM endpoint port number (configured later in this article).</span></span> <span data-ttu-id="da891-133">toofind hello DNS 名稱，瀏覽 toohello Azure 入口網站，然後選取**虛擬機器 （傳統）**。</span><span class="sxs-lookup"><span data-stu-id="da891-133">toofind hello DNS Name, navigate toohello Azure portal, and select **Virtual machines (classic)**.</span></span> <span data-ttu-id="da891-134">然後選取您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="da891-134">Then select your virtual machine.</span></span> <span data-ttu-id="da891-135">hello **DNS 名稱**如下所示 hello**概觀**> 一節。</span><span class="sxs-lookup"><span data-stu-id="da891-135">hello **DNS name** is shown in hello **Overview** section.</span></span>

<span data-ttu-id="da891-136">例如，假設名為 **mysqlvm** 的傳統虛擬機器，其 DNS 名稱為 **mysqlvm7777.cloudapp.net**，且 VM 端點是 **57500**。</span><span class="sxs-lookup"><span data-stu-id="da891-136">For example, consider a classic virtual machine named **mysqlvm** with a DNS Name of **mysqlvm7777.cloudapp.net** and a VM endpoint of **57500**.</span></span> <span data-ttu-id="da891-137">假設已正確設定的連線，下列連接字串 hello 可能是從任何地方使用的 tooaccess hello 虛擬機器上 hello 網際網路：</span><span class="sxs-lookup"><span data-stu-id="da891-137">Assuming properly configured connectivity, hello following connection string could be used tooaccess hello virtual machine from anywhere on hello internet:</span></span>

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

<span data-ttu-id="da891-138">雖然這會啟用連線用戶端透過 hello 網際網路，這不表示任何人都可以連線 tooyour SQL Server。</span><span class="sxs-lookup"><span data-stu-id="da891-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="da891-139">外部用戶端具備 toohello 正確的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="da891-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="da891-140">為了增加安全性，請勿將 hello 已知通訊埠 1433年用於 hello 公用虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="da891-140">For additional security, don't use hello well-known port 1433 for hello public virtual machine endpoint.</span></span> <span data-ttu-id="da891-141">如果可能，請考慮您端點 toorestrict 流量只有 toohello 用戶端上您允許新增 ACL。</span><span class="sxs-lookup"><span data-stu-id="da891-141">And if possible, consider adding an ACL on your endpoint toorestrict traffic only toohello clients you permit.</span></span> <span data-ttu-id="da891-142">如需有關使用具有端點 Acl 的指示，請參閱[端點上的管理 hello ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="da891-142">For instructions on using ACLs with endpoints, see [Manage hello ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

> [!NOTE]
> <span data-ttu-id="da891-143">這是很重要，當您使用這個技巧 toocommunicate 與 SQL Server 時，所有傳出資料 hello Azure 資料中心的 toonote 主旨 toonormal[上輸出資料傳輸定價](https://azure.microsoft.com/pricing/details/data-transfers/)。</span><span class="sxs-lookup"><span data-stu-id="da891-143">It is important toonote that when you use this technique toocommunicate with SQL Server, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a><span data-ttu-id="da891-144">連接中 hello tooSQL 伺服器相同的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="da891-144">Connect tooSQL Server in hello same virtual network</span></span>
<span data-ttu-id="da891-145">[虛擬網路](../../../virtual-network/virtual-networks-overview.md) 讓其他案例變得可行。</span><span class="sxs-lookup"><span data-stu-id="da891-145">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span></span> <span data-ttu-id="da891-146">您可以在相同虛擬網路，即使這些 Vm 存在於不同的雲端服務中的 hello 連接 Vm。</span><span class="sxs-lookup"><span data-stu-id="da891-146">You can connect VMs in hello same virtual network, even if those VMs exist in different cloud services.</span></span> <span data-ttu-id="da891-147">[站對站 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)可讓您建立能將 VM 連接至內部部署網路和電腦的混合式架構。</span><span class="sxs-lookup"><span data-stu-id="da891-147">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="da891-148">虛擬網路也可讓您 toojoin 您的 Azure Vm tooa 網域。</span><span class="sxs-lookup"><span data-stu-id="da891-148">Virtual networks also enables you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="da891-149">這是 hello 唯一方式 toouse Windows 驗證 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="da891-149">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="da891-150">hello 其他連線案例則需要 SQL 驗證的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="da891-150">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="da891-151">如果您正在 tooconfigure 網域環境及 Windows 驗證，您不需要這個發行項 tooconfigure hello 公用端點或 hello SQL 驗證與登入 toouse hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="da891-151">If you are going tooconfigure a domain environment and Windows Authentication, you do not need toouse hello steps in this article tooconfigure hello public endpoint or hello SQL Authentication and logins.</span></span> <span data-ttu-id="da891-152">在此案例中，您可以藉由指定 hello 連接字串中的 hello SQL Server VM 名稱連接 tooyour SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="da891-152">In this scenario, you can connect tooyour SQL Server instance by specifying hello SQL Server VM name in hello connection string.</span></span> <span data-ttu-id="da891-153">下列範例中的 hello 假設也已經設定 Windows 驗證，且該 hello 使用者已獲得存取 toohello SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="da891-153">hello following example assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a><span data-ttu-id="da891-154">Azure VM 中設定 SQL Server 連線的步驟</span><span class="sxs-lookup"><span data-stu-id="da891-154">Steps for configuring SQL Server connectivity in an Azure VM</span></span>
<span data-ttu-id="da891-155">hello 下列步驟示範如何透過 tooconnect toohello SQL Server 執行個體 hello 網際網路使用 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="da891-155">hello following steps demonstrate how tooconnect toohello SQL Server instance over hello internet using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="da891-156">不過，hello 相同的步驟套用 toomaking SQL Server 虛擬機器可對於您的應用程式中，然後再執行這兩個內部部署和 Azure 中存取。</span><span class="sxs-lookup"><span data-stu-id="da891-156">However, hello same steps apply toomaking your SQL Server virtual machine accessible for your applications, running both on-premises and in Azure.</span></span>

<span data-ttu-id="da891-157">您可以從另一個 VM 連接 toohello SQL Server 執行個體或 hello 網際網路之前，您必須完成下列工作，hello 以下各節中所述的 hello:</span><span class="sxs-lookup"><span data-stu-id="da891-157">Before you can connect toohello instance of SQL Server from another VM or hello internet, you must complete hello following tasks as described in hello sections that follow:</span></span>

* [<span data-ttu-id="da891-158">建立 hello 虛擬機器的 TCP 端點</span><span class="sxs-lookup"><span data-stu-id="da891-158">Create a TCP endpoint for hello virtual machine</span></span>](#create-a-tcp-endpoint-for-the-virtual-machine)
* [<span data-ttu-id="da891-159">Hello Windows 防火牆中開啟 TCP 通訊埠</span><span class="sxs-lookup"><span data-stu-id="da891-159">Open TCP ports in hello Windows firewall</span></span>](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [<span data-ttu-id="da891-160">設定 SQL Server toolisten hello TCP 通訊協定</span><span class="sxs-lookup"><span data-stu-id="da891-160">Configure SQL Server toolisten on hello TCP protocol</span></span>](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [<span data-ttu-id="da891-161">設定 SQL Server 以進行混合模式驗證</span><span class="sxs-lookup"><span data-stu-id="da891-161">Configure SQL Server for mixed mode authentication</span></span>](#configure-sql-server-for-mixed-mode-authentication)
* [<span data-ttu-id="da891-162">建立 SQL Server 驗證登入</span><span class="sxs-lookup"><span data-stu-id="da891-162">Create SQL Server authentication logins</span></span>](#create-sql-server-authentication-logins)
* [<span data-ttu-id="da891-163">判斷 hello hello 虛擬機器的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="da891-163">Determine hello DNS name of hello virtual machine</span></span>](#determine-the-dns-name-of-the-virtual-machine)
* [<span data-ttu-id="da891-164">從另一部電腦連接 toohello Database Engine</span><span class="sxs-lookup"><span data-stu-id="da891-164">Connect toohello Database Engine from another computer</span></span>](#connect-to-the-database-engine-from-another-computer)

<span data-ttu-id="da891-165">下列圖表中的 hello 的摘要 hello 連線路徑：</span><span class="sxs-lookup"><span data-stu-id="da891-165">hello connection path is summarized by hello following diagram:</span></span>

![連接 tooa SQL Server 虛擬機器](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a><span data-ttu-id="da891-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da891-167">Next Steps</span></span>
<span data-ttu-id="da891-168">如果您打算也針對高可用性和災害復原 toouse AlwaysOn 可用性群組，您應該考慮實作接聽程式。</span><span class="sxs-lookup"><span data-stu-id="da891-168">If you are also planning toouse AlwaysOn Availability Groups for high availability and disaster recovery, you should consider implementing a listener.</span></span> <span data-ttu-id="da891-169">資料庫用戶端連線 toohello 接聽程式，而非直接 tooone hello SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="da891-169">Database clients connect toohello listener rather than directly tooone of hello SQL Server instances.</span></span> <span data-ttu-id="da891-170">hello 接聽程式路由用戶端 toohello 主要複本 hello 可用性群組中。</span><span class="sxs-lookup"><span data-stu-id="da891-170">hello listener routes clients toohello primary replica in hello availability group.</span></span> <span data-ttu-id="da891-171">如需詳細資訊，請參閱 [設定 Azure 中 AlwaysOn 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="da891-171">For more information, see [Configure an ILB listener for AlwaysOn Availability Groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="da891-172">很重要的 tooreview hello 安全性的所有 Azure 的虛擬機器上執行的 SQL Server 的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="da891-172">It is important tooreview all of hello security best practices for SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="da891-173">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 安全性考量](../sql/virtual-machines-windows-sql-security.md)。</span><span class="sxs-lookup"><span data-stu-id="da891-173">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).</span></span>

<span data-ttu-id="da891-174">[瀏覽 hello 學習路徑](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/)Azure 虛擬機器上的 SQL server。</span><span class="sxs-lookup"><span data-stu-id="da891-174">[Explore hello Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span> 

<span data-ttu-id="da891-175">如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="da891-175">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

