---
title: "開始使用 AD Android aaaAzure |Microsoft 文件"
description: "如何 toobuild 與 Azure AD 進行登入並呼叫 Azure AD 整合的 Android 應用程式會將使用 OAuth 保護應用程式開發介面。"
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
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="864be-103">將 Azure AD 整合至 Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="864be-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="864be-104">嘗試的新 hello 預覽[開發人員入口網站](https://identity.microsoft.com/Docs/Android)，這將會幫助您獲得 Azure AD 在短短幾分鐘內啟動且正在執行。</span><span class="sxs-lookup"><span data-stu-id="864be-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="864be-105">hello 開發人員入口網站將引導您完成註冊應用程式與 Azure AD 整合您的程式碼 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="864be-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="864be-106">當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。</span><span class="sxs-lookup"><span data-stu-id="864be-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="864be-107">如果您正在開發的桌面應用程式，Azure Active Directory (Azure AD) 使其簡單又直接您 tooauthenticate 為您的使用者使用其內部部署 Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="864be-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="864be-108">它也可讓您的應用程式 toosecurely 取用任何 web API 受到 Azure AD，例如 hello Office 365 Api 或 hello Azure API。</span><span class="sxs-lookup"><span data-stu-id="864be-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="864be-109">對於 Android 用戶端需要 tooaccess 受保護的資源，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="864be-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="864be-110">hello 的 ADAL 的唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="864be-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="864be-111">toodemonstrate 多麼容易，所以我們將會建置 Android 待辦事項清單應用程式：</span><span class="sxs-lookup"><span data-stu-id="864be-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="864be-112">取得存取權杖呼叫待辦事項清單應用程式開發介面使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。</span><span class="sxs-lookup"><span data-stu-id="864be-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="864be-113">取得使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="864be-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="864be-114">登出使用者。</span><span class="sxs-lookup"><span data-stu-id="864be-114">Signs out users.</span></span>

