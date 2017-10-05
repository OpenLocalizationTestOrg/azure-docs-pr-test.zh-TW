---
title: "Azure 中的 SQL Server 安全性考量 | Microsoft Docs"
description: "本主題提供一般指導方針來保護在 Azure 虛擬機器中執行的 SQL Server。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 4ad9156e481eac0bae32bca35a2b126363e5d8b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a><span data-ttu-id="8e272-103">Azure 虛擬機器中的 SQL Server 安全性考量</span><span class="sxs-lookup"><span data-stu-id="8e272-103">Security Considerations for SQL Server in Azure Virtual Machines</span></span>

<span data-ttu-id="8e272-104">本主題包含整體安全性指導方針，可協助制定 Azure 虛擬機器 (VM) 中 SQL Server 執行個體的存取安全。</span><span class="sxs-lookup"><span data-stu-id="8e272-104">This topic includes overall security guidelines that help establish secure access to SQL Server instances in an Azure virtual machine (VM).</span></span>

<span data-ttu-id="8e272-105">Azure 符合多種業界規範及標準，可讓您使用在虛擬機器中執行的 SQL Server，建置相容的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8e272-105">Azure complies with several industry regulations and standards that can enable you to build a compliant solution with SQL Server running in a virtual machine.</span></span> <span data-ttu-id="8e272-106">如需 Azure 的法規相符性資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/)。</span><span class="sxs-lookup"><span data-stu-id="8e272-106">For information about regulatory compliance with Azure, see [Azure Trust Center](https://azure.microsoft.com/support/trust-center/).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-to-the-sql-vm"></a><span data-ttu-id="8e272-107">控制 SQL VM 的存取</span><span class="sxs-lookup"><span data-stu-id="8e272-107">Control access to the SQL VM</span></span>

<span data-ttu-id="8e272-108">當您建立 SQL Server 虛擬機器時，請考慮如何仔細控制誰可以存取電腦和 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="8e272-108">When you create your SQL Server virtual machine, consider how to carefully control who has access to the machine and to SQL Server.</span></span> <span data-ttu-id="8e272-109">一般而言，您應該執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="8e272-109">In general, you should do the following:</span></span>

- <span data-ttu-id="8e272-110">將 SQL Server 的存取只限於需要它的應用程式和用戶端。</span><span class="sxs-lookup"><span data-stu-id="8e272-110">Restrict access to SQL Server to only the applications and clients that need it.</span></span>
- <span data-ttu-id="8e272-111">遵循用來管理使用者帳戶和密碼的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="8e272-111">Follow best practices for managing user accounts and passwords.</span></span>

<span data-ttu-id="8e272-112">下列各節提供逐一考量這些點的建議。</span><span class="sxs-lookup"><span data-stu-id="8e272-112">The following sections provide suggestions on thinking through these points.</span></span>

## <a name="secure-connections"></a><span data-ttu-id="8e272-113">安全連線</span><span class="sxs-lookup"><span data-stu-id="8e272-113">Secure connections</span></span>

<span data-ttu-id="8e272-114">當您使用資源庫映像建立 SQL Server 虛擬機器時，[SQL Server 連線] 選項可讓您選擇 [本機 (在 VM 內)][私人 (在虛擬網路內)] 或 [公用 (網際網路)]。</span><span class="sxs-lookup"><span data-stu-id="8e272-114">When you create a SQL Server virtual machine with a gallery image, the **SQL Server Connectivity** option gives you the choice of **Local (inside VM)**, **Private (within Virtual Network)**, or **Public (Internet)**.</span></span>

