---
title: "使用 Azure AD 應用程式 Proxy 為發佈的應用程式設定自訂首頁 | Microsoft Docs"
description: "涵蓋 Azure AD 應用程式 Proxy 連接器的基本概念"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="921f1-103">使用 Azure AD 應用程式 Proxy 為發佈的應用程式設定自訂首頁</span><span class="sxs-lookup"><span data-stu-id="921f1-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="921f1-104">本文討論如何設定應用程式來將使用者導向自訂首頁。</span><span class="sxs-lookup"><span data-stu-id="921f1-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="921f1-105">當您使用應用程式 Proxy 發佈應用程式時，您會設定內部 URL，但有時這不是您的使用者應該先看到的頁面。</span><span class="sxs-lookup"><span data-stu-id="921f1-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="921f1-106">設定自訂首頁，以便使用者從 Azure Active Directory 存取面板或 Office 365 應用程式啟動器存取應用程式時，會前往正確的頁面。</span><span class="sxs-lookup"><span data-stu-id="921f1-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="921f1-107">當使用者啟動應用程式時，預設會將他們導向已發佈應用程式的根網域 URL。</span><span class="sxs-lookup"><span data-stu-id="921f1-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="921f1-108">登陸頁面通常設定為首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="921f1-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="921f1-109">如果您想要讓應用程式使用者登陸應用程式內的特定頁面，請使用 Azure AD PowerShell 模組定義自訂首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="921f1-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="921f1-110">例如：</span><span class="sxs-lookup"><span data-stu-id="921f1-110">For example:</span></span>
- <span data-ttu-id="921f1-111">在您的公司網路內部，使用者前往 *https://ExpenseApp/login/login.aspx* 登入並存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="921f1-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="921f1-112">由於您有應用程式 Proxy 需要在資料夾結構最上層存取的其他資產 (例如影像)，因此您以 *https://ExpenseApp* 作為內部 URL 來發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="921f1-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="921f1-113">預設外部 URL 是 *https://ExpenseApp-contoso.msappproxy.net*，不會引導使用者登入頁面。</span><span class="sxs-lookup"><span data-stu-id="921f1-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="921f1-114">將 *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* 設定為首頁 URL，為使用者提供順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="921f1-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="921f1-115">當您將已發佈應用程式的存取權提供給使用者時，應用程式會顯示在 [Azure AD 存取面板](active-directory-saas-access-panel-introduction.md)和 [Office 365 應用程式啟動器](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher)。</span><span class="sxs-lookup"><span data-stu-id="921f1-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="921f1-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="921f1-116">Before you start</span></span>

