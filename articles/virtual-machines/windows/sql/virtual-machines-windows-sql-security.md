---
title: "在 Azure 中的 SQL Server 的考量 aaaSecurity |Microsoft 文件"
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
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a><span data-ttu-id="64517-103">Azure 虛擬機器中的 SQL Server 安全性考量</span><span class="sxs-lookup"><span data-stu-id="64517-103">Security Considerations for SQL Server in Azure Virtual Machines</span></span>

<span data-ttu-id="64517-104">本主題包含協助建立 Azure 虛擬機器 (VM) 中的安全存取 tooSQL 伺服器執行個體的整體安全性指導方針。</span><span class="sxs-lookup"><span data-stu-id="64517-104">This topic includes overall security guidelines that help establish secure access tooSQL Server instances in an Azure virtual machine (VM).</span></span>

<span data-ttu-id="64517-105">Azure 符合多種業界規範及標準，可讓您 toobuild 相容解決方案與 SQL Server 虛擬機器中執行。</span><span class="sxs-lookup"><span data-stu-id="64517-105">Azure complies with several industry regulations and standards that can enable you toobuild a compliant solution with SQL Server running in a virtual machine.</span></span> <span data-ttu-id="64517-106">如需 Azure 的法規相符性資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/)。</span><span class="sxs-lookup"><span data-stu-id="64517-106">For information about regulatory compliance with Azure, see [Azure Trust Center](https://azure.microsoft.com/support/trust-center/).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a><span data-ttu-id="64517-107">控制存取 toohello SQL VM</span><span class="sxs-lookup"><span data-stu-id="64517-107">Control access toohello SQL VM</span></span>

<span data-ttu-id="64517-108">當您建立您的 SQL Server 虛擬機器時，請考慮如何 toocarefully 控制誰可以存取 toohello 電腦和 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="64517-108">When you create your SQL Server virtual machine, consider how toocarefully control who has access toohello machine and tooSQL Server.</span></span> <span data-ttu-id="64517-109">一般情況下，您應該做下列 hello:</span><span class="sxs-lookup"><span data-stu-id="64517-109">In general, you should do hello following:</span></span>

- <span data-ttu-id="64517-110">限制存取 tooSQL 伺服器 tooonly hello 應用程式與需要的用戶端。</span><span class="sxs-lookup"><span data-stu-id="64517-110">Restrict access tooSQL Server tooonly hello applications and clients that need it.</span></span>
- <span data-ttu-id="64517-111">遵循用來管理使用者帳戶和密碼的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="64517-111">Follow best practices for managing user accounts and passwords.</span></span>

<span data-ttu-id="64517-112">下列各節的 hello 考慮這些點上提供建議。</span><span class="sxs-lookup"><span data-stu-id="64517-112">hello following sections provide suggestions on thinking through these points.</span></span>

## <a name="secure-connections"></a><span data-ttu-id="64517-113">安全連線</span><span class="sxs-lookup"><span data-stu-id="64517-113">Secure connections</span></span>

<span data-ttu-id="64517-114">當您建立 SQL Server 虛擬機器圖庫映像時，hello **SQL Server 連接性**選項可讓您 hello 選擇**（在 VM) 內本機**，**私用 （在虛擬網路）**，或**公用 （網際網路）**。</span><span class="sxs-lookup"><span data-stu-id="64517-114">When you create a SQL Server virtual machine with a gallery image, hello **SQL Server Connectivity** option gives you hello choice of **Local (inside VM)**, **Private (within Virtual Network)**, or **Public (Internet)**.</span></span>

