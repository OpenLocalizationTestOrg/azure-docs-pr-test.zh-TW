---
title: "行動應用程式和行動服務中的 aaaClient 和伺服器 SDK 版本設定 |Microsoft 文件"
description: "列出適用於行動服務和 Azure Mobile Apps 的用戶端 SDK 和與伺服器 SDK 版本的相容性"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="5a82c-103">Mobile Apps 和行動服務中的用戶端和伺服器版本控制</span><span class="sxs-lookup"><span data-stu-id="5a82c-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="5a82c-104">hello 最新版本的 Azure Mobile Services 為 hello**行動應用程式**Azure 應用程式服務的功能。</span><span class="sxs-lookup"><span data-stu-id="5a82c-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="5a82c-105">hello 行動裝置應用程式用戶端和伺服器 Sdk 原本根據行動服務中的項目，但是可以*不*彼此相容。</span><span class="sxs-lookup"><span data-stu-id="5a82c-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="5a82c-106">也就是說，您必須使用 Mobile Apps 用戶端 SDK 搭配 Mobile Apps 伺服器 SDK，「行動服務」也是類似作法。</span><span class="sxs-lookup"><span data-stu-id="5a82c-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="5a82c-107">透過 hello 用戶端和伺服器 Sdk，所使用的特殊標頭值強制執行這項契約`ZUMO-API-VERSION`。</span><span class="sxs-lookup"><span data-stu-id="5a82c-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="5a82c-108">注意： 這份文件是指的每當 tooa*行動服務*後端，就不一定需要 toobe 裝載於行動服務。</span><span class="sxs-lookup"><span data-stu-id="5a82c-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="5a82c-109">它現在可能 toomigrate App Service 上的行動服務 toorun 不需要變更任何程式碼，但 hello 服務仍會在使用*行動服務*SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="5a82c-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="5a82c-110">深入了解 toolearn 移轉 tooApp 服務不需要變更任何程式碼，請參閱 hello 文章[移轉應用程式服務的行動服務 tooAzure]。</span><span class="sxs-lookup"><span data-stu-id="5a82c-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="5a82c-111">標頭規格</span><span class="sxs-lookup"><span data-stu-id="5a82c-111">Header specification</span></span>
<span data-ttu-id="5a82c-112">hello 金鑰`ZUMO-API-VERSION`可能 hello HTTP 標頭或 hello 查詢字串中指定。</span><span class="sxs-lookup"><span data-stu-id="5a82c-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="5a82c-113">hello 值為 hello 格式的版本字串**x.y.z**。</span><span class="sxs-lookup"><span data-stu-id="5a82c-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="5a82c-114">例如：</span><span class="sxs-lookup"><span data-stu-id="5a82c-114">For example:</span></span>

<span data-ttu-id="5a82c-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="5a82c-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="5a82c-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="5a82c-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="5a82c-118">選擇不進行版本檢查</span><span class="sxs-lookup"><span data-stu-id="5a82c-118">Opting out of version checking</span></span>
<span data-ttu-id="5a82c-119">您可以選擇退出版本檢查設定的值**true** hello 應用程式設定**MS_SkipVersionCheck**。</span><span class="sxs-lookup"><span data-stu-id="5a82c-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="5a82c-120">在 web.config 中或在 hello hello Azure 入口網站應用程式設定 區段中，請指定這個選項。</span><span class="sxs-lookup"><span data-stu-id="5a82c-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5a82c-121">有一些行動服務和行動應用程式，特別是在離線同步處理、 驗證和推播通知的 hello 區域之間的行為變更。</span><span class="sxs-lookup"><span data-stu-id="5a82c-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="5a82c-122">您應該只選擇退出，這些行為的變更不會中斷您的應用程式功能完整的測試 tooensure 後進行檢查的版本。</span><span class="sxs-lookup"><span data-stu-id="5a82c-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="5a82c-123">所有版本的相容性摘要</span><span class="sxs-lookup"><span data-stu-id="5a82c-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="5a82c-124">hello 下圖顯示 hello 所有用戶端和伺服器型別之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="5a82c-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="5a82c-125">後端會被分類為任一行動**服務**或行動裝置版**應用程式**hello server SDK，它會使用為基礎。</span><span class="sxs-lookup"><span data-stu-id="5a82c-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="5a82c-126">**行動服務** Node.js 或 .NET</span><span class="sxs-lookup"><span data-stu-id="5a82c-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="5a82c-127">**Mobile Apps** Node.js 或 .NET</span><span class="sxs-lookup"><span data-stu-id="5a82c-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a82c-128">[行動服務用戶端]</span><span class="sxs-lookup"><span data-stu-id="5a82c-128">[Mobile Services clients]</span></span> |<span data-ttu-id="5a82c-129">確定</span><span class="sxs-lookup"><span data-stu-id="5a82c-129">Ok</span></span> |<span data-ttu-id="5a82c-130">錯誤\*</span><span class="sxs-lookup"><span data-stu-id="5a82c-130">Error\*</span></span> |
| <span data-ttu-id="5a82c-131">[Mobile Apps 用戶端]</span><span class="sxs-lookup"><span data-stu-id="5a82c-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="5a82c-132">錯誤\*</span><span class="sxs-lookup"><span data-stu-id="5a82c-132">Error\*</span></span> |<span data-ttu-id="5a82c-133">確定</span><span class="sxs-lookup"><span data-stu-id="5a82c-133">Ok</span></span> |

