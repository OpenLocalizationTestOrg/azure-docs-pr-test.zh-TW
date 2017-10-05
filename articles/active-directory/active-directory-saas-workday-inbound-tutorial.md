---
title: "教學課程︰以內部部署 Active Directory 和 Azure Active Directory 設定自動化使用者佈建的 Workday | Microsoft Docs"
description: "了解如何使用 Workday 做為 Active Directory 和 Azure Active Directory 身分識別資料的來源。"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: f9cc94ca1fc44d10af19debab49435b265bf6e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a><span data-ttu-id="7b081-103">教學課程︰以內部部署 Active Directory 和 Azure Active Directory 設定自動化使用者佈建的 Workday</span><span class="sxs-lookup"><span data-stu-id="7b081-103">Tutorial: Configure Workday for automatic user provisioning with on-premises Active Directory and Azure Active Directory</span></span>
<span data-ttu-id="7b081-104">本教學課程的目標是說明將人員從 Workday 匯入 Active Directory 和 Azure Active Directory，以及將某些屬性選擇性回寫至 Workday 需要執行的步驟。</span><span class="sxs-lookup"><span data-stu-id="7b081-104">The objective of this tutorial is to show you the steps you need to perform to import people from Workday into both Active Directory and Azure Active Directory, with optional writeback of some attributes to Workday.</span></span> 



## <a name="overview"></a><span data-ttu-id="7b081-105">概觀</span><span class="sxs-lookup"><span data-stu-id="7b081-105">Overview</span></span>

<span data-ttu-id="7b081-106">[Azure Active Directory 使用者佈建服務](active-directory-saas-app-provisioning.md)與 [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) 整合以佈建使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b081-106">The [Azure Active Directory user provisioning service](active-directory-saas-app-provisioning.md) integrates with the [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in order to provision user accounts.</span></span> <span data-ttu-id="7b081-107">Azure AD 使用此連接啟用下列使用者佈建工作流程：</span><span class="sxs-lookup"><span data-stu-id="7b081-107">Azure AD uses this connection to enable the following user provisioning workflows:</span></span>

* <span data-ttu-id="7b081-108">**將使用者佈建至 Active Directory** - 將選取的使用者集合從 Workday 同步至一或多個 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="7b081-108">**Provisioning users to Active Directory** - Synchronize selected sets of users from Workday into one or more Active Directory forests.</span></span> 

* <span data-ttu-id="7b081-109">**將僅限雲端使用者佈建至 Azure Active Directory** - 可以使用 [AAD Connect](connect/active-directory-aadconnect.md)，將存在於 Active Directory 和 Azure Active Directory 的混合式使用者佈建至後者。</span><span class="sxs-lookup"><span data-stu-id="7b081-109">**Provisioning cloud-only users to Azure Active Directory** - Hybrid users who exist in both Active Directory and Azure Active Directory can be provisioned into the latter using [AAD Connect](connect/active-directory-aadconnect.md).</span></span> <span data-ttu-id="7b081-110">不過，可以使用 Azure AD 使用者佈建服務，將僅限雲端使用者從 Workday 直接佈建至 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="7b081-110">However, users that are cloud-only can be provisioned directly from Workday to Azure Active Directory using the Azure AD user provisioning service.</span></span>

* <span data-ttu-id="7b081-111">**將電子郵件地址回寫至 Workday** - Azure AD 使用者佈建服務可以將選取的 Azure AD 使用者屬性回寫至 Workday，例如電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7b081-111">**Writeback of email addresses to Workday** - the Azure AD user provisioning service can write selected Azure AD user attributes back to Workday, such as the email address.</span></span>

### <a name="scenarios-covered"></a><span data-ttu-id="7b081-112">涵蓋的案例</span><span class="sxs-lookup"><span data-stu-id="7b081-112">Scenarios covered</span></span>

<span data-ttu-id="7b081-113">Azure AD 使用者佈建服務支援的 Workday 使用者佈建工作流程，可啟用下列人力資源和身分識別生命週期管理案例的自動化：</span><span class="sxs-lookup"><span data-stu-id="7b081-113">The Workday user provisioning workflows supported by the Azure AD user provisioning service enables automation of the following human resources and identity lifecycle management scenarios:</span></span>

* <span data-ttu-id="7b081-114">**雇用新員工** - 將新員工新增至 Workday 時，系統會在 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)中自動建立使用者帳戶，並將電子郵件地址回寫至 Workday。</span><span class="sxs-lookup"><span data-stu-id="7b081-114">**Hiring new employees** - When a new employee is added to Workday, a user account will be automatically created in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md), with write back of the email address to Workday.</span></span>

* <span data-ttu-id="7b081-115">**員工屬性和設定檔更新** - 在 Workday 中更新員工記錄時 (例如姓名、職稱或經理)，系統會在 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)中自動更新其使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b081-115">**Employee attribute and profile updates** - When an employee record is updated in Workday (such as their name, title, or manager), their user account will be automatically updated in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="7b081-116">**員工離職** - 在 Workday 中將員工設定為離職時，系統會在 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)中自動停用其使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b081-116">**Employee terminations** - When an employee is terminated in Workday, their user account is automatically disabled in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="7b081-117">**重新雇用員工** - 在 Workday 中重新雇用員工時，系統會自動重新啟用其舊帳戶或將其重新佈建 (取決於您的喜好設定) 至 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="7b081-117">**Employee re-hires** - When an employee is rehired in Workday, their old account can be automatically reactivated or re-provisioned (depending on your preference) to Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>


## <a name="planning-your-solution"></a><span data-ttu-id="7b081-118">規劃您的解決方案</span><span class="sxs-lookup"><span data-stu-id="7b081-118">Planning your solution</span></span>

<span data-ttu-id="7b081-119">開始進行 Workday 整合之前，請檢查下列必要條件，並閱讀下列有關如何讓目前的 Active Directory 結構和使用者佈建需求與 Azure Active Directory 提供解決方案相符的指導。</span><span class="sxs-lookup"><span data-stu-id="7b081-119">Before beginning your Workday integration, check the prerequisites below and read the following guidance on how to match your current Active Directory architecture and user provisioning requirements with the solution(s) provided by Azure Active Directory.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7b081-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b081-120">Prerequisites</span></span>

