---
title: "Azure Active Directory B2C︰參考︰使用自訂原則來自訂使用者旅程的 UI | Microsoft Docs"
description: "Azure Active Directory B2C 自訂原則的主題"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 68f40aa638a687398512278a0b77d1ba392859cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="customize-the-ui-of-a-user-journey-with-custom-policies"></a><span data-ttu-id="e5a3c-103">使用自訂原則來自訂使用者旅程的 UI</span><span class="sxs-lookup"><span data-stu-id="e5a3c-103">Customize the UI of a user journey with Custom Policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> <span data-ttu-id="e5a3c-104">本文會進一步說明如何自訂 UI，以及如何使用身分識別體驗架構來對 B2C 自訂原則啟用 UI 自訂功能</span><span class="sxs-lookup"><span data-stu-id="e5a3c-104">This article is an advanced description of how UI customization works and how to enable with B2C Custom policies, using the Identity Experience Framework</span></span>


<span data-ttu-id="e5a3c-105">順暢的使用者體驗是任何「企業對客戶」解決方案的成功關鍵。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-105">A seamless user experience is key for any business-to-consumer solution.</span></span> <span data-ttu-id="e5a3c-106">所謂順暢的使用者體驗，不論是在裝置或瀏覽器上，都是指使用者在使用我們的服務時所經歷的旅程，和其使用客戶服務時的旅程沒有差異。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-106">By seamless user experience, we mean an experience, whether on device or browser, where a user’s journey through our service cannot be distinguished from that of the customer service they are using.</span></span>

## <a name="understand-the-cors-way-for-ui-customization"></a><span data-ttu-id="e5a3c-107">了解以 CORS 來自訂 UI 的方法</span><span class="sxs-lookup"><span data-stu-id="e5a3c-107">Understand the CORS way for UI customization</span></span>

<span data-ttu-id="e5a3c-108">Azure AD B2C 可讓您在各種頁面上自訂使用者體驗 (UX) 的外觀與風格，並可能由 Azure AD B2C 透過您的自訂原則來提供和顯示這些自訂。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-108">Azure AD B2C allows you to customize the look-and-feel of user experience (UX) on the various pages that can be potentially served and displayed by Azure AD B2C via your custom policies.</span></span>

