---
title: "多租用戶 Web 應用程式模式 | Microsoft Docs"
description: "找出說明如何在 Azure 實作多租用戶 Web 應用程式的結構概觀和設計模式。"
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 57ba0e46139bda2d74c9f7db0ffab2f2122b0df2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="multitenant-applications-in-azure"></a><span data-ttu-id="649d4-103">Azure 中的多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="649d4-103">Multitenant Applications in Azure</span></span>
<span data-ttu-id="649d4-104">多租用戶應用程式是一種共用資源，可讓個別使用者 (或「租用戶」) 將應用程式視為其本身的應用程式。</span><span class="sxs-lookup"><span data-stu-id="649d4-104">A multitenant application is a shared resource that allows separate users, or "tenants," to view the application as though it was their own.</span></span> <span data-ttu-id="649d4-105">適用多租用戶應用程式的常見情況，是應用程式的所有使用者都想自訂個人的使用性，但另一方面又有相同的基本商業需求時。</span><span class="sxs-lookup"><span data-stu-id="649d4-105">A typical scenario that lends itself to a multitenant application is one in which all users of the application may wish to customize the user experience but otherwise have the same basic business requirements.</span></span> <span data-ttu-id="649d4-106">舉例來說，Office 365、Outlook.com 和 visualstudio.com 都屬於大型多租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="649d4-106">Examples of large multitenant applications are Office 365, Outlook.com, and visualstudio.com.</span></span>

<span data-ttu-id="649d4-107">就應用程式提供者的觀點而言，多租用戶的好處大多與營運和成本效益有關。</span><span class="sxs-lookup"><span data-stu-id="649d4-107">From an application provider's perspective, the benefits of multitenancy mostly relate to operational and cost efficiencies.</span></span> <span data-ttu-id="649d4-108">您的某個應用程式版本可能符合許多租用戶/客戶的需求，而促使監視、效能調整、軟體維護和資料備份等系統管理工作得以整合。</span><span class="sxs-lookup"><span data-stu-id="649d4-108">One version of your application can meet the needs of many tenants/customers, allowing consolidation of system administration tasks such as monitoring, performance tuning, software maintenance, and data backups.</span></span>

<span data-ttu-id="649d4-109">以下將以提供者的角度列舉最重要的目標和需求。</span><span class="sxs-lookup"><span data-stu-id="649d4-109">The following provides a list of the most significant goals and requirements from a provider's perspective.</span></span>

* <span data-ttu-id="649d4-110">**佈建**：您必須能夠為應用程式佈建新的租用戶。</span><span class="sxs-lookup"><span data-stu-id="649d4-110">**Provisioning**: You must be able to provision new tenants for the application.</span></span>  <span data-ttu-id="649d4-111">就租用戶為數眾多的多租用戶應用程式而言，通常必須藉由啟用自助式佈建功能將此程序自動化。</span><span class="sxs-lookup"><span data-stu-id="649d4-111">For multitenant applications with a large number of tenants, it is usually necessary to automate this process by enabling self-service provisioning.</span></span>
* <span data-ttu-id="649d4-112">**可維護性**：您必須能夠在多名租用戶使用應用程式時，升級應用程式和執行其他維護工作。</span><span class="sxs-lookup"><span data-stu-id="649d4-112">**Maintainability**: You must be able to upgrade the application and perform other maintenance tasks while multiple tenants are using it.</span></span>
* <span data-ttu-id="649d4-113">**監視**：您必須能夠不間斷地監視應用程式，以識別出所有問題並加以疑難排解。</span><span class="sxs-lookup"><span data-stu-id="649d4-113">**Monitoring**: You must be able to monitor the application at all times to identify any problems and to troubleshoot them.</span></span> <span data-ttu-id="649d4-114">監視每個租用戶使用應用程式的情形，也是其中一環。</span><span class="sxs-lookup"><span data-stu-id="649d4-114">This includes monitoring how each tenant is using the application.</span></span>