![SQL Server 連線](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

<span data-ttu-id="64517-116">Hello 最佳的安全性，請選擇 hello 最嚴格的選項，您的案例。</span><span class="sxs-lookup"><span data-stu-id="64517-116">For hello best security, choose hello most restrictive option for your scenario.</span></span> <span data-ttu-id="64517-117">例如，如果您正在存取 SQL Server 的應用程式然後 hello 相同的 VM**本機**hello 最安全的選擇。</span><span class="sxs-lookup"><span data-stu-id="64517-117">For example, if you are running an application that accesses SQL Server on hello same VM, then **Local** is hello most secure choice.</span></span> <span data-ttu-id="64517-118">如果您正在執行的 Azure 應用程式需要存取 toohello SQL Server，然後**私人**保護通訊 tooSQL 伺服器只在指定的 hello [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="64517-118">If you are running an Azure application that requires access toohello SQL Server, then **Private** secures communication tooSQL Server only within hello specified [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="64517-119">如果您需要**公用**(internest) 存取 toohello SQL Server VM，然後請確定 toofollow 其他最佳作法在這個主題 tooreduce 攻擊面。</span><span class="sxs-lookup"><span data-stu-id="64517-119">If you require **Public** (internest) access toohello SQL Server VM, then make sure toofollow other best practices in this topic tooreduce your attack surface area.</span></span>

<span data-ttu-id="64517-120">hello hello 入口網站中選取的選項使用連入的安全性規則 hello Vm 上[網路安全性群組](../../../virtual-network/virtual-networks-nsg.md)(NSG) tooallow 或拒絕網路流量 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="64517-120">hello selected options in hello portal use inbound security rules on hello VMs [Network Security Group](../../../virtual-network/virtual-networks-nsg.md) (NSG) tooallow or deny network traffic tooyour virtual machine.</span></span> <span data-ttu-id="64517-121">您可以修改或建立新的輸入的 NSG 規則 tooallow 流量 toohello SQL Server 連接埠 （預設值 1433年）。</span><span class="sxs-lookup"><span data-stu-id="64517-121">You can modify or create new inbound NSG rules tooallow traffic toohello SQL Server port (default 1433).</span></span> <span data-ttu-id="64517-122">您也可以指定特定 toocommunicate 允許透過此連接埠的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="64517-122">You can also specify specific IP addresses that are allowed toocommunicate over this port.</span></span>

![網路安全性群組規則](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

<span data-ttu-id="64517-124">此外 tooNSG 規則 toorestrict 網路流量，您也可以使用 Windows 防火牆 hello hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="64517-124">In addition tooNSG rules toorestrict network traffic, you can also use hello Windows Firewall on hello virtual machine.</span></span>

<span data-ttu-id="64517-125">如果您使用端點與 hello 傳統部署模型，移除 hello 虛擬機器上的任何端點，如果您不要使用它們。</span><span class="sxs-lookup"><span data-stu-id="64517-125">If you are using endpoints with hello classic deployment model, remove any endpoints on hello virtual machine if you do not use them.</span></span> <span data-ttu-id="64517-126">如需有關使用具有端點 Acl 的指示，請參閱[端點上的管理 hello ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="64517-126">For instructions on using ACLs with endpoints, see [Manage hello ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span> <span data-ttu-id="64517-127">不需要使用 hello 資源管理員的 Vm。</span><span class="sxs-lookup"><span data-stu-id="64517-127">This is not necessary for VMs that use hello Resource Manager.</span></span>

<span data-ttu-id="64517-128">最後，請考慮啟用 hello Azure 的虛擬機器中的 hello SQL Server Database Engine 執行個體的加密的連接。</span><span class="sxs-lookup"><span data-stu-id="64517-128">Finally, consider enabling encrypted connections for hello instance of hello SQL Server Database Engine in your Azure virtual machine.</span></span> <span data-ttu-id="64517-129">使用簽署的憑證設定 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="64517-129">Configure SQL server instance with a signed certificate.</span></span> <span data-ttu-id="64517-130">如需詳細資訊，請參閱[啟用加密連接 toohello Database Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine)和[連接字串語法](https://msdn.microsoft.com/library/ms254500.aspx)。</span><span class="sxs-lookup"><span data-stu-id="64517-130">For more information, see [Enable Encrypted Connections toohello Database Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) and [Connection String Syntax](https://msdn.microsoft.com/library/ms254500.aspx).</span></span>

## <a name="use-a-non-default-port"></a><span data-ttu-id="64517-131">使用非預設連接埠</span><span class="sxs-lookup"><span data-stu-id="64517-131">Use a non-default port</span></span>

<span data-ttu-id="64517-132">根據預設，SQL Server 會在已知的通訊埠 1433 上接聽。</span><span class="sxs-lookup"><span data-stu-id="64517-132">By default, SQL Server listens on a well-known port, 1433.</span></span> <span data-ttu-id="64517-133">為了提高安全性，請在非預設連接埠，例如 1401年上設定 SQL Server toolisten。</span><span class="sxs-lookup"><span data-stu-id="64517-133">For increased security, configure SQL Server toolisten on a non-default port, such as 1401.</span></span> <span data-ttu-id="64517-134">如果您佈建 hello Azure 入口網站中的 SQL Server 組件庫映像，您可以指定此連接埠 hello **SQL Server 設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64517-134">If you provision a SQL Server gallery image in hello Azure portal, you can specify this port in hello **SQL Server settings** blade.</span></span>

<span data-ttu-id="64517-135">tooconfigure 此佈建之後，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="64517-135">tooconfigure this after provisioning, you have two options:</span></span>

- <span data-ttu-id="64517-136">針對資源管理員的 Vm，您可以選取**SQL Server 組態**從 hello VM 概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64517-136">For Resource Manager VMs, you can select **SQL Server configuration** from hello VM overview blade.</span></span> <span data-ttu-id="64517-137">這可讓選擇 toochange hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="64517-137">This provides an option toochange hello port.</span></span>

  ![在入口網站中變更 TCP 連接埠](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- <span data-ttu-id="64517-139">傳統的 Vm 或 hello 入口網站未佈建的 SQL Server Vm，您可以從遠端連線 toohello VM 來手動設定 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="64517-139">For Classic VMs or for SQL Server VMs that were not provisioned with hello portal, you can manually configure hello port by connecting remotely toohello VM.</span></span> <span data-ttu-id="64517-140">Hello 組態步驟，請參閱[特定 TCP 通訊埠上設定伺服器 tooListen](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。</span><span class="sxs-lookup"><span data-stu-id="64517-140">For hello configuration steps, see [Configure a Server tooListen on a Specific TCP Port](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).</span></span> <span data-ttu-id="64517-141">如果您使用此手動技巧，您也需要 tooadd Windows 防火牆規則 tooallow 連入流量的 TCP 連接埠上。</span><span class="sxs-lookup"><span data-stu-id="64517-141">If you use this manual technique, you also need tooadd a Windows Firewall rule tooallow incoming traffic on that TCP port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64517-142">指定非預設連接埠是個不錯的主意，如果您的 SQL Server 連接埠是開啟 toopublic 網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="64517-142">Specifying a non-default port is a good idea if your SQL Server port is open toopublic internet connections.</span></span>

<span data-ttu-id="64517-143">SQL Server 是在非預設連接埠上接聽，您必須指定 hello 連接埠，當您連線時。</span><span class="sxs-lookup"><span data-stu-id="64517-143">When SQL Server is listening on a non-default port, you must specify hello port when you connect.</span></span> <span data-ttu-id="64517-144">例如，假設其中 hello 伺服器 IP 位址是 13.55.255.255，而 SQL Server 接聽連接埠 1401年。</span><span class="sxs-lookup"><span data-stu-id="64517-144">For example, consider a scenario where hello server IP address is 13.55.255.255 and SQL Server is listening on port 1401.</span></span> <span data-ttu-id="64517-145">tooconnect tooSQL 伺服器，您會指定`13.55.255.255,1401`hello 連接字串中。</span><span class="sxs-lookup"><span data-stu-id="64517-145">tooconnect tooSQL Server, you would specify `13.55.255.255,1401` in hello connection string.</span></span>

## <a name="manage-accounts"></a><span data-ttu-id="64517-146">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="64517-146">Manage accounts</span></span>

<span data-ttu-id="64517-147">您不想攻擊者 tooeasily 猜測帳戶名稱或密碼。</span><span class="sxs-lookup"><span data-stu-id="64517-147">You don't want attackers tooeasily guess account names or passwords.</span></span> <span data-ttu-id="64517-148">使用下列秘訣 toohelp hello:</span><span class="sxs-lookup"><span data-stu-id="64517-148">Use hello following tips toohelp:</span></span>

- <span data-ttu-id="64517-149">建立不是名為 **Administrator**的唯一本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="64517-149">Create a unique local administrator account that is not named **Administrator**.</span></span>

- <span data-ttu-id="64517-150">為您的所有帳戶使用複雜的強式密碼。</span><span class="sxs-lookup"><span data-stu-id="64517-150">Use complex strong passwords for all your accounts.</span></span> <span data-ttu-id="64517-151">如需有關如何 toocreate 強式密碼，請參閱[建立強式密碼](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password)發行項。</span><span class="sxs-lookup"><span data-stu-id="64517-151">For more information about how toocreate a strong password, see [Create a strong password](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) article.</span></span>

- <span data-ttu-id="64517-152">根據預設，Azure 會在 SQL Server 虛擬機器安裝期間選取 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="64517-152">By default, Azure selects Windows Authentication during SQL Server Virtual Machine setup.</span></span> <span data-ttu-id="64517-153">因此，hello **SA**已停用登入和安裝程式會指派密碼。</span><span class="sxs-lookup"><span data-stu-id="64517-153">Therefore, hello **SA** login is disabled and a password is assigned by setup.</span></span> <span data-ttu-id="64517-154">我們建議您該 hello **SA**登入不應該用或啟用。</span><span class="sxs-lookup"><span data-stu-id="64517-154">We recommend that hello **SA** login should not be used or enabled.</span></span> <span data-ttu-id="64517-155">如果您必須具有 SQL 登入，請使用下列策略 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="64517-155">If you must have a SQL login, use one of hello following strategies:</span></span>

  - <span data-ttu-id="64517-156">使用具有 **sysadmin** 成員資格的唯一名稱建立 SQL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="64517-156">Create a SQL account with a unique name that has **sysadmin** membership.</span></span> <span data-ttu-id="64517-157">您可以從 hello 入口網站啟用**SQL 驗證**佈建期間。</span><span class="sxs-lookup"><span data-stu-id="64517-157">You can do this from hello portal by enabling **SQL Authentication** during provisioning.</span></span>

    > [!TIP] 
    > <span data-ttu-id="64517-158">如果您在佈建期間未啟用 SQL 驗證，您必須手動變更 hello 驗證模式太**SQL Server 和 Windows 驗證模式**。</span><span class="sxs-lookup"><span data-stu-id="64517-158">If you do not enable SQL Authentication during provisioning, you must manually change hello authentication mode too**SQL Server and Windows Authentication Mode**.</span></span> <span data-ttu-id="64517-159">如需詳細資訊，請參閱 [變更伺服器驗證模式](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode)。</span><span class="sxs-lookup"><span data-stu-id="64517-159">For more information, see [Change Server Authentication Mode](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).</span></span>

  - <span data-ttu-id="64517-160">如果您必須使用 hello **SA**登入，啟用 hello 登入之後佈建並指派新的增強式密碼。</span><span class="sxs-lookup"><span data-stu-id="64517-160">If you must use hello **SA** login, enable hello login after provisioning and assign a new strong password.</span></span>

## <a name="follow-on-premises-best-practices"></a><span data-ttu-id="64517-161">遵循內部部署最佳做法</span><span class="sxs-lookup"><span data-stu-id="64517-161">Follow on-premises best practices</span></span>

<span data-ttu-id="64517-162">此外，本主題中所述的 toohello 作法建議您檢閱並實作 hello 傳統內部部署安全性作法，在適用情況。</span><span class="sxs-lookup"><span data-stu-id="64517-162">In addition toohello practices described in this topic, we recommend that you review and implement hello traditional on-premises security practices where applicable.</span></span> <span data-ttu-id="64517-163">如需詳細資訊，請參閱 [SQL Server 安裝的安全性考量](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)</span><span class="sxs-lookup"><span data-stu-id="64517-163">For more information, see [Security Considerations for a SQL Server Installation](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="64517-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64517-164">Next Steps</span></span>

<span data-ttu-id="64517-165">如果您也想了解關於效能的最佳作法，請參閱 [Azure 虛擬機器中 SQL Server 的效能最佳作法](virtual-machines-windows-sql-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="64517-165">If you are also interested in best practices around performance, see [Performance Best Practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="64517-166">如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="64517-166">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

