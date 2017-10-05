---
title: "Azure Active Directory Connect Health 作業"
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
ms.openlocfilehash: 06afc6b4149ea1590a2994d1638d6979a89035e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-connect-health-operations"></a><span data-ttu-id="ade62-103">Azure Active Directory Connect Health 作業</span><span class="sxs-lookup"><span data-stu-id="ade62-103">Azure Active Directory Connect Health operations</span></span>
<span data-ttu-id="ade62-104">本主題說明您可以使用 Azure Active Directory (Azure AD) Connect Health 來執行的各種作業。</span><span class="sxs-lookup"><span data-stu-id="ade62-104">This topic describes the various operations you can perform by using Azure Active Directory (Azure AD) Connect Health.</span></span>

## <a name="enable-email-notifications"></a><span data-ttu-id="ade62-105">啟用電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="ade62-105">Enable email notifications</span></span>
<span data-ttu-id="ade62-106">您可以將 Azure AD Connect Health 服務設定為當警示表示您的身分識別基礎結構狀況不良時，傳送電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ade62-106">You can configure the Azure AD Connect Health service to send email notifications when alerts indicate that your identity infrastructure is not healthy.</span></span> <span data-ttu-id="ade62-107">產生警示和解決警示時會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="ade62-107">This occurs when an alert is generated, and when it is resolved.</span></span>