<span data-ttu-id="921f1-117">設定首頁 URL 之前，請記住下列需求︰</span><span class="sxs-lookup"><span data-stu-id="921f1-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="921f1-118">確保您指定的路徑是根網域 URL 的子網域路徑。</span><span class="sxs-lookup"><span data-stu-id="921f1-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="921f1-119">如果根網域 URL 是 https://apps.contoso.com/app1/，您設定的首頁 URL 開頭必須 https://apps.contoso.com/app1/。</span><span class="sxs-lookup"><span data-stu-id="921f1-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="921f1-120">若變更已發佈的應用程式，則變更可能會重設首頁 URL 的值。</span><span class="sxs-lookup"><span data-stu-id="921f1-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="921f1-121">當您未來更新應用程式時，您應該重新檢查並視需要更新首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="921f1-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="921f1-122">在 Azure 入口網站中變更首頁</span><span class="sxs-lookup"><span data-stu-id="921f1-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="921f1-123">以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="921f1-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="921f1-124">瀏覽至 [Azure Active Directory] > [應用程式註冊]，然後從清單中選擇您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="921f1-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="921f1-125">從設定中選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="921f1-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="921f1-126">使用新路徑更新 [首頁 URL] 欄位。</span><span class="sxs-lookup"><span data-stu-id="921f1-126">Update the **Home page URL** field with your new path.</span></span> 

   ![提供新的首頁 URL](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="921f1-128">選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="921f1-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="921f1-129">使用 PowerShell 變更首頁</span><span class="sxs-lookup"><span data-stu-id="921f1-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="921f1-130">安裝 Azure AD PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="921f1-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="921f1-131">使用 PowerShell 定義自訂首頁 URL 之前，請先安裝 Azure AD PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="921f1-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="921f1-132">您可以從 [PowerShell 資源庫](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131)下載此套件，其使用圖形 API 端點。</span><span class="sxs-lookup"><span data-stu-id="921f1-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="921f1-133">若要安裝套件，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="921f1-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="921f1-134">開啟標準 PowerShell 視窗，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="921f1-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="921f1-135">若您以非系統管理員身分執行此命令，請使用 `-scope currentuser` 選項。</span><span class="sxs-lookup"><span data-stu-id="921f1-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="921f1-136">在安裝期間，選取 [Y] 以從 Nuget.org 安裝兩個套件。兩個套件都是必要套件。</span><span class="sxs-lookup"><span data-stu-id="921f1-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="921f1-137">尋找應用程式的 ObjectID</span><span class="sxs-lookup"><span data-stu-id="921f1-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="921f1-138">取得應用程式中的 ObjectID，然後依其首頁搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="921f1-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="921f1-139">開啟 PowerShell 並匯入 Azure AD 模組。</span><span class="sxs-lookup"><span data-stu-id="921f1-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="921f1-140">以租用戶系統管理員身分登入 Azure AD 模組。</span><span class="sxs-lookup"><span data-stu-id="921f1-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="921f1-141">根據應用程式的首頁 URL 尋找它。</span><span class="sxs-lookup"><span data-stu-id="921f1-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="921f1-142">您可以在入口網站中找到 URL，請前往 [Azure Active Directory] > [企業應用程式] > [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="921f1-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="921f1-143">這個範例會使用 sharepoint-iddemo。</span><span class="sxs-lookup"><span data-stu-id="921f1-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="921f1-144">您應會取得如下所示的結果。</span><span class="sxs-lookup"><span data-stu-id="921f1-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="921f1-145">將 ObjectID GUID 複製以在下一節中使用。</span><span class="sxs-lookup"><span data-stu-id="921f1-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="921f1-146">更新首頁 URL</span><span class="sxs-lookup"><span data-stu-id="921f1-146">Update the home page URL</span></span>

<span data-ttu-id="921f1-147">在您於步驟 1 所使用的相同 PowerShell 模組中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="921f1-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="921f1-148">確認您有正確的應用程式，並將 *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* 取代為您在前一個步驟中複製的 ObjectID。</span><span class="sxs-lookup"><span data-stu-id="921f1-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="921f1-149">您現在已確認應用程式，可以開始依照下列指示更新首頁。</span><span class="sxs-lookup"><span data-stu-id="921f1-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="921f1-150">建立空白應用程式物件以存放您要進行的變更。</span><span class="sxs-lookup"><span data-stu-id="921f1-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="921f1-151">這個變數會包含您要更新的值。</span><span class="sxs-lookup"><span data-stu-id="921f1-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="921f1-152">此步驟不會建立任何項目。</span><span class="sxs-lookup"><span data-stu-id="921f1-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="921f1-153">將首頁 URL 設定為您想要的值。</span><span class="sxs-lookup"><span data-stu-id="921f1-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="921f1-154">此值必須是已發佈應用程式的子網域路徑。</span><span class="sxs-lookup"><span data-stu-id="921f1-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="921f1-155">例如，若將首頁 URL 從 *https://sharepoint-iddemo.msappproxy.net/* 變更為 *https://sharepoint-iddemo.msappproxy.net/hybrid/*，應用程式使用者會直接前往自訂首頁。</span><span class="sxs-lookup"><span data-stu-id="921f1-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="921f1-156">使用您在「步驟 1：尋找應用程式的 ObjectID」中複製的 GUID (ObjectID)，進行更新。</span><span class="sxs-lookup"><span data-stu-id="921f1-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="921f1-157">若要確認變更成功，請重新啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="921f1-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="921f1-158">您對應用程式所做的任何變更都可能會重設首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="921f1-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="921f1-159">如果您的首頁 URL 重設，請重複步驟 2。</span><span class="sxs-lookup"><span data-stu-id="921f1-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="921f1-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="921f1-160">Next steps</span></span>

- [<span data-ttu-id="921f1-161">使用 Azure AD 應用程式 Proxy 啟用 SharePoint 的遠端存取</span><span class="sxs-lookup"><span data-stu-id="921f1-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="921f1-162">在 Azure 入口網站中啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="921f1-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
