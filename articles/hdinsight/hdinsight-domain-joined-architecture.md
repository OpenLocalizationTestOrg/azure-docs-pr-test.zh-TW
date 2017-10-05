---
title: "已加入網域的 Azure HDInsight 架構 | Microsoft Docs"
description: "了解如何規劃已加入網域的 HDInsight。"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 7e34f47f09466a40993b4cc797ff1cad2bdaeafe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="0a981-103">規劃 HDInsight 中已加入網域的 Azure Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="0a981-103">Plan Azure domain-joined Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="0a981-104">傳統的 Hadoop 是單一使用者叢集。</span><span class="sxs-lookup"><span data-stu-id="0a981-104">The traditional Hadoop is a single-user cluster.</span></span> <span data-ttu-id="0a981-105">它適合大部分以小型應用程式團隊建置大型資料工作負載的公司。</span><span class="sxs-lookup"><span data-stu-id="0a981-105">It is suitable for most companies that have smaller application teams building large data workloads.</span></span> <span data-ttu-id="0a981-106">隨著 Hadoop 日益普及，許多企業都轉而採用由 IT 團隊管理叢集，且多個應用程式團隊共用叢集的模式。</span><span class="sxs-lookup"><span data-stu-id="0a981-106">As Hadoop gains popularity, many enterprises are moving toward a model in which clusters are managed by IT teams and multiple application teams share clusters.</span></span> <span data-ttu-id="0a981-107">因此，Azure HDInsight 中呼聲最高的就是涉及多使用者叢集的功能。</span><span class="sxs-lookup"><span data-stu-id="0a981-107">Thus, functionalities involving multiuser clusters are among the most requested functionalities in Azure HDInsight.</span></span>

<span data-ttu-id="0a981-108">HDInsight 不會建置自己的多使用者驗證和授權，而是依賴最受歡迎的識別提供者 – Active Directory (AD)。</span><span class="sxs-lookup"><span data-stu-id="0a981-108">Instead of building its own multiuser authentication and authorization, HDInsight relies on the most popular identity provider--Active Directory (AD).</span></span> <span data-ttu-id="0a981-109">AD 強大的安全性功能可用來管理 HDInsight 中的多使用者授權。</span><span class="sxs-lookup"><span data-stu-id="0a981-109">The powerful security functionality in AD can be used to manage multiuser authorization in HDInsight.</span></span> <span data-ttu-id="0a981-110">藉由整合 HDInsight 與 AD，您可以使用 AD 認證來與叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="0a981-110">By integrating HDInsight with AD, you can communicate with the clusters by using your AD credentials.</span></span> <span data-ttu-id="0a981-111">HDInsight 會將 AD 使用者對應至本機 Hadoop 使用者，讓通過驗證的使用者能在 HDInsight 上順暢地執行 Ambari、Hive 伺服器、Ranger、Spark Thrift 伺服器等所有服務。</span><span class="sxs-lookup"><span data-stu-id="0a981-111">HDInsight maps an AD user to a local Hadoop user, so all the services running on HDInsight (Ambari, Hive server, Ranger, Spark thrift server, and others) work seamlessly for the authenticated user.</span></span>

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a><span data-ttu-id="0a981-112">整合 HDInsight 與 AD 和 IaaS VM 上的 AD</span><span class="sxs-lookup"><span data-stu-id="0a981-112">Integrate HDInsight with AD and AD on IaaS VM</span></span>

