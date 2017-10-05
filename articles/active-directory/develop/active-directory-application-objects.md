---
title: "Azure Active Directory 應用程式和服務主體物件 | Microsoft Docs"
description: "Azure Active Directory 中的應用程式物件和服務主體物件之間的關聯性討論"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4c75ade5f4e47ef64ccc0fe8af4b174c377dc7bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a><span data-ttu-id="e0751-103">Azure Active Directory (Azure AD) 中的應用程式和服務主體物件</span><span class="sxs-lookup"><span data-stu-id="e0751-103">Application and service principal objects in Azure Active Directory (Azure AD)</span></span>
<span data-ttu-id="e0751-104">在 Azure AD 的內容中使用「應用程式」這個詞彙時，有時會誤解其意義。</span><span class="sxs-lookup"><span data-stu-id="e0751-104">Sometimes the meaning of the term "application" can be misunderstood when used in the context of Azure AD.</span></span> <span data-ttu-id="e0751-105">本文的目的是要藉由釐清 Azure AD 應用程式整合的概念和具體層面，並舉例說明如何註冊和同意[多租用戶應用程式](active-directory-dev-glossary.md#multi-tenant-application)，提供更清楚的說明。</span><span class="sxs-lookup"><span data-stu-id="e0751-105">The goal of this article is to make it clearer, by clarifying conceptual and concrete aspects of Azure AD application integration, with an illustration of registration and consent for a [multi-tenant application](active-directory-dev-glossary.md#multi-tenant-application).</span></span>

## <a name="overview"></a><span data-ttu-id="e0751-106">概觀</span><span class="sxs-lookup"><span data-stu-id="e0751-106">Overview</span></span>
<span data-ttu-id="e0751-107">已與 Azure AD 整合的應用程式，其含意已超出軟體層面。</span><span class="sxs-lookup"><span data-stu-id="e0751-107">An application that has been integrated with Azure AD has implications that go beyond the software aspect.</span></span> <span data-ttu-id="e0751-108">「應用程式」經常當作概念詞彙，不僅指應用程式軟體，在執行階段的驗證/授權「對話」中，也是指其 Azure AD 註冊和角色。</span><span class="sxs-lookup"><span data-stu-id="e0751-108">"Application" is frequently used as a conceptual term, referring to not only the the application software, but also its Azure AD registration and role in authentication/authorization "conversations" at runtime.</span></span> <span data-ttu-id="e0751-109">根據定義，應用程式的運作身分可以是[用戶端](active-directory-dev-glossary.md#client-application)角色 (取用資源)、[資源伺服器](active-directory-dev-glossary.md#resource-server)角色 (對用戶端公開 API)，或甚至身兼兩者。</span><span class="sxs-lookup"><span data-stu-id="e0751-109">By definition, an application can function in a [client](active-directory-dev-glossary.md#client-application) role (consuming a resource), a [resource server](active-directory-dev-glossary.md#resource-server) role (exposing APIs to clients), or even both.</span></span> <span data-ttu-id="e0751-110">對話通訊協定是由 [OAuth 2.0 授權授與流程](active-directory-dev-glossary.md#authorization-grant)所定義，可讓用戶端/資源各自存取/保護資源的資料。</span><span class="sxs-lookup"><span data-stu-id="e0751-110">The conversation protocol is defined by an [OAuth 2.0 Authorization Grant flow](active-directory-dev-glossary.md#authorization-grant), allowing the client/resource to access/protect a resource's data respectively.</span></span> <span data-ttu-id="e0751-111">現在讓我們再深入一點，看看 Azure AD 應用程式模型在設計階段和執行階段是如何代表應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0751-111">Now let's go a level deeper, and see how the Azure AD application model represents an application at design-time and run-time.</span></span> 

## <a name="application-registration"></a><span data-ttu-id="e0751-112">應用程式註冊</span><span class="sxs-lookup"><span data-stu-id="e0751-112">Application registration</span></span>
<span data-ttu-id="e0751-113">當您在 [Azure 入口網站][AZURE-Portal]註冊 Azure AD 應用程式時，Azure AD 租用戶中會建立兩個物件︰應用程式物件和服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="e0751-113">When you register an Azure AD application in the [Azure portal][AZURE-Portal], two objects are created in your Azure AD tenant: an application object, and a service principal object.</span></span>

#### <a name="application-object"></a><span data-ttu-id="e0751-114">應用程式物件</span><span class="sxs-lookup"><span data-stu-id="e0751-114">Application object</span></span>
<span data-ttu-id="e0751-115">Azure AD 應用程式是由其唯一一個應用程式物件所定義，該物件位於應用程式註冊所在的 Azure AD 租用戶，也稱為應用程式的「主要」租用戶。</span><span class="sxs-lookup"><span data-stu-id="e0751-115">An Azure AD application is defined by its one and only application object, which resides in the Azure AD tenant where the application was registered, known as the application's "home" tenant.</span></span> <span data-ttu-id="e0751-116">Azure AD Graph [Application 實體][AAD-Graph-App-Entity]會定義應用程式物件屬性的結構描述。</span><span class="sxs-lookup"><span data-stu-id="e0751-116">The Azure AD Graph [Application entity][AAD-Graph-App-Entity] defines the schema for an application object's properties.</span></span> 

#### <a name="service-principal-object"></a><span data-ttu-id="e0751-117">服務主體物件</span><span class="sxs-lookup"><span data-stu-id="e0751-117">Service principal object</span></span>
<span data-ttu-id="e0751-118">服務主體物件會定義在特定租用戶中使用應用程式時的原則和權限，為安全性主體提供在執行階段代表應用程式的基礎。</span><span class="sxs-lookup"><span data-stu-id="e0751-118">The service principal object defines the policy and permissions for an application's use in a specific tenant, providing the basis for a security principal to represent the application at run-time.</span></span> <span data-ttu-id="e0751-119">Azure AD Graph [ServicePrincipal 實體][AAD-Graph-Sp-Entity]會定義服務主體物件屬性的結構描述。</span><span class="sxs-lookup"><span data-stu-id="e0751-119">The Azure AD Graph [ServicePrincipal entity][AAD-Graph-Sp-Entity] defines the schema for a service principal object's properties.</span></span> 

#### <a name="application-and-service-principal-relationship"></a><span data-ttu-id="e0751-120">應用程式和服務主體關聯性</span><span class="sxs-lookup"><span data-stu-id="e0751-120">Application and service principal relationship</span></span>
<span data-ttu-id="e0751-121">將應用程式物件視為應用程式的「全域」代表 (用於所有租用戶)，而將服務主體看做是「本機」代表 (用於特定租用戶)。</span><span class="sxs-lookup"><span data-stu-id="e0751-121">Consider the application object as the *global* representation of your application for use across all tenants, and the service principal as the *local* representation for use in a specific tenant.</span></span> <span data-ttu-id="e0751-122">應用程式物件就像範本，可從中「衍生」通用和預設屬性，用以建立相對應的服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="e0751-122">The application object serves as the template from which common and default properties are *derived* for use in creating corresponding service principal objects.</span></span> <span data-ttu-id="e0751-123">因此，應用程式物件與軟體應用程式之間存在 1:1 關聯性，而與其對應的服務主體物件之間存在一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="e0751-123">An application object therefore has a 1:1 relationship with the software application, and a 1:many relationship with its corresponding service principal object(s).</span></span>

<span data-ttu-id="e0751-124">每一個會用到應用程式的租用戶中必須建立服務主體，才能讓它建立身分識別來登入及/或存取租用戶所保護的資源。</span><span class="sxs-lookup"><span data-stu-id="e0751-124">A service principal must be created in each tenant where the application will be used, enabling it to establish an identity for sign-in and/or access to resources being secured by the tenant.</span></span> <span data-ttu-id="e0751-125">單一租用戶的應用程式只能有一個服務主體 (在其主租用戶中)，通常是在應用程式註冊期間建立和同意使用。</span><span class="sxs-lookup"><span data-stu-id="e0751-125">A single-tenant application will have only one service principal (in its home tenant), usually created and consented for use during application registration.</span></span> <span data-ttu-id="e0751-126">如果是多租用戶 Web 應用程式/API，則在使用者已同意使用它的每個租用戶中，還會建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="e0751-126">A multi-tenant Web application/API will also have a service principal created in each tenant where a user from that tenant has consented to its use.</span></span>  

> [!NOTE]
> <span data-ttu-id="e0751-127">您對應用程式物件所做的任何變更也只會反映於它在應用程式的主要租用戶 (其註冊所在租用戶) 中的服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="e0751-127">Any changes you make to your application object, are also reflected in its service principal object in the application's home tenant only (the tenant where it was registered).</span></span> <span data-ttu-id="e0751-128">就多租用戶應用程式而言，對應用程式物件所做的變更，必須等到透過[應用程式存取面板](https://myapps.microsoft.com)移除存取權再重新授權之後，才會反映在任何取用者租用戶的服務主體物件中。</span><span class="sxs-lookup"><span data-stu-id="e0751-128">For multi-tenant applications, changes to the application object are not reflected in any consumer tenants' service principal objects, until the access is removed via the [Application Access Panel](https://myapps.microsoft.com) and granted again.</span></span>
><br>  
> <span data-ttu-id="e0751-129">也請注意，依預設，原生應用程式會註冊為多租用戶。</span><span class="sxs-lookup"><span data-stu-id="e0751-129">Also note that native applications are registered as multi-tenant by default.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="e0751-130">範例</span><span class="sxs-lookup"><span data-stu-id="e0751-130">Example</span></span>
<span data-ttu-id="e0751-131">下圖說明應用程式的應用程式物件與對應的服務主體物件之間的關係，是以一個稱為「HR 應用程式」 的範例多租用戶應用程式為背景。</span><span class="sxs-lookup"><span data-stu-id="e0751-131">The following diagram illustrates the relationship between an application's application object and corresponding service principal objects, in the context of a sample multi-tenant application called **HR app**.</span></span> <span data-ttu-id="e0751-132">此案例中有三個 Azure AD 租用戶︰</span><span class="sxs-lookup"><span data-stu-id="e0751-132">There are three Azure AD tenants in this scenario:</span></span> 

* <span data-ttu-id="e0751-133">**Adatum** - 開發 **HR 應用程式**之公司所使用的租用戶</span><span class="sxs-lookup"><span data-stu-id="e0751-133">**Adatum** - the tenant used by the company that developed the **HR app**</span></span>
* <span data-ttu-id="e0751-134">**Contoso** - Contoso 組織所使用的租用戶，其為 **HR 應用程式**的取用者</span><span class="sxs-lookup"><span data-stu-id="e0751-134">**Contoso** - the tenant used by the Contoso organization, which is a consumer of the **HR app**</span></span>
* <span data-ttu-id="e0751-135">**Fabrikam** - Fabrikam 組織所使用的租用戶，其亦會取用 **HR 應用程式**</span><span class="sxs-lookup"><span data-stu-id="e0751-135">**Fabrikam** - the tenant used by the Fabrikam organization, which also consumes the **HR app**</span></span>

![應用程式物件和服務主體物件之間的關聯性](./media/active-directory-application-objects/application-objects-relationship.png)

<span data-ttu-id="e0751-137">在前一張圖中，步驟 1 是在應用程式的主要租用戶中建立應用程式和服務主體物件的程序。</span><span class="sxs-lookup"><span data-stu-id="e0751-137">In the previous diagram, Step 1 is the process of creating the application and service principal objects in the application's home tenant.</span></span>

<span data-ttu-id="e0751-138">在步驟 2 中，當 Contoso 和 Fabrikam 的系統管理員完成同意，系統就會在其公司的 Azure AD 租用戶中建立服務主體物件，並指派系統管理員所授與的權限。</span><span class="sxs-lookup"><span data-stu-id="e0751-138">In Step 2, when Contoso and Fabrikam administrators complete consent, a service principal object is created in their company's Azure AD tenant and assigned the permissions that the administrator granted.</span></span> <span data-ttu-id="e0751-139">也請注意，HR 應用程式可能會設定/設計為允許由使用者同意以進行個人使用。</span><span class="sxs-lookup"><span data-stu-id="e0751-139">Also note that the HR app could be configured/designed to allow consent by users for individual use.</span></span>

<span data-ttu-id="e0751-140">在步驟 3 中，HR 應用程式的取用者租用戶 (Contoso 和 Fabrikam) 都分別擁有自己的服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="e0751-140">In Step 3, the consumer tenants of the HR application (Contoso and Fabrikam) each have their own service principal object.</span></span> <span data-ttu-id="e0751-141">每個均代表他們在執行階段的應用程式執行個體使用，其中皆受到個別系統管理員所同意的權限控管。</span><span class="sxs-lookup"><span data-stu-id="e0751-141">Each represents their use of an instance of the application at runtime, governed by the permissions consented by the respective administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0751-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0751-142">Next steps</span></span>
<span data-ttu-id="e0751-143">若要存取應用程式的應用程式物件，可以透過 Azure AD Graph API、[Azure 入口網站][AZURE-Portal]的應用程式資訊清單編輯器，或 [Azure AD PowerShell Cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0) 來存取 (如其 OData 的 [Application 實體][AAD-Graph-App-Entity]所代表)。</span><span class="sxs-lookup"><span data-stu-id="e0751-143">An application's application object can be accessed via the Azure AD Graph API, the [Azure portal's][AZURE-Portal] application manifest editor, or [Azure AD PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), as represented by its OData [Application entity][AAD-Graph-App-Entity].</span></span>

<span data-ttu-id="e0751-144">若要存取應用程式的服務主體物件，可以透過 Azure AD Graph API 或 [Azure AD PowerShell Cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0) 來存取 (如其 OData 的 [ServicePrincipal][AAD-Graph-Sp-Entity] 實體所代表)。</span><span class="sxs-lookup"><span data-stu-id="e0751-144">An application's service principal object can be accessed via the Azure AD Graph API or [Azure AD PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), as represented by its OData [ServicePrincipal entity][AAD-Graph-Sp-Entity].</span></span>

<span data-ttu-id="e0751-145">[Azure AD Graph 總管](https://graphexplorer.azurewebsites.net/)可用於查詢應用程式和服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="e0751-145">The [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) is useful for querying both the application and service principal objects.</span></span>

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
