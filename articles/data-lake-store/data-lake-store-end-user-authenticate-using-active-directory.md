---
title: "使用者驗證︰搭配使用 Azure Active Directory 與 Data Lake Store | Microsoft Docs"
description: "深入了解如何使用 Azure Active Directory 的 Data Lake Store tooachieve 使用者驗證"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="8d1e2-103">使用 Azure Active Directory 以 Data Lake Store 進行使用者驗證</span><span class="sxs-lookup"><span data-stu-id="8d1e2-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d1e2-104">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="8d1e2-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="8d1e2-105">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="8d1e2-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="8d1e2-106">Azure Data Lake Store 使用 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="8d1e2-107">如果之前撰寫的應用程式，適用於 Azure 資料湖存放區或 Azure Data Lake Analytics，您必須先決定您希望如何 tooauthenticate 應用程式與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8d1e2-108">hello 兩個主要選項如下：</span><span class="sxs-lookup"><span data-stu-id="8d1e2-108">hello two main options available are:</span></span>

* <span data-ttu-id="8d1e2-109">使用者驗證 (本文)</span><span class="sxs-lookup"><span data-stu-id="8d1e2-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="8d1e2-110">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="8d1e2-110">Service-to-service authentication</span></span>

<span data-ttu-id="8d1e2-111">這兩個選項會導致以 OAuth 2.0 權杖取得附加的 tooeach 所提出的要求 tooAzure 資料湖存放區或 Azure Data Lake Analytics 所提供的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="8d1e2-112">本文說明如何建立 **Azure AD 原生應用程式以進行使用者驗證**。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="8d1e2-113">如需服務對服務驗證的 Azure AD 應用程式組態的指示，請參閱[使用 Azure Active Directory 以 Data Lake Store 進行服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d1e2-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="8d1e2-114">Prerequisites</span></span>
* <span data-ttu-id="8d1e2-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-115">An Azure subscription.</span></span> <span data-ttu-id="8d1e2-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="8d1e2-117">您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-117">Your subscription ID.</span></span> <span data-ttu-id="8d1e2-118">您可以從 hello Azure 入口網站來擷取它。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="8d1e2-119">例如，它位於 hello Data Lake Store 帳戶 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![取得訂用帳戶識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="8d1e2-121">您的 Azure AD 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-121">Your Azure AD domain name.</span></span> <span data-ttu-id="8d1e2-122">您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="8d1e2-123">Hello 網域名稱是從 hello 以下螢幕擷取畫面， **contoso.onmicrosoft.com**，和括號中的 hello GUID 是 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![取得 AAD 網域](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="8d1e2-125">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="8d1e2-125">End-user authentication</span></span>
<span data-ttu-id="8d1e2-126">這是建議的方法，如果您想在 tooyour 應用程式透過 Azure AD 使用者 toolog hello。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="8d1e2-127">您的應用程式將會無法 tooaccess 以 hello Azure 資源相同的存取層級 hello 使用者的登入。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="8d1e2-128">您的使用者將需要 tooprovide 定期為了讓您的應用程式 toomaintain 存取其認證。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="8d1e2-129">擁有 hello 使用者登入的 hello 結果是您的應用程式提供存取權杖和重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="8d1e2-130">hello 存取權杖取得附加的 tooeach 要求 tooData 湖存放區或資料湖分析，並有效期為一小時的預設值。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="8d1e2-131">可以使用新的存取權杖，以及它無效，向上 tootwo 週，根據預設，如果定期使用的 tooobtain hello 重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="8d1e2-132">您可以使用兩種不同方法讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="8d1e2-133">使用 OAuth 2.0 hello 快顯視窗</span><span class="sxs-lookup"><span data-stu-id="8d1e2-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="8d1e2-134">您的應用程式可以觸發 OAuth 2.0 授權快顯視窗，在哪一個 hello 使用者輸入其認證。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="8d1e2-135">這個快顯視窗也會搭配 hello Azure AD 雙因素驗證 (2FA) 程序，視需要。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="8d1e2-136">不是支援這個方法尚未在 hello Azure AD 驗證程式庫 (ADAL) 的 Python 或 Java。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="8d1e2-137">直接傳遞使用者認證</span><span class="sxs-lookup"><span data-stu-id="8d1e2-137">Directly passing in user credentials</span></span>
<span data-ttu-id="8d1e2-138">您的應用程式可以直接提供使用者認證 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="8d1e2-139">這個方法僅適用於有組織識別碼的使用者帳戶；不適用於個人/「Live ID」使用者帳戶 (包括以 @outlook.com 或 @live.com 結尾的帳戶)。此外，這個方法與需要 Azure AD 雙因素驗證 (2FA) 的使用者帳戶不相容。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="8d1e2-140">採取這種方法需要 toouse？</span><span class="sxs-lookup"><span data-stu-id="8d1e2-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="8d1e2-141">Azure AD 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-141">Azure AD domain name.</span></span> <span data-ttu-id="8d1e2-142">這已經列於本文章的 hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="8d1e2-143">Azure AD **原生應用程式**</span><span class="sxs-lookup"><span data-stu-id="8d1e2-143">Azure AD **native application**</span></span>
* <span data-ttu-id="8d1e2-144">Hello Azure AD 的原生應用程式的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="8d1e2-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="8d1e2-145">Hello Azure AD 的原生應用程式重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="8d1e2-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="8d1e2-146">設定委派權限</span><span class="sxs-lookup"><span data-stu-id="8d1e2-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="8d1e2-147">步驟 1：建立 Active Directory 原生應用程式</span><span class="sxs-lookup"><span data-stu-id="8d1e2-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="8d1e2-148">建立和設定 Azure AD 原生應用程式，以便使用 Azure Active Directory 以 Azure Data Lake Store 進行使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="8d1e2-149">如需指示，請參閱[建立 Azure AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="8d1e2-150">遵循上述連結 hello hello 指示，請確定您選取**原生**應用程式類型，如 hello 以下螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="8d1e2-151">![建立 Web 應用程式](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "建立原生應用程式")</span><span class="sxs-lookup"><span data-stu-id="8d1e2-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="8d1e2-152">步驟 2：取得應用程式識別碼和重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="8d1e2-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="8d1e2-153">請參閱[取得 hello 應用程式識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)tooretrieve hello 的應用程式識別碼 （也稱為 hello Azure 傳統入口網站中的 hello 用戶端識別碼） hello Azure AD 的原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="8d1e2-154">tooretrieve hello 重新導向 URI，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="8d1e2-155">Hello Azure 入口網站，從選取**Azure Active Directory**，按一下 **應用程式註冊**，然後尋找並按一下您剛才建立的 Azure AD hello 原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="8d1e2-156">從 hello**設定**刀鋒視窗中的 hello 應用程式中，按一下**重新導向 Uri**。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![取得重新導向 URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="8d1e2-158">複製顯示 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="8d1e2-159">步驟 3：設定權限</span><span class="sxs-lookup"><span data-stu-id="8d1e2-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="8d1e2-160">Hello Azure 入口網站，從選取**Azure Active Directory**，按一下 **應用程式註冊**，然後尋找並按一下您剛才建立的 Azure AD hello 原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="8d1e2-161">從 hello**設定**刀鋒視窗中的 hello 應用程式中，按一下**必要的權限**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="8d1e2-163">在 hello**加入應用程式開發介面存取**刀鋒視窗中，按一下**選取應用程式開發介面**，按一下**Azure 資料湖**，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="8d1e2-165">在 hello**加入應用程式開發介面存取**刀鋒視窗中，按一下 [**選取權限**，選取 hello] 核取方塊 toogive**完整存取 tooData Lake Store**，然後按一下**選取**.</span><span class="sxs-lookup"><span data-stu-id="8d1e2-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="8d1e2-167">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-167">Click **Done**.</span></span>

5. <span data-ttu-id="8d1e2-168">重複的 hello 最後的兩個步驟 toogrant 權限**Windows Azure 服務管理 API**以及。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="8d1e2-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8d1e2-169">Next steps</span></span>
<span data-ttu-id="8d1e2-170">在本文中，您建立 Azure AD 的原生應用程式並收集到您需要在您撰寫使用.NET SDK、 Java SDK、 REST API 等用戶端應用程式中的 hello 資訊。您可以現在繼續 toohello 下列文章會討論如何 toouse hello Azure AD web 應用程式 toofirst 向資料湖存放區，然後再執行 hello 存放區上的其他操作。</span><span class="sxs-lookup"><span data-stu-id="8d1e2-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="8d1e2-171">使用 .NET SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8d1e2-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="8d1e2-172">使用 Java SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8d1e2-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="8d1e2-173">使用 REST API 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8d1e2-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

