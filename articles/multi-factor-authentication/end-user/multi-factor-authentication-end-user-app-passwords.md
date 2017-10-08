---
title: "aaaHow toouse 中 Azure MFA 的應用程式密碼？ | Microsoft Docs"
description: "此頁面可協助使用者了解何謂應用程式密碼以及什麼是用於具有考慮 tooAzure MFA。"
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
ms.openlocfilehash: bf2c11edc0ca81f2950eff0f7a3a24c8a5b34623
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="b6068-104">什麼是 Azure Multi-Factor Authentication 中的應用程式密碼？</span><span class="sxs-lookup"><span data-stu-id="b6068-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="b6068-105">某些非瀏覽器應用程式，例如 hello Apple 原生電子郵件用戶端會使用 Exchange Active Sync，目前不支援多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="b6068-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="b6068-106">Multi-Factor Authentication 會對每個使用者啟用。</span><span class="sxs-lookup"><span data-stu-id="b6068-106">Multi-factor authentication is enabled per user.</span></span> <span data-ttu-id="b6068-107">這表示，如果使用者已啟用多因素驗證，而且嘗試 toouse 非瀏覽器應用程式，它們將會無法 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="b6068-107">This means that if a user has been enabled for multi-factor authentication and they are attempting toouse non-browser apps, they will be unable toodo so.</span></span> <span data-ttu-id="b6068-108">應用程式密碼可讓此 toooccur。</span><span class="sxs-lookup"><span data-stu-id="b6068-108">An app password allows this toooccur.</span></span>

<span data-ttu-id="b6068-109">擁有應用程式密碼後，您可使用此密碼來取代這些非瀏覽器應用程式的原始密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-109">Once you have an app password, you use this in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="b6068-110">這是因為當您註冊進行兩步驟驗證，您告訴 Microsoft toolet 任何人登入您的密碼如果他們也不能執行 hello 第二個驗證。</span><span class="sxs-lookup"><span data-stu-id="b6068-110">This is because when you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="b6068-111">在手機上的 hello Apple 原生電子郵件用戶端無法與您帳戶登入因為它無法進行兩步驟驗證要求。</span><span class="sxs-lookup"><span data-stu-id="b6068-111">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="b6068-112">hello，是 toocreate 更安全的應用程式密碼，請勿使用日常，但僅針對那些無法支援雙步驟驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6068-112">hello solution for this is toocreate a more secure app password that you don't use day-to-day, but only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="b6068-113">使用 hello 應用程式密碼，以便可以略過 multi-factor authentication 應用程式，並繼續 toowork。</span><span class="sxs-lookup"><span data-stu-id="b6068-113">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>

> [!NOTE]
> <span data-ttu-id="b6068-114">Office 2013 用戶端 (包括 Outlook) 支援新式驗證通訊協定，而且可搭配雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="b6068-114">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span>  <span data-ttu-id="b6068-115">這表示一旦啟用後，應用程式密碼就不需要使用於 Office 2013 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b6068-115">This means that once enabled, app passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="b6068-116">如需詳細資訊，請參閱[發表的 Office 2013 新式驗證公開預覽](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。</span><span class="sxs-lookup"><span data-stu-id="b6068-116">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="b6068-117">如何 toouse 應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="b6068-117">How toouse app passwords</span></span>
<span data-ttu-id="b6068-118">hello 以下是如何一些事情 tooremember toouse 應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-118">hello following are some things tooremember on how toouse app passwords.</span></span>