<span data-ttu-id="864be-115">tooget 開始，您需要 Azure AD 租用戶，您可以建立使用者，並註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="864be-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="864be-116">如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="864be-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="864be-117">步驟 1： 下載並執行 hello Node.js REST API TODO 範例伺服器</span><span class="sxs-lookup"><span data-stu-id="864be-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="864be-118">特別是針對現有的 Azure ad 中建立單一租用戶待辦事項 REST API 範例 toowork 寫入 hello Node.js REST API TODO 範例。</span><span class="sxs-lookup"><span data-stu-id="864be-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="864be-119">這是快速入門的 hello 的必要條件。</span><span class="sxs-lookup"><span data-stu-id="864be-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="864be-120">如需有關如何 tooset 其設定，請參閱我們現有的範例中詳細[Microsoft Azure Active Directory 範例 REST API 服務 for Node.js](active-directory-devquickstarts-webapi-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="864be-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="864be-121">步驟 2：向 Azure AD 租用戶註冊 Web API</span><span class="sxs-lookup"><span data-stu-id="864be-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="864be-122">Active Directory 支援加入兩種類型的應用程式：</span><span class="sxs-lookup"><span data-stu-id="864be-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="864be-123">Web 應用程式開發介面中提供服務 toousers</span><span class="sxs-lookup"><span data-stu-id="864be-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="864be-124">存取應用程式 （hello 網站上或在裝置上執行） 的 web 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="864be-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="864be-125">在此步驟中，您正在註冊您在本機執行的測試這個範例的 hello web API。</span><span class="sxs-lookup"><span data-stu-id="864be-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="864be-126">一般來說，此 web API 是 REST 服務的供應項目功能的應用程式 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="864be-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="864be-127">Azure AD 可以保護任何端點。</span><span class="sxs-lookup"><span data-stu-id="864be-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="864be-128">我們假設您正在註冊 hello TODO REST API 參考之前。</span><span class="sxs-lookup"><span data-stu-id="864be-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="864be-129">但這適用於您想要 Azure Active Directory toohelp 保護任何 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="864be-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="864be-130">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="864be-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="864be-131">Hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="864be-131">On hello top bar, click your account.</span></span> <span data-ttu-id="864be-132">在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="864be-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="864be-133">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="864be-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="864be-134">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="864be-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="864be-135">輸入 hello 應用程式的易記名稱 (例如， **TodoListService**)，請選取**Web 應用程式和/或 Web API**，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="864be-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="864be-136">對於 hello 登入 URL，請輸入 hello 範例 hello 基底 URL。</span><span class="sxs-lookup"><span data-stu-id="864be-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="864be-137">依預設，這會是 `https://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="864be-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="864be-138">按一下**確定**toocomplete hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="864be-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="864be-139">仍在 hello Azure 入口網站，移至 tooyour 應用程式頁面、 尋找 hello 應用程式識別碼值，並將它複製。</span><span class="sxs-lookup"><span data-stu-id="864be-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="864be-140">您稍後在設定應用程式時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="864be-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="864be-141">從 hello**設定** -> **屬性**頁面上，更新 hello 應用程式識別碼 URI-輸入`https://<your_tenant_name>/TodoListService`。</span><span class="sxs-lookup"><span data-stu-id="864be-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="864be-142">取代`<your_tenant_name>`hello Azure AD 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="864be-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="864be-143">步驟 3： 註冊 hello 範例 Android 原生用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="864be-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="864be-144">在此範例中，您必須註冊您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="864be-144">You must register your web application in this sample.</span></span> <span data-ttu-id="864be-145">這可讓您的應用程式 toocommunicate 與 hello 剛註冊 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="864be-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="864be-146">Azure AD 會拒絕 tooeven 允許登入您的應用程式 tooask，除非它登錄。</span><span class="sxs-lookup"><span data-stu-id="864be-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="864be-147">屬於 hello hello 模型安全性。</span><span class="sxs-lookup"><span data-stu-id="864be-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="864be-148">我們假設您正在註冊 hello 範例應用程式先前已參考。</span><span class="sxs-lookup"><span data-stu-id="864be-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="864be-149">但此程序適用於任何您正在開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="864be-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="864be-150">也許您會納悶，為什麼要將應用程式和 Web API 都放在一個租用戶。</span><span class="sxs-lookup"><span data-stu-id="864be-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="864be-151">答案您可能已經猜到，您可以建置應用程式來存取在另一個租用戶的 Azure AD 中註冊的外部 API。</span><span class="sxs-lookup"><span data-stu-id="864be-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="864be-152">如果您這樣做，您的客戶將會提示您 tooconsent toohello hello API hello 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="864be-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="864be-153">Active Directory Authentication Library for iOS 會替您處理此同意舉動。</span><span class="sxs-lookup"><span data-stu-id="864be-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="864be-154">當我們瀏覽更進階的功能，您會看到這是從 Azure 和 Office，以及任何其他服務提供者的 Microsoft 應用程式開發介面的 hello 工作所需的 tooaccess hello 套件很重要的一部分。</span><span class="sxs-lookup"><span data-stu-id="864be-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="864be-155">現在，因為您註冊您的 web 應用程式開發介面和應用程式在 hello 相同租用戶，您不會看到任何提示，以取得同意。</span><span class="sxs-lookup"><span data-stu-id="864be-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="864be-156">如果您正在開發應用程式僅供您自己的公司 toouse，這是通常 hello 情況。</span><span class="sxs-lookup"><span data-stu-id="864be-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="864be-157">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="864be-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="864be-158">Hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="864be-158">On hello top bar, click your account.</span></span> <span data-ttu-id="864be-159">在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="864be-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="864be-160">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="864be-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="864be-161">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="864be-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="864be-162">輸入 hello 應用程式的易記名稱 (例如， **TodoListClient Android**)，請選取**原生用戶端應用程式**，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="864be-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="864be-163">Hello 重新導向 URI 中，輸入`http://TodoListClient`。</span><span class="sxs-lookup"><span data-stu-id="864be-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="864be-164">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="864be-164">Click **Finish**.</span></span>
7. <span data-ttu-id="864be-165">Hello 應用程式頁面中，找出 hello 應用程式識別碼值，並將它複製。</span><span class="sxs-lookup"><span data-stu-id="864be-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="864be-166">您稍後在設定應用程式時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="864be-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="864be-167">從 hello**設定**頁面上，選取**必要的使用權限**選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="864be-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="864be-168">找出並選取 TodoListService，並將 hello**存取 TodoListService**權限下的**委派的權限**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="864be-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="864be-169">與 Maven toobuild，您可以使用 pom.xml hello 上方層級：</span><span class="sxs-lookup"><span data-stu-id="864be-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="864be-170">將此儲存機制複製到您選擇的目錄：</span><span class="sxs-lookup"><span data-stu-id="864be-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="864be-171">Hello 中的 hello 步驟[Maven 環境適用於 Android 的必要條件 tooset](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android)。</span><span class="sxs-lookup"><span data-stu-id="864be-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="864be-172">設定 SDK 19 hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="864be-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="864be-173">移 toohello 您再製 hello 儲存機制的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="864be-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="864be-174">執行這個命令：`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="864be-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="864be-175">變更 hello 目錄 toohello 快速入門範例：`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="864be-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="864be-176">執行這個命令：`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="864be-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="864be-177">您應該會看到 hello 啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="864be-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="864be-178">輸入測試使用者認證 tootry。</span><span class="sxs-lookup"><span data-stu-id="864be-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="864be-179">JAR 封裝將立即送出 hello AAR 封裝旁邊。</span><span class="sxs-lookup"><span data-stu-id="864be-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="864be-180">步驟 4： 下載 Android ADAL hello，並將它加入 tooyour Eclipse 工作區</span><span class="sxs-lookup"><span data-stu-id="864be-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="864be-181">我們已經讓您 toohave 輕鬆多個選項 toouse ADAL Android 專案中：</span><span class="sxs-lookup"><span data-stu-id="864be-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="864be-182">您可以使用 hello 來源的程式碼 tooimport 此文件庫，到 Eclipse 和連結 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="864be-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="864be-183">如果您使用 Android Studio 中，您可以使用 hello AAR 封裝格式，並參考 hello 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="864be-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="864be-184">選項 1：原始檔 Zip</span><span class="sxs-lookup"><span data-stu-id="864be-184">Option 1: Source Zip</span></span>
<span data-ttu-id="864be-185">toodownload 副本 hello 原始程式碼中，按一下**Download ZIP**右邊 hello hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="864be-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="864be-186">或者，可以[從 GitHub 下載](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz)。</span><span class="sxs-lookup"><span data-stu-id="864be-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="864be-187">選項 2：透過 Git 取得原始檔</span><span class="sxs-lookup"><span data-stu-id="864be-187">Option 2: Source via Git</span></span>
<span data-ttu-id="864be-188">透過 Git，SDK 輸入 hello tooget hello 原始碼：</span><span class="sxs-lookup"><span data-stu-id="864be-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="864be-189">選項 3：透過 Gradle 取得二進位檔</span><span class="sxs-lookup"><span data-stu-id="864be-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="864be-190">您可以從 hello Maven 中央儲存機制取得 hello 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="864be-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="864be-191">hello AAR 封裝可以包含在 Android Studio 中的專案中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="864be-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="864be-192">選項 4：透過 Maven 取得 AAR</span><span class="sxs-lookup"><span data-stu-id="864be-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="864be-193">如果您使用 hello M2Eclipse 外掛程式，您可以指定 pom.xml 檔案中的 hello 相依性：</span><span class="sxs-lookup"><span data-stu-id="864be-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="864be-194">選項 5: Hello 程式庫資料夾內的 JAR 封裝</span><span class="sxs-lookup"><span data-stu-id="864be-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="864be-195">從 hello Maven 儲存機制取得 hello JAR 檔案，並將其放置到 hello**程式庫**專案資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="864be-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="864be-196">您需要 toocopy hello 所需的資源 tooyour 專案，因為 hello JAR 套件不包含它們。</span><span class="sxs-lookup"><span data-stu-id="864be-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="864be-197">步驟 5： 加入參考 tooAndroid ADAL tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="864be-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="864be-198">新增參考 tooyour 專案，並將它指定為 Android 程式庫。</span><span class="sxs-lookup"><span data-stu-id="864be-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="864be-199">如果您不確定如何 toodo，您可以取得更多有關 hello [Android Studio 網站](http://developer.android.com/tools/projects/projects-eclipse.html)。</span><span class="sxs-lookup"><span data-stu-id="864be-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="864be-200">新增您的專案設定成偵錯 hello 專案相依性。</span><span class="sxs-lookup"><span data-stu-id="864be-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="864be-201">更新您的專案 AndroidManifest.xml 檔案 tooinclude:</span><span class="sxs-lookup"><span data-stu-id="864be-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

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