<span data-ttu-id="5a82c-134">\*這可以藉由指定 **MS_SkipVersionCheck** 來控制。</span><span class="sxs-lookup"><span data-stu-id="5a82c-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="5a82c-135"><a name="1.0.0"></a>行動服務用戶端和伺服器</span><span class="sxs-lookup"><span data-stu-id="5a82c-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="5a82c-136">hello 表中的 hello 用戶端 Sdk 可與相容**行動服務**。</span><span class="sxs-lookup"><span data-stu-id="5a82c-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="5a82c-137">注意： hello 行動服務用戶端 Sdk*不*傳送的標頭值`ZUMO-API-VERSION`。</span><span class="sxs-lookup"><span data-stu-id="5a82c-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="5a82c-138">如果 hello 服務收到此標頭或查詢字串值，也將會傳回錯誤，除非您明確選擇逾時 （如上所述）。</span><span class="sxs-lookup"><span data-stu-id="5a82c-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="5a82c-139"><a name="MobileServicesClients"></a>行動「服務」用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="5a82c-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="5a82c-140">用戶端平台</span><span class="sxs-lookup"><span data-stu-id="5a82c-140">Client platform</span></span> | <span data-ttu-id="5a82c-141">版本</span><span class="sxs-lookup"><span data-stu-id="5a82c-141">Version</span></span> | <span data-ttu-id="5a82c-142">版本標頭值</span><span class="sxs-lookup"><span data-stu-id="5a82c-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a82c-143">受管理的用戶端 (Windows、Xamarin)</span><span class="sxs-lookup"><span data-stu-id="5a82c-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="5a82c-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="5a82c-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="5a82c-145">n/a</span><span class="sxs-lookup"><span data-stu-id="5a82c-145">n/a</span></span> |
| <span data-ttu-id="5a82c-146">iOS</span><span class="sxs-lookup"><span data-stu-id="5a82c-146">iOS</span></span> |[<span data-ttu-id="5a82c-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="5a82c-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="5a82c-148">n/a</span><span class="sxs-lookup"><span data-stu-id="5a82c-148">n/a</span></span> |
| <span data-ttu-id="5a82c-149">Android</span><span class="sxs-lookup"><span data-stu-id="5a82c-149">Android</span></span> |[<span data-ttu-id="5a82c-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="5a82c-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="5a82c-151">n/a</span><span class="sxs-lookup"><span data-stu-id="5a82c-151">n/a</span></span> |
| <span data-ttu-id="5a82c-152">HTML</span><span class="sxs-lookup"><span data-stu-id="5a82c-152">HTML</span></span> |[<span data-ttu-id="5a82c-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="5a82c-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="5a82c-154">n/a</span><span class="sxs-lookup"><span data-stu-id="5a82c-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="5a82c-155">行動「服務」  伺服器 SDK</span><span class="sxs-lookup"><span data-stu-id="5a82c-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="5a82c-156">伺服器平台</span><span class="sxs-lookup"><span data-stu-id="5a82c-156">Server platform</span></span> | <span data-ttu-id="5a82c-157">版本</span><span class="sxs-lookup"><span data-stu-id="5a82c-157">Version</span></span> | <span data-ttu-id="5a82c-158">接受的版本標頭</span><span class="sxs-lookup"><span data-stu-id="5a82c-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a82c-159">.NET</span><span class="sxs-lookup"><span data-stu-id="5a82c-159">.NET</span></span> |[<span data-ttu-id="5a82c-160">WindowsAzure.MobileServices.Backend.* 版本 1.0.x</span><span class="sxs-lookup"><span data-stu-id="5a82c-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="5a82c-161">* * 沒有版本標頭 * *</span><span class="sxs-lookup"><span data-stu-id="5a82c-161">**No version header **</span></span> |
| <span data-ttu-id="5a82c-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a82c-162">Node.js</span></span> |<span data-ttu-id="5a82c-163">(敬請期待)</span><span class="sxs-lookup"><span data-stu-id="5a82c-163">(coming soon)</span></span> |<span data-ttu-id="5a82c-164">**無版本標頭**</span><span class="sxs-lookup"><span data-stu-id="5a82c-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="5a82c-165">行動服務後端的行為</span><span class="sxs-lookup"><span data-stu-id="5a82c-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="5a82c-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="5a82c-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="5a82c-167">MS_SkipVersionCheck 的值</span><span class="sxs-lookup"><span data-stu-id="5a82c-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="5a82c-168">Response</span><span class="sxs-lookup"><span data-stu-id="5a82c-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a82c-169">未指定</span><span class="sxs-lookup"><span data-stu-id="5a82c-169">Not specified</span></span> |<span data-ttu-id="5a82c-170">任意</span><span class="sxs-lookup"><span data-stu-id="5a82c-170">Any</span></span> |<span data-ttu-id="5a82c-171">200 - 確定</span><span class="sxs-lookup"><span data-stu-id="5a82c-171">200 - OK</span></span> |
| <span data-ttu-id="5a82c-172">任何值</span><span class="sxs-lookup"><span data-stu-id="5a82c-172">Any value</span></span> |<span data-ttu-id="5a82c-173">True</span><span class="sxs-lookup"><span data-stu-id="5a82c-173">True</span></span> |<span data-ttu-id="5a82c-174">200 - 確定</span><span class="sxs-lookup"><span data-stu-id="5a82c-174">200 - OK</span></span> |
| <span data-ttu-id="5a82c-175">任何值</span><span class="sxs-lookup"><span data-stu-id="5a82c-175">Any value</span></span> |<span data-ttu-id="5a82c-176">False/未指定</span><span class="sxs-lookup"><span data-stu-id="5a82c-176">False/Not Specified</span></span> |<span data-ttu-id="5a82c-177">400 - 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="5a82c-177">400 - Bad Request</span></span> |

## <span data-ttu-id="5a82c-178"><a name="2.0.0"></a>Azure Mobile Apps 用戶端和伺服器</span><span class="sxs-lookup"><span data-stu-id="5a82c-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="5a82c-179"><a name="MobileAppsClients"></a> Mobile Apps 用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="5a82c-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="5a82c-180">版本檢查起 hello 遵循 hello client SDK 版本所導入的**Azure 行動應用程式**:</span><span class="sxs-lookup"><span data-stu-id="5a82c-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="5a82c-181">用戶端平台</span><span class="sxs-lookup"><span data-stu-id="5a82c-181">Client platform</span></span> | <span data-ttu-id="5a82c-182">版本</span><span class="sxs-lookup"><span data-stu-id="5a82c-182">Version</span></span> | <span data-ttu-id="5a82c-183">版本標頭值</span><span class="sxs-lookup"><span data-stu-id="5a82c-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a82c-184">受管理的用戶端 (Windows、Xamarin)</span><span class="sxs-lookup"><span data-stu-id="5a82c-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="5a82c-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="5a82c-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-186">2.0.0</span></span> |
| <span data-ttu-id="5a82c-187">iOS</span><span class="sxs-lookup"><span data-stu-id="5a82c-187">iOS</span></span> |[<span data-ttu-id="5a82c-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="5a82c-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-189">2.0.0</span></span> |
| <span data-ttu-id="5a82c-190">Android</span><span class="sxs-lookup"><span data-stu-id="5a82c-190">Android</span></span> |[<span data-ttu-id="5a82c-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="5a82c-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="5a82c-193">Mobile「Apps」  伺服器 SDK</span><span class="sxs-lookup"><span data-stu-id="5a82c-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="5a82c-194">下列伺服器 SDK 版本包含版本檢查：</span><span class="sxs-lookup"><span data-stu-id="5a82c-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="5a82c-195">伺服器平台</span><span class="sxs-lookup"><span data-stu-id="5a82c-195">Server platform</span></span> | <span data-ttu-id="5a82c-196">SDK</span><span class="sxs-lookup"><span data-stu-id="5a82c-196">SDK</span></span> | <span data-ttu-id="5a82c-197">接受的版本標頭</span><span class="sxs-lookup"><span data-stu-id="5a82c-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a82c-198">.NET</span><span class="sxs-lookup"><span data-stu-id="5a82c-198">.NET</span></span> |[<span data-ttu-id="5a82c-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="5a82c-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="5a82c-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-200">2.0.0</span></span> |
| <span data-ttu-id="5a82c-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a82c-201">Node.js</span></span> |[<span data-ttu-id="5a82c-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="5a82c-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="5a82c-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5a82c-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="5a82c-204">Mobile Apps 後端的行為</span><span class="sxs-lookup"><span data-stu-id="5a82c-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="5a82c-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="5a82c-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="5a82c-206">MS_SkipVersionCheck 的值</span><span class="sxs-lookup"><span data-stu-id="5a82c-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="5a82c-207">Response</span><span class="sxs-lookup"><span data-stu-id="5a82c-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a82c-208">x.y.z 或 Null</span><span class="sxs-lookup"><span data-stu-id="5a82c-208">x.y.z or Null</span></span> |<span data-ttu-id="5a82c-209">True</span><span class="sxs-lookup"><span data-stu-id="5a82c-209">True</span></span> |<span data-ttu-id="5a82c-210">200 - 確定</span><span class="sxs-lookup"><span data-stu-id="5a82c-210">200 - OK</span></span> |
| <span data-ttu-id="5a82c-211">Null</span><span class="sxs-lookup"><span data-stu-id="5a82c-211">Null</span></span> |<span data-ttu-id="5a82c-212">False/未指定</span><span class="sxs-lookup"><span data-stu-id="5a82c-212">False/Not Specified</span></span> |<span data-ttu-id="5a82c-213">400 - 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="5a82c-213">400 - Bad Request</span></span> |
| <span data-ttu-id="5a82c-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="5a82c-214">1.x.y</span></span> |<span data-ttu-id="5a82c-215">False/未指定</span><span class="sxs-lookup"><span data-stu-id="5a82c-215">False/Not Specified</span></span> |<span data-ttu-id="5a82c-216">400 - 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="5a82c-216">400 - Bad Request</span></span> |
| <span data-ttu-id="5a82c-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="5a82c-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="5a82c-218">False/未指定</span><span class="sxs-lookup"><span data-stu-id="5a82c-218">False/Not Specified</span></span> |<span data-ttu-id="5a82c-219">200 - 確定</span><span class="sxs-lookup"><span data-stu-id="5a82c-219">200 - OK</span></span> |
| <span data-ttu-id="5a82c-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="5a82c-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="5a82c-221">False/未指定</span><span class="sxs-lookup"><span data-stu-id="5a82c-221">False/Not Specified</span></span> |<span data-ttu-id="5a82c-222">400 - 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="5a82c-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a82c-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a82c-223">Next Steps</span></span>
* <span data-ttu-id="5a82c-224">[移轉應用程式服務的行動服務 tooAzure]</span><span class="sxs-lookup"><span data-stu-id="5a82c-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[行動服務用戶端]: #MobileServicesClients
[Mobile Apps 用戶端]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[移轉應用程式服務的行動服務 tooAzure]: app-service-mobile-migrating-from-mobile-services.md
