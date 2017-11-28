---
title: "aaaUsage 案例和 Azure AD Join 的部署考量 |Microsoft 文件"
description: "說明系統管理員如何為其使用者 (員工、學生、其他使用者) 設定 Azure AD Join。 它也會討論使用 Azure AD Join hello 不同真實世界的案例。"
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
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="97e58-104">適用於 Azure AD Join 的使用案例和部署考量</span><span class="sxs-lookup"><span data-stu-id="97e58-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="97e58-105">適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="97e58-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a><span data-ttu-id="97e58-106">Hello 定域機組中大部分的案例 1： 企業</span><span class="sxs-lookup"><span data-stu-id="97e58-106">Scenario 1: Businesses largely in hello cloud</span></span>
<span data-ttu-id="97e58-107">Azure Active Directory Join (Azure AD Join) 可以受益您您目前操作和管理您的業務 hello 雲端中的身分識別或要移動 toohello 雲端推出。</span><span class="sxs-lookup"><span data-stu-id="97e58-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in hello cloud or are moving toohello cloud soon.</span></span> <span data-ttu-id="97e58-108">您可以使用您已在 Azure AD toosign tooWindows 10 中建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="97e58-108">You can use an account that you have created in Azure AD toosign in tooWindows 10.</span></span> <span data-ttu-id="97e58-109">透過[第一次執行體驗 (FRX) 程序的 hello](active-directory-azureadjoin-user-frx.md)，或是從 Azure AD [hello 設定功能表](active-directory-azureadjoin-user-upgrade.md)，您的使用者可以加入其機器 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="97e58-109">Through [hello first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [hello settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines tooAzure AD.</span></span>  <span data-ttu-id="97e58-110">您的使用者也可以享受單一登入 (SSO) 存取太雲端資源，例如 Office 365，在瀏覽器中或在 Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97e58-110">Your users can also enjoy single sign-on (SSO) access too cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="97e58-111">案例 2：教育機構</span><span class="sxs-lookup"><span data-stu-id="97e58-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="97e58-112">教育機構通常有兩種使用者類型：教職員和學生。</span><span class="sxs-lookup"><span data-stu-id="97e58-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="97e58-113">教職員版成員視為長期 hello 組織成員。</span><span class="sxs-lookup"><span data-stu-id="97e58-113">Faculty members are considered longer-term members of hello organization.</span></span> <span data-ttu-id="97e58-114">為他們建立內部部署帳戶是比較好的做法。</span><span class="sxs-lookup"><span data-stu-id="97e58-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="97e58-115">不過學生 shorter-term hello 組織成員，因此可以在 Azure AD 中管理他們的帳戶。</span><span class="sxs-lookup"><span data-stu-id="97e58-115">But students are shorter-term members of hello organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="97e58-116">這表示，而不是儲存在內部 toohello 雲端可以推送目錄小數位數。</span><span class="sxs-lookup"><span data-stu-id="97e58-116">This means that directory scale can be pushed toohello cloud instead of being stored on-premises.</span></span> <span data-ttu-id="97e58-117">這也表示學生會是能在他們的 Azure AD 帳戶與 tooWindows toosign 和 tooOffice 365 資源取得存取權，在 Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97e58-117">It also means that students  will be able toosign in tooWindows with their Azure AD accounts and get access tooOffice 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="97e58-118">案例 3：零售業</span><span class="sxs-lookup"><span data-stu-id="97e58-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="97e58-119">零售業擁有季節性工作者和長期員工。</span><span class="sxs-lookup"><span data-stu-id="97e58-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="97e58-120">您通常會為較長期的全職員工建立內部部署帳戶，讓他們能夠使用已加入網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="97e58-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="97e58-121">但季節性工作者 shorter-term hello 組織的成員，而且希望 toomanage 其中使用者授權可以更輕鬆地移動其帳戶。</span><span class="sxs-lookup"><span data-stu-id="97e58-121">But seasonal workers are shorter-term members of hello organization, and it's desirable toomanage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="97e58-122">當您使用 Office 365 授權的 hello 雲端中建立他們的使用者帳戶時，這些使用者會獲得 hello 優勢登入 tooWindows 和 Azure AD 帳戶，Office 應用程式，當您離開後可維持更大的彈性與使用者的授權。</span><span class="sxs-lookup"><span data-stu-id="97e58-122">When you create their user accounts in hello cloud with Office 365 licenses, these users get hello benefits of signing in tooWindows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="97e58-123">案例 4：其他案例</span><span class="sxs-lookup"><span data-stu-id="97e58-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="97e58-124">先前討論過的 hello 優點，以及您從您的使用者因為簡化聯結的經驗、 有效率的裝置管理、 自動的行動裝置管理註冊和單一登入 tooAzure 加入其裝置 tooAzure AD 中獲益AD 和內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="97e58-124">Along with hello benefits discussed earlier, you  benefit from having your users join their devices tooAzure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on tooAzure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="97e58-125">適用於 Azure AD Join 的部署考量</span><span class="sxs-lookup"><span data-stu-id="97e58-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a><span data-ttu-id="97e58-126">啟用您的使用者 toojoin 公司擁有的裝置直接 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="97e58-126">Enable your users toojoin a company-owned device directly tooAzure AD</span></span>
<span data-ttu-id="97e58-127">企業可以提供僅限雲端帳戶 toopartner 公司和組織。</span><span class="sxs-lookup"><span data-stu-id="97e58-127">Enterprises can provide cloud-only accounts toopartner companies and organizations.</span></span> <span data-ttu-id="97e58-128">這些合作夥伴之後就能使用單一登入，輕易地存取公司的應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="97e58-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="97e58-129">這個案例是適用的 toousers 存取主要是在 hello 雲端中，例如 Office 365 或 SaaS 依賴 Azure AD 進行驗證的應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="97e58-129">This scenario is applicable toousers who access resources primarily in hello cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="97e58-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="97e58-130">Prerequisites</span></span>
<span data-ttu-id="97e58-131">**在 hello 企業層級 （系統管理員）**</span><span class="sxs-lookup"><span data-stu-id="97e58-131">**At hello enterprise level (administrator)**</span></span>

