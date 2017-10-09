---
title: "aaaProtect 個人資料與 Azure 身分識別和存取控制項 |Microsoft 文件"
description: "使用 Azure 身分識別和存取控制項 toohelp 保護您的個人資料"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="fd041-103">Azure Active Directory 和 Multi-factor Authentication：使用身分識別和存取控制來保護個人資料</span><span class="sxs-lookup"><span data-stu-id="fd041-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="fd041-104">本文章提供資訊和程序，您可以使用 tooprotect 個人資料使用 Azure Active Directory 和多重要素驗證的安全性功能和服務。</span><span class="sxs-lookup"><span data-stu-id="fd041-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="fd041-105">案例</span><span class="sxs-lookup"><span data-stu-id="fd041-105">Scenario</span></span>

<span data-ttu-id="fd041-106">大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。</span><span class="sxs-lookup"><span data-stu-id="fd041-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="fd041-107">toosupport 努力，它所取得數個較小的出航行位於義大利，德國、 丹麥和 hello 英國</span><span class="sxs-lookup"><span data-stu-id="fd041-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="fd041-108">hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="fd041-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="fd041-109">其中包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="fd041-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="fd041-110">它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fd041-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="fd041-111">hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。</span><span class="sxs-lookup"><span data-stu-id="fd041-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="fd041-112">位於 hello 世界各地的公司員工存取 hello 網路從 hello 公司遠端辦公室和旅行代理程式已存取 toosome 公司資源。</span><span class="sxs-lookup"><span data-stu-id="fd041-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="fd041-113">問題陳述</span><span class="sxs-lookup"><span data-stu-id="fd041-113">Problem statement</span></span>

<span data-ttu-id="fd041-114">hello 公司必須保護客戶的和員工的個人資料 hello 隱私權的搜尋 toouse 盜用身分 toogain 存取的攻擊者。</span><span class="sxs-lookup"><span data-stu-id="fd041-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="fd041-115">它們也必須確定合法使用者將資料限制為只有使用者需要 toodo 該存取 toopersonal 他們的工作。</span><span class="sxs-lookup"><span data-stu-id="fd041-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="fd041-116">公司目標</span><span class="sxs-lookup"><span data-stu-id="fd041-116">Company goal</span></span>

<span data-ttu-id="fd041-117">hello 公司的目標是 tooensure 存取 toopersonal 資料會受到嚴格控制。</span><span class="sxs-lookup"><span data-stu-id="fd041-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="fd041-118">請務必識別身分的使用者存取 toopersonal 資料受到強式驗證。</span><span class="sxs-lookup"><span data-stu-id="fd041-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="fd041-119">[最小權限] 的原則，讓合法使用者擁有唯一的存取，以及沒有更多的 hello 層級，必須強制執行 (https://en.wikipedia.org/wiki/Principle_of_least_privilege)。</span><span class="sxs-lookup"><span data-stu-id="fd041-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="fd041-120">解決方案</span><span class="sxs-lookup"><span data-stu-id="fd041-120">Solutions</span></span>

<span data-ttu-id="fd041-121">Microsoft Azure 提供身分識別和存取管理工具 toohelp 公司控制著具有存取 tooresources 包含個人資料。</span><span class="sxs-lookup"><span data-stu-id="fd041-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="fd041-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd041-122">Azure Active Directory</span></span>

<span data-ttu-id="fd041-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) 管理身分識別，並控制存取 tooAzure，以及其他內部部署其他雲端資源、 資料和應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd041-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="fd041-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)協助 Azure 系統管理員 toominimize hello 許多人都有存取 toocertain 資訊，例如個人資料。</span><span class="sxs-lookup"><span data-stu-id="fd041-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="fd041-125">它可讓他們 toodiscover、 限制，並監視特殊權限的身分識別及存取 tooresources 和 tooassign 暫時性的 Just-In-Time (JIT) 系統管理權限 tooeligible 使用者。</span><span class="sxs-lookup"><span data-stu-id="fd041-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="fd041-126">它也可供深入了解具有 AAD 系統管理員權限的人員。</span><span class="sxs-lookup"><span data-stu-id="fd041-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="fd041-127">在使用 AAD PIM hello 活動包括：</span><span class="sxs-lookup"><span data-stu-id="fd041-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="fd041-128">為您的目錄啟用 Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="fd041-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="fd041-129">使用 Privileged Identity Management 系統管理儀表板 toosee 重要資訊一目了然</span><span class="sxs-lookup"><span data-stu-id="fd041-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="fd041-130">新增或移除永久或符合資格的系統管理員 tooeach 角色來管理 hello 特殊權限身分識別 （系統管理員）</span><span class="sxs-lookup"><span data-stu-id="fd041-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="fd041-131">設定 hello 角色啟用</span><span class="sxs-lookup"><span data-stu-id="fd041-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="fd041-132">啟用角色</span><span class="sxs-lookup"><span data-stu-id="fd041-132">Activating roles</span></span>

