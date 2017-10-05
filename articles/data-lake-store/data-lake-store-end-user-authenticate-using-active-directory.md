---
title: "使用者驗證︰搭配使用 Azure Active Directory 與 Data Lake Store | Microsoft Docs"
description: "了解如何搭配使用 Azure Active Directory 與 Data Lake Store 以完成使用者驗證"
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
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="becf3-103">使用 Azure Active Directory 以 Data Lake Store 進行使用者驗證</span><span class="sxs-lookup"><span data-stu-id="becf3-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="becf3-104">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="becf3-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="becf3-105">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="becf3-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="becf3-106">Azure Data Lake Store 使用 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="becf3-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="becf3-107">撰寫搭配 Azure Data Lake Store 或 Azure Data Lake Analytics 的應用程式之前，必須先決定要如何以 Azure Active Directory (Azure AD) 驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="becf3-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="becf3-108">兩個主要選項為︰</span><span class="sxs-lookup"><span data-stu-id="becf3-108">The two main options available are:</span></span>

* <span data-ttu-id="becf3-109">使用者驗證 (本文)</span><span class="sxs-lookup"><span data-stu-id="becf3-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="becf3-110">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="becf3-110">Service-to-service authentication</span></span>

<span data-ttu-id="becf3-111">兩個選項都要靠 OAuth 2.0 權杖來提供您的應用程式，權杖會附加到每個對 Azure Data Lake Store 或 Azure Data Lake Analytics 提出的要求。</span><span class="sxs-lookup"><span data-stu-id="becf3-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="becf3-112">本文說明如何建立 **Azure AD 原生應用程式以進行使用者驗證**。</span><span class="sxs-lookup"><span data-stu-id="becf3-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="becf3-113">如需服務對服務驗證的 Azure AD 應用程式組態的指示，請參閱[使用 Azure Active Directory 以 Data Lake Store 進行服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="becf3-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="becf3-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="becf3-114">Prerequisites</span></span>
* <span data-ttu-id="becf3-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="becf3-115">An Azure subscription.</span></span> <span data-ttu-id="becf3-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="becf3-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="becf3-117">您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="becf3-117">Your subscription ID.</span></span> <span data-ttu-id="becf3-118">您可以在 Azure 入口網站擷取。</span><span class="sxs-lookup"><span data-stu-id="becf3-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="becf3-119">例如，可從 [Data Lake Store] 帳戶刀鋒視窗取得。</span><span class="sxs-lookup"><span data-stu-id="becf3-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![取得訂用帳戶識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="becf3-121">您的 Azure AD 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="becf3-121">Your Azure AD domain name.</span></span> <span data-ttu-id="becf3-122">將滑鼠游標停留在 Azure 入口網站右上角，即可擷取它。</span><span class="sxs-lookup"><span data-stu-id="becf3-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="becf3-123">在以下螢幕擷取畫面中，網域名稱是 **contoso.onmicrosoft.com**，括號內的 GUID 是租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="becf3-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![取得 AAD 網域](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="becf3-125">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="becf3-125">End-user authentication</span></span>
<span data-ttu-id="becf3-126">如果您想要讓使用者透過 Azure AD 登入您的應用程式，建議使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="becf3-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="becf3-127">您的應用程式將能夠存取 Azure 資源，並與登入使用者具有相同的存取層級。</span><span class="sxs-lookup"><span data-stu-id="becf3-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="becf3-128">您的使用者必須定期提供認證，您的應用程式才能繼續存取。</span><span class="sxs-lookup"><span data-stu-id="becf3-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="becf3-129">有使用者登入的結果，是系統會給您的應用程式一個存取權杖和一個重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="becf3-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="becf3-130">存取權杖會附加到每個對 Data Lake Store 或 Data Lake Analytics 提出的要求，預設的有效期是一小時。</span><span class="sxs-lookup"><span data-stu-id="becf3-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="becf3-131">重新整理權杖可用來取得新的存取權杖，預設的有效期是二小時，如果定期使用則最多兩週。</span><span class="sxs-lookup"><span data-stu-id="becf3-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="becf3-132">您可以使用兩種不同方法讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="becf3-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="becf3-133">使用 OAuth 2.0 快顯視窗</span><span class="sxs-lookup"><span data-stu-id="becf3-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="becf3-134">您的應用程式可以觸發 OAuth 2.0 授權快顯視窗，讓使用者輸入其認證。</span><span class="sxs-lookup"><span data-stu-id="becf3-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="becf3-135">如有必要，這個快顯視窗也適用於 Azure AD 雙因素驗證 (2FA) 程序。</span><span class="sxs-lookup"><span data-stu-id="becf3-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="becf3-136">適用於 Python 或 Java 的 Azure AD 驗證程式庫 (ADAL) 尚未支援這個方法。</span><span class="sxs-lookup"><span data-stu-id="becf3-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="becf3-137">直接傳遞使用者認證</span><span class="sxs-lookup"><span data-stu-id="becf3-137">Directly passing in user credentials</span></span>
<span data-ttu-id="becf3-138">您的應用程式可以直接提供對 Azure AD 的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="becf3-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="becf3-139">這個方法僅適用於有組織識別碼的使用者帳戶；不適用於個人/「Live ID」使用者帳戶 (包括以 @outlook.com 或 @live.com 結尾的帳戶)。</span><span class="sxs-lookup"><span data-stu-id="becf3-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="becf3-140">此外，這個方法與需要 Azure AD 雙因素驗證 (2FA) 的使用者帳戶不相容。</span><span class="sxs-lookup"><span data-stu-id="becf3-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="becf3-141">使用這個方法時需要什麼？</span><span class="sxs-lookup"><span data-stu-id="becf3-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="becf3-142">Azure AD 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="becf3-142">Azure AD domain name.</span></span> <span data-ttu-id="becf3-143">已列在本文的先決條件中。</span><span class="sxs-lookup"><span data-stu-id="becf3-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="becf3-144">Azure AD **原生應用程式**</span><span class="sxs-lookup"><span data-stu-id="becf3-144">Azure AD **native application**</span></span>
* <span data-ttu-id="becf3-145">Azure AD 原生應用程式的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="becf3-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="becf3-146">Azure AD 原生應用程式的重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="becf3-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="becf3-147">設定委派權限</span><span class="sxs-lookup"><span data-stu-id="becf3-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="becf3-148">步驟 1：建立 Active Directory 原生應用程式</span><span class="sxs-lookup"><span data-stu-id="becf3-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="becf3-149">建立和設定 Azure AD 原生應用程式，以便使用 Azure Active Directory 以 Azure Data Lake Store 進行使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="becf3-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="becf3-150">如需指示，請參閱[建立 Azure AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="becf3-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="becf3-151">依照上面連結中的指示進行時，請確定如以下螢幕擷取畫面所示，選取 [原生] 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="becf3-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="becf3-152">![建立 Web 應用程式](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "建立原生應用程式")</span><span class="sxs-lookup"><span data-stu-id="becf3-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="becf3-153">步驟 2：取得應用程式識別碼和重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="becf3-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="becf3-154">請參閱[取得應用程式識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)，以擷取 Azure AD 原生應用程式的應用程式識別碼 (在 Azure 傳統入口網站中也稱為用戶端識別碼)。</span><span class="sxs-lookup"><span data-stu-id="becf3-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="becf3-155">若要擷取重新導向 URI，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="becf3-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="becf3-156">在 Azure 入口網站中，選取 [Azure Active Directory]，按一下 [應用程式註冊]，然後尋找並按一下您剛剛建立的 Azure AD 原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="becf3-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="becf3-157">在應用程式的 [設定] 刀鋒視窗中，按一下 [重新導向 URI]。</span><span class="sxs-lookup"><span data-stu-id="becf3-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![取得重新導向 URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="becf3-159">複製顯示的值。</span><span class="sxs-lookup"><span data-stu-id="becf3-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="becf3-160">步驟 3：設定權限</span><span class="sxs-lookup"><span data-stu-id="becf3-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="becf3-161">在 Azure 入口網站中，選取 [Azure Active Directory]，按一下 [應用程式註冊]，然後尋找並按一下您剛剛建立的 Azure AD 原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="becf3-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="becf3-162">在應用程式的 [設定] 刀鋒視窗中，按一下 [必要的權限]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="becf3-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="becf3-164">在 [加入 API 存取權] 刀鋒視窗中，依序按一下 [選取 API]、[Azure Data Lake]，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="becf3-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="becf3-166">在 [加入 API 存取權] 刀鋒視窗中，按一下 [選取權限]，選取核取方塊以提供 **Data Lake Store 完整的存取權**，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="becf3-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="becf3-168">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="becf3-168">Click **Done**.</span></span>

5. <span data-ttu-id="becf3-169">重複最後兩個步驟，以便將權限也授與 **Windows Azure 服務管理 API**。</span><span class="sxs-lookup"><span data-stu-id="becf3-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="becf3-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="becf3-170">Next steps</span></span>
<span data-ttu-id="becf3-171">在本文中，您已建立 Azure AD 原生應用程式，並收集您使用 .NET SDK、Java SDK、REST API 等撰寫之用戶端應用程式中所需的資訊。您現在可以繼續進行下列文章，這些文章說明如何使用 Azure AD Web 應用程式先以 Data Lake Store 進行驗證，然後再於存放區上執行其他作業。</span><span class="sxs-lookup"><span data-stu-id="becf3-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="becf3-172">使用 .NET SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="becf3-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="becf3-173">使用 Java SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="becf3-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="becf3-174">使用 REST API 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="becf3-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