* <span data-ttu-id="97e58-132">Azure 訂用帳戶搭配 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97e58-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="97e58-133">**Hello 使用者層級**</span><span class="sxs-lookup"><span data-stu-id="97e58-133">**At hello user level**</span></span>

* <span data-ttu-id="97e58-134">Windows 10 (專業版和企業版)</span><span class="sxs-lookup"><span data-stu-id="97e58-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="97e58-135">系統管理員工作</span><span class="sxs-lookup"><span data-stu-id="97e58-135">Administrator tasks</span></span>
* [<span data-ttu-id="97e58-136">設定裝置註冊</span><span class="sxs-lookup"><span data-stu-id="97e58-136">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="97e58-137">使用者工作</span><span class="sxs-lookup"><span data-stu-id="97e58-137">User tasks</span></span>
* [<span data-ttu-id="97e58-138">設定期間使用 Azure AD 設定新的 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="97e58-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md)
* [<span data-ttu-id="97e58-139">設定 Azure AD 與 Windows 10 裝置 hello 設定 功能表</span><span class="sxs-lookup"><span data-stu-id="97e58-139">Set up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="97e58-140">加入個人的 Windows 10 裝置 tooyour 組織</span><span class="sxs-lookup"><span data-stu-id="97e58-140">Join a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="97e58-141">在組織中針對 Windows 10 啟用 BYOD</span><span class="sxs-lookup"><span data-stu-id="97e58-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="97e58-142">您可以設定您的使用者和員工 toouse 其個人的 Windows 裝置 (BYOD) tooaccess 公司應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="97e58-142">You can set up your users and employees toouse their personal Windows devices (BYOD) tooaccess company apps and resources.</span></span> <span data-ttu-id="97e58-143">使用者可以將其 Azure AD 帳戶 （工作或學校帳戶） tooa 個人的 Windows 裝置 tooaccess 資源安全且相容的方式。</span><span class="sxs-lookup"><span data-stu-id="97e58-143">Your users can add their Azure AD accounts (work or school accounts) tooa personal Windows device tooaccess resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="97e58-144">必要條件</span><span class="sxs-lookup"><span data-stu-id="97e58-144">Prerequisites</span></span>
<span data-ttu-id="97e58-145">**在 hello 企業層級 （系統管理員）**</span><span class="sxs-lookup"><span data-stu-id="97e58-145">**At hello enterprise level (administrator)**</span></span>

* <span data-ttu-id="97e58-146">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="97e58-146">Azure AD subscription</span></span>

<span data-ttu-id="97e58-147">**Hello 使用者層級**</span><span class="sxs-lookup"><span data-stu-id="97e58-147">**At hello user level**</span></span>

* <span data-ttu-id="97e58-148">Windows 10 (專業版和企業版)</span><span class="sxs-lookup"><span data-stu-id="97e58-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="97e58-149">系統管理員工作</span><span class="sxs-lookup"><span data-stu-id="97e58-149">Administrator tasks</span></span>
* [<span data-ttu-id="97e58-150">設定裝置註冊</span><span class="sxs-lookup"><span data-stu-id="97e58-150">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="97e58-151">使用者工作</span><span class="sxs-lookup"><span data-stu-id="97e58-151">User tasks</span></span>
* [<span data-ttu-id="97e58-152">加入個人的 Windows 10 裝置 tooyour 組織</span><span class="sxs-lookup"><span data-stu-id="97e58-152">Join a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a><span data-ttu-id="97e58-153">其他資訊</span><span class="sxs-lookup"><span data-stu-id="97e58-153">Additional information</span></span>
* [<span data-ttu-id="97e58-154">Hello 企業版的 Windows 10： 工作的方式 toouse 裝置</span><span class="sxs-lookup"><span data-stu-id="97e58-154">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="97e58-155">擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端</span><span class="sxs-lookup"><span data-stu-id="97e58-155">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="97e58-156">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="97e58-156">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="97e58-157">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="97e58-157">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="97e58-158">連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="97e58-158">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="97e58-159">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="97e58-159">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

