---
title: "一組錯誤的使用者佈建至 Azure AD 資源庫應用程式 | Microsoft Docs"
description: "了解如何查明為什麼一組不同於您所預期的使用者佈建至應用程式"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="1d821-103">一組錯誤的使用者佈建至 Azure AD 資源庫應用程式</span><span class="sxs-lookup"><span data-stu-id="1d821-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="1d821-104">哪些使用者會佈建至應用程式，主要取決於哪些使用者和群組已**指派**至應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d821-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="1d821-105">請利用下列資源，了解如何檢查 Azure Active Directory 內有哪些使用者和群組已指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d821-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="1d821-106">以系統管理員身分直接指派使用者</span><span class="sxs-lookup"><span data-stu-id="1d821-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="1d821-107">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="1d821-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1d821-108">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="1d821-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d821-109">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="1d821-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d821-110">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="1d821-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d821-111">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d821-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1d821-112">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1d821-113">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d821-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1d821-114">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d821-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1d821-115">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1d821-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1d821-116">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1d821-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1d821-117">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="1d821-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1d821-118">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="1d821-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1d821-119">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="1d821-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1d821-120">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1d821-121">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="1d821-122">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1d821-123">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="1d821-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="1d821-124">按一下 [指派] 按鈕，將應用程式指派至選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="1d821-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="1d821-125">如果已經為應用程式設定並執行佈建，新的使用者應該大約 10 分鐘就會佈建至應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d821-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="1d821-126">如需詳細資訊，請檢查**稽核記錄**。</span><span class="sxs-lookup"><span data-stu-id="1d821-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="1d821-127">以系統管理員身分將群組直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="1d821-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="1d821-128">若要直接將一或多個群組指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="1d821-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1d821-129">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="1d821-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d821-130">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="1d821-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d821-131">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="1d821-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d821-132">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d821-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1d821-133">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1d821-134">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d821-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1d821-135">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d821-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1d821-136">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1d821-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1d821-137">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1d821-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1d821-138">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="1d821-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1d821-139">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之群組的**完整群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="1d821-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1d821-140">將滑鼠停留在清單中的**群組**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="1d821-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1d821-141">按一下群組設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1d821-142">**選擇性︰**如果您想要**新增多個群組**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**完整群組名稱**，然後按一下核取方塊，將此群組新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="1d821-143">當您完成選取群組時，按一下 [選取] 按鈕，將它們新增到要指派給應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="1d821-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1d821-144">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取群組的角色。</span><span class="sxs-lookup"><span data-stu-id="1d821-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="1d821-145">按一下 [指派] 按鈕，將應用程式指派至選取的群組。</span><span class="sxs-lookup"><span data-stu-id="1d821-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="1d821-146">如果已經為應用程式設定並執行佈建，群組內包含的新使用者應該大約 10 分鐘就會佈建至應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d821-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="1d821-147">如需詳細資訊，請檢查**稽核記錄**。</span><span class="sxs-lookup"><span data-stu-id="1d821-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1d821-148">除了成員，還有群組名稱和群組詳細資訊的佈建 (如果某些應用程式有支援)。</span><span class="sxs-lookup"><span data-stu-id="1d821-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="1d821-149">您可以對 [佈建] 索引標籤中顯示的群組物件啟用或停用 [對應]，以啟用或停用此功能。</span><span class="sxs-lookup"><span data-stu-id="1d821-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="1d821-150">如果已啟用佈建群組，請務必檢閱屬性對應，以確保「比對識別碼」使用適當的欄位。</span><span class="sxs-lookup"><span data-stu-id="1d821-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="1d821-151">這可以是顯示名稱或電子郵件別名，因為如果 Azure AD 中某個群組的相符屬性空白或未填入，則不會佈建群組和其成員。</span><span class="sxs-lookup"><span data-stu-id="1d821-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d821-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d821-152">Next steps</span></span>
[<span data-ttu-id="1d821-153">自動化使用 Azure Active Directory 對於 SaaS 應用程式的使用者佈建和解除佈建</span><span class="sxs-lookup"><span data-stu-id="1d821-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