<span data-ttu-id="649d4-115">適當實作的多租用戶應用程式，可為使用者提供下列好處。</span><span class="sxs-lookup"><span data-stu-id="649d4-115">A properly implemented multitenant application provides the following benefits to users.</span></span>

* <span data-ttu-id="649d4-116">**隔離**：個別租用戶的活動不會影響其他租用戶使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="649d4-116">**Isolation**: The activities of individual tenants do not affect the use of the application by other tenants.</span></span> <span data-ttu-id="649d4-117">租用戶之間無法相互存取資料。</span><span class="sxs-lookup"><span data-stu-id="649d4-117">Tenants cannot access each other's data.</span></span> <span data-ttu-id="649d4-118">對租用戶而言，應用程式就如同是他們專用的一般。</span><span class="sxs-lookup"><span data-stu-id="649d4-118">It appears to the tenant as though they have exclusive use of the application.</span></span>
* <span data-ttu-id="649d4-119">**可用性**：個別租用戶希望應用程式能持續保有可用性，若能在 SLA 中明訂相關保證最好。</span><span class="sxs-lookup"><span data-stu-id="649d4-119">**Availability**: Individual tenants want the application to be constantly available, perhaps with guarantees defined in an SLA.</span></span> <span data-ttu-id="649d4-120">再次重申，其他租用戶的活動不會影響應用程式的可用性。</span><span class="sxs-lookup"><span data-stu-id="649d4-120">Again, the activities of other tenants should not affect the availability of the application.</span></span>
* <span data-ttu-id="649d4-121">**延展性**：應用程式可根據個別租用戶的需求調整。</span><span class="sxs-lookup"><span data-stu-id="649d4-121">**Scalability**: The application scales to meet the demand of individual tenants.</span></span> <span data-ttu-id="649d4-122">其他租用戶的存在與動作不會影響應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="649d4-122">The presence and actions of other tenants should not affect the performance of the application.</span></span>
* <span data-ttu-id="649d4-123">**成本**：成本比執行專用的單一租用戶應用程式低廉，因為在多租用的環境下可共用資源。</span><span class="sxs-lookup"><span data-stu-id="649d4-123">**Costs**: Costs are lower than running a dedicated, single-tenant application because multi-tenancy enables the sharing of resources.</span></span>
* <span data-ttu-id="649d4-124">**自訂能力**。</span><span class="sxs-lookup"><span data-stu-id="649d4-124">**Customizability**.</span></span> <span data-ttu-id="649d4-125">能夠以各種方式為個別租用戶自訂應用程式，例如新增或移除功能、變更色彩或標誌，甚或新增自己的程式碼或指令碼。</span><span class="sxs-lookup"><span data-stu-id="649d4-125">The ability to customize the application for an individual tenant in various ways such as adding or removing features, changing colors and logos, or even adding their own code or script.</span></span>

<span data-ttu-id="649d4-126">簡言之，要提供具有高度延展性的服務，的確需要考量許多事項，但也有不少目標和需求是許多多租用戶應用程式所共有的。</span><span class="sxs-lookup"><span data-stu-id="649d4-126">In short, while there are many considerations that you must take into account to provide a highly scalable service, there are also a number of the goals and requirements that are common to many multitenant applications.</span></span> <span data-ttu-id="649d4-127">有些可能與特定案例無關，且個別目標和需求的重要性也可能隨著案例而不同。</span><span class="sxs-lookup"><span data-stu-id="649d4-127">Some may not be relevant in specific scenarios, and the importance of individual goals and requirements will differ in each scenario.</span></span> <span data-ttu-id="649d4-128">如果您是多租用戶應用程式的提供者，您也會有目標和需求，例如：達到租用戶的目標和需求、利潤、收費、多重服務層級、佈建、可維護性監視和自動化等。</span><span class="sxs-lookup"><span data-stu-id="649d4-128">As a provider of the multitenant application, you will also have goals and requirements such as, meeting the tenants' goals and requirements, profitability, billing, multiple service levels, provisioning, maintainability monitoring, and automation.</span></span>

