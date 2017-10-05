---
title: "Azure AD Android 入門 | Microsoft Docs"
description: "如何建置 Android 應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="6cffa-103">將 Azure AD 整合至 Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="6cffa-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="6cffa-104">試用新的[開發人員入口網站](https://identity.microsoft.com/Docs/Android)預覽版本，這可協助您在短短幾分鐘內啟動並執行 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="6cffa-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="6cffa-105">開發人員入口網站會逐步引導您完成註冊應用程式並將 Azure AD 整合至您的程式碼的程序。</span><span class="sxs-lookup"><span data-stu-id="6cffa-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="6cffa-106">當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。</span><span class="sxs-lookup"><span data-stu-id="6cffa-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="6cffa-107">如果您正在開發桌面應用程式，Azure Active Directory (Azure AD) 讓您可以更簡單直接地用使用者的內部部署 Active Directory 帳戶來驗證他們。</span><span class="sxs-lookup"><span data-stu-id="6cffa-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="6cffa-108">它也可讓您的應用程式安全地使用任何受 Azure AD 保護的 Web API，例如 Office 365 API 或 Azure API。</span><span class="sxs-lookup"><span data-stu-id="6cffa-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="6cffa-109">對於需要存取受保護資源的 Android 用戶端，Azure AD 提供 Active Directory 驗證程式庫 (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="6cffa-110">ADAL 的唯一目的是為了讓您的應用程式輕鬆取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="6cffa-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="6cffa-111">為了示範究竟多麼簡單，我們將建置一個執行下列動作的 Android「待辦事項清單」應用程式：</span><span class="sxs-lookup"><span data-stu-id="6cffa-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="6cffa-112">取得存取權杖來使用 [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)呼叫待辦事項清單 API。</span><span class="sxs-lookup"><span data-stu-id="6cffa-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="6cffa-113">取得使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="6cffa-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="6cffa-114">登出使用者。</span><span class="sxs-lookup"><span data-stu-id="6cffa-114">Signs out users.</span></span>

<span data-ttu-id="6cffa-115">首先，您需要 Azure AD 租用戶，供您建立使用者並註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cffa-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="6cffa-116">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="6cffa-117">步驟 1：下載並執行 Node.js REST API TODO 範例伺服器</span><span class="sxs-lookup"><span data-stu-id="6cffa-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="6cffa-118">我們特別撰寫 Node.js REST API TODO 範例，以有別於為 Azure AD 建置單一租用戶 To-Do REST API 的現有範例。</span><span class="sxs-lookup"><span data-stu-id="6cffa-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="6cffa-119">這是快速入門的必要條件。</span><span class="sxs-lookup"><span data-stu-id="6cffa-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="6cffa-120">如需如何設置此 API 的資訊，請參閱現有範例[適用於 Node.js 的 Microsoft Azure Active Directory 範例 REST API 服務](active-directory-devquickstarts-webapi-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="6cffa-121">步驟 2：向 Azure AD 租用戶註冊 Web API</span><span class="sxs-lookup"><span data-stu-id="6cffa-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="6cffa-122">Active Directory 支援加入兩種類型的應用程式：</span><span class="sxs-lookup"><span data-stu-id="6cffa-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="6cffa-123">將服務提供給使用者的 Web API</span><span class="sxs-lookup"><span data-stu-id="6cffa-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="6cffa-124">會存取這些 Web API 的應用程式 (在 Web 或裝置上執行)</span><span class="sxs-lookup"><span data-stu-id="6cffa-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="6cffa-125">在此步驟中，您要註冊在本機執行且用來測試此範例的 Web API。</span><span class="sxs-lookup"><span data-stu-id="6cffa-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="6cffa-126">這個 Web API 通常是 REST 服務，提供您想要讓應用程式存取的功能。</span><span class="sxs-lookup"><span data-stu-id="6cffa-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="6cffa-127">Azure AD 可以保護任何端點。</span><span class="sxs-lookup"><span data-stu-id="6cffa-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="6cffa-128">我們假設您是註冊稍早提及的 TODO REST API。</span><span class="sxs-lookup"><span data-stu-id="6cffa-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="6cffa-129">但這個程序適用於任何您要讓 Azure Active Directory 保護的 Web API。</span><span class="sxs-lookup"><span data-stu-id="6cffa-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="6cffa-130">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6cffa-131">在頂端列中，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-131">On the top bar, click your account.</span></span> <span data-ttu-id="6cffa-132">在 [目錄] 清單中，選擇您要註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="6cffa-133">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="6cffa-134">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="6cffa-135">輸入應用程式的易記名稱，例如 **TodoListService**)，選取 [Web 應用程式和/或 Web API]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="6cffa-136">在 [登入 URL] 中，輸入範例的基礎 URL。</span><span class="sxs-lookup"><span data-stu-id="6cffa-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="6cffa-137">依預設，這會是 `https://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="6cffa-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="6cffa-138">按一下 [確定] 完成註冊。</span><span class="sxs-lookup"><span data-stu-id="6cffa-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="6cffa-139">仍是在 Azure 入口網站中，移至您的應用程式頁面，找出 [應用程式識別碼] 的值並複製。</span><span class="sxs-lookup"><span data-stu-id="6cffa-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="6cffa-140">您稍後在設定應用程式時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="6cffa-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="6cffa-141">從 [設定]  ->  [屬性] 頁面，更新應用程式識別碼 URI - 輸入 `https://<your_tenant_name>/TodoListService`。</span><span class="sxs-lookup"><span data-stu-id="6cffa-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="6cffa-142">將 `<your_tenant_name>` 取代為您的 Azure AD 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6cffa-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="6cffa-143">步驟 3：註冊範例 Android 原生用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="6cffa-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="6cffa-144">在此範例中，您必須註冊您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cffa-144">You must register your web application in this sample.</span></span> <span data-ttu-id="6cffa-145">這可讓您的應用程式與剛註冊的 Web API 通訊。</span><span class="sxs-lookup"><span data-stu-id="6cffa-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="6cffa-146">除非註冊應用程式，否則 Azure AD 甚至會拒絕讓您的應用程式要求登入。</span><span class="sxs-lookup"><span data-stu-id="6cffa-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="6cffa-147">這是模型安全性的一環。</span><span class="sxs-lookup"><span data-stu-id="6cffa-147">That's part of the security of the model.</span></span>

