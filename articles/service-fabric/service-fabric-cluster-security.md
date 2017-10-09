---
title: "aaaSecure Service Fabric 叢集 |Microsoft 文件"
description: "說明 Service Fabric 叢集和 hello 所用的不同技術 tooimplement hello 安全性案例的情況。"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a><span data-ttu-id="21fc5-103">Service Fabric 叢集安全性案例</span><span class="sxs-lookup"><span data-stu-id="21fc5-103">Service Fabric cluster security scenarios</span></span>
<span data-ttu-id="21fc5-104">Service Fabric 叢集是您所擁有的資源。</span><span class="sxs-lookup"><span data-stu-id="21fc5-104">A Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="21fc5-105">叢集必須是安全的 tooprevent 未經授權的使用者連接 tooyour 叢集，尤其是當它已在其上執行的實際執行工作負載。</span><span class="sxs-lookup"><span data-stu-id="21fc5-105">Clusters must be secured tooprevent unauthorized users from connecting tooyour cluster, especially when it has production workloads running on it.</span></span> <span data-ttu-id="21fc5-106">雖然可能 toocreate 不安全的叢集，這樣做可讓匿名使用者 tooconnect tooit，如果它會公開管理端點 toohello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="21fc5-106">Although it is possible toocreate an unsecured cluster, doing so allows anonymous users tooconnect tooit, if it exposes management endpoints toohello public Internet.</span></span> 

<span data-ttu-id="21fc5-107">本文概述 hello 安全性案例的叢集在 Azure 或獨立執行，且 hello 各種所用技術 tooimplement 的情況。</span><span class="sxs-lookup"><span data-stu-id="21fc5-107">This article provides an overview of hello security scenarios for clusters running on Azure or standalone and hello various technologies used tooimplement those scenarios.</span></span> <span data-ttu-id="21fc5-108">hello 叢集安全性案例包括：</span><span class="sxs-lookup"><span data-stu-id="21fc5-108">hello cluster security scenarios are:</span></span>

* <span data-ttu-id="21fc5-109">節點對節點安全性</span><span class="sxs-lookup"><span data-stu-id="21fc5-109">Node-to-node security</span></span>
* <span data-ttu-id="21fc5-110">用戶端對節點安全性</span><span class="sxs-lookup"><span data-stu-id="21fc5-110">Client-to-node security</span></span>
* <span data-ttu-id="21fc5-111">角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="21fc5-111">Role-based access control (RBAC)</span></span>

## <a name="node-to-node-security"></a><span data-ttu-id="21fc5-112">節點對節點安全性</span><span class="sxs-lookup"><span data-stu-id="21fc5-112">Node-to-node security</span></span>
<span data-ttu-id="21fc5-113">保護 hello Vm 或 hello 叢集中的機器之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="21fc5-113">Secures communication between hello VMs or machines in hello cluster.</span></span> <span data-ttu-id="21fc5-114">這可確保只有授權的 toojoin hello 叢集的電腦可以參與裝載應用程式和服務 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="21fc5-114">This ensures that only computers that are authorized toojoin hello cluster can participate in hosting applications and services in hello cluster.</span></span>

![節點對節點通訊的圖表][Node-to-Node]

