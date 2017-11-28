---
title: "aaaAzure Active Directory Connect Health 作業"
description: "本文說明可以在您部署 Azure AD Connect Health 之後執行的其他作業。"
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a><span data-ttu-id="5e8d0-103">Azure Active Directory Connect Health 作業</span><span class="sxs-lookup"><span data-stu-id="5e8d0-103">Azure Active Directory Connect Health operations</span></span>
<span data-ttu-id="5e8d0-104">本主題描述 hello 各種作業，您可以執行使用 Azure Active Directory (Azure AD) 連線的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-104">This topic describes hello various operations you can perform by using Azure Active Directory (Azure AD) Connect Health.</span></span>

## <a name="enable-email-notifications"></a><span data-ttu-id="5e8d0-105">啟用電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="5e8d0-105">Enable email notifications</span></span>
<span data-ttu-id="5e8d0-106">警示會指出您的身分識別基礎結構不是狀況良好時，您可以設定 hello Azure AD Connect Health 服務 toosend 電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-106">You can configure hello Azure AD Connect Health service toosend email notifications when alerts indicate that your identity infrastructure is not healthy.</span></span> <span data-ttu-id="5e8d0-107">產生警示和解決警示時會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-107">This occurs when an alert is generated, and when it is resolved.</span></span>

