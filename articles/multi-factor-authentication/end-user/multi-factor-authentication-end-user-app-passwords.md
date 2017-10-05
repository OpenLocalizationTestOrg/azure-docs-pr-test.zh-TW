---
title: "如何在 Azure MFA 中使用應用程式密碼？ | Microsoft Docs"
description: "本頁面將協助使用者了解什麼是應用程式密碼，以及它們在 Azure MFA 方面的用途。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: fe8fb3b6e249fbe6bc0f8e55c4267f09cfcfcff5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="920df-104">什麼是 Azure Multi-Factor Authentication 中的應用程式密碼？</span><span class="sxs-lookup"><span data-stu-id="920df-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="920df-105">有些非瀏覽器應用程式 (例如使用 Exchange Active Sync 的 Apple 原生電子郵件用戶端) 目前不支援 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="920df-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="920df-106">Multi-Factor Authentication 會對每個使用者啟用。</span><span class="sxs-lookup"><span data-stu-id="920df-106">Multi-factor authentication is enabled per user.</span></span> <span data-ttu-id="920df-107">這表示如果使用者已啟用 Multi-Factor Authentication，並嘗試使用非瀏覽器應用程式，他們將無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="920df-107">This means that if a user has been enabled for multi-factor authentication and they are attempting to use non-browser apps, they will be unable to do so.</span></span> <span data-ttu-id="920df-108">應用程式密碼允許發生此情形。</span><span class="sxs-lookup"><span data-stu-id="920df-108">An app password allows this to occur.</span></span>

<span data-ttu-id="920df-109">擁有應用程式密碼後，您可使用此密碼來取代這些非瀏覽器應用程式的原始密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-109">Once you have an app password, you use this in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="920df-110">這是因為當您註冊進行雙步驟驗證時，就是告知 Microsoft 如果有人使用您的密碼登入但未執行第二次驗證，則不允許他們登入。</span><span class="sxs-lookup"><span data-stu-id="920df-110">This is because when you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span></span> <span data-ttu-id="920df-111">您電話上的 Apple 原生電子郵件用戶端無法以您的身份登入，因為它不能要求進行雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="920df-111">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="920df-112">這個的解決方法是建立一個您不會每天使用的更安全應用程式密碼，而且它也只針對不支援雙步驟驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="920df-112">The solution for this is to create a more secure app password that you don't use day-to-day, but only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="920df-113">使用應用程式密碼可讓應用程式略過 Multi-Factor Authentication 並繼續運作。</span><span class="sxs-lookup"><span data-stu-id="920df-113">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span></span>

