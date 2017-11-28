---
title: "aaaAzure IoT 套件與 Azure Active Directory |Microsoft 文件"
description: "描述 Azure IoT 套件如何使用 Azure Active Directory toomanage 權限。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="00fa2-103">Hello azureiotsuite.com 網站的權限</span><span class="sxs-lookup"><span data-stu-id="00fa2-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="00fa2-104">當您登入時會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="00fa2-104">What happens when you sign in</span></span>

<span data-ttu-id="00fa2-105">hello 第一次登入在[azureiotsuite.com][lnk-azureiotsuite]，hello 站台會決定 hello 權限等級，您根據擁有 hello 目前選取的 Azure Active Directory (AAD) 租用戶與 Azure訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="00fa2-106">首先，toopopulate hello 清單中看到的租用戶下一步 tooyour 使用者名稱，hello 站台會找出從 Azure 隸屬於哪一個 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="00fa2-107">目前，hello 站台只能取得一個租用戶的使用者權杖一次。</span><span class="sxs-lookup"><span data-stu-id="00fa2-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="00fa2-108">因此，當您切換使用 hello 右上角中的 hello 下拉式清單中的租用戶，hello 站台記錄您 toothat 租用戶 tooobtain hello 語彙基元中針對該租用戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="00fa2-109">接下來，hello 站台會找出從 Azure 選取租用戶的您擁有 hello 與相關聯的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="00fa2-110">當您建立新的預先設定的方案，您會看到 hello 可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="00fa2-111">最後，hello 網站擷取 hello 訂用帳戶中的所有 hello 資源，資源群組會標記為預先設定的解決方案，並於其中填入 hello hello 首頁上的磚。</span><span class="sxs-lookup"><span data-stu-id="00fa2-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="00fa2-112">hello 下列各節說明 hello 角色控制存取 toohello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="00fa2-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="00fa2-113">AAD 角色</span><span class="sxs-lookup"><span data-stu-id="00fa2-113">AAD roles</span></span>

<span data-ttu-id="00fa2-114">hello AAD 角色控制 hello 能力預先設定的佈建解決方案，並在預先設定的解決方案中管理使用者。</span><span class="sxs-lookup"><span data-stu-id="00fa2-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="00fa2-115">您可以在[在 Azure AD 中指派系統管理員角色][lnk-aad-admin]中的 AAD 找到有關使用者和系統管理員角色的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="00fa2-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="00fa2-116">hello 目前文件著重於 hello**全域管理員**和 hello**使用者**目錄角色所使用的 hello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="00fa2-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="00fa2-117">全域管理員</span><span class="sxs-lookup"><span data-stu-id="00fa2-117">Global administrator</span></span>