4. <span data-ttu-id="864be-202">在您的主要活動建立 AuthenticationContext 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="864be-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="864be-203">這個呼叫的 hello 詳細資料已超出本主題中，hello 範圍，但是可以藉由查看 hello 很不錯的起點[Android 原生用戶端範例](https://github.com/AzureADSamples/NativeClient-Android)。</span><span class="sxs-lookup"><span data-stu-id="864be-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="864be-204">在下列範例的 hello，SharedPreferences hello 預設快取，而且授權單位是 hello 形式`https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="864be-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="864be-205">Hello 使用者輸入認證，並接收授權碼之後，請複製此程式碼區塊 toohandle hello 結尾 AuthenticationActivity:</span><span class="sxs-lookup"><span data-stu-id="864be-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="864be-206">tooask 權杖，來定義回呼：</span><span class="sxs-lookup"><span data-stu-id="864be-206">tooask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="864be-207">最後，使用該回呼來要求權杖：</span><span class="sxs-lookup"><span data-stu-id="864be-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="864be-208">以下是 hello 參數說明：</span><span class="sxs-lookup"><span data-stu-id="864be-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="864be-209">*資源*無須且您正嘗試 tooaccess hello 資源。</span><span class="sxs-lookup"><span data-stu-id="864be-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="864be-210">clientid 是必要參數，來自 AzureAD。</span><span class="sxs-lookup"><span data-stu-id="864be-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="864be-211">*RedirectUri*不是必要的 toobe hello acquireToken 呼叫所提供。</span><span class="sxs-lookup"><span data-stu-id="864be-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="864be-212">您可以將它設定為您的套件名稱。</span><span class="sxs-lookup"><span data-stu-id="864be-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="864be-213">*PromptBehavior* tooask 認證 tooskip hello 快取與 cookie 可幫助。</span><span class="sxs-lookup"><span data-stu-id="864be-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="864be-214">*回呼*後權杖交換 hello 授權程式碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="864be-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="864be-215">它有一個 AuthenticationResult 物件，提供存取權杖、過期日期和識別碼權杖資訊。</span><span class="sxs-lookup"><span data-stu-id="864be-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="864be-216">acquireTokenSilent 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="864be-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="864be-217">Toohandle 快取和權杖重新整理，您可以呼叫它。</span><span class="sxs-lookup"><span data-stu-id="864be-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="864be-218">它也提供 hello 的同步處理版本。</span><span class="sxs-lookup"><span data-stu-id="864be-218">It also provides hello sync version.</span></span> <span data-ttu-id="864be-219">它接受 userid 作為參數。</span><span class="sxs-lookup"><span data-stu-id="864be-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="864be-220">使用本逐步解說，您應該有您需要 toosuccessfully 與 Azure Active Directory 整合。</span><span class="sxs-lookup"><span data-stu-id="864be-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="864be-221">如需此工作的範例，請瀏覽 hello AzureADSamples / GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="864be-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="864be-222">重要資訊</span><span class="sxs-lookup"><span data-stu-id="864be-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="864be-223">自訂</span><span class="sxs-lookup"><span data-stu-id="864be-223">Customization</span></span>
<span data-ttu-id="864be-224">您的應用程式資源可以覆寫程式庫專案資源。</span><span class="sxs-lookup"><span data-stu-id="864be-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="864be-225">當您建置應用程式時會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="864be-225">This happens when your app is being built.</span></span> <span data-ttu-id="864be-226">基於這個理由，您可以自訂您想要的驗證活動配置 hello 方式。</span><span class="sxs-lookup"><span data-stu-id="864be-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="864be-227">是確定 tookeep hello 識別碼 hello 控制項，ADAL 會使用 (WebView)。</span><span class="sxs-lookup"><span data-stu-id="864be-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="864be-228">Broker</span><span class="sxs-lookup"><span data-stu-id="864be-228">Broker</span></span>
<span data-ttu-id="864be-229">hello Microsoft Intune 公司入口網站應用程式提供 hello broker 元件。</span><span class="sxs-lookup"><span data-stu-id="864be-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="864be-230">hello 帳戶會建立在 AccountManager。</span><span class="sxs-lookup"><span data-stu-id="864be-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="864be-231">hello 帳戶類型是"com.microsoft.workaccount。 」</span><span class="sxs-lookup"><span data-stu-id="864be-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="864be-232">AccountManager 只允許一個 SSO (單一登入) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="864be-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="864be-233">完成 hello 裝置挑戰的其中一個 hello 應用程式之後，它就會建立 hello 使用者的 SSO cookie。</span><span class="sxs-lookup"><span data-stu-id="864be-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="864be-234">ADAL 使用 hello broker 帳戶，如果在這個驗證器建立一個使用者帳戶，而且您選擇不 tooskip 它。</span><span class="sxs-lookup"><span data-stu-id="864be-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="864be-235">您可以略過與 hello broker 使用者：</span><span class="sxs-lookup"><span data-stu-id="864be-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="864be-236">您需要特殊的 RedirectUri tooregister broker 使用量。</span><span class="sxs-lookup"><span data-stu-id="864be-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="864be-237">RedirectUri 是 hello 格式`msauth://packagename/Base64UrlencodedSignature`。</span><span class="sxs-lookup"><span data-stu-id="864be-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="864be-238">您可以使用 hello 指令碼 brokerRedirectPrint.ps1 或 hello API 呼叫 mContext.getBrokerRedirectUri，應用程式取得您的 RedirectUri。</span><span class="sxs-lookup"><span data-stu-id="864be-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="864be-239">hello 簽章是相關的 tooyour 簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="864be-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="864be-240">hello 目前 broker 模型是針對一個使用者。</span><span class="sxs-lookup"><span data-stu-id="864be-240">hello current broker model is for one user.</span></span> <span data-ttu-id="864be-241">AuthenticationContext 提供 hello API 方法 tooget hello broker 使用者。</span><span class="sxs-lookup"><span data-stu-id="864be-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="864be-242">您的應用程式資訊清單應該具有下列權限 toouse AccountManager 帳戶 hello。</span><span class="sxs-lookup"><span data-stu-id="864be-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="864be-243">如需詳細資訊，請參閱 hello [hello Android 網站上的 AccountManager 資訊](http://developer.android.com/reference/android/accounts/AccountManager.html)。</span><span class="sxs-lookup"><span data-stu-id="864be-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="864be-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="864be-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="864be-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="864be-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="864be-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="864be-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="864be-247">授權單位 URL 和 AD FS</span><span class="sxs-lookup"><span data-stu-id="864be-247">Authority URL and AD FS</span></span>
<span data-ttu-id="864be-248">Active Directory Federation Services (AD FS) 無法辨識為生產 STS，因此您需要的執行個體探索 tooturn 和在 hello AuthenticationContext 建構函式傳遞 false。</span><span class="sxs-lookup"><span data-stu-id="864be-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="864be-249">hello 授權 URL 需要 STS 執行個體和[租用戶名稱](https://login.microsoftonline.com/yourtenant.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="864be-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="864be-250">查詢快取項目</span><span class="sxs-lookup"><span data-stu-id="864be-250">Querying cache items</span></span>
<span data-ttu-id="864be-251">ADAL 在 SharedPreferences 中提供預設快取與一些簡單的快取查詢函式。</span><span class="sxs-lookup"><span data-stu-id="864be-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="864be-252">您可以使用從 AuthenticationContext 取得 hello 目前快取：</span><span class="sxs-lookup"><span data-stu-id="864be-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="864be-253">您也可以提供您的快取實作，如果您想 toocustomize 它。</span><span class="sxs-lookup"><span data-stu-id="864be-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="864be-254">提示行為</span><span class="sxs-lookup"><span data-stu-id="864be-254">Prompt behavior</span></span>
<span data-ttu-id="864be-255">ADAL 提供選項 toospecify 提示行為。</span><span class="sxs-lookup"><span data-stu-id="864be-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="864be-256">PromptBehavior.Auto 如果 hello 重新整理權杖無效，而且不需要使用者的認證，將會顯示 hello UI。</span><span class="sxs-lookup"><span data-stu-id="864be-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="864be-257">PromptBehavior.Always 會略過 hello 快取使用量，並永遠顯示 hello UI。</span><span class="sxs-lookup"><span data-stu-id="864be-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="864be-258">從快取無訊息地要求權杖並重新整理</span><span class="sxs-lookup"><span data-stu-id="864be-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="864be-259">無訊息的權杖要求不會使用 hello UI 快顯，而且不需要的活動。</span><span class="sxs-lookup"><span data-stu-id="864be-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="864be-260">從 hello 快取，如果有的話，它就會傳回語彙基元。</span><span class="sxs-lookup"><span data-stu-id="864be-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="864be-261">如果 hello 權杖到期時，這個方法會嘗試 toorefresh 它。</span><span class="sxs-lookup"><span data-stu-id="864be-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="864be-262">如果 hello 重新整理權杖已過期或失敗，它會傳回 AuthenticationException。</span><span class="sxs-lookup"><span data-stu-id="864be-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="864be-263">您也可以使用此方法進行同步呼叫。</span><span class="sxs-lookup"><span data-stu-id="864be-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="864be-264">您可以設定 null toocallback 或 acquireTokenSilentSync。</span><span class="sxs-lookup"><span data-stu-id="864be-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="864be-265">診斷</span><span class="sxs-lookup"><span data-stu-id="864be-265">Diagnostics</span></span>
<span data-ttu-id="864be-266">這些是 hello 主要資訊來源的診斷問題：</span><span class="sxs-lookup"><span data-stu-id="864be-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="864be-267">例外狀況</span><span class="sxs-lookup"><span data-stu-id="864be-267">Exceptions</span></span>
* <span data-ttu-id="864be-268">記錄檔</span><span class="sxs-lookup"><span data-stu-id="864be-268">Logs</span></span>
* <span data-ttu-id="864be-269">網路追蹤</span><span class="sxs-lookup"><span data-stu-id="864be-269">Network traces</span></span>