<span data-ttu-id="0a981-113">藉由整合 HDInsight 與 Azure AD 或 IaaS VM 上的 AD，HDInsight 叢集節點會加入網域。</span><span class="sxs-lookup"><span data-stu-id="0a981-113">By integrating HDInsight with Azure AD or AD on Iaas VM, the HDInsight cluster nodes are domain-joined to a domain.</span></span> <span data-ttu-id="0a981-114">HDInsight 會針對在叢集上執行的 Hadoop 服務建立服務主體，並將它們放在 Azure AD 或 IaaS VM 上的 AD 中指定的組織單位 (OU) 內。</span><span class="sxs-lookup"><span data-stu-id="0a981-114">HDInsight creates service principals for the Hadoop services running on the cluster and places them within a specified organizational unit (OU) in Azure AD or AD on IaaS VM.</span></span> <span data-ttu-id="0a981-115">HDInsight 也會針對加入網域的節點 IP 位址，在網域中建立反向 DNS 對應。</span><span class="sxs-lookup"><span data-stu-id="0a981-115">HDInsight also creates reverse DNS mappings in the domain for the IP addresses of the nodes that are joined to the domain.</span></span>

<span data-ttu-id="0a981-116">您可以使用多個架構來達到這種設定。</span><span class="sxs-lookup"><span data-stu-id="0a981-116">You can achieve this setup by using multiple architectures.</span></span> <span data-ttu-id="0a981-117">您可以選擇下列架構。</span><span class="sxs-lookup"><span data-stu-id="0a981-117">You can choose from the following architectures.</span></span>

<span data-ttu-id="0a981-118">**HDInsight 已與在 Azure IaaS 上執行的 AD 整合**</span><span class="sxs-lookup"><span data-stu-id="0a981-118">**HDInsight integrated with AD running on Azure IaaS**</span></span>

<span data-ttu-id="0a981-119">這是最簡單的 HDInsight 與 Active Directory 整合架構。</span><span class="sxs-lookup"><span data-stu-id="0a981-119">This is the simplest architecture for integrating HDInsight with Active Directory.</span></span> <span data-ttu-id="0a981-120">AD 網域控制站會在 Azure 中的一部 (或多部) 虛擬機器 (VM) 上執行。</span><span class="sxs-lookup"><span data-stu-id="0a981-120">The AD domain controller runs on one (or multiple) virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="0a981-121">這些 VM 通常位於虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="0a981-121">These VMs are usually in a virtual network.</span></span> <span data-ttu-id="0a981-122">您可為 HDInsight 叢集設定另一個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a981-122">You set up another virtual network for the HDInsight cluster.</span></span> <span data-ttu-id="0a981-123">為了讓 HDInsight 能與 Active Directory 通訊，您必須使用 [VNet 對 VNet 對等互連](../virtual-network/virtual-network-create-peering.md)來對等互連這些虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a981-123">For HDInsight to have a line of sight to Active Directory, you need to peer these virtual networks by using [VNet-to-VNet peering](../virtual-network/virtual-network-create-peering.md).</span></span> <span data-ttu-id="0a981-124">如果您在 ARM 中建立 Active Directory，則您可以在相同的 VNet 中建立 Active Directory 與 HDInsight，不需要執行對等互連。</span><span class="sxs-lookup"><span data-stu-id="0a981-124">If you create the Active Directory in ARM, then you can create the Active Directory and HDInsight in the same VNet and you don't need to do peering.</span></span> 