> [!NOTE]
> <span data-ttu-id="920df-114">Office 2013 用戶端 (包括 Outlook) 支援新式驗證通訊協定，而且可搭配雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="920df-114">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span>  <span data-ttu-id="920df-115">這表示一旦啟用後，應用程式密碼就不需要使用於 Office 2013 用戶端。</span><span class="sxs-lookup"><span data-stu-id="920df-115">This means that once enabled, app passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="920df-116">如需詳細資訊，請參閱[發表的 Office 2013 新式驗證公開預覽](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。</span><span class="sxs-lookup"><span data-stu-id="920df-116">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-to-use-app-passwords"></a><span data-ttu-id="920df-117">如何使用應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-117">How to use app passwords</span></span>
<span data-ttu-id="920df-118">以下是使用應用程式密碼的一些注意事項。</span><span class="sxs-lookup"><span data-stu-id="920df-118">The following are some things to remember on how to use app passwords.</span></span>

* <span data-ttu-id="920df-119">您不用自行建立應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-119">You don't create your own app passwords.</span></span> <span data-ttu-id="920df-120">它們是自動產生的。</span><span class="sxs-lookup"><span data-stu-id="920df-120">Instead, they are automatically generated.</span></span> <span data-ttu-id="920df-121">因為每個應用程式只需要輸入應用程式密碼一次，所以使用較複雜且自動產生的密碼比您自創一個可記住的密碼更為安全。</span><span class="sxs-lookup"><span data-stu-id="920df-121">Since you only have to enter the app password once per app, it's safer to use a more complex, automatically generated password rather than making one that you can remember.</span></span>
* <span data-ttu-id="920df-122">每位使用者的密碼目前以 40 組為限。</span><span class="sxs-lookup"><span data-stu-id="920df-122">Currently there is a limit of 40 passwords per user.</span></span> <span data-ttu-id="920df-123">如果您嘗試在達到此限制後建立密碼，系統會提示您刪除其中一個現有的應用程式密碼，然後才能建立新密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-123">If you attempt to create one after you have reached the limit, you will be prompted to delete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="920df-124">您應該為每個裝置 (而非每個應用程式) 使用一個應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-124">You should use one app password per device, not per application.</span></span> <span data-ttu-id="920df-125">例如，您可以為膝上型電腦建立一個應用程式密碼，並將該應用程式密碼使用於該膝上型電腦上的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="920df-125">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="920df-126">接著，建立第二個應用程式密碼用於您桌面上的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="920df-126">Then, create a second app password to use for all your apps on your desktop.</span></span> 
* <span data-ttu-id="920df-127">您在第一次註冊進行雙步驟驗證時會獲得一個應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-127">You are given one app password the first time you register for two-step verification.</span></span>  <span data-ttu-id="920df-128">如果您需要其他密碼，您可加以建立。</span><span class="sxs-lookup"><span data-stu-id="920df-128">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="920df-129">建立和刪除應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-129">Creating and deleting app passwords</span></span>
<span data-ttu-id="920df-130">在初次登入期間，您會獲得可供使用的應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-130">During your initial sign-in you are given an app password that you can use.</span></span>  <span data-ttu-id="920df-131">此外，您也可以稍後再建立和刪除應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-131">Additionally you can also create and delete app passwords later on.</span></span>  <span data-ttu-id="920df-132">您執行此動作的方式取決於您使用 Multi-Factor Authentication 的方式。</span><span class="sxs-lookup"><span data-stu-id="920df-132">How you do this depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="920df-133">回答下列問題來判斷您應該到哪裡來管理應用程式密碼：</span><span class="sxs-lookup"><span data-stu-id="920df-133">Answer the following questions to determine where you should go to manage app passwords:</span></span> 

1. <span data-ttu-id="920df-134">您的個人 Microsoft 帳戶是否使用雙步驟驗證？</span><span class="sxs-lookup"><span data-stu-id="920df-134">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="920df-135">如果是，您應該參閱[應用程式密碼和雙步驟驗證](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification)一文的說明。</span><span class="sxs-lookup"><span data-stu-id="920df-135">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="920df-136">如果不是，繼續回答第二個問題。</span><span class="sxs-lookup"><span data-stu-id="920df-136">If no, continue to question two.</span></span>

2. <span data-ttu-id="920df-137">好，所以您的工作或學校帳戶使用雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="920df-137">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="920df-138">您是否用這些帳戶登入 Office 365 應用程式？</span><span class="sxs-lookup"><span data-stu-id="920df-138">Do you use it to sign in to Office 365 apps?</span></span> <span data-ttu-id="920df-139">如果是，您應該參閱[建立 Office 365 應用程式密碼](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183)的說明。</span><span class="sxs-lookup"><span data-stu-id="920df-139">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="920df-140">如果不是，繼續回答第三個問題。</span><span class="sxs-lookup"><span data-stu-id="920df-140">If no, continue to question three.</span></span> 

3. <span data-ttu-id="920df-141">您是否搭配 Microsoft Azure 使用雙步驟驗證？</span><span class="sxs-lookup"><span data-stu-id="920df-141">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="920df-142">如果是，繼續移至本文中[在 Azure 入口網站中管理應用程式密碼](#manage-app-passwords-in-the-Azure-portal)一節。</span><span class="sxs-lookup"><span data-stu-id="920df-142">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="920df-143">如果不是，繼續回答第四個問題。</span><span class="sxs-lookup"><span data-stu-id="920df-143">If no, continue to question four.</span></span>

4. <span data-ttu-id="920df-144">不確定您在哪裡使用雙步驟驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="920df-144">Not sure where you use two-step verification?</span></span> <span data-ttu-id="920df-145">繼續移至本文中[使用 MyApps 入口網站管理應用程式密碼](#manage-app-passwords-with-the-myapps-portal)一節。</span><span class="sxs-lookup"><span data-stu-id="920df-145">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-the-azure-portal"></a><span data-ttu-id="920df-146">在 Azure 入口網站中管理應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-146">Manage app passwords in the Azure portal</span></span>
<span data-ttu-id="920df-147">如果您搭配 Azure 使用雙步驟驗證，您會想要透過 Azure 入口網站建立應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-147">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span></span>

### <a name="to-create-app-passwords-in-the-azure-portal"></a><span data-ttu-id="920df-148">在 Azure 入口網站中建立應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-148">To create app passwords in the Azure portal</span></span>
1. <span data-ttu-id="920df-149">登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="920df-149">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="920df-150">在頂端，以滑鼠右鍵按一下您的使用者名稱並選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="920df-150">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="920df-151">在 proofup 頁面的頂端，選取應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-151">On the proofup page, at the top, select app passwords</span></span>
4. <span data-ttu-id="920df-152">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="920df-152">Click **Create**.</span></span>
5. <span data-ttu-id="920df-153">輸入應用程式密碼的名稱，然後按 [下一步] </span><span class="sxs-lookup"><span data-stu-id="920df-153">Enter a name for the app password and click **Next**</span></span>
6. <span data-ttu-id="920df-154">將應用程式密碼複製到剪貼簿，並將它貼到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="920df-154">Copy the app password to the clipboard and paste it into your app.</span></span>
   
   ![雲端](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="to-delete-app-passwords-in-the-azure-portal"></a><span data-ttu-id="920df-156">在 Azure 入口網站中刪除應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-156">To delete app passwords in the Azure portal</span></span>
1. <span data-ttu-id="920df-157">登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="920df-157">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="920df-158">在頂端，以滑鼠右鍵按一下您的使用者名稱並選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="920df-158">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="920df-159">在頂端的其他安全性驗證旁選取 [應用程式密碼]。</span><span class="sxs-lookup"><span data-stu-id="920df-159">At the top, next to additional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="920df-160">在您想要移除的應用程式密碼旁邊，選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="920df-160">Next to the app password you want to delete, select **Delete**.</span></span>
5. <span data-ttu-id="920df-161">按一下 [是] 確認刪除。</span><span class="sxs-lookup"><span data-stu-id="920df-161">Confirm the deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="920df-162">應用程式密碼刪除之後，就可以按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="920df-162">Once the app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-the-myapps-portal"></a><span data-ttu-id="920df-163">使用 MyApps 入口網站管理應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-163">Manage app passwords with the MyApps portal.</span></span>
<span data-ttu-id="920df-164">如果您不確定您使用 Multi-Factor Authentication 的方式，一律可以透過 myapps 入口網站建立和刪除應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-164">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="920df-165">使用 Myapps 入口網站建立應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-165">To create an app password using the Myapps portal</span></span>
1. <span data-ttu-id="920df-166">登入 [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="920df-166">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="920df-167">按一下右上方的您的名稱，然後選擇 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="920df-167">Click your name at the top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="920df-168">選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="920df-168">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="920df-169">![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="920df-169">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="920df-170">選取 [應用程式密碼]。</span><span class="sxs-lookup"><span data-stu-id="920df-170">Select **app passwords**.</span></span>
   <span data-ttu-id="920df-171">![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="920df-171">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="920df-172">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="920df-172">Click **Create**.</span></span>
6. <span data-ttu-id="920df-173">輸入應用程式密碼的名稱，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="920df-173">Enter a name for the app password and click **Next**.</span></span>
7. <span data-ttu-id="920df-174">將應用程式密碼複製到剪貼簿，並將它貼到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="920df-174">Copy the app password to the clipboard and paste it into your app.</span></span>
   <span data-ttu-id="920df-175">![建立應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="920df-175">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="920df-176">使用 Myapps 入口網站刪除應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="920df-176">To delete an app password using the Myapps portal</span></span>
1. <span data-ttu-id="920df-177">登入 [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="920df-177">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="920df-178">在頂端，選取 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="920df-178">At the top, select profile.</span></span>
3. <span data-ttu-id="920df-179">選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="920df-179">Select **Additional Security Verification**.</span></span>

   ![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="920df-181">選取 [應用程式密碼]。</span><span class="sxs-lookup"><span data-stu-id="920df-181">Select **app passwords**.</span></span>

   ![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="920df-183">在您想要刪除的應用程式密碼旁，按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="920df-183">Next to the app password you want to delete, click **Delete**.</span></span>

   ![刪除應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="920df-185">按一下 [是] 以確認您要刪除該密碼。</span><span class="sxs-lookup"><span data-stu-id="920df-185">Confirm that you want to delete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="920df-186">應用程式密碼刪除之後，就可以按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="920df-186">Once the app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="920df-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="920df-187">Next steps</span></span>

- [<span data-ttu-id="920df-188">管理雙步驟驗證設定</span><span class="sxs-lookup"><span data-stu-id="920df-188">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="920df-189">試用 [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)，透過應用程式通知來驗證您的登入，而不是透過文字訊息或電話。</span><span class="sxs-lookup"><span data-stu-id="920df-189">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