<span data-ttu-id="21fc5-116">在 Azure 上執行的叢集或在 Windows 上執行的獨立叢集可以使用[憑證安全性](https://msdn.microsoft.com/library/ff649801.aspx)或針對 Windows Server 機器使用 [Windows 安全性](https://msdn.microsoft.com/library/ff649396.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-116">Clusters running on Azure or standalone clusters running on Windows can use either [Certificate Security](https://msdn.microsoft.com/library/ff649801.aspx) or [Windows Security](https://msdn.microsoft.com/library/ff649396.aspx) for Windows Server machines.</span></span>

### <a name="node-to-node-certificate-security"></a><span data-ttu-id="21fc5-117">節點對節點憑證安全性</span><span class="sxs-lookup"><span data-stu-id="21fc5-117">Node-to-node certificate security</span></span>
<span data-ttu-id="21fc5-118">服務網狀架構會使用 X.509 伺服器憑證，當您建立叢集時，您指定為 hello 節點型別組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="21fc5-118">Service Fabric uses X.509 server certificates that you specify as a part of hello node-type configurations when you create a cluster.</span></span> <span data-ttu-id="21fc5-119">這篇文章的 hello 結尾會提供這些憑證是什麼，以及如何取得，或建立它們的快速概觀。</span><span class="sxs-lookup"><span data-stu-id="21fc5-119">A quick overview of what these certificates are and how you can acquire or create them is provided at hello end of this article.</span></span>

<span data-ttu-id="21fc5-120">憑證的安全性設定時建立 hello 叢集透過 hello Azure 入口網站、 Azure Resource Manager 範本或獨立 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="21fc5-120">Certificate security is configured while creating hello cluster either through hello Azure portal, Azure Resource Manager templates, or a standalone JSON template.</span></span> <span data-ttu-id="21fc5-121">您可以指定用於憑證變換的主要憑證和選用次要憑證。</span><span class="sxs-lookup"><span data-stu-id="21fc5-121">You can specify a primary certificate and an optional secondary certificate that is used for certificate rollovers.</span></span> <span data-ttu-id="21fc5-122">hello 您指定的主要和次要憑證應不同於 hello 管理用戶端以及您針對指定的唯讀用戶端憑證[用戶端對節點安全性](#client-to-node-security)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-122">hello primary and secondary certificates you specify should be different than hello admin client and read-only client certificates you specify for [Client-to-node security](#client-to-node-security).</span></span>

<span data-ttu-id="21fc5-123">讀取 Azure[設定叢集，利用 Azure 資源管理員範本](service-fabric-cluster-creation-via-arm.md)toolearn tooconfigure 憑證安全性在叢集中的方式。</span><span class="sxs-lookup"><span data-stu-id="21fc5-123">For Azure read [Set up a cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) toolearn how tooconfigure certificate security in a cluster.</span></span>

<span data-ttu-id="21fc5-124">對於獨立 Windows Server，請參閱 [使用 X.509 憑證保護 Windows 上的獨立叢集 ](service-fabric-windows-cluster-x509-security.md)</span><span class="sxs-lookup"><span data-stu-id="21fc5-124">For standalone Windows Server read [Secure a standalone cluster on Windows using X.509 certificates ](service-fabric-windows-cluster-x509-security.md)</span></span>

### <a name="node-to-node-windows-security"></a><span data-ttu-id="21fc5-125">節點對節點 Windows 安全性</span><span class="sxs-lookup"><span data-stu-id="21fc5-125">Node-to-node windows security</span></span>
<span data-ttu-id="21fc5-126">對於獨立 Windows Server，請參閱 [使用 Windows 安全性保護 Windows 上的獨立叢集](service-fabric-windows-cluster-windows-security.md)</span><span class="sxs-lookup"><span data-stu-id="21fc5-126">For standalone Windows Server read [Secure a standalone cluster on Windows using Windows security](service-fabric-windows-cluster-windows-security.md)</span></span>

## <a name="client-to-node-security"></a><span data-ttu-id="21fc5-127">用戶端對節點安全性</span><span class="sxs-lookup"><span data-stu-id="21fc5-127">Client-to-node security</span></span>
<span data-ttu-id="21fc5-128">驗證用戶端，及保護在用戶端與 hello 叢集中的個別節點之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="21fc5-128">Authenticates clients and secures communication between a client and individual nodes in hello cluster.</span></span> <span data-ttu-id="21fc5-129">這種類型的安全性驗證，並保護可確保只有授權的使用者可以存取 hello 叢集和 hello 叢集上部署的 hello 應用程式的用戶端通訊。</span><span class="sxs-lookup"><span data-stu-id="21fc5-129">This type of security authenticates and secures client communications, which ensures that only authorized users can access hello cluster and hello applications deployed on hello cluster.</span></span> <span data-ttu-id="21fc5-130">用戶端是透過其 Windows 安全性認證或其憑證安全性認證唯一識別。</span><span class="sxs-lookup"><span data-stu-id="21fc5-130">Clients are uniquely identified through either their Windows Security credentials or their certificate security credentials.</span></span>

![用戶端對節點通訊的圖表][Client-to-Node]

<span data-ttu-id="21fc5-132">在 Azure 上執行的叢集或在 Windows 上執行的獨立叢集可以使用[憑證安全性](https://msdn.microsoft.com/library/ff649801.aspx)或 [Windows 安全性](https://msdn.microsoft.com/library/ff649396.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-132">Clusters running on Azure or standalone clusters running on Windows can use either [Certificate Security](https://msdn.microsoft.com/library/ff649801.aspx) or [Windows Security](https://msdn.microsoft.com/library/ff649396.aspx).</span></span>

### <a name="client-to-node-certificate-security"></a><span data-ttu-id="21fc5-133">用戶端對節點憑證安全性</span><span class="sxs-lookup"><span data-stu-id="21fc5-133">Client-to-node certificate security</span></span>
 <span data-ttu-id="21fc5-134">用戶端對節點憑證的安全性設定時指定的系統管理員用戶端憑證及/或使用者的用戶端憑證，藉以建立 hello 叢集透過 hello Azure 入口網站中，資源管理員範本或獨立 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="21fc5-134">Client-to-node certificate security is configured while creating hello cluster either through hello Azure portal, Resource Manager templates or a standalone JSON template by specifying an admin client certificate and/or a user client certificate.</span></span>  <span data-ttu-id="21fc5-135">hello 管理用戶端和使用者用戶端憑證指定應該與不同 hello 主要和次要憑證指定為[節點對節點安全性](#node-to-node-security)最佳作法。</span><span class="sxs-lookup"><span data-stu-id="21fc5-135">hello admin client and user client certificates you specify should be different than hello primary and secondary certificates you specify for [Node-to-node security](#node-to-node-security) as a best practice.</span></span> <span data-ttu-id="21fc5-136">根據預設，hello 叢集節點的安全性憑證會加入 toohello 允許用戶端管理的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="21fc5-136">By default, hello cluster certificates for node-to-node security are added toohello allowed client Admin certificates list.</span></span>

<span data-ttu-id="21fc5-137">連接 toohello 叢集使用 hello 管理憑證的用戶端具有完整存取 toomanagement 功能。</span><span class="sxs-lookup"><span data-stu-id="21fc5-137">Clients connecting toohello cluster using hello admin certificate have full access toomanagement capabilities.</span></span>  <span data-ttu-id="21fc5-138">連接 toohello 叢集使用 hello 唯讀使用者用戶端憑證的用戶端擁有讀取權限 toomanagement 功能。</span><span class="sxs-lookup"><span data-stu-id="21fc5-138">Clients connecting toohello cluster using hello read-only user client certificate have only read access toomanagement capabilities.</span></span> <span data-ttu-id="21fc5-139">亦即這些憑證用於 hello 角色基底存取控制 (RBAC) 本文稍後所述。</span><span class="sxs-lookup"><span data-stu-id="21fc5-139">In other words these certificates are used for hello role bases access control (RBAC) described later in this article.</span></span>

<span data-ttu-id="21fc5-140">讀取 Azure[設定叢集，利用 Azure 資源管理員範本](service-fabric-cluster-creation-via-arm.md)toolearn tooconfigure 憑證安全性在叢集中的方式。</span><span class="sxs-lookup"><span data-stu-id="21fc5-140">For Azure read [Set up a cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) toolearn how tooconfigure certificate security in a cluster.</span></span>

<span data-ttu-id="21fc5-141">對於獨立 Windows Server，請參閱 [使用 X.509 憑證保護 Windows 上的獨立叢集 ](service-fabric-windows-cluster-x509-security.md)</span><span class="sxs-lookup"><span data-stu-id="21fc5-141">For standalone Windows Server read [Secure a standalone cluster on Windows using X.509 certificates ](service-fabric-windows-cluster-x509-security.md)</span></span>

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a><span data-ttu-id="21fc5-142">Azure 上的用戶端對節點 Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="21fc5-142">Client-to-node Azure Active Directory (AAD) security on Azure</span></span>
<span data-ttu-id="21fc5-143">在 Azure 上執行的叢集也可以保護存取使用 Azure Active Directory (AAD) toohello 管理端點。</span><span class="sxs-lookup"><span data-stu-id="21fc5-143">Clusters running on Azure can also secure access toohello management endpoints using Azure Active Directory (AAD).</span></span> <span data-ttu-id="21fc5-144">請參閱[設定叢集，利用 Azure 資源管理員範本](service-fabric-cluster-creation-via-arm.md)如需如何 toocreate hello 需要 AAD 成品時，如何 toopopulate 期間叢集建立和 tooconnect toothose 之後叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="21fc5-144">See [Set up a cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) for information on how toocreate hello necessary AAD artifacts, how toopopulate them during cluster creation, and how tooconnect toothose clusters afterwards.</span></span>

## <a name="security-recommendations"></a><span data-ttu-id="21fc5-145">安全性建議</span><span class="sxs-lookup"><span data-stu-id="21fc5-145">Security Recommendations</span></span>
<span data-ttu-id="21fc5-146">Azure 的叢集，建議您使用用戶端的安全性 tooauthenticate AAD 和憑證節點對節點的安全性。</span><span class="sxs-lookup"><span data-stu-id="21fc5-146">For Azure clusters, it is recommended that you use AAD security tooauthenticate clients and certificates for node-to-node security.</span></span>

<span data-ttu-id="21fc5-147">對於獨立 Windows Server 叢集，如果您有 Windows Server 2012 R2 和 Active Directory，建議您使用 Windows 安全性與群組管理帳戶 (GMA)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-147">For standalone Windows Server clusters it is recommended that you use Windows security with group managed accounts (GMA) if you have Windows Server 2012 R2 and Active Directory.</span></span> <span data-ttu-id="21fc5-148">否則仍然使用 Windows 安全性與 Windows 帳戶。</span><span class="sxs-lookup"><span data-stu-id="21fc5-148">Otherwise still use Windows security with Windows accounts.</span></span>

## <a name="role-based-access-control-rbac"></a><span data-ttu-id="21fc5-149">角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="21fc5-149">Role based access control (RBAC)</span></span>
<span data-ttu-id="21fc5-150">存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 叢集作業會針對不同使用者群組，讓 hello 叢集更安全。</span><span class="sxs-lookup"><span data-stu-id="21fc5-150">Access control allows hello cluster administrator toolimit access toocertain cluster operations for different groups of users, making hello cluster more secure.</span></span> <span data-ttu-id="21fc5-151">兩個不同的存取控制項類型支援連接 tooa 叢集的用戶端： 系統管理員角色和使用者角色。</span><span class="sxs-lookup"><span data-stu-id="21fc5-151">Two different access control types are supported for clients connecting tooa cluster: Administrator role and User role.</span></span>

<span data-ttu-id="21fc5-152">系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。</span><span class="sxs-lookup"><span data-stu-id="21fc5-152">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="21fc5-153">使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="21fc5-153">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>

<span data-ttu-id="21fc5-154">您指定 hello 系統管理員和使用者用戶端角色 hello 叢集建立時提供不同的身分識別 （憑證，AAD 等） 針對每個。</span><span class="sxs-lookup"><span data-stu-id="21fc5-154">You specify hello administrator and user client roles at hello time of cluster creation by providing separate identities (certificates, AAD etc.) for each.</span></span> <span data-ttu-id="21fc5-155">如需有關 hello 預設存取控制設定，以及如何 toochange hello 預設設定的詳細資訊，請參閱[角色型存取控制服務網狀架構用戶端](service-fabric-cluster-security-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-155">For more information on hello default access control settings and how toochange hello default settings, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>

## <a name="x509-certificates-and-service-fabric"></a><span data-ttu-id="21fc5-156">X.509 憑證和 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="21fc5-156">X.509 certificates and Service Fabric</span></span>
<span data-ttu-id="21fc5-157">X.509 數位憑證是常用的 tooauthenticate 用戶端和伺服器與 tooencrypt 以及數位簽署訊息。</span><span class="sxs-lookup"><span data-stu-id="21fc5-157">X.509 digital certificates are commonly used tooauthenticate clients and servers and tooencrypt and digitally sign messages.</span></span> <span data-ttu-id="21fc5-158">如需有關這些憑證的詳細資訊，請移至太[使用憑證](http://msdn.microsoft.com/library/ms731899.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-158">For more details on these certificates, go too[Working with certificates](http://msdn.microsoft.com/library/ms731899.aspx).</span></span>

<span data-ttu-id="21fc5-159">一些重要事項 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="21fc5-159">Some important things tooconsider:</span></span>

* <span data-ttu-id="21fc5-160">執行生產環境工作負載之叢集中所使用的憑證應該是使用已正確設定的 Windows Server 憑證服務來建立，或是從已核准的 [憑證授權單位 (CA)](https://en.wikipedia.org/wiki/Certificate_authority)取得。</span><span class="sxs-lookup"><span data-stu-id="21fc5-160">Certificates used in clusters running production workloads should be created by using a correctly configured Windows Server certificate service or obtained from an approved [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority).</span></span>
* <span data-ttu-id="21fc5-161">絕對不要在生產環境中使用以 MakeCert.exe 這類工具建立的暫時或測試憑證。</span><span class="sxs-lookup"><span data-stu-id="21fc5-161">Never use any temporary or test certificates in production that are created with tools such as MakeCert.exe.</span></span>
* <span data-ttu-id="21fc5-162">您可以使用自我簽署憑證，但應該只用於測試叢集，不應該在生產環境中使用。</span><span class="sxs-lookup"><span data-stu-id="21fc5-162">You can use a self-signed certificate, but should only do so for test clusters and not in production.</span></span>

### <a name="server-x509-certificates"></a><span data-ttu-id="21fc5-163">伺服器的 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="21fc5-163">Server X.509 certificates</span></span>
<span data-ttu-id="21fc5-164">伺服器憑證有 hello 主要工作就是驗證伺服器 （節點） tooclients，或驗證伺服器 （節點） tooa 伺服器 （節點）。</span><span class="sxs-lookup"><span data-stu-id="21fc5-164">Server certificates have hello primary task of authenticating a server (node) tooclients, or authenticating a server (node) tooa server (node).</span></span> <span data-ttu-id="21fc5-165">Toocheck hello 值 hello hello [主旨] 欄位中的一般名稱的其中一個 hello 初始檢查時用戶端或節點來驗證節點。</span><span class="sxs-lookup"><span data-stu-id="21fc5-165">One of hello initial checks when a client or node authenticates a node is toocheck hello value of hello common name in hello Subject field.</span></span> <span data-ttu-id="21fc5-166">此一般名稱或其中一個 hello 憑證的主體別名中必須要有 hello 的允許通用名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="21fc5-166">Either this common name or one of hello certificates' subject alternative names must be present in hello list of allowed common names.</span></span>

<span data-ttu-id="21fc5-167">hello 下列文章說明如何 toogenerate 憑證的主體別名 (SAN): [tooadd 主旨替代名稱 tooa 如何安全 LDAP 的憑證](http://support.microsoft.com/kb/931351)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-167">hello following article describes how toogenerate certificates with subject alternative names (SAN): [How tooadd a subject alternative name tooa secure LDAP certificate](http://support.microsoft.com/kb/931351).</span></span>

<span data-ttu-id="21fc5-168">hello 主旨欄位只能包含數個值，每一個加上初始化 tooindicate hello 實值型別。</span><span class="sxs-lookup"><span data-stu-id="21fc5-168">hello Subject field can contain several values, each prefixed with an initialization tooindicate hello value type.</span></span> <span data-ttu-id="21fc5-169">Hello 初始化大多數情況下，"CN"為一般名稱。例如，"CN = www.contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="21fc5-169">Most commonly, hello initialization is "CN" for common name; for example, "CN = www.contoso.com".</span></span> <span data-ttu-id="21fc5-170">它也可能會 hello 主旨欄位 toobe 空白。</span><span class="sxs-lookup"><span data-stu-id="21fc5-170">It is also possible for hello Subject field toobe blank.</span></span> <span data-ttu-id="21fc5-171">如果已填入 hello 選擇性主體替代名稱欄位，則必須包含 hello hello 憑證一般名稱和每個主體替代名稱的一個項目。</span><span class="sxs-lookup"><span data-stu-id="21fc5-171">If hello optional Subject Alternative Name field is populated, it must contain both hello common name of hello certificate and one entry per subject alternative name.</span></span> <span data-ttu-id="21fc5-172">這些會被輸入為 DNS 名稱值。</span><span class="sxs-lookup"><span data-stu-id="21fc5-172">These are entered as DNS Name values.</span></span>

<span data-ttu-id="21fc5-173">hello hello hello 憑證使用目的欄位值應該包含適當的值，例如 「 伺服器驗證 」 或 「 用戶端驗證 」。</span><span class="sxs-lookup"><span data-stu-id="21fc5-173">hello value of hello Intended Purposes field of hello certificate should include an appropriate value, such as "Server Authentication" or "Client Authentication".</span></span>

### <a name="client-x509-certificates"></a><span data-ttu-id="21fc5-174">用戶端 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="21fc5-174">Client X.509 certificates</span></span>
<span data-ttu-id="21fc5-175">用戶端憑證通常不是由第三方憑證授權單位所發行。</span><span class="sxs-lookup"><span data-stu-id="21fc5-175">Client certificates are not typically issued by a third-party certificate authority.</span></span> <span data-ttu-id="21fc5-176">相反地，hello hello 目前使用者位置的個人存放區通常包含用戶端憑證放在該處根授權單位，與目的為 「 用戶端驗證 」。</span><span class="sxs-lookup"><span data-stu-id="21fc5-176">Instead, hello Personal store of hello current user location typically contains client certificates placed there by a root authority, with an intended purpose of "Client Authentication".</span></span> <span data-ttu-id="21fc5-177">hello 用戶端需要相互驗證時，可以使用這類憑證。</span><span class="sxs-lookup"><span data-stu-id="21fc5-177">hello client can use such a certificate when mutual authentication is required.</span></span>

> [!NOTE]
> <span data-ttu-id="21fc5-178">Service Fabric 叢集上的所有管理作業都需要伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="21fc5-178">All management operations on a Service Fabric cluster require server certificates.</span></span> <span data-ttu-id="21fc5-179">用戶端憑證無法用於管理作業。</span><span class="sxs-lookup"><span data-stu-id="21fc5-179">Client certificates cannot be used for management.</span></span>
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a><span data-ttu-id="21fc5-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21fc5-180">Next steps</span></span>
<span data-ttu-id="21fc5-181">本文提供與叢集安全性有關的概念資訊。</span><span class="sxs-lookup"><span data-stu-id="21fc5-181">This article provides conceptual information about cluster security.</span></span> <span data-ttu-id="21fc5-182">接下來，</span><span class="sxs-lookup"><span data-stu-id="21fc5-182">Next,</span></span>


1.  [<span data-ttu-id="21fc5-183">使用 Resource Manager 範本在 Azure 中建立叢集</span><span class="sxs-lookup"><span data-stu-id="21fc5-183">create a cluster in Azure using a Resource Manager template</span></span>](service-fabric-cluster-creation-via-arm.md) 
2.  <span data-ttu-id="21fc5-184">[Azure 入口網站](service-fabric-cluster-creation-via-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="21fc5-184">[Azure portal](service-fabric-cluster-creation-via-portal.md).</span></span>

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
