---
title: "aaaAuthenticate 與 Mobile Engagement REST Api 手動安裝"
description: "描述如何 toomanually 安裝 Mobile Engagement REST Api 的驗證"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="44bec-103">使用 Mobile Engagement REST API 進行驗證 - 手動設定</span><span class="sxs-lookup"><span data-stu-id="44bec-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="44bec-104">這是附錄文件太[與 Mobile Engagement REST Api 的驗證](mobile-engagement-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="44bec-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="44bec-105">請確定讀取第一個 tooget hello 內容。</span><span class="sxs-lookup"><span data-stu-id="44bec-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="44bec-106">此描述您的驗證設定的替代方式 toodo hello 一次性安裝 hello Mobile Engagement REST Api 使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="44bec-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="44bec-107">下列的 hello 指示根據這個[Active Directory 指南](../azure-resource-manager/resource-group-create-service-principal-portal.md)和自訂的所需的 Mobile Engagement 應用程式開發介面的驗證內容。</span><span class="sxs-lookup"><span data-stu-id="44bec-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="44bec-108">因此如果您想 toounderstand hello 執行下列步驟在詳細資料，請參閱 tooit。</span><span class="sxs-lookup"><span data-stu-id="44bec-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="44bec-109">登入 tooyour Azure 帳戶透過 hello[傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="44bec-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="44bec-110">選取**Active Directory** hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="44bec-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![選取 Active Directory][1]
3. <span data-ttu-id="44bec-112">選擇 hello**預設的 Active Directory**在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="44bec-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![選擇目錄][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="44bec-114">這個方法僅適用於您要使用 hello 預設 Active Directory，您的帳戶，而且將無法運作，如果您已建立您的帳戶在 Active Directory 中進行。</span><span class="sxs-lookup"><span data-stu-id="44bec-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="44bec-115">tooview hello 應用程式在目錄中，按一下 **應用程式**。</span><span class="sxs-lookup"><span data-stu-id="44bec-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![檢視應用程式][3]
5. <span data-ttu-id="44bec-117">按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="44bec-117">Click on **ADD**.</span></span> 
   
     ![新增應用程式][4]
6. <span data-ttu-id="44bec-119">按一下 [加入] </span><span class="sxs-lookup"><span data-stu-id="44bec-119">Click on **Add an application my organization is developing**</span></span>
   
     ![新的應用程式][5]
7. <span data-ttu-id="44bec-121">填入 hello 應用程式和應用程式做為選取的 hello 類型名稱**WEB 應用程式和/或 WEB API**按一下 hello 下一步 按鈕。</span><span class="sxs-lookup"><span data-stu-id="44bec-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![名稱應用程式][6]
8. <span data-ttu-id="44bec-123">您可以針對 [登入 URL] 和 [應用程式識別碼 URI] 提供任何 dummy URL。</span><span class="sxs-lookup"><span data-stu-id="44bec-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="44bec-124">不會使用我們的案例並不會驗證其本身的 hello Url。</span><span class="sxs-lookup"><span data-stu-id="44bec-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![應用程式屬性][7]
9. <span data-ttu-id="44bec-126">在這個 hello 結束時，您會有 AAD 應用程式，但您先前提供類似 hello 下列 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="44bec-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="44bec-127">這是您的 **AD\_APP\_NAME**，請記下它。</span><span class="sxs-lookup"><span data-stu-id="44bec-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![應用程式名稱][8]
10. <span data-ttu-id="44bec-129">按一下 hello 應用程式名稱，然後按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="44bec-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![設定應用程式][9]
11. <span data-ttu-id="44bec-131">請記下將使用做為用戶端識別碼 hello**用戶端\_識別碼**對於您的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="44bec-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![設定應用程式][10]
12. <span data-ttu-id="44bec-133">捲動 toohello**金鑰**區段並加入最好 2 年 （過期） 持續時間的索引鍵，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="44bec-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![設定應用程式][11]
13. <span data-ttu-id="44bec-135">立即複製 hello 值顯示為 hello 金鑰現在只顯示並不會儲存，因此不會再顯示。</span><span class="sxs-lookup"><span data-stu-id="44bec-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="44bec-136">如果遺失則您將有 toogenerate 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="44bec-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="44bec-137">這會是 hello **CLIENT_SECRET**對於您的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="44bec-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![設定應用程式][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="44bec-139">此金鑰會過期結尾 hello hello 持續時間，您所指定，請確定 toorenew hello 時間否則一 API 驗證不會再。</span><span class="sxs-lookup"><span data-stu-id="44bec-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="44bec-140">如果您認為此金鑰遭到盜用，您也可以將它刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="44bec-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="44bec-141">按一下**檢視端點**按鈕現在這會開啟 hello**應用程式端點** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="44bec-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="44bec-142">從 hello 應用程式端點對話方塊中，複製 hello **OAUTH 2.0 權杖端點**。</span><span class="sxs-lookup"><span data-stu-id="44bec-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="44bec-143">此端點將處於下列其中 hello hello URL 中的 GUID 是表單的 hello 您**TENANT_ID**所以請記下它：</span><span class="sxs-lookup"><span data-stu-id="44bec-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="44bec-144">現在我們將繼續在此應用程式上的 tooconfigure hello 權限。</span><span class="sxs-lookup"><span data-stu-id="44bec-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="44bec-145">這就 tooopen 向上 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="44bec-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="44bec-146">按一下**資源群組**並尋找 hello **Mobile Engagement**資源群組。</span><span class="sxs-lookup"><span data-stu-id="44bec-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="44bec-147">按一下 hello **Mobile Engagement**資源群組，並瀏覽 toohello**設定**這裡刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="44bec-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="44bec-148">按一下**使用者**在 hello 設定 刀鋒視窗，然後按一下**新增**tooadd 使用者。</span><span class="sxs-lookup"><span data-stu-id="44bec-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="44bec-149">按一下 [選取角色] </span><span class="sxs-lookup"><span data-stu-id="44bec-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="44bec-150">按一下 [擁有者] </span><span class="sxs-lookup"><span data-stu-id="44bec-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="44bec-151">應用程式的 hello 名稱搜尋**AD\_應用程式\_名稱**hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="44bec-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="44bec-152">依預設，您不會在這裡看到它。</span><span class="sxs-lookup"><span data-stu-id="44bec-152">You will not see this by default here.</span></span> <span data-ttu-id="44bec-153">一旦您找到它，請選取它，然後按一下 **選取**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="44bec-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="44bec-154">在 hello**加入存取**刀鋒視窗中，它會顯示為**1 個使用者、 群組 0**。</span><span class="sxs-lookup"><span data-stu-id="44bec-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="44bec-155">按一下**確定**此刀鋒視窗 tooconfirm hello 變更。</span><span class="sxs-lookup"><span data-stu-id="44bec-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="44bec-156">您現在已完成所需的 hello AAD 設定，而且所有設定 toocall hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="44bec-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