![Azure AD Connect Health 電子郵件通知設定的螢幕擷取畫面](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> <span data-ttu-id="ade62-109">依預設會啟用電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ade62-109">Email notifications are enabled by default.</span></span>
>
>

### <a name="to-enable-azure-ad-connect-health-email-notifications"></a><span data-ttu-id="ade62-110">啟用 Azure AD Connect Health 電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="ade62-110">To enable Azure AD Connect Health email notifications</span></span>
1. <span data-ttu-id="ade62-111">針對您想要接收電子郵件通知的服務，開啟 [警示] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ade62-111">Open the **Alerts** blade for the service for which you want to receive email notification.</span></span>
2. <span data-ttu-id="ade62-112">從動作列中，按一下 [通知設定]。</span><span class="sxs-lookup"><span data-stu-id="ade62-112">From the action bar, click **Notification Settings**.</span></span>
3. <span data-ttu-id="ade62-113">在電子郵件通知開關上，選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="ade62-113">At the email notification switch, select **ON**.</span></span>
4. <span data-ttu-id="ade62-114">如果要讓所有全域管理員都接收電子郵件通知，請選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ade62-114">Select the check box if you want all global administrators to receive email notifications.</span></span>
5. <span data-ttu-id="ade62-115">如果想要用其他任何電子郵件地址來接收電子郵件通知，請在 [其他電子郵件收件者] 方塊中指定。</span><span class="sxs-lookup"><span data-stu-id="ade62-115">If you want to receive email notifications at any other email addresses, specify them in the **Additional Email Recipients** box.</span></span> <span data-ttu-id="ade62-116">若要從這份清單中移除電子郵件地址，請以滑鼠右鍵按一下該項目，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ade62-116">To remove an email address from this list, right-click the entry and select **Delete**.</span></span>
6. <span data-ttu-id="ade62-117">若要完成變更，請按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ade62-117">To finalize the changes, click **Save**.</span></span> <span data-ttu-id="ade62-118">只有在您儲存之後，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="ade62-118">Changes take effect only after you save.</span></span>

## <a name="delete-a-server-or-service-instance"></a><span data-ttu-id="ade62-119">刪除伺服器或服務執行個體</span><span class="sxs-lookup"><span data-stu-id="ade62-119">Delete a server or service instance</span></span>

<span data-ttu-id="ade62-120">在某些情況下，您可能需要移除不要監視的伺服器。</span><span class="sxs-lookup"><span data-stu-id="ade62-120">In some instances, you might want to remove a server from being monitored.</span></span> <span data-ttu-id="ade62-121">以下是從 Azure AD Connect Health 服務移除伺服器時所需要知道的事項。</span><span class="sxs-lookup"><span data-stu-id="ade62-121">Here's what you need to know to remove a server from the Azure AD Connect Health service.</span></span>

<span data-ttu-id="ade62-122">刪除伺服器時，請注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="ade62-122">When you're deleting a server, be aware of the following:</span></span>

* <span data-ttu-id="ade62-123">這個動作會停止從該伺服器收集任何進一步的資料。</span><span class="sxs-lookup"><span data-stu-id="ade62-123">This action stops collecting any further data from that server.</span></span> <span data-ttu-id="ade62-124">此伺服器會從監視服務中移除。</span><span class="sxs-lookup"><span data-stu-id="ade62-124">This server is removed from the monitoring service.</span></span> <span data-ttu-id="ade62-125">執行此動作之後，您就無法檢視此伺服器的新警示、監視或使用情況分析資料。</span><span class="sxs-lookup"><span data-stu-id="ade62-125">After this action, you are not able to view new alerts, monitoring, or usage analytics data for this server.</span></span>
* <span data-ttu-id="ade62-126">這個動作不會從伺服器解除安裝健康情況代理程式。</span><span class="sxs-lookup"><span data-stu-id="ade62-126">This action does not uninstall the Health Agent from your server.</span></span> <span data-ttu-id="ade62-127">如果您在執行此步驟之前未解除安裝健康情況代理程式，您可能會在伺服器上看到與健康情況代理程式相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="ade62-127">If you have not uninstalled the Health Agent before performing this step, you might see errors related to the Health Agent on the server.</span></span>
* <span data-ttu-id="ade62-128">這個動作不會刪除已從這部伺服器收集的資料。</span><span class="sxs-lookup"><span data-stu-id="ade62-128">This action does not delete the data already collected from this server.</span></span> <span data-ttu-id="ade62-129">將會依照 Azure 資料保留原則來刪除該資料。</span><span class="sxs-lookup"><span data-stu-id="ade62-129">That data is deleted in accordance with the Azure data retention policy.</span></span>
* <span data-ttu-id="ade62-130">執行此動作之後，如果想要重新開始監視相同的伺服器，您必須在這部伺服器上解除安裝健康情況代理程式，再重新安裝。</span><span class="sxs-lookup"><span data-stu-id="ade62-130">After performing this action, if you want to start monitoring the same server again, you must uninstall and reinstall the Health Agent on this server.</span></span>

### <a name="to-delete-a-server-from-the-azure-ad-connect-health-service"></a><span data-ttu-id="ade62-131">從 Azure AD Connect Health 服務刪除伺服器</span><span class="sxs-lookup"><span data-stu-id="ade62-131">To delete a server from the Azure AD Connect Health service</span></span>
<span data-ttu-id="ade62-132">適用於 Active Directory 同盟服務 (AD FS) 和 Azure AD Connect (Sync) 的 Azure AD Connect Health：</span><span class="sxs-lookup"><span data-stu-id="ade62-132">Azure AD Connect Health for Active Directory Federation Services (AD FS) and Azure AD Connect (Sync):</span></span>

1. <span data-ttu-id="ade62-133">從 [伺服器清單] 刀鋒視窗中選取要移除的伺服器名稱，以開啟 [伺服器] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ade62-133">Open the **Server** blade from the **Server List** blade by selecting the server name to be removed.</span></span>
2. <span data-ttu-id="ade62-134">在 [伺服器] 刀鋒視窗中，從動作列中按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ade62-134">On the **Server** blade, from the action bar, click **Delete**.</span></span>
3. <span data-ttu-id="ade62-135">在確認方塊中輸入伺服器名稱以確認。</span><span class="sxs-lookup"><span data-stu-id="ade62-135">Confirm by typing the server name in the confirmation box.</span></span>
4. <span data-ttu-id="ade62-136">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="ade62-136">Click **Delete**.</span></span>

<span data-ttu-id="ade62-137">Azure AD Connect Health for Azure Active Directory Domain Services：</span><span class="sxs-lookup"><span data-stu-id="ade62-137">Azure AD Connect Health for Azure Active Directory Domain Services:</span></span>

1. <span data-ttu-id="ade62-138">開啟 [網域控制站] 儀表板。</span><span class="sxs-lookup"><span data-stu-id="ade62-138">Open the **Domain Controllers** dashboard.</span></span>
2. <span data-ttu-id="ade62-139">選取要移除的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="ade62-139">Select the domain controller to be removed.</span></span>
3. <span data-ttu-id="ade62-140">從動作列中，按一下 [刪除已選取項目]。</span><span class="sxs-lookup"><span data-stu-id="ade62-140">From the action bar, click **Delete Selected**.</span></span>
4. <span data-ttu-id="ade62-141">確認刪除伺服器的動作。</span><span class="sxs-lookup"><span data-stu-id="ade62-141">Confirm the action to delete the server.</span></span>
5. <span data-ttu-id="ade62-142">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="ade62-142">Click **Delete**.</span></span>

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a><span data-ttu-id="ade62-143">從 Azure AD Connect Health 服務刪除服務執行個體</span><span class="sxs-lookup"><span data-stu-id="ade62-143">Delete a service instance from Azure AD Connect Health service</span></span>
<span data-ttu-id="ade62-144">在某些情況下，您可能需要移除服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="ade62-144">In some instances, you might want to remove a service instance.</span></span> <span data-ttu-id="ade62-145">以下是從 Azure AD Connect Health 服務移除服務執行個體時所需要知道的事項。</span><span class="sxs-lookup"><span data-stu-id="ade62-145">Here's what you need to know to remove a service instance from the Azure AD Connect Health service.</span></span>

<span data-ttu-id="ade62-146">刪除服務執行個體時，請注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="ade62-146">When you're deleting a service instance, be aware of the following:</span></span>

* <span data-ttu-id="ade62-147">這個動作會從監視服務移除目前的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="ade62-147">This action removes the current service instance from the monitoring service.</span></span>
* <span data-ttu-id="ade62-148">這個動作不會從已在此服務執行個體中監視的任何伺服器解除安裝或移除健康情況代理程式。</span><span class="sxs-lookup"><span data-stu-id="ade62-148">This action does not uninstall or remove the Health Agent from any of the servers that were monitored as part of this service instance.</span></span> <span data-ttu-id="ade62-149">如果您在執行此步驟之前未解除安裝健康情況代理程式，您可能會在伺服器上看到與健康情況代理程式相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="ade62-149">If you have not uninstalled the Health Agent before performing this step, you might see errors related to the Health Agent on the servers.</span></span>
* <span data-ttu-id="ade62-150">將會根據 Azure 資料保留原則來刪除此伺服器執行個體中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="ade62-150">All data from this service instance is deleted in accordance with the Azure data retention policy.</span></span>
* <span data-ttu-id="ade62-151">執行此動作之後，如果想要開始監視該服務，請在所有伺服器上解除安裝健康情況代理程式，再重新安裝。</span><span class="sxs-lookup"><span data-stu-id="ade62-151">After performing this action, if you want to start monitoring the service, uninstall and reinstall the Health Agent on all the servers.</span></span> <span data-ttu-id="ade62-152">執行此動作之後，如果想要重新開始監視相同的伺服器，請在該伺服器上解除安裝、重新安裝及註冊健康情況代理程式。</span><span class="sxs-lookup"><span data-stu-id="ade62-152">After performing this action, if you want to start monitoring the same server again, uninstall, reinstall, and register the Health Agent on that server.</span></span>

#### <a name="to-delete-a-service-instance-from-the-azure-ad-connect-health-service"></a><span data-ttu-id="ade62-153">從 Azure AD Connect Health 服務刪除服務執行個體</span><span class="sxs-lookup"><span data-stu-id="ade62-153">To delete a service instance from the Azure AD Connect Health service</span></span>
1. <span data-ttu-id="ade62-154">從 [服務清單] 刀鋒視窗中選取您想要移除的服務識別碼 (伺服陣列名稱)，以開啟 [服務] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ade62-154">Open the **Service** blade from the **Service List** blade by selecting the service identifier (farm name) that you want to remove.</span></span>
2. <span data-ttu-id="ade62-155">在 [伺服器] 刀鋒視窗中，從動作列中按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ade62-155">On the **Server** blade, from the action bar, click **Delete**.</span></span>
3. <span data-ttu-id="ade62-156">在確認方塊中輸入服務名稱以確認 (例如：sts.contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="ade62-156">Confirm by typing the service name in the confirmation box (for example: sts.contoso.com).</span></span>
4. <span data-ttu-id="ade62-157">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="ade62-157">Click **Delete**.</span></span>
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a><span data-ttu-id="ade62-158">使用角色型存取控制來管理存取</span><span class="sxs-lookup"><span data-stu-id="ade62-158">Manage access with Role-Based Access Control</span></span>
<span data-ttu-id="ade62-159">Azure AD Connect Health 的[角色型存取控制 (RBAC)](../role-based-access-control-configure.md) 提供存取權給全域管理員以外的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="ade62-159">[Role-Based Access Control (RBAC)](../role-based-access-control-configure.md) for Azure AD Connect Health provides access to users and groups other than global administrators.</span></span> <span data-ttu-id="ade62-160">RBAC 會指派角色給目標使用者和群組，並提供機制來限制您目錄內的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="ade62-160">RBAC assigns roles to the intended users and groups, and provides a mechanism to limit the global administrators within your directory.</span></span>

### <a name="roles"></a><span data-ttu-id="ade62-161">角色</span><span class="sxs-lookup"><span data-stu-id="ade62-161">Roles</span></span>
<span data-ttu-id="ade62-162">Azure AD Connect Health 支援下列內建角色：</span><span class="sxs-lookup"><span data-stu-id="ade62-162">Azure AD Connect Health supports the following built-in roles:</span></span>

| <span data-ttu-id="ade62-163">角色</span><span class="sxs-lookup"><span data-stu-id="ade62-163">Role</span></span> | <span data-ttu-id="ade62-164">權限</span><span class="sxs-lookup"><span data-stu-id="ade62-164">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="ade62-165">擁有者</span><span class="sxs-lookup"><span data-stu-id="ade62-165">Owner</span></span> |<span data-ttu-id="ade62-166">擁有者可以在 Azure AD Connect Health 內「管理存取」(例如將角色指派給使用者或群組)、「檢視入口網站中的所有資訊」(例如檢視警示)，以及「變更設定」(例如電子郵件通知)。</span><span class="sxs-lookup"><span data-stu-id="ade62-166">Owners can *manage access* (for example, assign a role to a user or group), *view all information* (for example, view alerts) from the portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> <br><span data-ttu-id="ade62-167">預設會指派此角色給 Azure AD 全域管理員，而且無法變更。</span><span class="sxs-lookup"><span data-stu-id="ade62-167">By default, Azure AD global administrators are assigned this role, and this cannot be changed.</span></span> |
| <span data-ttu-id="ade62-168">參與者</span><span class="sxs-lookup"><span data-stu-id="ade62-168">Contributor</span></span> |<span data-ttu-id="ade62-169">參與者可以在 Azure AD Connect Health 內「檢視入口網站中的所有資訊」(例如檢視警示)，以及「變更設定」(例如電子郵件通知)。</span><span class="sxs-lookup"><span data-stu-id="ade62-169">Contributors can *view all information* (for example, view alerts) from the portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> |
| <span data-ttu-id="ade62-170">讀取器</span><span class="sxs-lookup"><span data-stu-id="ade62-170">Reader</span></span> |<span data-ttu-id="ade62-171">讀者可以在 Azure AD Connect Health 內「檢視入口網站中的所有資訊」(例如檢視警示)。</span><span class="sxs-lookup"><span data-stu-id="ade62-171">Readers can *view all information* (for example, view alerts) from the portal within Azure AD Connect Health.</span></span> |

<span data-ttu-id="ade62-172">其他所有角色 (例如「使用者存取系統管理員」或「DevTest Labs 使用者」) 即使出現在入口網站體驗中，也不影響 Azure AD Connect Health 內的存取。</span><span class="sxs-lookup"><span data-stu-id="ade62-172">All other roles (such as User Access Administrators or DevTest Labs Users) have no impact to access within Azure AD Connect Health, even if the roles are available in the portal experience.</span></span>

### <a name="access-scope"></a><span data-ttu-id="ade62-173">存取範圍</span><span class="sxs-lookup"><span data-stu-id="ade62-173">Access scope</span></span>
<span data-ttu-id="ade62-174">Azure AD Connect Health 支援在兩個層級上管理存取：</span><span class="sxs-lookup"><span data-stu-id="ade62-174">Azure AD Connect Health supports managing access at two levels:</span></span>

* <span data-ttu-id="ade62-175">**所有服務執行個體**：在大部分情況下，這是建議的途徑。</span><span class="sxs-lookup"><span data-stu-id="ade62-175">**All service instances**: This is the recommended path in most cases.</span></span> <span data-ttu-id="ade62-176">它可以在 Azure AD Connect Health 所監視的所有角色類型上，控制所有服務執行個體的存取 (例如 AD FS 伺服陣列)。</span><span class="sxs-lookup"><span data-stu-id="ade62-176">It controls access for all service instances (for example, an AD FS farm) across all role types that are being monitored by Azure AD Connect Health.</span></span>
* <span data-ttu-id="ade62-177">**服務執行個體**：在某些情況下，您可能需要根據角色類型或服務執行個體來隔離存取。</span><span class="sxs-lookup"><span data-stu-id="ade62-177">**Service instance**: In some cases, you might need to segregate access based on role types or by a service instance.</span></span> <span data-ttu-id="ade62-178">在此情況下，您可以管理服務執行個體層級的存取。</span><span class="sxs-lookup"><span data-stu-id="ade62-178">In this case, you can manage access at the service instance level.</span></span>  

<span data-ttu-id="ade62-179">如果使用者具有目錄或服務執行個體層級的存取，則會授與權限。</span><span class="sxs-lookup"><span data-stu-id="ade62-179">Permission is granted if an end user has access either at the directory or service instance level.</span></span>

### <a name="allow-users-or-groups-access-to-azure-ad-connect-health"></a><span data-ttu-id="ade62-180">允許使用者或群組存取 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="ade62-180">Allow users or groups access to Azure AD Connect Health</span></span>
<span data-ttu-id="ade62-181">下列步驟示範如何允許存取。</span><span class="sxs-lookup"><span data-stu-id="ade62-181">The following steps show how to allow access.</span></span>
#### <a name="step-1-select-the-appropriate-access-scope"></a><span data-ttu-id="ade62-182">步驟 1：選取適當的存取範圍</span><span class="sxs-lookup"><span data-stu-id="ade62-182">Step 1: Select the appropriate access scope</span></span>
<span data-ttu-id="ade62-183">若要允許 Azure AD Connect Health 內的*所有服務執行個體*層級使用者存取，請開啟 Azure AD Connect Health 中的主要刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ade62-183">To allow a user access at the *all service instances* level within Azure AD Connect Health, open the main blade in Azure AD Connect Health.</span></span><br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a><span data-ttu-id="ade62-184">步驟 2：新增使用者和群組及指派角色</span><span class="sxs-lookup"><span data-stu-id="ade62-184">Step 2: Add users and groups, and assign roles</span></span>
1. <span data-ttu-id="ade62-185">從 [設定] 區段中，按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="ade62-185">From the **Configure** section, click **Users**.</span></span><br><span data-ttu-id="ade62-186">
   ![Azure AD Connect Health RBAC 主要刀鋒視窗的螢幕擷取畫面，已醒目提示 [使用者]](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span><span class="sxs-lookup"><span data-stu-id="ade62-186">
![Screenshot of Azure AD Connect Health RBAC main blade, with Users highlighted](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span></span>
2. <span data-ttu-id="ade62-187">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ade62-187">Select **Add**.</span></span>
3. <span data-ttu-id="ade62-188">在 [選取角色] 窗格中，選取角色 (例如，**擁有者**)。</span><span class="sxs-lookup"><span data-stu-id="ade62-188">In the **Select a role** pane, select a role (for example, **Owner**).</span></span><br><span data-ttu-id="ade62-189">
   ![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面](./media/active-directory-aadconnect-health/RBAC_add.png)</span><span class="sxs-lookup"><span data-stu-id="ade62-189">
![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_add.png)</span></span>
4. <span data-ttu-id="ade62-190">輸入目標使用者或群組的名稱或識別碼。</span><span class="sxs-lookup"><span data-stu-id="ade62-190">Type the name or identifier of the targeted user or group.</span></span> <span data-ttu-id="ade62-191">您可以同時選取一或多個使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="ade62-191">You can select one or more users or groups at the same time.</span></span> <span data-ttu-id="ade62-192">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="ade62-192">Click **Select**.</span></span>
   <span data-ttu-id="ade62-193">![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span><span class="sxs-lookup"><span data-stu-id="ade62-193">![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span></span>
5. <span data-ttu-id="ade62-194">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ade62-194">Select **OK**.</span></span><br>
6. <span data-ttu-id="ade62-195">完成角色指派之後，使用者和群組就會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="ade62-195">After the role assignment is complete, the users and groups appear in the list.</span></span><br><span data-ttu-id="ade62-196">
   ![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面，已醒目提示新使用者](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span><span class="sxs-lookup"><span data-stu-id="ade62-196">
![Screenshot of Azure AD Connect Health RBAC Users window, with new users highlighted](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span></span>

<span data-ttu-id="ade62-197">現在，列出的使用者和群組根據其獲指派的角色，已具有存取權。</span><span class="sxs-lookup"><span data-stu-id="ade62-197">Now the listed users and groups have access, according to their assigned roles.</span></span>

> [!NOTE]
> * <span data-ttu-id="ade62-198">全域管理員一律具有所有作業的完整存取，但全域管理員帳戶不會出現在上述清單中。</span><span class="sxs-lookup"><span data-stu-id="ade62-198">Global administrators always have full access to all the operations, but global administrator accounts are not present in the preceding list.</span></span>
> * <span data-ttu-id="ade62-199">Azure AD Connect Health 內不支援「邀請使用者」功能。</span><span class="sxs-lookup"><span data-stu-id="ade62-199">The Invite Users feature is not supported within Azure AD Connect Health.</span></span>
>
>

#### <a name="step-3-share-the-blade-location-with-users-or-groups"></a><span data-ttu-id="ade62-200">步驟 3：與使用者或群組共用刀鋒視窗位置</span><span class="sxs-lookup"><span data-stu-id="ade62-200">Step 3: Share the blade location with users or groups</span></span>
1. <span data-ttu-id="ade62-201">指派權限之後，使用者就可以前往[這裡](http://aka.ms/aadconnecthealth)來存取 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="ade62-201">After you assign permissions, a user can access Azure AD Connect Health by going [here](http://aka.ms/aadconnecthealth).</span></span>
2. <span data-ttu-id="ade62-202">在刀鋒視窗上，使用者可以將刀鋒視窗或其他組件釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="ade62-202">On the blade, the user can pin the blade, or different parts of it, to the dashboard.</span></span> <span data-ttu-id="ade62-203">只要按一下 [釘選到儀表板] 圖示即可。</span><span class="sxs-lookup"><span data-stu-id="ade62-203">Simply click the **Pin to dashboard** icon.</span></span><br><span data-ttu-id="ade62-204">
   ![Azure AD Connect Health RBAC 釘選刀鋒視窗的螢幕擷取畫面，已醒目提示釘選圖示](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span><span class="sxs-lookup"><span data-stu-id="ade62-204">
![Screenshot of Azure AD Connect Health RBAC pin blade, with pin icon highlighted](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span></span>

> [!NOTE]
> <span data-ttu-id="ade62-205">被指派「讀者」角色的使用者無法從 Azure Marketplace 取得 Azure AD Connect Health 擴充。</span><span class="sxs-lookup"><span data-stu-id="ade62-205">A user with the Reader role assigned is not able to get Azure AD Connect Health extension from the Azure Marketplace.</span></span> <span data-ttu-id="ade62-206">此使用者無法執行必要的「建立」作業來這麼做。</span><span class="sxs-lookup"><span data-stu-id="ade62-206">The user cannot perform the necessary "create" operation to do so.</span></span> <span data-ttu-id="ade62-207">此使用者仍可前往上述連結以存取刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ade62-207">The user can still get to the blade by going to the preceding link.</span></span> <span data-ttu-id="ade62-208">為方便之後使用，使用者可以將刀鋒視窗釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="ade62-208">For subsequent usage, the user can pin the blade to the dashboard.</span></span>
>
>

### <a name="remove-users-or-groups"></a><span data-ttu-id="ade62-209">移除使用者或群組</span><span class="sxs-lookup"><span data-stu-id="ade62-209">Remove users or groups</span></span>
<span data-ttu-id="ade62-210">您可以移除已新增至 Azure AD Connect Health RBAC 的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="ade62-210">You can remove a user or a group added to Azure AD Connect Health RBAC.</span></span> <span data-ttu-id="ade62-211">只要以滑鼠右鍵按一下使用者或群組，然後選取 [移除] 即可。</span><span class="sxs-lookup"><span data-stu-id="ade62-211">Simply right-click the user or group, and select **Remove**.</span></span><br><span data-ttu-id="ade62-212">
![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面，已醒目提示 [移除]](./media/active-directory-aadconnect-health/RBAC_remove.png)</span><span class="sxs-lookup"><span data-stu-id="ade62-212">
![Screenshot of Azure AD Connect Health RBAC Users window, with Remove highlighted](./media/active-directory-aadconnect-health/RBAC_remove.png)</span></span>

[//]: # (End of RBAC section)

## <a name="next-steps"></a><span data-ttu-id="ade62-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ade62-213">Next steps</span></span>
* [<span data-ttu-id="ade62-214">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="ade62-214">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="ade62-215">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="ade62-215">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="ade62-216">在 AD FS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="ade62-216">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="ade62-217">使用 Azure AD Connect Health 進行同步處理</span><span class="sxs-lookup"><span data-stu-id="ade62-217">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="ade62-218">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="ade62-218">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="ade62-219">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="ade62-219">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="ade62-220">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="ade62-220">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