<span data-ttu-id="649d4-129">若想進一步了解多租用戶應用程式的其他設計注意事項，請參閱[在 Azure 上裝載多租用戶應用程式][Hosting a Multi-Tenant Application on Azure] \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="649d4-129">For more information on additional design considerations of a multitenant application, see [Hosting a Multi-Tenant Application on Azure][Hosting a Multi-Tenant Application on Azure].</span></span> <span data-ttu-id="649d4-130">如需多租用戶型軟體即服務 (SaaS) 資料庫應用程式的常見資料架構模式的資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="649d4-130">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span> 

<span data-ttu-id="649d4-131">Azure 有多項功能可讓您處理在設計多租用戶系統時遇到的重大問題。</span><span class="sxs-lookup"><span data-stu-id="649d4-131">Azure provides many features that allow you to address the key problems encountered when designing a multitenant system.</span></span>

<span data-ttu-id="649d4-132">**隔離**</span><span class="sxs-lookup"><span data-stu-id="649d4-132">**Isolation**</span></span>

* <span data-ttu-id="649d4-133">依主機標頭區隔具有 (或沒有) SSL 通訊的網站租用戶</span><span class="sxs-lookup"><span data-stu-id="649d4-133">Segment Website Tenants by Host Headers with or without SSL communication</span></span>
* <span data-ttu-id="649d4-134">依查詢參數區隔網站租用戶</span><span class="sxs-lookup"><span data-stu-id="649d4-134">Segment Website Tenants by Query Parameters</span></span>
* <span data-ttu-id="649d4-135">背景工作角色中的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="649d4-135">Web Services in Worker Roles</span></span>
  * <span data-ttu-id="649d4-136">背景工作角色：</span><span class="sxs-lookup"><span data-stu-id="649d4-136">Worker Roles.</span></span> <span data-ttu-id="649d4-137">通常在應用程式後端處理資料。</span><span class="sxs-lookup"><span data-stu-id="649d4-137">that typically process data on the backend of an application.</span></span>
  * <span data-ttu-id="649d4-138">通常作為應用程式前端的 Web 角色。</span><span class="sxs-lookup"><span data-stu-id="649d4-138">Web Roles that typically act as the frontend for applications.</span></span>

<span data-ttu-id="649d4-139">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="649d4-139">**Storage**</span></span>

<span data-ttu-id="649d4-140">資料管理 (例如 Azure SQL Database) 或 Azure 儲存體服務 (例如為大量非結構化資料提供儲存服務的表格服務)，以及為大量非結構化文字或二進位資料 (例如視訊、音訊和影像) 提供儲存服務的 Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="649d4-140">Data management such as Azure SQL Database or Azure Storage services such as the Table service which provides services for storage of large amounts of unstructured data and the Blob service which provides services to store large amounts of unstructured text or binary data such as video, audio and images.</span></span>

* <span data-ttu-id="649d4-141">在 SQL Database 中保護多租用戶資料的安全：適當的個別租用戶 SQL Server 登入。</span><span class="sxs-lookup"><span data-stu-id="649d4-141">Securing Multitenant Data in SQL Database appropriate per-tenant SQL Server logins.</span></span>
* <span data-ttu-id="649d4-142">使用適用於應用程式資源的 Azure 資料表：指定容器層級存取原則，將使您能夠直接調整權限，而無須針對受到共用存取簽章保護的資源發出新的 URL。</span><span class="sxs-lookup"><span data-stu-id="649d4-142">Using Azure Tables for Application Resources By specifying a container level access policy, you can the ability to adjust permissions without having to issue new URL's for the resources protected with shared access signatures.</span></span>
* <span data-ttu-id="649d4-143">適用於應用程式資源的 Azure 佇列：Azure 佇列通常用來協助租用戶執行處理，但也可用來配送佈建或管理所需的工作。</span><span class="sxs-lookup"><span data-stu-id="649d4-143">Azure Queues for Application Resources Azure queues are commonly used to drive processing on behalf of tenants, but may also be used to distribute work required for provisioning or management.</span></span>
* <span data-ttu-id="649d4-144">適用於應用程式資源的服務匯流排佇列可將工作發送至共用服務，因此您可以使用單一佇列，讓每個租用戶傳送者僅具有推送至該佇列的權限 (衍生自 ACS 所發出的宣告)，同時只讓服務的接收者有權從佇列中提取多個租用戶所傳來的資料。</span><span class="sxs-lookup"><span data-stu-id="649d4-144">Service Bus Queues for Application Resources that pushes work to a shared a service, you can use a single queue where each tenant sender only has permissions (as derived from claims issued from ACS) to push to that queue, while only the receivers from the service have permission to pull from the queue the data coming from multiple tenants.</span></span>

