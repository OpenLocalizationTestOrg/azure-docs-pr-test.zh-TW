---
title: "aaaGet 開始使用 Azure 通知中心使用百度 |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toopush 通知 tooAndroid 裝置使用百度。"
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="8d6d0-103">透過百度開始使用通知中樞</span><span class="sxs-lookup"><span data-stu-id="8d6d0-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="8d6d0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8d6d0-104">Overview</span></span>
<span data-ttu-id="8d6d0-105">百度雲端推播是中文的雲端服務，您可以使用 toosend 推播通知 toomobile 裝置。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="8d6d0-106">這個服務是用於中國，其中傳遞 tooAndroid 很複雜，因為 hello 出現不同的應用程式存放區與推入的推播通知服務，除了 toohello 可用性的不是通常連接的 tooGCM (Google Android 裝置雲端傳訊）。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d6d0-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="8d6d0-107">Prerequisites</span></span>
<span data-ttu-id="8d6d0-108">本教學課程需要：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-108">This tutorial requires:</span></span>

* <span data-ttu-id="8d6d0-109">Android SDK （我們假設您使用 Eclipse），您可以下載從 hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android 的站台</a></span><span class="sxs-lookup"><span data-stu-id="8d6d0-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="8d6d0-110">[行動服務 Android SDK]</span><span class="sxs-lookup"><span data-stu-id="8d6d0-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="8d6d0-111">[百度發送的 Android SDK]</span><span class="sxs-lookup"><span data-stu-id="8d6d0-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="8d6d0-112">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8d6d0-113">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8d6d0-114">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="8d6d0-115">建立百度帳戶</span><span class="sxs-lookup"><span data-stu-id="8d6d0-115">Create a Baidu account</span></span>
<span data-ttu-id="8d6d0-116">toouse 百度，您必須在百度帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="8d6d0-117">如果您已經有一個，登入 toohello[百度入口網站]並略過 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="8d6d0-118">否則，請參閱如何在下列指示的 hello toocreate 百度帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="8d6d0-119">移 toohello[百度入口網站]按一下 hello**登录**(**登入**) 連結。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="8d6d0-120">按一下**立即注册**toostart hello 帳戶註冊程序。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="8d6d0-121">輸入所需的 hello 詳細資料 — 電話/電子郵件地址、 密碼和驗證程式碼，按一下 **註冊**。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="8d6d0-122">您將會收到電子郵件 toohello 電子郵件地址，您輸入連結 tooactivate 百度帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="8d6d0-123">登入 tooyour 電子郵件帳戶，開啟 hello 百度啟用郵件，然後按一下 hello 啟用連結 tooactivate 百度帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="8d6d0-124">一旦您擁有已啟用的百度帳戶，登入 toohello[百度入口網站]。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="8d6d0-125">註冊為百度開發人員</span><span class="sxs-lookup"><span data-stu-id="8d6d0-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="8d6d0-126">一旦您登入 toohello[百度入口網站]，按一下 **更多 >>** (**詳細**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="8d6d0-127">Hello 中向下捲動**站长与开发者服务 （網站管理員和開發人員服務）**區段，然後按一下**百度开放云平台**(**百度開放雲平台**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="8d6d0-128">在 hello 下一個頁面上，按一下 **开发者服务**(**開發人員服務**) hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="8d6d0-129">在 hello 下一個頁面上，按一下 **注册开发者**(**註冊開發人員**) 從 hello hello 右上角的功能表。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="8d6d0-130">輸入您的名稱、描述和可收到驗證簡訊的行動電話號碼，然後按一下送验证码 \(**傳送驗證碼**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="8d6d0-131">國際電話號碼，您需要括號括住 tooenclose hello 國家/地區碼。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="8d6d0-132">例如，如果是美國的電話號碼，則為 **(1)1234567890**。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="8d6d0-133">您接著應該會收到一則簡訊驗證數 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="8d6d0-134">輸入 hello 驗證數字中的 hello 訊息**验证码**(**確認碼**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="8d6d0-135">最後，完成 接受 hello 百度協議，然後按一下 hello 開發人員註冊**提交**(**送出**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="8d6d0-136">您會看到下列頁面上成功完成註冊的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d6d0-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="8d6d0-137">建立百度雲端推播專案</span><span class="sxs-lookup"><span data-stu-id="8d6d0-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="8d6d0-138">建立百度雲端推播專案時，您會收到應用程式識別碼、API 金鑰和秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="8d6d0-139">一旦您登入 toohello[百度入口網站]，按一下 **更多 >>** (**詳細**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="8d6d0-140">Hello 中向下捲動**站长与开发者服务**(**網站管理員和開發人員服務**) 區段，然後按一下**百度开放云平台**(**百度開放雲平台**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="8d6d0-141">在 hello 下一個頁面上，按一下 **开发者服务**(**開發人員服務**) hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="8d6d0-142">在 hello 下一個頁面上，按一下 **云推送**(**雲端推播**) 從 hello**云服务**(**雲端服務**) 一節。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="8d6d0-143">一旦您已註冊的開發人員，您會看到**管理控制台**(**管理主控台**) 在 hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="8d6d0-144">按一下 [开发者服务管理] \(**開發人員服務管理**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="8d6d0-145">在 hello 下一個頁面上，按一下 **创建工程**(**建立專案**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="8d6d0-146">輸入應用程式名稱，然後按一下 [创建] \(**建立**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="8d6d0-147">成功建立百度雲推送專案後，您會看到包含 **AppID**、**API 金鑰**與**祕密金鑰**的頁面。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="8d6d0-148">記下的 hello API 金鑰與秘密金鑰，我們將在稍後使用。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="8d6d0-149">按一下 設定推播通知的 hello 專案**云推送**(**雲端推播**) 在 hello 的左窗格。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="8d6d0-150">在 hello 下一個頁面上，按一下 hello**推送设置**(**設定推送**) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="8d6d0-151">在 hello 組態頁面上，加入您將使用在 hello Android 專案中的 hello 封裝名稱**应用包名**(**應用程式封裝**) 欄位，，然後按一下**保存设置**(**儲存**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="8d6d0-152">您會看到 hello**保存成功 ！** (**儲存成功！**\) 的訊息。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="8d6d0-153">設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="8d6d0-153">Configure your notification hub</span></span>
1. <span data-ttu-id="8d6d0-154">登入 toohello [Azure 傳統入口網站]，然後按一下 **+ 新增**在 hello 囉 」 畫面底部。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="8d6d0-155">依序按一下 應用程式服務、服務匯流排、通知中樞，然後按一下快速建立。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="8d6d0-156">提供名稱給您**通知中樞**，選取 hello**區域**和 hello**命名空間**此通知中樞將會建立，然後按一下 **建立新的通知中樞**。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="8d6d0-157">按一下您要在其中建立您的通知中樞的 hello 命名空間，然後按一下**通知中樞**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="8d6d0-158">選取 hello 通知中樞，您建立，然後按一下**設定**從 hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="8d6d0-159">捲動 toohello**百度通知設定**區段，然後輸入 hello API 金鑰及祕密金鑰，您先前取得的 hello 百度主控台百度雲端推入專案。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="8d6d0-160">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="8d6d0-161">按一下 hello**儀表板**hello 通知中樞，hello 頂端索引標籤，然後按一下**檢視連接字串**。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="8d6d0-162">請記下 hello **DefaultListenSharedAccessSignature**和**DefaultFullSharedAccessSignature**從 hello**存取連線資訊**視窗。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="8d6d0-163">連接您的應用程式 toohello 通知中樞</span><span class="sxs-lookup"><span data-stu-id="8d6d0-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="8d6d0-164">在 Eclipse ADT 中建立新的 Android 專案 ([檔案] > [新增] > [Android 應用程式專案])。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="8d6d0-165">輸入**應用程式名稱**，並確保該 hello**最低所需的 SDK**版本設定得**API 16: Android 4.1**。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="8d6d0-166">按一下**下一步**並繼續遵循 hello 精靈直到 hello**建立活動** 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="8d6d0-167">請確定**空白活動**已選取，最後選取**完成**toocreate 新的 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="8d6d0-168">請確定該 hello**專案建置目標**已正確設定。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="8d6d0-169">從 hello 下載 hello 通知-中樞-0.4.jar 檔案**檔案** 索引標籤的 hello[通知-中樞-Android-SDK 上 Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="8d6d0-170">新增 hello 檔案 toohello**程式庫**資料夾您 Eclipse 專案，並重新整理 hello*程式庫*資料夾。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="8d6d0-171">下載並解壓縮 hello[百度發送的 Android SDK]，開啟 hello**程式庫**資料夾，然後再複製 hello **pushservice x.y.z** jar 檔案和 hello **armeabi** &  **mips**資料夾中 hello**程式庫**Android 應用程式資料夾。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="8d6d0-172">開啟 hello **AndroidManifest.xml**檔案的 Android 專案，並加入 hello hello 百度 SDK 所需的權限。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="8d6d0-173">新增 hello **android: name**屬性 tooyour**應用程式**中的項目**AndroidManifest.xml**，並將*yourprojectname* （適用於範例中， **com.example.BaiduTest**)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="8d6d0-174">請確定此專案名稱符合 hello 一個 hello 百度主控台中設定。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="8d6d0-175">新增下列 hello 應用程式項目內的組態之後 hello hello **。MainActivity**活動項目，取代*yourprojectname* (例如， **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="8d6d0-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="8d6d0-176">加入新的類別稱為**ConfigurationSettings.java** toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="8d6d0-177">加入下列程式碼 tooit hello:</span><span class="sxs-lookup"><span data-stu-id="8d6d0-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="8d6d0-178">設定 hello 值**API_KEY**什麼您擷取 hello 百度雲端專案從較舊版本，與**NotificationHubName**以您的通知中樞名稱，從 Azure 傳統入口網站的 hello 和**NotificationHubConnectionString** DefaultListenSharedAccessSignature hello Azure 傳統入口網站中使用。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="8d6d0-179">加入新的類別稱為**DemoApplication.java**，並加入下列程式碼 tooit hello:</span><span class="sxs-lookup"><span data-stu-id="8d6d0-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="8d6d0-180">加入另一個新的類別稱為 「 **MyPushMessageReceiver.java**，並加入下列程式碼 tooit hello。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="8d6d0-181">它是控制代碼 hello hello 百度推入 server 從接收推播通知的 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="8d6d0-182">開啟**MainActivity.java**，並加入下列 toohello hello **onCreate**方法：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="8d6d0-183">開啟 hello 下列匯入在 hello 最上方的陳述式：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="8d6d0-184">傳送通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="8d6d0-184">Send notifications tooyour app</span></span>
<span data-ttu-id="8d6d0-185">您可以快速測試您的應用程式中接收通知，傳送通知給 hello 以[Azure 入口網站](https://portal.azure.com/)使用 hello**傳送**按鈕在 hello 通知中樞內，hello 遵循畫面所示：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="8d6d0-186">推播通知通常會以後端服務傳送，例如行動服務或使用相容程式庫的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="8d6d0-187">如果文件庫不適用於您的後端中，您可以使用 hello REST API 直接 toosend 通知訊息。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="8d6d0-188">在本教學課程中，我們會保持簡單，只示範測試用戶端應用程式透過傳送 hello.NET SDK 使用通知中心，而不是後端服務的主控台應用程式的通知。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="8d6d0-189">我們建議 hello[使用通知中樞 toopush 通知 toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)教學課程為 hello 下一個步驟，從 ASP.NET 後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="8d6d0-190">不過，hello 下列方法可用來傳送通知：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="8d6d0-191">**REST 介面**： 您可以使用 hello 任何後端平台上支援通知[REST 介面](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="8d6d0-192">**Microsoft Azure 通知中樞.NET SDK**: hello for Visual Studio 的 Nuget 封裝管理員，在執行[Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="8d6d0-193">**Node.js**:[如何 toouse 通知中樞，從 Node.js](notification-hubs-nodejs-push-notification-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="8d6d0-194">**行動應用程式**： 如需如何 toosend 通知從 Azure App Service 行動應用程式後端整合通知中心，請參閱[新增推播通知 tooyour 行動裝置應用程式](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="8d6d0-195">**Java / PHP**： 如需如何使用 toosend 通知 hello REST Api 的範例，請參閱 「 如何 toouse 來自 Java/PHP 的通知中心 」 ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="8d6d0-196">(選擇性) 從 .NET 主控台應用程式傳送通知。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="8d6d0-197">在本節中，我們會說明如何使用.NET 主控台應用程式傳送通知。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="8d6d0-198">建立新的 Visual C# 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="8d6d0-199">在 [hello 封裝管理員主控台] 視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d6d0-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="8d6d0-200">這個指令會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="8d6d0-201">開啟 hello 檔案**Program.cs**並加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="8d6d0-202">在您`Program`類別，加入下列方法 hello 並取代*DefaultFullSharedAccessSignatureSASConnectionString*和*NotificationHubName*您擁有 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="8d6d0-203">新增下列幾行中的 hello 您**Main**方法：</span><span class="sxs-lookup"><span data-stu-id="8d6d0-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="8d6d0-204">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="8d6d0-204">Test your app</span></span>
<span data-ttu-id="8d6d0-205">實際電話，只與此應用程式連接的 tootest hello 電話 tooyour 電腦使用 USB 纜線。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="8d6d0-206">這個動作會載入到附加的 hello 電話應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="8d6d0-207">此應用程式與 hello 模擬器，hello Eclipse 頂端工具列上，按一下 tootest**執行**，然後選取您的應用程式： hello 模擬器中，負載、 啟動和執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="8d6d0-208">hello 應用程式會從 hello 百度推播通知服務擷取 hello 'userId' 和 'channelId'，並註冊與 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="8d6d0-209">toosend 測試通知，您可以使用 hello hello Azure 傳統入口網站的 [偵錯] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="8d6d0-210">如果您建立 hello for Visual Studio.NET 主控台應用程式，請按 hello F5 鍵在 Visual Studio toorun hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="8d6d0-211">hello 應用程式傳送通知出現在您的裝置或模擬器 hello 上方的通知區域中。</span><span class="sxs-lookup"><span data-stu-id="8d6d0-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[行動服務 Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[百度發送的 Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Azure 傳統入口網站]: https://manage.windowsazure.com/
[百度入口網站]: http://www.baidu.com/