<span data-ttu-id="00fa2-118">每個 AAD 租用戶可以有很多全域系統管理員：</span><span class="sxs-lookup"><span data-stu-id="00fa2-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="00fa2-119">當您建立 AAD 租用戶時，您會由該租用戶的預設 hello 全域管理員。</span><span class="sxs-lookup"><span data-stu-id="00fa2-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="00fa2-120">hello 全域管理員可以佈建的預先設定的解決方案，而且會指派**Admin** hello 其 AAD 租用戶內的應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="00fa2-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="00fa2-121">如果另一位使用者在 hello 相同 AAD 租用戶建立的應用程式、 hello 預設角色授與 toohello 全域系統管理員是**ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="00fa2-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="00fa2-122">全域管理員可以指派使用 hello 應用程式的使用者 tooroles [Azure 入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="00fa2-123">網域使用者</span><span class="sxs-lookup"><span data-stu-id="00fa2-123">Domain user</span></span>

<span data-ttu-id="00fa2-124">每一個 AAD 租用戶可以有很多網域使用者：</span><span class="sxs-lookup"><span data-stu-id="00fa2-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="00fa2-125">網域使用者可以佈建的預先設定的解決方案，透過 hello [azureiotsuite.com] [ lnk-azureiotsuite]站台。</span><span class="sxs-lookup"><span data-stu-id="00fa2-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="00fa2-126">根據預設，hello 網域使用者被授與 hello **Admin** hello 中的角色佈建應用程式。</span><span class="sxs-lookup"><span data-stu-id="00fa2-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="00fa2-127">網域使用者可以建立應用程式使用 hello build.cmd 指令碼在 hello [azure iot-遠端-監視][lnk-rm-github-repo]， [azure iot-預測-維護][ lnk-pm-github-repo]，或[azure-iot-連線-原廠][ lnk-cf-github-repo]儲存機制。</span><span class="sxs-lookup"><span data-stu-id="00fa2-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="00fa2-128">不過，hello 預設角色授與 toohello 網域使用者是**ReadOnly**，因為網域使用者沒有權限 tooassign 角色。</span><span class="sxs-lookup"><span data-stu-id="00fa2-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="00fa2-129">如果 hello AAD 租用戶中的另一位使用者建立的應用程式，hello 網域使用者指派 hello **ReadOnly**依預設，該應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="00fa2-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="00fa2-130">網域使用者無法指派給角色給應用程式。因此，即使應用程式使用者佈建應用程式，網域使用者也無法針對應用程式的使用者新增使用者或角色。</span><span class="sxs-lookup"><span data-stu-id="00fa2-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="00fa2-131">來賓使用者</span><span class="sxs-lookup"><span data-stu-id="00fa2-131">Guest User</span></span>

<span data-ttu-id="00fa2-132">每一個 AAD 租用戶可以有很多來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="00fa2-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="00fa2-133">Guest 使用者 hello AAD 租用戶中有一組有限的權限。</span><span class="sxs-lookup"><span data-stu-id="00fa2-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="00fa2-134">如此一來，guest 使用者，無法佈建 hello AAD 租用戶中的預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="00fa2-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="00fa2-135">如需有關使用者和角色在 AAD 中的詳細資訊，請參閱 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="00fa2-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="00fa2-136">[在 Azure AD 中建立使用者][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="00fa2-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="00fa2-137">[指派使用者 tooapps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="00fa2-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="00fa2-138">Azure 訂用帳戶管理員角色</span><span class="sxs-lookup"><span data-stu-id="00fa2-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="00fa2-139">hello Azure 系統管理員角色來控制 hello 能力 toomap 的 Azure 訂用帳戶 tooan AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="00fa2-140">進一步了解 hello 文件中的 hello Azure 系統管理員角色[如何 tooadd 或變更 Azure 共同管理員、 服務管理員及帳戶管理員][lnk-admin-roles]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="00fa2-141">應用程式角色</span><span class="sxs-lookup"><span data-stu-id="00fa2-141">Application roles</span></span>

<span data-ttu-id="00fa2-142">hello 應用程式角色控制存取 toodevices 預先設定方案中。</span><span class="sxs-lookup"><span data-stu-id="00fa2-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="00fa2-143">在已佈建的應用程式中有兩個定義的角色和一個隱含角色：</span><span class="sxs-lookup"><span data-stu-id="00fa2-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="00fa2-144">**系統管理員：**具有完整控制權 tooadd，管理、 移除裝置，以及修改設定。</span><span class="sxs-lookup"><span data-stu-id="00fa2-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="00fa2-145">**唯讀：**可以檢視裝置、規則、動作、作業和遙測。</span><span class="sxs-lookup"><span data-stu-id="00fa2-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="00fa2-146">您可以找到 hello 權限指派中 hello tooeach 角色[RolePermissions.cs] [ lnk-resource-cs]原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="00fa2-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="00fa2-147">變更使用者的應用程式角色</span><span class="sxs-lookup"><span data-stu-id="00fa2-147">Changing application roles for a user</span></span>

<span data-ttu-id="00fa2-148">您可以使用下列程序 toomake 使用者部署 Active Directory 系統管理員的您預先設定的方案中的 hello。</span><span class="sxs-lookup"><span data-stu-id="00fa2-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="00fa2-149">您必須是使用者 AAD 全域管理員 toochange 角色：</span><span class="sxs-lookup"><span data-stu-id="00fa2-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="00fa2-150">移 toohello [Azure 入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="00fa2-151">選取 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="00fa2-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="00fa2-152">請確定您使用您選擇的 hello 目錄上 azureiotsuite.com 您佈建您的方案時。</span><span class="sxs-lookup"><span data-stu-id="00fa2-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="00fa2-153">如果您有多個訂用帳戶相關聯的目錄，您可以切換如果您按一下您在 hello 的右上方 hello 入口網站的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="00fa2-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="00fa2-154">依序按一下 [企業應用程式] 和 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="00fa2-155">顯示具有**任何**狀態的**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="00fa2-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="00fa2-156">然後搜尋具有預先設定解決方案名稱的應用程式。</span><span class="sxs-lookup"><span data-stu-id="00fa2-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="00fa2-157">按一下 hello 符合預先設定的方案名稱 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="00fa2-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="00fa2-158">按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="00fa2-159">選取您想要 tooswitch 角色 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="00fa2-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="00fa2-160">按一下**指派**和選取 hello 角色 (例如**Admin**) 您想要 tooassign toohello 使用者，按一下 hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="00fa2-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="00fa2-161">常見問題集</span><span class="sxs-lookup"><span data-stu-id="00fa2-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="00fa2-162">我的服務系統管理員，我希望我的訂閱與特定的 AAD 租用戶之間 toochange hello 目錄對應。</span><span class="sxs-lookup"><span data-stu-id="00fa2-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="00fa2-163">如何完成這項工作？</span><span class="sxs-lookup"><span data-stu-id="00fa2-163">How do I complete this task?</span></span>

1. <span data-ttu-id="00fa2-164">移 toohello [Azure 傳統入口網站][lnk-classic-portal]，按一下 **設定**hello 上 hello 左手邊服務清單中。</span><span class="sxs-lookup"><span data-stu-id="00fa2-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="00fa2-165">選取您想要到 toochange hello 目錄對應的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="00fa2-166">按一下 [編輯目錄] 。</span><span class="sxs-lookup"><span data-stu-id="00fa2-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="00fa2-167">選取 hello**目錄**希望 toouse hello 下拉式清單中的。</span><span class="sxs-lookup"><span data-stu-id="00fa2-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="00fa2-168">按一下 hello 正向箭號。</span><span class="sxs-lookup"><span data-stu-id="00fa2-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="00fa2-169">確認 hello 目錄對應，以及受影響的共同管理員。</span><span class="sxs-lookup"><span data-stu-id="00fa2-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="00fa2-170">如果您要從另一個目錄中移動，則會移除 hello 原始目錄中的 hello 共同管理員。</span><span class="sxs-lookup"><span data-stu-id="00fa2-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="00fa2-171">我是網域使用者/成員在 hello AAD 租用戶上，而且我已建立預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="00fa2-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="00fa2-172">如何獲得我的應用程式的角色？</span><span class="sxs-lookup"><span data-stu-id="00fa2-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="00fa2-173">您在 hello AAD 的全域管理員租用戶，然後將指派角色 toousers 自行要求全域管理員 toomake。</span><span class="sxs-lookup"><span data-stu-id="00fa2-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="00fa2-174">或者，請詢問全域管理員 tooassign 您直接的角色。</span><span class="sxs-lookup"><span data-stu-id="00fa2-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="00fa2-175">如果您想要 toochange hello AAD 租用戶已部署至您預先設定的方案，請參閱 hello 下一個問題。</span><span class="sxs-lookup"><span data-stu-id="00fa2-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="00fa2-176">我要如何切換 hello 指派給我的遠端監視的預先設定的解決方案和應用程式的 AAD 租用戶？</span><span class="sxs-lookup"><span data-stu-id="00fa2-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="00fa2-177">您可以從 <https://github.com/Azure/azure-iot-remote-monitoring> 執行雲端部署，並利用新建立的 AAD 租用戶重新部署。</span><span class="sxs-lookup"><span data-stu-id="00fa2-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="00fa2-178">因為您是根據預設，當您建立 AAD 租用戶的全域系統管理員權限 tooadd 使用者也可以 toothose 使用者指派角色。</span><span class="sxs-lookup"><span data-stu-id="00fa2-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="00fa2-179">建立 AAD 目錄中 hello [Azure 入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="00fa2-180">跳過<https://github.com/Azure/azure-iot-remote-monitoring>。</span><span class="sxs-lookup"><span data-stu-id="00fa2-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="00fa2-181">執行 `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (例如，`build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="00fa2-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="00fa2-182">出現提示時，設定 hello **tenantid** toobe 您新建立的租用戶，而不是您先前的租用戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="00fa2-183">我想 toochange 服務管理員或共同管理員，當使用 organisational 的帳戶登入</span><span class="sxs-lookup"><span data-stu-id="00fa2-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="00fa2-184">請參閱 hello 技術支援文件[變更服務管理員和共同管理員時的 organisational 帳戶登入時][lnk-service-admins]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="00fa2-185">為什麼出現以下錯誤？</span><span class="sxs-lookup"><span data-stu-id="00fa2-185">Why am I seeing this error?</span></span> <span data-ttu-id="00fa2-186">「 您的帳戶沒有 hello 適當的權限 toocreate 方案。</span><span class="sxs-lookup"><span data-stu-id="00fa2-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="00fa2-187">請洽詢您的帳戶管理員或嘗試使用不同的帳戶。」</span><span class="sxs-lookup"><span data-stu-id="00fa2-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="00fa2-188">查看下列指導方針的圖表 hello:</span><span class="sxs-lookup"><span data-stu-id="00fa2-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="00fa2-189">如果您繼續 toosee hello 錯誤驗證之後您 hello AAD 租用戶的全域系統管理員和共同管理員 hello 訂用帳戶，具有您的帳戶管理員移除 hello 使用者，並重新指派這個順序的必要權限。</span><span class="sxs-lookup"><span data-stu-id="00fa2-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="00fa2-190">首先，新增 hello 使用者的全域管理員身分，然後將使用者新增為 hello Azure 訂用帳戶的共同管理員。</span><span class="sxs-lookup"><span data-stu-id="00fa2-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="00fa2-191">如果問題持續發生，請連絡[說明與支援][lnk-help-support]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="00fa2-192">當我有 Azure 訂用帳戶時為何會出現此錯誤？</span><span class="sxs-lookup"><span data-stu-id="00fa2-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="00fa2-193">「 Azure 訂用帳戶是必要的 toocreate 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="00fa2-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="00fa2-194">只需要幾分鐘的時間，您就可以建立免費試用帳戶。」</span><span class="sxs-lookup"><span data-stu-id="00fa2-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="00fa2-195">如果您不確定您擁有 Azure 訂用帳戶，驗證 hello 租用戶訂用帳戶的對應，並確認 [hello] 下拉式清單中選取 hello 正確租用戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="00fa2-196">如果已驗證 hello 所需的租用戶是正確，請遵循上述圖表中的 hello，而且驗證 hello 對應您的訂閱，且此 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="00fa2-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00fa2-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00fa2-197">Next steps</span></span>
<span data-ttu-id="00fa2-198">toocontinue 深入了解 IoT 套件，請參閱 < 如何[來自訂預先設定的解決方案][lnk-customize]。</span><span class="sxs-lookup"><span data-stu-id="00fa2-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
