---
title: "適用於 Azure AD Join 的使用案例和部署考量| Microsoft Docs"
description: "說明系統管理員如何為其使用者 (員工、學生、其他使用者) 設定 Azure AD Join。 其中也會討論使用 Azure AD Join 時出現的各種真實案例。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: fd0aab1a14bbd324e734e5efe8fe101e8a8dfefa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="00e3b-104">適用於 Azure AD Join 的使用案例和部署考量</span><span class="sxs-lookup"><span data-stu-id="00e3b-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="00e3b-105">適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="00e3b-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-the-cloud"></a><span data-ttu-id="00e3b-106">案例 1：主要位於雲端的企業</span><span class="sxs-lookup"><span data-stu-id="00e3b-106">Scenario 1: Businesses largely in the cloud</span></span>
<span data-ttu-id="00e3b-107">如果您目前是在雲端為貴公司操作和管理身分識別，或者即將轉向雲端，則可從 Azure Active Directory Join (Azure AD Join) 獲益。</span><span class="sxs-lookup"><span data-stu-id="00e3b-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon.</span></span> <span data-ttu-id="00e3b-108">您可以使用在 Azure AD 中建立的帳戶來登入 Windows 10。</span><span class="sxs-lookup"><span data-stu-id="00e3b-108">You can use an account that you have created in Azure AD to sign in to Windows 10.</span></span> <span data-ttu-id="00e3b-109">透過[初次執行體驗 (FRX) 程序](active-directory-azureadjoin-user-frx.md)或從[設定功能表](active-directory-azureadjoin-user-upgrade.md)加入 Azure AD，您的使用者可將其電腦加入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="00e3b-109">Through [the first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [the settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines to Azure AD.</span></span>  <span data-ttu-id="00e3b-110">您的使用者也可以在瀏覽器或 Office 應用程式中，享受經由單一登入 (SSO) 存取雲端資源，例如 Office 365。</span><span class="sxs-lookup"><span data-stu-id="00e3b-110">Your users can also enjoy single sign-on (SSO) access to  cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="00e3b-111">案例 2：教育機構</span><span class="sxs-lookup"><span data-stu-id="00e3b-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="00e3b-112">教育機構通常有兩種使用者類型：教職員和學生。</span><span class="sxs-lookup"><span data-stu-id="00e3b-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="00e3b-113">教職成員會被視為組織中的長期成員。</span><span class="sxs-lookup"><span data-stu-id="00e3b-113">Faculty members are considered longer-term members of the organization.</span></span> <span data-ttu-id="00e3b-114">為他們建立內部部署帳戶是比較好的做法。</span><span class="sxs-lookup"><span data-stu-id="00e3b-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="00e3b-115">但學生是組織中較短期的成員，因而可將其帳戶放在 Azure AD 中管理。</span><span class="sxs-lookup"><span data-stu-id="00e3b-115">But students are shorter-term members of the organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="00e3b-116">這表示可以將目錄範圍推送至雲端，而不是儲存在內部部署</span><span class="sxs-lookup"><span data-stu-id="00e3b-116">This means that directory scale can be pushed to the cloud instead of being stored on-premises.</span></span> <span data-ttu-id="00e3b-117">這也表示學生可以使用其 Azure AD 帳戶登入 Windows，並在 Office 應用程式中存取 Office 365 資源。</span><span class="sxs-lookup"><span data-stu-id="00e3b-117">It also means that students  will be able to sign in to Windows with their Azure AD accounts and get access to Office 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="00e3b-118">案例 3：零售業</span><span class="sxs-lookup"><span data-stu-id="00e3b-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="00e3b-119">零售業擁有季節性工作者和長期員工。</span><span class="sxs-lookup"><span data-stu-id="00e3b-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="00e3b-120">您通常會為較長期的全職員工建立內部部署帳戶，讓他們能夠使用已加入網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="00e3b-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="00e3b-121">但季節性工作者是組織中較短期的成員，因而適合使用可更輕易四處移動使用者授權的帳戶來管理。</span><span class="sxs-lookup"><span data-stu-id="00e3b-121">But seasonal workers are shorter-term members of the organization, and it's desirable to manage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="00e3b-122">當您在具有 Office 365 授權的雲端中建立這些使用者帳戶時，這些使用者能夠因為使用 Azure AD 帳戶登入 Windows 和 Office 應用程式而獲益，同時在他們離開公司之後對於他們的授權保有更多彈性。</span><span class="sxs-lookup"><span data-stu-id="00e3b-122">When you create their user accounts in the cloud with Office 365 licenses, these users get the benefits of signing in to Windows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="00e3b-123">案例 4：其他案例</span><span class="sxs-lookup"><span data-stu-id="00e3b-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="00e3b-124">除了先前討論的案例，您還可以藉由讓使用者將其裝置加入 Azure AD，因為簡化的加入體驗、有效率的裝置管理、自動的行動裝置管理註冊，以及單一登入 Azure AD 和內部部署資源而獲益。</span><span class="sxs-lookup"><span data-stu-id="00e3b-124">Along with the benefits discussed earlier, you  benefit from having your users join their devices to Azure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on to Azure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="00e3b-125">適用於 Azure AD Join 的部署考量</span><span class="sxs-lookup"><span data-stu-id="00e3b-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-to-join-a-company-owned-device-directly-to-azure-ad"></a><span data-ttu-id="00e3b-126">讓使用者可將公司擁有的裝置直接加入 Azure AD</span><span class="sxs-lookup"><span data-stu-id="00e3b-126">Enable your users to join a company-owned device directly to Azure AD</span></span>
<span data-ttu-id="00e3b-127">企業可以為合作夥伴公司和組織提供僅限雲端的帳戶。</span><span class="sxs-lookup"><span data-stu-id="00e3b-127">Enterprises can provide cloud-only accounts to partner companies and organizations.</span></span> <span data-ttu-id="00e3b-128">這些合作夥伴之後就能使用單一登入，輕易地存取公司的應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="00e3b-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="00e3b-129">此案例適用於主要存取雲端資源的使用者，例如 Office 365 或 SaaS 應用程式，而這類資源會依賴 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="00e3b-129">This scenario is applicable to users who access resources primarily in the cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="00e3b-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="00e3b-130">Prerequisites</span></span>
<span data-ttu-id="00e3b-131">**在企業層級 (系統管理員)**</span><span class="sxs-lookup"><span data-stu-id="00e3b-131">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="00e3b-132">Azure 訂用帳戶搭配 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00e3b-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="00e3b-133">**在使用者層級**</span><span class="sxs-lookup"><span data-stu-id="00e3b-133">**At the user level**</span></span>