* <span data-ttu-id="b6068-119">您不用自行建立應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-119">You don't create your own app passwords.</span></span> <span data-ttu-id="b6068-120">它們是自動產生的。</span><span class="sxs-lookup"><span data-stu-id="b6068-120">Instead, they are automatically generated.</span></span> <span data-ttu-id="b6068-121">您只需要每個應用程式一次 tooenter hello 應用程式密碼，因為它是更安全 toouse 自動產生的複雜密碼，而非讓您能記住的其中一個。</span><span class="sxs-lookup"><span data-stu-id="b6068-121">Since you only have tooenter hello app password once per app, it's safer toouse a more complex, automatically generated password rather than making one that you can remember.</span></span>
* <span data-ttu-id="b6068-122">每位使用者的密碼目前以 40 組為限。</span><span class="sxs-lookup"><span data-stu-id="b6068-122">Currently there is a limit of 40 passwords per user.</span></span> <span data-ttu-id="b6068-123">如果您已達到 hello 限制之後，您可以嘗試 toocreate 其中一個，您將現有的應用程式密碼的提示的 toodelete 之前建立一個新。</span><span class="sxs-lookup"><span data-stu-id="b6068-123">If you attempt toocreate one after you have reached hello limit, you will be prompted toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="b6068-124">您應該為每個裝置 (而非每個應用程式) 使用一個應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-124">You should use one app password per device, not per application.</span></span> <span data-ttu-id="b6068-125">例如，您可以為膝上型電腦建立一個應用程式密碼，並將該應用程式密碼使用於該膝上型電腦上的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6068-125">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="b6068-126">然後，您的桌面上建立第二個應用程式密碼 toouse 所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6068-126">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="b6068-127">您會獲得一個應用程式密碼 hello 第一次登錄時進行兩步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="b6068-127">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="b6068-128">如果您需要其他密碼，您可加以建立。</span><span class="sxs-lookup"><span data-stu-id="b6068-128">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="b6068-129">建立和刪除應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="b6068-129">Creating and deleting app passwords</span></span>
<span data-ttu-id="b6068-130">在初次登入期間，您會獲得可供使用的應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-130">During your initial sign-in you are given an app password that you can use.</span></span>  <span data-ttu-id="b6068-131">此外，您也可以稍後再建立和刪除應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-131">Additionally you can also create and delete app passwords later on.</span></span>  <span data-ttu-id="b6068-132">您執行此動作的方式取決於您使用 Multi-Factor Authentication 的方式。</span><span class="sxs-lookup"><span data-stu-id="b6068-132">How you do this depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="b6068-133">下列回應 hello 問題的 toodetermine 您應該在哪裡 toomanage 應用程式密碼：</span><span class="sxs-lookup"><span data-stu-id="b6068-133">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="b6068-134">您的個人 Microsoft 帳戶是否使用雙步驟驗證？</span><span class="sxs-lookup"><span data-stu-id="b6068-134">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="b6068-135">如果是，您應該參閱 toohello[應用程式密碼及雙步驟驗證](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification)文件以取得說明。</span><span class="sxs-lookup"><span data-stu-id="b6068-135">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="b6068-136">若為否，繼續 tooquestion 兩個。</span><span class="sxs-lookup"><span data-stu-id="b6068-136">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="b6068-137">好，所以您的工作或學校帳戶使用雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="b6068-137">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="b6068-138">您使用它 toosign tooOffice 365 應用程式中？</span><span class="sxs-lookup"><span data-stu-id="b6068-138">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="b6068-139">如果是，您應該參閱太[for Office 365 中建立應用程式密碼](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183)的說明。</span><span class="sxs-lookup"><span data-stu-id="b6068-139">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="b6068-140">若為否，繼續 tooquestion 三個。</span><span class="sxs-lookup"><span data-stu-id="b6068-140">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="b6068-141">您是否搭配 Microsoft Azure 使用雙步驟驗證？</span><span class="sxs-lookup"><span data-stu-id="b6068-141">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="b6068-142">如果是，繼續 toohello[管理 hello Azure 入口網站中的應用程式密碼](#manage-app-passwords-in-the-Azure-portal)本文一節。</span><span class="sxs-lookup"><span data-stu-id="b6068-142">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="b6068-143">若為否，繼續 tooquestion 四個。</span><span class="sxs-lookup"><span data-stu-id="b6068-143">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="b6068-144">不確定您在哪裡使用雙步驟驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="b6068-144">Not sure where you use two-step verification?</span></span> <span data-ttu-id="b6068-145">繼續 toohello[管理與 hello MyApps 入口網站應用程式密碼](#manage-app-passwords-with-the-myapps-portal)本文一節。</span><span class="sxs-lookup"><span data-stu-id="b6068-145">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="b6068-146">管理 hello Azure 入口網站中的應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="b6068-146">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="b6068-147">如果您搭配 Azure 使用雙步驟驗證，您會想 toocreate 應用程式密碼透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b6068-147">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="b6068-148">toocreate hello Azure 入口網站中的應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="b6068-148">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="b6068-149">登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="b6068-149">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="b6068-150">在 hello 頂端，以滑鼠右鍵按一下您的使用者名稱並選取 其他安全性驗證。</span><span class="sxs-lookup"><span data-stu-id="b6068-150">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="b6068-151">在 hello proofup 頁面上，在 hello 頂端，選取 應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="b6068-151">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="b6068-152">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b6068-152">Click **Create**.</span></span>
5. <span data-ttu-id="b6068-153">輸入 hello 應用程式密碼的名稱，然後按一下**下一步**</span><span class="sxs-lookup"><span data-stu-id="b6068-153">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="b6068-154">複製 hello 應用程式密碼 toohello 剪貼簿，並將它貼到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6068-154">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![雲端](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="b6068-156">toodelete hello Azure 入口網站中的應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="b6068-156">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="b6068-157">登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="b6068-157">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="b6068-158">在 hello 頂端，以滑鼠右鍵按一下您的使用者名稱並選取 其他安全性驗證。</span><span class="sxs-lookup"><span data-stu-id="b6068-158">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="b6068-159">在 hello 頂端下, 一步 tooadditional 安全性驗證，選取**應用程式密碼。**</span><span class="sxs-lookup"><span data-stu-id="b6068-159">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="b6068-160">您想要 toodelete，選取 下一步 toohello 應用程式密碼**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b6068-160">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="b6068-161">按一下確認 hello 刪除**是**。</span><span class="sxs-lookup"><span data-stu-id="b6068-161">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="b6068-162">一旦刪除 hello 應用程式密碼，您可以按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="b6068-162">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="b6068-163">管理與 hello MyApps 入口網站應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-163">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="b6068-164">如果您不確定您使用多重要素驗證的方式，然後您可以一律建立及刪除透過 hello myapps 入口網站應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="b6068-164">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="b6068-165">應用程式密碼使用 toocreate hello Myapps 入口網站</span><span class="sxs-lookup"><span data-stu-id="b6068-165">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="b6068-166">登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="b6068-166">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="b6068-167">按一下您在 hello 右上方，名稱，然後選擇**設定檔**。</span><span class="sxs-lookup"><span data-stu-id="b6068-167">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="b6068-168">選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="b6068-168">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="b6068-169">![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="b6068-169">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="b6068-170">選取 [應用程式密碼]。</span><span class="sxs-lookup"><span data-stu-id="b6068-170">Select **app passwords**.</span></span>
   <span data-ttu-id="b6068-171">![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="b6068-171">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="b6068-172">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b6068-172">Click **Create**.</span></span>
6. <span data-ttu-id="b6068-173">輸入 hello 應用程式密碼的名稱，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b6068-173">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="b6068-174">複製 hello 應用程式密碼 toohello 剪貼簿，並將它貼到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6068-174">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="b6068-175">![建立應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="b6068-175">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="b6068-176">應用程式密碼使用 toodelete hello Myapps 入口網站</span><span class="sxs-lookup"><span data-stu-id="b6068-176">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="b6068-177">登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="b6068-177">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="b6068-178">在 hello 頂端，選取 設定檔。</span><span class="sxs-lookup"><span data-stu-id="b6068-178">At hello top, select profile.</span></span>
3. <span data-ttu-id="b6068-179">選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="b6068-179">Select **Additional Security Verification**.</span></span>

   ![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="b6068-181">選取 [應用程式密碼]。</span><span class="sxs-lookup"><span data-stu-id="b6068-181">Select **app passwords**.</span></span>

   ![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="b6068-183">按一下 下一步的 toohello 應用程式密碼，您想要 toodelete，**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b6068-183">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![刪除應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="b6068-185">確認您想 toodelete 該密碼即可**是**。</span><span class="sxs-lookup"><span data-stu-id="b6068-185">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="b6068-186">一旦刪除 hello 應用程式密碼，您可以按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="b6068-186">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6068-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6068-187">Next steps</span></span>

- [<span data-ttu-id="b6068-188">管理雙步驟驗證設定</span><span class="sxs-lookup"><span data-stu-id="b6068-188">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="b6068-189">試試看 hello [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)tooverify 應用程式通知，而不是文字或呼叫收到與您登入。</span><span class="sxs-lookup"><span data-stu-id="b6068-189">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
