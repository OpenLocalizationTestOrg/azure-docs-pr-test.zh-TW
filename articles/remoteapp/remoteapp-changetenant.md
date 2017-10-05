---
title: "變更 Azure RemoteApp 中 Azure Active Directory 租用戶 | Microsoft Docs"
description: "了解如何變更與 Azure RemoteApp 相關聯的 Azure Active Directory 租用戶"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 7c6c4ded8a11d8399968b2c32aff055d7f3ae5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-azure-active-directory-tenant-in-azure-remoteapp"></a><span data-ttu-id="e7f51-103">變更 Azure RemoteApp 中 Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="e7f51-103">Change the Azure Active Directory tenant in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e7f51-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="e7f51-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e7f51-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="e7f51-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e7f51-106">Azure RemoteApp 使用 Azure Active Directory (Azure AD) 以允許使用者存取權。</span><span class="sxs-lookup"><span data-stu-id="e7f51-106">Azure RemoteApp uses Azure Active Directory (Azure AD) to allow user access.</span></span> <span data-ttu-id="e7f51-107">您在 Azure RemoteApp 中只能使用與 Azure 訂閱相關聯的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e7f51-107">The only Azure AD tenant that you can use in Azure RemoteApp is the one associated with the Azure subscription.</span></span> <span data-ttu-id="e7f51-108">您可以在入口網站的 [設定]  頁面上檢視相關聯的訂閱。</span><span class="sxs-lookup"><span data-stu-id="e7f51-108">You can view the associated subscription on the **Settings** page in the portal.</span></span> <span data-ttu-id="e7f51-109">查看 [訂閱] 索引標籤上的 [目錄] 資料行。</span><span class="sxs-lookup"><span data-stu-id="e7f51-109">Look at the **Directory** column on the **Subscriptions** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="e7f51-110">此變更若要成功，首先從所有 Azure RemoteApp 集合移除現有 Azure Active Directory 租用戶中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="e7f51-110">For this change to succeed, first remove all users from the existing Azure Active Directory tenant from all Azure RemoteApp collections.</span></span> <span data-ttu-id="e7f51-111">若要這樣做，請移至 Azure 入口網站，並移至 [Azure RemoteApp]  索引標籤，然後開啟每個 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="e7f51-111">To do this, go to the Azure Portal, go to the **Azure RemoteApp** tab and open every Azure RemoteApp collection.</span></span> <span data-ttu-id="e7f51-112">移至 [使用者]  索引標籤，並移除屬於您目前 Azure Active Directory 租用戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="e7f51-112">Go to the **Users** tab and remove users that belong to your current Azure Active Directory tenant.</span></span> <span data-ttu-id="e7f51-113">針對所有現有 Azure RemoteApp 集合重複進行。</span><span class="sxs-lookup"><span data-stu-id="e7f51-113">Repeat for all existing Azure RemoteApp collections.</span></span> <span data-ttu-id="e7f51-114">不這麼做，您將無法建立或修正集合。</span><span class="sxs-lookup"><span data-stu-id="e7f51-114">Without doing this, you will not be able to create or patch collections.</span></span>
> 
> 

<span data-ttu-id="e7f51-115">如果您想要使用不同的租用戶，請使用下列步驟來變更訂閱的關聯：</span><span class="sxs-lookup"><span data-stu-id="e7f51-115">If you want to use a different tenant, use these steps to change the association with your subscription:</span></span>