<span data-ttu-id="7b081-121">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="7b081-121">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="7b081-122">具有全域系統管理員存取權的有效 Azure AD Premium P1 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7b081-122">A valid Azure AD Premium P1 subscription with global administrator access</span></span>
* <span data-ttu-id="7b081-123">可供測試和整合之用的 Workday 實作租用戶</span><span class="sxs-lookup"><span data-stu-id="7b081-123">A Workday implementation tenant for testing and integration purposes</span></span>
* <span data-ttu-id="7b081-124">可供測試之用的 Workday 系統管理員權限，以建立系統整合使用者和進行變更以測試員工資料</span><span class="sxs-lookup"><span data-stu-id="7b081-124">Administrator permissions in Workday to create a system integration user, and make changes to test employee data for testing purposes</span></span>
* <span data-ttu-id="7b081-125">佈建至 Active Directory 的使用者，需要執行 Windows Service 2012 或更新版本的已加入網域伺服器，才能裝載[內部部署同步代理程式](https://go.microsoft.com/fwlink/?linkid=847801)</span><span class="sxs-lookup"><span data-stu-id="7b081-125">For user provisioning to Active Directory, a domain-joined server running Windows Service 2012 or greater is required to host the [on-premises synchronization agent](https://go.microsoft.com/fwlink/?linkid=847801)</span></span>
* <span data-ttu-id="7b081-126">可在 Active Directory 與 Azure AD 之間同步處理的 [Azure AD Connect](connect/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="7b081-126">[Azure AD Connect](connect/active-directory-aadconnect.md) for synchronizing between Active Directory and Azure AD</span></span>

> [!NOTE]
> <span data-ttu-id="7b081-127">如果您的 Azure AD 租用戶位於歐洲，請參閱下列[已知問題](#known-issues)一節。</span><span class="sxs-lookup"><span data-stu-id="7b081-127">If your Azure AD tenant is located in Europe, please see the [Known issues](#known-issues) section below.</span></span>


### <a name="solution-architecture"></a><span data-ttu-id="7b081-128">方案架構</span><span class="sxs-lookup"><span data-stu-id="7b081-128">Solution architecture</span></span>

<span data-ttu-id="7b081-129">Azure AD 提供一組豐富的佈建連接器，協助您解決從 Workday 到 Active Directory、Azure AD、SaaS 應用程式等產品的佈建和身分識別生命週期管理。</span><span class="sxs-lookup"><span data-stu-id="7b081-129">Azure AD provides a rich set of provisioning connectors to help you solve provisioning and identity lifecycle management from Workday to Active Directory, Azure AD, SaaS apps, and beyond.</span></span> <span data-ttu-id="7b081-130">您將使用的功能和設定解決方案的方法將會視組織環境和需求而有所不同。</span><span class="sxs-lookup"><span data-stu-id="7b081-130">Which features you will use and how you set up the solution will vary depending on your organization's environment and requirements.</span></span> <span data-ttu-id="7b081-131">您的第一步便是評估組織中存在且已部署下列項目的數量：</span><span class="sxs-lookup"><span data-stu-id="7b081-131">As a first step, take stock of how many of the following are present and deployed in your organization:</span></span>

* <span data-ttu-id="7b081-132">您正在使用多少 Active Directory 樹系？</span><span class="sxs-lookup"><span data-stu-id="7b081-132">How many Active Directory Forests are in use?</span></span>
* <span data-ttu-id="7b081-133">您正在使用多少 Active Directory 網域？</span><span class="sxs-lookup"><span data-stu-id="7b081-133">How many Active Directory Domains are in use?</span></span>
* <span data-ttu-id="7b081-134">有多少 Active Directory 組織單位 (OU) 正在使用？</span><span class="sxs-lookup"><span data-stu-id="7b081-134">How many Active Directory Organizational Units (OUs) are in use?</span></span>
* <span data-ttu-id="7b081-135">有多少 Azure Active Directory 租用戶正在使用？</span><span class="sxs-lookup"><span data-stu-id="7b081-135">How many Azure Active Directory tenants are in use?</span></span>
* <span data-ttu-id="7b081-136">是否需要將任何使用者佈建至 Active Directory 和 Azure Active Directory (例如「混合式」使用者)？</span><span class="sxs-lookup"><span data-stu-id="7b081-136">Are there users who need to be provisioned to both Active Directory and Azure Active Directory (e.g. "hybrid" users)?</span></span>
* <span data-ttu-id="7b081-137">是否需要將任何使用者佈建至 Azure Active Directory，但不需要將其佈建至 Active Directory (例如「僅限雲端」使用者)？</span><span class="sxs-lookup"><span data-stu-id="7b081-137">Are there users who need to be provisioned to Azure Active Directory, but not Active Directory (e.g. "cloud-only" users)?</span></span>
* <span data-ttu-id="7b081-138">是否需要將使用者電子郵件地址寫回至 Workday？</span><span class="sxs-lookup"><span data-stu-id="7b081-138">Do user email addresses need to be written back to Workday?</span></span>

<span data-ttu-id="7b081-139">找到這些問題的答案之後，您便可以依照下列指導來計劃 Workday 佈建部署。</span><span class="sxs-lookup"><span data-stu-id="7b081-139">Once you have answers to these questions, you can plan your Workday provisioning deployment by following the guidance below.</span></span>

#### <a name="using-provisioning-connector-apps"></a><span data-ttu-id="7b081-140">使用佈建連接器應用程式</span><span class="sxs-lookup"><span data-stu-id="7b081-140">Using provisioning connector apps</span></span>

<span data-ttu-id="7b081-141">Azure Active Directory 支援適用於 Workday 和大量其他 SaaS 應用程式的預先整合佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="7b081-141">Azure Active Directory supports pre-integrated provisioning connectors for Workday and a large number of other SaaS applications.</span></span> 

<span data-ttu-id="7b081-142">其為具有單一來源系統 API 的單一佈建連接器介面，且有助於將資料佈建至單一目標系統。</span><span class="sxs-lookup"><span data-stu-id="7b081-142">A single provisioning connector interfaces with the API of a single source system, and helps provision data to a single target system.</span></span> <span data-ttu-id="7b081-143">Azure AD 支援的大部分佈建連接器都適用於單一來源和目標系統 (例如 Azure AD 至 ServiceNow)，且只要從 Azure AD 應用程式庫新增上述應用程式即可輕鬆設定 (例如 ServiceNow)。</span><span class="sxs-lookup"><span data-stu-id="7b081-143">Most provisioning connectors that Azure AD supports are for a single source and target system (e.g. Azure AD to ServiceNow), and can be setup by simply adding the app in question from the Azure AD app gallery (e.g. ServiceNow).</span></span> 

<span data-ttu-id="7b081-144">在 Azure AD 中佈建連接器執行個體與應用程式執行個體之間具有一對一關聯性：</span><span class="sxs-lookup"><span data-stu-id="7b081-144">There is a one-to-one relationship between provisioning connector instances and app instances in Azure AD:</span></span>

| <span data-ttu-id="7b081-145">來源系統</span><span class="sxs-lookup"><span data-stu-id="7b081-145">Source System</span></span> | <span data-ttu-id="7b081-146">目標系統</span><span class="sxs-lookup"><span data-stu-id="7b081-146">Target System</span></span> |
| ---------- | ---------- | 
| <span data-ttu-id="7b081-147">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="7b081-147">Azure AD tenant</span></span> | <span data-ttu-id="7b081-148">SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b081-148">SaaS application</span></span> |


<span data-ttu-id="7b081-149">不過，將 Workday 與 Active Directory 搭配使用時，需要考慮多個來源和目標系統：</span><span class="sxs-lookup"><span data-stu-id="7b081-149">However, when working with Workday and Active Directory, there are multiple source and target systems to be considered:</span></span>

| <span data-ttu-id="7b081-150">來源系統</span><span class="sxs-lookup"><span data-stu-id="7b081-150">Source System</span></span> | <span data-ttu-id="7b081-151">目標系統</span><span class="sxs-lookup"><span data-stu-id="7b081-151">Target System</span></span> | <span data-ttu-id="7b081-152">注意事項</span><span class="sxs-lookup"><span data-stu-id="7b081-152">Notes</span></span> |
| ---------- | ---------- | ---------- |
| <span data-ttu-id="7b081-153">Workday</span><span class="sxs-lookup"><span data-stu-id="7b081-153">Workday</span></span> | <span data-ttu-id="7b081-154">Active Directory 樹系</span><span class="sxs-lookup"><span data-stu-id="7b081-154">Active Directory Forest</span></span> | <span data-ttu-id="7b081-155">系統會將每個樹系視為相異目標系統</span><span class="sxs-lookup"><span data-stu-id="7b081-155">Each forest is treated as a distinct target system</span></span> |
| <span data-ttu-id="7b081-156">Workday</span><span class="sxs-lookup"><span data-stu-id="7b081-156">Workday</span></span> | <span data-ttu-id="7b081-157">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="7b081-157">Azure AD tenant</span></span> | <span data-ttu-id="7b081-158">根據僅限雲端使用者的要求</span><span class="sxs-lookup"><span data-stu-id="7b081-158">As required for cloud-only users</span></span> |
| <span data-ttu-id="7b081-159">Active Directory 樹系</span><span class="sxs-lookup"><span data-stu-id="7b081-159">Active Directory Forest</span></span> | <span data-ttu-id="7b081-160">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="7b081-160">Azure AD tenant</span></span> | <span data-ttu-id="7b081-161">目前由 AAD Connect 處理此流程</span><span class="sxs-lookup"><span data-stu-id="7b081-161">This flow is handled by AAD Connect today</span></span> |
| <span data-ttu-id="7b081-162">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="7b081-162">Azure AD tenant</span></span> | <span data-ttu-id="7b081-163">Workday</span><span class="sxs-lookup"><span data-stu-id="7b081-163">Workday</span></span> | <span data-ttu-id="7b081-164">適用於電子郵件地址的回寫</span><span class="sxs-lookup"><span data-stu-id="7b081-164">For writeback of email addresses</span></span> |

<span data-ttu-id="7b081-165">為了讓這些工作流程便利於多個來源和目標系統，Azure AD 提供可以從 Azure AD 應用程式庫新增的多個佈建連接器應用程式：</span><span class="sxs-lookup"><span data-stu-id="7b081-165">To facilitate these multiple workflows to multiple source and target systems, Azure AD provides multiple provisioning connector apps that you can add from the Azure AD app gallery:</span></span>

![AAD 應用程式庫](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* <span data-ttu-id="7b081-167">**Workday to Active Directory Provisioning** - 此應用程式可協助將使用者帳戶從 Workday 佈建至單一 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="7b081-167">**Workday to Active Directory Provisioning** - This app facilitates user account provisioning from Workday to a single Active Directory forest.</span></span> <span data-ttu-id="7b081-168">如果您擁有多個樹系，則可以針對要進行佈建的每個 Active Directory 樹系，從 Azure AD 應用程式庫新增此應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b081-168">If you have multiple forests, you can add one instance of this app from the Azure AD app gallery for each Active Directory forest you need to provision to.</span></span>

* <span data-ttu-id="7b081-169">**Workday to Azure AD Provisioning** -雖然應使用 AAD Connect 這項工具將 Active Directory 使用者同步處理至 Azure Active Directory，但此應用程式可用於協助將僅限雲端使用者從 Workday 佈建至單一 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7b081-169">**Workday to Azure AD Provisioning** - While AAD Connect is the tool that should be used to synchronize Active Directory users to Azure Active Directory, this app can be used to facilitate provisioning of cloud-only users from Workday to a single Azure Active Directory tenant.</span></span>

* <span data-ttu-id="7b081-170">**Workday Writeback** - 此應用程式可協助將使用者的電子郵件地址從 Azure Active Directory 回寫至 Workday。</span><span class="sxs-lookup"><span data-stu-id="7b081-170">**Workday Writeback** - This app facilitates writeback of user's email addresses from Azure Active Directory to Workday.</span></span>

> [!TIP]
> <span data-ttu-id="7b081-171">您可以使用一般「Workday」應用程式設定 Workday 與 Azure Active Directory 之間的單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b081-171">The regular "Workday" app is used for setting up single sign-on between Workday and Azure Active Directory.</span></span> 

<span data-ttu-id="7b081-172">如何安裝及設定這些特殊佈建連接器應用程式是本教學課程其餘章節的主題。</span><span class="sxs-lookup"><span data-stu-id="7b081-172">How to set up and configure these special provisioning connector apps is the subject of the remaining sections of this tutorial.</span></span> <span data-ttu-id="7b081-173">您選擇要設定的應用程式將取決於需要進行佈建的系統，以及環境中的 Active Directory 樹系和 Azure AD 租用戶數量。</span><span class="sxs-lookup"><span data-stu-id="7b081-173">Which apps you choose to configure will depend on which systems you need to provision to, and how many Active Directory Forests and Azure AD tenants are in your environment.</span></span>

![概觀](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a><span data-ttu-id="7b081-175">在 Workday 中設定系統整合使用者</span><span class="sxs-lookup"><span data-stu-id="7b081-175">Configure a system integration user in Workday</span></span>
<span data-ttu-id="7b081-176">所有 Workday 佈建連接器的常見需求，是其需要 Workday 系統整合帳戶的認證才能連線至 Workday Human Resources API。</span><span class="sxs-lookup"><span data-stu-id="7b081-176">A common requirement of all the Workday provisioning connectors is they require credentials for a Workday system integration account to connect to the Workday Human Resources API.</span></span> <span data-ttu-id="7b081-177">本章節說明如何在 Workday 中建立系統整合者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b081-177">This section describes how to create a system integrator account in Workday.</span></span>

> [!NOTE]
> <span data-ttu-id="7b081-178">您可以略過此程序，改用 Workday 全域系統管理員帳戶做為系統整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b081-178">It is possible to bypass this procedure and instead use a Workday global administrator account as the system integration account.</span></span> <span data-ttu-id="7b081-179">這可能會在示範中正常運作，但不建議用於生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="7b081-179">This may work fine for demos, but is not recommended for production deployments.</span></span>

### <a name="create-an-integration-system-user"></a><span data-ttu-id="7b081-180">建立整合系統使用者</span><span class="sxs-lookup"><span data-stu-id="7b081-180">Create an integration system user</span></span>

<span data-ttu-id="7b081-181">**建立整合系統使用者：**</span><span class="sxs-lookup"><span data-stu-id="7b081-181">**To create an integration system user:**</span></span>

1. <span data-ttu-id="7b081-182">使用系統管理員帳戶登入 Workday 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7b081-182">Sign into your Workday tenant using an administrator account.</span></span> <span data-ttu-id="7b081-183">在 [工作日工作台] 中的搜尋方塊輸入 create user，然後按一下 [建立整合系統使用者]。</span><span class="sxs-lookup"><span data-stu-id="7b081-183">In the **Workday Workbench**, enter create user in the search box, and then click **Create Integration System User**.</span></span> 
   
    <span data-ttu-id="7b081-184">![建立使用者](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="7b081-184">![Create user](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Create user")</span></span>
2. <span data-ttu-id="7b081-185">為新的「整合系統使用者」 提供使用者名稱和密碼來完成「建立整合系統使用者」  工作。</span><span class="sxs-lookup"><span data-stu-id="7b081-185">Complete the **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="7b081-186">保持 [下次登入時要求新密碼] 選項未核取，因為該使用者會以程式設計的方式登入。</span><span class="sxs-lookup"><span data-stu-id="7b081-186">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span> 
 * <span data-ttu-id="7b081-187">保持 [工作階段逾時分鐘數] 為預設值 [0]，這會防止使用者的工作階段提早逾時。</span><span class="sxs-lookup"><span data-stu-id="7b081-187">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span></span> 
   
    <span data-ttu-id="7b081-188">![建立整合系統使用者](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "建立整合系統使用者")</span><span class="sxs-lookup"><span data-stu-id="7b081-188">![Create Integration System User](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Create Integration System User")</span></span>

### <a name="create-a-security-group"></a><span data-ttu-id="7b081-189">建立安全性群組</span><span class="sxs-lookup"><span data-stu-id="7b081-189">Create a security group</span></span>
<span data-ttu-id="7b081-190">您需要建立未受限制的整合系統安全性群組，並將使用者指派到該群組。</span><span class="sxs-lookup"><span data-stu-id="7b081-190">You need to create an unconstrained integration system security group and assign the user to it.</span></span>

<span data-ttu-id="7b081-191">**建立安全性群組：**</span><span class="sxs-lookup"><span data-stu-id="7b081-191">**To create a security group:**</span></span>

1. <span data-ttu-id="7b081-192">在搜尋方塊中輸入 create security group，然後按一下 [建立安全性群組] 連結。</span><span class="sxs-lookup"><span data-stu-id="7b081-192">Enter create security group in the search box, and then click **Create Security Group**.</span></span> 
   
    <span data-ttu-id="7b081-193">![建立安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "建立安全性群組")</span><span class="sxs-lookup"><span data-stu-id="7b081-193">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span></span>
2. <span data-ttu-id="7b081-194">完成**建立安全性群組**工作。</span><span class="sxs-lookup"><span data-stu-id="7b081-194">Complete the **Create Security Group** task.</span></span>  
3. <span data-ttu-id="7b081-195">從 [租用安全性群組類型] 下拉式清單選取 [整合系統安全性群組—未受限制]。</span><span class="sxs-lookup"><span data-stu-id="7b081-195">Select Integration System Security Group—Unconstrained from the **Type of Tenanted Security Group** dropdown.</span></span>
4. <span data-ttu-id="7b081-196">建立安全性群組以供明確新增使用者。</span><span class="sxs-lookup"><span data-stu-id="7b081-196">Create a security group to which members will be explicitly added.</span></span> 
   
    <span data-ttu-id="7b081-197">![建立安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "建立安全性群組")</span><span class="sxs-lookup"><span data-stu-id="7b081-197">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span></span>

### <a name="assign-the-integration-system-user-to-the-security-group"></a><span data-ttu-id="7b081-198">將整合系統使用者指派到安全性群組</span><span class="sxs-lookup"><span data-stu-id="7b081-198">Assign the integration system user to the security group</span></span>

<span data-ttu-id="7b081-199">**指派整合系統使用者：**</span><span class="sxs-lookup"><span data-stu-id="7b081-199">**To assign the integration system user:**</span></span>

1. <span data-ttu-id="7b081-200">在搜尋方塊中輸入 edit security group，然後按一下 [編輯全性群組] 連結。</span><span class="sxs-lookup"><span data-stu-id="7b081-200">Enter edit security group in the search box, and then click **Edit Security Group**.</span></span> 
   
    <span data-ttu-id="7b081-201">![編輯安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "編輯安全性群組")</span><span class="sxs-lookup"><span data-stu-id="7b081-201">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edit Security Group")</span></span>
2. <span data-ttu-id="7b081-202">依名稱搜尋新的整合安全性群組，並選取該群組。</span><span class="sxs-lookup"><span data-stu-id="7b081-202">Search for, and select the new integration security group by name.</span></span> 
   
    <span data-ttu-id="7b081-203">![編輯安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "編輯安全性群組")</span><span class="sxs-lookup"><span data-stu-id="7b081-203">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edit Security Group")</span></span>
3. <span data-ttu-id="7b081-204">將新的整合系統使用者指派到安全性群組。</span><span class="sxs-lookup"><span data-stu-id="7b081-204">Add the new integration system user to the new security group.</span></span> 
   
    <span data-ttu-id="7b081-205">![系統安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "系統安全性群組")</span><span class="sxs-lookup"><span data-stu-id="7b081-205">![System Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "System Security Group")</span></span>  

### <a name="configure-security-group-options"></a><span data-ttu-id="7b081-206">設定安全性群組選項</span><span class="sxs-lookup"><span data-stu-id="7b081-206">Configure security group options</span></span>
<span data-ttu-id="7b081-207">在此步驟中，您授予新的安全性群組，對受下列網域安全性原則保護之物件進行 **Get** 和 **Put** 作業：</span><span class="sxs-lookup"><span data-stu-id="7b081-207">In this step, you grant to the new security group permissions for **Get** and **Put** operations on the objects secured by the following domain security policies:</span></span>

* <span data-ttu-id="7b081-208">外部帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="7b081-208">External Account Provisioning</span></span>
* <span data-ttu-id="7b081-209">人員資料：公用人員報告</span><span class="sxs-lookup"><span data-stu-id="7b081-209">Worker Data: Public Worker Reports</span></span>
* <span data-ttu-id="7b081-210">人員資料：所有職位</span><span class="sxs-lookup"><span data-stu-id="7b081-210">Worker Data: All Positions</span></span>
* <span data-ttu-id="7b081-211">人員資料：目前人員配置資訊</span><span class="sxs-lookup"><span data-stu-id="7b081-211">Worker Data: Current Staffing Information</span></span>
* <span data-ttu-id="7b081-212">人員資料：人員個人檔案的職稱</span><span class="sxs-lookup"><span data-stu-id="7b081-212">Worker Data: Business Title on Worker Profile</span></span>

<span data-ttu-id="7b081-213">**設定安全性群組選項：**</span><span class="sxs-lookup"><span data-stu-id="7b081-213">**To configure security group options:**</span></span>

1. <span data-ttu-id="7b081-214">在搜尋方塊中輸入 domain security policies，然後按一下 [功能區域的網域安全性原則]。</span><span class="sxs-lookup"><span data-stu-id="7b081-214">Enter domain security policies in the search box, and then click on the link **Domain Security Policies for Functional Area**.</span></span>  
   
    <span data-ttu-id="7b081-215">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="7b081-215">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="7b081-216">搜尋 system 並選取 [系統]  功能區域。</span><span class="sxs-lookup"><span data-stu-id="7b081-216">Search for system and select the **System** functional area.</span></span>  <span data-ttu-id="7b081-217">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7b081-217">Click **OK**.</span></span>  
   
    <span data-ttu-id="7b081-218">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="7b081-218">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="7b081-219">在 [系統] 功能區域的安全性原則清單中，展開 [安全性管理]，並選取 [外部帳戶佈建] 網域安全性原則。</span><span class="sxs-lookup"><span data-stu-id="7b081-219">In the list of security policies for the System functional area, expand **Security Administration** and select the domain security policy **External Account Provisioning**.</span></span>  
   
    <span data-ttu-id="7b081-220">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="7b081-220">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span></span>  
4. <span data-ttu-id="7b081-221">按一下 [編輯權限] 按鈕，然後在 [編輯權限] 畫面上，將新的安全性群組新增具有 **Get** 和 **Put** 整合權限的群組清單。</span><span class="sxs-lookup"><span data-stu-id="7b081-221">Click **Edit Permissions**, and then, on the **Edit Permissions**dialog page, add the new security group to the list of security groups with **Get** and **Put** integration permissions.</span></span> 
   
    <span data-ttu-id="7b081-222">![編輯權限](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "編輯權限")</span><span class="sxs-lookup"><span data-stu-id="7b081-222">![Edit Permission](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Edit Permission")</span></span>  
5. <span data-ttu-id="7b081-223">重複上述步驟 1，以返回選取功能區域的畫面，這次改為搜尋 staffing，然後選取 [人員配置] 功能區域，再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7b081-223">Repeat step 1 above to return to the screen for selecting functional areas, and this time, search for staffing, select the **Staffing functional area** and click **OK**.</span></span>
   
    <span data-ttu-id="7b081-224">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="7b081-224">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Domain Security Policies")</span></span>  
6. <span data-ttu-id="7b081-225">在 [人員配置] 功能區域的安全性原則清單中，展開 [人員資料：人員配置]，並對其餘的各安全性原則重複上述步驟 4：</span><span class="sxs-lookup"><span data-stu-id="7b081-225">In the list of security policies for the Staffing functional area, expand **Worker Data: Staffing** and repeat step 4 above for each of these remaining security policies:</span></span>

   * <span data-ttu-id="7b081-226">人員資料：公用人員報告</span><span class="sxs-lookup"><span data-stu-id="7b081-226">Worker Data: Public Worker Reports</span></span>
   * <span data-ttu-id="7b081-227">人員資料：所有職位</span><span class="sxs-lookup"><span data-stu-id="7b081-227">Worker Data: All Positions</span></span>
   * <span data-ttu-id="7b081-228">人員資料：目前人員配置資訊</span><span class="sxs-lookup"><span data-stu-id="7b081-228">Worker Data: Current Staffing Information</span></span>
   * <span data-ttu-id="7b081-229">人員資料：人員個人檔案的職稱</span><span class="sxs-lookup"><span data-stu-id="7b081-229">Worker Data: Business Title on Worker Profile</span></span>
   
7. <span data-ttu-id="7b081-230">重複上述步驟 1，以返回選取功能區域的畫面，這次改為搜尋 **Contact Information**，然後選取 [人員配置] 功能區域，再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7b081-230">Repeat step 1, above, to return to the screen for selecting  functional areas, and this time, search for **Contact Information**,  select the Staffing functional area, and click **OK**.</span></span>

8.  <span data-ttu-id="7b081-231">在 [人員配置] 功能區域的安全性原則清單中，展開 [人員資料：公司連絡資訊]，並對下列安全性原則重複上述步驟 4：</span><span class="sxs-lookup"><span data-stu-id="7b081-231">In the list of security policies for the Staffing functional area, expand **Worker Data: Work Contact Information**, and repeat step 4 above for the security policies below:</span></span>

    * <span data-ttu-id="7b081-232">人員資料：公司電子郵件</span><span class="sxs-lookup"><span data-stu-id="7b081-232">Worker Data: Work Email</span></span>

    <span data-ttu-id="7b081-233">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="7b081-233">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Domain Security Policies")</span></span>  
    
### <a name="activate-security-policy-changes"></a><span data-ttu-id="7b081-234">啟用安全性原則變更</span><span class="sxs-lookup"><span data-stu-id="7b081-234">Activate security policy changes</span></span>

<span data-ttu-id="7b081-235">**啟用安全性原則變更：**</span><span class="sxs-lookup"><span data-stu-id="7b081-235">**To activate security policy changes:**</span></span>

1. <span data-ttu-id="7b081-236">在搜尋方塊中輸入 activate，然後按一下 [啟用擱置的安全性原則變更] 連結。</span><span class="sxs-lookup"><span data-stu-id="7b081-236">Enter activate in the search box, and then click on the link **Activate Pending Security Policy Changes**.</span></span> 
   
    <span data-ttu-id="7b081-237">![啟用](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "啟用")</span><span class="sxs-lookup"><span data-stu-id="7b081-237">![Activate](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activate")</span></span> 
2. <span data-ttu-id="7b081-238">輸入供稽核用的註解並按一下 [確定] 按鈕，以開始「啟用擱置的安全性原則變更」工作。</span><span class="sxs-lookup"><span data-stu-id="7b081-238">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span></span> 
   
    <span data-ttu-id="7b081-239">![啟用擱置的安全性](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "啟用擱置的安全性")</span><span class="sxs-lookup"><span data-stu-id="7b081-239">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span></span>   
3. <span data-ttu-id="7b081-240">在下一個畫面核取 [確認] 核取方塊，然後按一下 [確定] 以完成工作。</span><span class="sxs-lookup"><span data-stu-id="7b081-240">Complete the task on the next screen by checking the checkbox **Confirm**, and then click **OK**.</span></span> 
   
    <span data-ttu-id="7b081-241">![啟用擱置的安全性](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "啟用擱置的安全性")</span><span class="sxs-lookup"><span data-stu-id="7b081-241">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configuring-user-provisioning-from-workday-to-active-directory"></a><span data-ttu-id="7b081-242">設定將使用者從 Workday 佈建至 Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b081-242">Configuring user provisioning from Workday to Active Directory</span></span>
<span data-ttu-id="7b081-243">請遵循下列指示來設定將使用者帳戶從 Workday 佈建至需要進行佈建的每個 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="7b081-243">Follow these instructions to configure user account provisioning from Workday to each Active Directory forest that you require provisioning to.</span></span>

### <a name="part-1-adding-the-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="7b081-244">第 1 部分：新增佈建連接器應用程式和建立 Workday 連接</span><span class="sxs-lookup"><span data-stu-id="7b081-244">Part 1: Adding the provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="7b081-245">**若要設定 Workday 至 Active Directory 佈建：**</span><span class="sxs-lookup"><span data-stu-id="7b081-245">**To configure Workday to Active Directory provisioning:**</span></span>

1.  <span data-ttu-id="7b081-246">移至 <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="7b081-246">Go to <https://portal.azure.com></span></span>

2.  <span data-ttu-id="7b081-247">在左側導覽列中，選取 [Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="7b081-247">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="7b081-248">依序選取 [企業應用程式] 和 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7b081-248">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="7b081-249">選取 [新增應用程式]，然後選取 [全部] 類別。</span><span class="sxs-lookup"><span data-stu-id="7b081-249">Select **Add an application**, and select the **All** category.</span></span>

5.  <span data-ttu-id="7b081-250">搜尋 **Workday Provisioning to Active Directory**，並從資源庫新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b081-250">Search for **Workday Provisioning to Active Directory**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="7b081-251">新增應用程式並顯示應用程式詳細資料畫面之後，請選取 [佈建]</span><span class="sxs-lookup"><span data-stu-id="7b081-251">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="7b081-252">將 [佈建模式] 變更為 [自動]</span><span class="sxs-lookup"><span data-stu-id="7b081-252">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="7b081-253">完成 [系統管理員認證] 區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7b081-253">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="7b081-254">**系統管理員使用者名稱** – 輸入 Workday 整合系統帳戶的使用者名稱，並附加租用戶網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7b081-254">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="7b081-255">**其應該類似於：username@contoso4**</span><span class="sxs-lookup"><span data-stu-id="7b081-255">**Should look something like: username@contoso4**</span></span>

   * <span data-ttu-id="7b081-256">**系統管理員密碼 –** 輸入 Workday 整合系統帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="7b081-256">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="7b081-257">**租用戶 URL –** 輸入租用戶 Workday Web 服務端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="7b081-257">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="7b081-258">其應該類似於：https://wd3-impl-services1.workday.com/ccx/service/contoso4，其中請將 contoso4 取代為正確的租用戶名稱，並將 wd3-impl 取代為正確的環境字串。</span><span class="sxs-lookup"><span data-stu-id="7b081-258">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string.</span></span>

   * <span data-ttu-id="7b081-259">**Active Directory 樹系 -** Get-ADForest powershell commandlet 所傳回 Active Directory 樹系的「名稱」。</span><span class="sxs-lookup"><span data-stu-id="7b081-259">**Active Directory Forest -** The “Name” of your Active Directory forest, as returned by the Get-ADForest powershell commandlet.</span></span> <span data-ttu-id="7b081-260">此字串通常類似於：*contoso.com*</span><span class="sxs-lookup"><span data-stu-id="7b081-260">This is typically a string like: *contoso.com*</span></span>

   * <span data-ttu-id="7b081-261">**Active Directory 容器 -** 輸入包含 AD 樹系中所有使用者的容器字串。</span><span class="sxs-lookup"><span data-stu-id="7b081-261">**Active Directory Container -** Enter the container string that contains all users in your AD forest.</span></span> <span data-ttu-id="7b081-262">範例：*OU=Standard Users,OU=Users,DC=contoso,DC=test*</span><span class="sxs-lookup"><span data-stu-id="7b081-262">Example: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span></span>

   * <span data-ttu-id="7b081-263">**電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7b081-263">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="7b081-264">按一下 [測試連線] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b081-264">Click the **Test Connection** button.</span></span> <span data-ttu-id="7b081-265">如果連線測試成功，請按一下頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b081-265">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="7b081-266">如果失敗，請仔細檢查 Workday 認證在 Workday 中是否有效。</span><span class="sxs-lookup"><span data-stu-id="7b081-266">If it fails, double-check that the Workday credentials are valid in Workday.</span></span> 

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="7b081-268">第 2 部分：設定屬性對應</span><span class="sxs-lookup"><span data-stu-id="7b081-268">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="7b081-269">在本節中，您會設定使用者資料從 Workday 流動至 Active Directory 的方式。</span><span class="sxs-lookup"><span data-stu-id="7b081-269">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="7b081-270">在 [佈建] 索引標籤的 [對應] 下，按一下 [將 Workday 人員同步至內部部署]。</span><span class="sxs-lookup"><span data-stu-id="7b081-270">On the Provisioning tab under **Mappings**, click **Synchronize Workday Workers to OnPremises**.</span></span>

2.  <span data-ttu-id="7b081-271">在 [來源物件範圍] 欄位中，您可以透過定義一組屬性型篩選，選取應該佈建至 AD 的 Workday 使用者集合範圍。</span><span class="sxs-lookup"><span data-stu-id="7b081-271">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="7b081-272">預設範圍是「Workday 中的所有使用者」。</span><span class="sxs-lookup"><span data-stu-id="7b081-272">The default scope is “all users in Workday”.</span></span> <span data-ttu-id="7b081-273">範例篩選：</span><span class="sxs-lookup"><span data-stu-id="7b081-273">Example filters:</span></span>

   * <span data-ttu-id="7b081-274">範例：人員識別碼介於 1000000 到 2000000 之間的使用者範圍</span><span class="sxs-lookup"><span data-stu-id="7b081-274">Example: Scope to users with Worker IDs between 1000000 and    2000000</span></span>

      * <span data-ttu-id="7b081-275">屬性：WorkerID</span><span class="sxs-lookup"><span data-stu-id="7b081-275">Attribute: WorkerID</span></span>

      * <span data-ttu-id="7b081-276">運算子：REGEX Match</span><span class="sxs-lookup"><span data-stu-id="7b081-276">Operator: REGEX Match</span></span>

      * <span data-ttu-id="7b081-277">值：(1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="7b081-277">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="7b081-278">範例：僅員工和非約聘人員</span><span class="sxs-lookup"><span data-stu-id="7b081-278">Example: Only employees and not contingent workers</span></span> 

      * <span data-ttu-id="7b081-279">屬性：EmployeeID</span><span class="sxs-lookup"><span data-stu-id="7b081-279">Attribute: EmployeeID</span></span>

      * <span data-ttu-id="7b081-280">運算子：IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="7b081-280">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="7b081-281">在 [目標物件動作] 欄位中，您可以全域篩選允許在 Active Directory 上執行哪些動作。</span><span class="sxs-lookup"><span data-stu-id="7b081-281">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Active Directory.</span></span> <span data-ttu-id="7b081-282">最常見的動作是 [建立] 和 [更新]。</span><span class="sxs-lookup"><span data-stu-id="7b081-282">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="7b081-283">在 [屬性對應] 區段中，您可以定義個別 Workday 屬性如何對應至 Active Directory 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-283">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span></span>

5. <span data-ttu-id="7b081-284">按一下現有的屬性對應以進行更新，或按一下畫面底端的 [新增新對應] 以新增新對應。</span><span class="sxs-lookup"><span data-stu-id="7b081-284">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span></span> <span data-ttu-id="7b081-285">個別屬性對應支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="7b081-285">An individual attribute mapping supports these properties:</span></span>

      * <span data-ttu-id="7b081-286">**對應類型**</span><span class="sxs-lookup"><span data-stu-id="7b081-286">**Mapping Type**</span></span>

         * <span data-ttu-id="7b081-287">**直接** – 將 Workday 屬性的值寫入 AD 屬性，且不進行變更</span><span class="sxs-lookup"><span data-stu-id="7b081-287">**Direct** – Writes the value of the Workday attribute      to the AD attribute, with no changes</span></span>

         * <span data-ttu-id="7b081-288">**常數** - 將靜態的常數字串值寫入 AD 屬性</span><span class="sxs-lookup"><span data-stu-id="7b081-288">**Constant** - Write a static, constant string value to      the AD attribute</span></span>

         * <span data-ttu-id="7b081-289">**運算式** – 可讓您根據一或多個 Workday 屬性，將自訂值寫入 AD 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-289">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="7b081-290">[如需詳細資訊，請參閱這篇有關運算式的文章](active-directory-saas-writing-expressions-for-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="7b081-290">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

      * <span data-ttu-id="7b081-291">**來源屬性** - 來自 Workday 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-291">**Source attribute** - The user attribute from Workday.</span></span>

      * <span data-ttu-id="7b081-292">**預設值** – 選用。</span><span class="sxs-lookup"><span data-stu-id="7b081-292">**Default value** – Optional.</span></span> <span data-ttu-id="7b081-293">如果來源屬性具有空值，則對應將會改為寫入此值。</span><span class="sxs-lookup"><span data-stu-id="7b081-293">If the source attribute has an empty value, the mapping will write this value instead.</span></span>
            <span data-ttu-id="7b081-294">最常見的設定是將其保留空白。</span><span class="sxs-lookup"><span data-stu-id="7b081-294">Most common configuration is to leave this blank.</span></span>

      * <span data-ttu-id="7b081-295">**目標屬性** – Active Directory 中的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-295">**Target attribute** – The user attribute in Active     Directory.</span></span>

      * <span data-ttu-id="7b081-296">**使用此屬性比對物件** – 是否應該將此對應用於唯一識別 Workday 與 Active Directory 之間的使用者。</span><span class="sxs-lookup"><span data-stu-id="7b081-296">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Active Directory.</span></span> <span data-ttu-id="7b081-297">此設定通常會設定於 Workday 的 [人員識別碼] 欄位，且通常會在 Active Directory 中對應至其中一個員工識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-297">This is typically set on the Worker ID field for Workday, which is typically mapped to one of the Employee ID attributes in Active Directory.</span></span>

      * <span data-ttu-id="7b081-298">**比對優先順序** – 您可以設定多個比對屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-298">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="7b081-299">具有多個屬性時，系統會以此欄位定義的順序進行評估。</span><span class="sxs-lookup"><span data-stu-id="7b081-299">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="7b081-300">只要找到相符項目，便不會評估進一步比對屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-300">As soon as a match is found, no further matching attributes are evaluated.</span></span>

      * <span data-ttu-id="7b081-301">**套用此對應**</span><span class="sxs-lookup"><span data-stu-id="7b081-301">**Apply this mapping**</span></span>
       
         * <span data-ttu-id="7b081-302">**一律** – 將此對應套用於使用者建立和更新動作</span><span class="sxs-lookup"><span data-stu-id="7b081-302">**Always** – Apply this mapping on both user creation      and update actions</span></span>

         * <span data-ttu-id="7b081-303">**僅限建立期間** - 僅將此對應套用於使用者建立動作</span><span class="sxs-lookup"><span data-stu-id="7b081-303">**Only during creation** - Apply this mapping only on      user creation actions</span></span>

6. <span data-ttu-id="7b081-304">若要儲存您的對應，請按一下 [屬性對應] 區段頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7b081-304">To save your mappings, click **Save** at the top of the      Attribute Mapping section.</span></span>

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

<span data-ttu-id="7b081-306">**下列為 Workday 與 Active Directory 之間的一些範例屬性對應，以及一些常用運算式**</span><span class="sxs-lookup"><span data-stu-id="7b081-306">**Below are some example attribute mappings between Workday and Active Directory, with some common expressions**</span></span>

-   <span data-ttu-id="7b081-307">對應至 parentDistinguishedName AD 屬性的運算式可用於根據一或多個 Workday 來源屬性，將使用者佈建至特定 OU。</span><span class="sxs-lookup"><span data-stu-id="7b081-307">The expression that maps to the parentDistinguishedName AD attribute can be used to provision a user to a specific OU based on one or more Workday source attributes.</span></span> <span data-ttu-id="7b081-308">此範例會根據使用者在 Workday 中的城市資料，將其置於不同的 OU。</span><span class="sxs-lookup"><span data-stu-id="7b081-308">This example places users in different OUs depending on their city data in Workday.</span></span>

-   <span data-ttu-id="7b081-309">對應至 userPrincipalName AD 屬性的運算式會建立 firstName.LastName@contoso.com 的 UPN。</span><span class="sxs-lookup"><span data-stu-id="7b081-309">The expression that maps to the userPrincipalName AD attribute create a UPN of firstName.LastName@contoso.com.</span></span> <span data-ttu-id="7b081-310">其也會取代不合法的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="7b081-310">It also replaces illegal special characters.</span></span>

-   [<span data-ttu-id="7b081-311">此為有關撰寫運算式的文件</span><span class="sxs-lookup"><span data-stu-id="7b081-311">There is documentation on writing expressions here</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| <span data-ttu-id="7b081-312">WORKDAY 屬性</span><span class="sxs-lookup"><span data-stu-id="7b081-312">WORKDAY ATTRIBUTE</span></span> | <span data-ttu-id="7b081-313">ACTIVE DIRECTORY 屬性</span><span class="sxs-lookup"><span data-stu-id="7b081-313">ACTIVE DIRECTORY ATTRIBUTE</span></span> |  <span data-ttu-id="7b081-314">比對識別碼？</span><span class="sxs-lookup"><span data-stu-id="7b081-314">MATCHING ID?</span></span> | <span data-ttu-id="7b081-315">建立/更新</span><span class="sxs-lookup"><span data-stu-id="7b081-315">CREATE / UPDATE</span></span> |
| ---------- | ---------- | ---------- | ---------- |
|  <span data-ttu-id="7b081-316">**WorkerID**</span><span class="sxs-lookup"><span data-stu-id="7b081-316">**WorkerID**</span></span>  |  <span data-ttu-id="7b081-317">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="7b081-317">EmployeeID</span></span> | <span data-ttu-id="7b081-318">**是**</span><span class="sxs-lookup"><span data-stu-id="7b081-318">**Yes**</span></span> | <span data-ttu-id="7b081-319">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="7b081-319">Written on create only</span></span> | 
|  <span data-ttu-id="7b081-320">**Municipality**</span><span class="sxs-lookup"><span data-stu-id="7b081-320">**Municipality**</span></span>   |   <span data-ttu-id="7b081-321">l</span><span class="sxs-lookup"><span data-stu-id="7b081-321">l</span></span>   |     | <span data-ttu-id="7b081-322">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-322">Create + update</span></span> |
|  <span data-ttu-id="7b081-323">**Company**</span><span class="sxs-lookup"><span data-stu-id="7b081-323">**Company**</span></span>         | <span data-ttu-id="7b081-324">company</span><span class="sxs-lookup"><span data-stu-id="7b081-324">company</span></span>   |     |  <span data-ttu-id="7b081-325">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-325">Create + update</span></span> |
|  <span data-ttu-id="7b081-326">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="7b081-326">**CountryReferenceTwoLetter**</span></span>      |   <span data-ttu-id="7b081-327">co</span><span class="sxs-lookup"><span data-stu-id="7b081-327">co</span></span> |     |   <span data-ttu-id="7b081-328">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-328">Create + update</span></span> |
| <span data-ttu-id="7b081-329">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="7b081-329">**CountryReferenceTwoLetter**</span></span>    |  <span data-ttu-id="7b081-330">c</span><span class="sxs-lookup"><span data-stu-id="7b081-330">c</span></span>  |     |         <span data-ttu-id="7b081-331">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-331">Create + update</span></span> |
| <span data-ttu-id="7b081-332">**SupervisoryOrganization**</span><span class="sxs-lookup"><span data-stu-id="7b081-332">**SupervisoryOrganization**</span></span>  | <span data-ttu-id="7b081-333">department</span><span class="sxs-lookup"><span data-stu-id="7b081-333">department</span></span>  |     |  <span data-ttu-id="7b081-334">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-334">Create + update</span></span> |
|  <span data-ttu-id="7b081-335">**PreferredNameData**</span><span class="sxs-lookup"><span data-stu-id="7b081-335">**PreferredNameData**</span></span>  |  <span data-ttu-id="7b081-336">displayName</span><span class="sxs-lookup"><span data-stu-id="7b081-336">displayName</span></span> |     |   <span data-ttu-id="7b081-337">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-337">Create + update</span></span> |
| <span data-ttu-id="7b081-338">**EmployeeID**</span><span class="sxs-lookup"><span data-stu-id="7b081-338">**EmployeeID**</span></span>    |  <span data-ttu-id="7b081-339">cn</span><span class="sxs-lookup"><span data-stu-id="7b081-339">cn</span></span>    |   |   <span data-ttu-id="7b081-340">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="7b081-340">Written on create only</span></span> |
| <span data-ttu-id="7b081-341">**Fax**</span><span class="sxs-lookup"><span data-stu-id="7b081-341">**Fax**</span></span>      | <span data-ttu-id="7b081-342">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="7b081-342">facsimileTelephoneNumber</span></span>     |     |    <span data-ttu-id="7b081-343">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-343">Create + update</span></span> |
| <span data-ttu-id="7b081-344">**名字**</span><span class="sxs-lookup"><span data-stu-id="7b081-344">**FirstName**</span></span>   | <span data-ttu-id="7b081-345">givenName</span><span class="sxs-lookup"><span data-stu-id="7b081-345">givenName</span></span>       |     |    <span data-ttu-id="7b081-346">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-346">Create + update</span></span> |
| <span data-ttu-id="7b081-347">**Switch(\[Active\], , "0", "True", "1",)**</span><span class="sxs-lookup"><span data-stu-id="7b081-347">**Switch(\[Active\], , "0", "True", "1",)**</span></span> |  <span data-ttu-id="7b081-348">accountDisabled</span><span class="sxs-lookup"><span data-stu-id="7b081-348">accountDisabled</span></span>      |     | <span data-ttu-id="7b081-349">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-349">Create + update</span></span> |
| <span data-ttu-id="7b081-350">**Mobile**</span><span class="sxs-lookup"><span data-stu-id="7b081-350">**Mobile**</span></span>  |    <span data-ttu-id="7b081-351">mobile</span><span class="sxs-lookup"><span data-stu-id="7b081-351">mobile</span></span>       |     |       <span data-ttu-id="7b081-352">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="7b081-352">Written on create only</span></span> |
| <span data-ttu-id="7b081-353">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="7b081-353">**EmailAddress**</span></span>    | <span data-ttu-id="7b081-354">mail</span><span class="sxs-lookup"><span data-stu-id="7b081-354">mail</span></span>    |     |     <span data-ttu-id="7b081-355">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-355">Create + update</span></span> |
| <span data-ttu-id="7b081-356">**ManagerReference**</span><span class="sxs-lookup"><span data-stu-id="7b081-356">**ManagerReference**</span></span>   | <span data-ttu-id="7b081-357">manager</span><span class="sxs-lookup"><span data-stu-id="7b081-357">manager</span></span>  |     |  <span data-ttu-id="7b081-358">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-358">Create + update</span></span> |
| <span data-ttu-id="7b081-359">**WorkSpaceReference**</span><span class="sxs-lookup"><span data-stu-id="7b081-359">**WorkSpaceReference**</span></span> | <span data-ttu-id="7b081-360">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="7b081-360">physicalDeliveryOfficeName</span></span>    |     |  <span data-ttu-id="7b081-361">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-361">Create + update</span></span> |
| <span data-ttu-id="7b081-362">**PostalCode**</span><span class="sxs-lookup"><span data-stu-id="7b081-362">**PostalCode**</span></span>  |   <span data-ttu-id="7b081-363">postalCode</span><span class="sxs-lookup"><span data-stu-id="7b081-363">postalCode</span></span>  |     | <span data-ttu-id="7b081-364">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-364">Create + update</span></span> |
| <span data-ttu-id="7b081-365">**LocalReference**</span><span class="sxs-lookup"><span data-stu-id="7b081-365">**LocalReference**</span></span> |  <span data-ttu-id="7b081-366">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="7b081-366">preferredLanguage</span></span>  |     |  <span data-ttu-id="7b081-367">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-367">Create + update</span></span> |
| <span data-ttu-id="7b081-368">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span><span class="sxs-lookup"><span data-stu-id="7b081-368">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span></span>|<span data-ttu-id="7b081-369">\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**</span><span class="sxs-lookup"><span data-stu-id="7b081-369">\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**</span></span>      |    <span data-ttu-id="7b081-370">sAMAccountName</span><span class="sxs-lookup"><span data-stu-id="7b081-370">sAMAccountName</span></span>            |     |         <span data-ttu-id="7b081-371">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="7b081-371">Written on create only</span></span> |
| <span data-ttu-id="7b081-372">**姓氏**</span><span class="sxs-lookup"><span data-stu-id="7b081-372">**LastName**</span></span>   |   <span data-ttu-id="7b081-373">sn</span><span class="sxs-lookup"><span data-stu-id="7b081-373">sn</span></span>   |     |  <span data-ttu-id="7b081-374">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-374">Create + update</span></span> |
| <span data-ttu-id="7b081-375">**CountryRegionReference**</span><span class="sxs-lookup"><span data-stu-id="7b081-375">**CountryRegionReference**</span></span> |  <span data-ttu-id="7b081-376">st</span><span class="sxs-lookup"><span data-stu-id="7b081-376">st</span></span>     |     | <span data-ttu-id="7b081-377">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-377">Create + update</span></span> |
| <span data-ttu-id="7b081-378">**AddressLineData**</span><span class="sxs-lookup"><span data-stu-id="7b081-378">**AddressLineData**</span></span>    |  <span data-ttu-id="7b081-379">streetAddress</span><span class="sxs-lookup"><span data-stu-id="7b081-379">streetAddress</span></span>  |     |   <span data-ttu-id="7b081-380">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-380">Create + update</span></span> |
| <span data-ttu-id="7b081-381">**PrimaryWorkTelephone**</span><span class="sxs-lookup"><span data-stu-id="7b081-381">**PrimaryWorkTelephone**</span></span>  |  <span data-ttu-id="7b081-382">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="7b081-382">telephoneNumber</span></span>   |     | <span data-ttu-id="7b081-383">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="7b081-383">Written on create only</span></span> |
| <span data-ttu-id="7b081-384">**BusinessTitle**</span><span class="sxs-lookup"><span data-stu-id="7b081-384">**BusinessTitle**</span></span>   |  <span data-ttu-id="7b081-385">title</span><span class="sxs-lookup"><span data-stu-id="7b081-385">title</span></span>     |     |  <span data-ttu-id="7b081-386">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-386">Create + update</span></span> |
| <span data-ttu-id="7b081-387">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span><span class="sxs-lookup"><span data-stu-id="7b081-387">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span></span>   | <span data-ttu-id="7b081-388">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="7b081-388">userPrincipalName</span></span>     |     | <span data-ttu-id="7b081-389">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-389">Create + update</span></span>                                                   
| <span data-ttu-id="7b081-390">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span><span class="sxs-lookup"><span data-stu-id="7b081-390">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span></span>  | <span data-ttu-id="7b081-391">parentDistinguishedName</span><span class="sxs-lookup"><span data-stu-id="7b081-391">parentDistinguishedName</span></span>     |     |  <span data-ttu-id="7b081-392">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="7b081-392">Create + update</span></span> |
  
### <a name="part-3-configure-the-on-premises-synchronization-agent"></a><span data-ttu-id="7b081-393">第 3 部分：設定內部部署同步代理程式</span><span class="sxs-lookup"><span data-stu-id="7b081-393">Part 3: Configure the on-premises synchronization agent</span></span>

<span data-ttu-id="7b081-394">若要佈建至 Active Directory 內部部署，您必須在所需 Active Directory 樹系的已加入網域伺服器上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="7b081-394">In order to provision to Active Directory on-premises, an agent must be installed on a domain-joined server in the desire Active Directory forest.</span></span> <span data-ttu-id="7b081-395">您需要網域系統管理員 (或企業系統管理員) 認證才能完成此程序。</span><span class="sxs-lookup"><span data-stu-id="7b081-395">Domain admin (or Enterprise admin) credentials are required to complete the procedure.</span></span>

<span data-ttu-id="7b081-396">**[您可以在此處下載內部部署同步代理程式](https://go.microsoft.com/fwlink/?linkid=847801)**</span><span class="sxs-lookup"><span data-stu-id="7b081-396">**[You can download the on-premises synchronization agent here](https://go.microsoft.com/fwlink/?linkid=847801)**</span></span>

<span data-ttu-id="7b081-397">安裝代理程式之後，請執行下列 PowerShell 命令以設定環境的代理程式。</span><span class="sxs-lookup"><span data-stu-id="7b081-397">After installing agent, run the Powershell commands below to configure the agent for your environment.</span></span>

<span data-ttu-id="7b081-398">**命令 1**</span><span class="sxs-lookup"><span data-stu-id="7b081-398">**Command #1**</span></span>

> <span data-ttu-id="7b081-399">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span><span class="sxs-lookup"><span data-stu-id="7b081-399">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span></span>

> <span data-ttu-id="7b081-400">import-module AADSyncAgent.psd1</span><span class="sxs-lookup"><span data-stu-id="7b081-400">import-module AADSyncAgent.psd1</span></span>

<span data-ttu-id="7b081-401">**命令 2**</span><span class="sxs-lookup"><span data-stu-id="7b081-401">**Command #2**</span></span>

> <span data-ttu-id="7b081-402">Add-ADSyncAgentActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b081-402">Add-ADSyncAgentActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="7b081-403">輸入：針對「目錄名稱」輸入 AD 樹系名稱，如第 \#2 部分所輸入</span><span class="sxs-lookup"><span data-stu-id="7b081-403">Input: For "Directory Name", enter the AD Forest name, as entered in part \#2</span></span>
* <span data-ttu-id="7b081-404">輸入：Active Directory 樹系的系統管理員使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="7b081-404">Input: Admin username and password for Active Directory forest</span></span>

<span data-ttu-id="7b081-405">**命令 3**</span><span class="sxs-lookup"><span data-stu-id="7b081-405">**Command #3**</span></span>

> <span data-ttu-id="7b081-406">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b081-406">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="7b081-407">輸入：Azure AD 租用戶的全域系統管理員使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="7b081-407">Input: Global admin username and password for your Azure AD tenant</span></span>

<span data-ttu-id="7b081-408">**命令 4**</span><span class="sxs-lookup"><span data-stu-id="7b081-408">**Command #4**</span></span>

> <span data-ttu-id="7b081-409">Get-AdSyncAgentProvisioningTasks</span><span class="sxs-lookup"><span data-stu-id="7b081-409">Get-AdSyncAgentProvisioningTasks</span></span>

* <span data-ttu-id="7b081-410">動作：確認已傳回資料。</span><span class="sxs-lookup"><span data-stu-id="7b081-410">Action: Confirm data is returned.</span></span> <span data-ttu-id="7b081-411">此命令會自動探索 Azure AD 租用戶中的 Workday 佈建應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b081-411">This command automatically discovers Workday provisioning apps in your Azure AD tenant.</span></span> <span data-ttu-id="7b081-412">範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="7b081-412">Example output:</span></span>

> <span data-ttu-id="7b081-413">名稱：我的 AD 樹系</span><span class="sxs-lookup"><span data-stu-id="7b081-413">Name          : My AD Forest</span></span>
>
> <span data-ttu-id="7b081-414">已啟用：True</span><span class="sxs-lookup"><span data-stu-id="7b081-414">Enabled       : True</span></span>
>
> <span data-ttu-id="7b081-415">DirectoryName：mydomain.contoso.com</span><span class="sxs-lookup"><span data-stu-id="7b081-415">DirectoryName : mydomain.contoso.com</span></span>
>
> <span data-ttu-id="7b081-416">已認證：False</span><span class="sxs-lookup"><span data-stu-id="7b081-416">Credentialed  : False</span></span>
>
> <span data-ttu-id="7b081-417">識別碼：WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span><span class="sxs-lookup"><span data-stu-id="7b081-417">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span></span>

<span data-ttu-id="7b081-418">**命令 5**</span><span class="sxs-lookup"><span data-stu-id="7b081-418">**Command #5**</span></span>

> <span data-ttu-id="7b081-419">Start-AdSyncAgentSynchronization -Automatic</span><span class="sxs-lookup"><span data-stu-id="7b081-419">Start-AdSyncAgentSynchronization -Automatic</span></span>

<span data-ttu-id="7b081-420">**命令 6**</span><span class="sxs-lookup"><span data-stu-id="7b081-420">**Command #6**</span></span>

> <span data-ttu-id="7b081-421">net stop aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="7b081-421">net stop aadsyncagent</span></span>

<span data-ttu-id="7b081-422">**命令 7**</span><span class="sxs-lookup"><span data-stu-id="7b081-422">**Command #7**</span></span>

> <span data-ttu-id="7b081-423">net start aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="7b081-423">net start aadsyncagent</span></span>

### <a name="part-4-start-the-service"></a><span data-ttu-id="7b081-424">第 4 部分：啟動服務</span><span class="sxs-lookup"><span data-stu-id="7b081-424">Part 4: Start the service</span></span>
<span data-ttu-id="7b081-425">完成第 1-3 部分之後，您可以在 Azure 管理入口網站中重新啟動佈建服務。</span><span class="sxs-lookup"><span data-stu-id="7b081-425">Once parts 1-3 have been completed, you can start the provisioning service back in the Azure Management Portal.</span></span>

1.  <span data-ttu-id="7b081-426">在 [佈建] 索引標籤中，將 [佈建狀態] 設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="7b081-426">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="7b081-427">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7b081-427">Click **Save**.</span></span>

3. <span data-ttu-id="7b081-428">這會啟動初始同步，取決於 Workday 中的使用者人數，其可能要花費數小時。</span><span class="sxs-lookup"><span data-stu-id="7b081-428">This will start the initial sync, which can take a variable number of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="7b081-429">您可以在 [稽核記錄] 索引標籤中檢視個別同步事件 (例如，正在 Workday 外讀取哪些使用者，然後接著新增或更新至 Active Directory)。</span><span class="sxs-lookup"><span data-stu-id="7b081-429">Individual sync events such as what users are being read out of Workday, and then subsequently added or updated to Active Directory, can be viewed in the **Audit Logs** tab.</span></span> <span data-ttu-id="7b081-430">**[請參閱佈建報告指南，瞭解有關如何讀取稽核記錄的詳細指示](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="7b081-430">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5.  <span data-ttu-id="7b081-431">代理程式電腦上的 Windows 應用程式記錄檔將會顯示透過代理程式執行的所有作業。</span><span class="sxs-lookup"><span data-stu-id="7b081-431">The Windows Application log on the agent machine will show all operations performed via the agent.</span></span>

6. <span data-ttu-id="7b081-432">完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7b081-432">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-to-azure-active-directory"></a><span data-ttu-id="7b081-434">設定將使用者佈建至 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b081-434">Configuring user provisioning to Azure Active Directory</span></span>
<span data-ttu-id="7b081-435">設定 Azure Active Directory 佈建的方法將取決於佈建需求，如下表所述。</span><span class="sxs-lookup"><span data-stu-id="7b081-435">How you configure provisioning to Azure Active Directory will depend on your provisioning requirements, as detailed in the table below.</span></span>

| <span data-ttu-id="7b081-436">案例</span><span class="sxs-lookup"><span data-stu-id="7b081-436">Scenario</span></span> | <span data-ttu-id="7b081-437">方案</span><span class="sxs-lookup"><span data-stu-id="7b081-437">Solution</span></span> |
| -------- | -------- |
| <span data-ttu-id="7b081-438">**需要佈建至 Active Directory 和 Azure AD 的使用者**</span><span class="sxs-lookup"><span data-stu-id="7b081-438">**Users need to be provisioned to Active Directory and Azure AD**</span></span> | <span data-ttu-id="7b081-439">使用 **[AAD Connect](connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="7b081-439">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="7b081-440">**只需要佈建至 Active Directory 的使用者**</span><span class="sxs-lookup"><span data-stu-id="7b081-440">**Users need to be provisioned to Active Directory only**</span></span> | <span data-ttu-id="7b081-441">使用 **[AAD Connect](connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="7b081-441">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="7b081-442">**只需要佈建至 Azure AD 的使用者 (僅限雲端)**</span><span class="sxs-lookup"><span data-stu-id="7b081-442">**Users need to be provisioned to Azure AD only (cloud only)**</span></span> | <span data-ttu-id="7b081-443">使用應用程式庫中的 **Workday to Azure Active Directory Provisioning** 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b081-443">Use the **Workday to Azure Active Directory provisioning** app in the app gallery</span></span> |

<span data-ttu-id="7b081-444">如需有關設定 Azure AD Connect 的指示，請參閱 [Azure AD Connect 文件](connect/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="7b081-444">For instructions on setting up Azure AD Connect, see the [Azure AD Connect documentation](connect/active-directory-aadconnect.md).</span></span>

<span data-ttu-id="7b081-445">下列各節說明如何設定 Workday 與 Azure AD 之間的連接以佈建僅限雲端使用者。</span><span class="sxs-lookup"><span data-stu-id="7b081-445">The following sections describe setting up a connection between Workday and Azure AD to provision cloud-only users.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b081-446">如果您擁有需要佈建至 Azure AD 的僅限雲端使用者且沒有內部部署 Active Directory，請僅遵循下列程序。</span><span class="sxs-lookup"><span data-stu-id="7b081-446">Only follow the procedure below if you have cloud-only users that need to be provisioned to Azure AD and not on-premises Active Directory.</span></span>

### <a name="part-1-adding-the-azure-ad-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="7b081-447">第 1 部分：新增 Azure AD 佈建連接器應用程式和建立 Workday 連接</span><span class="sxs-lookup"><span data-stu-id="7b081-447">Part 1: Adding the Azure AD provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="7b081-448">**若要針對僅限雲端使用者設定 Workday 至 Azure Active Directory 佈建：**</span><span class="sxs-lookup"><span data-stu-id="7b081-448">**To configure Workday to Azure Active Directory provisioning for cloud-only users:**</span></span>

1.  <span data-ttu-id="7b081-449">移至 <https://portal.azure.com>。</span><span class="sxs-lookup"><span data-stu-id="7b081-449">Go to <https://portal.azure.com>.</span></span>

2.  <span data-ttu-id="7b081-450">在左側導覽列中，選取 [Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="7b081-450">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="7b081-451">依序選取 [企業應用程式] 和 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7b081-451">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="7b081-452">選取 [新增應用程式]，然後選取 [全部] 類別。</span><span class="sxs-lookup"><span data-stu-id="7b081-452">Select **Add an application**, and then select the **All** category.</span></span>

5.  <span data-ttu-id="7b081-453">搜尋 **Workday to Azure AD Provisioning**，並從資源庫新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b081-453">Search for **Workday to Azure AD provisioning**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="7b081-454">新增應用程式並顯示應用程式詳細資料畫面之後，請選取 [佈建]</span><span class="sxs-lookup"><span data-stu-id="7b081-454">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="7b081-455">將 [佈建模式] 變更為 [自動]</span><span class="sxs-lookup"><span data-stu-id="7b081-455">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="7b081-456">完成 [系統管理員認證] 區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7b081-456">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="7b081-457">**系統管理員使用者名稱** – 輸入 Workday 整合系統帳戶的使用者名稱，並附加租用戶網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7b081-457">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="7b081-458">其應該類似於：username@contoso4</span><span class="sxs-lookup"><span data-stu-id="7b081-458">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="7b081-459">**系統管理員密碼 –** 輸入 Workday 整合系統帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="7b081-459">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="7b081-460">**租用戶 URL –** 輸入租用戶 Workday Web 服務端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="7b081-460">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="7b081-461">其應該類似於：https://wd3-impl-services1.workday.com/ccx/service/contoso4，其中請將 contoso4 取代為正確的租用戶名稱，並將 wd3-impl 取代為正確的環境字串 (如有必要)。</span><span class="sxs-lookup"><span data-stu-id="7b081-461">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string (if necessary).</span></span>

   * <span data-ttu-id="7b081-462">**電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7b081-462">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="7b081-463">按一下 [測試連線] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b081-463">Click the **Test Connection** button.</span></span>

   * <span data-ttu-id="7b081-464">如果連線測試成功，請按一下頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b081-464">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="7b081-465">如果失敗，請仔細檢查 Workday URL 和認證在 Workday 中是否有效。</span><span class="sxs-lookup"><span data-stu-id="7b081-465">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="7b081-466">第 2 部分：設定屬性對應</span><span class="sxs-lookup"><span data-stu-id="7b081-466">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="7b081-467">在本節中，您會針對僅限雲端使用者設定使用者資料從 Workday 流動至 Azure Active Directory 的方式。</span><span class="sxs-lookup"><span data-stu-id="7b081-467">In this section, you will configure how user data flows from Workday to Azure Active Directory for cloud-only users.</span></span>

1.  <span data-ttu-id="7b081-468">在 [佈建] 索引標籤的 [對應] 下，按一下 [將人員同步至 Azure AD]。</span><span class="sxs-lookup"><span data-stu-id="7b081-468">On the Provisioning tab under **Mappings**, click **Synchronize Workers to Azure AD**.</span></span>

2.   <span data-ttu-id="7b081-469">在 [來源物件範圍] 欄位中，您可以透過定義一組屬性型篩選，選取應該佈建至 Azure AD 的 Workday 使用者集合範圍。</span><span class="sxs-lookup"><span data-stu-id="7b081-469">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to Azure AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="7b081-470">預設範圍是「Workday 中的所有使用者」。</span><span class="sxs-lookup"><span data-stu-id="7b081-470">The default scope is “all users in Workday”.</span></span> <span data-ttu-id="7b081-471">範例篩選：</span><span class="sxs-lookup"><span data-stu-id="7b081-471">Example filters:</span></span>

   * <span data-ttu-id="7b081-472">範例：人員識別碼介於 1000000 到 2000000 之間的使用者範圍</span><span class="sxs-lookup"><span data-stu-id="7b081-472">Example: Scope to users with Worker IDs between 1000000 and   2000000</span></span>

      * <span data-ttu-id="7b081-473">屬性：WorkerID</span><span class="sxs-lookup"><span data-stu-id="7b081-473">Attribute: WorkerID</span></span>

      * <span data-ttu-id="7b081-474">運算子：REGEX Match</span><span class="sxs-lookup"><span data-stu-id="7b081-474">Operator: REGEX Match</span></span>

      * <span data-ttu-id="7b081-475">值：(1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="7b081-475">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="7b081-476">範例：僅約聘人員和非正式員工</span><span class="sxs-lookup"><span data-stu-id="7b081-476">Example: Only contingent workers and not regular employees</span></span>

      * <span data-ttu-id="7b081-477">屬性：ContingentID</span><span class="sxs-lookup"><span data-stu-id="7b081-477">Attribute: ContingentID</span></span>

      * <span data-ttu-id="7b081-478">運算子：IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="7b081-478">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="7b081-479">在 [目標物件動作] 欄位中，您可以全域篩選允許在 Azure AD 上執行哪些動作。</span><span class="sxs-lookup"><span data-stu-id="7b081-479">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Azure AD.</span></span> <span data-ttu-id="7b081-480">最常見的動作是 [建立] 和 [更新]。</span><span class="sxs-lookup"><span data-stu-id="7b081-480">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="7b081-481">在 [屬性對應] 區段中，您可以定義個別 Workday 屬性如何對應至 Active Directory 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-481">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span></span>

5. <span data-ttu-id="7b081-482">按一下現有的屬性對應以進行更新，或按一下畫面底端的 [新增新對應] 以新增新對應。</span><span class="sxs-lookup"><span data-stu-id="7b081-482">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span></span> <span data-ttu-id="7b081-483">個別屬性對應支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="7b081-483">An individual attribute mapping supports these properties:</span></span>

   * <span data-ttu-id="7b081-484">**對應類型**</span><span class="sxs-lookup"><span data-stu-id="7b081-484">**Mapping Type**</span></span>

      * <span data-ttu-id="7b081-485">**直接** – 將 Workday 屬性的值寫入 AD 屬性，且不進行變更</span><span class="sxs-lookup"><span data-stu-id="7b081-485">**Direct** – Writes the value of the Workday attribute         to the AD attribute, with no changes</span></span>

      * <span data-ttu-id="7b081-486">**常數** - 將靜態的常數字串值寫入 AD 屬性</span><span class="sxs-lookup"><span data-stu-id="7b081-486">**Constant** - Write a static, constant string value to         the AD attribute</span></span>

      * <span data-ttu-id="7b081-487">**運算式** – 可讓您根據一或多個 Workday 屬性，將自訂值寫入 AD 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-487">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="7b081-488">[如需詳細資訊，請參閱這篇有關運算式的文章](active-directory-saas-writing-expressions-for-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="7b081-488">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

   * <span data-ttu-id="7b081-489">**來源屬性** - 來自 Workday 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-489">**Source attribute** - The user attribute from Workday.</span></span>

   * <span data-ttu-id="7b081-490">**預設值** – 選用。</span><span class="sxs-lookup"><span data-stu-id="7b081-490">**Default value** – Optional.</span></span> <span data-ttu-id="7b081-491">如果來源屬性具有空值，則對應將會改為寫入此值。</span><span class="sxs-lookup"><span data-stu-id="7b081-491">If the source attribute has an empty value, the mapping will write this value instead.</span></span>
            <span data-ttu-id="7b081-492">最常見的設定是將其保留空白。</span><span class="sxs-lookup"><span data-stu-id="7b081-492">Most common configuration is to leave this blank.</span></span>

   * <span data-ttu-id="7b081-493">**目標屬性** – Azure AD 中的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-493">**Target attribute** – The user attribute in Azure AD.</span></span>

   * <span data-ttu-id="7b081-494">**使用此屬性比對物件** – 是否應該將此對應用於唯一識別 Workday 與 Azure AD 之間的使用者。</span><span class="sxs-lookup"><span data-stu-id="7b081-494">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Azure AD.</span></span> <span data-ttu-id="7b081-495">此設定通常會設定於 Workday 的 [人員識別碼] 欄位，且通常會在 Azure AD 中對應至員工識別碼屬性 (新) 或擴充屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-495">This is typically set on the Worker ID field for Workday, which is typically mapped to the Employee ID attribute (new) or an extension attribute in Azure AD.</span></span>

   * <span data-ttu-id="7b081-496">**比對優先順序** – 您可以設定多個比對屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-496">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="7b081-497">具有多個屬性時，系統會以此欄位定義的順序進行評估。</span><span class="sxs-lookup"><span data-stu-id="7b081-497">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="7b081-498">只要找到相符項目，便不會評估進一步比對屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-498">As soon as a match is found, no further matching attributes are evaluated.</span></span>

   * <span data-ttu-id="7b081-499">**套用此對應**</span><span class="sxs-lookup"><span data-stu-id="7b081-499">**Apply this mapping**</span></span>

     * <span data-ttu-id="7b081-500">**一律** – 將此對應套用於使用者建立和更新動作</span><span class="sxs-lookup"><span data-stu-id="7b081-500">**Always** – Apply this mapping on both user creation          and update actions</span></span>

     * <span data-ttu-id="7b081-501">**僅限建立期間** - 僅將此對應套用於使用者建立動作</span><span class="sxs-lookup"><span data-stu-id="7b081-501">**Only during creation** - Apply this mapping only on          user creation actions</span></span>

6. <span data-ttu-id="7b081-502">若要儲存您的對應，請按一下 [屬性對應] 區段頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7b081-502">To save your mappings, click **Save** at the top of the      Attribute Mapping section.</span></span>

### <a name="part-3-start-the-service"></a><span data-ttu-id="7b081-503">第 3 部分：啟動服務</span><span class="sxs-lookup"><span data-stu-id="7b081-503">Part 3: Start the service</span></span>
<span data-ttu-id="7b081-504">完成第 1-2 部分之後，您可以啟動佈建服務。</span><span class="sxs-lookup"><span data-stu-id="7b081-504">Once parts 1-2 have been completed, you can start the provisioning service.</span></span>

1.  <span data-ttu-id="7b081-505">在 [佈建] 索引標籤中，將 [佈建狀態] 設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="7b081-505">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="7b081-506">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7b081-506">Click **Save**.</span></span>

3. <span data-ttu-id="7b081-507">這會啟動初始同步，取決於 Workday 中的使用者人數，其可能要花費數小時。</span><span class="sxs-lookup"><span data-stu-id="7b081-507">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="7b081-508">您可以在 [稽核記錄] 索引標籤中檢視個別同步事件。</span><span class="sxs-lookup"><span data-stu-id="7b081-508">Individual sync events can be viewed in the **Audit Logs** tab.</span></span> <span data-ttu-id="7b081-509">**[請參閱佈建報告指南，瞭解有關如何讀取稽核記錄的詳細指示](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="7b081-509">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="7b081-510">完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7b081-510">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>


## <a name="configuring-writeback-of-email-addresses-to-workday"></a><span data-ttu-id="7b081-511">設定將電子郵件地址回寫至 Workday</span><span class="sxs-lookup"><span data-stu-id="7b081-511">Configuring writeback of email addresses to Workday</span></span>
<span data-ttu-id="7b081-512">請遵循下列指示來設定將使用者電子郵件地址從 Azure Active Directory 回寫至 Workday。</span><span class="sxs-lookup"><span data-stu-id="7b081-512">Follow these instructions to configure writeback of user email addresses from Azure Active Directory to Workday.</span></span>

### <a name="part-1-adding-the-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="7b081-513">第 1 部分：新增佈建連接器應用程式和建立 Workday 連接</span><span class="sxs-lookup"><span data-stu-id="7b081-513">Part 1: Adding the provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="7b081-514">**若要設定 Workday 至 Active Directory 佈建：**</span><span class="sxs-lookup"><span data-stu-id="7b081-514">**To configure Workday to Active Directory provisioning:**</span></span>

1.  <span data-ttu-id="7b081-515">移至 <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="7b081-515">Go to <https://portal.azure.com></span></span>

2.  <span data-ttu-id="7b081-516">在左側導覽列中，選取 [Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="7b081-516">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="7b081-517">依序選取 [企業應用程式] 和 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7b081-517">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="7b081-518">選取 [新增應用程式]，然後選取 [全部] 類別。</span><span class="sxs-lookup"><span data-stu-id="7b081-518">Select **Add an application**, then select the **All** category.</span></span>

5.  <span data-ttu-id="7b081-519">搜尋 **Workday Writeback**，並從資源庫新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b081-519">Search for **Workday Writeback**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="7b081-520">新增應用程式並顯示應用程式詳細資料畫面之後，請選取 [佈建]</span><span class="sxs-lookup"><span data-stu-id="7b081-520">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="7b081-521">將 [佈建模式] 變更為 [自動]</span><span class="sxs-lookup"><span data-stu-id="7b081-521">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="7b081-522">完成 [系統管理員認證] 區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7b081-522">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="7b081-523">**系統管理員使用者名稱** – 輸入 Workday 整合系統帳戶的使用者名稱，並附加租用戶網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7b081-523">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="7b081-524">其應該類似於：username@contoso4</span><span class="sxs-lookup"><span data-stu-id="7b081-524">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="7b081-525">**系統管理員密碼 –** 輸入 Workday 整合系統帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="7b081-525">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="7b081-526">**租用戶 URL –** 輸入租用戶 Workday Web 服務端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="7b081-526">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="7b081-527">其應該類似於：https://wd3-impl-services1.workday.com/ccx/service/contoso4，其中請將 contoso4 取代為正確的租用戶名稱，並將 wd3-impl 取代為正確的環境字串 (如有必要)。</span><span class="sxs-lookup"><span data-stu-id="7b081-527">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string (if necessary).</span></span>

   * <span data-ttu-id="7b081-528">**電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7b081-528">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="7b081-529">按一下 [測試連線] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b081-529">Click the **Test Connection** button.</span></span> <span data-ttu-id="7b081-530">如果連線測試成功，請按一下頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b081-530">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="7b081-531">如果失敗，請仔細檢查 Workday URL 和認證在 Workday 中是否有效。</span><span class="sxs-lookup"><span data-stu-id="7b081-531">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="7b081-532">第 2 部分：設定屬性對應</span><span class="sxs-lookup"><span data-stu-id="7b081-532">Part 2: Configure attribute mappings</span></span> 


<span data-ttu-id="7b081-533">在本節中，您會設定使用者資料從 Workday 流動至 Active Directory 的方式。</span><span class="sxs-lookup"><span data-stu-id="7b081-533">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="7b081-534">在 [佈建] 索引標籤的 [對應] 下，按一下 [將 Azure AD 使用者同步至 Workday]。</span><span class="sxs-lookup"><span data-stu-id="7b081-534">On the Provisioning tab under **Mappings**, click **Synchronize Azure AD Users to Workday**.</span></span>

2.  <span data-ttu-id="7b081-535">在 [來源物件範圍] 欄位中，您可以選擇性地篩選應該將電子郵件地址寫回至 Workday 的 Azure Active Directory 使用者集合。</span><span class="sxs-lookup"><span data-stu-id="7b081-535">In the **Source Object Scope** field, you can optionally filter which sets of users in Azure Active Directory should have their email addresses written back to Workday.</span></span> <span data-ttu-id="7b081-536">預設範圍是「Azure AD 中的所有使用者」。</span><span class="sxs-lookup"><span data-stu-id="7b081-536">The default scope is “all users in Azure AD”.</span></span> 

3.  <span data-ttu-id="7b081-537">在 [屬性對應] 區段中，您可以定義個別 Workday 屬性如何對應至 Active Directory 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b081-537">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span></span> <span data-ttu-id="7b081-538">根據預設，存在電子郵件地址的對應。</span><span class="sxs-lookup"><span data-stu-id="7b081-538">There is a mapping for the email address by default.</span></span> <span data-ttu-id="7b081-539">不過，您必須更新比對識別碼以在 Azure AD 中比對使用者及其在 Workday 中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="7b081-539">However, the matching ID must be updated to match users in Azure AD with their corresponding entries in Workday.</span></span> <span data-ttu-id="7b081-540">常用的比對方法是將 Workday 人員識別碼或員工識別碼同步至 Azure AD 中的 extensionAttribute1-15，然後在 Azure AD 中使用此屬性再次比對 Workday 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7b081-540">A popular matching method is to synchronize the Workday worker ID or employee ID to extensionAttribute1-15 in Azure AD, and then use this attribute in Azure AD to match users back in Workday.</span></span>

4.  <span data-ttu-id="7b081-541">若要儲存您的對應，請按一下 [屬性對應] 區段頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7b081-541">To save your mappings, click **Save** at the top of the Attribute Mapping section.</span></span>

### <a name="part-3-start-the-service"></a><span data-ttu-id="7b081-542">第 3 部分：啟動服務</span><span class="sxs-lookup"><span data-stu-id="7b081-542">Part 3: Start the service</span></span>
<span data-ttu-id="7b081-543">完成第 1-2 部分之後，您可以啟動佈建服務。</span><span class="sxs-lookup"><span data-stu-id="7b081-543">Once parts 1-2 have been completed, you can start the provisioning service.</span></span>

1.  <span data-ttu-id="7b081-544">在 [佈建] 索引標籤中，將 [佈建狀態] 設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="7b081-544">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="7b081-545">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7b081-545">Click **Save**.</span></span>

3. <span data-ttu-id="7b081-546">這會啟動初始同步，取決於 Workday 中的使用者人數，其可能要花費數小時。</span><span class="sxs-lookup"><span data-stu-id="7b081-546">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="7b081-547">您可以在 [稽核記錄] 索引標籤中檢視個別同步事件。</span><span class="sxs-lookup"><span data-stu-id="7b081-547">Individual sync events can be viewed in the **Audit Logs** tab.</span></span> <span data-ttu-id="7b081-548">**[請參閱佈建報告指南，瞭解有關如何讀取稽核記錄的詳細指示](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="7b081-548">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="7b081-549">完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7b081-549">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7b081-550">已知問題</span><span class="sxs-lookup"><span data-stu-id="7b081-550">Known issues</span></span>

* <span data-ttu-id="7b081-551">**歐洲地區設定中的稽核記錄** - 發布此技術預覽版本後，已存在[稽核記錄](active-directory-saas-provisioning-reporting.md)的已知問題，如果 Azure AD 租用戶位於歐洲資料中心，則 Workday 連接器應用程式不會顯示於 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7b081-551">**Audit logs in European locales** - As of the release of this technical preview, there is a known issue with the [audit logs](active-directory-saas-provisioning-reporting.md) for the Workday connector apps not appearing in the [Azure portal](https://portal.azure.com) if the Azure AD tenant resides in a European data center.</span></span> <span data-ttu-id="7b081-552">我們即將推出此問題的修正。</span><span class="sxs-lookup"><span data-stu-id="7b081-552">A fix for this issue is forthcoming.</span></span> <span data-ttu-id="7b081-553">請於近期再次檢查此空間以取得更新。</span><span class="sxs-lookup"><span data-stu-id="7b081-553">Please check this space again in the near future for updates.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b081-554">其他資源</span><span class="sxs-lookup"><span data-stu-id="7b081-554">Additional resources</span></span>
* [<span data-ttu-id="7b081-555">教學課程：設定 Workday 與 Azure Active Directory 之間的單一登入</span><span class="sxs-lookup"><span data-stu-id="7b081-555">Tutorial: Configuring single sign-on between Workday and Azure Active Directory</span></span>](active-directory-saas-workday-tutorial.md)
* [<span data-ttu-id="7b081-556">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7b081-556">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b081-557">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7b081-557">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="7b081-558">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b081-558">Next steps</span></span>

* [<span data-ttu-id="7b081-559">瞭解如何針對佈建活動檢閱記錄和取得報告</span><span class="sxs-lookup"><span data-stu-id="7b081-559">Learn how to review logs and get reports on provisioning activity</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