<span data-ttu-id="649d4-145">**連接和安全性服務**</span><span class="sxs-lookup"><span data-stu-id="649d4-145">**Connection and Security Services**</span></span>

* <span data-ttu-id="649d4-146">Azure 服務匯流排是存在於應用程式之間的訊息基礎結構，可讓應用程式以鬆散耦合的方式交換訊息，以提升延展性與恢復能力。</span><span class="sxs-lookup"><span data-stu-id="649d4-146">Azure Service Bus, a messaging infrastructure that sits between applications allowing them to exchange messages in a loosely coupled way for improved scale and resiliency.</span></span>

<span data-ttu-id="649d4-147">**網路服務**</span><span class="sxs-lookup"><span data-stu-id="649d4-147">**Networking Services**</span></span>

<span data-ttu-id="649d4-148">Azure 提供了幾項支援驗證、並且可讓受到代管的應用程式提升可管理性的網路服務。</span><span class="sxs-lookup"><span data-stu-id="649d4-148">Azure provides several networking services that support authentication, and improve manageability of your hosted applications.</span></span> <span data-ttu-id="649d4-149">這些服務包括：</span><span class="sxs-lookup"><span data-stu-id="649d4-149">These services include the following:</span></span>

* <span data-ttu-id="649d4-150">Azure 虛擬網路可讓您在 Azure 中佈建及管理虛擬私人網路 (VPN)，並使用內部部署 IT 基礎結構安全地連結這些網路。</span><span class="sxs-lookup"><span data-stu-id="649d4-150">Azure Virtual Network lets you provision and manage virtual private networks (VPNs) in Azure as well as securely link these with on-premises IT infrastructure.</span></span>
* <span data-ttu-id="649d4-151">虛擬網路流量管理員可讓您對多個代管 Azure 服務間的傳入流量進行負載平衡，無論這些服務是在相同的資料中心內執行，還是在世界各地不同的資料中心間執行。</span><span class="sxs-lookup"><span data-stu-id="649d4-151">Virtual Network Traffic Manager allows you to load balance incoming traffic across multiple hosted Azure services whether they're running in the same datacenter or across different datacenters around the world.</span></span>
* <span data-ttu-id="649d4-152">Azure Active Directory (Azure AD) 是以 REST 為基礎的新式服務，可為您的雲端應用程式提供身分識別管理和存取控制功能。</span><span class="sxs-lookup"><span data-stu-id="649d4-152">Azure Active Directory (Azure AD) is a modern, REST-based service that provides identity management and access control capabilities for your cloud applications.</span></span> <span data-ttu-id="649d4-153">使用適用於應用程式資源的 Azure AD，可讓您輕鬆地對要存取您的 Web 應用程式和服務的使用者進行驗證和授權，並可讓您在程式碼中排除驗證和授權功能的考量。</span><span class="sxs-lookup"><span data-stu-id="649d4-153">Using Azure AD for Application Resources Azure AD to provides an easy way of authenticating and authorizing users to gain access to your web applications and services while allowing the features of authentication and authorization to be factored out of your code.</span></span>
* <span data-ttu-id="649d4-154">Azure 服務匯流排可為分散式和混合式應用程式提供安全訊息和資料流程功能 (例如 Azure 代管的應用程式與內部部署應用程式和服務之間的通訊)，而無須使用複雜的防火牆和安全性基礎結構。</span><span class="sxs-lookup"><span data-stu-id="649d4-154">Azure Service Bus provides a secure messaging and data flow capability for distributed and hybrid applications, such as communication between Azure hosted applications and on-premises applications and services, without requiring complex firewall and security infrastructures.</span></span> <span data-ttu-id="649d4-155">使用適用於應用程式資源的服務匯流排轉送：公開為端點的服務可能是屬於租用戶的服務 (例如，在內部部署環境之類的系統外部受到代管的服務)，或者可能是明確針對租用戶佈建的服務 (因為敏感的租用戶特定資料會透過這些服務進行傳送)。</span><span class="sxs-lookup"><span data-stu-id="649d4-155">Using Service Bus Relay for Application Resources to The services that are exposed as endpoints may belong to the tenant (for example, hosted outside of the system, such as on-premises), or they may be services provisioned specifically for the tenant (because sensitive, tenant-specific data travels across them).</span></span>

