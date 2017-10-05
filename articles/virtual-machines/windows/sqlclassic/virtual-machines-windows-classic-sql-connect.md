---
title: "連線到 Azure 上的 SQL Server 虛擬機器 (傳統) | Microsoft Docs"
description: "了解如何連接在 Azure 虛擬機器上執行的 SQL Server。 本主題使用傳統部署模型。 案例會視網路組態和用戶端的位置而有所不同。"
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
ms.openlocfilehash: 4218b6d274abbeda542c1507aec998ba56f5c145
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-classic-deployment"></a><span data-ttu-id="03dca-105">連線到 Azure 上的 SQL Server 虛擬機器 (傳統部署)</span><span class="sxs-lookup"><span data-stu-id="03dca-105">Connect to a SQL Server Virtual Machine on Azure (Classic Deployment)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03dca-106">資源管理員</span><span class="sxs-lookup"><span data-stu-id="03dca-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="03dca-107">傳統</span><span class="sxs-lookup"><span data-stu-id="03dca-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="03dca-108">Overview</span><span class="sxs-lookup"><span data-stu-id="03dca-108">Overview</span></span>
<span data-ttu-id="03dca-109">本主題說明如何連線到在 Azure 虛擬機器上執行的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="03dca-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="03dca-110">其中涵蓋一些[一般連線案例](#connection-scenarios)並提供[在 Azure VM 中設定 SQL Server 連線的詳細步驟](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。</span><span class="sxs-lookup"><span data-stu-id="03dca-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="03dca-111">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="03dca-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="03dca-112">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="03dca-112">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="03dca-113">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="03dca-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="03dca-114">如果您是使用 Resource Manager VM，請參閱 [使用 Resource Manager 連接到 Azure 上的 SQL Server 虛擬機器](../sql/virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="03dca-114">If you are using Resource Manager VMs, see [Connect to a SQL Server Virtual Machine on Azure using Resource Manager](../sql/virtual-machines-windows-sql-connect.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="03dca-115">連接案例</span><span class="sxs-lookup"><span data-stu-id="03dca-115">Connection scenarios</span></span>
<span data-ttu-id="03dca-116">用戶端連接在虛擬機器上執行的 SQL Server 方式，取決於用戶端的位置與電腦/網路組態。</span><span class="sxs-lookup"><span data-stu-id="03dca-116">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the machine/networking configuration.</span></span> <span data-ttu-id="03dca-117">這些案例包括：</span><span class="sxs-lookup"><span data-stu-id="03dca-117">These scenarios include:</span></span>

* [<span data-ttu-id="03dca-118">連接相同雲端服務中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="03dca-118">Connect to SQL Server in the same cloud service</span></span>](#connect-to-sql-server-in-the-same-cloud-service)
* [<span data-ttu-id="03dca-119">連接網際網路中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="03dca-119">Connect to SQL Server over the internet</span></span>](#connect-to-sql-server-over-the-internet)
* [<span data-ttu-id="03dca-120">連接相同虛擬網路中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="03dca-120">Connect to SQL Server in the same virtual network</span></span>](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> <span data-ttu-id="03dca-121">在使用其中任一種方法來連接之前，您必須遵循 [本文章中的步驟設定連線能力](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。</span><span class="sxs-lookup"><span data-stu-id="03dca-121">Before you connect with any of these methods, you must follow the [steps in this article to configure connectivity](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>
> 
> 

### <a name="connect-to-sql-server-in-the-same-cloud-service"></a><span data-ttu-id="03dca-122">連接相同雲端服務中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="03dca-122">Connect to SQL Server in the same cloud service</span></span>
<span data-ttu-id="03dca-123">可以在相同的雲端服務中建立多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="03dca-123">Multiple virtual machines can be created in the same cloud service.</span></span> <span data-ttu-id="03dca-124">若要了解此虛擬機器案例，請參閱 [如何連接虛擬機器與虛擬網路或雲端服務](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="03dca-124">To understand this virtual machines scenario, see [How to connect virtual machines with a virtual network or cloud service](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service).</span></span> <span data-ttu-id="03dca-125">此案例為當虛擬機器上的用戶端嘗試連接到在同一個雲端服務中執行的另一部虛擬機器上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="03dca-125">This scenario is when a client on one virtual machine attempts to connect to SQL Server running on another virtual machine in the same cloud service.</span></span>

<span data-ttu-id="03dca-126">在此案例中，您可以使用 VM **名稱** (在入口網站中也稱為**電腦名稱**或**主機名稱**) 來連接。</span><span class="sxs-lookup"><span data-stu-id="03dca-126">In this scenario, you can connect using the VM **Name** (also shown as **Computer Name** or **hostname** in the portal).</span></span> <span data-ttu-id="03dca-127">這是您在建立期間提供給 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="03dca-127">This is the name you provided for the VM during creation.</span></span> <span data-ttu-id="03dca-128">例如，如果將您的 SQL VM 命名為 **mysqlvm**，則在相同雲端服務中的用戶端 VM 將可以使用下列連接字串來連接：</span><span class="sxs-lookup"><span data-stu-id="03dca-128">For example, if you named your SQL VM **mysqlvm**, a client VM in the same cloud service could use the following connection string to connect:</span></span>

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="03dca-129">連接網際網路中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="03dca-129">Connect to SQL Server over the Internet</span></span>
<span data-ttu-id="03dca-130">如果您希望透過網際網路連接您的 SQL Server 資料庫引擎，您必須建立虛擬機器端點以進行傳入 TCP 通訊。</span><span class="sxs-lookup"><span data-stu-id="03dca-130">If you want to connect to your SQL Server database engine from the Internet, you must create a virtual machine endpoint for incoming TCP communication.</span></span> <span data-ttu-id="03dca-131">此 Azure 組態步驟能將傳入 TCP 連接埠流量導向虛擬機器可存取的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="03dca-131">This Azure configuration step, directs incoming TCP port traffic to a TCP port that is accessible to the virtual machine.</span></span>

<span data-ttu-id="03dca-132">若要透過網際網路連接，您必須使用 VM 的 DNS 名稱和 VM 端點連接埠號碼 (稍後在本文中設定)。</span><span class="sxs-lookup"><span data-stu-id="03dca-132">To connect over the internet, you must use the VM's DNS name and the VM endpoint port number (configured later in this article).</span></span> <span data-ttu-id="03dca-133">若要尋找 DNS 名稱，請瀏覽至 Azure 入口網站，然後選取 [虛擬機器 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="03dca-133">To find the DNS Name, navigate to the Azure portal, and select **Virtual machines (classic)**.</span></span> <span data-ttu-id="03dca-134">然後選取您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="03dca-134">Then select your virtual machine.</span></span> <span data-ttu-id="03dca-135">[摘要] 區段中會顯示 [DNS 名稱]。</span><span class="sxs-lookup"><span data-stu-id="03dca-135">The **DNS name** is shown in the **Overview** section.</span></span>

<span data-ttu-id="03dca-136">例如，假設名為 **mysqlvm** 的傳統虛擬機器，其 DNS 名稱為 **mysqlvm7777.cloudapp.net**，且 VM 端點是 **57500**。</span><span class="sxs-lookup"><span data-stu-id="03dca-136">For example, consider a classic virtual machine named **mysqlvm** with a DNS Name of **mysqlvm7777.cloudapp.net** and a VM endpoint of **57500**.</span></span> <span data-ttu-id="03dca-137">假設已適當設定連線能力，則使用下列連接字串，就能從網際網路上任何位置存取該虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="03dca-137">Assuming properly configured connectivity, the following connection string could be used to access the virtual machine from anywhere on the internet:</span></span>

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

<span data-ttu-id="03dca-138">用戶端雖然可透過網際網路連線，但這不表示任何人都可以連接您的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="03dca-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="03dca-139">外部用戶端必須要有正確的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="03dca-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="03dca-140">為了增加安全性，請勿使用知名的 1433 連接埠做為公用虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="03dca-140">For additional security, don't use the well-known port 1433 for the public virtual machine endpoint.</span></span> <span data-ttu-id="03dca-141">請盡可能考慮在您的端點加入 ACL 來限制流量，只開放給您允許的用戶端。</span><span class="sxs-lookup"><span data-stu-id="03dca-141">And if possible, consider adding an ACL on your endpoint to restrict traffic only to the clients you permit.</span></span> <span data-ttu-id="03dca-142">如需有關在端點中使用 ACL 的指示，請參閱 [在端點上管理 ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="03dca-142">For instructions on using ACLs with endpoints, see [Manage the ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

> [!NOTE]
> <span data-ttu-id="03dca-143">請務必注意，當您使用此技術與 SQL Server 通訊時，所有從 Azure 資料中心傳出的資料都會以一般 [輸出資料傳輸價格](https://azure.microsoft.com/pricing/details/data-transfers/)計費。</span><span class="sxs-lookup"><span data-stu-id="03dca-143">It is important to note that when you use this technique to communicate with SQL Server, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>
> 
> 

### <a name="connect-to-sql-server-in-the-same-virtual-network"></a><span data-ttu-id="03dca-144">連接相同虛擬網路中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="03dca-144">Connect to SQL Server in the same virtual network</span></span>
<span data-ttu-id="03dca-145">[虛擬網路](../../../virtual-network/virtual-networks-overview.md) 讓其他案例變得可行。</span><span class="sxs-lookup"><span data-stu-id="03dca-145">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span></span> <span data-ttu-id="03dca-146">您可連接相同虛擬網路中的 VM，即使這些 VM 位於不同的雲端服務也沒關係。</span><span class="sxs-lookup"><span data-stu-id="03dca-146">You can connect VMs in the same virtual network, even if those VMs exist in different cloud services.</span></span> <span data-ttu-id="03dca-147">[站對站 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)可讓您建立能將 VM 連接至內部部署網路和電腦的混合式架構。</span><span class="sxs-lookup"><span data-stu-id="03dca-147">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="03dca-148">虛擬網路也可讓您將 Azure VM 加入網域。</span><span class="sxs-lookup"><span data-stu-id="03dca-148">Virtual networks also enables you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="03dca-149">這是在 SQL Server 使用的 Windows 驗證的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="03dca-149">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="03dca-150">其他連接案例則需要使用者名稱和密碼進行 SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="03dca-150">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="03dca-151">如果您要設定網域環境及 Windows 驗證，您就不需要使用本文中的步驟來設定公用端點或是 SQL 驗證及登入。</span><span class="sxs-lookup"><span data-stu-id="03dca-151">If you are going to configure a domain environment and Windows Authentication, you do not need to use the steps in this article to configure the public endpoint or the SQL Authentication and logins.</span></span> <span data-ttu-id="03dca-152">在此案例中，您可以在連接字串中指定 SQL Server VM 名稱來連接 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="03dca-152">In this scenario, you can connect to your SQL Server instance by specifying the SQL Server VM name in the connection string.</span></span> <span data-ttu-id="03dca-153">下列範例假設 Windows 驗證也已設定，且使用者已獲得存取 SQL Server 執行個體的權限。</span><span class="sxs-lookup"><span data-stu-id="03dca-153">The following example assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a><span data-ttu-id="03dca-154">Azure VM 中設定 SQL Server 連線的步驟</span><span class="sxs-lookup"><span data-stu-id="03dca-154">Steps for configuring SQL Server connectivity in an Azure VM</span></span>
<span data-ttu-id="03dca-155">下列步驟示範如何使用 SQL Server Management Studio (SSMS) 透過網際網路連線到 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="03dca-155">The following steps demonstrate how to connect to the SQL Server instance over the internet using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="03dca-156">不過，相同的步驟適用於讓您在內部部署或 Azure 中執行的應用程式可存取 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="03dca-156">However, the same steps apply to making your SQL Server virtual machine accessible for your applications, running both on-premises and in Azure.</span></span>

<span data-ttu-id="03dca-157">您必須先完成後續各小節描述的下列工作，才能從其他 VM 或網際網路連接 SQL Server 的執行個體：</span><span class="sxs-lookup"><span data-stu-id="03dca-157">Before you can connect to the instance of SQL Server from another VM or the internet, you must complete the following tasks as described in the sections that follow:</span></span>

* [<span data-ttu-id="03dca-158">為虛擬機器建立 TCP 端點</span><span class="sxs-lookup"><span data-stu-id="03dca-158">Create a TCP endpoint for the virtual machine</span></span>](#create-a-tcp-endpoint-for-the-virtual-machine)
* [<span data-ttu-id="03dca-159">在 Windows 防火牆中開啟 TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="03dca-159">Open TCP ports in the Windows firewall</span></span>](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [<span data-ttu-id="03dca-160">設定 SQL Server 以接聽 TCP 通訊協定</span><span class="sxs-lookup"><span data-stu-id="03dca-160">Configure SQL Server to listen on the TCP protocol</span></span>](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [<span data-ttu-id="03dca-161">設定 SQL Server 以進行混合模式驗證</span><span class="sxs-lookup"><span data-stu-id="03dca-161">Configure SQL Server for mixed mode authentication</span></span>](#configure-sql-server-for-mixed-mode-authentication)
* [<span data-ttu-id="03dca-162">建立 SQL Server 驗證登入</span><span class="sxs-lookup"><span data-stu-id="03dca-162">Create SQL Server authentication logins</span></span>](#create-sql-server-authentication-logins)
* [<span data-ttu-id="03dca-163">決定虛擬機器的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="03dca-163">Determine the DNS name of the virtual machine</span></span>](#determine-the-dns-name-of-the-virtual-machine)
* [<span data-ttu-id="03dca-164">從另一部電腦連接到 Database Engine</span><span class="sxs-lookup"><span data-stu-id="03dca-164">Connect to the Database Engine from another computer</span></span>](#connect-to-the-database-engine-from-another-computer)

<span data-ttu-id="03dca-165">連線路徑如以下圖表總結：</span><span class="sxs-lookup"><span data-stu-id="03dca-165">The connection path is summarized by the following diagram:</span></span>

![連接 SQL Server 虛擬機器](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect to SQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect to SQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect to SQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a><span data-ttu-id="03dca-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03dca-167">Next Steps</span></span>
<span data-ttu-id="03dca-168">如果您計畫針對高可用性和嚴重損壞修復使用 AlwaysOn 可用性群組，您應該考慮實作接聽程式。</span><span class="sxs-lookup"><span data-stu-id="03dca-168">If you are also planning to use AlwaysOn Availability Groups for high availability and disaster recovery, you should consider implementing a listener.</span></span> <span data-ttu-id="03dca-169">資料庫用戶端會連接至接聽程式，而非直接連接其中一個 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="03dca-169">Database clients connect to the listener rather than directly to one of the SQL Server instances.</span></span> <span data-ttu-id="03dca-170">接聽程式路由傳送用戶端至可用性群組中的主要複本。</span><span class="sxs-lookup"><span data-stu-id="03dca-170">The listener routes clients to the primary replica in the availability group.</span></span> <span data-ttu-id="03dca-171">如需詳細資訊，請參閱 [設定 Azure 中 AlwaysOn 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="03dca-171">For more information, see [Configure an ILB listener for AlwaysOn Availability Groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="03dca-172">請務必檢閱在 Azure 虛擬機器上執行之 SQL Server 的所有安全性最佳做法。</span><span class="sxs-lookup"><span data-stu-id="03dca-172">It is important to review all of the security best practices for SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="03dca-173">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 安全性考量](../sql/virtual-machines-windows-sql-security.md)。</span><span class="sxs-lookup"><span data-stu-id="03dca-173">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).</span></span>

<span data-ttu-id="03dca-174">[探索學習路徑](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) ：Azure 虛擬機器上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="03dca-174">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span> 

<span data-ttu-id="03dca-175">如需有關在 Azure VM 中執行 SQL Server 的其他主題，請參閱 [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="03dca-175">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

