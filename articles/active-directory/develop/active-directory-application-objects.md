---
title: "aaaAzure Active Directory 應用程式和服務主體物件 |Microsoft 文件"
description: "討論的 hello 應用程式與 Azure Active Directory 中的服務主體物件之間的關聯性"
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
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a><span data-ttu-id="97a0c-103">Azure Active Directory (Azure AD) 中的應用程式和服務主體物件</span><span class="sxs-lookup"><span data-stu-id="97a0c-103">Application and service principal objects in Azure Active Directory (Azure AD)</span></span>
<span data-ttu-id="97a0c-104">有時 hello hello 詞彙用於 Azure AD 的 hello 內容時，可以造成誤解 「 應用程式 」 的意義。</span><span class="sxs-lookup"><span data-stu-id="97a0c-104">Sometimes hello meaning of hello term "application" can be misunderstood when used in hello context of Azure AD.</span></span> <span data-ttu-id="97a0c-105">這篇文章的 hello 目標是 toomake 更清楚，釐清概念和具體方面的 Azure AD 的應用程式整合的說明，註冊以及同意，以便與它[多租用戶應用程式](active-directory-dev-glossary.md#multi-tenant-application)。</span><span class="sxs-lookup"><span data-stu-id="97a0c-105">hello goal of this article is toomake it clearer, by clarifying conceptual and concrete aspects of Azure AD application integration, with an illustration of registration and consent for a [multi-tenant application](active-directory-dev-glossary.md#multi-tenant-application).</span></span>

## <a name="overview"></a><span data-ttu-id="97a0c-106">概觀</span><span class="sxs-lookup"><span data-stu-id="97a0c-106">Overview</span></span>
<span data-ttu-id="97a0c-107">已與 Azure AD 整合的應用程式具有超越 hello 軟體方面的影響。</span><span class="sxs-lookup"><span data-stu-id="97a0c-107">An application that has been integrated with Azure AD has implications that go beyond hello software aspect.</span></span> <span data-ttu-id="97a0c-108">「 應用程式 」 通常做為概念的詞彙，參考 toonot 只有 hello hello 應用程式軟體，但也其 Azure AD 註冊和驗證/授權 「 交談 」，在執行階段中的角色。</span><span class="sxs-lookup"><span data-stu-id="97a0c-108">"Application" is frequently used as a conceptual term, referring toonot only hello hello application software, but also its Azure AD registration and role in authentication/authorization "conversations" at runtime.</span></span> <span data-ttu-id="97a0c-109">根據定義，應用程式可以扮演[用戶端](active-directory-dev-glossary.md#client-application)（耗用資源），角色[資源伺服器](active-directory-dev-glossary.md#resource-server)角色 (公開 Api tooclients)，或甚至兩個。</span><span class="sxs-lookup"><span data-stu-id="97a0c-109">By definition, an application can function in a [client](active-directory-dev-glossary.md#client-application) role (consuming a resource), a [resource server](active-directory-dev-glossary.md#resource-server) role (exposing APIs tooclients), or even both.</span></span> <span data-ttu-id="97a0c-110">hello 對話通訊協定由定義[OAuth 2.0 授權授與流程](active-directory-dev-glossary.md#authorization-grant)，允許 hello 用戶端/資源 tooaccess/保護資源的資料分別。</span><span class="sxs-lookup"><span data-stu-id="97a0c-110">hello conversation protocol is defined by an [OAuth 2.0 Authorization Grant flow](active-directory-dev-glossary.md#authorization-grant), allowing hello client/resource tooaccess/protect a resource's data respectively.</span></span> <span data-ttu-id="97a0c-111">現在讓我們繼續更深度的層級，並請參閱如何 hello Azure AD 應用程式模型代表應用程式在設計階段和執行階段。</span><span class="sxs-lookup"><span data-stu-id="97a0c-111">Now let's go a level deeper, and see how hello Azure AD application model represents an application at design-time and run-time.</span></span> 

## <a name="application-registration"></a><span data-ttu-id="97a0c-112">應用程式註冊</span><span class="sxs-lookup"><span data-stu-id="97a0c-112">Application registration</span></span>
<span data-ttu-id="97a0c-113">當您註冊 Azure AD 應用程式在 hello [Azure 入口網站][AZURE-Portal]，Azure AD 租用戶中建立兩個物件： 應用程式物件與服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="97a0c-113">When you register an Azure AD application in hello [Azure portal][AZURE-Portal], two objects are created in your Azure AD tenant: an application object, and a service principal object.</span></span>

#### <a name="application-object"></a><span data-ttu-id="97a0c-114">應用程式物件</span><span class="sxs-lookup"><span data-stu-id="97a0c-114">Application object</span></span>
<span data-ttu-id="97a0c-115">Azure AD 應用程式是由定義它的一個，只有應用程式物件，該物件位於 hello 應用程式註冊所在的 hello Azure AD 租用戶中，稱為 hello 應用程式"home"租用戶。</span><span class="sxs-lookup"><span data-stu-id="97a0c-115">An Azure AD application is defined by its one and only application object, which resides in hello Azure AD tenant where hello application was registered, known as hello application's "home" tenant.</span></span> <span data-ttu-id="97a0c-116">hello Azure AD Graph[應用程式的實體][ AAD-Graph-App-Entity]定義 hello 應用程式物件的屬性結構描述。</span><span class="sxs-lookup"><span data-stu-id="97a0c-116">hello Azure AD Graph [Application entity][AAD-Graph-App-Entity] defines hello schema for an application object's properties.</span></span> 

#### <a name="service-principal-object"></a><span data-ttu-id="97a0c-117">服務主體物件</span><span class="sxs-lookup"><span data-stu-id="97a0c-117">Service principal object</span></span>
<span data-ttu-id="97a0c-118">hello 服務主體物件定義特定租用戶，提供 hello 基礎安全性主體 toorepresent hello 應用程式在執行階段中的 hello 原則和應用程式所使用的使用權限。</span><span class="sxs-lookup"><span data-stu-id="97a0c-118">hello service principal object defines hello policy and permissions for an application's use in a specific tenant, providing hello basis for a security principal toorepresent hello application at run-time.</span></span> <span data-ttu-id="97a0c-119">hello Azure AD Graph [ServicePrincipal 實體][ AAD-Graph-Sp-Entity] hello 為定義結構描述的服務主體物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="97a0c-119">hello Azure AD Graph [ServicePrincipal entity][AAD-Graph-Sp-Entity] defines hello schema for a service principal object's properties.</span></span> 

#### <a name="application-and-service-principal-relationship"></a><span data-ttu-id="97a0c-120">應用程式和服務主體關聯性</span><span class="sxs-lookup"><span data-stu-id="97a0c-120">Application and service principal relationship</span></span>
<span data-ttu-id="97a0c-121">請考慮為 hello hello 應用程式物件*全域*表示您的應用程式用來跨所有租用戶和 hello 服務主體做 hello*本機*用於特定的表示法租用戶。</span><span class="sxs-lookup"><span data-stu-id="97a0c-121">Consider hello application object as hello *global* representation of your application for use across all tenants, and hello service principal as hello *local* representation for use in a specific tenant.</span></span> <span data-ttu-id="97a0c-122">hello 應用程式物件會作為 hello 從哪一個常見的範本和預設屬性是*衍生*可用來建立相對應的服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="97a0c-122">hello application object serves as hello template from which common and default properties are *derived* for use in creating corresponding service principal objects.</span></span> <span data-ttu-id="97a0c-123">1:1 關聯性與 hello 軟體應用程式，以及其對應的服務主體物件 1:many 之間的關係，因此有應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="97a0c-123">An application object therefore has a 1:1 relationship with hello software application, and a 1:many relationship with its corresponding service principal object(s).</span></span>

<span data-ttu-id="97a0c-124">必須在每個租用戶建立服務主體，其中 hello 應用程式將會使用，讓它 tooestablish 登入的身分識別及/或存取 tooresources hello 租用戶所受保護。</span><span class="sxs-lookup"><span data-stu-id="97a0c-124">A service principal must be created in each tenant where hello application will be used, enabling it tooestablish an identity for sign-in and/or access tooresources being secured by hello tenant.</span></span> <span data-ttu-id="97a0c-125">單一租用戶的應用程式只能有一個服務主體 (在其主租用戶中)，通常是在應用程式註冊期間建立和同意使用。</span><span class="sxs-lookup"><span data-stu-id="97a0c-125">A single-tenant application will have only one service principal (in its home tenant), usually created and consented for use during application registration.</span></span> <span data-ttu-id="97a0c-126">多租用戶 Web 應用程式/API 也會有每個租用戶中建立服務主體，該租用戶的使用者已經同意 tooits 使用。</span><span class="sxs-lookup"><span data-stu-id="97a0c-126">A multi-tenant Web application/API will also have a service principal created in each tenant where a user from that tenant has consented tooits use.</span></span>  

> [!NOTE]
> <span data-ttu-id="97a0c-127">Tooyour 應用程式物件，您所做的變更也會反映其 hello 應用程式的主要租用戶中只 （自從註冊 hello 租用戶） 的服務主體物件中。</span><span class="sxs-lookup"><span data-stu-id="97a0c-127">Any changes you make tooyour application object, are also reflected in its service principal object in hello application's home tenant only (hello tenant where it was registered).</span></span> <span data-ttu-id="97a0c-128">對於多租用戶應用程式，變更 toohello 應用程式物件不會反映在任何取用者租用戶的服務主體物件，必須先移除 hello 存取透過 hello[應用程式存取面板](https://myapps.microsoft.com)和授與一次。</span><span class="sxs-lookup"><span data-stu-id="97a0c-128">For multi-tenant applications, changes toohello application object are not reflected in any consumer tenants' service principal objects, until hello access is removed via hello [Application Access Panel](https://myapps.microsoft.com) and granted again.</span></span>
><br>  
> <span data-ttu-id="97a0c-129">也請注意，依預設，原生應用程式會註冊為多租用戶。</span><span class="sxs-lookup"><span data-stu-id="97a0c-129">Also note that native applications are registered as multi-tenant by default.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="97a0c-130">範例</span><span class="sxs-lookup"><span data-stu-id="97a0c-130">Example</span></span>
<span data-ttu-id="97a0c-131">hello 下列圖表說明 hello 應用程式的應用程式物件和相對應主體物件，在 hello 範例多租用戶應用程式的內容中呼叫的服務之間的關聯性**HR app**。</span><span class="sxs-lookup"><span data-stu-id="97a0c-131">hello following diagram illustrates hello relationship between an application's application object and corresponding service principal objects, in hello context of a sample multi-tenant application called **HR app**.</span></span> <span data-ttu-id="97a0c-132">此案例中有三個 Azure AD 租用戶︰</span><span class="sxs-lookup"><span data-stu-id="97a0c-132">There are three Azure AD tenants in this scenario:</span></span> 

* <span data-ttu-id="97a0c-133">**Adatum** -hello 開發 hello hello 公司所使用的租用戶**HR 應用程式**</span><span class="sxs-lookup"><span data-stu-id="97a0c-133">**Adatum** - hello tenant used by hello company that developed hello **HR app**</span></span>
* <span data-ttu-id="97a0c-134">**Contoso** -hello hello Contoso 組織是 hello 取用者所使用的租用戶**HR 應用程式**</span><span class="sxs-lookup"><span data-stu-id="97a0c-134">**Contoso** - hello tenant used by hello Contoso organization, which is a consumer of hello **HR app**</span></span>
* <span data-ttu-id="97a0c-135">**Fabrikam** -hello hello Fabrikam 組織，也會耗用 hello 所使用的租用戶**HR 應用程式**</span><span class="sxs-lookup"><span data-stu-id="97a0c-135">**Fabrikam** - hello tenant used by hello Fabrikam organization, which also consumes hello **HR app**</span></span>

![應用程式物件和服務主體物件之間的關聯性](./media/active-directory-application-objects/application-objects-relationship.png)

<span data-ttu-id="97a0c-137">Hello 上圖中，在步驟 1 是 hello 程序建立 hello 應用程式的主要租用戶中的 hello 應用程式和服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="97a0c-137">In hello previous diagram, Step 1 is hello process of creating hello application and service principal objects in hello application's home tenant.</span></span>

<span data-ttu-id="97a0c-138">在步驟 2 中，Contoso 和 Fabrikam 的系統管理員同意時，完成的服務主體物件會建立在其公司的 Azure AD 租用戶和指派的 hello 權限授與該 hello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="97a0c-138">In Step 2, when Contoso and Fabrikam administrators complete consent, a service principal object is created in their company's Azure AD tenant and assigned hello permissions that hello administrator granted.</span></span> <span data-ttu-id="97a0c-139">也請注意該 hello HR 應用程式可能是供個人使用的使用者設定/設計 tooallow 同意。</span><span class="sxs-lookup"><span data-stu-id="97a0c-139">Also note that hello HR app could be configured/designed tooallow consent by users for individual use.</span></span>

<span data-ttu-id="97a0c-140">步驟 3 中，取用者租用戶 hello hello HR 應用程式 （Contoso 和 Fabrikam） 每個有自己的服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="97a0c-140">In Step 3, hello consumer tenants of hello HR application (Contoso and Fabrikam) each have their own service principal object.</span></span> <span data-ttu-id="97a0c-141">每一個代表執行個體在執行階段，由 hello 各自的系統管理員權限同意的 hello hello 應用程式的用法。</span><span class="sxs-lookup"><span data-stu-id="97a0c-141">Each represents their use of an instance of hello application at runtime, governed by hello permissions consented by hello respective administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97a0c-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97a0c-142">Next steps</span></span>
<span data-ttu-id="97a0c-143">應用程式的應用程式物件可以透過 Azure AD Graph API hello hello [Azure 入口網站][ AZURE-Portal]應用程式資訊清單編輯器] 中，或[Azure AD PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0)，表示其 OData 的[應用程式的實體][AAD-Graph-App-Entity]。</span><span class="sxs-lookup"><span data-stu-id="97a0c-143">An application's application object can be accessed via hello Azure AD Graph API, hello [Azure portal's][AZURE-Portal] application manifest editor, or [Azure AD PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), as represented by its OData [Application entity][AAD-Graph-App-Entity].</span></span>

<span data-ttu-id="97a0c-144">應用程式的服務主體物件可以透過 hello Azure AD Graph API 或[Azure AD PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0)，表示其 OData 的[ServicePrincipal 實體][ AAD-Graph-Sp-Entity].</span><span class="sxs-lookup"><span data-stu-id="97a0c-144">An application's service principal object can be accessed via hello Azure AD Graph API or [Azure AD PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), as represented by its OData [ServicePrincipal entity][AAD-Graph-Sp-Entity].</span></span>

<span data-ttu-id="97a0c-145">hello [Azure AD Graph 總管](https://graphexplorer.azurewebsites.net/)可用於查詢 hello 應用程式和服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="97a0c-145">hello [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) is useful for querying both hello application and service principal objects.</span></span>

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