- <span data-ttu-id="fd041-133">檢閱角色活動</span><span class="sxs-lookup"><span data-stu-id="fd041-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="fd041-134">如何啟用 ADD PIM？</span><span class="sxs-lookup"><span data-stu-id="fd041-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="fd041-135">為您的目錄中，使用 PIM toostart 不要遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="fd041-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="fd041-136">登入 toohello Azure 入口網站為您的目錄的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="fd041-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="fd041-137">如果您的組織具有多個目錄，選取您的使用者名稱 hello 右上角的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="fd041-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="fd041-138">選取您將在其中使用 Azure AD Privileged Identity Management hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="fd041-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="fd041-139">選取**更多服務**並用 hello**篩選**文字方塊 toosearch 的 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="fd041-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="fd041-140">請檢查**Pin toodashboard** ，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="fd041-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="fd041-141">hello Privileged Identity Management 的應用程式會開啟。</span><span class="sxs-lookup"><span data-stu-id="fd041-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="fd041-142">一旦設定 Azure AD Privileged Identity Management 之後，每當您開啟 hello 應用程式時看到 hello 瀏覽 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fd041-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="fd041-143">如需開始使用 AAD PIM 的詳細資訊和指示，請參閱[開始使用 Azure AD Privileged Identity Management](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="fd041-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="fd041-144">Azure 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="fd041-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="fd041-145">[Azure 角色型存取控制](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)(RBAC) 可協助管理存取 tooAzure 資源啟用 hello 授與的存取權限 hello 使用者指派角色的 Azure 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="fd041-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="fd041-146">您可以隔離小組內的責任，並授與僅 hello 數量存取 toousers、 群組和應用程式，它們必須 tooperform 他們的工作。</span><span class="sxs-lookup"><span data-stu-id="fd041-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="fd041-147">可以授與以角色為基礎的存取權 toousers 使用 hello Azure 入口網站、 Azure 命令列工具或 Azure 管理 Api。</span><span class="sxs-lookup"><span data-stu-id="fd041-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="fd041-148">如需有關 Azure rbac 進行基本概念的詳細資訊，請參閱[開始使用 hello Azure 入口網站中的 角色型存取控制。](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="fd041-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="fd041-149">如何使用 PowerShell 管理 Azure RBAC？</span><span class="sxs-lookup"><span data-stu-id="fd041-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="fd041-150">您可以使用 PowerShell cmdlet toomanage Azure rbac 進行，包括下列管理工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="fd041-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="fd041-151">列出角色</span><span class="sxs-lookup"><span data-stu-id="fd041-151">List roles</span></span>

- <span data-ttu-id="fd041-152">查看誰具有存取權</span><span class="sxs-lookup"><span data-stu-id="fd041-152">See who has access</span></span>

- <span data-ttu-id="fd041-153">授與存取權</span><span class="sxs-lookup"><span data-stu-id="fd041-153">Grant access</span></span>

- <span data-ttu-id="fd041-154">移除存取</span><span class="sxs-lookup"><span data-stu-id="fd041-154">Remove access</span></span>

- <span data-ttu-id="fd041-155">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="fd041-155">Create a custom role</span></span>

- <span data-ttu-id="fd041-156">取得資源提供者的動作</span><span class="sxs-lookup"><span data-stu-id="fd041-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="fd041-157">修改自訂角色</span><span class="sxs-lookup"><span data-stu-id="fd041-157">Modify a custom role</span></span>

- <span data-ttu-id="fd041-158">刪除自訂角色</span><span class="sxs-lookup"><span data-stu-id="fd041-158">Delete a custom role</span></span>

- <span data-ttu-id="fd041-159">列出自訂角色</span><span class="sxs-lookup"><span data-stu-id="fd041-159">List custom roles</span></span>

<span data-ttu-id="fd041-160">如需有關如何 toomanage Azure RBAC 使用 PowerShell，請參閱指示[使用 Azure PowerShell 管理角色為基礎的存取](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell)。</span><span class="sxs-lookup"><span data-stu-id="fd041-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="fd041-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="fd041-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="fd041-162">[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) 是協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求的兩步驟驗證解決方案。</span><span class="sxs-lookup"><span data-stu-id="fd041-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="fd041-163">它可以透過一些驗證方法 (包括電話、文字訊息，或行動應用程式驗證) 來提供強大的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="fd041-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="fd041-164">toodeploy MFA hello Azure 雲端中的，您需要 toofirst 啟用它，然後再開啟雙步驟驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="fd041-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="fd041-165">如何啟用 Azure toouse MFA？</span><span class="sxs-lookup"><span data-stu-id="fd041-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="fd041-166">如果您的使用者包括 Azure Multi-factor Authentication Server 的授權，並沒有您需要 Azure MFA 上的 toodo tooturn。</span><span class="sxs-lookup"><span data-stu-id="fd041-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="fd041-167">如果沒有，您需要在您的目錄中的 toocreate Multi-factor Auth 提供者。</span><span class="sxs-lookup"><span data-stu-id="fd041-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="fd041-168">toodo，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fd041-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="fd041-169">選取**Active Directory** hello Azure 傳統入口網站 （登入為系統管理員） 中。</span><span class="sxs-lookup"><span data-stu-id="fd041-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="fd041-170">選取 [Multi-Factor Authentication Provider]。</span><span class="sxs-lookup"><span data-stu-id="fd041-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="fd041-171">選取 [新增]，然後在 [應用程式服務] 之下，選取 [Multi-Factor Auth Provider]。</span><span class="sxs-lookup"><span data-stu-id="fd041-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="fd041-172">選取 [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="fd041-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="fd041-173">填寫 hello 名稱 欄位中，選取 （每次驗證或每個啟用的使用者） 的使用方式模型。</span><span class="sxs-lookup"><span data-stu-id="fd041-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="fd041-174">指定哪些 hello MFA 提供者所關聯的目錄。</span><span class="sxs-lookup"><span data-stu-id="fd041-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="fd041-175">按一下 hello**建立** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fd041-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="fd041-176">如需有關的詳細指示 toomanage 您 Multi-factor Auth 提供者，請參閱[開始使用 Azure Multi-factor Auth 提供者。](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="fd041-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="fd041-177">如何對使用者開啟雙步驟驗證？</span><span class="sxs-lookup"><span data-stu-id="fd041-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="fd041-178">您可以強制執行雙步驟驗證的所有登入，或您在特定條件時，才可以建立條件式存取原則 toorequire 雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="fd041-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="fd041-179">Azure MFA 啟用藉由變更使用者的狀態是 hello 要求雙步驟驗證的傳統方式。</span><span class="sxs-lookup"><span data-stu-id="fd041-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="fd041-180">您所啟用的所有 hello 使用者都會都將每次登入時 hello 相同需求 tooperform 雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="fd041-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="fd041-181">啟用使用者的效力會凌駕任何可能影響該使用者的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="fd041-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="fd041-182">使用條件式存取原則來啟用 Azure MFA 是用來要求使用雙步驟驗證的更彈性方法。</span><span class="sxs-lookup"><span data-stu-id="fd041-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="fd041-183">您可以建立適用於 toogroups 與個別使用者的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="fd041-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="fd041-184">您可以對高風險群組施加比低風險群組更多的限制，或者，也可以只針對高風險雲端應用程式要求雙步驟驗證，至於低風險的雲端應用程式則略過雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="fd041-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="fd041-185">不過，條件式存取是 Azure Active Directory 的付費功能。</span><span class="sxs-lookup"><span data-stu-id="fd041-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="fd041-186">tooenable MFA 藉由變更使用者狀態，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="fd041-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="fd041-187">Toohello Azure 入口網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="fd041-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="fd041-188">跳過**Azure Active Directory\>使用者和群組\>所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="fd041-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="fd041-189">選取 [多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="fd041-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="fd041-190">您為 Azure MFA 想 tooenable 尋找 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="fd041-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="fd041-191">您可能需要 toochange hello hello 頂端的檢視。</span><span class="sxs-lookup"><span data-stu-id="fd041-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="fd041-192">請檢查 hello 方塊下一步 toohello 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="fd041-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="fd041-193">在 hello 右下快速步驟，選擇**啟用**。</span><span class="sxs-lookup"><span data-stu-id="fd041-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="fd041-194">確認您的選擇會開啟 hello 快顯視窗中。</span><span class="sxs-lookup"><span data-stu-id="fd041-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="fd041-195">針對已啟用 MFA 的使用者將會詢問 tooregister hello 下一次登入。</span><span class="sxs-lookup"><span data-stu-id="fd041-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="fd041-196">條件式存取原則，tooenable Azure MFA 進行 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="fd041-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="fd041-197">Toohello Azure 入口網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="fd041-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="fd041-198">跳過**Azure Active Directory\>條件式存取**。</span><span class="sxs-lookup"><span data-stu-id="fd041-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="fd041-199">選取 [新增原則]。</span><span class="sxs-lookup"><span data-stu-id="fd041-199">Select **New policy**.</span></span>

4. <span data-ttu-id="fd041-200">在 [指派] 底下選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fd041-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="fd041-201">使用 hello **Include**和**排除**toospecify hello 原則將管理哪些使用者和群組的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fd041-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="fd041-202">在 [指派] 底下選取 [雲端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fd041-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="fd041-203">選擇太**包含所有雲端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fd041-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="fd041-204">在 [存取控制] 底下選取 [授與]。</span><span class="sxs-lookup"><span data-stu-id="fd041-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="fd041-205">選擇 [需要多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="fd041-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="fd041-206">開啟**啟用原則**太**上**，然後選取 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="fd041-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="fd041-207">如需如何設定詐騙警示 tooconfigure Azure MFA 設定 tooset 建立單次許可時，使用自訂語音訊息、 設定快取、 指定受信任的 Ip、 建立應用程式密碼、 啟用記住裝置信任的使用者，並選取 MFA驗證方法，請參閱[設定 Azure Multi-factor Authentication 設定。](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="fd041-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd041-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd041-208">Next steps</span></span>

- [<span data-ttu-id="fd041-209">保護 Azure AD 中的特殊權限存取</span><span class="sxs-lookup"><span data-stu-id="fd041-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="fd041-210">與 Azure Multi-Factor Authentication 相關的常見問題</span><span class="sxs-lookup"><span data-stu-id="fd041-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="fd041-211">角色型存取控制疑難排解</span><span class="sxs-lookup"><span data-stu-id="fd041-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="fd041-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="fd041-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
