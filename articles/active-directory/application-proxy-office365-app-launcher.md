---
title: "aaaSet 自訂的首頁上，使用 Azure AD Application Proxy 發行應用程式 |Microsoft 文件"
description: "涵蓋有關 Azure AD 應用程式 Proxy 連接器 hello 基本概念"
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
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="6ffb3-103">使用 Azure AD 應用程式 Proxy 為發佈的應用程式設定自訂首頁</span><span class="sxs-lookup"><span data-stu-id="6ffb3-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="6ffb3-104">本文將討論如何 tooconfigure 應用程式 toodirect 使用者 tooa 自訂的首頁。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="6ffb3-105">當您發行應用程式 Proxy 的應用程式時，設定內部 URL，但有時候，可能會不 hello 頁面，您的使用者應該會看到第一次。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="6ffb3-106">設定自訂的首頁，讓您的使用者會從 Azure Active Directory 存取面板 hello 或 hello Office 365 應用程式啟動器存取 hello 應用程式時，請移 toohello 右頁。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="6ffb3-107">當使用者啟動 hello 應用程式時，系統正在指示由預設 toohello 根網域 URL hello 發行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="6ffb3-108">hello 登陸頁面通常設定為 hello 首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="6ffb3-109">當您想要應用程式使用者 tooland hello 應用程式內的特定頁面上，請使用 hello Azure AD PowerShell 模組 toodefine 自訂的首頁 Url。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="6ffb3-110">例如：</span><span class="sxs-lookup"><span data-stu-id="6ffb3-110">For example:</span></span>
- <span data-ttu-id="6ffb3-111">您的公司網路內部使用者前往太*https://ExpenseApp/login/login.aspx* toosign 中的並存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="6ffb3-112">因為您有其他資產，如同應用程式 Proxy 需要 tooaccess 在 hello hello 資料夾結構的高層級的影像，您發行 hello 應用程式與*https://ExpenseApp*為 hello 內部 URL。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="6ffb3-113">hello 的預設外部 URL 是*https://ExpenseApp-contoso.msappproxy.net*，而不需要您的使用者 toohello 登頁面中。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="6ffb3-114">設定*https://ExpenseApp-contoso.msappproxy.net/login/login.aspx*為 hello 首頁 URL toogive 使用者順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="6ffb3-115">當您授與使用者存取 toopublished 應用程式時，hello 應用程式會顯示在 hello [Azure AD 存取面板](active-directory-saas-access-panel-introduction.md)和 hello [Office 365 應用程式啟動器](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher)。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6ffb3-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="6ffb3-116">Before you start</span></span>

<span data-ttu-id="6ffb3-117">設定 hello 首頁 URL 之前，請注意下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb3-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="6ffb3-118">請確定您指定的 hello 路徑是子網域的 hello 根網域的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="6ffb3-119">如果 hello 根網域的 URL，例如 https://apps.contoso.com/app1/，您所設定的 hello 首頁 URL 開頭必須 https://apps.contoso.com/app1/。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="6ffb3-120">如果您變更 toohello 發佈應用程式時，hello 變更可能會重設 hello hello 首頁 URL 值。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="6ffb3-121">當您更新在未來的 hello hello 應用程式時，您應該重新檢查，然後必要時，更新 hello 首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="6ffb3-122">變更 hello Azure 入口網站中的 hello 首頁</span><span class="sxs-lookup"><span data-stu-id="6ffb3-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="6ffb3-123">登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="6ffb3-124">瀏覽過**Azure Active Directory** > **應用程式註冊**和從 hello 清單中選擇您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="6ffb3-125">選取**屬性**hello 設定。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="6ffb3-126">更新 hello**首頁 URL**欄位與新的路徑。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![提供新的首頁 URL](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="6ffb3-128">選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="6ffb3-129">使用 PowerShell 變更 hello 首頁</span><span class="sxs-lookup"><span data-stu-id="6ffb3-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="6ffb3-130">安裝 hello Azure AD PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="6ffb3-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="6ffb3-131">您使用 PowerShell 來定義自訂的首頁 URL 之前，先安裝 hello Azure AD PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="6ffb3-132">您可以從 hello 下載 hello 封裝[PowerShell 資源庫](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131)，它會使用 hello Graph API 端點。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="6ffb3-133">tooinstall hello 封裝，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ffb3-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="6ffb3-134">開啟標準的 PowerShell 視窗，並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb3-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="6ffb3-135">如果您以非系統管理員執行 hello 命令，請使用 hello`-scope currentuser`選項。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="6ffb3-136">Hello 安裝期間選取**Y** tooinstall 兩從 Nuget.org 的封裝。兩個套件都是必要套件。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="6ffb3-137">Hello ObjectID hello 應用程式中尋找</span><span class="sxs-lookup"><span data-stu-id="6ffb3-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="6ffb3-138">取得 hello ObjectID hello 應用程式，，然後搜尋 hello 應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="6ffb3-139">開啟 PowerShell 並匯入 hello Azure AD 模組。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="6ffb3-140">以登入 toohello Azure AD 模組 hello 租用戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="6ffb3-141">尋找 hello 應用程式依據首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="6ffb3-142">您可以在 hello 入口網站中找到 hello URL 太移**Azure Active Directory** > **企業應用程式** > **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="6ffb3-143">這個範例會使用 sharepoint-iddemo。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="6ffb3-144">您應該取得結果，其會類似 toohello 一個如下所示。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="6ffb3-145">複製 hello ObjectID GUID toouse hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="6ffb3-146">更新 hello 首頁 URL</span><span class="sxs-lookup"><span data-stu-id="6ffb3-146">Update hello home page URL</span></span>

<span data-ttu-id="6ffb3-147">在 hello 為步驟 1 所用的同一個 PowerShell 模組中執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb3-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="6ffb3-148">確認您擁有 hello 更正應用程式，並取代*8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4*以 hello hello 前面步驟中複製的 ObjectID。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="6ffb3-149">現在您已確認 hello 應用程式，您已準備好 tooupdate hello 首頁上，，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="6ffb3-150">建立空白的應用程式物件 toohold 想 toomake hello 變更。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="6ffb3-151">這個變數會保存您想 tooupdate hello 值。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="6ffb3-152">此步驟不會建立任何項目。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="6ffb3-153">設定 hello 首頁 URL toohello 您想要的值。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="6ffb3-154">hello 值必須是子網域 hello 已發行應用程式的路徑。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="6ffb3-155">例如，如果您變更 hello 首頁 URL 從*https://sharepoint-iddemo.msappproxy.net/*太*https://sharepoint-iddemo.msappproxy.net/hybrid/*，應用程式的使用者而直接前往 toohello 自訂首頁。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="6ffb3-156">請使用 hello GUID (ObjectID) 中複製 hello 更新 」 步驟 1： 尋找 hello hello 應用程式的 ObjectID。 」</span><span class="sxs-lookup"><span data-stu-id="6ffb3-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="6ffb3-157">tooconfirm hello 變更已成功，重新啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="6ffb3-158">您讓 toohello 應用程式的任何變更可能會重設 hello 首頁 URL。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="6ffb3-159">如果您的首頁 URL 重設，請重複步驟 2。</span><span class="sxs-lookup"><span data-stu-id="6ffb3-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ffb3-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ffb3-160">Next steps</span></span>

- [<span data-ttu-id="6ffb3-161">啟用與 Azure AD Application Proxy 的遠端存取 tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="6ffb3-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="6ffb3-162">在 hello Azure 入口網站中啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="6ffb3-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
