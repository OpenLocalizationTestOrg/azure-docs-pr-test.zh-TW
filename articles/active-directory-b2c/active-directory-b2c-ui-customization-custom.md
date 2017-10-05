---
title: "使用自訂原則來自訂 UI - Azure AD B2C | Microsoft Docs"
description: "了解如何在 Azure AD B2C 中使用自訂原則時自訂使用者介面 (UI)。"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: d5a3c0a323b31696d39e3d2b36317dec3a2337d7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="3be34-103">Azure Active Directory B2C︰在自訂原則中設定 UI 自訂</span><span class="sxs-lookup"><span data-stu-id="3be34-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="3be34-104">完成本文之後，您將擁有一個具備您的品牌和外觀的註冊和登入自訂原則。</span><span class="sxs-lookup"><span data-stu-id="3be34-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="3be34-105">使用 Azure Active Directory B2C (Azure AD B2C)，幾乎可完全掌控對使用者呈現的 HTML 和 CSS 內容。</span><span class="sxs-lookup"><span data-stu-id="3be34-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span></span> <span data-ttu-id="3be34-106">使用自訂原則時，您會以 XML 設定 UI 自訂，而不是在 Azure 入口網站中使用控制項。</span><span class="sxs-lookup"><span data-stu-id="3be34-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3be34-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="3be34-107">Prerequisites</span></span>

