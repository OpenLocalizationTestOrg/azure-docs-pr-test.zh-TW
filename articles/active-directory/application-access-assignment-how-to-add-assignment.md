---
title: "如何將使用者和群組指派至應用程式 | Microsoft Docs"
description: "將使用者指派至應用程式以授與存取權"
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="43c08-103">如何將使用者和群組指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="43c08-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="43c08-104">您必須先**將使用者指派至應用程式**以授與存取權，使用者才能對特定應用程式執行以下任何動作︰</span><span class="sxs-lookup"><span data-stu-id="43c08-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="43c08-105">**直接瀏覽至應用程式的 URL** 以存取應用程式 (也稱為 SP 初始化登入)。</span><span class="sxs-lookup"><span data-stu-id="43c08-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="43c08-106">使用應用程式 [屬性] 頁面上的 [使用者存取 URL] 以存取應用程式 (也稱為 IDP 初始化登入)。</span><span class="sxs-lookup"><span data-stu-id="43c08-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="43c08-107">看到應用程式出現在其[應用程式存取面板](https://myapps.microsoft.com/)或行動應用程式上。</span><span class="sxs-lookup"><span data-stu-id="43c08-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="43c08-108">看到應用程式出現在其 [Office 365 應用程式啟動程式](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a)上。</span><span class="sxs-lookup"><span data-stu-id="43c08-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="43c08-109">使用 Azure Active Directory 指派應用程式的方法</span><span class="sxs-lookup"><span data-stu-id="43c08-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="43c08-110">使用 Azure Active Directory 指派應用程式有 3 種方法：</span><span class="sxs-lookup"><span data-stu-id="43c08-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="43c08-111">以系統管理員身分將使用者直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="43c08-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="43c08-112">以系統管理員身分將群組直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="43c08-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="43c08-113">啟用自助應用程式存取以允許使用者尋找自己的應用程式</span><span class="sxs-lookup"><span data-stu-id="43c08-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="43c08-114">以系統管理員身分直接指派使用者</span><span class="sxs-lookup"><span data-stu-id="43c08-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="43c08-115">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="43c08-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="43c08-116">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="43c08-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="43c08-117">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="43c08-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43c08-118">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="43c08-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43c08-119">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="43c08-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43c08-120">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="43c08-121">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="43c08-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="43c08-122">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c08-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="43c08-123">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="43c08-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43c08-124">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="43c08-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="43c08-125">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="43c08-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="43c08-126">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="43c08-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="43c08-127">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="43c08-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="43c08-128">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="43c08-129">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="43c08-130">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="43c08-131">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="43c08-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="43c08-132">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="43c08-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="43c08-133">稍待片刻，您已選取的使用者就能夠使用解決方案描述一節所述的方法，啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c08-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="43c08-134">以系統管理員身分將群組直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="43c08-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="43c08-135">若要直接將一或多個群組指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="43c08-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="43c08-136">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="43c08-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="43c08-137">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="43c08-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43c08-138">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="43c08-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43c08-139">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="43c08-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43c08-140">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="43c08-141">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="43c08-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="43c08-142">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c08-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="43c08-143">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="43c08-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43c08-144">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="43c08-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="43c08-145">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="43c08-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="43c08-146">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之群組的**完整群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="43c08-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="43c08-147">將滑鼠停留在清單中的**群組**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="43c08-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="43c08-148">按一下群組設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="43c08-149">**選擇性︰**如果您想要**新增多個群組**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**完整群組名稱**，然後按一下核取方塊，將此群組新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="43c08-150">當您完成選取群組時，按一下 [選取] 按鈕，將它們新增到要指派給應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="43c08-151">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取群組的角色。</span><span class="sxs-lookup"><span data-stu-id="43c08-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="43c08-152">按一下 [指派] 按鈕，將應用程式指派至選取的群組。</span><span class="sxs-lookup"><span data-stu-id="43c08-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="43c08-153">稍待片刻，您已選取之群組內的使用者就能夠使用解決方案描述一節所述的方法，啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c08-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="43c08-154">如果這些都是動態群組，對於這些指派的群組內的使用者，這些指派可能會出現一些額外的處理延遲。</span><span class="sxs-lookup"><span data-stu-id="43c08-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="43c08-155">啟用自助應用程式存取以允許使用者尋找自己的應用程式</span><span class="sxs-lookup"><span data-stu-id="43c08-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="43c08-156">自助應用程式存取是讓使用者自行探索應用程式的絕佳方式，還可讓商務群組核准對那些應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="43c08-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="43c08-157">您可以讓商務群組直接從其存取面板，管理指派給「密碼單一登入應用程式」使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="43c08-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="43c08-158">若要啟用對應用程式的自助存取，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="43c08-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="43c08-159">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="43c08-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="43c08-160">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="43c08-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43c08-161">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="43c08-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43c08-162">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="43c08-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43c08-163">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="43c08-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="43c08-164">若在這裡沒看到您要的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="43c08-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="43c08-165">從該清單選取您要啟用自助存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c08-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="43c08-166">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [自助]。</span><span class="sxs-lookup"><span data-stu-id="43c08-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43c08-167">若要啟用此應用程式的自助式應用程式存取，請將 [要允許使用者要求此應用程式的存取權嗎?] 切換開關切換為 [是]。</span><span class="sxs-lookup"><span data-stu-id="43c08-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="43c08-168">接著，若要為要求存取此應用程式的使用者指派群組，請按一下 [要將指派的使用者新增至哪個群組呢?] 標籤旁的選取控制項，然後選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="43c08-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="43c08-169">**選擇性：**若要將使用者設定為必須經過商務核准才能存取應用程式，請將 [需要核准才能授予此應用程式的存取權嗎?] 切換開關設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="43c08-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="43c08-170">**選擇性：對於只使用密碼單一登入的應用程式，**若要讓那些商務核准者為核准的使用者指定傳送給此應用程式的密碼，請將 [要允許核准者為此應用程式設定使用者的密碼嗎?] 切換開關設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="43c08-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="43c08-171">**選擇性：**若要指定商務核准者以核准此應用程式存取權，請按一下 [哪些人員可核准此應用程式的存取權?] 標籤旁的選取控制項以選取最多 10 個商務核准者。</span><span class="sxs-lookup"><span data-stu-id="43c08-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="43c08-172">不支援群組。</span><span class="sxs-lookup"><span data-stu-id="43c08-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="43c08-173">**選擇性：****對於公開角色的應用程式，**若要將已獲得自助存取核准的使用者指派給角色，請按一下 [在此應用程式中應為使用者指派的角色為?] 旁的選取控制項，以選取要為這些使用者指派的角色。</span><span class="sxs-lookup"><span data-stu-id="43c08-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="43c08-174">按一下刀鋒視窗頂端的 [儲存] 按鈕以完成此動作。</span><span class="sxs-lookup"><span data-stu-id="43c08-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="43c08-175">完成自助應用程式設定之後，使用者可以瀏覽到其[應用程式存取面板](https://myapps.microsoft.com/)並按一下 [+新增] 按鈕以尋找您已啟用自助存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c08-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="43c08-176">商務核准者在其[應用程式存取面板](https://myapps.microsoft.com/)中也會看到通知。</span><span class="sxs-lookup"><span data-stu-id="43c08-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="43c08-177">您可以啟用電子郵件，通知他們有使用者已要求存取應用程式，需要他們核准。</span><span class="sxs-lookup"><span data-stu-id="43c08-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="43c08-178">這些核准只支援單一核准工作流程，這表示若您指定多個核准者，任何核准者都可以核准應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="43c08-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43c08-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43c08-179">Next steps</span></span>
[<span data-ttu-id="43c08-180">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="43c08-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