* <span data-ttu-id="00e3b-134">Windows 10 (專業版和企業版)</span><span class="sxs-lookup"><span data-stu-id="00e3b-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="00e3b-135">系統管理員工作</span><span class="sxs-lookup"><span data-stu-id="00e3b-135">Administrator tasks</span></span>
* [<span data-ttu-id="00e3b-136">設定裝置註冊</span><span class="sxs-lookup"><span data-stu-id="00e3b-136">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="00e3b-137">使用者工作</span><span class="sxs-lookup"><span data-stu-id="00e3b-137">User tasks</span></span>
* [<span data-ttu-id="00e3b-138">設定期間使用 Azure AD 設定新的 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="00e3b-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md)
* [<span data-ttu-id="00e3b-139">從設定功能表使用 Azure AD 設定 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="00e3b-139">Set up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="00e3b-140">將個人的 Windows 10 裝置加入您的組織</span><span class="sxs-lookup"><span data-stu-id="00e3b-140">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="00e3b-141">在組織中針對 Windows 10 啟用 BYOD</span><span class="sxs-lookup"><span data-stu-id="00e3b-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="00e3b-142">您可以設定使用者和員工，使用其個人的 Windows 裝置 (BYOD) 來存取公司應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="00e3b-142">You can set up your users and employees to use their personal Windows devices (BYOD) to access company apps and resources.</span></span> <span data-ttu-id="00e3b-143">您的使用者可將其 Azure AD 帳戶 (工作或學校帳戶) 新增到個人的 Windows 裝置，以安全且相容的方式來存取資源。</span><span class="sxs-lookup"><span data-stu-id="00e3b-143">Your users can add their Azure AD accounts (work or school accounts) to a personal Windows device to access resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="00e3b-144">必要條件</span><span class="sxs-lookup"><span data-stu-id="00e3b-144">Prerequisites</span></span>
<span data-ttu-id="00e3b-145">**在企業層級 (系統管理員)**</span><span class="sxs-lookup"><span data-stu-id="00e3b-145">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="00e3b-146">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="00e3b-146">Azure AD subscription</span></span>

<span data-ttu-id="00e3b-147">**在使用者層級**</span><span class="sxs-lookup"><span data-stu-id="00e3b-147">**At the user level**</span></span>

* <span data-ttu-id="00e3b-148">Windows 10 (專業版和企業版)</span><span class="sxs-lookup"><span data-stu-id="00e3b-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="00e3b-149">系統管理員工作</span><span class="sxs-lookup"><span data-stu-id="00e3b-149">Administrator tasks</span></span>
* [<span data-ttu-id="00e3b-150">設定裝置註冊</span><span class="sxs-lookup"><span data-stu-id="00e3b-150">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="00e3b-151">使用者工作</span><span class="sxs-lookup"><span data-stu-id="00e3b-151">User tasks</span></span>
* [<span data-ttu-id="00e3b-152">將個人的 Windows 10 裝置加入您的組織</span><span class="sxs-lookup"><span data-stu-id="00e3b-152">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a><span data-ttu-id="00e3b-153">其他資訊</span><span class="sxs-lookup"><span data-stu-id="00e3b-153">Additional information</span></span>
* [<span data-ttu-id="00e3b-154">適合企業使用的 Windows 10：使用裝置工作的方式</span><span class="sxs-lookup"><span data-stu-id="00e3b-154">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="00e3b-155">透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能</span><span class="sxs-lookup"><span data-stu-id="00e3b-155">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="00e3b-156">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="00e3b-156">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="00e3b-157">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="00e3b-157">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="00e3b-158">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="00e3b-158">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="00e3b-159">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="00e3b-159">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

