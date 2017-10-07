---
title: "教學課程︰以內部部署 Active Directory 和 Azure Active Directory 設定自動化使用者佈建的 Workday | Microsoft Docs"
description: "深入了解如何 toouse Workday 的 Active Directory 和 Azure Active Directory 身分識別資料來源。"
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
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a><span data-ttu-id="0f093-103">教學課程︰以內部部署 Active Directory 和 Azure Active Directory 設定自動化使用者佈建的 Workday</span><span class="sxs-lookup"><span data-stu-id="0f093-103">Tutorial: Configure Workday for automatic user provisioning with on-premises Active Directory and Azure Active Directory</span></span>
<span data-ttu-id="0f093-104">本教學課程的 hello 目標是 tooshow hello 到 Active Directory 和 Azure Active Directory，必須使用選擇性的回寫的某些屬性 tooWorkday tooperform tooimport 人從 Workday 步驟。</span><span class="sxs-lookup"><span data-stu-id="0f093-104">hello objective of this tutorial is tooshow you hello steps you need tooperform tooimport people from Workday into both Active Directory and Azure Active Directory, with optional writeback of some attributes tooWorkday.</span></span> 



## <a name="overview"></a><span data-ttu-id="0f093-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0f093-105">Overview</span></span>

<span data-ttu-id="0f093-106">hello[佈建服務的 Azure Active Directory 使用者](active-directory-saas-app-provisioning.md)hello 與整合[Workday 人力資源應用程式開發介面](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html)中排序 tooprovision 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-106">hello [Azure Active Directory user provisioning service](active-directory-saas-app-provisioning.md) integrates with hello [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in order tooprovision user accounts.</span></span> <span data-ttu-id="0f093-107">Azure AD 會使用此連接 tooenable hello 遵循使用者佈建工作流程：</span><span class="sxs-lookup"><span data-stu-id="0f093-107">Azure AD uses this connection tooenable hello following user provisioning workflows:</span></span>

* <span data-ttu-id="0f093-108">**佈建使用者 tooActive 目錄**-到一或多個 Active Directory 樹系同步處理選取的使用者集合將 Workday 中。</span><span class="sxs-lookup"><span data-stu-id="0f093-108">**Provisioning users tooActive Directory** - Synchronize selected sets of users from Workday into one or more Active Directory forests.</span></span> 

* <span data-ttu-id="0f093-109">**僅限雲端的使用者 tooAzure Active Directory 佈建**-存在於 Active Directory 和 Azure Active Directory 的混合式使用者可以佈建到 hello 後者使用[AAD Connect](connect/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="0f093-109">**Provisioning cloud-only users tooAzure Active Directory** - Hybrid users who exist in both Active Directory and Azure Active Directory can be provisioned into hello latter using [AAD Connect](connect/active-directory-aadconnect.md).</span></span> <span data-ttu-id="0f093-110">不過，僅限雲端的使用者可以直接從 Workday tooAzure Active Directory 使用 hello 佈建服務的 Azure AD 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="0f093-110">However, users that are cloud-only can be provisioned directly from Workday tooAzure Active Directory using hello Azure AD user provisioning service.</span></span>

* <span data-ttu-id="0f093-111">**電子郵件的回寫位址 tooWorkday** -hello Azure AD 使用者佈建服務可以撰寫選取 Azure AD 使用者屬性後的 tooWorkday，例如 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0f093-111">**Writeback of email addresses tooWorkday** - hello Azure AD user provisioning service can write selected Azure AD user attributes back tooWorkday, such as hello email address.</span></span>

### <a name="scenarios-covered"></a><span data-ttu-id="0f093-112">涵蓋的案例</span><span class="sxs-lookup"><span data-stu-id="0f093-112">Scenarios covered</span></span>

<span data-ttu-id="0f093-113">hello Workday 使用者佈建 hello Azure AD 使用者佈建服務所支援的工作流程可讓 hello 下列人力資源和身分識別生命週期管理案例的自動化：</span><span class="sxs-lookup"><span data-stu-id="0f093-113">hello Workday user provisioning workflows supported by hello Azure AD user provisioning service enables automation of hello following human resources and identity lifecycle management scenarios:</span></span>

* <span data-ttu-id="0f093-114">**雇用的員工**-tooWorkday，加入新的員工時在 Active Directory、 Azure Active Directory 和 Office 365 （選擇性） 將會自動建立使用者帳戶和[支援 Azure AD 的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)，寫入 hello 電子郵件地址 tooWorkday 背面。</span><span class="sxs-lookup"><span data-stu-id="0f093-114">**Hiring new employees** - When a new employee is added tooWorkday, a user account will be automatically created in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md), with write back of hello email address tooWorkday.</span></span>