<span data-ttu-id="e5a3c-109">為了達成該目的，Azure AD B2C 會在取用者的瀏覽器中執行程式碼，並使用現代且標準的方法 ([跨原始資源共用 (CORS)](http://www.w3.org/TR/cors/)) 來載入自訂內容，內容來源則是您在自訂原則中指定為指向 HTML5/CSS 範本的特定 URL。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-109">For that purpose, Azure AD B2C runs code in your consumer's browser and uses the modern and standard approach [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/) to load custom content from a specific URL that you specify in a custom policy to point to your HTML5/CSS templates.</span></span> <span data-ttu-id="e5a3c-110">CORS 機制可讓您從網頁上受限制資源 (如字型) 來源網域以外的其他網域，對該項資源提出要求。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-110">CORS is a mechanism that allows restricted resources, like fonts, on a web page to be requested from another domain outside the domain from which the resource originated.</span></span>

<span data-ttu-id="e5a3c-111">而在傳統的舊式方法中，範本頁面是由解決方案擁有、您只提供有限的文字和影像、版面配置與風格只提供有限的控制能力，因此會導致更多問題而難以實現順暢體驗，相較之下，CORS 方法則支援 HTML5 及 CSS，因此可讓您︰</span><span class="sxs-lookup"><span data-stu-id="e5a3c-111">Compared to the old traditional way, where template pages are owned by the solution where you provided limited text and images, where limited control of layout and feel was offered leading to more than difficulties to achieve a seamless experience, the CORS way supports HTML5 and CSS and allow you to:</span></span>

- <span data-ttu-id="e5a3c-112">裝載內容，解決方案則會使用用戶端指令碼來插入其控制項。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-112">Host the content and the solution injects its controls using client side script.</span></span>
- <span data-ttu-id="e5a3c-113">完整控制版面配置與風格的每個像素。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-113">Have full control over every pixel of layout and feel.</span></span>

<span data-ttu-id="e5a3c-114">您可以適當地製作 HTML5/CSS 檔案來提供任意數量的內容頁面。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-114">You can provide as many content pages as you like by crafting HTML5/CSS files as appropriate.</span></span>

> [!NOTE]
> <span data-ttu-id="e5a3c-115">為確保安全，系統目前禁止使用 JavaScript 來進行自訂。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-115">For security reasons, the use of JavaScript is currently blocked for customization.</span></span> <span data-ttu-id="e5a3c-116">若要將 JavaScript 的此一禁制取消，則需要為 Azure AD B2C 租用戶使用自訂的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-116">To unblock JavaScript, use of a custom domain name for your Azure AD B2C tenant is needed.</span></span>

<span data-ttu-id="e5a3c-117">在每個 HTML5/CSS 範本中，您都需要提供「錨點」元素，以便對應至 HTML 或內容頁面中所需的 `<div id=”api”>` 元素，如以下所述。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-117">In each of your HTML5/CSS templates, you provide an *anchor* element, which corresponds to the required `<div id=”api”>` element in the HTML or the content page as illustrate hereafter.</span></span> <span data-ttu-id="e5a3c-118">Azure AD B2C 要求所有內容頁面都必須有這個特定 div。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-118">Azure AD B2C requires that all content pages have this specific div.</span></span>

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

<span data-ttu-id="e5a3c-119">頁面的 Azure AD B2C 相關內容會插入這個 div 中，頁面的其餘部分則由您控制。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-119">Azure AD B2C-related content for the page will be injected into this div, while the rest of the page is yours to control.</span></span> <span data-ttu-id="e5a3c-120">Azure AD B2C 的 JavaScript 程式碼會提取您的內容，並將我們的 HTML 插入到這個特定的 div 元素。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-120">The Azure AD B2C’s JavaScript code pulls in your content and injects our HTML into this specific div element.</span></span> <span data-ttu-id="e5a3c-121">Azure AD B2C 會適當插入下列控制項︰帳戶選擇器控制項、登入控制項、多因素 (目前為電話式) 控制項和屬性集合控制項。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-121">Azure AD B2C injects the following controls as appropriate: account chooser control, login controls, multi-factor (currently phone-based) controls, and attribute collection controls.</span></span> <span data-ttu-id="e5a3c-122">Azure AD B2C 可確保所有控制項都符合 HTML5 規範且可供存取、所有控制項都可完全自訂樣式，且控制項版本不會倒退。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-122">Azure AD B2C ensures that all the controls are HTML5 compliant and accessible, all the controls can be fully styled, and that a control version will not regress.</span></span>

<span data-ttu-id="e5a3c-123">合併的內容最終會以動態文件的形式向取用者顯示。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-123">The merged content is eventually displayed as the dynamic document to your consumer.</span></span>

<span data-ttu-id="e5a3c-124">若要確保上述各項正常運作，您必須︰</span><span class="sxs-lookup"><span data-stu-id="e5a3c-124">To ensure of the above works as expected, you must:</span></span>

- <span data-ttu-id="e5a3c-125">確保內容符合 HTML5 規範且可供存取</span><span class="sxs-lookup"><span data-stu-id="e5a3c-125">Ensure your content is HTML5 compliant and accessible</span></span>
- <span data-ttu-id="e5a3c-126">確保內容伺服器已啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-126">Ensure your content server is enabled for CORS.</span></span>
- <span data-ttu-id="e5a3c-127">透過 HTTPS 提供內容。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-127">Serve content over HTTPS.</span></span>
- <span data-ttu-id="e5a3c-128">對所有連結和 CSS 內容使用絕對 URL，例如 https://yourdomain/content。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-128">Use absolute URLS such as https://yourdomain/content for all links and CSS content.</span></span>

> [!TIP]
> <span data-ttu-id="e5a3c-129">若要確認您要用來裝載內容的網站已啟用 CORS 並測試 CORS 要求，您可以使用 http://test-cors.org/ 網站。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-129">To verify that the site you are hosting your content on has CORS enabled and test CORS requests, you can use the site http://test-cors.org/.</span></span> <span data-ttu-id="e5a3c-130">由於有此網站，您可以直接將 CORS 要求傳送到遠端伺服器 (以進行測試，前提是該伺服器支援 CORS)，或將 CORS 要求傳送至測試伺服器 (以瀏覽 CORS 的某些功能)。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-130">Thanks to this site, you can simply either send the CORS request to a remote server (to test if CORS is supported), or send the CORS request to a test server (to explore certain features of CORS).</span></span>

> [!TIP]
> <span data-ttu-id="e5a3c-131">http://enable-cors.org/ 網站也會在 CORS 上構成更有用的資源。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-131">The site http://enable-cors.org/ also constitutes a more than useful resources on CORS.</span></span>

<span data-ttu-id="e5a3c-132">由於有此 CORS 式方法，使用者之後會在您的應用程式與 Azure AD B2C 所提供的頁面之間獲得一致的體驗。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-132">Thanks to this CORS-based approach, the end users will then have consistent experiences between your application and the pages served by Azure AD B2C.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="e5a3c-133">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e5a3c-133">Create a storage account</span></span>

<span data-ttu-id="e5a3c-134">先決條件是，您必須建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-134">As a prerequisite, you need to create a storage account.</span></span> <span data-ttu-id="e5a3c-135">您需要有  Azure 訂用帳戶才能建立 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-135">You will need an Azure subscription to create an Azure Blob Storage account.</span></span> <span data-ttu-id="e5a3c-136">您可以在 [Azure 網站](https://azure.microsoft.com/en-us/pricing/free-trial/)上註冊免費試用版。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-136">You can sign up a free trial at the [Azure website](https://azure.microsoft.com/en-us/pricing/free-trial/).</span></span>

1. <span data-ttu-id="e5a3c-137">開啟瀏覽工作階段並瀏覽至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-137">Open a browsing session and navigate to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e5a3c-138">使用您的系統管理認證來登入。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-138">Sign in with your administrative credentials.</span></span>
3. <span data-ttu-id="e5a3c-139">按一下 [新增] > [資料 + 儲存體] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-139">Click **New** > **Data + Storage** > **Storage account**.</span></span>  <span data-ttu-id="e5a3c-140">此時會開啟 [建立儲存體帳戶] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-140">A **Create storage account** blade opens up.</span></span>
4. <span data-ttu-id="e5a3c-141">在 [名稱] 中，提供儲存體帳戶的名稱，例如 contoso369b2c。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-141">In **Name**, provide a name for the storage account, for example, *contoso369b2c*.</span></span> <span data-ttu-id="e5a3c-142">此值稍後會指稱為 storageAccountName。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-142">This value will be later referred as to *storageAccountName*.</span></span>
5. <span data-ttu-id="e5a3c-143">選擇適當的定價層、資源群組和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-143">Pick the appropriate selections for the pricing tier, the resource group and the subscription.</span></span> <span data-ttu-id="e5a3c-144">確定您已核取 [釘選到「開始面板」]  選項。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-144">Make sure that you have the **Pin to Startboard** option checked.</span></span> <span data-ttu-id="e5a3c-145">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-145">Click **Create**.</span></span>
6. <span data-ttu-id="e5a3c-146">回到「開始面板」，然後按一下您剛建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-146">Go back to the Startboard and click the storage account that you just created.</span></span>
7. <span data-ttu-id="e5a3c-147">在 [服務] 區段中，按一下 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-147">In the **Services** section, click **Blobs**.</span></span> <span data-ttu-id="e5a3c-148">[Blob 服務] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-148">A **Blob service blade** opens up.</span></span>
8. <span data-ttu-id="e5a3c-149">按一下 [+容器]。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-149">Click **+ Container**.</span></span>
9. <span data-ttu-id="e5a3c-150">在 [名稱] 中提供容器的名稱，例如 b2c。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-150">In **Name**, provide a name for the container, for example, *b2c*.</span></span> <span data-ttu-id="e5a3c-151">此值稍後會指稱為 containerName。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-151">This value will be later referred to as *containerName*.</span></span>
9. <span data-ttu-id="e5a3c-152">選取 [Blob] 來作為 [存取類型]。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-152">Select **Blob** as the **Access type**.</span></span> <span data-ttu-id="e5a3c-153">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-153">Click **Create**.</span></span>
10. <span data-ttu-id="e5a3c-154">您建立的容器將會出現在 [Blob 服務] 刀鋒視窗的清單中。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-154">The container that you created will appear in the list on the **Blob service blade**.</span></span>
11. <span data-ttu-id="e5a3c-155">關閉 [Blob]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-155">Close the **Blobs** blade.</span></span>
12. <span data-ttu-id="e5a3c-156">在 [儲存體帳戶] 刀鋒視窗上，按一下 [金鑰] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-156">On the **storage account blade**, click the **Key** icon.</span></span> <span data-ttu-id="e5a3c-157">[存取金鑰] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-157">An **Access keys blade** opens up.</span></span>  
13. <span data-ttu-id="e5a3c-158">記下 **key1** 的值。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-158">Write down the value of **key1**.</span></span> <span data-ttu-id="e5a3c-159">此值稍後會指稱為 key1。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-159">This value will be later referred as *key1*.</span></span>

## <a name="downloading-the-helper-tool"></a><span data-ttu-id="e5a3c-160">下載協助程式工具</span><span class="sxs-lookup"><span data-stu-id="e5a3c-160">Downloading the helper tool</span></span>

1.  <span data-ttu-id="e5a3c-161">從 [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) 下載協助程式工具。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-161">Download the helper tool from [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).</span></span>
2.  <span data-ttu-id="e5a3c-162">將 B2C-AzureBlobStorage-Client-master.zip 檔案儲存在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-162">Save the *B2C-AzureBlobStorage-Client-master.zip* file on your local machine.</span></span>
3.  <span data-ttu-id="e5a3c-163">在本機磁碟上解壓縮 B2C-AzureBlobStorage-Client-master.zip 檔案的內容，例如在 **UI-Customization-Pack** 資料夾下解壓縮。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-163">Extract the content of the B2C-AzureBlobStorage-Client-master.zip file on your local disk, for example under the **UI-Customization-Pack** folder.</span></span> <span data-ttu-id="e5a3c-164">這會在其底下建立 B2C-AzureBlobStorage-Client-master 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-164">This will create a *B2C-AzureBlobStorage-Client-master* folder underneath.</span></span>
4.  <span data-ttu-id="e5a3c-165">開啟該資料夾，並在其中解壓縮 B2CAzureStorageClient.zip 封存檔的內容。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-165">Open that folder and extract the content of the archive file *B2CAzureStorageClient.zip* within it.</span></span>

## <a name="upload-the-ui-customization-pack-sample-files"></a><span data-ttu-id="e5a3c-166">上傳 UI-Customization-Pack 範例檔</span><span class="sxs-lookup"><span data-stu-id="e5a3c-166">Upload the UI-Customization-Pack sample files</span></span>

1.  <span data-ttu-id="e5a3c-167">使用 Windows 檔案總管，瀏覽至上一節所建立之 UI-Customization-Pack 資料夾底下的 B2C-AzureBlobStorage-Client-master 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-167">Using Windows Explorer, navigate to the folder *B2C-AzureBlobStorage-Client-master* located under the *UI-Customization-Pack* folder created in the previous section.</span></span>
2.  <span data-ttu-id="e5a3c-168">執行 B2CAzureStorageClient.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-168">Run the *B2CAzureStorageClient.exe* file.</span></span> <span data-ttu-id="e5a3c-169">這個程式只會將您指定目錄中的所有檔案上傳至您的儲存體帳戶，並允許 CORS 存取這些檔案。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-169">This program will simply upload all the files in the directory that you specify to your storage account, and enable CORS access for those files.</span></span>
3.  <span data-ttu-id="e5a3c-170">請在提示出現時指定︰a.</span><span class="sxs-lookup"><span data-stu-id="e5a3c-170">When prompted, specify: a.</span></span>  <span data-ttu-id="e5a3c-171">您儲存體帳戶 storageAccountName 的名稱，例如 contoso369b2c。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-171">The name of your storage account, *storageAccountName*, for example *contoso369b2c*.</span></span>
    <span data-ttu-id="e5a3c-172">b.</span><span class="sxs-lookup"><span data-stu-id="e5a3c-172">b.</span></span>  <span data-ttu-id="e5a3c-173">您的 Azure Blob 儲存體 key1 的主要存取金鑰，例如 contoso369b2c。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-173">The primary access key of your azure blob storage, *key1*, for example *contoso369b2c*.</span></span>
    <span data-ttu-id="e5a3c-174">c.</span><span class="sxs-lookup"><span data-stu-id="e5a3c-174">c.</span></span>  <span data-ttu-id="e5a3c-175">您的儲存體 Blob 儲存體容器 containerName 的名稱，例如 b2c。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-175">The name of your storage blob storage container, *containerName*, for example *b2c*.</span></span>
    <span data-ttu-id="e5a3c-176">d.</span><span class="sxs-lookup"><span data-stu-id="e5a3c-176">d.</span></span>  <span data-ttu-id="e5a3c-177">Starter-Pack 範例檔的路徑，例如 ..\B2CTemplates\wingtiptoys。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-177">The path of the *Starter-Pack* sample files, for example *..\B2CTemplates\wingtiptoys*.</span></span>

<span data-ttu-id="e5a3c-178">如果您遵循上述步驟，虛構公司 **wingtiptoys** 之 UI-Customization-Pack 的 HTML5 和 CSS 檔案現在會指向您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-178">If you followed the steps above, the HTML5 and CSS files of the *UI-Customization-Pack* for the fictitious company **wingtiptoys** will now be pointing to your storage account.</span></span>  <span data-ttu-id="e5a3c-179">您可以在 Azure 入口網站中開啟相關的容器刀鋒視窗，以確認該內容已正確上傳。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-179">You can verify that the content has been uploaded correctly by opening the related container blade in the Azure portal.</span></span> <span data-ttu-id="e5a3c-180">或者，您也可以從瀏覽器存取頁面來確認該內容已正確上傳。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-180">You can alternatively verify that the content has been uploaded correctly by accessing the page from a browser.</span></span> <span data-ttu-id="e5a3c-181">如需詳細資訊，請參閱 [Azure Active Directory B2C︰用來示範頁面使用者介面 (UI) 自訂功能的協助程式工具](active-directory-b2c-reference-ui-customization-helper-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-181">For more information, see [Azure Active Directory B2C: A helper tool used to demonstrate the page user interface (UI) customization feature](active-directory-b2c-reference-ui-customization-helper-tool.md).</span></span>

## <a name="ensure-the-storage-account-has-cors-enabled"></a><span data-ttu-id="e5a3c-182">確定儲存體帳戶已啟用 CORS</span><span class="sxs-lookup"><span data-stu-id="e5a3c-182">Ensure the storage account has CORS enabled</span></span>

<span data-ttu-id="e5a3c-183">您的端點必須啟用 CORS (跨原始資源共用)，Azure AD B2C 進階版才能載入您的內容。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-183">CORS (Cross-Origin Resource Sharing) must be enabled on your endpoint for Azure AD B2C Premium to load your content.</span></span> <span data-ttu-id="e5a3c-184">這是因為您的內容裝載所在的網域，與 Azure AD B2C 進階版用來從中提供頁面的網域不同。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-184">This is because your content is hosted on a different domain than the domain Azure AD B2C Premium will be serving the page from.</span></span>

<span data-ttu-id="e5a3c-185">若要確認您要用來裝載內容的儲存體已啟用 CORS，請進行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="e5a3c-185">To verify that the storage you are hosting your content on has CORS enabled, proceed with the following steps:</span></span>

1. <span data-ttu-id="e5a3c-186">開啟瀏覽工作階段，並使用 unified.html 頁面在儲存體帳戶中所在位置的完整 URL `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html` 來瀏覽至該頁面。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-186">Open a browsing session and navigate to the page *unified.html* using the full URL of its location in your storage account, `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`.</span></span> <span data-ttu-id="e5a3c-187">例如，https://contoso369b2c.blob.core.windows.net/b2c/unified.html。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-187">For example, https://contoso369b2c.blob.core.windows.net/b2c/unified.html.</span></span>
2. <span data-ttu-id="e5a3c-188">瀏覽至 http://test-cors.org。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-188">Navigate to http://test-cors.org.</span></span> <span data-ttu-id="e5a3c-189">這個網站可讓您確認您要使用的頁面已啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-189">This site allows you to verify that the page you are using has CORS enabled.</span></span>  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. <span data-ttu-id="e5a3c-190">在 [遠端 URL] 中，輸入 unified.html 內容的完整 URL，然後按一下 [傳送要求]。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-190">In **Remote URL**, enter the full URL for your unified.html content, and click **Send Request**.</span></span>
4. <span data-ttu-id="e5a3c-191">確認 [結果] 區段中的輸出包含「XHR status: 200」。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-191">Verify that the output in the **Results** section contains *XHR status: 200*.</span></span> <span data-ttu-id="e5a3c-192">這表示 CORS 已啟用。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-192">This indicates that CORS is enabled.</span></span>
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
<span data-ttu-id="e5a3c-193">儲存體帳戶現在應該包含我們的示例中名為 b2c 的 Blob 容器，其中並包含下列來自 Starter-Pack 的 wingtiptoys 範本。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-193">The storage account should now contain a blob container named *b2c* in our illustration that contains the following wingtiptoys templates from the *Starter-Pack*.</span></span>

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

<span data-ttu-id="e5a3c-194">下表說明上述 HTML5 網頁的目的。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-194">The following table describes the purpose of the above HTML5 pages.</span></span>

| <span data-ttu-id="e5a3c-195">HTML5 範本</span><span class="sxs-lookup"><span data-stu-id="e5a3c-195">HTML5 template</span></span> | <span data-ttu-id="e5a3c-196">說明</span><span class="sxs-lookup"><span data-stu-id="e5a3c-196">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="e5a3c-197">phonefactor.html</span><span class="sxs-lookup"><span data-stu-id="e5a3c-197">*phonefactor.html*</span></span> | <span data-ttu-id="e5a3c-198">此頁面可作為 Multi-Factor Authentication 頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-198">This page can be used as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="e5a3c-199">resetpassword.html</span><span class="sxs-lookup"><span data-stu-id="e5a3c-199">*resetpassword.html*</span></span> | <span data-ttu-id="e5a3c-200">此頁面可作為忘記密碼頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-200">This page can be used as a template for a forgot password page.</span></span> |
| <span data-ttu-id="e5a3c-201">selfasserted.html</span><span class="sxs-lookup"><span data-stu-id="e5a3c-201">*selfasserted.html*</span></span> | <span data-ttu-id="e5a3c-202">此頁面可作為社交帳戶註冊頁面、本機帳戶註冊頁面或本機帳戶登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-202">This page can be used as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="e5a3c-203">unified.html</span><span class="sxs-lookup"><span data-stu-id="e5a3c-203">*unified.html*</span></span> | <span data-ttu-id="e5a3c-204">此頁面可作為統一之註冊或登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-204">This page can be used as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="e5a3c-205">updateprofile.html</span><span class="sxs-lookup"><span data-stu-id="e5a3c-205">*updateprofile.html*</span></span> | <span data-ttu-id="e5a3c-206">此頁面可作為設定檔更新頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-206">This page can be used as a template for a profile update page.</span></span> |

## <a name="add-a-link-to-your-html5css-templates-to-your-user-journey"></a><span data-ttu-id="e5a3c-207">將 HTML5/CSS 範本的連結新增至使用者旅程</span><span class="sxs-lookup"><span data-stu-id="e5a3c-207">Add a link to your HTML5/CSS templates to your user journey</span></span>

<span data-ttu-id="e5a3c-208">您可以藉由直接編輯自訂原則，將 HTML5/CSS 範本的連結新增至使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-208">You can add a link to your HTML5/CSS templates to your user journey by editing a custom policy directly.</span></span>

<span data-ttu-id="e5a3c-209">要在使用者旅程中使用的自訂 HTML5/CSS 範本，必須在可用於這些使用者旅程的內容定義清單加以指定。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-209">The custom HTML5/CSS templates to use in your user journey have to be specified in a list of content definitions that can be used in those user journeys.</span></span> <span data-ttu-id="e5a3c-210">為此，您必須在自訂原則 XML 檔的 <BuildingBlocks> 區段下，宣告選擇性的 <ContentDefinitions> XML 元素。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-210">For that purpose, an optional *<ContentDefinitions>* XML element must be declared under the *<BuildingBlocks>* section of your custom policy XML file.</span></span>

<span data-ttu-id="e5a3c-211">下表說明 Azure AD B2C 身分識別體驗引擎所能辨識之內容定義識別碼的集合，以及與這些識別碼有關的頁面類型。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-211">The following table describes the set of content definition ids recognized by the Azure AD B2C identity experience engine and the type of pages that relates to them.</span></span>

| <span data-ttu-id="e5a3c-212">內容定義識別碼</span><span class="sxs-lookup"><span data-stu-id="e5a3c-212">Content definition id</span></span> | <span data-ttu-id="e5a3c-213">說明</span><span class="sxs-lookup"><span data-stu-id="e5a3c-213">Description</span></span> |
|-----------------------|-------------|
| <span data-ttu-id="e5a3c-214">api.error</span><span class="sxs-lookup"><span data-stu-id="e5a3c-214">*api.error*</span></span> | <span data-ttu-id="e5a3c-215">**錯誤頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-215">**Error page**.</span></span> <span data-ttu-id="e5a3c-216">在發生例外狀況或錯誤時，系統會顯示此頁面。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-216">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="e5a3c-217">api.idpselections</span><span class="sxs-lookup"><span data-stu-id="e5a3c-217">*api.idpselections*</span></span> | <span data-ttu-id="e5a3c-218">**識別提供者選取頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-218">**Identity provider selection page**.</span></span> <span data-ttu-id="e5a3c-219">此頁面包含使用者可以在登入期間選擇的識別提供者清單。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-219">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="e5a3c-220">這些提供者是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶 (以電子郵件地址或使用者名稱為基礎)。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-220">These are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span> |
| <span data-ttu-id="e5a3c-221">api.idpselections.signup</span><span class="sxs-lookup"><span data-stu-id="e5a3c-221">*api.idpselections.signup*</span></span> | <span data-ttu-id="e5a3c-222">**用於註冊的識別提供者選取**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-222">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="e5a3c-223">此頁面包含使用者可以在註冊期間選擇的識別提供者清單。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-223">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="e5a3c-224">這些提供者是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶 (以電子郵件地址或使用者名稱為基礎)。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-224">These are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span> |
| <span data-ttu-id="e5a3c-225">api.localaccountpasswordreset</span><span class="sxs-lookup"><span data-stu-id="e5a3c-225">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="e5a3c-226">**忘記密碼頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-226">**Forgot password page**.</span></span> <span data-ttu-id="e5a3c-227">此頁面包含表單，使用者必須填寫此表單才能重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-227">This page contains a form that the user has to fill to initiate their password reset.</span></span>  |
| <span data-ttu-id="e5a3c-228">api.localaccountsignin</span><span class="sxs-lookup"><span data-stu-id="e5a3c-228">*api.localaccountsignin*</span></span> | <span data-ttu-id="e5a3c-229">**本機帳戶登入頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-229">**Local account sign-in page**.</span></span> <span data-ttu-id="e5a3c-230">此頁面包含登入表單，使用者必須填寫此表單才能使用以電子郵件地址或使用者名稱為基礎的本機帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-230">This page contains a sign-in form that the user has to fill in when signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="e5a3c-231">此表單可以包含文字輸入方塊和密碼輸入方塊。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-231">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="e5a3c-232">api.localaccountsignup</span><span class="sxs-lookup"><span data-stu-id="e5a3c-232">*api.localaccountsignup*</span></span> | <span data-ttu-id="e5a3c-233">**本機帳戶註冊頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-233">**Local account sign-up page**.</span></span> <span data-ttu-id="e5a3c-234">此頁面包含使用者在使用以電子郵件地址或使用者名稱為基礎的本機帳戶註冊時所需填寫的註冊表單。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-234">This page contains a sign-up form that the user has to fill in when signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="e5a3c-235">此表單可以包含不同的輸入控制項，例如文字輸入方塊、密碼輸入方塊、選項按鈕、單選下拉式清單方塊和多選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-235">The form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="e5a3c-236">api.phonefactor</span><span class="sxs-lookup"><span data-stu-id="e5a3c-236">*api.phonefactor*</span></span> | <span data-ttu-id="e5a3c-237">**Multi-Factor Authentication 頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-237">**Multi-factor authentication page**.</span></span> <span data-ttu-id="e5a3c-238">在此頁面上，使用者可以在註冊或登入期間驗證其電話號碼 (使用文字或語音)。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-238">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="e5a3c-239">api.selfasserted</span><span class="sxs-lookup"><span data-stu-id="e5a3c-239">*api.selfasserted*</span></span> | <span data-ttu-id="e5a3c-240">**社交帳戶註冊頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-240">**Social account sign-up page**.</span></span> <span data-ttu-id="e5a3c-241">此頁面包含使用者在使用社交識別提供者 (例如 Facebook 或 Google+) 的現有帳戶註冊時所需填寫的註冊表單。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-241">This page contains a sign-up form that the user has to fill in when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="e5a3c-242">此頁面類似於上述的社交帳戶註冊頁面，但密碼輸入欄位除外。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-242">This page is similar to the above social account sign-up page with the exception of the password entry fields.</span></span> |
| <span data-ttu-id="e5a3c-243">api.selfasserted.profileupdate</span><span class="sxs-lookup"><span data-stu-id="e5a3c-243">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="e5a3c-244">**設定檔更新頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-244">**Profile update page**.</span></span> <span data-ttu-id="e5a3c-245">此頁面包含表單，以供使用者用來更新其設定檔。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-245">This page contains a form that the user can use to update their profile.</span></span> <span data-ttu-id="e5a3c-246">此頁面類似於上述的社交帳戶註冊頁面，但密碼輸入欄位除外。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-246">This page is similar to the above social account sign-up page with the exception of the password entry fields.</span></span> |
| <span data-ttu-id="e5a3c-247">api.signuporsignin</span><span class="sxs-lookup"><span data-stu-id="e5a3c-247">*api.signuporsignin*</span></span> | <span data-ttu-id="e5a3c-248">**統一的註冊或登入頁面**。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-248">**Unified sign-up or sign-in page**.</span></span>  <span data-ttu-id="e5a3c-249">此頁面可處理使用者的註冊和登入，這些使用者可使用企業識別提供者、社交識別提供者 (例如 Facebook 或 Google+) 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5a3c-249">This page handles both sign-up & sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5a3c-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5a3c-250">Next steps</span></span>
[<span data-ttu-id="e5a3c-251">參考︰了解自訂原則如何在 B2C 中使用身分識別體驗架構</span><span class="sxs-lookup"><span data-stu-id="e5a3c-251">Reference: Understand how custom policies work with the Identity Experience Framework in B2C</span></span>](active-directory-b2c-reference-custom-policies-understanding-contents.md)