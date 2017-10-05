---
title: "使用 Mobile Engagement REST API 進行驗證 - 手動設定"
description: "描述如何手動設定 Mobile Engagement REST API 的驗證"
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
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="c55f9-103">使用 Mobile Engagement REST API 進行驗證 - 手動設定</span><span class="sxs-lookup"><span data-stu-id="c55f9-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="c55f9-104">這是 [使用 Mobile Engagement REST API 進行驗證](mobile-engagement-api-authentication.md)的附錄說明文件。</span><span class="sxs-lookup"><span data-stu-id="c55f9-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="c55f9-105">請務必先閱讀它，以取得內容。</span><span class="sxs-lookup"><span data-stu-id="c55f9-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="c55f9-106">這會說明如何使用 Azure 入口網站設定 Mobile Engagement REST API 驗證的一次性設定的替代方式。</span><span class="sxs-lookup"><span data-stu-id="c55f9-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="c55f9-107">下列指示是根據這份 [Active Directory 指南](../azure-resource-manager/resource-group-create-service-principal-portal.md) ，並且針對 Mobile Engagement API 驗證所需進行自訂。</span><span class="sxs-lookup"><span data-stu-id="c55f9-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="c55f9-108">如果您想要了解以下的詳細步驟，請參閱它。</span><span class="sxs-lookup"><span data-stu-id="c55f9-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="c55f9-109">透過 [傳統入口網站](https://manage.windowsazure.com/)登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c55f9-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="c55f9-110">從左窗格中，選取 [ **Active Directory** ]。</span><span class="sxs-lookup"><span data-stu-id="c55f9-110">Select **Active Directory** from the left pane.</span></span>
   
     ![選取 Active Directory][1]
3. <span data-ttu-id="c55f9-112">在 Azure 入口網站中選擇 [預設 Active Directory]  。</span><span class="sxs-lookup"><span data-stu-id="c55f9-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![選擇目錄][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="c55f9-114">這個方法只適用於您在帳戶的預設 Active Directory 中工作時，如果您在帳戶中建立的 Active Directory 中進行則無效。</span><span class="sxs-lookup"><span data-stu-id="c55f9-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="c55f9-115">若要檢視目錄中的應用程式，請按一下 [ **應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="c55f9-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![檢視應用程式][3]
5. <span data-ttu-id="c55f9-117">按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="c55f9-117">Click on **ADD**.</span></span> 
   
     ![新增應用程式][4]
6. <span data-ttu-id="c55f9-119">按一下 [加入] </span><span class="sxs-lookup"><span data-stu-id="c55f9-119">Click on **Add an application my organization is developing**</span></span>
   
     ![新的應用程式][5]
7. <span data-ttu-id="c55f9-121">填入應用程式的名稱，然後選取 [WEB 應用程式和/或 WEB API]  作為應用程式的類型，再按一下 [下一步] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c55f9-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![名稱應用程式][6]
8. <span data-ttu-id="c55f9-123">您可以針對 [登入 URL] 和 [應用程式識別碼 URI] 提供任何 dummy URL。</span><span class="sxs-lookup"><span data-stu-id="c55f9-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="c55f9-124">我們的案例不會使用它們，且不會驗證 URL 本身。</span><span class="sxs-lookup"><span data-stu-id="c55f9-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![應用程式屬性][7]
9. <span data-ttu-id="c55f9-126">在這結束時，您將會有 AAD 應用程式，且具有您先前提供如下的名稱。</span><span class="sxs-lookup"><span data-stu-id="c55f9-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="c55f9-127">這是您的 **AD\_APP\_NAME**，請記下它。</span><span class="sxs-lookup"><span data-stu-id="c55f9-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![應用程式名稱][8]
10. <span data-ttu-id="c55f9-129">按一下應用程式名稱，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="c55f9-129">Click on the app name and click on **Configure**.</span></span>
    
      ![設定應用程式][9]
11. <span data-ttu-id="c55f9-131">記下將作為 API 呼叫之 **CLIENT\_ID** 的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="c55f9-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![設定應用程式][10]
12. <span data-ttu-id="c55f9-133">向下捲動至 [金鑰] 區段，並加入持續時間最好為 2 年 (到期) 的金鑰，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c55f9-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![設定應用程式][11]
13. <span data-ttu-id="c55f9-135">立即複製為金鑰顯示的值，因為它只會現在顯示，且不會儲存，因此不會再顯示。</span><span class="sxs-lookup"><span data-stu-id="c55f9-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="c55f9-136">如果您遺失它，則必須產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c55f9-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="c55f9-137">這會是您 API 呼叫的 **CLIENT_SECRET**。</span><span class="sxs-lookup"><span data-stu-id="c55f9-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![設定應用程式][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="c55f9-139">此金鑰將在您指定的持續時間結束時到期，因此到時候請務必更新，否則您的 API 驗證將無法再使用。</span><span class="sxs-lookup"><span data-stu-id="c55f9-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="c55f9-140">如果您認為此金鑰遭到盜用，您也可以將它刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="c55f9-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="c55f9-141">按一下 [檢視端點] 按鈕，現在它將會開啟 [應用程式端點] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c55f9-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="c55f9-142">從 [應用程式端點] 對話方塊中，複製 [OAUTH 2.0 權杖端點] 。</span><span class="sxs-lookup"><span data-stu-id="c55f9-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="c55f9-143">此端點將為下列形式，其中 URL 中的 GUID 是您的 **TENANT_ID**，因此請記下它︰</span><span class="sxs-lookup"><span data-stu-id="c55f9-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="c55f9-144">現在我們將繼續設定此應用程式上的權限。</span><span class="sxs-lookup"><span data-stu-id="c55f9-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="c55f9-145">這將需要開啟 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c55f9-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="c55f9-146">按一下 [資源群組] 並尋找 [Mobile Engagement] 資源群組。</span><span class="sxs-lookup"><span data-stu-id="c55f9-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="c55f9-147">按一下 [Mobile Engagement] 資源群組，並瀏覽至此處的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c55f9-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="c55f9-148">在 [設定] 刀鋒視窗中按一下 [使用者]，然後按一下 [新增] 來新增使用者。</span><span class="sxs-lookup"><span data-stu-id="c55f9-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="c55f9-149">按一下 [選取角色] </span><span class="sxs-lookup"><span data-stu-id="c55f9-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="c55f9-150">按一下 [擁有者] </span><span class="sxs-lookup"><span data-stu-id="c55f9-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="c55f9-151">在 [搜尋] 方塊中搜尋應用程式的名稱 **AD\_APP\_NAME**。</span><span class="sxs-lookup"><span data-stu-id="c55f9-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="c55f9-152">依預設，您不會在這裡看到它。</span><span class="sxs-lookup"><span data-stu-id="c55f9-152">You will not see this by default here.</span></span> <span data-ttu-id="c55f9-153">找到之後請選取它，然後按一下刀鋒視窗底部的 [選取]  。</span><span class="sxs-lookup"><span data-stu-id="c55f9-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="c55f9-154">在 [新增存取] 刀鋒視窗中，它會顯示為 [1 個使用者、0 個群組]。</span><span class="sxs-lookup"><span data-stu-id="c55f9-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="c55f9-155">按一下此刀鋒視窗中的 [確定]  ，確認變更。</span><span class="sxs-lookup"><span data-stu-id="c55f9-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="c55f9-156">您現在已完成所需的 AAD 組態，可以呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="c55f9-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

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



