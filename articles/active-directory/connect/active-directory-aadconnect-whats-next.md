---
title: "Azure AD Connect：後續步驟及如何管理 Azure AD Connect | Microsoft Docs"
description: "了解如何針對 Azure AD Connect 擴充預設組態和作業工作。"
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
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="69c8a-103">接下來的步驟，以及如何管理 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="69c8a-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="69c8a-104">使用本文中的操作程序來自訂 Azure Active Directory (Azure AD) Connect，以符合您組織的需要和需求。</span><span class="sxs-lookup"><span data-stu-id="69c8a-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="69c8a-105">新增額外的同步處理管理員</span><span class="sxs-lookup"><span data-stu-id="69c8a-105">Add additional sync admins</span></span>
<span data-ttu-id="69c8a-106">根據預設，只有執行安裝的使用者和本機系統管理員，才能管理已安裝的同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="69c8a-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="69c8a-107">如想讓其他人存取及管理同步處理引擎，請找到本機伺服器上名為 ADSyncAdmins 的群組，將這些人加入這個群組中。</span><span class="sxs-lookup"><span data-stu-id="69c8a-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="69c8a-108">將授權指派給 Azure AD Premium 和 Enterprise Mobility Suite 使用者</span><span class="sxs-lookup"><span data-stu-id="69c8a-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="69c8a-109">既然您的使用者已同步到雲端，現在您必須為他們指派授權，他們才能開始使用雲端應用程式 (例如 Office 365)。</span><span class="sxs-lookup"><span data-stu-id="69c8a-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="69c8a-110">指派 Azure AD Premium 或 Enterprise Mobility Suite 授權</span><span class="sxs-lookup"><span data-stu-id="69c8a-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="69c8a-111">以系統管理員身分登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="69c8a-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="69c8a-112">選取左邊的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="69c8a-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="69c8a-113">在 [Active Directory] 頁面上，在有您想要設定之使用者的目錄上按兩下。</span><span class="sxs-lookup"><span data-stu-id="69c8a-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="69c8a-114">在目錄頁面頂端，選取 [授權] 。</span><span class="sxs-lookup"><span data-stu-id="69c8a-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="69c8a-115">在 [授權] 頁面上，選取 [Active Directory Premium] 或 [Enterprise Mobility Suite]，然後按一下 [指派]。</span><span class="sxs-lookup"><span data-stu-id="69c8a-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="69c8a-116">在對話方塊中，選取您要對其指派授權的使用者，然後按一下核取記號圖示，以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="69c8a-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="69c8a-117">確認已排定的同步處理工作</span><span class="sxs-lookup"><span data-stu-id="69c8a-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="69c8a-118">使用 Azure 入口網站來檢查同步處理的狀態。</span><span class="sxs-lookup"><span data-stu-id="69c8a-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="69c8a-119">確認已排程的同步處理工作</span><span class="sxs-lookup"><span data-stu-id="69c8a-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="69c8a-120">以系統管理員身分登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="69c8a-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="69c8a-121">選取左邊的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="69c8a-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="69c8a-122">在 [Active Directory] 頁面上，在有您想要設定之使用者的目錄上按兩下。</span><span class="sxs-lookup"><span data-stu-id="69c8a-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="69c8a-123">在 [目錄] 頁面的頂端，選取 [目錄整合] 。</span><span class="sxs-lookup"><span data-stu-id="69c8a-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="69c8a-124">請注意 [與本機 Active Directory 整合] 下方的上次同步處理時間。</span><span class="sxs-lookup"><span data-stu-id="69c8a-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="69c8a-125"><center>![目錄同步處理時間](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="69c8a-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="69c8a-126">啟動已排定的同步處理工作</span><span class="sxs-lookup"><span data-stu-id="69c8a-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="69c8a-127">如果您需要執行同步處理工作，只要將 Azure AD Connect 精靈整個再執行一遍即可。</span><span class="sxs-lookup"><span data-stu-id="69c8a-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="69c8a-128">您需要提供 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="69c8a-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="69c8a-129">在精靈中，選取 [自訂同步處理選項] 工作，然後按 [下一步] 來繼續完成精靈步驟。</span><span class="sxs-lookup"><span data-stu-id="69c8a-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="69c8a-130">最後，確定已選取 [初始設定一完成，即開始同步處理程序]  方塊。</span><span class="sxs-lookup"><span data-stu-id="69c8a-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="69c8a-131"><center>![開始同步處理](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="69c8a-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="69c8a-132">如需有關 Azure AD Connect 同步排程器的詳細資訊，請參閱 [Azure AD Connect 排程器](active-directory-aadconnectsync-feature-scheduler.md)。</span><span class="sxs-lookup"><span data-stu-id="69c8a-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="69c8a-133">Azure AD Connect 中可用的其他工作</span><span class="sxs-lookup"><span data-stu-id="69c8a-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="69c8a-134">在初始 Azure AD Connect 的安裝之後，您隨時可以從 Azure AD Connect 開始頁面或桌面捷徑啟動精靈。</span><span class="sxs-lookup"><span data-stu-id="69c8a-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="69c8a-135">您會發現將精靈整個再執行一遍時，會以其他工作的形式提供一些新的選項。</span><span class="sxs-lookup"><span data-stu-id="69c8a-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="69c8a-136">下表提供這些工作的摘要及個別工作的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="69c8a-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![其他工作清單](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="69c8a-138">其他工作</span><span class="sxs-lookup"><span data-stu-id="69c8a-138">Additional task</span></span> | <span data-ttu-id="69c8a-139">說明</span><span class="sxs-lookup"><span data-stu-id="69c8a-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69c8a-140">**檢視所選取的案例**</span><span class="sxs-lookup"><span data-stu-id="69c8a-140">**View the selected scenario**</span></span> |<span data-ttu-id="69c8a-141">檢視目前的 Azure AD Connect 解決方案。</span><span class="sxs-lookup"><span data-stu-id="69c8a-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="69c8a-142">這包括一般設定、同步處理的目錄，以及同步處理設定。</span><span class="sxs-lookup"><span data-stu-id="69c8a-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="69c8a-143">**自訂同步處理選項**</span><span class="sxs-lookup"><span data-stu-id="69c8a-143">**Customize synchronization options**</span></span> |<span data-ttu-id="69c8a-144">變更目前的組態，像是將其他 Active Directory 樹系新增到組態中或啟用同步處理選項 (例如使用者、群組、裝置或密碼回寫)。</span><span class="sxs-lookup"><span data-stu-id="69c8a-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="69c8a-145">**啟用預備模式**</span><span class="sxs-lookup"><span data-stu-id="69c8a-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="69c8a-146">預備不會立即同步處理及匯出到 Azure AD 或內部部署 Active Directory 的資訊。</span><span class="sxs-lookup"><span data-stu-id="69c8a-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="69c8a-147">此功能可讓您在進行同步處理之前，先進行預覽。</span><span class="sxs-lookup"><span data-stu-id="69c8a-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="69c8a-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69c8a-148">Next steps</span></span>
<span data-ttu-id="69c8a-149">深入了解[將內部部署身分識別與 Azure Active Directory 整合](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="69c8a-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