<span data-ttu-id="3be34-108">開始之前，請完成[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="3be34-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="3be34-109">您應該有一個使用本機帳戶來註冊和登入的有效自訂原則。</span><span class="sxs-lookup"><span data-stu-id="3be34-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="3be34-110">頁面 UI 自訂</span><span class="sxs-lookup"><span data-stu-id="3be34-110">Page UI customization</span></span>

<span data-ttu-id="3be34-111">您可以使用頁面 UI 自訂功能，自訂任何自訂原則的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="3be34-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span></span> <span data-ttu-id="3be34-112">您也可以維護應用程式與 Azure AD B2C 之間的品牌和視覺一致性。</span><span class="sxs-lookup"><span data-stu-id="3be34-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="3be34-113">運作方式如下：Azure AD B2C 會在客戶的瀏覽器中執行程式碼並使用稱為[跨原始資源共用 (CORS)](http://www.w3.org/TR/cors/) 的新式方法。</span><span class="sxs-lookup"><span data-stu-id="3be34-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="3be34-114">首先，在自訂原則中使用自訂 HTML 內容指定 URL。</span><span class="sxs-lookup"><span data-stu-id="3be34-114">First, you specify a URL in the custom policy with customized HTML content.</span></span> <span data-ttu-id="3be34-115">Azure AD B2C 會合併 UI 元素與從您 URL 載入的 HTML 內容，然後對客戶顯示此頁面。</span><span class="sxs-lookup"><span data-stu-id="3be34-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="3be34-116">建立您的 HTML5 內容</span><span class="sxs-lookup"><span data-stu-id="3be34-116">Create your HTML5 content</span></span>

<span data-ttu-id="3be34-117">建立 HTML 內容並在標題中顯示您的產品品牌名稱。</span><span class="sxs-lookup"><span data-stu-id="3be34-117">Create HTML content with your product's brand name in the title.</span></span>

1. <span data-ttu-id="3be34-118">複製下列 HTML 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="3be34-118">Copy the following HTML snippet.</span></span> <span data-ttu-id="3be34-119">它是語式正確的 HTML5，在 *\<body\>* 內標籤內有一個稱為 *\<div id="api"\>\</div\>* 的空元素。</span><span class="sxs-lookup"><span data-stu-id="3be34-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span></span> <span data-ttu-id="3be34-120">這個元素指出要插入 Azure AD B2C 內容的地方。</span><span class="sxs-lookup"><span data-stu-id="3be34-120">This element indicates where Azure AD B2C content is to be inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="3be34-121">為確保安全，系統目前禁止使用 JavaScript 來進行自訂。</span><span class="sxs-lookup"><span data-stu-id="3be34-121">For security reasons, the use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="3be34-122">在文字編輯器中貼上所複製的程式碼片段，然後將檔案儲存為 customize-ui.html。</span><span class="sxs-lookup"><span data-stu-id="3be34-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="3be34-123">建立 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3be34-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="3be34-124">在本文中，我們使用 Azure Blob 儲存體來裝載內容。</span><span class="sxs-lookup"><span data-stu-id="3be34-124">In this article, we use Azure Blob storage to host our content.</span></span> <span data-ttu-id="3be34-125">您可以選擇在 Web 伺服器上裝載您的內容，但必須[在 Web 伺服器上啟用 CORS](https://enable-cors.org/server.html)。</span><span class="sxs-lookup"><span data-stu-id="3be34-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="3be34-126">若要在 Blob 儲存體中裝載此 HTML 內容，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="3be34-126">To host this HTML content in Blob storage, do the following:</span></span>

1. <span data-ttu-id="3be34-127">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3be34-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3be34-128">在 [中樞] 功能表上，選取 [新增] > [儲存體] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3be34-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="3be34-129">輸入儲存體帳戶的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="3be34-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="3be34-130">[部署模型] 可保持為 [資源管理員]。</span><span class="sxs-lookup"><span data-stu-id="3be34-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="3be34-131">將 [帳戶類型] 變更為 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="3be34-131">Change **Account Kind** to **Blob storage**.</span></span>
6. <span data-ttu-id="3be34-132">[效能] 可保持為 [標準]。</span><span class="sxs-lookup"><span data-stu-id="3be34-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="3be34-133">[複寫] 可保持為 [RA-GRS]。</span><span class="sxs-lookup"><span data-stu-id="3be34-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="3be34-134">[存取層] 可保持為 [經常性存取]。</span><span class="sxs-lookup"><span data-stu-id="3be34-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="3be34-135">[儲存體服務加密] 可保持為 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="3be34-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="3be34-136">選取儲存體帳戶的 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3be34-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="3be34-137">建立**資源群組**，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3be34-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="3be34-138">選取儲存體帳戶的 [地理位置]。</span><span class="sxs-lookup"><span data-stu-id="3be34-138">Select the **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="3be34-139">按一下 [建立]  建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3be34-139">Click **Create** to create the storage account.</span></span>  
    <span data-ttu-id="3be34-140">部署完成後，[儲存體帳戶] 刀鋒視窗會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="3be34-140">After the deployment is completed, the **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="3be34-141">建立容器</span><span class="sxs-lookup"><span data-stu-id="3be34-141">Create a container</span></span>

<span data-ttu-id="3be34-142">若要在 Blob 儲存體中建立公用容器，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="3be34-142">To create a public container in Blob storage, do the following:</span></span>

1. <span data-ttu-id="3be34-143">按一下 [概觀] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3be34-143">Click the **Overview** tab.</span></span>
2. <span data-ttu-id="3be34-144">按一下 [容器]。</span><span class="sxs-lookup"><span data-stu-id="3be34-144">Click **Container**.</span></span>
3. <span data-ttu-id="3be34-145">在 [名稱] 中，輸入 **$root**。</span><span class="sxs-lookup"><span data-stu-id="3be34-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="3be34-146">將 [存取類型] 設定為 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="3be34-146">Set **Access type** to **Blob**.</span></span>
5. <span data-ttu-id="3be34-147">按一下 **$root** 以開啟新的容器。</span><span class="sxs-lookup"><span data-stu-id="3be34-147">Click **$root** to open the new container.</span></span>
6. <span data-ttu-id="3be34-148">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="3be34-148">Click **Upload**.</span></span>
7. <span data-ttu-id="3be34-149">按一下 [選取檔案] 旁的資料夾圖示。</span><span class="sxs-lookup"><span data-stu-id="3be34-149">Click the folder icon next to **Select a file**.</span></span>
8. <span data-ttu-id="3be34-150">移至 **customize-ui.html**，這是您稍早在[頁面 UI 自訂](#the-page-ui-customization-feature)一節中建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="3be34-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="3be34-151">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="3be34-151">Click **Upload**.</span></span>
10. <span data-ttu-id="3be34-152">選取您上傳的 customize-ui.html blob。</span><span class="sxs-lookup"><span data-stu-id="3be34-152">Select the customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="3be34-153">在 **URL** 旁邊，按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="3be34-153">Next to **URL**, click **Copy**.</span></span>
12. <span data-ttu-id="3be34-154">在瀏覽器中，貼上所複製的 URL，然後移至網站。</span><span class="sxs-lookup"><span data-stu-id="3be34-154">In a browser, paste the copied URL, and go to the site.</span></span> <span data-ttu-id="3be34-155">如果無法存取此網站，請確定容器的存取類型設定為 **blob**。</span><span class="sxs-lookup"><span data-stu-id="3be34-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="3be34-156">設定 CORS</span><span class="sxs-lookup"><span data-stu-id="3be34-156">Configure CORS</span></span>

<span data-ttu-id="3be34-157">執行下列作業，針對跨原始資源共用設定 Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="3be34-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span></span>

>[!NOTE]
><span data-ttu-id="3be34-158">想要使用我們的範例 HTML 和 CSS 內容來嘗試 UI 自訂功能嗎？</span><span class="sxs-lookup"><span data-stu-id="3be34-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="3be34-159">我們已提供[簡單的協助程式工具](active-directory-b2c-reference-ui-customization-helper-tool.md)，讓您上傳我們的範例內容，並在您的 Blob 儲存體帳戶上設定。</span><span class="sxs-lookup"><span data-stu-id="3be34-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="3be34-160">如果您使用此工具，請直接跳到[修改註冊或登入自訂原則](#modify-your-sign-up-or-sign-in-custom-policy)。</span><span class="sxs-lookup"><span data-stu-id="3be34-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="3be34-161">在 [設定] 下的 [儲存體] 刀鋒視窗中，開啟 [CORS]。</span><span class="sxs-lookup"><span data-stu-id="3be34-161">On the **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="3be34-162">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3be34-162">Click **Add**.</span></span>
3. <span data-ttu-id="3be34-163">針對 [允許的來源]，輸入星號 (\*)。</span><span class="sxs-lookup"><span data-stu-id="3be34-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="3be34-164">在 [允許的動詞命令] 下拉式清單中，同時選取 **GET** 和 **OPTIONS**。</span><span class="sxs-lookup"><span data-stu-id="3be34-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="3be34-165">針對 [允許的標頭]，輸入星號 (\*)。</span><span class="sxs-lookup"><span data-stu-id="3be34-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="3be34-166">針對 [公開的標頭]，輸入星號 (\*)。</span><span class="sxs-lookup"><span data-stu-id="3be34-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="3be34-167">針對 [最長使用期限 (秒)]，輸入 **200**。</span><span class="sxs-lookup"><span data-stu-id="3be34-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="3be34-168">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3be34-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="3be34-169">測試 CORS</span><span class="sxs-lookup"><span data-stu-id="3be34-169">Test CORS</span></span>

<span data-ttu-id="3be34-170">執行下列作業來驗證您已準備就緒：</span><span class="sxs-lookup"><span data-stu-id="3be34-170">Validate that you're ready by doing the following:</span></span>

1. <span data-ttu-id="3be34-171">移至 [test-cors.org](http://test-cors.org/) 網站，然後在 [遠端 URL] 方塊中貼上 URL。</span><span class="sxs-lookup"><span data-stu-id="3be34-171">Go to the [test-cors.org](http://test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span></span>
2. <span data-ttu-id="3be34-172">按一下 [傳送要求]。</span><span class="sxs-lookup"><span data-stu-id="3be34-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="3be34-173">如果您收到錯誤，請確定您的 [CORS 設定](#configure-cors)正確無誤。</span><span class="sxs-lookup"><span data-stu-id="3be34-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="3be34-174">您也可能需要清除瀏覽器快取，或按 Ctrl+Shift+P 來開啟 InPrivate 瀏覽工作階段。</span><span class="sxs-lookup"><span data-stu-id="3be34-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="3be34-175">修改您的註冊或登入自訂原則</span><span class="sxs-lookup"><span data-stu-id="3be34-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="3be34-176">在最上層的 \<TrustFrameworkPolicy\> 標籤中，您應該會發現 \<BuildingBlocks\> 標籤。</span><span class="sxs-lookup"><span data-stu-id="3be34-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="3be34-177">在 \<BuildingBlocks\> 標籤內，藉由複製下列範例來新增 \<ContentDefinitions\> 標籤。</span><span class="sxs-lookup"><span data-stu-id="3be34-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span></span> <span data-ttu-id="3be34-178">使用您的儲存體帳戶名稱來取代 *your_storage_account*。</span><span class="sxs-lookup"><span data-stu-id="3be34-178">Replace *your_storage_account* with the name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="3be34-179">上傳更新的自訂原則</span><span class="sxs-lookup"><span data-stu-id="3be34-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="3be34-180">在 [Azure 入口網站](https://portal.azure.com)中，[切換至您的 Azure AD B2C 租用戶環境](active-directory-b2c-navigate-to-b2c-context.md)，然後開啟 [Azure AD B2C] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3be34-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="3be34-181">按一下 [所有原則]。</span><span class="sxs-lookup"><span data-stu-id="3be34-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="3be34-182">按一下 [上傳原則]。</span><span class="sxs-lookup"><span data-stu-id="3be34-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="3be34-183">上傳 `SignUpOrSignin.xml` 與您先前新增的 \<ContentDefinitions\> 標籤。</span><span class="sxs-lookup"><span data-stu-id="3be34-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="3be34-184">使用 [立即執行] 測試自訂原則</span><span class="sxs-lookup"><span data-stu-id="3be34-184">Test the custom policy by using **Run now**</span></span>

1. <span data-ttu-id="3be34-185">在 [Azure AD B2C] 刀鋒視窗上，移至 [所有原則]。</span><span class="sxs-lookup"><span data-stu-id="3be34-185">On the **Azure AD B2C** blade, go to **All polices**.</span></span>
2. <span data-ttu-id="3be34-186">選取您上傳的自訂原則，按一下 [立即執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3be34-186">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="3be34-187">您應該可以使用電子郵件地址註冊。</span><span class="sxs-lookup"><span data-stu-id="3be34-187">You should be able to sign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="3be34-188">參考</span><span class="sxs-lookup"><span data-stu-id="3be34-188">Reference</span></span>

<span data-ttu-id="3be34-189">您可以在此找到 UI 自訂的範例範本：</span><span class="sxs-lookup"><span data-stu-id="3be34-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="3be34-190">Sample_templates/wingtip 資料夾包含下列 HTML 檔案：</span><span class="sxs-lookup"><span data-stu-id="3be34-190">The sample_templates/wingtip folder contains the following HTML files:</span></span>

| <span data-ttu-id="3be34-191">HTML5 範本</span><span class="sxs-lookup"><span data-stu-id="3be34-191">HTML5 template</span></span> | <span data-ttu-id="3be34-192">說明</span><span class="sxs-lookup"><span data-stu-id="3be34-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="3be34-193">phonefactor.html</span><span class="sxs-lookup"><span data-stu-id="3be34-193">*phonefactor.html*</span></span> | <span data-ttu-id="3be34-194">使用此檔案作為多重要素驗證頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="3be34-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="3be34-195">resetpassword.html</span><span class="sxs-lookup"><span data-stu-id="3be34-195">*resetpassword.html*</span></span> | <span data-ttu-id="3be34-196">使用此檔案作為忘記密碼頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="3be34-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="3be34-197">selfasserted.html</span><span class="sxs-lookup"><span data-stu-id="3be34-197">*selfasserted.html*</span></span> | <span data-ttu-id="3be34-198">使用此檔案作為社交帳戶註冊頁面、本機帳戶註冊頁面或本機帳戶登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="3be34-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="3be34-199">unified.html</span><span class="sxs-lookup"><span data-stu-id="3be34-199">*unified.html*</span></span> | <span data-ttu-id="3be34-200">使用此檔案作為統一註冊或登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="3be34-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="3be34-201">updateprofile.html</span><span class="sxs-lookup"><span data-stu-id="3be34-201">*updateprofile.html*</span></span> | <span data-ttu-id="3be34-202">使用此檔案作為統一註冊或登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="3be34-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="3be34-203">在[修改註冊或登入自訂原則](#modify-your-sign-up-or-sign-in-custom-policy)區段中，設定 `api.idpselections` 的內容定義。</span><span class="sxs-lookup"><span data-stu-id="3be34-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span></span> <span data-ttu-id="3be34-204">Azure AD B2C 身分識別體驗架構所能辨識的一組完整內容定義識別碼，而其說明位於下表中：</span><span class="sxs-lookup"><span data-stu-id="3be34-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span></span>

| <span data-ttu-id="3be34-205">內容定義識別碼</span><span class="sxs-lookup"><span data-stu-id="3be34-205">Content definition ID</span></span> | <span data-ttu-id="3be34-206">說明</span><span class="sxs-lookup"><span data-stu-id="3be34-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="3be34-207">api.error</span><span class="sxs-lookup"><span data-stu-id="3be34-207">*api.error*</span></span> | <span data-ttu-id="3be34-208">**錯誤頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-208">**Error page**.</span></span> <span data-ttu-id="3be34-209">在發生例外狀況或錯誤時，系統會顯示此頁面。</span><span class="sxs-lookup"><span data-stu-id="3be34-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="3be34-210">api.idpselections</span><span class="sxs-lookup"><span data-stu-id="3be34-210">*api.idpselections*</span></span> | <span data-ttu-id="3be34-211">**識別提供者選取頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-211">**Identity provider selection page**.</span></span> <span data-ttu-id="3be34-212">此頁面包含使用者可以在登入期間選擇的識別提供者清單。</span><span class="sxs-lookup"><span data-stu-id="3be34-212">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="3be34-213">這些選項是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="3be34-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="3be34-214">api.idpselections.signup</span><span class="sxs-lookup"><span data-stu-id="3be34-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="3be34-215">**用於註冊的識別提供者選取**。</span><span class="sxs-lookup"><span data-stu-id="3be34-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="3be34-216">此頁面包含使用者可以在註冊期間選擇的識別提供者清單。</span><span class="sxs-lookup"><span data-stu-id="3be34-216">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="3be34-217">這些選項是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="3be34-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="3be34-218">api.localaccountpasswordreset</span><span class="sxs-lookup"><span data-stu-id="3be34-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="3be34-219">**忘記密碼頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-219">**Forgot password page**.</span></span> <span data-ttu-id="3be34-220">此頁面包含一份表單，使用者必須填妥此表單才能開始重設密碼。</span><span class="sxs-lookup"><span data-stu-id="3be34-220">This page contains a form that the user must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="3be34-221">api.localaccountsignin</span><span class="sxs-lookup"><span data-stu-id="3be34-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="3be34-222">**本機帳戶登入頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-222">**Local account sign-in page**.</span></span> <span data-ttu-id="3be34-223">此頁面包含登入表單，可供使用以電子郵件地址或使用者名稱為基礎的本機帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="3be34-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="3be34-224">此表單可以包含文字輸入方塊和密碼輸入方塊。</span><span class="sxs-lookup"><span data-stu-id="3be34-224">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="3be34-225">api.localaccountsignup</span><span class="sxs-lookup"><span data-stu-id="3be34-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="3be34-226">**本機帳戶註冊頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-226">**Local account sign-up page**.</span></span> <span data-ttu-id="3be34-227">此頁面包含登入表單，可供註冊以電子郵件地址或使用者名稱為基礎的本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="3be34-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="3be34-228">此表單可以包含各種輸入控制項，例如文字輸入方塊、密碼輸入方塊、選項按鈕、單選下拉式清單方塊和多選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3be34-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="3be34-229">api.phonefactor</span><span class="sxs-lookup"><span data-stu-id="3be34-229">*api.phonefactor*</span></span> | <span data-ttu-id="3be34-230">**Multi-Factor Authentication 頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="3be34-231">在此頁面上，使用者可以在註冊或登入期間驗證其電話號碼 (藉由使用文字或語音)。</span><span class="sxs-lookup"><span data-stu-id="3be34-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="3be34-232">api.selfasserted</span><span class="sxs-lookup"><span data-stu-id="3be34-232">*api.selfasserted*</span></span> | <span data-ttu-id="3be34-233">**社交帳戶註冊頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-233">**Social account sign-up page**.</span></span> <span data-ttu-id="3be34-234">此頁面包含使用者在使用社交識別提供者 (例如 Facebook 或 Google+) 的現有帳戶註冊時必須填妥的註冊表單。</span><span class="sxs-lookup"><span data-stu-id="3be34-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="3be34-235">此頁面類似於上述的社交帳戶註冊頁面，但密碼輸入欄位除外。</span><span class="sxs-lookup"><span data-stu-id="3be34-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="3be34-236">api.selfasserted.profileupdate</span><span class="sxs-lookup"><span data-stu-id="3be34-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="3be34-237">**設定檔更新頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-237">**Profile update page**.</span></span> <span data-ttu-id="3be34-238">此頁面包含一份表單，以供使用者用來更新其設定檔。</span><span class="sxs-lookup"><span data-stu-id="3be34-238">This page contains a form that users can use to update their profile.</span></span> <span data-ttu-id="3be34-239">此頁面類似於社交帳戶註冊頁面，但密碼輸入欄位除外。</span><span class="sxs-lookup"><span data-stu-id="3be34-239">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="3be34-240">api.signuporsignin</span><span class="sxs-lookup"><span data-stu-id="3be34-240">*api.signuporsignin*</span></span> | <span data-ttu-id="3be34-241">**統一的註冊或登入頁面**。</span><span class="sxs-lookup"><span data-stu-id="3be34-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="3be34-242">此頁面可處理使用者的註冊和登入，這些使用者可使用企業識別提供者、社交識別提供者 (例如 Facebook 或 Google+) 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="3be34-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="3be34-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3be34-243">Next steps</span></span>

<span data-ttu-id="3be34-244">如需有關可自訂之 UI 元素的其他資訊，請參閱[內建原則 UI 自訂參考指南](active-directory-b2c-reference-ui-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="3be34-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