![Azure AD Connect Health 電子郵件通知設定的螢幕擷取畫面](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> <span data-ttu-id="5e8d0-109">依預設會啟用電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-109">Email notifications are enabled by default.</span></span>
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a><span data-ttu-id="5e8d0-110">tooenable Azure AD Connect Health 電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="5e8d0-110">tooenable Azure AD Connect Health email notifications</span></span>
1. <span data-ttu-id="5e8d0-111">開啟 hello**警示**刀鋒視窗中，您會想 tooreceive 電子郵件通知的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-111">Open hello **Alerts** blade for hello service for which you want tooreceive email notification.</span></span>
2. <span data-ttu-id="5e8d0-112">在 hello 動作列中，按一下**通知設定**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-112">From hello action bar, click **Notification Settings**.</span></span>
3. <span data-ttu-id="5e8d0-113">在 hello 電子郵件通知交換器中，選取**ON**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-113">At hello email notification switch, select **ON**.</span></span>
4. <span data-ttu-id="5e8d0-114">如果您想要所有全域管理員 tooreceive 電子郵件通知，請選取 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-114">Select hello check box if you want all global administrators tooreceive email notifications.</span></span>
5. <span data-ttu-id="5e8d0-115">如果您想在任何其他的電子郵件地址 tooreceive 電子郵件通知，來指定 hello**其他電子郵件收件者**方塊。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-115">If you want tooreceive email notifications at any other email addresses, specify them in hello **Additional Email Recipients** box.</span></span> <span data-ttu-id="5e8d0-116">這份清單中，從電子郵件地址 tooremove hello 項目上按一下滑鼠右鍵，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-116">tooremove an email address from this list, right-click hello entry and select **Delete**.</span></span>
6. <span data-ttu-id="5e8d0-117">toofinalize hello 變更，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-117">toofinalize hello changes, click **Save**.</span></span> <span data-ttu-id="5e8d0-118">只有在您儲存之後，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-118">Changes take effect only after you save.</span></span>

## <a name="delete-a-server-or-service-instance"></a><span data-ttu-id="5e8d0-119">刪除伺服器或服務執行個體</span><span class="sxs-lookup"><span data-stu-id="5e8d0-119">Delete a server or service instance</span></span>

<span data-ttu-id="5e8d0-120">在某些情況下，您可能想 tooremove 從受監視的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-120">In some instances, you might want tooremove a server from being monitored.</span></span> <span data-ttu-id="5e8d0-121">以下是您的需要 tooknow tooremove hello Azure AD Connect Health 服務中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-121">Here's what you need tooknow tooremove a server from hello Azure AD Connect Health service.</span></span>

<span data-ttu-id="5e8d0-122">當您要刪除伺服器時，請注意下列 hello:</span><span class="sxs-lookup"><span data-stu-id="5e8d0-122">When you're deleting a server, be aware of hello following:</span></span>

* <span data-ttu-id="5e8d0-123">這個動作會停止從該伺服器收集任何進一步的資料。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-123">This action stops collecting any further data from that server.</span></span> <span data-ttu-id="5e8d0-124">此伺服器會從監視服務的 hello 移除。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-124">This server is removed from hello monitoring service.</span></span> <span data-ttu-id="5e8d0-125">此動作之後, 您不能 tooview 新警示、 監視或此伺服器的使用方式分析資料。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-125">After this action, you are not able tooview new alerts, monitoring, or usage analytics data for this server.</span></span>
* <span data-ttu-id="5e8d0-126">此動作不會解除安裝 hello 健康情況代理程式從您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-126">This action does not uninstall hello Health Agent from your server.</span></span> <span data-ttu-id="5e8d0-127">如果您不解除安裝然後再執行此步驟中的 hello 健康情況代理程式，您可能會看到 hello 伺服器上的錯誤相關的 toohello 健康情況代理程式。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-127">If you have not uninstalled hello Health Agent before performing this step, you might see errors related toohello Health Agent on hello server.</span></span>
* <span data-ttu-id="5e8d0-128">此動作不會刪除 hello 從這部伺服器已收集的資料。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-128">This action does not delete hello data already collected from this server.</span></span> <span data-ttu-id="5e8d0-129">根據 hello Azure 資料保留原則會刪除該資料。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-129">That data is deleted in accordance with hello Azure data retention policy.</span></span>
* <span data-ttu-id="5e8d0-130">之後執行此動作，如果您想要監視 toostart hello 相同的伺服器同樣地，您必須解除安裝，並在此伺服器上重新安裝 hello 健康情況代理程式。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-130">After performing this action, if you want toostart monitoring hello same server again, you must uninstall and reinstall hello Health Agent on this server.</span></span>

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a><span data-ttu-id="5e8d0-131">toodelete hello Azure AD Connect Health 服務中的伺服器</span><span class="sxs-lookup"><span data-stu-id="5e8d0-131">toodelete a server from hello Azure AD Connect Health service</span></span>
<span data-ttu-id="5e8d0-132">適用於 Active Directory 同盟服務 (AD FS) 和 Azure AD Connect (Sync) 的 Azure AD Connect Health：</span><span class="sxs-lookup"><span data-stu-id="5e8d0-132">Azure AD Connect Health for Active Directory Federation Services (AD FS) and Azure AD Connect (Sync):</span></span>

1. <span data-ttu-id="5e8d0-133">開啟 hello**伺服器**刀鋒視窗中的 hello**伺服器清單**選取 hello 伺服器名稱 toobe 刀鋒視窗中移除。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-133">Open hello **Server** blade from hello **Server List** blade by selecting hello server name toobe removed.</span></span>
2. <span data-ttu-id="5e8d0-134">在 hello**伺服器**刀鋒視窗中的，在 hello 動作列中，按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-134">On hello **Server** blade, from hello action bar, click **Delete**.</span></span>
3. <span data-ttu-id="5e8d0-135">確認 hello 確認方塊中輸入 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-135">Confirm by typing hello server name in hello confirmation box.</span></span>
4. <span data-ttu-id="5e8d0-136">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-136">Click **Delete**.</span></span>

<span data-ttu-id="5e8d0-137">Azure AD Connect Health for Azure Active Directory Domain Services：</span><span class="sxs-lookup"><span data-stu-id="5e8d0-137">Azure AD Connect Health for Azure Active Directory Domain Services:</span></span>

1. <span data-ttu-id="5e8d0-138">開啟 hello**網域控制站**儀表板。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-138">Open hello **Domain Controllers** dashboard.</span></span>
2. <span data-ttu-id="5e8d0-139">選取 hello 網域控制站 toobe 移除。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-139">Select hello domain controller toobe removed.</span></span>
3. <span data-ttu-id="5e8d0-140">在 hello 動作列中，按一下**選取 刪除**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-140">From hello action bar, click **Delete Selected**.</span></span>
4. <span data-ttu-id="5e8d0-141">確認 hello 動作 toodelete hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-141">Confirm hello action toodelete hello server.</span></span>
5. <span data-ttu-id="5e8d0-142">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-142">Click **Delete**.</span></span>

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a><span data-ttu-id="5e8d0-143">從 Azure AD Connect Health 服務刪除服務執行個體</span><span class="sxs-lookup"><span data-stu-id="5e8d0-143">Delete a service instance from Azure AD Connect Health service</span></span>
<span data-ttu-id="5e8d0-144">在某些情況下，您可能想 tooremove 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-144">In some instances, you might want tooremove a service instance.</span></span> <span data-ttu-id="5e8d0-145">以下是您需要 tooknow tooremove 服務執行個體從 hello Azure AD Connect Health 服務。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-145">Here's what you need tooknow tooremove a service instance from hello Azure AD Connect Health service.</span></span>

<span data-ttu-id="5e8d0-146">當您要刪除的服務執行個體時，請注意下列 hello:</span><span class="sxs-lookup"><span data-stu-id="5e8d0-146">When you're deleting a service instance, be aware of hello following:</span></span>

* <span data-ttu-id="5e8d0-147">這個動作會移除從監視服務的 hello hello 目前服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-147">This action removes hello current service instance from hello monitoring service.</span></span>
* <span data-ttu-id="5e8d0-148">此動作不解除安裝或移除任何受監視的此服務執行個體一部分 hello 伺服器 hello 健康情況代理程式。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-148">This action does not uninstall or remove hello Health Agent from any of hello servers that were monitored as part of this service instance.</span></span> <span data-ttu-id="5e8d0-149">如果您不解除安裝然後再執行此步驟中的 hello 健康情況代理程式，您可能會看到錯誤相關的 toohello 健康情況代理程式在 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-149">If you have not uninstalled hello Health Agent before performing this step, you might see errors related toohello Health Agent on hello servers.</span></span>
* <span data-ttu-id="5e8d0-150">此服務執行個體的所有資料會根據 hello Azure 資料保留原則都刪除。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-150">All data from this service instance is deleted in accordance with hello Azure data retention policy.</span></span>
* <span data-ttu-id="5e8d0-151">執行此動作之後，如果您想 toostart 監視 hello 服務時，解除安裝，並在 hello 的所有伺服器上重新安裝 hello 健康情況代理程式。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-151">After performing this action, if you want toostart monitoring hello service, uninstall and reinstall hello Health Agent on all hello servers.</span></span> <span data-ttu-id="5e8d0-152">執行此動作之後，如果您想要監視相同的伺服器同樣地，解除安裝、 重新安裝，然後將註冊的 hello toostart 會 hello 健康情況代理程式在該伺服器上。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-152">After performing this action, if you want toostart monitoring hello same server again, uninstall, reinstall, and register hello Health Agent on that server.</span></span>

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a><span data-ttu-id="5e8d0-153">toodelete 從 hello Azure AD Connect Health 服務的服務執行個體</span><span class="sxs-lookup"><span data-stu-id="5e8d0-153">toodelete a service instance from hello Azure AD Connect Health service</span></span>
1. <span data-ttu-id="5e8d0-154">開啟 hello**服務**刀鋒視窗中的 hello**服務清單**刀鋒視窗中的選取您想 tooremove hello service 識別碼 （陣列名稱）。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-154">Open hello **Service** blade from hello **Service List** blade by selecting hello service identifier (farm name) that you want tooremove.</span></span>
2. <span data-ttu-id="5e8d0-155">在 hello**伺服器**刀鋒視窗中的，在 hello 動作列中，按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-155">On hello **Server** blade, from hello action bar, click **Delete**.</span></span>
3. <span data-ttu-id="5e8d0-156">確認 hello 確認方塊中輸入 hello 服務名稱 (例如： sts.contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-156">Confirm by typing hello service name in hello confirmation box (for example: sts.contoso.com).</span></span>
4. <span data-ttu-id="5e8d0-157">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-157">Click **Delete**.</span></span>
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a><span data-ttu-id="5e8d0-158">使用角色型存取控制來管理存取</span><span class="sxs-lookup"><span data-stu-id="5e8d0-158">Manage access with Role-Based Access Control</span></span>
<span data-ttu-id="5e8d0-159">[角色型存取控制 (RBAC)](../role-based-access-control-configure.md) Azure AD Connect Health 提供存取 toousers 和全域系統管理員以外的群組。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-159">[Role-Based Access Control (RBAC)](../role-based-access-control-configure.md) for Azure AD Connect Health provides access toousers and groups other than global administrators.</span></span> <span data-ttu-id="5e8d0-160">RBAC 角色 toohello 適合使用者和群組，並提供一個機制，在您的目錄 toolimit hello 全域管理員。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-160">RBAC assigns roles toohello intended users and groups, and provides a mechanism toolimit hello global administrators within your directory.</span></span>

### <a name="roles"></a><span data-ttu-id="5e8d0-161">角色</span><span class="sxs-lookup"><span data-stu-id="5e8d0-161">Roles</span></span>
<span data-ttu-id="5e8d0-162">Azure AD Connect Health 支援 hello 下列內建的角色：</span><span class="sxs-lookup"><span data-stu-id="5e8d0-162">Azure AD Connect Health supports hello following built-in roles:</span></span>

| <span data-ttu-id="5e8d0-163">角色</span><span class="sxs-lookup"><span data-stu-id="5e8d0-163">Role</span></span> | <span data-ttu-id="5e8d0-164">權限</span><span class="sxs-lookup"><span data-stu-id="5e8d0-164">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="5e8d0-165">擁有者</span><span class="sxs-lookup"><span data-stu-id="5e8d0-165">Owner</span></span> |<span data-ttu-id="5e8d0-166">擁有者可以使用*管理存取*（例如，指派角色 tooa 使用者或群組），*檢視的所有資訊*（例如，都檢視警示） 從 hello 入口網站，和*變更設定*(例如，電子郵件通知） 在 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-166">Owners can *manage access* (for example, assign a role tooa user or group), *view all information* (for example, view alerts) from hello portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> <br><span data-ttu-id="5e8d0-167">預設會指派此角色給 Azure AD 全域管理員，而且無法變更。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-167">By default, Azure AD global administrators are assigned this role, and this cannot be changed.</span></span> |
| <span data-ttu-id="5e8d0-168">參與者</span><span class="sxs-lookup"><span data-stu-id="5e8d0-168">Contributor</span></span> |<span data-ttu-id="5e8d0-169">參與者可以*檢視的所有資訊*（例如，都檢視警示） 從 hello 入口網站，和*變更設定*（例如，電子郵件通知） 在 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-169">Contributors can *view all information* (for example, view alerts) from hello portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> |
| <span data-ttu-id="5e8d0-170">讀取者</span><span class="sxs-lookup"><span data-stu-id="5e8d0-170">Reader</span></span> |<span data-ttu-id="5e8d0-171">讀取器可以*檢視的所有資訊*（例如，都檢視警示） 從 Azure AD Connect Health 內 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-171">Readers can *view all information* (for example, view alerts) from hello portal within Azure AD Connect Health.</span></span> |

<span data-ttu-id="5e8d0-172">所有其他的角色 （例如使用者存取系統管理員或 DevTest 實驗室使用者） 有 Azure AD Connect Health，在不影響 tooaccess，即使 hello 入口網站體驗中的 hello 角色可用。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-172">All other roles (such as User Access Administrators or DevTest Labs Users) have no impact tooaccess within Azure AD Connect Health, even if hello roles are available in hello portal experience.</span></span>

### <a name="access-scope"></a><span data-ttu-id="5e8d0-173">存取範圍</span><span class="sxs-lookup"><span data-stu-id="5e8d0-173">Access scope</span></span>
<span data-ttu-id="5e8d0-174">Azure AD Connect Health 支援在兩個層級上管理存取：</span><span class="sxs-lookup"><span data-stu-id="5e8d0-174">Azure AD Connect Health supports managing access at two levels:</span></span>

* <span data-ttu-id="5e8d0-175">**所有服務執行個體**： 這是建議的路徑，在大部分情況下的 hello。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-175">**All service instances**: This is hello recommended path in most cases.</span></span> <span data-ttu-id="5e8d0-176">它可以在 Azure AD Connect Health 所監視的所有角色類型上，控制所有服務執行個體的存取 (例如 AD FS 伺服陣列)。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-176">It controls access for all service instances (for example, an AD FS farm) across all role types that are being monitored by Azure AD Connect Health.</span></span>
* <span data-ttu-id="5e8d0-177">**服務執行個體**： 在某些情況下，您可能需要根據角色型別或由服務執行個體的 toosegregate 存取。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-177">**Service instance**: In some cases, you might need toosegregate access based on role types or by a service instance.</span></span> <span data-ttu-id="5e8d0-178">在此情況下，您可以管理 hello 服務執行個體層級的存取。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-178">In this case, you can manage access at hello service instance level.</span></span>  

<span data-ttu-id="5e8d0-179">權限授與使用者是否有權存取在 hello 目錄或服務執行個體層級。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-179">Permission is granted if an end user has access either at hello directory or service instance level.</span></span>

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a><span data-ttu-id="5e8d0-180">允許使用者或群組存取 tooAzure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5e8d0-180">Allow users or groups access tooAzure AD Connect Health</span></span>
<span data-ttu-id="5e8d0-181">hello 下列步驟示範如何存取 tooallow。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-181">hello following steps show how tooallow access.</span></span>
#### <a name="step-1-select-hello-appropriate-access-scope"></a><span data-ttu-id="5e8d0-182">步驟 1： 選取 hello 適當的存取範圍</span><span class="sxs-lookup"><span data-stu-id="5e8d0-182">Step 1: Select hello appropriate access scope</span></span>
<span data-ttu-id="5e8d0-183">使用者存取在 hello tooallow*所有服務執行個體*Azure AD Connect Health，開啟 hello Azure AD Connect Health 中的 [主要] 刀鋒視窗中的層級。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-183">tooallow a user access at hello *all service instances* level within Azure AD Connect Health, open hello main blade in Azure AD Connect Health.</span></span><br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a><span data-ttu-id="5e8d0-184">步驟 2：新增使用者和群組及指派角色</span><span class="sxs-lookup"><span data-stu-id="5e8d0-184">Step 2: Add users and groups, and assign roles</span></span>
1. <span data-ttu-id="5e8d0-185">從 hello**設定**區段中，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-185">From hello **Configure** section, click **Users**.</span></span><br><span data-ttu-id="5e8d0-186">
   ![Azure AD Connect Health RBAC 主要刀鋒視窗的螢幕擷取畫面，已醒目提示 [使用者]](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span><span class="sxs-lookup"><span data-stu-id="5e8d0-186">
![Screenshot of Azure AD Connect Health RBAC main blade, with Users highlighted](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span></span>
2. <span data-ttu-id="5e8d0-187">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-187">Select **Add**.</span></span>
3. <span data-ttu-id="5e8d0-188">在 hello**選取角色** 窗格中，選取一個角色 (例如，**擁有者**)。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-188">In hello **Select a role** pane, select a role (for example, **Owner**).</span></span><br><span data-ttu-id="5e8d0-189">
   ![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面](./media/active-directory-aadconnect-health/RBAC_add.png)</span><span class="sxs-lookup"><span data-stu-id="5e8d0-189">
![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_add.png)</span></span>
4. <span data-ttu-id="5e8d0-190">輸入 hello 名稱或識別碼 hello 目標使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-190">Type hello name or identifier of hello targeted user or group.</span></span> <span data-ttu-id="5e8d0-191">您可以選取一個或多個使用者或群組在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-191">You can select one or more users or groups at hello same time.</span></span> <span data-ttu-id="5e8d0-192">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-192">Click **Select**.</span></span>
   <span data-ttu-id="5e8d0-193">![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span><span class="sxs-lookup"><span data-stu-id="5e8d0-193">![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span></span>
5. <span data-ttu-id="5e8d0-194">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-194">Select **OK**.</span></span><br>
6. <span data-ttu-id="5e8d0-195">Hello 角色指派完成後，hello 使用者和群組會出現在 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-195">After hello role assignment is complete, hello users and groups appear in hello list.</span></span><br><span data-ttu-id="5e8d0-196">
   ![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面，已醒目提示新使用者](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span><span class="sxs-lookup"><span data-stu-id="5e8d0-196">
![Screenshot of Azure AD Connect Health RBAC Users window, with new users highlighted](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span></span>

<span data-ttu-id="5e8d0-197">現在 hello 列出使用者和群組都可以存取，根據 tootheir 指派角色。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-197">Now hello listed users and groups have access, according tootheir assigned roles.</span></span>

> [!NOTE]
> * <span data-ttu-id="5e8d0-198">全域管理員一定會有完整存取 tooall hello 作業，但全域系統管理員帳戶不會出現在上述清單中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-198">Global administrators always have full access tooall hello operations, but global administrator accounts are not present in hello preceding list.</span></span>
> * <span data-ttu-id="5e8d0-199">Azure AD Connect Health 內不支援 hello 邀請使用者功能。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-199">hello Invite Users feature is not supported within Azure AD Connect Health.</span></span>
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a><span data-ttu-id="5e8d0-200">步驟 3： 共用 hello 刀鋒視窗位置與使用者或群組</span><span class="sxs-lookup"><span data-stu-id="5e8d0-200">Step 3: Share hello blade location with users or groups</span></span>
1. <span data-ttu-id="5e8d0-201">指派權限之後，使用者就可以前往[這裡](http://aka.ms/aadconnecthealth)來存取 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-201">After you assign permissions, a user can access Azure AD Connect Health by going [here](http://aka.ms/aadconnecthealth).</span></span>
2. <span data-ttu-id="5e8d0-202">Hello 刀鋒視窗，hello 使用者可以釘選 hello 刀鋒視窗中或它 toohello 儀表板的不同部分。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-202">On hello blade, hello user can pin hello blade, or different parts of it, toohello dashboard.</span></span> <span data-ttu-id="5e8d0-203">只要按一下 hello **Pin toodashboard**圖示。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-203">Simply click hello **Pin toodashboard** icon.</span></span><br><span data-ttu-id="5e8d0-204">
   ![Azure AD Connect Health RBAC 釘選刀鋒視窗的螢幕擷取畫面，已醒目提示釘選圖示](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span><span class="sxs-lookup"><span data-stu-id="5e8d0-204">
![Screenshot of Azure AD Connect Health RBAC pin blade, with pin icon highlighted](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span></span>

> [!NOTE]
> <span data-ttu-id="5e8d0-205">具有 hello 讀取者角色指派的使用者不能 tooget Azure AD Connect Health 延伸 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-205">A user with hello Reader role assigned is not able tooget Azure AD Connect Health extension from hello Azure Marketplace.</span></span> <span data-ttu-id="5e8d0-206">hello 使用者所以無法執行 hello 需要 「 建立 」 作業 toodo。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-206">hello user cannot perform hello necessary "create" operation toodo so.</span></span> <span data-ttu-id="5e8d0-207">hello 使用者仍然可以取得上述連結會 toohello toohello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-207">hello user can still get toohello blade by going toohello preceding link.</span></span> <span data-ttu-id="5e8d0-208">對於後續的使用方式，hello 使用者可以釘選 hello 刀鋒視窗 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-208">For subsequent usage, hello user can pin hello blade toohello dashboard.</span></span>
>
>

### <a name="remove-users-or-groups"></a><span data-ttu-id="5e8d0-209">移除使用者或群組</span><span class="sxs-lookup"><span data-stu-id="5e8d0-209">Remove users or groups</span></span>
<span data-ttu-id="5e8d0-210">您可以移除使用者或群組加入 tooAzure AD 連線健全狀況 RBAC。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-210">You can remove a user or a group added tooAzure AD Connect Health RBAC.</span></span> <span data-ttu-id="5e8d0-211">只要以滑鼠右鍵按一下 hello 使用者或群組，然後選取 **移除**。</span><span class="sxs-lookup"><span data-stu-id="5e8d0-211">Simply right-click hello user or group, and select **Remove**.</span></span><br><span data-ttu-id="5e8d0-212">
![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面，已醒目提示 [移除]](./media/active-directory-aadconnect-health/RBAC_remove.png)</span><span class="sxs-lookup"><span data-stu-id="5e8d0-212">
![Screenshot of Azure AD Connect Health RBAC Users window, with Remove highlighted](./media/active-directory-aadconnect-health/RBAC_remove.png)</span></span>

[//]: # (End of RBAC section)

## <a name="next-steps"></a><span data-ttu-id="5e8d0-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e8d0-213">Next steps</span></span>
* [<span data-ttu-id="5e8d0-214">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5e8d0-214">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="5e8d0-215">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="5e8d0-215">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="5e8d0-216">在 AD FS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5e8d0-216">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="5e8d0-217">使用 Azure AD Connect Health 進行同步處理</span><span class="sxs-lookup"><span data-stu-id="5e8d0-217">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="5e8d0-218">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5e8d0-218">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="5e8d0-219">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="5e8d0-219">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="5e8d0-220">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="5e8d0-220">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