![已加入網域的 HDInsight 叢集拓撲](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> <span data-ttu-id="0a981-126">在此架構中，您無法搭配使用 Azure Data Lake Store 與 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0a981-126">In this architecture, you cannot use Azure Data Lake Store with the HDInsight cluster.</span></span>


<span data-ttu-id="0a981-127">Active Directory 的必要條件︰</span><span class="sxs-lookup"><span data-stu-id="0a981-127">Prerequisites for Active Directory:</span></span>

* <span data-ttu-id="0a981-128">您必須建立[組織單位](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md)，以在其中放置叢集所用的 HDInsight 叢集 VM 和服務主體。</span><span class="sxs-lookup"><span data-stu-id="0a981-128">An [organizational unit](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) must be created, within which you place the HDInsight cluster VMs and the service principals used by the cluster.</span></span>
* <span data-ttu-id="0a981-129">必須設定[輕量型目錄存取通訊協定](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAP)，才能與 AD 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="0a981-129">[Lightweight Directory Access Protocols](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) must be set up for communicating with AD.</span></span> <span data-ttu-id="0a981-130">必須使用真正的憑證 (而非自我簽署憑證) 來設定 LDAPS 的憑證。</span><span class="sxs-lookup"><span data-stu-id="0a981-130">The certificate used to set up LDAPS must be a real certificate (not a self-signed certificate).</span></span>
* <span data-ttu-id="0a981-131">必須在網域上建立反向 DNS 區域，以供 HDInsight 子網路的 IP 位址範圍使用 (例如上一張圖中的 10.2.0.0/24)。</span><span class="sxs-lookup"><span data-stu-id="0a981-131">Reverse DNS zones must be created on the domain for the IP address range of the HDInsight subnet (for example, 10.2.0.0/24 in the previous picture).</span></span>
* <span data-ttu-id="0a981-132">需要服務帳戶或使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a981-132">A service account or a user account is needed.</span></span> <span data-ttu-id="0a981-133">使用此帳戶來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0a981-133">Use this account to create the HDInsight cluster.</span></span> <span data-ttu-id="0a981-134">此帳戶必須具備下列權限：</span><span class="sxs-lookup"><span data-stu-id="0a981-134">This account must have the following permissions:</span></span>

    - <span data-ttu-id="0a981-135">在組織單位內建立服務主體物件和電腦物件的權限</span><span class="sxs-lookup"><span data-stu-id="0a981-135">Permissions to create service principal objects and machine objects within the organizational unit</span></span>
    - <span data-ttu-id="0a981-136">建立反向 DNS Proxy 規則的權限</span><span class="sxs-lookup"><span data-stu-id="0a981-136">Permissions to create reverse DNS proxy rules</span></span>
    - <span data-ttu-id="0a981-137">將電腦加入 Active Directory 網域的權限</span><span class="sxs-lookup"><span data-stu-id="0a981-137">Permissions to join machines to the Active Directory domain</span></span>

<span data-ttu-id="0a981-138">**HDInsight 與僅限雲端的 Azure AD 整合**</span><span class="sxs-lookup"><span data-stu-id="0a981-138">**HDInsight integrated with cloud-only Azure AD**</span></span>

<span data-ttu-id="0a981-139">若為僅限雲端的 Azure AD，請設定網域控制站，讓 HDInsight 可以與 Azure AD 整合。</span><span class="sxs-lookup"><span data-stu-id="0a981-139">For cloud-only Azure AD, configure a domain controller so that HDInsight can be integrated with Azure AD.</span></span> <span data-ttu-id="0a981-140">使用 [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS) 即可達成此目的。</span><span class="sxs-lookup"><span data-stu-id="0a981-140">This is achieved by using [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS).</span></span> <span data-ttu-id="0a981-141">Azure AD DS 可在雲端建立網域控制站電腦，並提供 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0a981-141">Azure AD DS creates domain controller machines on the cloud and provides IP addresses for them.</span></span> <span data-ttu-id="0a981-142">它會建立兩個網域控制站，以達到高可用性。</span><span class="sxs-lookup"><span data-stu-id="0a981-142">It creates two domain controllers for high availability.</span></span>

<span data-ttu-id="0a981-143">目前，Azure AD DS 只存在於傳統虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a981-143">Currently, Azure AD DS exists only in classic virtual networks.</span></span> <span data-ttu-id="0a981-144">只能使用 Azure 傳統入口網站來存取。</span><span class="sxs-lookup"><span data-stu-id="0a981-144">It is only accessible by using the Azure classic portal.</span></span> <span data-ttu-id="0a981-145">HDInsight 虛擬網路存在於 Azure 入口網站，必須使用 VNet 對 VNet 對等互連來與傳統虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="0a981-145">The HDInsight virtual network exists in the Azure portal, which needs to be peered with the classic virtual network by using VNet-to-VNet peering.</span></span>

> [!NOTE]
> <span data-ttu-id="0a981-146">傳統虛擬網路與 Azure Resource Manager 虛擬網路之間對等互連時，兩個虛擬網路必須位於相同區域中，而且在相同 Azure 訂用帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="0a981-146">Peering between a classic virtual network and an Azure Resource Manager virtual network requires that both virtual networks are in the same region and under the same Azure subscription.</span></span>

![已加入網域的 HDInsight 叢集拓撲](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

<span data-ttu-id="0a981-148">Azure AD 的必要條件：</span><span class="sxs-lookup"><span data-stu-id="0a981-148">Prerequisites for Azure AD:</span></span>

* <span data-ttu-id="0a981-149">您必須建立[組織單位](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md)，以在其中放置叢集所用的 HDInsight 叢集 VM 和服務主體。</span><span class="sxs-lookup"><span data-stu-id="0a981-149">An [organizational unit](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) must be created within which you place the HDInsight cluster VMs and the service principals used by the cluster.</span></span>
* <span data-ttu-id="0a981-150">您必須在設定 Azure AD DS 時設定 [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)。</span><span class="sxs-lookup"><span data-stu-id="0a981-150">[LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) must be set up when you configure Azure AD DS.</span></span> <span data-ttu-id="0a981-151">必須使用真正的憑證 (而非自我簽署憑證) 來設定 LDAPS 的憑證。</span><span class="sxs-lookup"><span data-stu-id="0a981-151">The certificate used to set up LDAPS must be a real certificate (not a self-signed certificate).</span></span>
* <span data-ttu-id="0a981-152">必須在網域上建立反向 DNS 區域，以供 HDInsight 子網路的 IP 位址範圍使用 (例如上一張圖中的 10.2.0.0/24)。</span><span class="sxs-lookup"><span data-stu-id="0a981-152">Reverse DNS zones must be created on the domain for the IP address range of the HDInsight subnet (for example, 10.2.0.0/24 in the previous picture).</span></span>
* <span data-ttu-id="0a981-153">[密碼雜湊](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md)必須從 Azure AD 同步處理至 Azure AD DS。</span><span class="sxs-lookup"><span data-stu-id="0a981-153">[Password hashes](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) must be synced from Azure AD to Azure AD DS.</span></span>
* <span data-ttu-id="0a981-154">需要服務帳戶或使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a981-154">A service account or a user account is needed.</span></span> <span data-ttu-id="0a981-155">使用此帳戶來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0a981-155">Use this account to create the HDInsight cluster.</span></span> <span data-ttu-id="0a981-156">此帳戶必須具備下列權限：</span><span class="sxs-lookup"><span data-stu-id="0a981-156">This account must have the following permissions:</span></span>

    - <span data-ttu-id="0a981-157">在組織單位內建立服務主體物件和電腦物件的權限</span><span class="sxs-lookup"><span data-stu-id="0a981-157">Permissions to create service principal objects and machine objects within the organizational unit</span></span>
    - <span data-ttu-id="0a981-158">建立反向 DNS Proxy 規則的權限</span><span class="sxs-lookup"><span data-stu-id="0a981-158">Permissions to create reverse DNS proxy rules</span></span>
    - <span data-ttu-id="0a981-159">將電腦加入 Azure AD 網域的權限</span><span class="sxs-lookup"><span data-stu-id="0a981-159">Permissions to join machines to the Azure AD domain</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a981-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a981-160">Next steps</span></span>
* <span data-ttu-id="0a981-161">若要設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInisight 叢集](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="0a981-161">To configure a domain-joined HDInsight cluster, see [Configure domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="0a981-162">若要管理已加入網域的 HDInsight 叢集，請參閱[管理已加入網域的 HDInisight 叢集](hdinsight-domain-joined-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="0a981-162">To manage domain-joined HDInsight clusters, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="0a981-163">若要設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInsight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="0a981-163">To configure Hive policies and run Hive queries, see [Configure Hive policies for domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="0a981-164">若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="0a981-164">To run Hive queries by using SSH on domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