<span data-ttu-id="6cffa-148">我們假設您是註冊稍早提及的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cffa-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="6cffa-149">但此程序適用於任何您正在開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cffa-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="6cffa-150">也許您會納悶，為什麼要將應用程式和 Web API 都放在一個租用戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="6cffa-151">答案您可能已經猜到，您可以建置應用程式來存取在另一個租用戶的 Azure AD 中註冊的外部 API。</span><span class="sxs-lookup"><span data-stu-id="6cffa-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="6cffa-152">如果您這麼做，系統會提示您的客戶同意您可以使用應用程式中的 API。</span><span class="sxs-lookup"><span data-stu-id="6cffa-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="6cffa-153">Active Directory Authentication Library for iOS 會替您處理此同意舉動。</span><span class="sxs-lookup"><span data-stu-id="6cffa-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="6cffa-154">隨著我們深入更進階的功能，您將了解這是從 Azure 和 Office 及任何其他服務提供者存取 Microsoft API 套件時所需的一件重要工作。</span><span class="sxs-lookup"><span data-stu-id="6cffa-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="6cffa-155">現在，因為您在相同租用戶下註冊您的 Web API 和應用程式，因此您不會看到任何要求同意的提示。</span><span class="sxs-lookup"><span data-stu-id="6cffa-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="6cffa-156">如果您開發的應用程式僅供自己公司使用，通常會是這種情況。</span><span class="sxs-lookup"><span data-stu-id="6cffa-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="6cffa-157">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6cffa-158">在頂端列中，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-158">On the top bar, click your account.</span></span> <span data-ttu-id="6cffa-159">在 [目錄] 清單中，選擇您要註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="6cffa-160">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="6cffa-161">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="6cffa-162">輸入應用程式的易記名稱，例如 **TodoListClient-Android**，選取 [原生用戶端應用程式]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="6cffa-163">在 [重新導向 URI] 中，輸入 `http://TodoListClient`。</span><span class="sxs-lookup"><span data-stu-id="6cffa-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="6cffa-164">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-164">Click **Finish**.</span></span>
7. <span data-ttu-id="6cffa-165">在應用程式頁面中，找到應用程式識別碼的值並複製。</span><span class="sxs-lookup"><span data-stu-id="6cffa-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="6cffa-166">您稍後在設定應用程式時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="6cffa-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="6cffa-167">在 [設定] 頁面中，選取 [必要的權限]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="6cffa-168">找出並選取 [TodoListService]，然後在 [委派的權限] 底下新增 [存取 TodoListService] 權限，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="6cffa-169">若要使用 Maven 來建置，您可以使用最上層的 pom.xml：</span><span class="sxs-lookup"><span data-stu-id="6cffa-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="6cffa-170">將此儲存機制複製到您選擇的目錄：</span><span class="sxs-lookup"><span data-stu-id="6cffa-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="6cffa-171">請遵循[為 Android 設定 Maven 環境的必要條件](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="6cffa-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="6cffa-172">使用 SDK 19 設定模擬器。</span><span class="sxs-lookup"><span data-stu-id="6cffa-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="6cffa-173">移至您已複製儲存機制的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cffa-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="6cffa-174">執行這個命令：`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="6cffa-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="6cffa-175">將目錄變更為快速入門範例：`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="6cffa-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="6cffa-176">執行這個命令：`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="6cffa-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="6cffa-177">您應該會看到應用程式啟動。</span><span class="sxs-lookup"><span data-stu-id="6cffa-177">You should see the app starting.</span></span>
8. <span data-ttu-id="6cffa-178">輸入測試使用者認證來測試一下。</span><span class="sxs-lookup"><span data-stu-id="6cffa-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="6cffa-179">除了 AAR 套件，也會提交 JAR 套件。</span><span class="sxs-lookup"><span data-stu-id="6cffa-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="6cffa-180">步驟 4：下載 Android ADAL，並將它加入您的 Eclipse 工作區</span><span class="sxs-lookup"><span data-stu-id="6cffa-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="6cffa-181">我們提供多個選項，讓您輕鬆地在 Android 專案中使用 ADAL：</span><span class="sxs-lookup"><span data-stu-id="6cffa-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="6cffa-182">您可以使用原始程式碼將此程式庫匯入到 Eclipse，並連結至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cffa-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="6cffa-183">如果您使用 Android Studio，可以使用 AAR 套件格式並參考二進位檔。</span><span class="sxs-lookup"><span data-stu-id="6cffa-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="6cffa-184">選項 1：原始檔 Zip</span><span class="sxs-lookup"><span data-stu-id="6cffa-184">Option 1: Source Zip</span></span>
<span data-ttu-id="6cffa-185">若要下載原始程式碼，按一下頁面右側的 [下載 ZIP]。</span><span class="sxs-lookup"><span data-stu-id="6cffa-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="6cffa-186">或者，可以[從 GitHub 下載](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="6cffa-187">選項 2：透過 Git 取得原始檔</span><span class="sxs-lookup"><span data-stu-id="6cffa-187">Option 2: Source via Git</span></span>
<span data-ttu-id="6cffa-188">若要透過 Git 取得 SDK 的原始程式碼，請輸入：</span><span class="sxs-lookup"><span data-stu-id="6cffa-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="6cffa-189">選項 3：透過 Gradle 取得二進位檔</span><span class="sxs-lookup"><span data-stu-id="6cffa-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="6cffa-190">您可以從 Maven 中央儲存機制取得二進位檔。</span><span class="sxs-lookup"><span data-stu-id="6cffa-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="6cffa-191">AAR 套件可以在 AndroidStudio 中加入您的專案中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6cffa-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="6cffa-192">選項 4：透過 Maven 取得 AAR</span><span class="sxs-lookup"><span data-stu-id="6cffa-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="6cffa-193">如果您使用 M2E 外掛程式，可以在 pom.xml 檔案中指定相依性：</span><span class="sxs-lookup"><span data-stu-id="6cffa-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="6cffa-194">選項 5：libs 資料夾內的 JAR 套件</span><span class="sxs-lookup"><span data-stu-id="6cffa-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="6cffa-195">您可以從 Maven 儲存機制取得 JAR 檔案，並放入專案的 **libs** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6cffa-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="6cffa-196">您也需要將必要的資源複製到專案，因為 JAR 套件中沒有它們。</span><span class="sxs-lookup"><span data-stu-id="6cffa-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="6cffa-197">步驟 5：將 Android ADAL 參考加入至您的專案</span><span class="sxs-lookup"><span data-stu-id="6cffa-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="6cffa-198">在專案中加入參考，並指定為 Android 程式庫。</span><span class="sxs-lookup"><span data-stu-id="6cffa-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="6cffa-199">如果您不確定怎麼做，可以從 [Android Studio 網站](http://developer.android.com/tools/projects/projects-eclipse.html)取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6cffa-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="6cffa-200">加入專案相依性，以針對您的專案設定進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="6cffa-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="6cffa-201">更新專案的 AndroidManifest.xml 檔案來包含：</span><span class="sxs-lookup"><span data-stu-id="6cffa-201">Update your project's AndroidManifest.xml file to include:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="6cffa-202">在您的主要活動建立 AuthenticationContext 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="6cffa-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="6cffa-203">此呼叫的詳細資料超出本主題的範圍，但您可以查看 [Android 原生用戶端範例](https://github.com/AzureADSamples/NativeClient-Android)，由此開始也很不錯。</span><span class="sxs-lookup"><span data-stu-id="6cffa-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="6cffa-204">在以下範例中，SharedPreferences 是預設快取，Authority 格式為 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`：</span><span class="sxs-lookup"><span data-stu-id="6cffa-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="6cffa-205">複製此程式碼區塊，以便於使用者輸入認證並收到授權碼之後處理 AuthenticationActivity 的結束工作：</span><span class="sxs-lookup"><span data-stu-id="6cffa-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="6cffa-206">若要要求權杖，定義回呼：</span><span class="sxs-lookup"><span data-stu-id="6cffa-206">To ask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="6cffa-207">最後，使用該回呼來要求權杖：</span><span class="sxs-lookup"><span data-stu-id="6cffa-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="6cffa-208">以下是參數的說明：</span><span class="sxs-lookup"><span data-stu-id="6cffa-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="6cffa-209">resource 是必要參數，是您嘗試存取的資源。</span><span class="sxs-lookup"><span data-stu-id="6cffa-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="6cffa-210">clientid 是必要參數，來自 AzureAD。</span><span class="sxs-lookup"><span data-stu-id="6cffa-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="6cffa-211">RedirectUri 在 acquireToken 呼叫中不是必要參數。</span><span class="sxs-lookup"><span data-stu-id="6cffa-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="6cffa-212">您可以將它設定為您的套件名稱。</span><span class="sxs-lookup"><span data-stu-id="6cffa-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="6cffa-213">PromptBehavior 有助於在要求認證時略過快取和 Cookie。</span><span class="sxs-lookup"><span data-stu-id="6cffa-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="6cffa-214">授權碼兌換成權杖之後，就會呼叫 callback。</span><span class="sxs-lookup"><span data-stu-id="6cffa-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="6cffa-215">它有一個 AuthenticationResult 物件，提供存取權杖、過期日期和識別碼權杖資訊。</span><span class="sxs-lookup"><span data-stu-id="6cffa-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="6cffa-216">acquireTokenSilent 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="6cffa-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="6cffa-217">您可以呼叫它來處理快取和權杖重新整理。</span><span class="sxs-lookup"><span data-stu-id="6cffa-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="6cffa-218">它也提供同步處理版本。</span><span class="sxs-lookup"><span data-stu-id="6cffa-218">It also provides the sync version.</span></span> <span data-ttu-id="6cffa-219">它接受 userid 作為參數。</span><span class="sxs-lookup"><span data-stu-id="6cffa-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="6cffa-220">經過這個逐步解說，您應該已擁有與 Azure Active Directory 成功整合所需的項目。</span><span class="sxs-lookup"><span data-stu-id="6cffa-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="6cffa-221">如需此工作的更多範例，請瀏覽 GitHub 上的 AzureADSamples/ 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="6cffa-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="6cffa-222">重要資訊</span><span class="sxs-lookup"><span data-stu-id="6cffa-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="6cffa-223">自訂</span><span class="sxs-lookup"><span data-stu-id="6cffa-223">Customization</span></span>
<span data-ttu-id="6cffa-224">您的應用程式資源可以覆寫程式庫專案資源。</span><span class="sxs-lookup"><span data-stu-id="6cffa-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="6cffa-225">當您建置應用程式時會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="6cffa-225">This happens when your app is being built.</span></span> <span data-ttu-id="6cffa-226">基於這個理由，您可以依想要的方式自訂驗證活動配置。</span><span class="sxs-lookup"><span data-stu-id="6cffa-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="6cffa-227">請記下 ADAL 使用的控制項 (WebView) 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="6cffa-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="6cffa-228">Broker</span><span class="sxs-lookup"><span data-stu-id="6cffa-228">Broker</span></span>
<span data-ttu-id="6cffa-229">Microsoft Intune 公司入口網站應用程式提供「訊息代理程式」元件。</span><span class="sxs-lookup"><span data-stu-id="6cffa-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="6cffa-230">帳戶會在 AccountManager 中建立。</span><span class="sxs-lookup"><span data-stu-id="6cffa-230">The account is created in AccountManager.</span></span> <span data-ttu-id="6cffa-231">帳戶類型為 "com.microsoft.workaccount"。</span><span class="sxs-lookup"><span data-stu-id="6cffa-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="6cffa-232">AccountManager 只允許一個 SSO (單一登入) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="6cffa-233">完成其中一個應用程式的裝置挑戰之後，就會建立此使用者的 SSO Cookie。</span><span class="sxs-lookup"><span data-stu-id="6cffa-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="6cffa-234">如果在這個驗證器上建立使用者帳戶，且您選擇不要略過它，ADAL 會使用訊息代理程式帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="6cffa-235">您可以使用以下方法來略過訊息代理程式使用者：</span><span class="sxs-lookup"><span data-stu-id="6cffa-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="6cffa-236">您必須註冊特殊的 RedirectUri 供訊息代理程式使用。</span><span class="sxs-lookup"><span data-stu-id="6cffa-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="6cffa-237">RedirectUri 的格式為 `msauth://packagename/Base64UrlencodedSignature`。</span><span class="sxs-lookup"><span data-stu-id="6cffa-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="6cffa-238">您可以使用指令碼 brokerRedirectPrint.ps1 或使用 API 呼叫 mContext.getBrokerRedirectUri，以取得應用程式的 RedirectUri。</span><span class="sxs-lookup"><span data-stu-id="6cffa-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="6cffa-239">簽章與您的簽署憑證有關。</span><span class="sxs-lookup"><span data-stu-id="6cffa-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="6cffa-240">目前的訊息代理程式模型僅能用於一位使用者。</span><span class="sxs-lookup"><span data-stu-id="6cffa-240">The current broker model is for one user.</span></span> <span data-ttu-id="6cffa-241">AuthenticationContext 提供 API 方法來取得訊息代理程式使用者。</span><span class="sxs-lookup"><span data-stu-id="6cffa-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="6cffa-242">您的應用程式資訊清單應有下列權限才能使用 AccountManager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cffa-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="6cffa-243">如需詳細資訊，請參閱[Android 網站上的 AccountManager 資訊](http://developer.android.com/reference/android/accounts/AccountManager.html)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="6cffa-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="6cffa-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="6cffa-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="6cffa-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="6cffa-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="6cffa-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="6cffa-247">授權單位 URL 和 AD FS</span><span class="sxs-lookup"><span data-stu-id="6cffa-247">Authority URL and AD FS</span></span>
<span data-ttu-id="6cffa-248">Active Directory 同盟服務 (AD FS) 不視為正式的 STS，因此您需要開啟執行個體探索，並在 AuthenticationContext 建構函式上傳遞 false。</span><span class="sxs-lookup"><span data-stu-id="6cffa-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="6cffa-249">授權單位 URL 需要 STS 執行個體和[租用戶名稱](https://login.microsoftonline.com/yourtenant.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="6cffa-250">查詢快取項目</span><span class="sxs-lookup"><span data-stu-id="6cffa-250">Querying cache items</span></span>
<span data-ttu-id="6cffa-251">ADAL 在 SharedPreferences 中提供預設快取與一些簡單的快取查詢函式。</span><span class="sxs-lookup"><span data-stu-id="6cffa-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="6cffa-252">您可以使用以下方法從 AuthenticationContext 取得目前的快取︰</span><span class="sxs-lookup"><span data-stu-id="6cffa-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="6cffa-253">如果想要自訂它，您也可以提供您的快取實作。</span><span class="sxs-lookup"><span data-stu-id="6cffa-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="6cffa-254">提示行為</span><span class="sxs-lookup"><span data-stu-id="6cffa-254">Prompt behavior</span></span>
<span data-ttu-id="6cffa-255">ADAL 提供可指定提示行為的選項。</span><span class="sxs-lookup"><span data-stu-id="6cffa-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="6cffa-256">如果重新整理權杖無效，而且需要使用者認證，PromptBehavior.Auto 會顯示 UI。</span><span class="sxs-lookup"><span data-stu-id="6cffa-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="6cffa-257">PromptBehavior.Always 會略過快取使用，並一律顯示 UI。</span><span class="sxs-lookup"><span data-stu-id="6cffa-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="6cffa-258">從快取無訊息地要求權杖並重新整理</span><span class="sxs-lookup"><span data-stu-id="6cffa-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="6cffa-259">無訊息要求權杖不會使用 UI 快顯，也不需要活動。</span><span class="sxs-lookup"><span data-stu-id="6cffa-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="6cffa-260">它會從快取傳回權杖 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="6cffa-261">如果權杖已過期，這個方法會嘗試重新整理它。</span><span class="sxs-lookup"><span data-stu-id="6cffa-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="6cffa-262">如果重新整理權杖已過期或失效，則傳回 AuthenticationException。</span><span class="sxs-lookup"><span data-stu-id="6cffa-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="6cffa-263">您也可以使用此方法進行同步呼叫。</span><span class="sxs-lookup"><span data-stu-id="6cffa-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="6cffa-264">您可以將 callback 設為 null，或使用 acquireTokenSilentSync。</span><span class="sxs-lookup"><span data-stu-id="6cffa-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="6cffa-265">診斷</span><span class="sxs-lookup"><span data-stu-id="6cffa-265">Diagnostics</span></span>
<span data-ttu-id="6cffa-266">診斷問題的主要資訊來源有：</span><span class="sxs-lookup"><span data-stu-id="6cffa-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="6cffa-267">例外狀況</span><span class="sxs-lookup"><span data-stu-id="6cffa-267">Exceptions</span></span>
* <span data-ttu-id="6cffa-268">記錄檔</span><span class="sxs-lookup"><span data-stu-id="6cffa-268">Logs</span></span>
* <span data-ttu-id="6cffa-269">網路追蹤</span><span class="sxs-lookup"><span data-stu-id="6cffa-269">Network traces</span></span>

<span data-ttu-id="6cffa-270">請注意，相互關聯識別碼在程式庫中是診斷的核心。</span><span class="sxs-lookup"><span data-stu-id="6cffa-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="6cffa-271">如果您想要將 ADAL 要求與程式碼中其他的作業相互關聯，您可以依每一個要求來設定相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="6cffa-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="6cffa-272">如果您沒有設定相互關聯識別碼，ADAL 會隨機產生一個。</span><span class="sxs-lookup"><span data-stu-id="6cffa-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="6cffa-273">然後所有記錄訊息和網路呼叫加上相互關聯識別碼的戳記。</span><span class="sxs-lookup"><span data-stu-id="6cffa-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="6cffa-274">自行產生的識別碼隨每個要求而不同。</span><span class="sxs-lookup"><span data-stu-id="6cffa-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="6cffa-275">例外狀況</span><span class="sxs-lookup"><span data-stu-id="6cffa-275">Exceptions</span></span>
<span data-ttu-id="6cffa-276">例外狀況是第一個診斷。</span><span class="sxs-lookup"><span data-stu-id="6cffa-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="6cffa-277">我們試著提供有用的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6cffa-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="6cffa-278">如果您發現沒有幫助的錯誤訊息，請提出問題來告訴我們。</span><span class="sxs-lookup"><span data-stu-id="6cffa-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="6cffa-279">請同時提供裝置資訊，例如機型和 SDK 號碼。</span><span class="sxs-lookup"><span data-stu-id="6cffa-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="6cffa-280">記錄檔</span><span class="sxs-lookup"><span data-stu-id="6cffa-280">Logs</span></span>
<span data-ttu-id="6cffa-281">您可以設定程式庫來產生記錄訊息，用以協助診斷問題。</span><span class="sxs-lookup"><span data-stu-id="6cffa-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="6cffa-282">設定記錄時，請執行下列呼叫來設定回呼，供 ADAL 用來移交每一個產生的記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="6cffa-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="6cffa-283">可以在自訂記錄檔中寫入訊息，如以下程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="6cffa-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="6cffa-284">不幸的是，從裝置取得記錄檔沒有標準方法。</span><span class="sxs-lookup"><span data-stu-id="6cffa-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="6cffa-285">有一些服務可協助您處理這部份。</span><span class="sxs-lookup"><span data-stu-id="6cffa-285">There are some services that can help you with this.</span></span> <span data-ttu-id="6cffa-286">您可以也自創方法，例如將檔案傳送到伺服器。</span><span class="sxs-lookup"><span data-stu-id="6cffa-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="6cffa-287">記錄層級分為：</span><span class="sxs-lookup"><span data-stu-id="6cffa-287">These are the logging levels:</span></span>
* <span data-ttu-id="6cffa-288">Error (例外狀況)</span><span class="sxs-lookup"><span data-stu-id="6cffa-288">Error (exceptions)</span></span>
* <span data-ttu-id="6cffa-289">Warn (警告)</span><span class="sxs-lookup"><span data-stu-id="6cffa-289">Warn (warning)</span></span>
* <span data-ttu-id="6cffa-290">Info (參考用途)</span><span class="sxs-lookup"><span data-stu-id="6cffa-290">Info (information purposes)</span></span>
* <span data-ttu-id="6cffa-291">Verbose (更多詳細資料)</span><span class="sxs-lookup"><span data-stu-id="6cffa-291">Verbose (more details)</span></span>

<span data-ttu-id="6cffa-292">設定記錄層級的方法如下：</span><span class="sxs-lookup"><span data-stu-id="6cffa-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="6cffa-293">所有記錄訊息除了傳送至任何自訂記錄檔回呼，也會傳送至 logcat。</span><span class="sxs-lookup"><span data-stu-id="6cffa-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="6cffa-294">您可以將記錄傳送至檔案形式 logcat，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6cffa-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="6cffa-295">如需有關 adb 命令的詳細資訊，請參閱 [Android 網站上的 logcat 資訊](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="6cffa-296">網路追蹤</span><span class="sxs-lookup"><span data-stu-id="6cffa-296">Network traces</span></span>
<span data-ttu-id="6cffa-297">您可以使用各種工具來擷取 ADAL 產生的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="6cffa-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="6cffa-298">如果您熟悉 OAuth 通訊協定，或如果您需要提供診斷資訊給 Microsoft 或其他支援管道，這最有用。</span><span class="sxs-lookup"><span data-stu-id="6cffa-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="6cffa-299">Fiddler 是最簡單的 HTTP 追蹤工具。</span><span class="sxs-lookup"><span data-stu-id="6cffa-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="6cffa-300">請使用下列連結來設定它，以正確記錄 ADAL 網路流量。</span><span class="sxs-lookup"><span data-stu-id="6cffa-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="6cffa-301">為了讓追蹤工具 (如 Fiddler、Charles) 更實用，必須將其設定為記錄未加密的 SSL 流量。</span><span class="sxs-lookup"><span data-stu-id="6cffa-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="6cffa-302">這種方式產生的追蹤可能包含極機密的資訊，例如存取權杖、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6cffa-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="6cffa-303">如果您使用實際執行帳戶，請勿將這些追蹤洩漏給第三方。</span><span class="sxs-lookup"><span data-stu-id="6cffa-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="6cffa-304">如果您需要提供追蹤給某人以取得支援，請使用您不介意共用使用者名稱和密碼的暫時帳戶來重現問題。</span><span class="sxs-lookup"><span data-stu-id="6cffa-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="6cffa-305">從 Telerik 網站：[設定適用於 Android 的 Fiddler](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="6cffa-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="6cffa-306">從 GitHub：[設定適用於 ADAL 的 Fiddler 規則](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="6cffa-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="6cffa-307">對話方塊模式</span><span class="sxs-lookup"><span data-stu-id="6cffa-307">Dialog mode</span></span>
<span data-ttu-id="6cffa-308">沒有活動的 acquireToken 方法支援對話方塊提示。</span><span class="sxs-lookup"><span data-stu-id="6cffa-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="6cffa-309">加密</span><span class="sxs-lookup"><span data-stu-id="6cffa-309">Encryption</span></span>
<span data-ttu-id="6cffa-310">根據預設，ADAL 會加密權杖並儲存在 SharedPreferences 中。</span><span class="sxs-lookup"><span data-stu-id="6cffa-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="6cffa-311">您可以在 StorageHelper 類別查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6cffa-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="6cffa-312">Android 引進 Android KeyStore 4.3 (API 18) 安全儲存體來存放私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6cffa-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="6cffa-313">ADAL 對 API 18 和更新版本使用此機制。</span><span class="sxs-lookup"><span data-stu-id="6cffa-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="6cffa-314">如果您想要使用較低 SDK 版本的 ADAL，您需要在 AuthenticationSettings.INSTANCE.setSecretKey 提供秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6cffa-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="6cffa-315">OAuth2 持有者挑戰</span><span class="sxs-lookup"><span data-stu-id="6cffa-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="6cffa-316">AuthenticationParameters 類別提供從 OAuth2 持有者挑戰取得 authorization_uri 的功能。</span><span class="sxs-lookup"><span data-stu-id="6cffa-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="6cffa-317">WebView 中的工作階段 Cookie</span><span class="sxs-lookup"><span data-stu-id="6cffa-317">Session cookies in WebView</span></span>
<span data-ttu-id="6cffa-318">在應用程式關閉後，Android WebView 不會清除工作階段 Cookie。</span><span class="sxs-lookup"><span data-stu-id="6cffa-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="6cffa-319">您可以使用以下範例程式碼來處理這部分：</span><span class="sxs-lookup"><span data-stu-id="6cffa-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="6cffa-320">如需有關 Cookie 的詳細資訊，請參閱 [Android 網站上的 CookieSyncManager 資訊](http://developer.android.com/reference/android/webkit/CookieSyncManager.html)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="6cffa-321">資源覆寫</span><span class="sxs-lookup"><span data-stu-id="6cffa-321">Resource overrides</span></span>
<span data-ttu-id="6cffa-322">ADAL 程式庫包含 ProgressDialog 訊息的英文字串。</span><span class="sxs-lookup"><span data-stu-id="6cffa-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="6cffa-323">如果想要當地語系化的字串，您的應用程式應該覆寫這些英文字串。</span><span class="sxs-lookup"><span data-stu-id="6cffa-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="6cffa-324">NTLM 對話方塊</span><span class="sxs-lookup"><span data-stu-id="6cffa-324">NTLM dialog box</span></span>
<span data-ttu-id="6cffa-325">ADAL 1.1.0 版支援 NTLM 對話方塊，此對話方塊是透過 WebViewClient 的 onReceivedHttpAuthRequest 事件來處理。</span><span class="sxs-lookup"><span data-stu-id="6cffa-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="6cffa-326">您可以自訂對話方塊的版面配置和字串。</span><span class="sxs-lookup"><span data-stu-id="6cffa-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="6cffa-327">跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="6cffa-327">Cross-app SSO</span></span>
<span data-ttu-id="6cffa-328">了解[如何使用 ADAL 啟用跨應用程式的 SSO](active-directory-sso-android.md)。</span><span class="sxs-lookup"><span data-stu-id="6cffa-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