1. <span data-ttu-id="e7f51-116">在入口網站中，移除您獲授與 Azure RemoteApp 集合存取權的任何 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="e7f51-116">In the portal, remove any Azure AD users to which you’ve given access to Azure RemoteApp collections.</span></span> <span data-ttu-id="e7f51-117">(作法請參閱上述的注意事項。)</span><span class="sxs-lookup"><span data-stu-id="e7f51-117">(See the note above for steps on how to do this.)</span></span>
2. <span data-ttu-id="e7f51-118">設定 Microsoft 帳戶 (先前稱為 Live ID) 做為服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e7f51-118">Set a Microsoft account (formerly called a Live ID) as the Service administrator.</span></span> <span data-ttu-id="e7f51-119">(不確定是否已經是服務管理員嗎？</span><span class="sxs-lookup"><span data-stu-id="e7f51-119">(Don't know if you already are the service admin?</span></span> <span data-ttu-id="e7f51-120">您可以按一下 [設定] -> [系統管理員] 來查看。)接下來，以下是變更的方法：</span><span class="sxs-lookup"><span data-stu-id="e7f51-120">You can find out by clicking **Settings -> Administrators**.) Now, here's how you change that:</span></span>
   
   1. <span data-ttu-id="e7f51-121">在右上角按一下使用者，然後按一下 [檢視我的帳單] 。</span><span class="sxs-lookup"><span data-stu-id="e7f51-121">Click the user in the upper right corner, and then click **View my bill**.</span></span>
   2. <span data-ttu-id="e7f51-122">按一下訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7f51-122">Click the subscription.</span></span> <span data-ttu-id="e7f51-123">然後，在新的頁面上，向下捲動並按一下右側的 [訂用帳戶詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="e7f51-123">Then, on the new page, scroll down and click **Edit subscription details** in the right.</span></span> <span data-ttu-id="e7f51-124">(大約在底部右側中間位置，若有助於您尋找。)</span><span class="sxs-lookup"><span data-stu-id="e7f51-124">(Sort of the middle bottom right, if that helps you find it.)</span></span>
   3. <span data-ttu-id="e7f51-125">輸入應是服務管理員的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7f51-125">Type the Microsoft account for the user that should be the service admin.</span></span>
3. <span data-ttu-id="e7f51-126">登出入口網站，然後使用您在上一個步驟指定的 Microsoft 帳戶重新登入。</span><span class="sxs-lookup"><span data-stu-id="e7f51-126">Now, sign out of the portal, and then sign back in with the Microsoft account you specified in the previous step.</span></span>
4. <span data-ttu-id="e7f51-127">依序按一下 [新增] > [應用程式服務] > [Active Directory] > [目錄] > [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="e7f51-127">Click **New -> App Services -> Active Directory -> Directory -> Custom Create**.</span></span>
5. <span data-ttu-id="e7f51-128">在 [目錄] 下方，選擇 [使用現有的目錄]。</span><span class="sxs-lookup"><span data-stu-id="e7f51-128">Under **Directory**, choose **Use existing directory**.</span></span> <span data-ttu-id="e7f51-129">我們現在必須讓您登出入口網站，請選取 [我已經準備好要登出了] 。</span><span class="sxs-lookup"><span data-stu-id="e7f51-129">We're going to have to sign you out of the portal now, so choose **I am ready to be signed out now**.</span></span>
6. <span data-ttu-id="e7f51-130">以要新增的目錄之全域管理員身分再次登入入口網站。</span><span class="sxs-lookup"><span data-stu-id="e7f51-130">Sign back into the portal as a global admin of the directory you want to add.</span></span> <span data-ttu-id="e7f51-131">(如果您還不是全域管理員，您將會經歷一回的登入然後登出。)</span><span class="sxs-lookup"><span data-stu-id="e7f51-131">(If you weren't already a global admin, you will be after a round of sign in and then sign out.)</span></span>
7. <span data-ttu-id="e7f51-132">系統會在您登入時詢問您是否要使用訂用帳戶現有的 AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e7f51-132">You'll be asked when you sign in if you want to use your existing AD tenant with your subscription.</span></span> <span data-ttu-id="e7f51-133">按一下 [繼續]，然後按一下 [立即登出]。</span><span class="sxs-lookup"><span data-stu-id="e7f51-133">Click **Continue**, and then click **Sign out now**.</span></span>
8. <span data-ttu-id="e7f51-134">重新登入，然後返回 [設定] -> [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="e7f51-134">Sign back in again, and go back to **Settings -> Subscriptions**.</span></span> <span data-ttu-id="e7f51-135">選取您的訂用帳戶，然後按一下 [編輯目錄] 。</span><span class="sxs-lookup"><span data-stu-id="e7f51-135">Select your subscription, and then click **Edit Directory**.</span></span> <span data-ttu-id="e7f51-136">選取您想要使用的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e7f51-136">Select the Azure AD tenant that you want to use.</span></span>

<span data-ttu-id="e7f51-137">您現在可以使用新的 Azure AD 租用戶來控制 Azure 訂用帳戶的存取權，以及在 Azure RemoteApp 中設定使用者存取權。</span><span class="sxs-lookup"><span data-stu-id="e7f51-137">You can now use the new Azure AD tenant to control access to the Azure subscription and to configure user access in Azure RemoteApp.</span></span>

