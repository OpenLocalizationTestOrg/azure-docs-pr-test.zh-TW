---
title: "Azure AD Connect： 後續步驟及如何 toomanage Azure AD Connect |Microsoft 文件"
description: "了解如何 tooextend hello 預設設定和操作工作 Azure AD Connect。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="6ec47-103">後續步驟及如何 toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6ec47-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="6ec47-104">貴組織的需求與需求，請使用此發行項 toocustomize Azure Active Directory (Azure AD) 連線 toomeet hello 操作程序。</span><span class="sxs-lookup"><span data-stu-id="6ec47-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="6ec47-105">新增額外的同步處理管理員</span><span class="sxs-lookup"><span data-stu-id="6ec47-105">Add additional sync admins</span></span>
<span data-ttu-id="6ec47-106">根據預設，安裝和本機系統管理員未 hello 唯一 hello 使用者會無法 toomanage hello 安裝同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="6ec47-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="6ec47-107">針對其他人 toobe 無法 tooaccess 和管理 hello 同步處理引擎，找出 hello 本機伺服器上名為 ADSyncAdmins hello 群組並將它們加入 toothis 群組。</span><span class="sxs-lookup"><span data-stu-id="6ec47-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="6ec47-108">指派授權 tooAzure AD Premium 和 Enterprise Mobility Suite 的使用者</span><span class="sxs-lookup"><span data-stu-id="6ec47-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="6ec47-109">現在，您的使用者已同步處理 toohello 雲端需要 tooassign 它們以便它們可以開始使用雲端應用程式，例如 Office 365 的授權。</span><span class="sxs-lookup"><span data-stu-id="6ec47-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="6ec47-110">Azure AD Premium 或 Enterprise Mobility Suite 授權 tooassign</span><span class="sxs-lookup"><span data-stu-id="6ec47-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="6ec47-111">登入 toohello Azure 入口網站為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="6ec47-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="6ec47-112">Hello 左側選取**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="6ec47-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="6ec47-113">在 [hello **Active Directory**頁面中，按兩下要 tooset hello 使用者 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="6ec47-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="6ec47-114">在 hello 頂端 hello 目錄] 頁面上，選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="6ec47-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="6ec47-115">在 [hello**授權**頁面上，選取**Active Directory Premium**或**Enterprise Mobility Suite**，然後按一下 [**指派**。</span><span class="sxs-lookup"><span data-stu-id="6ec47-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="6ec47-116">在 hello] 對話方塊中，選取您想 tooassign 授權，然後按一下 [hello 核取記號圖示 toosave hello 變更 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="6ec47-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="6ec47-117">驗證 hello 排程的同步處理工作</span><span class="sxs-lookup"><span data-stu-id="6ec47-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="6ec47-118">使用同步處理的 hello Azure 入口網站 toocheck hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="6ec47-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="6ec47-119">tooverify hello 排程的同步處理工作</span><span class="sxs-lookup"><span data-stu-id="6ec47-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="6ec47-120">登入 toohello Azure 入口網站為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="6ec47-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="6ec47-121">Hello 左側選取**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="6ec47-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="6ec47-122">在 [hello **Active Directory**頁面中，按兩下要 tooset hello 使用者 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="6ec47-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="6ec47-123">在 hello 頂端 hello 目錄] 頁面上，選取**目錄整合**。</span><span class="sxs-lookup"><span data-stu-id="6ec47-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="6ec47-124">在下**與本機 active directory 整合**，注意 hello 上次同步處理時間。</span><span class="sxs-lookup"><span data-stu-id="6ec47-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="6ec47-125"><center>![目錄同步處理時間](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="6ec47-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="6ec47-126">啟動已排定的同步處理工作</span><span class="sxs-lookup"><span data-stu-id="6ec47-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="6ec47-127">如果您需要 toorun 同步處理工作，您可以透過 hello Azure AD Connect 精靈重新執行。</span><span class="sxs-lookup"><span data-stu-id="6ec47-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="6ec47-128">您需要 tooprovide Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="6ec47-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="6ec47-129">在 hello 精靈中，選取 [hello**自訂同步處理選項**工作，並按一下**下一步**toomove 透過 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="6ec47-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="6ec47-130">在 hello 結束時，請確定該 hello **hello 初始設定完成之後儘速開始 hello 同步處理程序**方塊為已選取。</span><span class="sxs-lookup"><span data-stu-id="6ec47-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="6ec47-131"><center>![開始同步處理](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="6ec47-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="6ec47-132">如需有關 hello Azure AD Connect 同步處理排程器的詳細資訊，請參閱[Azure AD 連接排程器](active-directory-aadconnectsync-feature-scheduler.md)。</span><span class="sxs-lookup"><span data-stu-id="6ec47-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="6ec47-133">Azure AD Connect 中可用的其他工作</span><span class="sxs-lookup"><span data-stu-id="6ec47-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="6ec47-134">之後您的 Azure AD Connect 的初始安裝，您可以一律 hello 重新啟動精靈從 hello Azure AD Connect 開始頁面或桌面捷徑。</span><span class="sxs-lookup"><span data-stu-id="6ec47-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="6ec47-135">您會發現，再次進行 hello 精靈提供的其他工作的 hello 表單中的部分新選項。</span><span class="sxs-lookup"><span data-stu-id="6ec47-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="6ec47-136">hello 下表提供這些工作的摘要和每項工作的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="6ec47-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![其他工作清單](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="6ec47-138">其他工作</span><span class="sxs-lookup"><span data-stu-id="6ec47-138">Additional task</span></span> | <span data-ttu-id="6ec47-139">說明</span><span class="sxs-lookup"><span data-stu-id="6ec47-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ec47-140">**檢視 hello 選取的案例**</span><span class="sxs-lookup"><span data-stu-id="6ec47-140">**View hello selected scenario**</span></span> |<span data-ttu-id="6ec47-141">檢視目前的 Azure AD Connect 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6ec47-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="6ec47-142">這包括一般設定、同步處理的目錄，以及同步處理設定。</span><span class="sxs-lookup"><span data-stu-id="6ec47-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="6ec47-143">**自訂同步處理選項**</span><span class="sxs-lookup"><span data-stu-id="6ec47-143">**Customize synchronization options**</span></span> |<span data-ttu-id="6ec47-144">變更 hello 如加入額外的 Active Directory 樹系 toohello 設定，或啟用同步處理選項，例如使用者、 群組、 裝置或密碼回寫目前的設定。</span><span class="sxs-lookup"><span data-stu-id="6ec47-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="6ec47-145">**啟用預備模式**</span><span class="sxs-lookup"><span data-stu-id="6ec47-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="6ec47-146">階段資訊不會立即同步處理，也不會匯出 tooAzure AD 或內部部署 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="6ec47-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="6ec47-147">利用此功能，您可以在發生前加以預覽 hello 同步處理。</span><span class="sxs-lookup"><span data-stu-id="6ec47-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ec47-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ec47-148">Next steps</span></span>
<span data-ttu-id="6ec47-149">深入了解[將內部部署身分識別與 Azure Active Directory 整合](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="6ec47-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