<span data-ttu-id="864be-270">請注意，相互關聯識別碼 hello 文件庫中的中央 toohello 診斷。</span><span class="sxs-lookup"><span data-stu-id="864be-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="864be-271">如果您想的 toocorrelate ADAL 要求與其他程式碼中的作業，您可以依每個要求來設定相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="864be-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="864be-272">如果您沒有設定相互關聯識別碼，ADAL 會隨機產生一個。</span><span class="sxs-lookup"><span data-stu-id="864be-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="864be-273">所有記錄訊息和網路呼叫，會再印有 hello 相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="864be-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="864be-274">hello 自我產生每一個要求的識別碼的變更。</span><span class="sxs-lookup"><span data-stu-id="864be-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="864be-275">例外狀況</span><span class="sxs-lookup"><span data-stu-id="864be-275">Exceptions</span></span>
<span data-ttu-id="864be-276">例外狀況是 hello 先診斷。</span><span class="sxs-lookup"><span data-stu-id="864be-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="864be-277">我們嘗試 tooprovide 有用的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="864be-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="864be-278">如果您發現沒有幫助的錯誤訊息，請提出問題來告訴我們。</span><span class="sxs-lookup"><span data-stu-id="864be-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="864be-279">請同時提供裝置資訊，例如機型和 SDK 號碼。</span><span class="sxs-lookup"><span data-stu-id="864be-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="864be-280">記錄檔</span><span class="sxs-lookup"><span data-stu-id="864be-280">Logs</span></span>
<span data-ttu-id="864be-281">您可以設定 hello 文件庫 toogenerate 記錄檔訊息，您可以使用 toohelp 診斷問題。</span><span class="sxs-lookup"><span data-stu-id="864be-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="864be-282">您可以進行 hello 下列呼叫 tooconfigure 回呼，ADAL 會使用 toohand 關閉每個記錄檔訊息，它會產生作為設定記錄。</span><span class="sxs-lookup"><span data-stu-id="864be-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="864be-283">Hello，下列程式碼所示，訊息可以寫入 tooa 自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="864be-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="864be-284">不幸的是，從裝置取得記錄檔沒有標準方法。</span><span class="sxs-lookup"><span data-stu-id="864be-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="864be-285">有一些服務可協助您處理這部份。</span><span class="sxs-lookup"><span data-stu-id="864be-285">There are some services that can help you with this.</span></span> <span data-ttu-id="864be-286">您也可以設計您自己的資源，例如傳送嗨檔案 tooa 伺服器。</span><span class="sxs-lookup"><span data-stu-id="864be-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="864be-287">這些是 hello 記錄層級：</span><span class="sxs-lookup"><span data-stu-id="864be-287">These are hello logging levels:</span></span>
* <span data-ttu-id="864be-288">Error (例外狀況)</span><span class="sxs-lookup"><span data-stu-id="864be-288">Error (exceptions)</span></span>
* <span data-ttu-id="864be-289">Warn (警告)</span><span class="sxs-lookup"><span data-stu-id="864be-289">Warn (warning)</span></span>
* <span data-ttu-id="864be-290">Info (參考用途)</span><span class="sxs-lookup"><span data-stu-id="864be-290">Info (information purposes)</span></span>
* <span data-ttu-id="864be-291">Verbose (更多詳細資料)</span><span class="sxs-lookup"><span data-stu-id="864be-291">Verbose (more details)</span></span>

