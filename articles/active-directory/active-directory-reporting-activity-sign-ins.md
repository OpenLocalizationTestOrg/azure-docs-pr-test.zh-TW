---
title: "hello Azure Active Directory 入口網站中的 aaaSign 入活動報表 |Microsoft 文件"
description: "在 hello Azure Active Directory 入口網站的簡介 toosign 中活動報告"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="df244-103">Hello Azure Active Directory 入口網站中的登入活動報表</span><span class="sxs-lookup"><span data-stu-id="df244-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="df244-104">使用 Azure Active Directory (Azure AD) 報告 hello [Azure 入口網站](https://portal.azure.com)，您可以取得需要您的環境執行的方式 toodetermine hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="df244-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="df244-105">hello Azure Active Directory 中的報表架構包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="df244-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="df244-106">**活動**</span><span class="sxs-lookup"><span data-stu-id="df244-106">**Activity**</span></span> 
    - <span data-ttu-id="df244-107">**登入活動**– hello 使用量資訊的受管理的應用程式和使用者登入活動</span><span class="sxs-lookup"><span data-stu-id="df244-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="df244-108">**稽核記錄** - 關於使用者和群組管理、受管理應用程式和目錄活動的系統活動資訊。</span><span class="sxs-lookup"><span data-stu-id="df244-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="df244-109">**安全性**</span><span class="sxs-lookup"><span data-stu-id="df244-109">**Security**</span></span> 
    - <span data-ttu-id="df244-110">**高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。</span><span class="sxs-lookup"><span data-stu-id="df244-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="df244-111">如需詳細資訊，請參閱＜有風險的登入＞。</span><span class="sxs-lookup"><span data-stu-id="df244-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="df244-112">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="df244-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="df244-113">如需詳細資訊，請參閱＜標幟為有風險的使用者＞。</span><span class="sxs-lookup"><span data-stu-id="df244-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="df244-114">本主題提供 hello 登入活動的概觀。</span><span class="sxs-lookup"><span data-stu-id="df244-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="df244-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="df244-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="df244-116">誰可以存取 hello 資料？</span><span class="sxs-lookup"><span data-stu-id="df244-116">Who can access hello data?</span></span>
* <span data-ttu-id="df244-117">Hello 安全性系統管理員或安全性 Reader 角色中的使用者</span><span class="sxs-lookup"><span data-stu-id="df244-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="df244-118">全域管理員</span><span class="sxs-lookup"><span data-stu-id="df244-118">Global Admins</span></span>
* <span data-ttu-id="df244-119">任何使用者 (非系統管理員) 都可以存取自己的登入</span><span class="sxs-lookup"><span data-stu-id="df244-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="df244-120">Azure AD 授權您需要 tooaccess 登入活動嗎？</span><span class="sxs-lookup"><span data-stu-id="df244-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="df244-121">您的租用戶必須有與其相關聯的 Azure AD Premium 授權 toosee hello 所有最多登入活動報表</span><span class="sxs-lookup"><span data-stu-id="df244-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="df244-122">登入活動</span><span class="sxs-lookup"><span data-stu-id="df244-122">Signs-in activities</span></span>

<span data-ttu-id="df244-123">Hello hello 使用者登入報表所提供的資訊，您可以找到解答 tooquestions，例如：</span><span class="sxs-lookup"><span data-stu-id="df244-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="df244-124">Hello 登入使用者的模式是什麼？</span><span class="sxs-lookup"><span data-stu-id="df244-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="df244-125">一週內有多少使用者登入？</span><span class="sxs-lookup"><span data-stu-id="df244-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="df244-126">這些登入的 hello 狀態為何？</span><span class="sxs-lookup"><span data-stu-id="df244-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="df244-127">第一個項目點 tooall 登入活動資料**登入**hello 活動一節中**Azure Active**。</span><span class="sxs-lookup"><span data-stu-id="df244-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="df244-128">![登入活動](./media/active-directory-reporting-activity-sign-ins/61.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="df244-129">稽核記錄的預設清單檢視顯示︰</span><span class="sxs-lookup"><span data-stu-id="df244-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="df244-130">hello 相關的使用者</span><span class="sxs-lookup"><span data-stu-id="df244-130">hello related user</span></span>
- <span data-ttu-id="df244-131">hello 應用程式 hello 使用者已登入</span><span class="sxs-lookup"><span data-stu-id="df244-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="df244-132">hello 登入狀態</span><span class="sxs-lookup"><span data-stu-id="df244-132">hello sign-in status</span></span>
- <span data-ttu-id="df244-133">hello 登入時間</span><span class="sxs-lookup"><span data-stu-id="df244-133">hello sign-in time</span></span>