<span data-ttu-id="649d4-156">**佈建資源**</span><span class="sxs-lookup"><span data-stu-id="649d4-156">**Provisioning Resources**</span></span>

<span data-ttu-id="649d4-157">Azure 提供許多可為應用程式佈建新租用戶的方式。</span><span class="sxs-lookup"><span data-stu-id="649d4-157">Azure provides a number of ways provision new tenants for the application.</span></span> <span data-ttu-id="649d4-158">就租用戶為數眾多的多租用戶應用程式而言，通常必須藉由啟用自助式佈建功能將此程序自動化。</span><span class="sxs-lookup"><span data-stu-id="649d4-158">For multitenant applications with a large number of tenants, it is usually necessary to automate this process by enabling self-service provisioning.</span></span>

* <span data-ttu-id="649d4-159">背景工作角色可讓您佈建及取消佈建個別的租用戶資源 (例如在新租用戶註冊或取消時)、收集用於計量的度量，以及管理特定排程之後或超出關鍵效能指標臨界值時所做的因應調整。</span><span class="sxs-lookup"><span data-stu-id="649d4-159">Worker roles allow you to provision and de-provision per tenant resources (such as when a new tenant signs-up or cancels), collect metrics for metering use, and manage scale following a certain schedule or in response to the crossing of thresholds of key performance indicators.</span></span> <span data-ttu-id="649d4-160">此角色也可用來將更新和升級推送至方案。</span><span class="sxs-lookup"><span data-stu-id="649d4-160">This same role may also be used to push out updates and upgrades to the solution.</span></span>
* <span data-ttu-id="649d4-161">Azure Blob 可用來為新租用戶佈建計算或預先初始化的儲存資源，同時提供容器層級存取原則，以保護計算服務封裝、VHD 映像和其他資源。</span><span class="sxs-lookup"><span data-stu-id="649d4-161">Azure Blobs can be used to provision compute or pre-initialized storage resources for new tenants while providing container level access policies to protect the compute service Packages, VHD images and other resources.</span></span>
* <span data-ttu-id="649d4-162">為租用戶佈建 SQL Database 資源的選項包括：</span><span class="sxs-lookup"><span data-stu-id="649d4-162">Options for provisioning SQL Database resources for a tenant include:</span></span>
  
  * <span data-ttu-id="649d4-163">指令碼中的 DDL，或在組件中內嵌為資源的 DDL</span><span class="sxs-lookup"><span data-stu-id="649d4-163">DDL in scripts or embedded as resources within assemblies</span></span>
  * <span data-ttu-id="649d4-164">以程式設計方式部署的 SQL Server 2008 R2 DAC 封裝。</span><span class="sxs-lookup"><span data-stu-id="649d4-164">SQL Server 2008 R2 DAC Packages deployed programmatically.</span></span>
  * <span data-ttu-id="649d4-165">從主要參考資料庫複製</span><span class="sxs-lookup"><span data-stu-id="649d4-165">Copying from a master reference database</span></span>
  * <span data-ttu-id="649d4-166">使用資料庫匯入和匯出功能，從檔案佈建新資料庫。</span><span class="sxs-lookup"><span data-stu-id="649d4-166">Using database Import and Export to provision new databases from a file.</span></span>

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
