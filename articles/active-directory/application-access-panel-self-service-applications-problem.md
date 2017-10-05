---
title: "使用自助應用程式存取時遇到問題 | Microsoft Docs"
description: "針對自助應用程式存取的相關問題進行疑難排解"
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
ms.reviewer: japere
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="5a389-103">使用自助應用程式存取時遇到問題</span><span class="sxs-lookup"><span data-stu-id="5a389-103">Problem using self-service application access</span></span>

<span data-ttu-id="5a389-104">自助應用程式存取是讓使用者自行探索應用程式的絕佳方式，還可讓商務群組核准對那些應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="5a389-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="5a389-105">您可以讓商務群組直接從其存取面板，管理指派給「密碼單一登入應用程式」使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="5a389-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="5a389-106">對於您想要允許使用者自行探索和要求存取的任何應用程式，您必須啟用**自助應用程式存取**，使用者才能從存取面板自行探索應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a389-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="5a389-107">首先檢查的一般問題</span><span class="sxs-lookup"><span data-stu-id="5a389-107">General issues to check first</span></span>

-   <span data-ttu-id="5a389-108">請確定已正確設定自助應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="5a389-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="5a389-109">請參閱＜如何設定自助應用程式存取＞。</span><span class="sxs-lookup"><span data-stu-id="5a389-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="5a389-110">請確定已允許使用者或群組要求自助應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="5a389-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="5a389-111">請確定使用者造訪正確的位置來要求自助應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="5a389-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="5a389-112">使用者可以瀏覽至其[應用程式存取面板](https://myapps.microsoft.com/)，並按一下 [+新增] 按鈕，以尋找您已啟用自助存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a389-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="5a389-113">如果最近才剛設定自助應用程式存取，請在幾分鐘之後嘗試登入並再次登出使用者的存取面板，查明自助存取變更是否出現。</span><span class="sxs-lookup"><span data-stu-id="5a389-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="5a389-114">如何設定自助應用程式存取</span><span class="sxs-lookup"><span data-stu-id="5a389-114">How to configure self-service application access</span></span>

<span data-ttu-id="5a389-115">若要啟用對應用程式的自助存取，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="5a389-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="5a389-116">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="5a389-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5a389-117">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="5a389-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5a389-118">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="5a389-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5a389-119">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5a389-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5a389-120">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5a389-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5a389-121">若在這裡沒看到您要的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5a389-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5a389-122">從該清單選取您要啟用自助存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a389-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="5a389-123">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [自助]。</span><span class="sxs-lookup"><span data-stu-id="5a389-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5a389-124">若要啟用此應用程式的自助式應用程式存取，請將 [要允許使用者要求此應用程式的存取權嗎?] 切換開關切換為 [是]。</span><span class="sxs-lookup"><span data-stu-id="5a389-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="5a389-125">接著，若要為要求存取此應用程式的使用者指派群組，請按一下 [要將指派的使用者新增至哪個群組呢?] 標籤旁的選取控制項，然後選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="5a389-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="5a389-126">**選擇性：**若要將使用者設定為必須經過商務核准才能存取應用程式，請將 [需要核准才能授予此應用程式的存取權嗎?] 切換開關設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="5a389-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="5a389-127">**選擇性：對於只使用密碼單一登入的應用程式，**若要讓那些商務核准者為核准的使用者指定傳送給此應用程式的密碼，請將 [要允許核准者為此應用程式設定使用者的密碼嗎?] 切換開關設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="5a389-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="5a389-128">**選擇性：**若要指定商務核准者以核准此應用程式存取權，請按一下 [哪些人員可核准此應用程式的存取權?] 標籤旁的選取控制項以選取最多 10 個商務核准者。</span><span class="sxs-lookup"><span data-stu-id="5a389-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="5a389-129">不支援群組。</span><span class="sxs-lookup"><span data-stu-id="5a389-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="5a389-130">**選擇性：****對於公開角色的應用程式，**若要將已獲得自助存取核准的使用者指派給角色，請按一下 [在此應用程式中應為使用者指派的角色為?] 旁的選取控制項，以選取要為這些使用者指派的角色。</span><span class="sxs-lookup"><span data-stu-id="5a389-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="5a389-131">按一下刀鋒視窗頂端的 [儲存] 按鈕以完成此動作。</span><span class="sxs-lookup"><span data-stu-id="5a389-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="5a389-132">完成自助應用程式設定之後，使用者可以瀏覽到其[應用程式存取面板](https://myapps.microsoft.com/)並按一下 [+新增] 按鈕以尋找您已啟用自助存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a389-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="5a389-133">商務核准者在其[應用程式存取面板](https://myapps.microsoft.com/)中也會看到通知。</span><span class="sxs-lookup"><span data-stu-id="5a389-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="5a389-134">您可以啟用電子郵件，通知他們有使用者已要求存取應用程式，需要他們核准。</span><span class="sxs-lookup"><span data-stu-id="5a389-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="5a389-135">這些核准只支援單一核准工作流程，這表示若您指定多個核准者，任何核准者都可以核准應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="5a389-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="5a389-136">如果這些疑難排解步驟無法解決問題</span><span class="sxs-lookup"><span data-stu-id="5a389-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="5a389-137">使用下列資訊 (若有的話) 開啟支援票證︰</span><span class="sxs-lookup"><span data-stu-id="5a389-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="5a389-138">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="5a389-138">Correlation error ID</span></span>

-   <span data-ttu-id="5a389-139">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="5a389-139">UPN (user email address)</span></span>

-   <span data-ttu-id="5a389-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="5a389-140">TenantID</span></span>

-   <span data-ttu-id="5a389-141">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="5a389-141">Browser type</span></span>

-   <span data-ttu-id="5a389-142">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="5a389-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5a389-143">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="5a389-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a389-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a389-144">Next steps</span></span>
[<span data-ttu-id="5a389-145">設定 Azure Active Directory 進行自助服務群組管理</span><span class="sxs-lookup"><span data-stu-id="5a389-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