<span data-ttu-id="df244-134">![登入活動](./media/active-directory-reporting-activity-sign-ins/41.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-135">您可以自訂 hello 清單檢視中，依序按一下**資料行**hello 工具列中。</span><span class="sxs-lookup"><span data-stu-id="df244-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="df244-136">![登入活動](./media/active-directory-reporting-activity-sign-ins/19.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-137">這可讓您 toodisplay 其他欄位，或移除已顯示的欄位。</span><span class="sxs-lookup"><span data-stu-id="df244-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="df244-138">![登入活動](./media/active-directory-reporting-activity-sign-ins/42.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-139">依序按一下 hello 清單檢視中的項目，您會取得所有可用的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="df244-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="df244-140">![登入活動](./media/active-directory-reporting-activity-sign-ins/43.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="df244-141">篩選登入活動</span><span class="sxs-lookup"><span data-stu-id="df244-141">Filtering sign-in activities</span></span>

<span data-ttu-id="df244-142">關閉 hello toonarrow 報告資料 tooa 層級，適用於您，您可以篩選 hello 登入資料使用 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="df244-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="df244-143">時間間隔</span><span class="sxs-lookup"><span data-stu-id="df244-143">Time interval</span></span>
- <span data-ttu-id="df244-144">User</span><span class="sxs-lookup"><span data-stu-id="df244-144">User</span></span>
- <span data-ttu-id="df244-145">應用程式</span><span class="sxs-lookup"><span data-stu-id="df244-145">Application</span></span>
- <span data-ttu-id="df244-146">用戶端</span><span class="sxs-lookup"><span data-stu-id="df244-146">Client</span></span>
- <span data-ttu-id="df244-147">登入狀態</span><span class="sxs-lookup"><span data-stu-id="df244-147">Sign-in status</span></span>

<span data-ttu-id="df244-148">![登入活動](./media/active-directory-reporting-activity-sign-ins/44.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="df244-149">hello**時間間隔**篩選器可讓 tooyou toodefine hello 的時間範圍內傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="df244-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="df244-150">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="df244-150">Possible values are:</span></span>

- <span data-ttu-id="df244-151">1 個月</span><span class="sxs-lookup"><span data-stu-id="df244-151">1 month</span></span>
- <span data-ttu-id="df244-152">7 天</span><span class="sxs-lookup"><span data-stu-id="df244-152">7 days</span></span>
- <span data-ttu-id="df244-153">24 小時</span><span class="sxs-lookup"><span data-stu-id="df244-153">24 hours</span></span>
- <span data-ttu-id="df244-154">自訂</span><span class="sxs-lookup"><span data-stu-id="df244-154">Custom</span></span>

<span data-ttu-id="df244-155">當您選取自訂時間範圍時，可以設定開始時間和結束時間。</span><span class="sxs-lookup"><span data-stu-id="df244-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="df244-156">hello**使用者**篩選器可讓您 toospecify hello 名稱或 hello 使用者主體名稱 (UPN) 您關心的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="df244-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="df244-157">hello**應用程式**篩選器可讓您 toospecify hello 您關心的 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="df244-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="df244-158">hello**用戶端**篩選器可讓您 toospecify hello 裝置，您很重視的資訊。</span><span class="sxs-lookup"><span data-stu-id="df244-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="df244-159">hello**登入狀態**篩選器可讓您的下列篩選器的 hello tooselect 其中一個：</span><span class="sxs-lookup"><span data-stu-id="df244-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="df244-160">全部</span><span class="sxs-lookup"><span data-stu-id="df244-160">All</span></span>
- <span data-ttu-id="df244-161">成功</span><span class="sxs-lookup"><span data-stu-id="df244-161">Success</span></span>
- <span data-ttu-id="df244-162">失敗</span><span class="sxs-lookup"><span data-stu-id="df244-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="df244-163">登入活動捷徑</span><span class="sxs-lookup"><span data-stu-id="df244-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="df244-164">此外 tooAzure Active Directory，hello Azure 入口網站為您提供兩個其他的進入點 toosign 中活動資料：</span><span class="sxs-lookup"><span data-stu-id="df244-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="df244-165">使用者和群組</span><span class="sxs-lookup"><span data-stu-id="df244-165">Users and groups</span></span>
- <span data-ttu-id="df244-166">企業應用程式</span><span class="sxs-lookup"><span data-stu-id="df244-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="df244-167">使用者和群組登入活動</span><span class="sxs-lookup"><span data-stu-id="df244-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="df244-168">Hello hello 使用者登入報表所提供的資訊，您可以找到解答 tooquestions，例如：</span><span class="sxs-lookup"><span data-stu-id="df244-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="df244-169">Hello 登入使用者的模式是什麼？</span><span class="sxs-lookup"><span data-stu-id="df244-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="df244-170">一週內有多少使用者登入？</span><span class="sxs-lookup"><span data-stu-id="df244-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="df244-171">這些登入的 hello 狀態為何？</span><span class="sxs-lookup"><span data-stu-id="df244-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="df244-172">您的進入點 toothis 資料是 hello 使用者登入在 hello 圖形**概觀**區段**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="df244-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="df244-173">![登入活動](./media/active-directory-reporting-activity-sign-ins/45.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-174">hello 使用者登入圖表會顯示每週彙總的符號集在給定的時間週期內的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="df244-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="df244-175">hello 的 hello 預設期間為 30 天。</span><span class="sxs-lookup"><span data-stu-id="df244-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="df244-176">![登入活動](./media/active-directory-reporting-activity-sign-ins/46.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-177">當您按一下 hello 登入圖形中的哪一天時，您會取得這一天的 hello 登入活動的詳細的清單。</span><span class="sxs-lookup"><span data-stu-id="df244-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="df244-178">![登入活動](./media/active-directory-reporting-activity-sign-ins/41.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-179">每個資料列 hello 登入活動的清單提供 hello hello 選取登入如需詳細的資訊：</span><span class="sxs-lookup"><span data-stu-id="df244-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="df244-180">誰已登入？</span><span class="sxs-lookup"><span data-stu-id="df244-180">Who has signed in?</span></span>
* <span data-ttu-id="df244-181">什麼是 hello 相關 UPN 嗎？</span><span class="sxs-lookup"><span data-stu-id="df244-181">What was hello related UPN?</span></span>
* <span data-ttu-id="df244-182">哪些應用程式的 hello hello 登入的目標？</span><span class="sxs-lookup"><span data-stu-id="df244-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="df244-183">什麼是 hello hello 登入的 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="df244-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="df244-184">Hello hello 登入的狀態是什麼？</span><span class="sxs-lookup"><span data-stu-id="df244-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="df244-185">hello**登入**選項可讓您所有的使用者登入的完整概觀。</span><span class="sxs-lookup"><span data-stu-id="df244-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="df244-186">![登入活動](./media/active-directory-reporting-activity-sign-ins/51.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="df244-187">受管理應用程式的使用情況</span><span class="sxs-lookup"><span data-stu-id="df244-187">Usage of managed applications</span></span>

<span data-ttu-id="df244-188">利用登入資料以應用程式為主的檢視，您可以回答下列問題︰</span><span class="sxs-lookup"><span data-stu-id="df244-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="df244-189">誰在使用我的應用程式？</span><span class="sxs-lookup"><span data-stu-id="df244-189">Who is using my applications?</span></span>
* <span data-ttu-id="df244-190">Hello 前 3 的應用程式在組織中有哪些？</span><span class="sxs-lookup"><span data-stu-id="df244-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="df244-191">我最近已推出一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="df244-191">I have recently rolled out an application.</span></span> <span data-ttu-id="df244-192">它的情況為何？</span><span class="sxs-lookup"><span data-stu-id="df244-192">How is it doing?</span></span>

<span data-ttu-id="df244-193">是 hello 前 3 的應用程式在 hello hello 過去 30 天內報表內組織中的項目點 toothis 資料**概觀**區段**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="df244-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="df244-194">![登入活動](./media/active-directory-reporting-activity-sign-ins/64.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-195">hello 應用程式使用量圖形每週的彙總的前 3 名應用程式在指定的時段內登入。</span><span class="sxs-lookup"><span data-stu-id="df244-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="df244-196">hello 的 hello 預設期間為 30 天。</span><span class="sxs-lookup"><span data-stu-id="df244-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="df244-197">![登入活動](./media/active-directory-reporting-activity-sign-ins/47.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="df244-198">如果您想要您可以設定特定的應用程式的 hello 焦點。</span><span class="sxs-lookup"><span data-stu-id="df244-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="df244-199">![報告](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "報告")</span><span class="sxs-lookup"><span data-stu-id="df244-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="df244-200">當您按一下 hello 應用程式使用量圖表中的哪一天時，您會取得 hello 登入活動的詳細的清單。</span><span class="sxs-lookup"><span data-stu-id="df244-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="df244-201">![登入活動](./media/active-directory-reporting-activity-sign-ins/48.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="df244-202">hello**登入**選項可讓您所有的登入事件 tooyour 應用程式的完整概觀。</span><span class="sxs-lookup"><span data-stu-id="df244-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="df244-203">![登入活動](./media/active-directory-reporting-activity-sign-ins/49.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="df244-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="df244-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df244-204">Next steps</span></span>

<span data-ttu-id="df244-205">如果您想深入了解登入活動錯誤碼 tooknow，請參閱 hello[登入活動報表中的錯誤碼 hello Azure Active Directory 網站](active-directory-reporting-activity-sign-ins-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="df244-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

