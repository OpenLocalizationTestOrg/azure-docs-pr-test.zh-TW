---
title: "設定已加入網域的 HDInsight 叢集 - Azure | Microsoft Docs"
description: "了解如何安裝及設定已加入網域的 HDInsight 叢集"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 9964c3dff24ef8a3a6047fe18c0f36c12c1de33d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="6c092-103">設定已加入網域的 HDInsight 叢集 (預覽)</span><span class="sxs-lookup"><span data-stu-id="6c092-103">Configure Domain-joined HDInsight clusters (Preview)</span></span>

<span data-ttu-id="6c092-104">了解如何設定 Azure HDInsight 叢集與 Azure Active Directory (Azure AD) 和 [Apache Ranger](http://hortonworks.com/apache/ranger/)，以利用增強式驗證和豐富的角色型存取控制 (RBAC) 原則。</span><span class="sxs-lookup"><span data-stu-id="6c092-104">Learn how to set up an Azure HDInsight cluster with Azure Active Directory (Azure AD) and [Apache Ranger](http://hortonworks.com/apache/ranger/) to take advantage of strong authentication and rich role-based access control (RBAC) policies.</span></span>  <span data-ttu-id="6c092-105">您可以只在 Linux 架構的叢集上設定已加入網域的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="6c092-105">Domain-joined HDInsight can only be configured on Linux-based clusters.</span></span> <span data-ttu-id="6c092-106">如需詳細資訊，請參閱[已加入網域的 HDInsight 叢集簡介](hdinsight-domain-joined-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-106">For more information, see [Introduce Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c092-107">Oozie 未在已加入網域的 HDInsight 上啟用。</span><span class="sxs-lookup"><span data-stu-id="6c092-107">Oozie is not enabled on domain-joined HDInsight.</span></span>

<span data-ttu-id="6c092-108">本文是此系列文章的其中一篇：</span><span class="sxs-lookup"><span data-stu-id="6c092-108">This article is the first tutorial of a series:</span></span>

* <span data-ttu-id="6c092-109">建立連接到已啟用 Apache Ranger 之 Azure AD 的 HDInsight 叢集 (透過 Azure Directory 網域服務功能)。</span><span class="sxs-lookup"><span data-stu-id="6c092-109">Create an HDInsight cluster connected to Azure AD (via the Azure Directory Domain Services capability) with Apache Ranger enabled.</span></span>
* <span data-ttu-id="6c092-110">透過 Apache Ranger 建立和套用 Hive 原則，並允許使用者 (如資料科學家) 使用 ODBC 型工具 (如 Excel、Tableau 等) 連線到 Hive。Microsoft 正努力將其他工作負載 (例如 HBase、Spark、Storm) 盡快新增至已加入網域的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="6c092-110">Create and apply Hive policies through Apache Ranger, and allow users (for example, data scientists) to connect to Hive using ODBC-based tools, for example Excel, Tableau etc. Microsoft is working on adding other workloads, such as HBase, Spark, and Storm, to Domain-joined HDInsight soon.</span></span>

<span data-ttu-id="6c092-111">最終的拓樸範例如下：</span><span class="sxs-lookup"><span data-stu-id="6c092-111">An example of the final topology looks as follows:</span></span>

![已加入網域的 HDInsight 拓樸](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

<span data-ttu-id="6c092-113">因為 Azure AD 目前只支援傳統虛擬網路 (VNet)，而 Linux 架構的 HDInsight 叢集僅支援 Azure Resource Manager 架構的 VNet，HDInsight Azure AD 整合需要兩個 VNet 以及在兩者之間的對等互連。</span><span class="sxs-lookup"><span data-stu-id="6c092-113">Because Azure AD currently only supports classic virtual networks (VNets) and Linux-based HDInsight clusters only support Azure Resource Manager based VNets, HDInsight Azure AD integration requires two VNets and a peering between them.</span></span> <span data-ttu-id="6c092-114">如需兩種部署模型的比較資訊，請參閱 [Azure Resource Manager 與傳統部署比較：了解資源的部署模型和狀態](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-114">For the comparison information between the two deployment models, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6c092-115">這兩個 VNet 必須位於與 Azure AD DS 相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="6c092-115">The two VNets must be in the same region as the Azure AD DS.</span></span>

<span data-ttu-id="6c092-116">Azure 服務名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="6c092-116">Azure service names must be globally unique.</span></span> <span data-ttu-id="6c092-117">本教學課程中使用下列名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-117">The following names are used in this tutorial.</span></span> <span data-ttu-id="6c092-118">Contoso 是虛構的名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-118">Contoso is a fictitious name.</span></span> <span data-ttu-id="6c092-119">當您進行本教學課程時，必須將 contoso 取代為其他名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-119">You must replace *contoso* with a different name when you go through the tutorial.</span></span> 

<span data-ttu-id="6c092-120">**名稱︰**</span><span class="sxs-lookup"><span data-stu-id="6c092-120">**Names:**</span></span>

| <span data-ttu-id="6c092-121">屬性</span><span class="sxs-lookup"><span data-stu-id="6c092-121">Property</span></span> | <span data-ttu-id="6c092-122">值</span><span class="sxs-lookup"><span data-stu-id="6c092-122">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6c092-123">Azure AD VNet</span><span class="sxs-lookup"><span data-stu-id="6c092-123">Azure AD VNet</span></span> |<span data-ttu-id="6c092-124">contosoaadvnet</span><span class="sxs-lookup"><span data-stu-id="6c092-124">contosoaadvnet</span></span> |
| <span data-ttu-id="6c092-125">Azure AD Vnet 資源群組</span><span class="sxs-lookup"><span data-stu-id="6c092-125">Azure AD Vnet resource group</span></span> |<span data-ttu-id="6c092-126">contosoaadrg</span><span class="sxs-lookup"><span data-stu-id="6c092-126">contosoaadrg</span></span> |
| <span data-ttu-id="6c092-127">Azure AD 目錄</span><span class="sxs-lookup"><span data-stu-id="6c092-127">Azure AD directory</span></span> |<span data-ttu-id="6c092-128">contosoaaddirectory</span><span class="sxs-lookup"><span data-stu-id="6c092-128">contosoaaddirectory</span></span> |
| <span data-ttu-id="6c092-129">Azure AD 網域名稱</span><span class="sxs-lookup"><span data-stu-id="6c092-129">Azure AD domain name</span></span> |<span data-ttu-id="6c092-130">contoso (contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="6c092-130">contoso (contoso.onmicrosoft.com)</span></span> |
| <span data-ttu-id="6c092-131">HDInsight VNet</span><span class="sxs-lookup"><span data-stu-id="6c092-131">HDInsight VNet</span></span> |<span data-ttu-id="6c092-132">contosohdivnet</span><span class="sxs-lookup"><span data-stu-id="6c092-132">contosohdivnet</span></span> |
| <span data-ttu-id="6c092-133">HDInsight VNet 資源群組</span><span class="sxs-lookup"><span data-stu-id="6c092-133">HDInsight VNet resource group</span></span> |<span data-ttu-id="6c092-134">contosohdirg</span><span class="sxs-lookup"><span data-stu-id="6c092-134">contosohdirg</span></span> |
| <span data-ttu-id="6c092-135">HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="6c092-135">HDInsight cluster</span></span> |<span data-ttu-id="6c092-136">contosohdicluster</span><span class="sxs-lookup"><span data-stu-id="6c092-136">contosohdicluster</span></span> |

<span data-ttu-id="6c092-137">本教學課程提供「設定已加入網域的 HDInsight 叢集」的步驟。</span><span class="sxs-lookup"><span data-stu-id="6c092-137">This tutorial provides the steps for configuring a domain-joined HDInsight cluster.</span></span> <span data-ttu-id="6c092-138">每一節都有其他文件的連結，以提供更詳細的背景資訊。</span><span class="sxs-lookup"><span data-stu-id="6c092-138">Each section has links to other articles with more background information.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="6c092-139">必要條件：</span><span class="sxs-lookup"><span data-stu-id="6c092-139">Prerequisite:</span></span>
* <span data-ttu-id="6c092-140">您熟悉 [Azure AD 網域服務](https://azure.microsoft.com/services/active-directory-ds/)及其 [價格](https://azure.microsoft.com/pricing/details/active-directory-ds/)結構。</span><span class="sxs-lookup"><span data-stu-id="6c092-140">Familiarize yourself with [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) its [pricing](https://azure.microsoft.com/pricing/details/active-directory-ds/) structure.</span></span>
* <span data-ttu-id="6c092-141">確定您的訂用帳戶已列入此公開預覽版本的允許清單中。</span><span class="sxs-lookup"><span data-stu-id="6c092-141">Ensure that your subscription is whitelisted for this public preview.</span></span> <span data-ttu-id="6c092-142">您可以傳送電子郵件與您的訂用帳戶識別碼給 hdipreview@microsoft.com 要求列入。</span><span class="sxs-lookup"><span data-stu-id="6c092-142">You can do so by sending an email to hdipreview@microsoft.com with your subscription ID.</span></span>
* <span data-ttu-id="6c092-143">SSL 憑證，需由您的網域的簽章授權單位簽署。</span><span class="sxs-lookup"><span data-stu-id="6c092-143">An SSL certificate that is signed by a signing authority for your domain.</span></span> <span data-ttu-id="6c092-144">設定安全的 LDAP 需有此憑證。</span><span class="sxs-lookup"><span data-stu-id="6c092-144">The certificate is required by configuring secure LDAP.</span></span> <span data-ttu-id="6c092-145">不可使用自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="6c092-145">Self-signed certificates cannot be used.</span></span>

## <a name="procedures"></a><span data-ttu-id="6c092-146">程序</span><span class="sxs-lookup"><span data-stu-id="6c092-146">Procedures</span></span>
1. <span data-ttu-id="6c092-147">為您的 Azure AD 建立 Azure 傳統 VNet。</span><span class="sxs-lookup"><span data-stu-id="6c092-147">Create an Azure classic VNet for your Azure AD.</span></span>  
2. <span data-ttu-id="6c092-148">建立和設定 Azure AD 與 Azure AD DS。</span><span class="sxs-lookup"><span data-stu-id="6c092-148">Create and configure Azure AD and Azure AD DS.</span></span>
3. <span data-ttu-id="6c092-149">在 Azure 資源管理模式中建立 HDInsight VNet。</span><span class="sxs-lookup"><span data-stu-id="6c092-149">Create an HDInsight VNet in the Azure resource management mode.</span></span>
4. <span data-ttu-id="6c092-150">對等互連兩個 VNet。</span><span class="sxs-lookup"><span data-stu-id="6c092-150">Peer the two VNets.</span></span>
5. <span data-ttu-id="6c092-151">建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6c092-151">Create an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6c092-152">本教學課程假設您已沒有 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="6c092-152">This tutorial assumes that you do not have an Azure AD.</span></span> <span data-ttu-id="6c092-153">如果您有的話，可以略過步驟 2 的部分。</span><span class="sxs-lookup"><span data-stu-id="6c092-153">If you have one, you can skip the portion in step 2.</span></span>
> 
> 

<span data-ttu-id="6c092-154">有 PowerShell 指令碼可自動執行步驟 3 到步驟 7。</span><span class="sxs-lookup"><span data-stu-id="6c092-154">There is a PowerShell script that automates step 3 through step 7.</span></span>  <span data-ttu-id="6c092-155">如需詳細資訊，請參閱[使用 Azure PowerShell 設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure-use-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-155">For more information, see [Configure Domain-joined HDInsight clusters use Azure PowerShell](hdinsight-domain-joined-configure-use-powershell.md).</span></span>

## <a name="create-an-azure-virtual-network-classic"></a><span data-ttu-id="6c092-156">建立 Azure 虛擬網路 (傳統)</span><span class="sxs-lookup"><span data-stu-id="6c092-156">Create an Azure virtual network (classic)</span></span>
<span data-ttu-id="6c092-157">在本節中，您會使用 Azure 入口網站建立虛擬網路 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="6c092-157">In this section, you create a virtual network (classic) using the Azure portal.</span></span> <span data-ttu-id="6c092-158">在下一節，您會啟用虛擬網路中 Azure AD 的 Azure AD DS。</span><span class="sxs-lookup"><span data-stu-id="6c092-158">In the next section, you enable the Azure AD DS for your Azure AD in the virtual network.</span></span> <span data-ttu-id="6c092-159">如需下列程序和使用其他虛擬網路建立方法的詳細資訊，請參閱[使用 Azure 入口網站建立虛擬網路 (傳統)](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-159">For more information about the following procedure and using other virtual network creation methods, see [Create a virtual network (classic) by using the Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>

<span data-ttu-id="6c092-160">**建立傳統 VNet**</span><span class="sxs-lookup"><span data-stu-id="6c092-160">**To create a classic VNet**</span></span>

1. <span data-ttu-id="6c092-161">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6c092-161">Sign on to the [Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="6c092-162">按一下 [新增]  >  [網路]  >  [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="6c092-162">Click **New** > **Networking** > **Virtual Network**.</span></span>
3. <span data-ttu-id="6c092-163">在 [選取部署模型] 中，選取 [傳統]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6c092-163">In **Select a deployment model**, select **Classic**, and then click **Create**.</span></span>
4. <span data-ttu-id="6c092-164">輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="6c092-164">Enter or select the following values:</span></span>
   
   * <span data-ttu-id="6c092-165">**名稱**：contosoaadvnet</span><span class="sxs-lookup"><span data-stu-id="6c092-165">**Name**: contosoaadvnet</span></span>
   * <span data-ttu-id="6c092-166">**位址空間**：10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6c092-166">**Address space**: 10.1.0.0/16</span></span>
   * <span data-ttu-id="6c092-167">**子網路名稱**：Subnet1</span><span class="sxs-lookup"><span data-stu-id="6c092-167">**Subnet name**: Subnet1</span></span>
   * <span data-ttu-id="6c092-168">**子網路位址範圍**：10.1.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6c092-168">**Subnet address range**: 10.1.0.0/24</span></span>
   * <span data-ttu-id="6c092-169">**訂用帳戶**：(選取用來建立此 VNet 的訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="6c092-169">**Subscription**: (Select a subscription used for creating this VNet.)</span></span>
   * <span data-ttu-id="6c092-170">**ResourceGroup**：contosoaadrg</span><span class="sxs-lookup"><span data-stu-id="6c092-170">**ResourceGroup**: contosoaadrg</span></span>
   * <span data-ttu-id="6c092-171">**位置**：(選取 HDInsight 叢集的區域。)</span><span class="sxs-lookup"><span data-stu-id="6c092-171">**Location**: (Select a region for your HDInsight cluster.)</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="6c092-172">您必須選擇支援 Azure AD DS 的位置。</span><span class="sxs-lookup"><span data-stu-id="6c092-172">You must choose a location that supports Azure AD DS.</span></span> <span data-ttu-id="6c092-173">如需詳細資訊，請參閱[不同區域提供的產品](https://azure.microsoft.com/en-us/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="6c092-173">For more information, see [Products available by region](https://azure.microsoft.com/en-us/regions/services/).</span></span> 
     > 
     > <span data-ttu-id="6c092-174">傳統 VNet 和資源群組 VNet 皆必須位於與 Azure AD DS 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="6c092-174">Both the classic VNet and the Resource Group VNet must be in the same region as the Azure AD DS.</span></span>
     > 
     > 
5. <span data-ttu-id="6c092-175">按一下 [建立] 來建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="6c092-175">Click **Create** to create the VNet.</span></span>

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a><span data-ttu-id="6c092-176">為您的 Azure AD 建立和設定 Azure AD DS。</span><span class="sxs-lookup"><span data-stu-id="6c092-176">Create and configure Azure AD DS for your Azure AD</span></span>
<span data-ttu-id="6c092-177">在本節中，您將：</span><span class="sxs-lookup"><span data-stu-id="6c092-177">In this section, you will:</span></span>

1. <span data-ttu-id="6c092-178">建立 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="6c092-178">Create an Azure AD.</span></span>
2. <span data-ttu-id="6c092-179">建立 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="6c092-179">Create Azure AD users.</span></span> <span data-ttu-id="6c092-180">這些使用者是網域使用者。</span><span class="sxs-lookup"><span data-stu-id="6c092-180">These users are domain users.</span></span> <span data-ttu-id="6c092-181">您使用第一位使用者來設定搭配 Azure AD 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6c092-181">You use the first user for configuring the HDInsight cluster with the Azure AD.</span></span>  <span data-ttu-id="6c092-182">其他兩位使用者在本教學課程中都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="6c092-182">The other two users are optional for this tutorial.</span></span> <span data-ttu-id="6c092-183">當您設定 Apache Ranger 時，您會使用他們來[針對已加入網域的 HDInsight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-183">They will be used in [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) when you configure Apache Ranger policies.</span></span>
3. <span data-ttu-id="6c092-184">建立 AAD DC 系統管理員群組，並將 Azure AD 使用者新增至群組。</span><span class="sxs-lookup"><span data-stu-id="6c092-184">Create the AAD DC Administrators group and add the Azure AD user to the group.</span></span> <span data-ttu-id="6c092-185">您可以使用這位使用者來建立組織單位。</span><span class="sxs-lookup"><span data-stu-id="6c092-185">You use this user to create the organizational unit.</span></span>
4. <span data-ttu-id="6c092-186">啟用 Azure AD 的 Azure AD 網域服務 (Azure AD DS)。</span><span class="sxs-lookup"><span data-stu-id="6c092-186">Enable Azure AD Domain Services (Azure AD DS) for the Azure AD.</span></span>
5. <span data-ttu-id="6c092-187">設定 Azure AD 的 LDAPS。</span><span class="sxs-lookup"><span data-stu-id="6c092-187">Configure LDAPS for the Azure AD.</span></span> <span data-ttu-id="6c092-188">輕量型目錄存取通訊協定 (LDAP) 是用來從 Azure AD 讀取和寫入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="6c092-188">The Lightweight Directory Access Protocol (LDAP) is used to read from and write to Azure AD.</span></span>

<span data-ttu-id="6c092-189">如果您想要使用現有的 Azure AD，可以略過步驟 1 和 2。</span><span class="sxs-lookup"><span data-stu-id="6c092-189">If you prefer to use an existing Azure AD, you can skip steps 1 and 2.</span></span>

<span data-ttu-id="6c092-190">**建立 Azure AD**</span><span class="sxs-lookup"><span data-stu-id="6c092-190">**To create an Azure AD**</span></span>

1. <span data-ttu-id="6c092-191">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [新增]  >  [應用程式服務]  >  [Active Directory]  >  [目錄]  >  [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="6c092-191">From the [Azure classic portal](https://manage.windowsazure.com), click **New** > **App Services** > **Active Directory** > **Directory** > **Custom Create**.</span></span> 
2. <span data-ttu-id="6c092-192">輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="6c092-192">Enter or select the following values:</span></span>
   
   * <span data-ttu-id="6c092-193">**名稱**：contosoaaddirectory</span><span class="sxs-lookup"><span data-stu-id="6c092-193">**Name**: contosoaaddirectory</span></span>
   * <span data-ttu-id="6c092-194">**網域名稱**：contoso。</span><span class="sxs-lookup"><span data-stu-id="6c092-194">**Domain name**: contoso.</span></span>  <span data-ttu-id="6c092-195">此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="6c092-195">This name must be globally unique.</span></span>
   * <span data-ttu-id="6c092-196">**國家或區域**：選取您的國家或區域。</span><span class="sxs-lookup"><span data-stu-id="6c092-196">**Country or region**: Select your country or region.</span></span>
3. <span data-ttu-id="6c092-197">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="6c092-197">Click **Complete**.</span></span>

<span data-ttu-id="6c092-198">**建立 Azure AD 使用者**</span><span class="sxs-lookup"><span data-stu-id="6c092-198">**Create an Azure AD user**</span></span>

1. <span data-ttu-id="6c092-199">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  ->  [contosoaaddirectory]。</span><span class="sxs-lookup"><span data-stu-id="6c092-199">From the [Azure classic portal](https://manage.windowsazure.com), click **Active Directory** -> **contosoaaddirectory**.</span></span> 
2. <span data-ttu-id="6c092-200">按一下頂端功能表中的 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="6c092-200">Click **Users** from the top menu.</span></span>
3. <span data-ttu-id="6c092-201">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="6c092-201">Click **Add User**.</span></span>
4. <span data-ttu-id="6c092-202">輸入 [使用者名稱]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6c092-202">Enter **User Name**, and then click **Next**.</span></span> 
5. <span data-ttu-id="6c092-203">設定使用者設定檔；在 [角色] 選取 [全域管理員]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6c092-203">Configure user profile; In **Role**, select **Global Admin**; and then click **Next**.</span></span>  <span data-ttu-id="6c092-204">需要「全域管理員角色」才能建立組織單位。</span><span class="sxs-lookup"><span data-stu-id="6c092-204">The Global Admin role is needed to create organizational units.</span></span>
6. <span data-ttu-id="6c092-205">按一下 [建立] 取得暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="6c092-205">Click **Create** to get a temporary password.</span></span>
7. <span data-ttu-id="6c092-206">複製一份密碼，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="6c092-206">Make a copy of the password, and then click **Complete**.</span></span> <span data-ttu-id="6c092-207">在本教學課程稍後，您會使用這個全域管理使用者來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6c092-207">Later in this tutorial, you will use this global admin user to create the HDInsight cluster.</span></span>

<span data-ttu-id="6c092-208">依照相同程序建立另外兩位使用者，**使用者**角色分別為 hiveuser1 和 hiveuser2。</span><span class="sxs-lookup"><span data-stu-id="6c092-208">Follow the same procedure to create two more users with the **User** role, hiveuser1 and hiveuser2.</span></span> <span data-ttu-id="6c092-209">下列使用者會用於[針對已加入網域的 HDInsight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-209">The following users will be used in [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>

<span data-ttu-id="6c092-210">**建立 AAD DC 系統管理員群組，並新增 Azure AD 使用者**</span><span class="sxs-lookup"><span data-stu-id="6c092-210">**To create the AAD DC Administrators' group, and add an Azure AD user**</span></span>

1. <span data-ttu-id="6c092-211">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  >  [contosoaaddirectory]。</span><span class="sxs-lookup"><span data-stu-id="6c092-211">From the [Azure classic portal](https://manage.windowsazure.com), click **Active Directory** > **contosoaaddirectory**.</span></span> 
2. <span data-ttu-id="6c092-212">按一下頂端功能表中的 [群組]。</span><span class="sxs-lookup"><span data-stu-id="6c092-212">Click **Groups** from the top menu.</span></span>
3. <span data-ttu-id="6c092-213">按一下 [新增一個群組] 或 [新增群組]。</span><span class="sxs-lookup"><span data-stu-id="6c092-213">Click **Add a Group** or **Add Group**.</span></span>
4. <span data-ttu-id="6c092-214">輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="6c092-214">Enter or select the following values:</span></span>
   
   * <span data-ttu-id="6c092-215">**名稱**：AAD DC 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="6c092-215">**Name**: AAD DC Administrators.</span></span>  <span data-ttu-id="6c092-216">請勿變更群組名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-216">Don't change the group name.</span></span>
   * <span data-ttu-id="6c092-217">**群組類型**：安全性。</span><span class="sxs-lookup"><span data-stu-id="6c092-217">**Group Type**: Security.</span></span>
5. <span data-ttu-id="6c092-218">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="6c092-218">Click **Complete**.</span></span>
6. <span data-ttu-id="6c092-219">按一下[AAD DC 系統管理員] 以開啟群組。</span><span class="sxs-lookup"><span data-stu-id="6c092-219">Click **AAD DC Administrators** to open the group.</span></span>
7. <span data-ttu-id="6c092-220">按一下[新增成員]。</span><span class="sxs-lookup"><span data-stu-id="6c092-220">Click **Add Members**.</span></span>
8. <span data-ttu-id="6c092-221">選取您在前一個步驟建立的第一位使用者，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="6c092-221">Select the first user you created in the previous step, and then click **Complete**.</span></span>
9. <span data-ttu-id="6c092-222">重複相同步驟來建立另一個名為 **HiveUsers** 的群組，並將兩個 Hive 使用者新增至群組。</span><span class="sxs-lookup"><span data-stu-id="6c092-222">Repeat the same steps to create another group called **HiveUsers**, and add the two Hive users to the group.</span></span>

<span data-ttu-id="6c092-223">如需詳細資訊，請參閱[Azure AD 網域服務 (預覽) - 建立「AAD DC 系統管理員」的群組](../active-directory-domain-services/active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-223">For more information, see [Azure AD Domain Services (Preview) - Create the 'AAD DC Administrators' group](../active-directory-domain-services/active-directory-ds-getting-started.md).</span></span>

<span data-ttu-id="6c092-224">**為您的 Azure AD 啟用 Azure AD DS**</span><span class="sxs-lookup"><span data-stu-id="6c092-224">**To enable Azure AD DS for your Azure AD**</span></span>

1. <span data-ttu-id="6c092-225">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  >  [contosoaaddirectory]。</span><span class="sxs-lookup"><span data-stu-id="6c092-225">From the [Azure classic portal](https://manage.windowsazure.com), click **Active Directory** > **contosoaaddirectory**.</span></span> 
2. <span data-ttu-id="6c092-226">按一下頂端的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="6c092-226">Click **Configure** from the top menu.</span></span>
3. <span data-ttu-id="6c092-227">向下捲動至 [網域服務]，設定下列值︰</span><span class="sxs-lookup"><span data-stu-id="6c092-227">Scroll down to **Domain Services**, and set the following values:</span></span>
   
   * <span data-ttu-id="6c092-228">**啟用此目錄的網域服務**：是。</span><span class="sxs-lookup"><span data-stu-id="6c092-228">**Enable domain services for this directory**: Yes.</span></span>
   * <span data-ttu-id="6c092-229">**網域服務的 DNS 網域名稱**︰這會顯示 Azure 目錄的預設 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-229">**DNS domain name of domain services**: This shows the default DNS name of the Azure directory.</span></span> <span data-ttu-id="6c092-230">例如，contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="6c092-230">For example, contoso.onmicrosoft.com.</span></span>
   * <span data-ttu-id="6c092-231">**將網域服務連接到此虛擬網路**：選取您稍早建立的傳統虛擬網路，即 **contosoaadvnet**。</span><span class="sxs-lookup"><span data-stu-id="6c092-231">**Connect domain services to this virtual network**: Select the classic virtual network you created earlier, i.e. **contosoaadvnet**.</span></span>
4. <span data-ttu-id="6c092-232">按一下頁面底部的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="6c092-232">Click **Save** from the bottom of the page.</span></span> <span data-ttu-id="6c092-233">在 [啟用此目錄的網域服務] 旁您會看到 [擱置中...]。</span><span class="sxs-lookup"><span data-stu-id="6c092-233">You will see **Pending ...** next to **Enable domain services for this directory**.</span></span>  
5. <span data-ttu-id="6c092-234">等 [擱置中...] 消失，[IP 位址] 就會填入值。</span><span class="sxs-lookup"><span data-stu-id="6c092-234">Wait until **Pending ...** disappears, and **IP Address** gets populated.</span></span> <span data-ttu-id="6c092-235">一共會填入兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6c092-235">Two IP addresses will get populated.</span></span> <span data-ttu-id="6c092-236">這些是由網域服務佈建的網域控制站的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6c092-236">These are the IP addresses of the domain controllers provisioned by Domain Services.</span></span> <span data-ttu-id="6c092-237">對應的網域控制站佈建並就緒之後，將會顯示每個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6c092-237">Each IP address will be visible after the corresponding domain controller is provisioned and ready.</span></span> <span data-ttu-id="6c092-238">寫下這兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6c092-238">Write down the two IP addresses.</span></span> <span data-ttu-id="6c092-239">稍後您將需要這些資訊。</span><span class="sxs-lookup"><span data-stu-id="6c092-239">You will need them later.</span></span>

<span data-ttu-id="6c092-240">如需詳細資訊，請參閱 [Azure AD 網域服務 (預覽) - 啟用 Azure AD 網域服務](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-240">For more information, see [Azure AD Domain Services (Preview) - Enable Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).</span></span>

<span data-ttu-id="6c092-241">**同步處理密碼**</span><span class="sxs-lookup"><span data-stu-id="6c092-241">**To synchronize password**</span></span>

<span data-ttu-id="6c092-242">如果您使用自己的網域，您需要將密碼同步。</span><span class="sxs-lookup"><span data-stu-id="6c092-242">If you use your own domain, you need to synchronize the password.</span></span> <span data-ttu-id="6c092-243">請參閱[為僅限雲端的 Azure AD 目錄啟用 Azure AD 網域服務的密碼同步處理](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-243">See [Enable password synchronization to Azure AD domain services for a cloud-only Azure AD directory](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).</span></span>

<span data-ttu-id="6c092-244">**設定 Azure AD 的 LDAPS**</span><span class="sxs-lookup"><span data-stu-id="6c092-244">**To configure LDAPS for the Azure AD**</span></span>

1. <span data-ttu-id="6c092-245">取得由您的網域的簽章授權單位簽署的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6c092-245">Get an SSL certificate that is signed by a signing authority for your domain.</span></span> <span data-ttu-id="6c092-246">如果您要使用自我簽署憑證，請向 hdipreview@microsoft.com 要求例外處理。</span><span class="sxs-lookup"><span data-stu-id="6c092-246">If you want to use a self-signed certificate, please reach out to hdipreview@microsoft.com for an exception.</span></span>
2. <span data-ttu-id="6c092-247">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  >  [contosoaaddirectory]。</span><span class="sxs-lookup"><span data-stu-id="6c092-247">From the [Azure classic portal](https://manage.windowsazure.com), click **Active Directory** > **contosoaaddirectory**.</span></span> 
3. <span data-ttu-id="6c092-248">按一下頂端的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="6c092-248">Click **Configure** from the top menu.</span></span>
4. <span data-ttu-id="6c092-249">捲動到 [網域服務]。</span><span class="sxs-lookup"><span data-stu-id="6c092-249">Scroll to **domain services**.</span></span>
5. <span data-ttu-id="6c092-250">按一下 [設定憑證]。</span><span class="sxs-lookup"><span data-stu-id="6c092-250">Click **Configure certificate**.</span></span>
6. <span data-ttu-id="6c092-251">依照指示來指定憑證檔案和密碼。</span><span class="sxs-lookup"><span data-stu-id="6c092-251">Follow the instruction to specify the certificate file and the password.</span></span> <span data-ttu-id="6c092-252">在 [啟用此目錄的網域服務] 旁您會看到 [擱置中...]。</span><span class="sxs-lookup"><span data-stu-id="6c092-252">You will see **Pending ...** next to **Enable domain services for this directory**.</span></span>  
7. <span data-ttu-id="6c092-253">等 [擱置中...] 消失，[安全 LDAP 憑證] 就會填入值。</span><span class="sxs-lookup"><span data-stu-id="6c092-253">Wait until **Pending ...** disappears, and **Secure LDAP Certificate** got populated.</span></span>  <span data-ttu-id="6c092-254">這項作業需要 10 分鐘或更久。</span><span class="sxs-lookup"><span data-stu-id="6c092-254">This can take up 10 minutes or more.</span></span>

> [!NOTE]
> <span data-ttu-id="6c092-255">如果 Azure AD DS 上正在執行某些背景工作，您上傳憑證時可能會看到錯誤 - 此租用戶有作業正在執行。<i>請稍後再試。</i></span><span class="sxs-lookup"><span data-stu-id="6c092-255">If some background tasks are being run on the Azure AD DS, you may see an error while uploading certificate - <i>There is an operation being performed for this tenant. Please try again later</i>.</span></span>  <span data-ttu-id="6c092-256">如果您遇到這個錯誤，請稍待片刻後再試一次。</span><span class="sxs-lookup"><span data-stu-id="6c092-256">In case you experience this error, please try again after some time.</span></span> <span data-ttu-id="6c092-257">佈建第二個網域控制站 IP 可能需要長達 3 小時。</span><span class="sxs-lookup"><span data-stu-id="6c092-257">The second domain controller IP may take up to 3 hours to be provisioned.</span></span>
> 
> 

<span data-ttu-id="6c092-258">如需詳細資訊，請參閱[針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-258">For more information, see [Configure Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a><span data-ttu-id="6c092-259">建立用於 HDInsight 叢集的 Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="6c092-259">Create a Resource Manager VNet for HDInsight cluster</span></span>
<span data-ttu-id="6c092-260">在本節中，您會建立將用於 HDInsight 的 Azure Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="6c092-260">In this section, you will create an Azure Resource Manager VNet that will be used for the HDInsight cluster.</span></span> <span data-ttu-id="6c092-261">如需使用其他方法建立 Azure VNet 的詳細資訊，請參閱[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-261">For more information on creating Azure VNET using other methods, see [Create a virtual network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)</span></span>

<span data-ttu-id="6c092-262">建立 VNet 之後，需將 Azure Resource Manager VNet 設定成使用與 Azure AD VNet 所用的同一 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6c092-262">After creating the VNet, you will configure the Resource Manager VNet to use the same DNS servers as for the Azure AD VNet.</span></span> <span data-ttu-id="6c092-263">如果您已遵循本教學課程中的步驟建立傳統 VNet 和 Azure AD，則 DNS 伺服器是 10.1.0.4 和 10.1.0.5。</span><span class="sxs-lookup"><span data-stu-id="6c092-263">If you followed the steps in this tutorial to create the classic VNet and the Azure AD, the DNS servers are 10.1.0.4 and 10.1.0.5.</span></span>

<span data-ttu-id="6c092-264">**建立 Resource Manager VNet**</span><span class="sxs-lookup"><span data-stu-id="6c092-264">**To create a Resource Manager VNet**</span></span>

1. <span data-ttu-id="6c092-265">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6c092-265">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c092-266">依序按一下 [新增]、[網路] 及 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="6c092-266">Click **New**, **Networking**, and then **Virtual network**.</span></span> 
3. <span data-ttu-id="6c092-267">在 [選取部署模型] 中，選取 [Resource Manager]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6c092-267">In **Select a deployment model**, select **Resource Manager**, and then click **Create**.</span></span>
4. <span data-ttu-id="6c092-268">輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="6c092-268">Type or select the following values:</span></span>
   
   * <span data-ttu-id="6c092-269">**名稱**：contosohdivnet</span><span class="sxs-lookup"><span data-stu-id="6c092-269">**Name**: contosohdivnet</span></span>
   * <span data-ttu-id="6c092-270">**位址空間**：10.2.0.0/16。</span><span class="sxs-lookup"><span data-stu-id="6c092-270">**Address space**: 10.2.0.0/16.</span></span> <span data-ttu-id="6c092-271">請確定位址範圍沒有與傳統 VNet 的 IP位址範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="6c092-271">Make sure the address range cannot overlap with the IP address range of the classic VNet.</span></span>
   * <span data-ttu-id="6c092-272">**子網路名稱**：Subnet1</span><span class="sxs-lookup"><span data-stu-id="6c092-272">**Subnet name**: Subnet1</span></span>
   * <span data-ttu-id="6c092-273">**子網路位址範圍**：10.2.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6c092-273">**Subnet address range**: 10.2.0.0/24</span></span>
   * <span data-ttu-id="6c092-274">**訂用帳戶**：(選取您的 Azure 訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="6c092-274">**Subscription**: (Select your Azure subscription.)</span></span>
   * <span data-ttu-id="6c092-275">**資源群組**：contosohdirg</span><span class="sxs-lookup"><span data-stu-id="6c092-275">**Resource group**: contosohdirg</span></span>
   * <span data-ttu-id="6c092-276">**位置**：(選取與 Azure AD VNet 相同的位置，也就是 contosoaadvnet。)</span><span class="sxs-lookup"><span data-stu-id="6c092-276">**Location**: (Select the same location as the Azure AD VNet, i.e. contosoaadvnet.)</span></span>
5. <span data-ttu-id="6c092-277">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6c092-277">Click **Create**.</span></span>

<span data-ttu-id="6c092-278">**設定 Resource Manager VNet 的 DNS**</span><span class="sxs-lookup"><span data-stu-id="6c092-278">**To configure DNS for the Resource Manager VNet**</span></span>

1. <span data-ttu-id="6c092-279">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [更多服務]  ->  [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="6c092-279">From the [Azure portal](https://portal.azure.com), click **More services** -> **Virtual networks**.</span></span> <span data-ttu-id="6c092-280">確定沒有按到 [虛擬網路 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="6c092-280">Ensure not to click **Virtual networks (classic)**.</span></span>
2. <span data-ttu-id="6c092-281">按一下 [contosohdivnet]。</span><span class="sxs-lookup"><span data-stu-id="6c092-281">Click **contosohdivnet**.</span></span>
3. <span data-ttu-id="6c092-282">按一下左側刀鋒視窗中的 [DNS 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="6c092-282">Click **DNS servers** from the left side of the new blade.</span></span>
4. <span data-ttu-id="6c092-283">按一下 [自訂]，然後輸入下列值︰</span><span class="sxs-lookup"><span data-stu-id="6c092-283">Click **Custom**, and then enter the following values:</span></span>
   
   * <span data-ttu-id="6c092-284">10.1.0.4</span><span class="sxs-lookup"><span data-stu-id="6c092-284">10.1.0.4</span></span>
   * <span data-ttu-id="6c092-285">10.1.0.5</span><span class="sxs-lookup"><span data-stu-id="6c092-285">10.1.0.5</span></span>
     
     <span data-ttu-id="6c092-286">這些 DNS 伺服器 IP 位址必須與 Azure AD VNet (傳統 VNet) 中的 DNS 伺服器相符。</span><span class="sxs-lookup"><span data-stu-id="6c092-286">These DNS server IP addresses must match to the DNS servers in the Azure AD VNet (classic VNet).</span></span>
5. <span data-ttu-id="6c092-287">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6c092-287">Click **Save**.</span></span>

## <a name="peer-the-azure-ad-vnet-and-the-hdinsight-vnet"></a><span data-ttu-id="6c092-288">對等互連 Azure AD VNet 和 HDInsight VNet</span><span class="sxs-lookup"><span data-stu-id="6c092-288">Peer the Azure AD VNet and the HDInsight VNet</span></span>
<span data-ttu-id="6c092-289">**對等互連兩個 VNet**</span><span class="sxs-lookup"><span data-stu-id="6c092-289">**To peer the two VNet**</span></span>

1. <span data-ttu-id="6c092-290">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6c092-290">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c092-291">按一下左側功能表中的 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="6c092-291">Click **More services** from the left menu.</span></span>
3. <span data-ttu-id="6c092-292">按一下 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="6c092-292">Click **Virtual Networks**.</span></span> <span data-ttu-id="6c092-293">確定沒有按到 [虛擬網路 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="6c092-293">Don't click **Virtual networks (classic)**.</span></span>
4. <span data-ttu-id="6c092-294">按一下 [contosohdivnet]。</span><span class="sxs-lookup"><span data-stu-id="6c092-294">Click **contosohdivnet**.</span></span>  <span data-ttu-id="6c092-295">這是 HDInsight VNet。</span><span class="sxs-lookup"><span data-stu-id="6c092-295">This is the HDInsight VNet.</span></span>
5. <span data-ttu-id="6c092-296">按一下刀鋒視窗左側功能表中的 [對等互連]。</span><span class="sxs-lookup"><span data-stu-id="6c092-296">Click **Peerings** on the left menu of the blade.</span></span>
6. <span data-ttu-id="6c092-297">按一下頂端功能表中的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6c092-297">Click **Add** from the top menu.</span></span> <span data-ttu-id="6c092-298">[新增對等互連] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6c092-298">It opens the **Add peering** blade.</span></span>
7. <span data-ttu-id="6c092-299">在 [新增對等互連] 刀鋒視窗中，設定或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="6c092-299">On the **Add peering** blade, set or select the following values:</span></span>
   
   * <span data-ttu-id="6c092-300">**名稱**：ContosoAADHDIVNetPeering</span><span class="sxs-lookup"><span data-stu-id="6c092-300">**Name**: ContosoAADHDIVNetPeering</span></span>
   * <span data-ttu-id="6c092-301">**虛擬網路部署模型**︰傳統</span><span class="sxs-lookup"><span data-stu-id="6c092-301">**Virtual network deployment model**: Classic</span></span>
   * <span data-ttu-id="6c092-302">**訂用帳戶**：選取您用於傳統 (Azure AD) VNet 的訂用帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="6c092-302">**Subscription**: Select your subscription name used for the classic (Azure AD) vnet.</span></span>
   * <span data-ttu-id="6c092-303">**虛擬網路**：contosoaadvnet</span><span class="sxs-lookup"><span data-stu-id="6c092-303">**Virtual network**: contosoaadvnet.</span></span>
   * <span data-ttu-id="6c092-304">**允許虛擬網路存取**：(勾選)</span><span class="sxs-lookup"><span data-stu-id="6c092-304">**Allow virtual network access**: (Check)</span></span>
   * <span data-ttu-id="6c092-305">**允許轉送的流量**：(勾選)。</span><span class="sxs-lookup"><span data-stu-id="6c092-305">**Allow forwarded traffic**: (Check).</span></span> <span data-ttu-id="6c092-306">其他兩個核取方塊保持未勾選。</span><span class="sxs-lookup"><span data-stu-id="6c092-306">Leave the other two checkboxes unchecked.</span></span>
8. <span data-ttu-id="6c092-307">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6c092-307">Click **OK**.</span></span>

## <a name="create-hdinsight-cluster"></a><span data-ttu-id="6c092-308">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="6c092-308">Create HDInsight cluster</span></span>
<span data-ttu-id="6c092-309">在本節中，您會使用 Azure 入口網站或 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)，在 HDInsight 中建立 Linux 架構的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="6c092-309">In this section, you create a Linux-based Hadoop cluster in HDInsight using either the Azure portal or [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="6c092-310">如需其他叢集建立方法及了解各項設定，請參閱 [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-310">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="6c092-311">如需有關使用 Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集的詳細資訊，請參閱[使用 Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-create-windows-clusters-arm-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-311">For more information about using Resource Manager template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

<span data-ttu-id="6c092-312">**使用 Azure 入口網站建立已加入網域的 HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="6c092-312">**To create a Domain-joined HDInsight cluster using the Azure portal**</span></span>

1. <span data-ttu-id="6c092-313">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6c092-313">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c092-314">依序選取 [新增]、[情報 + 分析] 及 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="6c092-314">Click **New**, **Intelligence + analytics**, and then **HDInsight**.</span></span>
3. <span data-ttu-id="6c092-315">在 [新增 HDInsight 叢集] 刀鋒視窗中，輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="6c092-315">From the **New HDInsight cluster** blade, enter or select the following values:</span></span>
   
   * <span data-ttu-id="6c092-316">**叢集名稱**︰為已加入網域的 HDInsight 叢集輸入新叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-316">**Cluster name**: Enter a new cluster name for the Domain-joined HDInsight cluster.</span></span>
   * <span data-ttu-id="6c092-317">**訂用帳戶**：選取用來建立此叢集的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c092-317">**Subscription**: Select an Azure subscription used for creating this cluster.</span></span>
   * <span data-ttu-id="6c092-318">**叢集組態**：</span><span class="sxs-lookup"><span data-stu-id="6c092-318">**Cluster configuration**:</span></span>
     
     * <span data-ttu-id="6c092-319">**叢集類型**：Hadoop。</span><span class="sxs-lookup"><span data-stu-id="6c092-319">**Cluster Type**: Hadoop.</span></span> <span data-ttu-id="6c092-320">目前在 Hadoop 叢集上僅支援已加入網域的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="6c092-320">Domain-joined HDInsight is currently only supported on Hadoop clusters.</span></span>
     * <span data-ttu-id="6c092-321">**作業系統**：Linux。</span><span class="sxs-lookup"><span data-stu-id="6c092-321">**Operating System**: Linux.</span></span>  <span data-ttu-id="6c092-322">目前在 Linux 架構的 HDInsight 叢集上僅支援已加入網域的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="6c092-322">Domain-joined HDInsight is only supported on Linux-based HDInsight clusters.</span></span>
     * <span data-ttu-id="6c092-323">**版本**：HDI 3.6。</span><span class="sxs-lookup"><span data-stu-id="6c092-323">**Version**: HDI 3.6.</span></span> <span data-ttu-id="6c092-324">在 HDInsight 叢集版本 3.6 上僅支援已加入網域的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="6c092-324">Domain-joined HDInsight is only supported on HDInsight cluster version 3.6.</span></span>
     * <span data-ttu-id="6c092-325">**叢集類型**：進階 PREMIUM</span><span class="sxs-lookup"><span data-stu-id="6c092-325">**Cluster Type**: PREMIUM</span></span>
       
       <span data-ttu-id="6c092-326">按一下 [選取] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="6c092-326">Click **Select** to save the changes.</span></span>
   * <span data-ttu-id="6c092-327">**認證**︰設定叢集使用者和 SSH 使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="6c092-327">**Credentials**: Configure the credentials for both the cluster user and the SSH user.</span></span>
   * <span data-ttu-id="6c092-328">**資料來源**：建立新的儲存體帳戶或使用現有的儲存體帳戶，做為 HDInsight 叢集的預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c092-328">**Data Source**: Create a new Storage account or use an existing Storage account as the default Storage account for the HDInsight cluster.</span></span> <span data-ttu-id="6c092-329">此位置必須與兩個 VNet 的位置相同。</span><span class="sxs-lookup"><span data-stu-id="6c092-329">The location must be the same as the two VNets.</span></span>  <span data-ttu-id="6c092-330">此位置也是 HDInsight 叢集的位置。</span><span class="sxs-lookup"><span data-stu-id="6c092-330">The location is also the location of the HDInsight cluster.</span></span>
   * <span data-ttu-id="6c092-331">**價格**：選取叢集的背景工作角色節點數目。</span><span class="sxs-lookup"><span data-stu-id="6c092-331">**Pricing**: Select the number of worker nodes of your cluster.</span></span>
   * <span data-ttu-id="6c092-332">**進階組態**：</span><span class="sxs-lookup"><span data-stu-id="6c092-332">**Advanced configurations**:</span></span> 
     
     * <span data-ttu-id="6c092-333">**加入網域與 VNet/子網路**：</span><span class="sxs-lookup"><span data-stu-id="6c092-333">**Domain-joining & Vnet/Subnet**:</span></span> 
       
       * <span data-ttu-id="6c092-334">**網域設定**：</span><span class="sxs-lookup"><span data-stu-id="6c092-334">**Domain settings**:</span></span> 
         
         * <span data-ttu-id="6c092-335">**網域名稱**：contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="6c092-335">**Domain name**: contoso.onmicrosoft.com</span></span>
         * <span data-ttu-id="6c092-336">**網域使用者名稱**：輸入網域使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-336">**Domain user name**: Enter a domain user name.</span></span> <span data-ttu-id="6c092-337">這個網域必須有下列權限︰將電腦加入網域，並將它們放在您於叢集建立期間指定的組織單位內；在您於叢集建立期間指定的組織單位內建立服務主體；建立反向 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="6c092-337">This domain must have the following privileges: Join machines to the domain and place them in the organization unit you specify during cluster creation; Create service principals within the organization unit you specify during cluster creation; Create reverse DNS entries.</span></span> <span data-ttu-id="6c092-338">此網域使用者會成為這個已加入網域的 HDInsight 叢集的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="6c092-338">This domain user will become the administrator of this domain-joined HDInsight cluster.</span></span>
         * <span data-ttu-id="6c092-339">**網域密碼**︰輸入網域使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="6c092-339">**Domain password**: Enter the domain user password.</span></span>
         * <span data-ttu-id="6c092-340">**組織單位**︰輸入您要搭配 HDInsight 叢集使用的 OU 辨別名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-340">**Organization Unit**: Enter the distinguished name of the OU that you want to use with HDInsight cluster.</span></span> <span data-ttu-id="6c092-341">例如：OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com。</span><span class="sxs-lookup"><span data-stu-id="6c092-341">For example: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com.</span></span> <span data-ttu-id="6c092-342">如果此 OU 不存在，HDInsight 叢集會嘗試建立這個 OU。</span><span class="sxs-lookup"><span data-stu-id="6c092-342">If this OU does not exist, HDInsight cluster will attempt to create this OU.</span></span> <span data-ttu-id="6c092-343">確定 OU 已經存在，或是網域帳戶具有建立新 OU 的權限。</span><span class="sxs-lookup"><span data-stu-id="6c092-343">Make sure the OU is already present or the domain account has permissions to create a new one.</span></span> <span data-ttu-id="6c092-344">如果您使用屬於 AADDC 系統管理員的網域帳戶，它就已經有建立 OU 的所需權限。</span><span class="sxs-lookup"><span data-stu-id="6c092-344">If you use the domain account which is part of AADDC Administrators, it will have necessary permissions to create the OU.</span></span>
         * <span data-ttu-id="6c092-345">**LDAPS URL**：ldaps://contoso.onmicrosoft.com:636</span><span class="sxs-lookup"><span data-stu-id="6c092-345">**LDAPS URL**: ldaps://contoso.onmicrosoft.com:636</span></span>
         * <span data-ttu-id="6c092-346">**存取使用者群組**︰指定您要將其使用者同步至叢集的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="6c092-346">**Access user group**: Specify the security group whose users you want to sync to the cluster.</span></span> <span data-ttu-id="6c092-347">例如，HiveUsers。</span><span class="sxs-lookup"><span data-stu-id="6c092-347">For example, HiveUsers.</span></span>
           
           <span data-ttu-id="6c092-348">按一下 [選取] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="6c092-348">Click **Select** to save the changes.</span></span>
           
           ![已加入網域的 HDInsight 入口網站的設定網域](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * <span data-ttu-id="6c092-350">**虛擬網路**：contosohdivnet</span><span class="sxs-lookup"><span data-stu-id="6c092-350">**Virtual Network**: contosohdivnet</span></span>
       * <span data-ttu-id="6c092-351">**子網路**：Subnet1</span><span class="sxs-lookup"><span data-stu-id="6c092-351">**Subnet**: Subnet1</span></span>
         
         <span data-ttu-id="6c092-352">按一下 [選取] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="6c092-352">Click **Select** to save the changes.</span></span>        
         <span data-ttu-id="6c092-353">按一下 [選取] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="6c092-353">Click **Select** to save the changes.</span></span>
   * <span data-ttu-id="6c092-354">**資源群組**：選取用於 HDInsight VNet 的資源群組 (contosohdirg)。</span><span class="sxs-lookup"><span data-stu-id="6c092-354">**Resource Group**: Select the resource group used for the HDInsight VNet (contosohdirg).</span></span>
4. <span data-ttu-id="6c092-355">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6c092-355">Click **Create**.</span></span>  

<span data-ttu-id="6c092-356">建立加入網域的 HDInsight 叢集的另一個選擇，是使用 Azure Resource Management 範本。</span><span class="sxs-lookup"><span data-stu-id="6c092-356">Another option for creating Domain-joined HDInsight cluster is to use Azure Resource Management template.</span></span> <span data-ttu-id="6c092-357">下列程序說明做法：</span><span class="sxs-lookup"><span data-stu-id="6c092-357">The following procedure shows you how:</span></span>

<span data-ttu-id="6c092-358">**使用 Azure Resource Manager 範本建立加入網域的 HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="6c092-358">**To create a Domain-joined HDInsight cluster using a Resource Management template**</span></span>

1. <span data-ttu-id="6c092-359">在 Azure 入口網站中，按一下以下影像以開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6c092-359">Click the following image to open a Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="6c092-360">Resource Manager 範本位於公用 Blob 容器中。</span><span class="sxs-lookup"><span data-stu-id="6c092-360">The Resource Manager template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="6c092-361">在 [參數] 刀鋒視窗中輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="6c092-361">From the **Parameters** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="6c092-362">**訂用帳戶**：(選取您的 Azure 訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="6c092-362">**Subscription**: (Select your Azure subscription).</span></span>
   * <span data-ttu-id="6c092-363">**資源群組**︰ 按一下 [使用現有的]，並指定您剛才使用的同一資源群組。</span><span class="sxs-lookup"><span data-stu-id="6c092-363">**Resource group**: Click **Use existing**, and specify the same resource group you have been using.</span></span>  <span data-ttu-id="6c092-364">例如 contosohdirg。</span><span class="sxs-lookup"><span data-stu-id="6c092-364">For example contosohdirg.</span></span> 
   * <span data-ttu-id="6c092-365">**位置**：指定資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="6c092-365">**Location**: Specify a resource group location.</span></span>
   * <span data-ttu-id="6c092-366">**叢集名稱**：輸入您將建立的 Hadoop 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="6c092-366">**Cluster Name**: Enter a name for the Hadoop cluster that you will create.</span></span> <span data-ttu-id="6c092-367">例如 contosohdicluster。</span><span class="sxs-lookup"><span data-stu-id="6c092-367">For example contosohdicluster.</span></span>
   * <span data-ttu-id="6c092-368">**叢集類型**：選取叢集類型。</span><span class="sxs-lookup"><span data-stu-id="6c092-368">**Cluster Type**: Select a cluster type.</span></span>  <span data-ttu-id="6c092-369">預設值為 **hadoop**。</span><span class="sxs-lookup"><span data-stu-id="6c092-369">The default value is **hadoop**.</span></span>
   * <span data-ttu-id="6c092-370">**位置**：選取叢集的位置。</span><span class="sxs-lookup"><span data-stu-id="6c092-370">**Location**: Select a location for the cluster.</span></span>  <span data-ttu-id="6c092-371">預設儲存體帳戶會使用相同的位置。</span><span class="sxs-lookup"><span data-stu-id="6c092-371">The default storage account uses the same location.</span></span>
   * <span data-ttu-id="6c092-372">**叢集背景工作節點計數**︰選取背景工作角色節點的數目。</span><span class="sxs-lookup"><span data-stu-id="6c092-372">**Cluster Worker Node count**: Select the number of worker nodes.</span></span>
   * <span data-ttu-id="6c092-373">**叢集登入名稱和密碼**：預設登入名稱是 **admin**。</span><span class="sxs-lookup"><span data-stu-id="6c092-373">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="6c092-374">**SSH 使用者名稱和密碼**：預設使用者名稱是 **sshuser**。</span><span class="sxs-lookup"><span data-stu-id="6c092-374">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="6c092-375">您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="6c092-375">You can rename it.</span></span> 
   * <span data-ttu-id="6c092-376">**虛擬網路識別碼**：/subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName></span><span class="sxs-lookup"><span data-stu-id="6c092-376">**Virtual Network Id**: /subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName></span></span>
   * <span data-ttu-id="6c092-377">**虛擬網路子網路**：/subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>/subnets/Subnet1</span><span class="sxs-lookup"><span data-stu-id="6c092-377">**Virtual Network Subnet**: /subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>/subnets/Subnet1</span></span>
   * <span data-ttu-id="6c092-378">**網域名稱**：contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="6c092-378">**Domain Name**: contoso.onmicrosoft.com</span></span>
   * <span data-ttu-id="6c092-379">**組織單位辨別名稱**：OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com</span><span class="sxs-lookup"><span data-stu-id="6c092-379">**Organization Unit DN**: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com</span></span>
   * <span data-ttu-id="6c092-380">**叢集使用者群組 DN**：[\"HiveUsers\"]</span><span class="sxs-lookup"><span data-stu-id="6c092-380">**Cluster Users Group DNs**: [\"HiveUsers\"]</span></span>
   * <span data-ttu-id="6c092-381">**LDAPS URL**：["ldaps://contoso.onmicrosoft.com:636"]</span><span class="sxs-lookup"><span data-stu-id="6c092-381">**LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]</span></span>
   * <span data-ttu-id="6c092-382">**DomainAdminUserName**：(輸入網域系統管理員使用者名稱)</span><span class="sxs-lookup"><span data-stu-id="6c092-382">**DomainAdminUserName**: (Enter the domain admin user name)</span></span>
   * <span data-ttu-id="6c092-383">**DomainAdminPassword**：(輸入網域系統管理員使用者密碼)</span><span class="sxs-lookup"><span data-stu-id="6c092-383">**DomainAdminPassword**: (enter the domain admin user password)</span></span>
   * <span data-ttu-id="6c092-384">**我同意上方所述的條款及條件**：(勾選)</span><span class="sxs-lookup"><span data-stu-id="6c092-384">**I agree to the terms and conditions stated above**: (Check)</span></span>
   * <span data-ttu-id="6c092-385">**釘選到儀表板**：(勾選)</span><span class="sxs-lookup"><span data-stu-id="6c092-385">**Pin to dashboard**: (Check)</span></span>
3. <span data-ttu-id="6c092-386">按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="6c092-386">Click **Purchase**.</span></span> <span data-ttu-id="6c092-387">您將會看到標題為 [進行範本部署] 的新圖格。</span><span class="sxs-lookup"><span data-stu-id="6c092-387">You will see a new tile titled **Deploying Template deployment**.</span></span> <span data-ttu-id="6c092-388">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="6c092-388">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="6c092-389">一旦建立叢集後，您可以在入口網站按一下 [叢集] 刀鋒視窗來開啟它。</span><span class="sxs-lookup"><span data-stu-id="6c092-389">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="6c092-390">完成本教學課程之後，您可以刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="6c092-390">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="6c092-391">利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。</span><span class="sxs-lookup"><span data-stu-id="6c092-391">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="6c092-392">您也需支付 HDInsight 叢集的費用 (即使未使用)。</span><span class="sxs-lookup"><span data-stu-id="6c092-392">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="6c092-393">由於叢集費用是儲存體費用的許多倍，所以刪除未使用的叢集符合經濟效益。</span><span class="sxs-lookup"><span data-stu-id="6c092-393">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="6c092-394">如需有關刪除叢集的指示，請參閱[使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集](hdinsight-administer-use-management-portal.md#delete-clusters)。</span><span class="sxs-lookup"><span data-stu-id="6c092-394">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c092-395">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c092-395">Next steps</span></span>
* <span data-ttu-id="6c092-396">如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="6c092-396">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="6c092-397">如需使用 SSH 連線到已加入網域的 HDInsight 叢集，請參閱[從 Linux、Unix 或 OS X 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。</span><span class="sxs-lookup"><span data-stu-id="6c092-397">For using SSH to connect to Domain-joined HDInsight clusters, see [Use SSH with Linux-based Hadoop on HDInsight from Linux, Unix, or OS X](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>