* <span data-ttu-id="0f093-115">**員工屬性和設定檔更新** - 在 Workday 中更新員工記錄時 (例如姓名、職稱或經理)，系統會在 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)中自動更新其使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-115">**Employee attribute and profile updates** - When an employee record is updated in Workday (such as their name, title, or manager), their user account will be automatically updated in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="0f093-116">**員工離職** - 在 Workday 中將員工設定為離職時，系統會在 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)中自動停用其使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-116">**Employee terminations** - When an employee is terminated in Workday, their user account is automatically disabled in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="0f093-117">**重新雇用的員工**-當員工 rehired workday，舊的帳戶可以自動重新啟動或重新佈建 （取決於您的喜好設定） tooActive 目錄、 Azure Active Directory，並選擇性地 Office 365 和[支援 Azure AD 的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="0f093-117">**Employee re-hires** - When an employee is rehired in Workday, their old account can be automatically reactivated or re-provisioned (depending on your preference) tooActive Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>


## <a name="planning-your-solution"></a><span data-ttu-id="0f093-118">規劃您的解決方案</span><span class="sxs-lookup"><span data-stu-id="0f093-118">Planning your solution</span></span>

<span data-ttu-id="0f093-119">開始之前您的 Workday 整合，確認下列和讀取 hello 下列指引的 hello 必要條件 toomatch 您目前的 Active Directory 架構和使用者佈建需求與 hello 方案提供的 Azure Active目錄。</span><span class="sxs-lookup"><span data-stu-id="0f093-119">Before beginning your Workday integration, check hello prerequisites below and read hello following guidance on how toomatch your current Active Directory architecture and user provisioning requirements with hello solution(s) provided by Azure Active Directory.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0f093-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="0f093-120">Prerequisites</span></span>

<span data-ttu-id="0f093-121">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="0f093-121">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="0f093-122">具有全域系統管理員存取權的有效 Azure AD Premium P1 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0f093-122">A valid Azure AD Premium P1 subscription with global administrator access</span></span>
* <span data-ttu-id="0f093-123">可供測試和整合之用的 Workday 實作租用戶</span><span class="sxs-lookup"><span data-stu-id="0f093-123">A Workday implementation tenant for testing and integration purposes</span></span>
* <span data-ttu-id="0f093-124">在 Workday toocreate 系統整合使用者的系統管理員權限和基於測試目的請變更 tootest 員工資料</span><span class="sxs-lookup"><span data-stu-id="0f093-124">Administrator permissions in Workday toocreate a system integration user, and make changes tootest employee data for testing purposes</span></span>
* <span data-ttu-id="0f093-125">使用者佈建 tooActive 目錄，2012年或更新版本執行 Windows 服務已加入網域的伺服器是需要的 toohost hello[在內部部署同步處理代理程式](https://go.microsoft.com/fwlink/?linkid=847801)</span><span class="sxs-lookup"><span data-stu-id="0f093-125">For user provisioning tooActive Directory, a domain-joined server running Windows Service 2012 or greater is required toohost hello [on-premises synchronization agent](https://go.microsoft.com/fwlink/?linkid=847801)</span></span>
* <span data-ttu-id="0f093-126">可在 Active Directory 與 Azure AD 之間同步處理的 [Azure AD Connect](connect/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="0f093-126">[Azure AD Connect](connect/active-directory-aadconnect.md) for synchronizing between Active Directory and Azure AD</span></span>

> [!NOTE]
> <span data-ttu-id="0f093-127">如果您的 Azure AD 租用戶位於歐洲，請參閱 hello[已知問題](#known-issues)下一節。</span><span class="sxs-lookup"><span data-stu-id="0f093-127">If your Azure AD tenant is located in Europe, please see hello [Known issues](#known-issues) section below.</span></span>


### <a name="solution-architecture"></a><span data-ttu-id="0f093-128">方案架構</span><span class="sxs-lookup"><span data-stu-id="0f093-128">Solution architecture</span></span>

<span data-ttu-id="0f093-129">Azure AD 提供一組豐富的佈建連接器 toohelp 解決佈建和身分識別生命週期管理從 Workday tooActive 目錄中，Azure AD，SaaS 應用程式和更新版本。</span><span class="sxs-lookup"><span data-stu-id="0f093-129">Azure AD provides a rich set of provisioning connectors toohelp you solve provisioning and identity lifecycle management from Workday tooActive Directory, Azure AD, SaaS apps, and beyond.</span></span> <span data-ttu-id="0f093-130">哪些功能您將使用，而且設定 hello 方案的方式會根據您的組織環境和需求而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0f093-130">Which features you will use and how you set up hello solution will vary depending on your organization's environment and requirements.</span></span> <span data-ttu-id="0f093-131">第一個步驟中，採用 hello 下列數量的確實存在且已部署在組織中的內的建：</span><span class="sxs-lookup"><span data-stu-id="0f093-131">As a first step, take stock of how many of hello following are present and deployed in your organization:</span></span>

* <span data-ttu-id="0f093-132">您正在使用多少 Active Directory 樹系？</span><span class="sxs-lookup"><span data-stu-id="0f093-132">How many Active Directory Forests are in use?</span></span>
* <span data-ttu-id="0f093-133">您正在使用多少 Active Directory 網域？</span><span class="sxs-lookup"><span data-stu-id="0f093-133">How many Active Directory Domains are in use?</span></span>
* <span data-ttu-id="0f093-134">有多少 Active Directory 組織單位 (OU) 正在使用？</span><span class="sxs-lookup"><span data-stu-id="0f093-134">How many Active Directory Organizational Units (OUs) are in use?</span></span>
* <span data-ttu-id="0f093-135">有多少 Azure Active Directory 租用戶正在使用？</span><span class="sxs-lookup"><span data-stu-id="0f093-135">How many Azure Active Directory tenants are in use?</span></span>
* <span data-ttu-id="0f093-136">有需要佈建 toobe tooboth Active Directory 與 Azure Active Directory （例如 「 混合 」 使用者） 的使用者嗎？</span><span class="sxs-lookup"><span data-stu-id="0f093-136">Are there users who need toobe provisioned tooboth Active Directory and Azure Active Directory (e.g. "hybrid" users)?</span></span>
* <span data-ttu-id="0f093-137">有需要佈建 toobe tooAzure Active Directory，但沒有 Active Directory （例如 「 僅限雲端的 「 使用者） 的使用者嗎？</span><span class="sxs-lookup"><span data-stu-id="0f093-137">Are there users who need toobe provisioned tooAzure Active Directory, but not Active Directory (e.g. "cloud-only" users)?</span></span>
* <span data-ttu-id="0f093-138">使用者電子郵件地址需要寫回 tooWorkday toobe 嗎？</span><span class="sxs-lookup"><span data-stu-id="0f093-138">Do user email addresses need toobe written back tooWorkday?</span></span>

<span data-ttu-id="0f093-139">答案 toothese 問題之後，您可以規劃佈建部署下列 hello 準則工作日。</span><span class="sxs-lookup"><span data-stu-id="0f093-139">Once you have answers toothese questions, you can plan your Workday provisioning deployment by following hello guidance below.</span></span>

#### <a name="using-provisioning-connector-apps"></a><span data-ttu-id="0f093-140">使用佈建連接器應用程式</span><span class="sxs-lookup"><span data-stu-id="0f093-140">Using provisioning connector apps</span></span>

<span data-ttu-id="0f093-141">Azure Active Directory 支援適用於 Workday 和大量其他 SaaS 應用程式的預先整合佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="0f093-141">Azure Active Directory supports pre-integrated provisioning connectors for Workday and a large number of other SaaS applications.</span></span> 

<span data-ttu-id="0f093-142">單一的佈建連接器以單一來源系統的 hello API 介面，並協助佈建資料 tooa 單一目標系統。</span><span class="sxs-lookup"><span data-stu-id="0f093-142">A single provisioning connector interfaces with hello API of a single source system, and helps provision data tooa single target system.</span></span> <span data-ttu-id="0f093-143">大部分 Azure AD 支援的佈建連接器為單一來源和目標系統 (例如 Azure AD tooServiceNow)，可能會安裝程式只需加 hello 應用程式有問題從 hello Azure AD app 資源庫 (例如 ServiceNow)。</span><span class="sxs-lookup"><span data-stu-id="0f093-143">Most provisioning connectors that Azure AD supports are for a single source and target system (e.g. Azure AD tooServiceNow), and can be setup by simply adding hello app in question from hello Azure AD app gallery (e.g. ServiceNow).</span></span> 

<span data-ttu-id="0f093-144">在 Azure AD 中佈建連接器執行個體與應用程式執行個體之間具有一對一關聯性：</span><span class="sxs-lookup"><span data-stu-id="0f093-144">There is a one-to-one relationship between provisioning connector instances and app instances in Azure AD:</span></span>

| <span data-ttu-id="0f093-145">來源系統</span><span class="sxs-lookup"><span data-stu-id="0f093-145">Source System</span></span> | <span data-ttu-id="0f093-146">目標系統</span><span class="sxs-lookup"><span data-stu-id="0f093-146">Target System</span></span> |
| ---------- | ---------- | 
| <span data-ttu-id="0f093-147">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="0f093-147">Azure AD tenant</span></span> | <span data-ttu-id="0f093-148">SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f093-148">SaaS application</span></span> |


<span data-ttu-id="0f093-149">不過，當使用 Workday 和 Active Directory，會視為的多個來源和目標系統 toobe:</span><span class="sxs-lookup"><span data-stu-id="0f093-149">However, when working with Workday and Active Directory, there are multiple source and target systems toobe considered:</span></span>

| <span data-ttu-id="0f093-150">來源系統</span><span class="sxs-lookup"><span data-stu-id="0f093-150">Source System</span></span> | <span data-ttu-id="0f093-151">目標系統</span><span class="sxs-lookup"><span data-stu-id="0f093-151">Target System</span></span> | <span data-ttu-id="0f093-152">注意事項</span><span class="sxs-lookup"><span data-stu-id="0f093-152">Notes</span></span> |
| ---------- | ---------- | ---------- |
| <span data-ttu-id="0f093-153">Workday</span><span class="sxs-lookup"><span data-stu-id="0f093-153">Workday</span></span> | <span data-ttu-id="0f093-154">Active Directory 樹系</span><span class="sxs-lookup"><span data-stu-id="0f093-154">Active Directory Forest</span></span> | <span data-ttu-id="0f093-155">系統會將每個樹系視為相異目標系統</span><span class="sxs-lookup"><span data-stu-id="0f093-155">Each forest is treated as a distinct target system</span></span> |
| <span data-ttu-id="0f093-156">Workday</span><span class="sxs-lookup"><span data-stu-id="0f093-156">Workday</span></span> | <span data-ttu-id="0f093-157">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="0f093-157">Azure AD tenant</span></span> | <span data-ttu-id="0f093-158">根據僅限雲端使用者的要求</span><span class="sxs-lookup"><span data-stu-id="0f093-158">As required for cloud-only users</span></span> |
| <span data-ttu-id="0f093-159">Active Directory 樹系</span><span class="sxs-lookup"><span data-stu-id="0f093-159">Active Directory Forest</span></span> | <span data-ttu-id="0f093-160">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="0f093-160">Azure AD tenant</span></span> | <span data-ttu-id="0f093-161">目前由 AAD Connect 處理此流程</span><span class="sxs-lookup"><span data-stu-id="0f093-161">This flow is handled by AAD Connect today</span></span> |
| <span data-ttu-id="0f093-162">Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="0f093-162">Azure AD tenant</span></span> | <span data-ttu-id="0f093-163">Workday</span><span class="sxs-lookup"><span data-stu-id="0f093-163">Workday</span></span> | <span data-ttu-id="0f093-164">適用於電子郵件地址的回寫</span><span class="sxs-lookup"><span data-stu-id="0f093-164">For writeback of email addresses</span></span> |

<span data-ttu-id="0f093-165">toofacilitate 這些多個工作流程 toomultiple 來源和目標系統，Azure AD 提供多個佈建連接器應用程式，您可以從 hello Azure AD app 資源庫加入：</span><span class="sxs-lookup"><span data-stu-id="0f093-165">toofacilitate these multiple workflows toomultiple source and target systems, Azure AD provides multiple provisioning connector apps that you can add from hello Azure AD app gallery:</span></span>

![AAD 應用程式庫](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* <span data-ttu-id="0f093-167">**目錄佈建的 workday tooActive** -此應用程式可協助從 Workday tooa 單一 Active Directory 樹系佈建的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-167">**Workday tooActive Directory Provisioning** - This app facilitates user account provisioning from Workday tooa single Active Directory forest.</span></span> <span data-ttu-id="0f093-168">如果您有多個樹系，您可以從每個 Active Directory 樹系需要以 tooprovision hello Azure AD app 資源庫來新增此應用程式的一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="0f093-168">If you have multiple forests, you can add one instance of this app from hello Azure AD app gallery for each Active Directory forest you need tooprovision to.</span></span>

* <span data-ttu-id="0f093-169">**Workday tooAzure AD 佈建**-雖然 AAD Connect 是 hello 工具應該使用的 toosynchronize Active Directory 使用者 tooAzure Active Directory，此應用程式可能會使用的 toofacilitate 從 Workday tooa 單一的僅限雲端的使用者佈建Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-169">**Workday tooAzure AD Provisioning** - While AAD Connect is hello tool that should be used toosynchronize Active Directory users tooAzure Active Directory, this app can be used toofacilitate provisioning of cloud-only users from Workday tooa single Azure Active Directory tenant.</span></span>

* <span data-ttu-id="0f093-170">**Workday 的回寫**-此應用程式可協助從 Azure Active Directory tooWorkday 使用者的電子郵件地址的回寫。</span><span class="sxs-lookup"><span data-stu-id="0f093-170">**Workday Writeback** - This app facilitates writeback of user's email addresses from Azure Active Directory tooWorkday.</span></span>

> [!TIP]
> <span data-ttu-id="0f093-171">hello 規則 」 Workday 」 應用程式用來設定單一登入 Workday 與 Azure Active Directory 之間。</span><span class="sxs-lookup"><span data-stu-id="0f093-171">hello regular "Workday" app is used for setting up single sign-on between Workday and Azure Active Directory.</span></span> 

<span data-ttu-id="0f093-172">如何 tooset 安裝及設定這些特殊佈建連接器應用程式 」 是 hello hello 剩餘各節，本教學課程的主題。</span><span class="sxs-lookup"><span data-stu-id="0f093-172">How tooset up and configure these special provisioning connector apps is hello subject of hello remaining sections of this tutorial.</span></span> <span data-ttu-id="0f093-173">哪些應用程式，您可以選擇 tooconfigure 將取決於您的系統上需要 tooprovision，以及多少 Active Directory 樹系與 Azure AD 租用戶不在您的環境中。</span><span class="sxs-lookup"><span data-stu-id="0f093-173">Which apps you choose tooconfigure will depend on which systems you need tooprovision to, and how many Active Directory Forests and Azure AD tenants are in your environment.</span></span>

![概觀](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a><span data-ttu-id="0f093-175">在 Workday 中設定系統整合使用者</span><span class="sxs-lookup"><span data-stu-id="0f093-175">Configure a system integration user in Workday</span></span>
<span data-ttu-id="0f093-176">所有 hello Workday 佈建連接器的常見的需求是它們需要認證的 Workday 系統整合帳戶 tooconnect toohello Workday 人力資源應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="0f093-176">A common requirement of all hello Workday provisioning connectors is they require credentials for a Workday system integration account tooconnect toohello Workday Human Resources API.</span></span> <span data-ttu-id="0f093-177">本章節描述 toocreate 系統整合者 Workday 中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-177">This section describes how toocreate a system integrator account in Workday.</span></span>

> [!NOTE]
> <span data-ttu-id="0f093-178">它是可能 toobypass 此程序，並以 hello 系統整合帳戶改用 Workday 全域管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-178">It is possible toobypass this procedure and instead use a Workday global administrator account as hello system integration account.</span></span> <span data-ttu-id="0f093-179">這可能會在示範中正常運作，但不建議用於生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="0f093-179">This may work fine for demos, but is not recommended for production deployments.</span></span>

### <a name="create-an-integration-system-user"></a><span data-ttu-id="0f093-180">建立整合系統使用者</span><span class="sxs-lookup"><span data-stu-id="0f093-180">Create an integration system user</span></span>

<span data-ttu-id="0f093-181">**toocreate 整合系統使用者：**</span><span class="sxs-lookup"><span data-stu-id="0f093-181">**toocreate an integration system user:**</span></span>

1. <span data-ttu-id="0f093-182">使用系統管理員帳戶登入 Workday 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0f093-182">Sign into your Workday tenant using an administrator account.</span></span> <span data-ttu-id="0f093-183">在 hello **Workday Workbench**，輸入在 hello 搜尋方塊中，建立使用者，然後按一下**建立整合系統使用者**。</span><span class="sxs-lookup"><span data-stu-id="0f093-183">In hello **Workday Workbench**, enter create user in hello search box, and then click **Create Integration System User**.</span></span> 
   
    <span data-ttu-id="0f093-184">![建立使用者](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="0f093-184">![Create user](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Create user")</span></span>
2. <span data-ttu-id="0f093-185">完整的 hello**建立整合系統使用者**藉由提供使用者名稱和密碼為新的整合系統使用者的工作。</span><span class="sxs-lookup"><span data-stu-id="0f093-185">Complete hello **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="0f093-186">保留 hello**在下次登入時要求新密碼**選項未選取，因為這個使用者會登入以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="0f093-186">Leave hello **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span> 
 * <span data-ttu-id="0f093-187">保留 hello**工作階段逾時分鐘數**其預設值是 0，這可以防止 hello 使用者工作階段提前逾時。</span><span class="sxs-lookup"><span data-stu-id="0f093-187">Leave hello **Session Timeout Minutes** with its default value of 0, which will prevent hello user’s sessions from timing out prematurely.</span></span> 
   
    <span data-ttu-id="0f093-188">![建立整合系統使用者](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "建立整合系統使用者")</span><span class="sxs-lookup"><span data-stu-id="0f093-188">![Create Integration System User](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Create Integration System User")</span></span>

### <a name="create-a-security-group"></a><span data-ttu-id="0f093-189">建立安全性群組</span><span class="sxs-lookup"><span data-stu-id="0f093-189">Create a security group</span></span>
<span data-ttu-id="0f093-190">您需要 toocreate 受限的整合系統安全性群組，並指派 hello 使用者 tooit。</span><span class="sxs-lookup"><span data-stu-id="0f093-190">You need toocreate an unconstrained integration system security group and assign hello user tooit.</span></span>

<span data-ttu-id="0f093-191">**toocreate 安全性群組：**</span><span class="sxs-lookup"><span data-stu-id="0f093-191">**toocreate a security group:**</span></span>

1. <span data-ttu-id="0f093-192">輸入在 hello 搜尋方塊中，建立安全性群組，然後按一下**建立安全性群組**。</span><span class="sxs-lookup"><span data-stu-id="0f093-192">Enter create security group in hello search box, and then click **Create Security Group**.</span></span> 
   
    <span data-ttu-id="0f093-193">![建立安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "建立安全性群組")</span><span class="sxs-lookup"><span data-stu-id="0f093-193">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span></span>
2. <span data-ttu-id="0f093-194">完整的 hello**建立安全性群組**工作。</span><span class="sxs-lookup"><span data-stu-id="0f093-194">Complete hello **Create Security Group** task.</span></span>  
3. <span data-ttu-id="0f093-195">選取整合系統安全性群組 — 未受限從 hello**類型的安全性群組**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="0f093-195">Select Integration System Security Group—Unconstrained from hello **Type of Tenanted Security Group** dropdown.</span></span>
4. <span data-ttu-id="0f093-196">建立安全性群組 toowhich 明確加入成員。</span><span class="sxs-lookup"><span data-stu-id="0f093-196">Create a security group toowhich members will be explicitly added.</span></span> 
   
    <span data-ttu-id="0f093-197">![建立安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "建立安全性群組")</span><span class="sxs-lookup"><span data-stu-id="0f093-197">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span></span>

### <a name="assign-hello-integration-system-user-toohello-security-group"></a><span data-ttu-id="0f093-198">指派 hello 整合系統使用者 toohello 安全性群組</span><span class="sxs-lookup"><span data-stu-id="0f093-198">Assign hello integration system user toohello security group</span></span>

<span data-ttu-id="0f093-199">**tooassign hello 整合系統使用者：**</span><span class="sxs-lookup"><span data-stu-id="0f093-199">**tooassign hello integration system user:**</span></span>

1. <span data-ttu-id="0f093-200">在 [hello] 搜尋方塊中，輸入編輯安全性群組，然後按一下**編輯安全性群組**。</span><span class="sxs-lookup"><span data-stu-id="0f093-200">Enter edit security group in hello search box, and then click **Edit Security Group**.</span></span> 
   
    <span data-ttu-id="0f093-201">![編輯安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "編輯安全性群組")</span><span class="sxs-lookup"><span data-stu-id="0f093-201">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edit Security Group")</span></span>
2. <span data-ttu-id="0f093-202">搜尋，並依名稱選取 hello 新整合的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="0f093-202">Search for, and select hello new integration security group by name.</span></span> 
   
    <span data-ttu-id="0f093-203">![編輯安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "編輯安全性群組")</span><span class="sxs-lookup"><span data-stu-id="0f093-203">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edit Security Group")</span></span>
3. <span data-ttu-id="0f093-204">新增 hello 新整合系統使用者 toohello 新安全性群組。</span><span class="sxs-lookup"><span data-stu-id="0f093-204">Add hello new integration system user toohello new security group.</span></span> 
   
    <span data-ttu-id="0f093-205">![系統安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "系統安全性群組")</span><span class="sxs-lookup"><span data-stu-id="0f093-205">![System Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "System Security Group")</span></span>  

### <a name="configure-security-group-options"></a><span data-ttu-id="0f093-206">設定安全性群組選項</span><span class="sxs-lookup"><span data-stu-id="0f093-206">Configure security group options</span></span>
<span data-ttu-id="0f093-207">在此步驟中，您將授與 toohello 新的安全群組的權限**取得**和**放**hello 下列網域安全性原則所保護的 hello 物件上的作業：</span><span class="sxs-lookup"><span data-stu-id="0f093-207">In this step, you grant toohello new security group permissions for **Get** and **Put** operations on hello objects secured by hello following domain security policies:</span></span>

* <span data-ttu-id="0f093-208">外部帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="0f093-208">External Account Provisioning</span></span>
* <span data-ttu-id="0f093-209">人員資料：公用人員報告</span><span class="sxs-lookup"><span data-stu-id="0f093-209">Worker Data: Public Worker Reports</span></span>
* <span data-ttu-id="0f093-210">人員資料：所有職位</span><span class="sxs-lookup"><span data-stu-id="0f093-210">Worker Data: All Positions</span></span>
* <span data-ttu-id="0f093-211">人員資料：目前人員配置資訊</span><span class="sxs-lookup"><span data-stu-id="0f093-211">Worker Data: Current Staffing Information</span></span>
* <span data-ttu-id="0f093-212">人員資料：人員個人檔案的職稱</span><span class="sxs-lookup"><span data-stu-id="0f093-212">Worker Data: Business Title on Worker Profile</span></span>

<span data-ttu-id="0f093-213">**tooconfigure 安全性群組選項：**</span><span class="sxs-lookup"><span data-stu-id="0f093-213">**tooconfigure security group options:**</span></span>

1. <span data-ttu-id="0f093-214">Hello 搜尋方塊中，輸入網域安全性原則，然後按一下 hello 連結**功能區域的網域安全性原則**。</span><span class="sxs-lookup"><span data-stu-id="0f093-214">Enter domain security policies in hello search box, and then click on hello link **Domain Security Policies for Functional Area**.</span></span>  
   
    <span data-ttu-id="0f093-215">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="0f093-215">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="0f093-216">搜尋系統和選取 hello**系統**功能區域。</span><span class="sxs-lookup"><span data-stu-id="0f093-216">Search for system and select hello **System** functional area.</span></span>  <span data-ttu-id="0f093-217">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0f093-217">Click **OK**.</span></span>  
   
    <span data-ttu-id="0f093-218">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="0f093-218">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="0f093-219">在 [hello] 清單中的 hello 系統功能區域的安全性原則，依序展開**安全性管理**hello 網域安全性原則並加以選取**外部帳戶佈建**。</span><span class="sxs-lookup"><span data-stu-id="0f093-219">In hello list of security policies for hello System functional area, expand **Security Administration** and select hello domain security policy **External Account Provisioning**.</span></span>  
   
    <span data-ttu-id="0f093-220">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="0f093-220">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span></span>  
4. <span data-ttu-id="0f093-221">按一下**編輯權限**，然後在 hello**編輯權限**對話方塊頁面上，新增 hello 新安全性群組 toohello 安全性群組清單與**取得**和**放**整合權限。</span><span class="sxs-lookup"><span data-stu-id="0f093-221">Click **Edit Permissions**, and then, on hello **Edit Permissions**dialog page, add hello new security group toohello list of security groups with **Get** and **Put** integration permissions.</span></span> 
   
    <span data-ttu-id="0f093-222">![編輯權限](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "編輯權限")</span><span class="sxs-lookup"><span data-stu-id="0f093-222">![Edit Permission](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Edit Permission")</span></span>  
5. <span data-ttu-id="0f093-223">重複步驟 1 選取的功能區域，tooreturn toohello 螢幕上，再搜尋人員配置，這次選取 hello**人員配置 功能區域**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0f093-223">Repeat step 1 above tooreturn toohello screen for selecting functional areas, and this time, search for staffing, select hello **Staffing functional area** and click **OK**.</span></span>
   
    <span data-ttu-id="0f093-224">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="0f093-224">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Domain Security Policies")</span></span>  
6. <span data-ttu-id="0f093-225">在 hello 清單中的 hello 人員配置 功能區域的安全性原則，依序展開**工作者資料： 人員配置**和重複上述步驟 4 的每一種剩餘的安全性原則：</span><span class="sxs-lookup"><span data-stu-id="0f093-225">In hello list of security policies for hello Staffing functional area, expand **Worker Data: Staffing** and repeat step 4 above for each of these remaining security policies:</span></span>

   * <span data-ttu-id="0f093-226">人員資料：公用人員報告</span><span class="sxs-lookup"><span data-stu-id="0f093-226">Worker Data: Public Worker Reports</span></span>
   * <span data-ttu-id="0f093-227">人員資料：所有職位</span><span class="sxs-lookup"><span data-stu-id="0f093-227">Worker Data: All Positions</span></span>
   * <span data-ttu-id="0f093-228">人員資料：目前人員配置資訊</span><span class="sxs-lookup"><span data-stu-id="0f093-228">Worker Data: Current Staffing Information</span></span>
   * <span data-ttu-id="0f093-229">人員資料：人員個人檔案的職稱</span><span class="sxs-lookup"><span data-stu-id="0f093-229">Worker Data: Business Title on Worker Profile</span></span>
   
7. <span data-ttu-id="0f093-230">重複步驟 1 所選取的功能區域的 tooreturn toohello 螢幕上，這次搜尋**連絡人資訊**選取 hello 人員配置 功能區域，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0f093-230">Repeat step 1, above, tooreturn toohello screen for selecting  functional areas, and this time, search for **Contact Information**,  select hello Staffing functional area, and click **OK**.</span></span>

8.  <span data-ttu-id="0f093-231">在 hello 清單中的 hello 人員配置 功能區域的安全性原則，依序展開**工作者資料： 工作的連絡資訊**，並重複上述步驟 4 hello 安全性原則下：</span><span class="sxs-lookup"><span data-stu-id="0f093-231">In hello list of security policies for hello Staffing functional area, expand **Worker Data: Work Contact Information**, and repeat step 4 above for hello security policies below:</span></span>

    * <span data-ttu-id="0f093-232">人員資料：公司電子郵件</span><span class="sxs-lookup"><span data-stu-id="0f093-232">Worker Data: Work Email</span></span>

    <span data-ttu-id="0f093-233">![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "網域安全性原則")</span><span class="sxs-lookup"><span data-stu-id="0f093-233">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Domain Security Policies")</span></span>  
    
### <a name="activate-security-policy-changes"></a><span data-ttu-id="0f093-234">啟用安全性原則變更</span><span class="sxs-lookup"><span data-stu-id="0f093-234">Activate security policy changes</span></span>

<span data-ttu-id="0f093-235">**tooactivate 安全性原則變更：**</span><span class="sxs-lookup"><span data-stu-id="0f093-235">**tooactivate security policy changes:**</span></span>

1. <span data-ttu-id="0f093-236">輸入啟動 hello 搜尋 方塊中，然後按一下 hello 連結**啟動擱置安全性原則變更**。</span><span class="sxs-lookup"><span data-stu-id="0f093-236">Enter activate in hello search box, and then click on hello link **Activate Pending Security Policy Changes**.</span></span> 
   
    <span data-ttu-id="0f093-237">![啟用](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "啟用")</span><span class="sxs-lookup"><span data-stu-id="0f093-237">![Activate](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activate")</span></span> 
2. <span data-ttu-id="0f093-238">啟動擱置安全性原則變更為稽核用途，輸入註解工作，然後按一下開始 hello**確定**。</span><span class="sxs-lookup"><span data-stu-id="0f093-238">Begin hello Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span></span> 
   
    <span data-ttu-id="0f093-239">![啟用擱置的安全性](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "啟用擱置的安全性")</span><span class="sxs-lookup"><span data-stu-id="0f093-239">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span></span>   
3. <span data-ttu-id="0f093-240">Hello 藉由檢查 hello 核取方塊的下一個畫面上的完整 hello 工作**確認**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0f093-240">Complete hello task on hello next screen by checking hello checkbox **Confirm**, and then click **OK**.</span></span> 
   
    <span data-ttu-id="0f093-241">![啟用擱置的安全性](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "啟用擱置的安全性")</span><span class="sxs-lookup"><span data-stu-id="0f093-241">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a><span data-ttu-id="0f093-242">設定使用者佈建從 Workday tooActive 目錄</span><span class="sxs-lookup"><span data-stu-id="0f093-242">Configuring user provisioning from Workday tooActive Directory</span></span>
<span data-ttu-id="0f093-243">請遵循這些指示 tooconfigure 使用者帳戶佈建從 Workday tooeach 您需要佈建的 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="0f093-243">Follow these instructions tooconfigure user account provisioning from Workday tooeach Active Directory forest that you require provisioning to.</span></span>

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="0f093-244">第 1 部分： 加入 hello 佈建的連接器應用程式和建立 hello 連接 tooWorkday</span><span class="sxs-lookup"><span data-stu-id="0f093-244">Part 1: Adding hello provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="0f093-245">**tooconfigure Workday tooActive 目錄佈建：**</span><span class="sxs-lookup"><span data-stu-id="0f093-245">**tooconfigure Workday tooActive Directory provisioning:**</span></span>

1.  <span data-ttu-id="0f093-246">跳過<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="0f093-246">Go too<https://portal.azure.com></span></span>

2.  <span data-ttu-id="0f093-247">在 hello 左的導覽列中，選取  **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="0f093-247">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="0f093-248">依序選取 [企業應用程式] 和 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0f093-248">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="0f093-249">選取**新增應用程式**，並選取 hello**所有**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="0f093-249">Select **Add an application**, and select hello **All** category.</span></span>

5.  <span data-ttu-id="0f093-250">搜尋**Workday 佈建 tooActive 目錄**，並從 hello 組件庫中加入該應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f093-250">Search for **Workday Provisioning tooActive Directory**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="0f093-251">Hello 之後加入的應用程式，而且會顯示 hello 應用程式詳細資料 畫面中，選取**佈建**</span><span class="sxs-lookup"><span data-stu-id="0f093-251">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="0f093-252">變更 hello**佈建****模式**太**自動**</span><span class="sxs-lookup"><span data-stu-id="0f093-252">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="0f093-253">完整的 hello**系統管理員認證**區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0f093-253">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="0f093-254">**系統管理員使用者名稱**– 附加 hello 租用戶網域名稱輸入 hello hello Workday 的整合系統帳戶，使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0f093-254">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="0f093-255">**其應該類似於：username@contoso4**</span><span class="sxs-lookup"><span data-stu-id="0f093-255">**Should look something like: username@contoso4**</span></span>

   * <span data-ttu-id="0f093-256">**系統管理員密碼 –** Enter hello hello Workday 的整合系統帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="0f093-256">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="0f093-257">**租用戶 URL-**輸入您的租用戶 hello URL toohello Workday web 服務端點。</span><span class="sxs-lookup"><span data-stu-id="0f093-257">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="0f093-258">這應該看起來： https://wd3-impl-services1.workday.com/ccx/service/contoso4 其中 contoso4 會取代您正確租用戶的名稱，而 wd3 impl 取代 hello 正確環境字串。</span><span class="sxs-lookup"><span data-stu-id="0f093-258">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string.</span></span>

   * <span data-ttu-id="0f093-259">**Active Directory 樹系-** hello hello Get ADForest powershell 指令程式所傳回的 「 名稱 」 您的 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="0f093-259">**Active Directory Forest -** hello “Name” of your Active Directory forest, as returned by hello Get-ADForest powershell commandlet.</span></span> <span data-ttu-id="0f093-260">此字串通常類似於：*contoso.com*</span><span class="sxs-lookup"><span data-stu-id="0f093-260">This is typically a string like: *contoso.com*</span></span>

   * <span data-ttu-id="0f093-261">**Active Directory 容器-**輸入 hello 容器字串，其中包含您的 AD 樹系中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="0f093-261">**Active Directory Container -** Enter hello container string that contains all users in your AD forest.</span></span> <span data-ttu-id="0f093-262">範例：*OU=Standard Users,OU=Users,DC=contoso,DC=test*</span><span class="sxs-lookup"><span data-stu-id="0f093-262">Example: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span></span>

   * <span data-ttu-id="0f093-263">**電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0f093-263">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="0f093-264">按一下 hello**測試連接** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f093-264">Click hello **Test Connection** button.</span></span> <span data-ttu-id="0f093-265">如果 hello 連接測試成功，按一下 hello**儲存**hello 頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f093-265">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="0f093-266">如果失敗，請仔細檢查 hello 的 Workday 認證會在 Workday 中有效。</span><span class="sxs-lookup"><span data-stu-id="0f093-266">If it fails, double-check that hello Workday credentials are valid in Workday.</span></span> 

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="0f093-268">第 2 部分：設定屬性對應</span><span class="sxs-lookup"><span data-stu-id="0f093-268">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="0f093-269">在本節中，您會設定使用者資料從 Workday 流動至 Active Directory 的方式。</span><span class="sxs-lookup"><span data-stu-id="0f093-269">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="0f093-270">在 hello 佈建索引標籤下**對應**，按一下 **同步處理新的 Workday 工作者 tooOnPremises**。</span><span class="sxs-lookup"><span data-stu-id="0f093-270">On hello Provisioning tab under **Mappings**, click **Synchronize Workday Workers tooOnPremises**.</span></span>

2.  <span data-ttu-id="0f093-271">在 hello**來源物件範圍**欄位，您可以選取 在 Workday 中的使用者將應該提供 tooAD，藉由定義一組屬性為基礎的篩選條件的範圍內。</span><span class="sxs-lookup"><span data-stu-id="0f093-271">In hello **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning tooAD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="0f093-272">hello 預設範圍為 「 Workday 中的所有使用者 」。</span><span class="sxs-lookup"><span data-stu-id="0f093-272">hello default scope is “all users in Workday”.</span></span> <span data-ttu-id="0f093-273">範例篩選：</span><span class="sxs-lookup"><span data-stu-id="0f093-273">Example filters:</span></span>

   * <span data-ttu-id="0f093-274">範例： 範圍 toousers 以背景工作識別碼 2000000 1000000 之間</span><span class="sxs-lookup"><span data-stu-id="0f093-274">Example: Scope toousers with Worker IDs between 1000000 and    2000000</span></span>

      * <span data-ttu-id="0f093-275">屬性：WorkerID</span><span class="sxs-lookup"><span data-stu-id="0f093-275">Attribute: WorkerID</span></span>

      * <span data-ttu-id="0f093-276">運算子：REGEX Match</span><span class="sxs-lookup"><span data-stu-id="0f093-276">Operator: REGEX Match</span></span>

      * <span data-ttu-id="0f093-277">值：(1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="0f093-277">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="0f093-278">範例：僅員工和非約聘人員</span><span class="sxs-lookup"><span data-stu-id="0f093-278">Example: Only employees and not contingent workers</span></span> 

      * <span data-ttu-id="0f093-279">屬性：EmployeeID</span><span class="sxs-lookup"><span data-stu-id="0f093-279">Attribute: EmployeeID</span></span>

      * <span data-ttu-id="0f093-280">運算子：IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="0f093-280">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="0f093-281">在 hello**目標物件動作**欄位，您可以全域篩選允許 toobe Active Directory 上執行哪些動作。</span><span class="sxs-lookup"><span data-stu-id="0f093-281">In hello **Target Object Actions** field, you can globally filter what actions are allowed toobe performed on Active Directory.</span></span> <span data-ttu-id="0f093-282">最常見的動作是 [建立] 和 [更新]。</span><span class="sxs-lookup"><span data-stu-id="0f093-282">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="0f093-283">在 [hello**屬性對應**] 區段中，您可以定義如何個別 Workday 對應 tooActive 目錄屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-283">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span>

5. <span data-ttu-id="0f093-284">按一下現有的屬性對應 tooupdate，或是按一下**加入新的對應**底部 hello hello 螢幕 tooadd 新對應。</span><span class="sxs-lookup"><span data-stu-id="0f093-284">Click on an existing attribute mapping tooupdate it, or click **Add new mapping** at hello bottom of hello screen tooadd new mappings.</span></span> <span data-ttu-id="0f093-285">個別屬性對應支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0f093-285">An individual attribute mapping supports these properties:</span></span>

      * <span data-ttu-id="0f093-286">**對應類型**</span><span class="sxs-lookup"><span data-stu-id="0f093-286">**Mapping Type**</span></span>

         * <span data-ttu-id="0f093-287">**直接**– 寫入 hello hello Workday 屬性 toohello AD 具有屬性值，任何變更</span><span class="sxs-lookup"><span data-stu-id="0f093-287">**Direct** – Writes hello value of hello Workday attribute      toohello AD attribute, with no changes</span></span>

         * <span data-ttu-id="0f093-288">**常數**-將靜態、 常數字串值寫入至 hello AD 屬性</span><span class="sxs-lookup"><span data-stu-id="0f093-288">**Constant** - Write a static, constant string value to      hello AD attribute</span></span>

         * <span data-ttu-id="0f093-289">**運算式**– 可讓您 toowrite hello AD 屬性，根據一個或多個新的 Workday 屬性的自訂值。</span><span class="sxs-lookup"><span data-stu-id="0f093-289">**Expression** – Allows you toowrite a custom value to hello AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="0f093-290">[如需詳細資訊，請參閱這篇有關運算式的文章](active-directory-saas-writing-expressions-for-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="0f093-290">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

      * <span data-ttu-id="0f093-291">**來源屬性**-從 Workday hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-291">**Source attribute** - hello user attribute from Workday.</span></span>

      * <span data-ttu-id="0f093-292">**預設值** – 選用。</span><span class="sxs-lookup"><span data-stu-id="0f093-292">**Default value** – Optional.</span></span> <span data-ttu-id="0f093-293">如果 hello 來源屬性的值是空的 hello 對應會改為寫入此值。</span><span class="sxs-lookup"><span data-stu-id="0f093-293">If hello source attribute has an empty value, hello mapping will write this value instead.</span></span>
            <span data-ttu-id="0f093-294">此空白 tooleave 最常見的組態。</span><span class="sxs-lookup"><span data-stu-id="0f093-294">Most common configuration is tooleave this blank.</span></span>

      * <span data-ttu-id="0f093-295">**目標屬性**– Active Directory 中的 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-295">**Target attribute** – hello user attribute in Active     Directory.</span></span>

      * <span data-ttu-id="0f093-296">**符合使用此屬性的物件**– 是否應使用此對應 toouniquely 識別 Workday 與 Active Directory 之間的使用者。</span><span class="sxs-lookup"><span data-stu-id="0f093-296">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between Workday and Active Directory.</span></span> <span data-ttu-id="0f093-297">這通常是背景工作 ID 欄位上設定，workday，通常會對應至其中一個 Active Directory 中的 hello 員工識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-297">This is typically set on the Worker ID field for Workday, which is typically mapped to one of hello Employee ID attributes in Active Directory.</span></span>

      * <span data-ttu-id="0f093-298">**比對優先順序** – 您可以設定多個比對屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-298">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="0f093-299">具有多個屬性時，系統會以此欄位定義的順序進行評估。</span><span class="sxs-lookup"><span data-stu-id="0f093-299">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="0f093-300">只要找到相符項目，便不會評估進一步比對屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-300">As soon as a match is found, no further matching attributes are evaluated.</span></span>

      * <span data-ttu-id="0f093-301">**套用此對應**</span><span class="sxs-lookup"><span data-stu-id="0f093-301">**Apply this mapping**</span></span>
       
         * <span data-ttu-id="0f093-302">**一律** – 將此對應套用於使用者建立和更新動作</span><span class="sxs-lookup"><span data-stu-id="0f093-302">**Always** – Apply this mapping on both user creation      and update actions</span></span>

         * <span data-ttu-id="0f093-303">**僅限建立期間** - 僅將此對應套用於使用者建立動作</span><span class="sxs-lookup"><span data-stu-id="0f093-303">**Only during creation** - Apply this mapping only on      user creation actions</span></span>

6. <span data-ttu-id="0f093-304">toosave 對應時，按一下**儲存**頂端 hello 屬性對應的區段。</span><span class="sxs-lookup"><span data-stu-id="0f093-304">toosave your mappings, click **Save** at hello top of the      Attribute Mapping section.</span></span>

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

<span data-ttu-id="0f093-306">**下列為 Workday 與 Active Directory 之間的一些範例屬性對應，以及一些常用運算式**</span><span class="sxs-lookup"><span data-stu-id="0f093-306">**Below are some example attribute mappings between Workday and Active Directory, with some common expressions**</span></span>

-   <span data-ttu-id="0f093-307">對應 toohello parentDistinguishedName AD 屬性的 hello 運算式可以是使用的 tooprovision 使用者 tooa 特定 OU 根據一個或多個新的 Workday 來源屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-307">hello expression that maps toohello parentDistinguishedName AD attribute can be used tooprovision a user tooa specific OU based on one or more Workday source attributes.</span></span> <span data-ttu-id="0f093-308">此範例會根據使用者在 Workday 中的城市資料，將其置於不同的 OU。</span><span class="sxs-lookup"><span data-stu-id="0f093-308">This example places users in different OUs depending on their city data in Workday.</span></span>

-   <span data-ttu-id="0f093-309">對應 toohello userPrincipalName AD 屬性的 hello 運算式建立的 UPN firstName.LastName@contoso.com。其也會取代不合法的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="0f093-309">hello expression that maps toohello userPrincipalName AD attribute create a UPN of firstName.LastName@contoso.com. It also replaces illegal special characters.</span></span>

-   [<span data-ttu-id="0f093-310">此為有關撰寫運算式的文件</span><span class="sxs-lookup"><span data-stu-id="0f093-310">There is documentation on writing expressions here</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| <span data-ttu-id="0f093-311">WORKDAY 屬性</span><span class="sxs-lookup"><span data-stu-id="0f093-311">WORKDAY ATTRIBUTE</span></span> | <span data-ttu-id="0f093-312">ACTIVE DIRECTORY 屬性</span><span class="sxs-lookup"><span data-stu-id="0f093-312">ACTIVE DIRECTORY ATTRIBUTE</span></span> |  <span data-ttu-id="0f093-313">比對識別碼？</span><span class="sxs-lookup"><span data-stu-id="0f093-313">MATCHING ID?</span></span> | <span data-ttu-id="0f093-314">建立/更新</span><span class="sxs-lookup"><span data-stu-id="0f093-314">CREATE / UPDATE</span></span> |
| ---------- | ---------- | ---------- | ---------- |
|  <span data-ttu-id="0f093-315">**WorkerID**</span><span class="sxs-lookup"><span data-stu-id="0f093-315">**WorkerID**</span></span>  |  <span data-ttu-id="0f093-316">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="0f093-316">EmployeeID</span></span> | <span data-ttu-id="0f093-317">**是**</span><span class="sxs-lookup"><span data-stu-id="0f093-317">**Yes**</span></span> | <span data-ttu-id="0f093-318">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="0f093-318">Written on create only</span></span> | 
|  <span data-ttu-id="0f093-319">**Municipality**</span><span class="sxs-lookup"><span data-stu-id="0f093-319">**Municipality**</span></span>   |   <span data-ttu-id="0f093-320">l</span><span class="sxs-lookup"><span data-stu-id="0f093-320">l</span></span>   |     | <span data-ttu-id="0f093-321">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-321">Create + update</span></span> |
|  <span data-ttu-id="0f093-322">**Company**</span><span class="sxs-lookup"><span data-stu-id="0f093-322">**Company**</span></span>         | <span data-ttu-id="0f093-323">company</span><span class="sxs-lookup"><span data-stu-id="0f093-323">company</span></span>   |     |  <span data-ttu-id="0f093-324">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-324">Create + update</span></span> |
|  <span data-ttu-id="0f093-325">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="0f093-325">**CountryReferenceTwoLetter**</span></span>      |   <span data-ttu-id="0f093-326">co</span><span class="sxs-lookup"><span data-stu-id="0f093-326">co</span></span> |     |   <span data-ttu-id="0f093-327">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-327">Create + update</span></span> |
| <span data-ttu-id="0f093-328">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="0f093-328">**CountryReferenceTwoLetter**</span></span>    |  <span data-ttu-id="0f093-329">c</span><span class="sxs-lookup"><span data-stu-id="0f093-329">c</span></span>  |     |         <span data-ttu-id="0f093-330">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-330">Create + update</span></span> |
| <span data-ttu-id="0f093-331">**SupervisoryOrganization**</span><span class="sxs-lookup"><span data-stu-id="0f093-331">**SupervisoryOrganization**</span></span>  | <span data-ttu-id="0f093-332">department</span><span class="sxs-lookup"><span data-stu-id="0f093-332">department</span></span>  |     |  <span data-ttu-id="0f093-333">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-333">Create + update</span></span> |
|  <span data-ttu-id="0f093-334">**PreferredNameData**</span><span class="sxs-lookup"><span data-stu-id="0f093-334">**PreferredNameData**</span></span>  |  <span data-ttu-id="0f093-335">displayName</span><span class="sxs-lookup"><span data-stu-id="0f093-335">displayName</span></span> |     |   <span data-ttu-id="0f093-336">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-336">Create + update</span></span> |
| <span data-ttu-id="0f093-337">**EmployeeID**</span><span class="sxs-lookup"><span data-stu-id="0f093-337">**EmployeeID**</span></span>    |  <span data-ttu-id="0f093-338">cn</span><span class="sxs-lookup"><span data-stu-id="0f093-338">cn</span></span>    |   |   <span data-ttu-id="0f093-339">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="0f093-339">Written on create only</span></span> |
| <span data-ttu-id="0f093-340">**Fax**</span><span class="sxs-lookup"><span data-stu-id="0f093-340">**Fax**</span></span>      | <span data-ttu-id="0f093-341">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="0f093-341">facsimileTelephoneNumber</span></span>     |     |    <span data-ttu-id="0f093-342">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-342">Create + update</span></span> |
| <span data-ttu-id="0f093-343">**名字**</span><span class="sxs-lookup"><span data-stu-id="0f093-343">**FirstName**</span></span>   | <span data-ttu-id="0f093-344">givenName</span><span class="sxs-lookup"><span data-stu-id="0f093-344">givenName</span></span>       |     |    <span data-ttu-id="0f093-345">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-345">Create + update</span></span> |
| <span data-ttu-id="0f093-346">**Switch(\[Active\], , "0", "True", "1",)**</span><span class="sxs-lookup"><span data-stu-id="0f093-346">**Switch(\[Active\], , "0", "True", "1",)**</span></span> |  <span data-ttu-id="0f093-347">accountDisabled</span><span class="sxs-lookup"><span data-stu-id="0f093-347">accountDisabled</span></span>      |     | <span data-ttu-id="0f093-348">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-348">Create + update</span></span> |
| <span data-ttu-id="0f093-349">**Mobile**</span><span class="sxs-lookup"><span data-stu-id="0f093-349">**Mobile**</span></span>  |    <span data-ttu-id="0f093-350">mobile</span><span class="sxs-lookup"><span data-stu-id="0f093-350">mobile</span></span>       |     |       <span data-ttu-id="0f093-351">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="0f093-351">Written on create only</span></span> |
| <span data-ttu-id="0f093-352">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="0f093-352">**EmailAddress**</span></span>    | <span data-ttu-id="0f093-353">mail</span><span class="sxs-lookup"><span data-stu-id="0f093-353">mail</span></span>    |     |     <span data-ttu-id="0f093-354">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-354">Create + update</span></span> |
| <span data-ttu-id="0f093-355">**ManagerReference**</span><span class="sxs-lookup"><span data-stu-id="0f093-355">**ManagerReference**</span></span>   | <span data-ttu-id="0f093-356">manager</span><span class="sxs-lookup"><span data-stu-id="0f093-356">manager</span></span>  |     |  <span data-ttu-id="0f093-357">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-357">Create + update</span></span> |
| <span data-ttu-id="0f093-358">**WorkSpaceReference**</span><span class="sxs-lookup"><span data-stu-id="0f093-358">**WorkSpaceReference**</span></span> | <span data-ttu-id="0f093-359">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="0f093-359">physicalDeliveryOfficeName</span></span>    |     |  <span data-ttu-id="0f093-360">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-360">Create + update</span></span> |
| <span data-ttu-id="0f093-361">**PostalCode**</span><span class="sxs-lookup"><span data-stu-id="0f093-361">**PostalCode**</span></span>  |   <span data-ttu-id="0f093-362">postalCode</span><span class="sxs-lookup"><span data-stu-id="0f093-362">postalCode</span></span>  |     | <span data-ttu-id="0f093-363">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-363">Create + update</span></span> |
| <span data-ttu-id="0f093-364">**LocalReference**</span><span class="sxs-lookup"><span data-stu-id="0f093-364">**LocalReference**</span></span> |  <span data-ttu-id="0f093-365">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="0f093-365">preferredLanguage</span></span>  |     |  <span data-ttu-id="0f093-366">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-366">Create + update</span></span> |
| <span data-ttu-id="0f093-367">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span><span class="sxs-lookup"><span data-stu-id="0f093-367">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span></span>|<span data-ttu-id="0f093-368">\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**</span><span class="sxs-lookup"><span data-stu-id="0f093-368">\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**</span></span>      |    <span data-ttu-id="0f093-369">sAMAccountName</span><span class="sxs-lookup"><span data-stu-id="0f093-369">sAMAccountName</span></span>            |     |         <span data-ttu-id="0f093-370">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="0f093-370">Written on create only</span></span> |
| <span data-ttu-id="0f093-371">**姓氏**</span><span class="sxs-lookup"><span data-stu-id="0f093-371">**LastName**</span></span>   |   <span data-ttu-id="0f093-372">sn</span><span class="sxs-lookup"><span data-stu-id="0f093-372">sn</span></span>   |     |  <span data-ttu-id="0f093-373">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-373">Create + update</span></span> |
| <span data-ttu-id="0f093-374">**CountryRegionReference**</span><span class="sxs-lookup"><span data-stu-id="0f093-374">**CountryRegionReference**</span></span> |  <span data-ttu-id="0f093-375">st</span><span class="sxs-lookup"><span data-stu-id="0f093-375">st</span></span>     |     | <span data-ttu-id="0f093-376">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-376">Create + update</span></span> |
| <span data-ttu-id="0f093-377">**AddressLineData**</span><span class="sxs-lookup"><span data-stu-id="0f093-377">**AddressLineData**</span></span>    |  <span data-ttu-id="0f093-378">streetAddress</span><span class="sxs-lookup"><span data-stu-id="0f093-378">streetAddress</span></span>  |     |   <span data-ttu-id="0f093-379">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-379">Create + update</span></span> |
| <span data-ttu-id="0f093-380">**PrimaryWorkTelephone**</span><span class="sxs-lookup"><span data-stu-id="0f093-380">**PrimaryWorkTelephone**</span></span>  |  <span data-ttu-id="0f093-381">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="0f093-381">telephoneNumber</span></span>   |     | <span data-ttu-id="0f093-382">僅於建立時寫入</span><span class="sxs-lookup"><span data-stu-id="0f093-382">Written on create only</span></span> |
| <span data-ttu-id="0f093-383">**BusinessTitle**</span><span class="sxs-lookup"><span data-stu-id="0f093-383">**BusinessTitle**</span></span>   |  <span data-ttu-id="0f093-384">title</span><span class="sxs-lookup"><span data-stu-id="0f093-384">title</span></span>     |     |  <span data-ttu-id="0f093-385">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-385">Create + update</span></span> |
| <span data-ttu-id="0f093-386">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span><span class="sxs-lookup"><span data-stu-id="0f093-386">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span></span>   | <span data-ttu-id="0f093-387">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0f093-387">userPrincipalName</span></span>     |     | <span data-ttu-id="0f093-388">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-388">Create + update</span></span>                                                   
| <span data-ttu-id="0f093-389">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span><span class="sxs-lookup"><span data-stu-id="0f093-389">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span></span>  | <span data-ttu-id="0f093-390">parentDistinguishedName</span><span class="sxs-lookup"><span data-stu-id="0f093-390">parentDistinguishedName</span></span>     |     |  <span data-ttu-id="0f093-391">建立 + 更新</span><span class="sxs-lookup"><span data-stu-id="0f093-391">Create + update</span></span> |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a><span data-ttu-id="0f093-392">第 3 部分： Hello 在內部部署同步處理代理程式設定</span><span class="sxs-lookup"><span data-stu-id="0f093-392">Part 3: Configure hello on-premises synchronization agent</span></span>

<span data-ttu-id="0f093-393">在訂單 tooprovision tooActive 目錄在內部，必須 hello desire Active Directory 樹系中網域的伺服器上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="0f093-393">In order tooprovision tooActive Directory on-premises, an agent must be installed on a domain-joined server in hello desire Active Directory forest.</span></span> <span data-ttu-id="0f093-394">網域系統管理員 （或企業系統管理員） 完成 hello 程序所需的認證。</span><span class="sxs-lookup"><span data-stu-id="0f093-394">Domain admin (or Enterprise admin) credentials are required to complete hello procedure.</span></span>

<span data-ttu-id="0f093-395">**[您可以下載 hello 在內部部署同步處理代理程式在此](https://go.microsoft.com/fwlink/?linkid=847801)**</span><span class="sxs-lookup"><span data-stu-id="0f093-395">**[You can download hello on-premises synchronization agent here](https://go.microsoft.com/fwlink/?linkid=847801)**</span></span>

<span data-ttu-id="0f093-396">安裝代理程式之後, 執行以下 tooconfigure hello 代理程式，您的環境的 hello Powershell 命令。</span><span class="sxs-lookup"><span data-stu-id="0f093-396">After installing agent, run hello Powershell commands below tooconfigure hello agent for your environment.</span></span>

<span data-ttu-id="0f093-397">**命令 1**</span><span class="sxs-lookup"><span data-stu-id="0f093-397">**Command #1**</span></span>

> <span data-ttu-id="0f093-398">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span><span class="sxs-lookup"><span data-stu-id="0f093-398">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span></span>

> <span data-ttu-id="0f093-399">import-module AADSyncAgent.psd1</span><span class="sxs-lookup"><span data-stu-id="0f093-399">import-module AADSyncAgent.psd1</span></span>

<span data-ttu-id="0f093-400">**命令 2**</span><span class="sxs-lookup"><span data-stu-id="0f093-400">**Command #2**</span></span>

> <span data-ttu-id="0f093-401">Add-ADSyncAgentActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="0f093-401">Add-ADSyncAgentActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="0f093-402">輸入： 針對 [目錄名稱] 輸入 hello AD 樹系名稱，如同部分輸入\#2</span><span class="sxs-lookup"><span data-stu-id="0f093-402">Input: For "Directory Name", enter hello AD Forest name, as entered in part \#2</span></span>
* <span data-ttu-id="0f093-403">輸入：Active Directory 樹系的系統管理員使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="0f093-403">Input: Admin username and password for Active Directory forest</span></span>

<span data-ttu-id="0f093-404">**命令 3**</span><span class="sxs-lookup"><span data-stu-id="0f093-404">**Command #3**</span></span>

> <span data-ttu-id="0f093-405">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="0f093-405">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="0f093-406">輸入：Azure AD 租用戶的全域系統管理員使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="0f093-406">Input: Global admin username and password for your Azure AD tenant</span></span>

<span data-ttu-id="0f093-407">**命令 4**</span><span class="sxs-lookup"><span data-stu-id="0f093-407">**Command #4**</span></span>

> <span data-ttu-id="0f093-408">Get-AdSyncAgentProvisioningTasks</span><span class="sxs-lookup"><span data-stu-id="0f093-408">Get-AdSyncAgentProvisioningTasks</span></span>

* <span data-ttu-id="0f093-409">動作：確認已傳回資料。</span><span class="sxs-lookup"><span data-stu-id="0f093-409">Action: Confirm data is returned.</span></span> <span data-ttu-id="0f093-410">此命令會自動探索 Azure AD 租用戶中的 Workday 佈建應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f093-410">This command automatically discovers Workday provisioning apps in your Azure AD tenant.</span></span> <span data-ttu-id="0f093-411">範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="0f093-411">Example output:</span></span>

> <span data-ttu-id="0f093-412">名稱：我的 AD 樹系</span><span class="sxs-lookup"><span data-stu-id="0f093-412">Name          : My AD Forest</span></span>
>
> <span data-ttu-id="0f093-413">已啟用：True</span><span class="sxs-lookup"><span data-stu-id="0f093-413">Enabled       : True</span></span>
>
> <span data-ttu-id="0f093-414">DirectoryName：mydomain.contoso.com</span><span class="sxs-lookup"><span data-stu-id="0f093-414">DirectoryName : mydomain.contoso.com</span></span>
>
> <span data-ttu-id="0f093-415">已認證：False</span><span class="sxs-lookup"><span data-stu-id="0f093-415">Credentialed  : False</span></span>
>
> <span data-ttu-id="0f093-416">識別碼：WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span><span class="sxs-lookup"><span data-stu-id="0f093-416">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span></span>

<span data-ttu-id="0f093-417">**命令 5**</span><span class="sxs-lookup"><span data-stu-id="0f093-417">**Command #5**</span></span>

> <span data-ttu-id="0f093-418">Start-AdSyncAgentSynchronization -Automatic</span><span class="sxs-lookup"><span data-stu-id="0f093-418">Start-AdSyncAgentSynchronization -Automatic</span></span>

<span data-ttu-id="0f093-419">**命令 6**</span><span class="sxs-lookup"><span data-stu-id="0f093-419">**Command #6**</span></span>

> <span data-ttu-id="0f093-420">net stop aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="0f093-420">net stop aadsyncagent</span></span>

<span data-ttu-id="0f093-421">**命令 7**</span><span class="sxs-lookup"><span data-stu-id="0f093-421">**Command #7**</span></span>

> <span data-ttu-id="0f093-422">net start aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="0f093-422">net start aadsyncagent</span></span>

### <a name="part-4-start-hello-service"></a><span data-ttu-id="0f093-423">第 4 部分： 啟動 hello 服務</span><span class="sxs-lookup"><span data-stu-id="0f093-423">Part 4: Start hello service</span></span>
<span data-ttu-id="0f093-424">當組件 1-3 已完成之後時，您可以開始佈建服務 hello Azure 管理入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f093-424">Once parts 1-3 have been completed, you can start hello provisioning service back in hello Azure Management Portal.</span></span>

1.  <span data-ttu-id="0f093-425">在 hello**佈建**索引標籤，設定 hello**佈建狀態**至**上**。</span><span class="sxs-lookup"><span data-stu-id="0f093-425">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="0f093-426">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0f093-426">Click **Save**.</span></span>

3. <span data-ttu-id="0f093-427">這會啟動 hello 初始同步處理，這可能要花費數小時取決於使用者人數會 workday。</span><span class="sxs-lookup"><span data-stu-id="0f093-427">This will start hello initial sync, which can take a variable number of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="0f093-428">個別同步處理的事件，例如哪些使用者會讀出 Workday，以及之後加入或已更新 tooActive 目錄，然後可以在 hello 檢視**稽核記錄檔** 索引標籤。**[請參閱 hello 佈建上 tooread hello 稽核記錄的方式的詳細指示的報告指南](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="0f093-428">Individual sync events such as what users are being read out of  Workday, and then subsequently added or updated tooActive Directory,  can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5.  <span data-ttu-id="0f093-429">hello hello 代理程式電腦上的 Windows 應用程式記錄檔會顯示透過 hello 代理程式執行的所有作業。</span><span class="sxs-lookup"><span data-stu-id="0f093-429">hello Windows Application log on hello agent machine will show all operations performed via hello agent.</span></span>

6. <span data-ttu-id="0f093-430">完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0f093-430">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a><span data-ttu-id="0f093-432">設定使用者佈建 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f093-432">Configuring user provisioning tooAzure Active Directory</span></span>
<span data-ttu-id="0f093-433">設定佈建 tooAzure Active Directory 的方式將取決於您佈建的需求，在 hello 表中所述。</span><span class="sxs-lookup"><span data-stu-id="0f093-433">How you configure provisioning tooAzure Active Directory will depend on your provisioning requirements, as detailed in hello table below.</span></span>

| <span data-ttu-id="0f093-434">案例</span><span class="sxs-lookup"><span data-stu-id="0f093-434">Scenario</span></span> | <span data-ttu-id="0f093-435">方案</span><span class="sxs-lookup"><span data-stu-id="0f093-435">Solution</span></span> |
| -------- | -------- |
| <span data-ttu-id="0f093-436">**使用者需要佈建 toobe tooActive 目錄與 Azure AD**</span><span class="sxs-lookup"><span data-stu-id="0f093-436">**Users need toobe provisioned tooActive Directory and Azure AD**</span></span> | <span data-ttu-id="0f093-437">使用 **[AAD Connect](connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="0f093-437">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="0f093-438">**使用者需要佈建 toobe tooActive 目錄只**</span><span class="sxs-lookup"><span data-stu-id="0f093-438">**Users need toobe provisioned tooActive Directory only**</span></span> | <span data-ttu-id="0f093-439">使用 **[AAD Connect](connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="0f093-439">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="0f093-440">**使用者需要佈建 toobe tooAzure AD 唯一 （僅限雲端）**</span><span class="sxs-lookup"><span data-stu-id="0f093-440">**Users need toobe provisioned tooAzure AD only (cloud only)**</span></span> | <span data-ttu-id="0f093-441">使用 hello **Workday tooAzure Active Directory 佈建**hello 應用程式庫中的應用程式</span><span class="sxs-lookup"><span data-stu-id="0f093-441">Use hello **Workday tooAzure Active Directory provisioning** app in hello app gallery</span></span> |

<span data-ttu-id="0f093-442">如需設定 Azure AD Connect 的指示，請參閱 hello [Azure AD Connect 文件](connect/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="0f093-442">For instructions on setting up Azure AD Connect, see hello [Azure AD Connect documentation](connect/active-directory-aadconnect.md).</span></span>

<span data-ttu-id="0f093-443">hello 下列各節描述如何設定 Workday 和 Azure AD tooprovision 僅限雲端的使用者之間的連線。</span><span class="sxs-lookup"><span data-stu-id="0f093-443">hello following sections describe setting up a connection between Workday and Azure AD tooprovision cloud-only users.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f093-444">如果您需要佈建 toobe tooAzure AD 和不在內部部署 Active Directory 的僅限雲端的使用者，只能後面 hello 的下列程序。</span><span class="sxs-lookup"><span data-stu-id="0f093-444">Only follow hello procedure below if you have cloud-only users that need toobe provisioned tooAzure AD and not on-premises Active Directory.</span></span>

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="0f093-445">第 1 部分： 加入 hello Azure AD 佈建的連接器應用程式和建立 hello 連接 tooWorkday</span><span class="sxs-lookup"><span data-stu-id="0f093-445">Part 1: Adding hello Azure AD provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="0f093-446">**tooconfigure Workday tooAzure Active Directory 佈建為僅限雲端的使用者：**</span><span class="sxs-lookup"><span data-stu-id="0f093-446">**tooconfigure Workday tooAzure Active Directory provisioning for cloud-only users:**</span></span>

1.  <span data-ttu-id="0f093-447">跳過<https://portal.azure.com>。</span><span class="sxs-lookup"><span data-stu-id="0f093-447">Go too<https://portal.azure.com>.</span></span>

2.  <span data-ttu-id="0f093-448">在 hello 左的導覽列中，選取  **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="0f093-448">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="0f093-449">依序選取 [企業應用程式] 和 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0f093-449">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="0f093-450">選取**新增應用程式**，然後選取 hello**所有**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="0f093-450">Select **Add an application**, and then select hello **All** category.</span></span>

5.  <span data-ttu-id="0f093-451">搜尋**Workday tooAzure AD 佈建**，並從 hello 組件庫中加入該應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f093-451">Search for **Workday tooAzure AD provisioning**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="0f093-452">Hello 之後加入的應用程式，而且會顯示 hello 應用程式詳細資料 畫面中，選取**佈建**</span><span class="sxs-lookup"><span data-stu-id="0f093-452">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="0f093-453">變更 hello**佈建****模式**太**自動**</span><span class="sxs-lookup"><span data-stu-id="0f093-453">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="0f093-454">完整的 hello**系統管理員認證**區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0f093-454">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="0f093-455">**系統管理員使用者名稱**– 附加 hello 租用戶網域名稱輸入 hello hello Workday 的整合系統帳戶，使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0f093-455">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="0f093-456">其應該類似於：username@contoso4</span><span class="sxs-lookup"><span data-stu-id="0f093-456">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="0f093-457">**系統管理員密碼 –** Enter hello hello Workday 的整合系統帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="0f093-457">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="0f093-458">**租用戶 URL-**輸入您的租用戶 hello URL toohello Workday web 服務端點。</span><span class="sxs-lookup"><span data-stu-id="0f093-458">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="0f093-459">這應該看起來： https://wd3-impl-services1.workday.com/ccx/service/contoso4 其中 contoso4 會取代您正確租用戶的名稱，而 wd3 impl 會取代 hello 正確環境字串 （如有必要）。</span><span class="sxs-lookup"><span data-stu-id="0f093-459">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string (if necessary).</span></span>

   * <span data-ttu-id="0f093-460">**電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0f093-460">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="0f093-461">按一下 hello**測試連接** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f093-461">Click hello **Test Connection** button.</span></span>

   * <span data-ttu-id="0f093-462">如果 hello 連接測試成功，按一下 hello**儲存**hello 頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f093-462">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="0f093-463">如果失敗，，再次該 hello Workday 的 URL 是 Workday 中的有效認證。</span><span class="sxs-lookup"><span data-stu-id="0f093-463">If it fails, double-check that hello Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="0f093-464">第 2 部分：設定屬性對應</span><span class="sxs-lookup"><span data-stu-id="0f093-464">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="0f093-465">在本節中，您會針對僅限雲端使用者設定使用者資料從 Workday 流動至 Azure Active Directory 的方式。</span><span class="sxs-lookup"><span data-stu-id="0f093-465">In this section, you will configure how user data flows from Workday to Azure Active Directory for cloud-only users.</span></span>

1.  <span data-ttu-id="0f093-466">在 hello 佈建索引標籤下**對應**，按一下 **同步處理的背景工作 tooAzure AD**。</span><span class="sxs-lookup"><span data-stu-id="0f093-466">On hello Provisioning tab under **Mappings**, click **Synchronize Workers tooAzure AD**.</span></span>

2.   <span data-ttu-id="0f093-467">在 hello**來源物件範圍**欄位，您可以選取 Workday 中的使用者將應該提供 tooAzure AD，藉由定義一組屬性為基礎的篩選條件的範圍內。</span><span class="sxs-lookup"><span data-stu-id="0f093-467">In hello **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning tooAzure AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="0f093-468">hello 預設範圍為 「 Workday 中的所有使用者 」。</span><span class="sxs-lookup"><span data-stu-id="0f093-468">hello default scope is “all users in Workday”.</span></span> <span data-ttu-id="0f093-469">範例篩選：</span><span class="sxs-lookup"><span data-stu-id="0f093-469">Example filters:</span></span>

   * <span data-ttu-id="0f093-470">範例： 範圍 toousers 以背景工作識別碼 2000000 1000000 之間</span><span class="sxs-lookup"><span data-stu-id="0f093-470">Example: Scope toousers with Worker IDs between 1000000 and   2000000</span></span>

      * <span data-ttu-id="0f093-471">屬性：WorkerID</span><span class="sxs-lookup"><span data-stu-id="0f093-471">Attribute: WorkerID</span></span>

      * <span data-ttu-id="0f093-472">運算子：REGEX Match</span><span class="sxs-lookup"><span data-stu-id="0f093-472">Operator: REGEX Match</span></span>

      * <span data-ttu-id="0f093-473">值：(1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="0f093-473">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="0f093-474">範例：僅約聘人員和非正式員工</span><span class="sxs-lookup"><span data-stu-id="0f093-474">Example: Only contingent workers and not regular employees</span></span>

      * <span data-ttu-id="0f093-475">屬性：ContingentID</span><span class="sxs-lookup"><span data-stu-id="0f093-475">Attribute: ContingentID</span></span>

      * <span data-ttu-id="0f093-476">運算子：IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="0f093-476">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="0f093-477">在 hello**目標物件動作**欄位，您可以全域篩選允許 toobe 在 Azure AD 上執行哪些動作。</span><span class="sxs-lookup"><span data-stu-id="0f093-477">In hello **Target Object Actions** field, you can globally filter what actions are allowed toobe performed on Azure AD.</span></span> <span data-ttu-id="0f093-478">最常見的動作是 [建立] 和 [更新]。</span><span class="sxs-lookup"><span data-stu-id="0f093-478">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="0f093-479">在 [hello**屬性對應**] 區段中，您可以定義如何個別 Workday 對應 tooActive 目錄屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-479">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span>

5. <span data-ttu-id="0f093-480">按一下現有的屬性對應 tooupdate，或是按一下**加入新的對應**底部 hello hello 螢幕 tooadd 新對應。</span><span class="sxs-lookup"><span data-stu-id="0f093-480">Click on an existing attribute mapping tooupdate it, or click **Add new mapping** at hello bottom of hello screen tooadd new mappings.</span></span> <span data-ttu-id="0f093-481">個別屬性對應支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0f093-481">An individual attribute mapping supports these properties:</span></span>

   * <span data-ttu-id="0f093-482">**對應類型**</span><span class="sxs-lookup"><span data-stu-id="0f093-482">**Mapping Type**</span></span>

      * <span data-ttu-id="0f093-483">**直接**– 寫入 hello hello Workday 屬性 toohello AD 具有屬性值，任何變更</span><span class="sxs-lookup"><span data-stu-id="0f093-483">**Direct** – Writes hello value of hello Workday attribute         toohello AD attribute, with no changes</span></span>

      * <span data-ttu-id="0f093-484">**常數**-將靜態、 常數字串值寫入至 hello AD 屬性</span><span class="sxs-lookup"><span data-stu-id="0f093-484">**Constant** - Write a static, constant string value to         hello AD attribute</span></span>

      * <span data-ttu-id="0f093-485">**運算式**– 可讓您 toowrite hello AD 屬性，根據一個或多個新的 Workday 屬性的自訂值。</span><span class="sxs-lookup"><span data-stu-id="0f093-485">**Expression** – Allows you toowrite a custom value to hello AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="0f093-486">[如需詳細資訊，請參閱這篇有關運算式的文章](active-directory-saas-writing-expressions-for-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="0f093-486">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

   * <span data-ttu-id="0f093-487">**來源屬性**-從 Workday hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-487">**Source attribute** - hello user attribute from Workday.</span></span>

   * <span data-ttu-id="0f093-488">**預設值** – 選用。</span><span class="sxs-lookup"><span data-stu-id="0f093-488">**Default value** – Optional.</span></span> <span data-ttu-id="0f093-489">如果 hello 來源屬性的值是空的 hello 對應會改為寫入此值。</span><span class="sxs-lookup"><span data-stu-id="0f093-489">If hello source attribute has an empty value, hello mapping will write this value instead.</span></span>
            <span data-ttu-id="0f093-490">此空白 tooleave 最常見的組態。</span><span class="sxs-lookup"><span data-stu-id="0f093-490">Most common configuration is tooleave this blank.</span></span>

   * <span data-ttu-id="0f093-491">**目標屬性**– 在 Azure AD 中的 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-491">**Target attribute** – hello user attribute in Azure AD.</span></span>

   * <span data-ttu-id="0f093-492">**符合使用此屬性的物件**– 是否應使用此對應 toouniquely 識別 Workday 與 Azure AD 之間的使用者。</span><span class="sxs-lookup"><span data-stu-id="0f093-492">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between Workday and Azure AD.</span></span> <span data-ttu-id="0f093-493">這通常是背景工作 ID 欄位上設定，workday，通常在 Azure AD 中對應至 hello 員工 ID 屬性 （新） 或延伸模組屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-493">This is typically set on the Worker ID field for Workday, which is typically mapped to hello Employee ID attribute (new) or an extension attribute in Azure AD.</span></span>

   * <span data-ttu-id="0f093-494">**比對優先順序** – 您可以設定多個比對屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-494">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="0f093-495">具有多個屬性時，系統會以此欄位定義的順序進行評估。</span><span class="sxs-lookup"><span data-stu-id="0f093-495">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="0f093-496">只要找到相符項目，便不會評估進一步比對屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-496">As soon as a match is found, no further matching attributes are evaluated.</span></span>

   * <span data-ttu-id="0f093-497">**套用此對應**</span><span class="sxs-lookup"><span data-stu-id="0f093-497">**Apply this mapping**</span></span>

     * <span data-ttu-id="0f093-498">**一律** – 將此對應套用於使用者建立和更新動作</span><span class="sxs-lookup"><span data-stu-id="0f093-498">**Always** – Apply this mapping on both user creation          and update actions</span></span>

     * <span data-ttu-id="0f093-499">**僅限建立期間** - 僅將此對應套用於使用者建立動作</span><span class="sxs-lookup"><span data-stu-id="0f093-499">**Only during creation** - Apply this mapping only on          user creation actions</span></span>

6. <span data-ttu-id="0f093-500">toosave 對應時，按一下**儲存**頂端 hello 屬性對應的區段。</span><span class="sxs-lookup"><span data-stu-id="0f093-500">toosave your mappings, click **Save** at hello top of the      Attribute Mapping section.</span></span>

### <a name="part-3-start-hello-service"></a><span data-ttu-id="0f093-501">第 3 部分： 啟動 hello 服務</span><span class="sxs-lookup"><span data-stu-id="0f093-501">Part 3: Start hello service</span></span>
<span data-ttu-id="0f093-502">當組件 1-2 已經完成時，您可以開始佈建服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f093-502">Once parts 1-2 have been completed, you can start hello provisioning service.</span></span>

1.  <span data-ttu-id="0f093-503">在 hello**佈建**索引標籤，設定 hello**佈建狀態**至**上**。</span><span class="sxs-lookup"><span data-stu-id="0f093-503">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="0f093-504">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0f093-504">Click **Save**.</span></span>

3. <span data-ttu-id="0f093-505">這會啟動 hello 初始同步處理，這可能要花費數小時取決於使用者人數會 workday。</span><span class="sxs-lookup"><span data-stu-id="0f093-505">This will start hello initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="0f093-506">可以檢視個別的同步處理事件，在 hello**稽核記錄檔** 索引標籤。**[請參閱 hello 佈建上 tooread hello 稽核記錄的方式的詳細指示的報告指南](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="0f093-506">Individual sync events can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="0f093-507">完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0f093-507">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a><span data-ttu-id="0f093-508">設定電子郵件地址 tooWorkday 的回寫</span><span class="sxs-lookup"><span data-stu-id="0f093-508">Configuring writeback of email addresses tooWorkday</span></span>
<span data-ttu-id="0f093-509">從 Azure Active Directory tooWorkday 遵循這些指示 tooconfigure 回寫的使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0f093-509">Follow these instructions tooconfigure writeback of user email addresses from Azure Active Directory tooWorkday.</span></span>

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="0f093-510">第 1 部分： 加入 hello 佈建的連接器應用程式和建立 hello 連接 tooWorkday</span><span class="sxs-lookup"><span data-stu-id="0f093-510">Part 1: Adding hello provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="0f093-511">**tooconfigure Workday tooActive 目錄佈建：**</span><span class="sxs-lookup"><span data-stu-id="0f093-511">**tooconfigure Workday tooActive Directory provisioning:**</span></span>

1.  <span data-ttu-id="0f093-512">跳過<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="0f093-512">Go too<https://portal.azure.com></span></span>

2.  <span data-ttu-id="0f093-513">在 hello 左的導覽列中，選取  **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="0f093-513">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="0f093-514">依序選取 [企業應用程式] 和 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0f093-514">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="0f093-515">選取**新增應用程式**，然後選取 hello**所有**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="0f093-515">Select **Add an application**, then select hello **All** category.</span></span>

5.  <span data-ttu-id="0f093-516">搜尋**Workday 回寫**，並從 hello 組件庫中加入該應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f093-516">Search for **Workday Writeback**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="0f093-517">Hello 之後加入的應用程式，而且會顯示 hello 應用程式詳細資料 畫面中，選取**佈建**</span><span class="sxs-lookup"><span data-stu-id="0f093-517">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="0f093-518">變更 hello**佈建****模式**太**自動**</span><span class="sxs-lookup"><span data-stu-id="0f093-518">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="0f093-519">完整的 hello**系統管理員認證**區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0f093-519">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="0f093-520">**系統管理員使用者名稱**– 附加 hello 租用戶網域名稱輸入 hello hello Workday 的整合系統帳戶，使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0f093-520">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="0f093-521">其應該類似於：username@contoso4</span><span class="sxs-lookup"><span data-stu-id="0f093-521">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="0f093-522">**系統管理員密碼 –** Enter hello hello Workday 的整合系統帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="0f093-522">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="0f093-523">**租用戶 URL-**輸入您的租用戶 hello URL toohello Workday web 服務端點。</span><span class="sxs-lookup"><span data-stu-id="0f093-523">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="0f093-524">這應該看起來： https://wd3-impl-services1.workday.com/ccx/service/contoso4 其中 contoso4 會取代您正確租用戶的名稱，而 wd3 impl 會取代 hello 正確環境字串 （如有必要）。</span><span class="sxs-lookup"><span data-stu-id="0f093-524">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string (if necessary).</span></span>

   * <span data-ttu-id="0f093-525">**電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0f093-525">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="0f093-526">按一下 hello**測試連接** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f093-526">Click hello **Test Connection** button.</span></span> <span data-ttu-id="0f093-527">如果 hello 連接測試成功，按一下 hello**儲存**hello 頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f093-527">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="0f093-528">如果失敗，，再次該 hello Workday 的 URL 是 Workday 中的有效認證。</span><span class="sxs-lookup"><span data-stu-id="0f093-528">If it fails, double-check that hello Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="0f093-529">第 2 部分：設定屬性對應</span><span class="sxs-lookup"><span data-stu-id="0f093-529">Part 2: Configure attribute mappings</span></span> 


<span data-ttu-id="0f093-530">在本節中，您會設定使用者資料從 Workday 流動至 Active Directory 的方式。</span><span class="sxs-lookup"><span data-stu-id="0f093-530">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="0f093-531">在 hello 佈建索引標籤下**對應**，按一下 **同步處理 Azure AD 使用者 tooWorkday**。</span><span class="sxs-lookup"><span data-stu-id="0f093-531">On hello Provisioning tab under **Mappings**, click **Synchronize Azure AD Users tooWorkday**.</span></span>

2.  <span data-ttu-id="0f093-532">在 hello**來源物件範圍**欄位，您可以選擇性地篩選將 Azure Active Directory 中的使用者應該擁有電子郵件地址寫回 tooWorkday。</span><span class="sxs-lookup"><span data-stu-id="0f093-532">In hello **Source Object Scope** field, you can optionally filter which sets of users in Azure Active Directory should have their email addresses written back tooWorkday.</span></span> <span data-ttu-id="0f093-533">hello 預設範圍為 「 在 Azure AD 中的所有使用者 」。</span><span class="sxs-lookup"><span data-stu-id="0f093-533">hello default scope is “all users in Azure AD”.</span></span> 

3.  <span data-ttu-id="0f093-534">在 [hello**屬性對應**] 區段中，您可以定義如何個別 Workday 對應 tooActive 目錄屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-534">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span> <span data-ttu-id="0f093-535">沒有預設的 hello 電子郵件地址的對應。</span><span class="sxs-lookup"><span data-stu-id="0f093-535">There is a mapping for hello email address by default.</span></span> <span data-ttu-id="0f093-536">不過，符合識別碼的 hello 必須更新的 toomatch 使用者在其對應的項目與 workday 的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0f093-536">However, hello matching ID must be updated toomatch users in Azure AD with their corresponding entries in Workday.</span></span> <span data-ttu-id="0f093-537">受歡迎的比對方法 toosynchronize hello Workday 背景工作識別碼或員工識別碼在 Azure AD 中為 tooextensionAttribute1 15，然後在 Workday 在 Azure AD toomatch 使用者使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="0f093-537">A popular matching method is toosynchronize hello Workday worker ID or employee ID tooextensionAttribute1-15 in Azure AD, and then use this attribute in Azure AD toomatch users back in Workday.</span></span>

4.  <span data-ttu-id="0f093-538">您的對應，按一下 toosave**儲存**頂端 hello hello 屬性對應 > 一節。</span><span class="sxs-lookup"><span data-stu-id="0f093-538">toosave your mappings, click **Save** at hello top of hello Attribute Mapping section.</span></span>

### <a name="part-3-start-hello-service"></a><span data-ttu-id="0f093-539">第 3 部分： 啟動 hello 服務</span><span class="sxs-lookup"><span data-stu-id="0f093-539">Part 3: Start hello service</span></span>
<span data-ttu-id="0f093-540">當組件 1-2 已經完成時，您可以開始佈建服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f093-540">Once parts 1-2 have been completed, you can start hello provisioning service.</span></span>

1.  <span data-ttu-id="0f093-541">在 hello**佈建**索引標籤，設定 hello**佈建狀態**至**上**。</span><span class="sxs-lookup"><span data-stu-id="0f093-541">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="0f093-542">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0f093-542">Click **Save**.</span></span>

3. <span data-ttu-id="0f093-543">這會啟動 hello 初始同步處理，這可能要花費數小時取決於使用者人數會 workday。</span><span class="sxs-lookup"><span data-stu-id="0f093-543">This will start hello initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="0f093-544">可以檢視個別的同步處理事件，在 hello**稽核記錄檔** 索引標籤。**[請參閱 hello 佈建上 tooread hello 稽核記錄的方式的詳細指示的報告指南](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="0f093-544">Individual sync events can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="0f093-545">完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0f093-545">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0f093-546">已知問題</span><span class="sxs-lookup"><span data-stu-id="0f093-546">Known issues</span></span>

* <span data-ttu-id="0f093-547">**稽核記錄檔在歐洲地區設定中**-因為 hello 本版 technical preview 版本的已知的問題與 hello[稽核記錄檔](active-directory-saas-provisioning-reporting.md)hello Workday 連接器應用程式並未出現在 hello [的Azure入口網站](https://portal.azure.com)如果 hello Azure AD 租用戶位於歐洲的資料中心。</span><span class="sxs-lookup"><span data-stu-id="0f093-547">**Audit logs in European locales** - As of hello release of this technical preview, there is a known issue with hello [audit logs](active-directory-saas-provisioning-reporting.md) for hello Workday connector apps not appearing in hello [Azure portal](https://portal.azure.com) if hello Azure AD tenant resides in a European data center.</span></span> <span data-ttu-id="0f093-548">我們即將推出此問題的修正。</span><span class="sxs-lookup"><span data-stu-id="0f093-548">A fix for this issue is forthcoming.</span></span> <span data-ttu-id="0f093-549">請檢查此空間在 hello 附近未來更新一次。</span><span class="sxs-lookup"><span data-stu-id="0f093-549">Please check this space again in hello near future for updates.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0f093-550">其他資源</span><span class="sxs-lookup"><span data-stu-id="0f093-550">Additional resources</span></span>
* [<span data-ttu-id="0f093-551">教學課程：設定 Workday 與 Azure Active Directory 之間的單一登入</span><span class="sxs-lookup"><span data-stu-id="0f093-551">Tutorial: Configuring single sign-on between Workday and Azure Active Directory</span></span>](active-directory-saas-workday-tutorial.md)
* [<span data-ttu-id="0f093-552">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f093-552">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f093-553">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0f093-553">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="0f093-554">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f093-554">Next steps</span></span>

* [<span data-ttu-id="0f093-555">瞭解如何 tooreview 記錄並取得上佈建活動報表</span><span class="sxs-lookup"><span data-stu-id="0f093-555">Learn how tooreview logs and get reports on provisioning activity</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