![SQL Server 連線](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

<span data-ttu-id="8e272-116">如需最佳的安全性，請為您的案例選擇最嚴格的選項。</span><span class="sxs-lookup"><span data-stu-id="8e272-116">For the best security, choose the most restrictive option for your scenario.</span></span> <span data-ttu-id="8e272-117">例如，如果您執行的應用程式可存取相同 VM 上的 SQL Server，則 [本機] 是最安全的選擇。</span><span class="sxs-lookup"><span data-stu-id="8e272-117">For example, if you are running an application that accesses SQL Server on the same VM, then **Local** is the most secure choice.</span></span> <span data-ttu-id="8e272-118">如果您執行的 Azure 應用程式需要存取 SQL Server，則 [私人] 只可保護指定之 [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md) 內的 SQL Server 通訊。</span><span class="sxs-lookup"><span data-stu-id="8e272-118">If you are running an Azure application that requires access to the SQL Server, then **Private** secures communication to SQL Server only within the specified [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="8e272-119">如果您需要 SQL Server VM的 [公用] \(網際網路) 存取，請務必遵循本主題中的其他最佳做法，以縮寫受攻擊面。</span><span class="sxs-lookup"><span data-stu-id="8e272-119">If you require **Public** (internest) access to the SQL Server VM, then make sure to follow other best practices in this topic to reduce your attack surface area.</span></span>

<span data-ttu-id="8e272-120">入口網站中選取的選項會使用 VM [網路安全性群組](../../../virtual-network/virtual-networks-nsg.md) (NSG) 上的輸入安全性規則來允許或拒絕虛擬機器的網路流量。</span><span class="sxs-lookup"><span data-stu-id="8e272-120">The selected options in the portal use inbound security rules on the VMs [Network Security Group](../../../virtual-network/virtual-networks-nsg.md) (NSG) to allow or deny network traffic to your virtual machine.</span></span> <span data-ttu-id="8e272-121">您可以修改或建立新的輸入 NSG 規則，以允許 SQL Server 連接埠 (預設值 1433) 的流量。</span><span class="sxs-lookup"><span data-stu-id="8e272-121">You can modify or create new inbound NSG rules to allow traffic to the SQL Server port (default 1433).</span></span> <span data-ttu-id="8e272-122">您也可以指定允許透過此連接埠通訊的特定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8e272-122">You can also specify specific IP addresses that are allowed to communicate over this port.</span></span>

![網路安全性群組規則](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

<span data-ttu-id="8e272-124">除了可限制網路流量的 NSG 規則，您也可以在虛擬機器上使用 Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="8e272-124">In addition to NSG rules to restrict network traffic, you can also use the Windows Firewall on the virtual machine.</span></span>

<span data-ttu-id="8e272-125">使用您使用端點搭配傳統部署模型，如果虛擬機器上有任何不使用的端點，請將它們全部移除。</span><span class="sxs-lookup"><span data-stu-id="8e272-125">If you are using endpoints with the classic deployment model, remove any endpoints on the virtual machine if you do not use them.</span></span> <span data-ttu-id="8e272-126">如需有關在端點中使用 ACL 的指示，請參閱 [在端點上管理 ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="8e272-126">For instructions on using ACLs with endpoints, see [Manage the ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span> <span data-ttu-id="8e272-127">使用 Resource Manager 的 VM 不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="8e272-127">This is not necessary for VMs that use the Resource Manager.</span></span>

<span data-ttu-id="8e272-128">最後，請考慮對 Azure 虛擬機器中的 SQL Server Database Engine 執行個體啟用已加密的連線。</span><span class="sxs-lookup"><span data-stu-id="8e272-128">Finally, consider enabling encrypted connections for the instance of the SQL Server Database Engine in your Azure virtual machine.</span></span> <span data-ttu-id="8e272-129">使用簽署的憑證設定 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="8e272-129">Configure SQL server instance with a signed certificate.</span></span> <span data-ttu-id="8e272-130">如需詳細資訊，請參閱[啟用 Database Engine 的加密連接](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine)和[連接字串語法](https://msdn.microsoft.com/library/ms254500.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e272-130">For more information, see [Enable Encrypted Connections to the Database Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) and [Connection String Syntax](https://msdn.microsoft.com/library/ms254500.aspx).</span></span>

## <a name="use-a-non-default-port"></a><span data-ttu-id="8e272-131">使用非預設連接埠</span><span class="sxs-lookup"><span data-stu-id="8e272-131">Use a non-default port</span></span>

<span data-ttu-id="8e272-132">根據預設，SQL Server 會在已知的通訊埠 1433 上接聽。</span><span class="sxs-lookup"><span data-stu-id="8e272-132">By default, SQL Server listens on a well-known port, 1433.</span></span> <span data-ttu-id="8e272-133">為了提高安全性，將 SQL Server 設定為在非預設連接埠 (例如 1401) 上接聽。</span><span class="sxs-lookup"><span data-stu-id="8e272-133">For increased security, configure SQL Server to listen on a non-default port, such as 1401.</span></span> <span data-ttu-id="8e272-134">如果您在 Azure 入口網站中佈建 SQL Server 資源庫映像，您可以在 [SQL Server 設定] 刀鋒視窗中指定此連接埠。</span><span class="sxs-lookup"><span data-stu-id="8e272-134">If you provision a SQL Server gallery image in the Azure portal, you can specify this port in the **SQL Server settings** blade.</span></span>

<span data-ttu-id="8e272-135">若要在佈建後進行此設定，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="8e272-135">To configure this after provisioning, you have two options:</span></span>

- <span data-ttu-id="8e272-136">對於 Resource Manager VM，您可以從 VM 概觀刀鋒視窗選取 [SQL Server 組態]。</span><span class="sxs-lookup"><span data-stu-id="8e272-136">For Resource Manager VMs, you can select **SQL Server configuration** from the VM overview blade.</span></span> <span data-ttu-id="8e272-137">這可提供變更連接埠的選項。</span><span class="sxs-lookup"><span data-stu-id="8e272-137">This provides an option to change the port.</span></span>

  ![在入口網站中變更 TCP 連接埠](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- <span data-ttu-id="8e272-139">對於傳統 VM 或不是透過入口網站的 SQL Server VM，您可以從遠端連線至 VM 來手動設定連接埠。</span><span class="sxs-lookup"><span data-stu-id="8e272-139">For Classic VMs or for SQL Server VMs that were not provisioned with the portal, you can manually configure the port by connecting remotely to the VM.</span></span> <span data-ttu-id="8e272-140">如需設定步驟，請參閱[設定伺服器以在特定 TCP 通訊埠上接聽](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。</span><span class="sxs-lookup"><span data-stu-id="8e272-140">For the configuration steps, see [Configure a Server to Listen on a Specific TCP Port](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).</span></span> <span data-ttu-id="8e272-141">如果您使用此手動技巧，您也需要新增 Windows 防火牆規則，以允許該 TCP 連接埠的連入流量。</span><span class="sxs-lookup"><span data-stu-id="8e272-141">If you use this manual technique, you also need to add a Windows Firewall rule to allow incoming traffic on that TCP port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e272-142">如果您的 SQL Server 連接埠已對公用網際網路連線開啟，則指定非預設連接埠是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="8e272-142">Specifying a non-default port is a good idea if your SQL Server port is open to public internet connections.</span></span>

<span data-ttu-id="8e272-143">當 SQL Server 在非預設連接埠上接聽時，您必須在連線時指定連接埠。</span><span class="sxs-lookup"><span data-stu-id="8e272-143">When SQL Server is listening on a non-default port, you must specify the port when you connect.</span></span> <span data-ttu-id="8e272-144">例如，考量伺服器 IP 位址為 13.55.255.255，且 SQL Server 在連接埠 1401 上接聽的案例。</span><span class="sxs-lookup"><span data-stu-id="8e272-144">For example, consider a scenario where the server IP address is 13.55.255.255 and SQL Server is listening on port 1401.</span></span> <span data-ttu-id="8e272-145">若要連線到 SQL Server，您會在連接字串中指定 `13.55.255.255,1401`。</span><span class="sxs-lookup"><span data-stu-id="8e272-145">To connect to SQL Server, you would specify `13.55.255.255,1401` in the connection string.</span></span>

## <a name="manage-accounts"></a><span data-ttu-id="8e272-146">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="8e272-146">Manage accounts</span></span>

<span data-ttu-id="8e272-147">您不希望攻擊者容易猜到帳戶名稱或密碼。</span><span class="sxs-lookup"><span data-stu-id="8e272-147">You don't want attackers to easily guess account names or passwords.</span></span> <span data-ttu-id="8e272-148">使用下列秘訣來協助：</span><span class="sxs-lookup"><span data-stu-id="8e272-148">Use the following tips to help:</span></span>

- <span data-ttu-id="8e272-149">建立不是名為 **Administrator**的唯一本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e272-149">Create a unique local administrator account that is not named **Administrator**.</span></span>

- <span data-ttu-id="8e272-150">為您的所有帳戶使用複雜的強式密碼。</span><span class="sxs-lookup"><span data-stu-id="8e272-150">Use complex strong passwords for all your accounts.</span></span> <span data-ttu-id="8e272-151">如需如何建立強式密碼的詳細資訊，請參閱 [建立強式密碼](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password)一文。</span><span class="sxs-lookup"><span data-stu-id="8e272-151">For more information about how to create a strong password, see [Create a strong password](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) article.</span></span>

- <span data-ttu-id="8e272-152">根據預設，Azure 會在 SQL Server 虛擬機器安裝期間選取 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="8e272-152">By default, Azure selects Windows Authentication during SQL Server Virtual Machine setup.</span></span> <span data-ttu-id="8e272-153">因此，系統會停用 **SA** 登入，並由安裝程式指派密碼。</span><span class="sxs-lookup"><span data-stu-id="8e272-153">Therefore, the **SA** login is disabled and a password is assigned by setup.</span></span> <span data-ttu-id="8e272-154">我們建議不要使用或啟用 **SA** 登入。</span><span class="sxs-lookup"><span data-stu-id="8e272-154">We recommend that the **SA** login should not be used or enabled.</span></span> <span data-ttu-id="8e272-155">如果您必須具有 SQL 登入，請使用下列其中一個策略：</span><span class="sxs-lookup"><span data-stu-id="8e272-155">If you must have a SQL login, use one of the following strategies:</span></span>

  - <span data-ttu-id="8e272-156">使用具有 **sysadmin** 成員資格的唯一名稱建立 SQL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e272-156">Create a SQL account with a unique name that has **sysadmin** membership.</span></span> <span data-ttu-id="8e272-157">在佈建期間啟用 **SQL 驗證**，即可從入口網站執行此作業。</span><span class="sxs-lookup"><span data-stu-id="8e272-157">You can do this from the portal by enabling **SQL Authentication** during provisioning.</span></span>

    > [!TIP] 
    > <span data-ttu-id="8e272-158">如果您未在佈建期間啟用 SQL 驗證，您必須將驗證模式手動變更為 **SQL Server 和 Windows 驗證模式**。</span><span class="sxs-lookup"><span data-stu-id="8e272-158">If you do not enable SQL Authentication during provisioning, you must manually change the authentication mode to **SQL Server and Windows Authentication Mode**.</span></span> <span data-ttu-id="8e272-159">如需詳細資訊，請參閱 [變更伺服器驗證模式](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode)。</span><span class="sxs-lookup"><span data-stu-id="8e272-159">For more information, see [Change Server Authentication Mode](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).</span></span>

  - <span data-ttu-id="8e272-160">如果您必須使用 **SA** 登入，請在佈建後啟用此登入，然後指派新的強式密碼。</span><span class="sxs-lookup"><span data-stu-id="8e272-160">If you must use the **SA** login, enable the login after provisioning and assign a new strong password.</span></span>

## <a name="follow-on-premises-best-practices"></a><span data-ttu-id="8e272-161">遵循內部部署最佳做法</span><span class="sxs-lookup"><span data-stu-id="8e272-161">Follow on-premises best practices</span></span>

<span data-ttu-id="8e272-162">除了本主題中所述的作法，建議您檢閱並實作適用的傳統內部部署安全性作法。</span><span class="sxs-lookup"><span data-stu-id="8e272-162">In addition to the practices described in this topic, we recommend that you review and implement the traditional on-premises security practices where applicable.</span></span> <span data-ttu-id="8e272-163">如需詳細資訊，請參閱 [SQL Server 安裝的安全性考量](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)</span><span class="sxs-lookup"><span data-stu-id="8e272-163">For more information, see [Security Considerations for a SQL Server Installation](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e272-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e272-164">Next Steps</span></span>

<span data-ttu-id="8e272-165">如果您也想了解關於效能的最佳作法，請參閱 [Azure 虛擬機器中 SQL Server 的效能最佳作法](virtual-machines-windows-sql-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="8e272-165">If you are also interested in best practices around performance, see [Performance Best Practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="8e272-166">如需在 Azure VM 中執行 SQL Server 的其他相關主題，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8e272-166">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

