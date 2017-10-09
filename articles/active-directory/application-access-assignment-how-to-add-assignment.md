---
title: "aaaHow tooassign 使用者和群組 tooan 應用程式 |Microsoft 文件"
description: "將使用者指派 toogrant toohello 應用程式的存取"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="bc8d2-103">如何 tooassign 使用者和群組 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc8d2-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="bc8d2-104">您的使用者可以執行以下的 hello 特定應用程式之前，您需要 toofirst **toohello 應用程式將它們指派**toogrant 這些使用者存取：</span><span class="sxs-lookup"><span data-stu-id="bc8d2-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="bc8d2-105">存取應用程式由**直接瀏覽 toohello 應用程式的 URL** （也稱為 SP 初始化登入）。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="bc8d2-106">存取應用程式使用 hello**使用者存取 URL**應用程式上**屬性**頁面 （也稱為 IDP 初始化登入）。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="bc8d2-107">看到應用程式出現在其[應用程式存取面板](https://myapps.microsoft.com/)或行動應用程式上。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="bc8d2-108">看到應用程式出現在其 [Office 365 應用程式啟動程式](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a)上。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="bc8d2-109">方法 tooassign 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc8d2-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="bc8d2-110">使用 Azure Active Directory 指派應用程式有 3 種方法：</span><span class="sxs-lookup"><span data-stu-id="bc8d2-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="bc8d2-111">指派給使用者直接 tooan 應用程式做為系統管理員</span><span class="sxs-lookup"><span data-stu-id="bc8d2-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="bc8d2-112">將群組指派直接 tooan 應用程式做為系統管理員</span><span class="sxs-lookup"><span data-stu-id="bc8d2-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="bc8d2-113">啟用自助服務應用程式存取 tooallow 使用者 toofind 自己的應用程式</span><span class="sxs-lookup"><span data-stu-id="bc8d2-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="bc8d2-114">以系統管理員身分直接指派使用者</span><span class="sxs-lookup"><span data-stu-id="bc8d2-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="bc8d2-115">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bc8d2-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="bc8d2-116">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bc8d2-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bc8d2-117">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bc8d2-118">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bc8d2-119">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bc8d2-120">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bc8d2-121">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bc8d2-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bc8d2-122">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="bc8d2-123">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bc8d2-124">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="bc8d2-125">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="bc8d2-126">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="bc8d2-127">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="bc8d2-128">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="bc8d2-129">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="bc8d2-130">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="bc8d2-131">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="bc8d2-132">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="bc8d2-133">一段短時間，您已選取的 hello 使用者是使用這些應用程式 hello hello 方案描述 部分中所述的方法可以 toolaunch。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="bc8d2-134">將群組指派直接 tooan 應用程式做為系統管理員</span><span class="sxs-lookup"><span data-stu-id="bc8d2-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="bc8d2-135">tooassign 一或多個群組 tooan 的應用程式直接管理，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bc8d2-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="bc8d2-136">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bc8d2-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bc8d2-137">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bc8d2-138">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bc8d2-139">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bc8d2-140">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bc8d2-141">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bc8d2-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bc8d2-142">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="bc8d2-143">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bc8d2-144">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="bc8d2-145">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="bc8d2-146">型別在 hello**完整的群組名稱**您感興趣指派到 hello hello 群組的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="bc8d2-147">將滑鼠停留在 hello**群組**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="bc8d2-148">按一下 [hello] 核取方塊下一步 toohello 群組的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="bc8d2-149">**選擇性：**如果您希望太**新增多個群組**，在另一個類型**完整的群組名稱**到 hello**依名稱或電子郵件地址搜尋**搜尋方塊中，按一下此群組 toohello hello 核取方塊 tooadd**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="bc8d2-150">當您完成選取群組，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="bc8d2-151">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 群組您已選取。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="bc8d2-152">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的群組。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="bc8d2-153">一段短時間，您選取的 hello 群組內的 hello 使用者都是可以 toolaunch 使用這些應用程式 hello hello 方案描述 部分中所述的方法。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="bc8d2-154">如果這些都是動態群組，對於這些指派的群組內的使用者，這些指派可能會出現一些額外的處理延遲。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="bc8d2-155">啟用自助服務應用程式存取 tooallow 使用者 toofind 自己的應用程式</span><span class="sxs-lookup"><span data-stu-id="bc8d2-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="bc8d2-156">自助應用程式的存取是很好的方法 tooallow 使用者 tooself-探索應用程式，請選擇性地允許 hello 商務群組 tooapprove 存取 toothose 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="bc8d2-157">您可以允許 hello 商務群組 toomanage hello 認證指派 toothose 使用者從他們的存取面板的密碼單一登入應用程式權限。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="bc8d2-158">tooenable 自助應用程式存取 tooan 應用程式，下列的後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bc8d2-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="bc8d2-159">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bc8d2-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bc8d2-160">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bc8d2-161">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bc8d2-162">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bc8d2-163">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="bc8d2-164">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bc8d2-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bc8d2-165">選取您想要 tooenable 自助存取 toofrom hello 清單 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="bc8d2-166">一旦 hello 應用程式載入時，按一下 **自助**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bc8d2-167">tooenable 自助式應用程式存取此應用程式中，開啟 hello**允許使用者應用程式的存取 toothis toorequest？**太切換**[是]。**</span><span class="sxs-lookup"><span data-stu-id="bc8d2-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="bc8d2-168">Tooselect hello 群組 toowhich 要求使用者應加入 toothis 應用程式的存取，接下來，按一下 hello 選取器下一個 toohello 標籤**toowhich 群組應該指派給新增的使用者？**並選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="bc8d2-169">**選擇性：**如果您想 toorequire 商務核准允許使用者存取之前，設定 hello**之前授與存取 toothis 應用程式需要核准？**太切換**是**。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="bc8d2-170">**選用： 為應用程式上，使用密碼單一登**如果您想 tooallow toothis 應用程式的核准的使用者傳送這些商務核准者 toospecify hello 密碼時，設定 hello**允許核准者 tooset此應用程式的使用者的密碼嗎？**太切換**是**。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="bc8d2-171">**選擇性：** toospecify hello 公司核准者允許 tooapprove 存取 toothis 應用程式中，按一下 hello 選取器下一個 toohello 標籤**誰 tooapprove 存取 toothis 應用程式？** tooselect 向上too10 個別商務核准者。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="bc8d2-172">不支援群組。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="bc8d2-173">**選擇性：** **的應用程式的公開角色**，如果您想 tooa tooassign 自助核准的使用者的角色，按一下 下一步 toohello 的 hello 選取器**toowhich 角色應該指派給使用者在此應用程式嗎？** tooselect hello 角色 toowhich 應該指派這些使用者。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="bc8d2-174">按一下 hello**儲存**在 hello 刀鋒視窗 toofinish hello 最上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="bc8d2-175">一旦您完成自助應用程式組態設定，使用者可以瀏覽 tootheir[應用程式存取面板](https://myapps.microsoft.com/)按一下 hello **+ 加**按鈕 toofind hello 應用程式 toowhich 已啟用自助存取。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="bc8d2-176">商務核准者在其[應用程式存取面板](https://myapps.microsoft.com/)中也會看到通知。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="bc8d2-177">您可以啟用在使用者要求存取 tooan 應用程式需要核准時，通知他們的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="bc8d2-178">這些核准會支援單一核准工作流程，這表示如果您指定多個核准者，任何單一核准者可能核准者存取 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc8d2-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc8d2-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc8d2-179">Next steps</span></span>
[<span data-ttu-id="bc8d2-180">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="bc8d2-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