<span data-ttu-id="864be-292">您設定 hello 記錄層級，像這樣：</span><span class="sxs-lookup"><span data-stu-id="864be-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="864be-293">所有的記錄訊息會傳送 toologcat，加法 tooany 自訂記錄回呼中。</span><span class="sxs-lookup"><span data-stu-id="864be-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="864be-294">您可以從 logcat 取得記錄 tooa 檔，如下所示：</span><span class="sxs-lookup"><span data-stu-id="864be-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="864be-295">如需 adb 命令的詳細資訊，請參閱 hello [hello Android 網站上的 logcat 資訊](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat)。</span><span class="sxs-lookup"><span data-stu-id="864be-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="864be-296">網路追蹤</span><span class="sxs-lookup"><span data-stu-id="864be-296">Network traces</span></span>
<span data-ttu-id="864be-297">您可以使用各種工具 toocapture hello HTTP 流量，ADAL 會產生。</span><span class="sxs-lookup"><span data-stu-id="864be-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="864be-298">如果您已熟悉 hello OAuth 通訊協定，或您需要 tooprovide 診斷資訊 tooMicrosoft 或其他支援管道，這是最有用。</span><span class="sxs-lookup"><span data-stu-id="864be-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="864be-299">Fiddler 是 hello 最簡單的 HTTP 追蹤工具。</span><span class="sxs-lookup"><span data-stu-id="864be-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="864be-300">使用 hello 下列連結 tooset 它 toocorrectly 記錄 ADAL 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="864be-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="864be-301">Fiddler 或 Charles toobe 有用追蹤工具，您必須設定它以未加密的 toorecord SSL 流量。</span><span class="sxs-lookup"><span data-stu-id="864be-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="864be-302">這種方式產生的追蹤可能包含極機密的資訊，例如存取權杖、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="864be-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="864be-303">如果您使用實際執行帳戶，請勿將這些追蹤洩漏給第三方。</span><span class="sxs-lookup"><span data-stu-id="864be-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="864be-304">如果您需要 toosupply 追蹤 toosomeone 順序 tooget 支援，請使用暫時帳戶使用者名稱和密碼與您不介意共用重現 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="864be-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="864be-305">從 hello Telerik 網站：[設定總 Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="864be-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="864be-306">從 GitHub：[設定適用於 ADAL 的 Fiddler 規則](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="864be-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="864be-307">對話方塊模式</span><span class="sxs-lookup"><span data-stu-id="864be-307">Dialog mode</span></span>
<span data-ttu-id="864be-308">hello acquireToken 方法，而活動不支援對話方塊提示字元。</span><span class="sxs-lookup"><span data-stu-id="864be-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="864be-309">加密</span><span class="sxs-lookup"><span data-stu-id="864be-309">Encryption</span></span>
<span data-ttu-id="864be-310">ADAL 會加密 hello 語彙基元和 SharedPreferences 中預設的存放區。</span><span class="sxs-lookup"><span data-stu-id="864be-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="864be-311">您可以查看 hello StorageHelper 類別 toosee hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="864be-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="864be-312">Android 引進 Android KeyStore 4.3 (API 18) 安全儲存體來存放私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="864be-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="864be-313">ADAL 對 API 18 和更新版本使用此機制。</span><span class="sxs-lookup"><span data-stu-id="864be-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="864be-314">如果您想要 toouse ADAL 較低的 SDK 版本，您需要 tooprovide 在 AuthenticationSettings.INSTANCE.setSecretKey 祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="864be-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="864be-315">OAuth2 持有者挑戰</span><span class="sxs-lookup"><span data-stu-id="864be-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="864be-316">hello AuthenticationParameters 類別提供的功能 tooget authorization_uri 從 hello OAuth2 bearer 挑戰。</span><span class="sxs-lookup"><span data-stu-id="864be-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="864be-317">WebView 中的工作階段 Cookie</span><span class="sxs-lookup"><span data-stu-id="864be-317">Session cookies in WebView</span></span>
<span data-ttu-id="864be-318">Android WebView hello 應用程式關閉後，不會清除工作階段 cookie。</span><span class="sxs-lookup"><span data-stu-id="864be-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="864be-319">您可以使用以下範例程式碼來處理這部分：</span><span class="sxs-lookup"><span data-stu-id="864be-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="864be-320">如需 cookie 的詳細資訊，請參閱 hello [hello Android 網站上的 CookieSyncManager 資訊](http://developer.android.com/reference/android/webkit/CookieSyncManager.html)。</span><span class="sxs-lookup"><span data-stu-id="864be-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="864be-321">資源覆寫</span><span class="sxs-lookup"><span data-stu-id="864be-321">Resource overrides</span></span>
<span data-ttu-id="864be-322">hello ADAL 程式庫包含英文 ProgressDialog 訊息字串。</span><span class="sxs-lookup"><span data-stu-id="864be-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="864be-323">如果想要當地語系化的字串，您的應用程式應該覆寫這些英文字串。</span><span class="sxs-lookup"><span data-stu-id="864be-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="864be-324">NTLM 對話方塊</span><span class="sxs-lookup"><span data-stu-id="864be-324">NTLM dialog box</span></span>
<span data-ttu-id="864be-325">ADAL 1.1.0 版支援透過從 WebViewClient hello onReceivedHttpAuthRequest 事件處理 [NTLM] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="864be-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="864be-326">您可以自訂 hello 配置和字串 hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="864be-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="864be-327">跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="864be-327">Cross-app SSO</span></span>
<span data-ttu-id="864be-328">深入了解[如何 tooenable 跨應用程式使用 ADAL 在 Android 上的 SSO](active-directory-sso-android.md)。</span><span class="sxs-lookup"><span data-stu-id="864be-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
