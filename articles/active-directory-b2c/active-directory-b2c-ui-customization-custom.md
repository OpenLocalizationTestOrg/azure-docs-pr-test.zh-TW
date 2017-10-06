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
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="436dd-103">Azure Active Directory B2C︰在自訂原則中設定 UI 自訂</span><span class="sxs-lookup"><span data-stu-id="436dd-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="436dd-104">完成本文之後，您將擁有一個具備您的品牌和外觀的註冊和登入自訂原則。</span><span class="sxs-lookup"><span data-stu-id="436dd-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="436dd-105">使用 Azure Active Directory B2C (Azure AD B2C)，您會得到幾乎已滿控制 hello HTML 和 CSS 內容，顯示 toousers。</span><span class="sxs-lookup"><span data-stu-id="436dd-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of hello HTML and CSS content that's presented toousers.</span></span> <span data-ttu-id="436dd-106">當您使用自訂原則時，您設定自訂 UI XML 中而不是使用 hello Azure 入口網站中的控制項。</span><span class="sxs-lookup"><span data-stu-id="436dd-106">When you use a custom policy, you configure UI customization in XML instead of using controls in hello Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="436dd-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="436dd-107">Prerequisites</span></span>

<span data-ttu-id="436dd-108">開始之前，請完成[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="436dd-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="436dd-109">您應該有一個使用本機帳戶來註冊和登入的有效自訂原則。</span><span class="sxs-lookup"><span data-stu-id="436dd-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="436dd-110">頁面 UI 自訂</span><span class="sxs-lookup"><span data-stu-id="436dd-110">Page UI customization</span></span>

<span data-ttu-id="436dd-111">使用 hello 頁面 UI 自訂功能，您可以自訂 hello 外觀及操作的任何自訂的原則。</span><span class="sxs-lookup"><span data-stu-id="436dd-111">By using hello page UI customization feature, you can customize hello look and feel of any custom policy.</span></span> <span data-ttu-id="436dd-112">您也可以維護應用程式與 Azure AD B2C 之間的品牌和視覺一致性。</span><span class="sxs-lookup"><span data-stu-id="436dd-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="436dd-113">運作方式如下：Azure AD B2C 會在客戶的瀏覽器中執行程式碼並使用稱為[跨原始資源共用 (CORS)](http://www.w3.org/TR/cors/) 的新式方法。</span><span class="sxs-lookup"><span data-stu-id="436dd-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="436dd-114">首先，使用自訂 HTML 內容的 hello 自訂原則中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="436dd-114">First, you specify a URL in hello custom policy with customized HTML content.</span></span> <span data-ttu-id="436dd-115">Azure AD B2C 合併以 hello HTML 內容，是從您的 URL 載入然後顯示 hello 頁面 toohello 客戶的 UI 項目。</span><span class="sxs-lookup"><span data-stu-id="436dd-115">Azure AD B2C merges UI elements with hello HTML content that's loaded from your URL and then displays hello page toohello customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="436dd-116">建立您的 HTML5 內容</span><span class="sxs-lookup"><span data-stu-id="436dd-116">Create your HTML5 content</span></span>

<span data-ttu-id="436dd-117">建立 hello 標題中的 HTML 內容與您的產品品牌名稱。</span><span class="sxs-lookup"><span data-stu-id="436dd-117">Create HTML content with your product's brand name in hello title.</span></span>

1. <span data-ttu-id="436dd-118">複製下列 HTML 程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="436dd-118">Copy hello following HTML snippet.</span></span> <span data-ttu-id="436dd-119">它是語式正確空項目與 HTML5 呼叫* \<d i v id ="api 」\>\</div\> *位於 hello *\<主體\>*標記。</span><span class="sxs-lookup"><span data-stu-id="436dd-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within hello *\<body\>* tags.</span></span> <span data-ttu-id="436dd-120">此元素表示 Azure AD B2C 內容所在 toobe 插入。</span><span class="sxs-lookup"><span data-stu-id="436dd-120">This element indicates where Azure AD B2C content is toobe inserted.</span></span>

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
   ><span data-ttu-id="436dd-121">基於安全性理由，JavaScript hello 使用目前被封鎖進行自訂。</span><span class="sxs-lookup"><span data-stu-id="436dd-121">For security reasons, hello use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="436dd-122">在文字編輯器中，貼 hello 複製程式碼片段，然後再將 hello 檔案儲存為*自訂 ui.html*。</span><span class="sxs-lookup"><span data-stu-id="436dd-122">Paste hello copied snippet in a text editor, and then save hello file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="436dd-123">建立 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="436dd-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="436dd-124">在本文中，我們使用 Azure Blob 儲存體 toohost 我們的內容。</span><span class="sxs-lookup"><span data-stu-id="436dd-124">In this article, we use Azure Blob storage toohost our content.</span></span> <span data-ttu-id="436dd-125">您可以選擇 toohost web 伺服器上，您的內容，但您必須[web 伺服器上啟用 CORS](https://enable-cors.org/server.html)。</span><span class="sxs-lookup"><span data-stu-id="436dd-125">You can choose toohost your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="436dd-126">toohost 此 HTML 內容，在 Blob 儲存體，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="436dd-126">toohost this HTML content in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="436dd-127">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="436dd-127">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="436dd-128">在 [hello**中樞**功能表上，選取**新增** > **儲存體** > **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="436dd-128">On hello **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="436dd-129">輸入儲存體帳戶的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="436dd-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="436dd-130">[部署模型] 可保持為 [資源管理員]。</span><span class="sxs-lookup"><span data-stu-id="436dd-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="436dd-131">變更**帳戶種類**太**Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="436dd-131">Change **Account Kind** too**Blob storage**.</span></span>
6. <span data-ttu-id="436dd-132">[效能] 可保持為 [標準]。</span><span class="sxs-lookup"><span data-stu-id="436dd-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="436dd-133">[複寫] 可保持為 [RA-GRS]。</span><span class="sxs-lookup"><span data-stu-id="436dd-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="436dd-134">[存取層] 可保持為 [經常性存取]。</span><span class="sxs-lookup"><span data-stu-id="436dd-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="436dd-135">[儲存體服務加密] 可保持為 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="436dd-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="436dd-136">選取儲存體帳戶的 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="436dd-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="436dd-137">建立**資源群組**，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="436dd-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="436dd-138">選取 hello**地理位置**儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="436dd-138">Select hello **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="436dd-139">按一下**建立**toocreate hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="436dd-139">Click **Create** toocreate hello storage account.</span></span>  
    <span data-ttu-id="436dd-140">Hello 部署完成之後，hello**儲存體帳戶**刀鋒視窗會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="436dd-140">After hello deployment is completed, hello **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="436dd-141">建立容器</span><span class="sxs-lookup"><span data-stu-id="436dd-141">Create a container</span></span>

<span data-ttu-id="436dd-142">toocreate 公用容器中 Blob 儲存體，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="436dd-142">toocreate a public container in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="436dd-143">按一下 hello**概觀**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="436dd-143">Click hello **Overview** tab.</span></span>
2. <span data-ttu-id="436dd-144">按一下 [容器]。</span><span class="sxs-lookup"><span data-stu-id="436dd-144">Click **Container**.</span></span>
3. <span data-ttu-id="436dd-145">在 [名稱] 中，輸入 **$root**。</span><span class="sxs-lookup"><span data-stu-id="436dd-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="436dd-146">設定**存取類型**太**Blob**。</span><span class="sxs-lookup"><span data-stu-id="436dd-146">Set **Access type** too**Blob**.</span></span>
5. <span data-ttu-id="436dd-147">按一下**$root** tooopen hello 新容器。</span><span class="sxs-lookup"><span data-stu-id="436dd-147">Click **$root** tooopen hello new container.</span></span>
6. <span data-ttu-id="436dd-148">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="436dd-148">Click **Upload**.</span></span>
7. <span data-ttu-id="436dd-149">按一下資料夾圖示，hello 下一步太**選取檔案**。</span><span class="sxs-lookup"><span data-stu-id="436dd-149">Click hello folder icon next too**Select a file**.</span></span>
8. <span data-ttu-id="436dd-150">跳過**自訂 ui.html**，這您先前在 hello[自訂分頁 UI](#the-page-ui-customization-feature) > 一節。</span><span class="sxs-lookup"><span data-stu-id="436dd-150">Go too**customize-ui.html**, which you created earlier in hello [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="436dd-151">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="436dd-151">Click **Upload**.</span></span>
10. <span data-ttu-id="436dd-152">選取您上傳的 hello 自訂 ui.html blob。</span><span class="sxs-lookup"><span data-stu-id="436dd-152">Select hello customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="436dd-153">下一步太**URL**，按一下 [**複製**。</span><span class="sxs-lookup"><span data-stu-id="436dd-153">Next too**URL**, click **Copy**.</span></span>
12. <span data-ttu-id="436dd-154">在瀏覽器中，貼上 hello 複製 URL，並移 toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="436dd-154">In a browser, paste hello copied URL, and go toohello site.</span></span> <span data-ttu-id="436dd-155">如果無法存取 hello 站台，請確定 hello 容器存取類型會設定太**blob**。</span><span class="sxs-lookup"><span data-stu-id="436dd-155">If hello site is inaccessible, make sure hello container access type is set too**blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="436dd-156">設定 CORS</span><span class="sxs-lookup"><span data-stu-id="436dd-156">Configure CORS</span></span>

<span data-ttu-id="436dd-157">設定跨原始資源共用的 Blob 儲存體，藉由 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="436dd-157">Configure Blob storage for Cross-Origin Resource Sharing by doing hello following:</span></span>

>[!NOTE]
><span data-ttu-id="436dd-158">使用我們的範例 HTML 和 CSS 內容想 tootry 出 hello UI 自訂功能？</span><span class="sxs-lookup"><span data-stu-id="436dd-158">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="436dd-159">我們已提供[簡單的協助程式工具](active-directory-b2c-reference-ui-customization-helper-tool.md)，讓您上傳我們的範例內容，並在您的 Blob 儲存體帳戶上設定。</span><span class="sxs-lookup"><span data-stu-id="436dd-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="436dd-160">如果您使用 hello 工具，跳過[修改註冊或登入自訂原則](#modify-your-sign-up-or-sign-in-custom-policy)。</span><span class="sxs-lookup"><span data-stu-id="436dd-160">If you use hello tool, skip ahead too[Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="436dd-161">在 hello**儲存體**刀鋒視窗底下**設定**，開啟**CORS**。</span><span class="sxs-lookup"><span data-stu-id="436dd-161">On hello **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="436dd-162">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="436dd-162">Click **Add**.</span></span>
3. <span data-ttu-id="436dd-163">針對 [允許的來源]，輸入星號 (\*)。</span><span class="sxs-lookup"><span data-stu-id="436dd-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="436dd-164">在 [hello**允許指令動詞**下拉式清單中，同時選取**取得**和**選項**。</span><span class="sxs-lookup"><span data-stu-id="436dd-164">In hello **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="436dd-165">針對 [允許的標頭]，輸入星號 (\*)。</span><span class="sxs-lookup"><span data-stu-id="436dd-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="436dd-166">針對 [公開的標頭]，輸入星號 (\*)。</span><span class="sxs-lookup"><span data-stu-id="436dd-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="436dd-167">針對 [最長使用期限 (秒)]，輸入 **200**。</span><span class="sxs-lookup"><span data-stu-id="436dd-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="436dd-168">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="436dd-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="436dd-169">測試 CORS</span><span class="sxs-lookup"><span data-stu-id="436dd-169">Test CORS</span></span>

<span data-ttu-id="436dd-170">驗證，您可以藉由下列 hello:</span><span class="sxs-lookup"><span data-stu-id="436dd-170">Validate that you're ready by doing hello following:</span></span>

1. <span data-ttu-id="436dd-171">移 toohello[測試 cors.org](http://test-cors.org/)網站，然後按一下 [貼上的 hello URL 在 hello**遠端 URL**方塊。</span><span class="sxs-lookup"><span data-stu-id="436dd-171">Go toohello [test-cors.org](http://test-cors.org/) website, and then paste hello URL in hello **Remote URL** box.</span></span>
2. <span data-ttu-id="436dd-172">按一下 [傳送要求]。</span><span class="sxs-lookup"><span data-stu-id="436dd-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="436dd-173">如果您收到錯誤，請確定您的 [CORS 設定](#configure-cors)正確無誤。</span><span class="sxs-lookup"><span data-stu-id="436dd-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="436dd-174">您也可能需要 tooclear 您的瀏覽器快取，或按下 Ctrl + Shift + P 開啟 inprivate 瀏覽工作階段。</span><span class="sxs-lookup"><span data-stu-id="436dd-174">You might also need tooclear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="436dd-175">修改您的註冊或登入自訂原則</span><span class="sxs-lookup"><span data-stu-id="436dd-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="436dd-176">在最上層的 hello * \<TrustFrameworkPolicy\> *標記中，您應該會發現* \<BuildingBlocks\> *標記。</span><span class="sxs-lookup"><span data-stu-id="436dd-176">Under hello top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="436dd-177">Hello 內* \<BuildingBlocks\> *標記，加入* \<ContentDefinitions\> *藉由複製下列範例中的 hello 的標記。</span><span class="sxs-lookup"><span data-stu-id="436dd-177">Within hello *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying hello following example.</span></span> <span data-ttu-id="436dd-178">取代*your_storage_account* hello 的儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="436dd-178">Replace *your_storage_account* with hello name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="436dd-179">上傳更新的自訂原則</span><span class="sxs-lookup"><span data-stu-id="436dd-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="436dd-180">在 [hello [Azure 入口網站](https://portal.azure.com)，[切換至您的 Azure AD B2C 租用戶的 hello 內容](active-directory-b2c-navigate-to-b2c-context.md)，然後開啟 [hello **Azure AD B2C**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="436dd-180">In hello [Azure portal](https://portal.azure.com), [switch into hello context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open hello **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="436dd-181">按一下 [所有原則]。</span><span class="sxs-lookup"><span data-stu-id="436dd-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="436dd-182">按一下 [上傳原則]。</span><span class="sxs-lookup"><span data-stu-id="436dd-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="436dd-183">上傳`SignUpOrSignin.xml`以 hello * \<ContentDefinitions\> *您先前加入的標記。</span><span class="sxs-lookup"><span data-stu-id="436dd-183">Upload `SignUpOrSignin.xml` with hello *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="436dd-184">使用測試 hello 自訂原則**立即執行**</span><span class="sxs-lookup"><span data-stu-id="436dd-184">Test hello custom policy by using **Run now**</span></span>

1. <span data-ttu-id="436dd-185">在 [hello **Azure AD B2C**刀鋒視窗中，跳過**所有原則**。</span><span class="sxs-lookup"><span data-stu-id="436dd-185">On hello **Azure AD B2C** blade, go too**All polices**.</span></span>
2. <span data-ttu-id="436dd-186">選取您上傳，hello 自訂原則，然後按一下 hello**立即執行**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="436dd-186">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="436dd-187">您應該能夠 toosign 向上使用電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="436dd-187">You should be able toosign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="436dd-188">參考</span><span class="sxs-lookup"><span data-stu-id="436dd-188">Reference</span></span>

<span data-ttu-id="436dd-189">您可以在此找到 UI 自訂的範例範本：</span><span class="sxs-lookup"><span data-stu-id="436dd-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="436dd-190">hello sample_templates/wingtip 資料夾包含下列 HTML 檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="436dd-190">hello sample_templates/wingtip folder contains hello following HTML files:</span></span>

| <span data-ttu-id="436dd-191">HTML5 範本</span><span class="sxs-lookup"><span data-stu-id="436dd-191">HTML5 template</span></span> | <span data-ttu-id="436dd-192">說明</span><span class="sxs-lookup"><span data-stu-id="436dd-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="436dd-193">phonefactor.html</span><span class="sxs-lookup"><span data-stu-id="436dd-193">*phonefactor.html*</span></span> | <span data-ttu-id="436dd-194">使用此檔案作為多重要素驗證頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="436dd-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="436dd-195">resetpassword.html</span><span class="sxs-lookup"><span data-stu-id="436dd-195">*resetpassword.html*</span></span> | <span data-ttu-id="436dd-196">使用此檔案作為忘記密碼頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="436dd-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="436dd-197">selfasserted.html</span><span class="sxs-lookup"><span data-stu-id="436dd-197">*selfasserted.html*</span></span> | <span data-ttu-id="436dd-198">使用此檔案作為社交帳戶註冊頁面、本機帳戶註冊頁面或本機帳戶登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="436dd-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="436dd-199">unified.html</span><span class="sxs-lookup"><span data-stu-id="436dd-199">*unified.html*</span></span> | <span data-ttu-id="436dd-200">使用此檔案作為統一註冊或登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="436dd-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="436dd-201">updateprofile.html</span><span class="sxs-lookup"><span data-stu-id="436dd-201">*updateprofile.html*</span></span> | <span data-ttu-id="436dd-202">使用此檔案作為統一註冊或登入頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="436dd-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="436dd-203">在 [hello[修改註冊或登入自訂原則區段](#modify-your-sign-up-or-sign-in-custom-policy)，設定 hello 內容定義`api.idpselections`。</span><span class="sxs-lookup"><span data-stu-id="436dd-203">In hello [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured hello content definition for `api.idpselections`.</span></span> <span data-ttu-id="436dd-204">hello 的整組內容定義辨識 hello Azure AD B2C 身分識別體驗架構以及其描述的識別碼是下表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="436dd-204">hello full set of content definition IDs that are recognized by hello Azure AD B2C identity experience framework and their descriptions are in hello following table:</span></span>

| <span data-ttu-id="436dd-205">內容定義識別碼</span><span class="sxs-lookup"><span data-stu-id="436dd-205">Content definition ID</span></span> | <span data-ttu-id="436dd-206">說明</span><span class="sxs-lookup"><span data-stu-id="436dd-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="436dd-207">api.error</span><span class="sxs-lookup"><span data-stu-id="436dd-207">*api.error*</span></span> | <span data-ttu-id="436dd-208">**錯誤頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-208">**Error page**.</span></span> <span data-ttu-id="436dd-209">在發生例外狀況或錯誤時，系統會顯示此頁面。</span><span class="sxs-lookup"><span data-stu-id="436dd-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="436dd-210">api.idpselections</span><span class="sxs-lookup"><span data-stu-id="436dd-210">*api.idpselections*</span></span> | <span data-ttu-id="436dd-211">**識別提供者選取頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-211">**Identity provider selection page**.</span></span> <span data-ttu-id="436dd-212">此頁面包含一份 hello 使用者的提供者在登入時，可以選擇從身分識別。</span><span class="sxs-lookup"><span data-stu-id="436dd-212">This page contains a list of identity providers that hello user can choose from during sign-in.</span></span> <span data-ttu-id="436dd-213">這些選項是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="436dd-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="436dd-214">api.idpselections.signup</span><span class="sxs-lookup"><span data-stu-id="436dd-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="436dd-215">**用於註冊的識別提供者選取**。</span><span class="sxs-lookup"><span data-stu-id="436dd-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="436dd-216">此頁面包含身分識別提供者，hello 使用者可以選擇在註冊期間的清單。</span><span class="sxs-lookup"><span data-stu-id="436dd-216">This page contains a list of identity providers that hello user can choose from during sign-up.</span></span> <span data-ttu-id="436dd-217">這些選項是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="436dd-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="436dd-218">api.localaccountpasswordreset</span><span class="sxs-lookup"><span data-stu-id="436dd-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="436dd-219">**忘記密碼頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-219">**Forgot password page**.</span></span> <span data-ttu-id="436dd-220">此頁面包含表單 hello 使用者必須完成的 tooinitiate 密碼重設。</span><span class="sxs-lookup"><span data-stu-id="436dd-220">This page contains a form that hello user must complete tooinitiate a password reset.</span></span>  |
| <span data-ttu-id="436dd-221">api.localaccountsignin</span><span class="sxs-lookup"><span data-stu-id="436dd-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="436dd-222">**本機帳戶登入頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-222">**Local account sign-in page**.</span></span> <span data-ttu-id="436dd-223">此頁面包含登入表單，可供使用以電子郵件地址或使用者名稱為基礎的本機帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="436dd-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="436dd-224">hello 表單可以包含文字輸入的方塊和密碼項目] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="436dd-224">hello form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="436dd-225">api.localaccountsignup</span><span class="sxs-lookup"><span data-stu-id="436dd-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="436dd-226">**本機帳戶註冊頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-226">**Local account sign-up page**.</span></span> <span data-ttu-id="436dd-227">此頁面包含登入表單，可供註冊以電子郵件地址或使用者名稱為基礎的本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="436dd-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="436dd-228">hello 表單可以包含各種輸入的控制項的詳細資訊，例如輸入的文字方塊、 密碼輸入方塊、 選項按鈕、 單一選取下拉式清單方塊中和多重選取的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="436dd-228">hello form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="436dd-229">api.phonefactor</span><span class="sxs-lookup"><span data-stu-id="436dd-229">*api.phonefactor*</span></span> | <span data-ttu-id="436dd-230">**Multi-Factor Authentication 頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="436dd-231">在此頁面上，使用者可以在註冊或登入期間驗證其電話號碼 (藉由使用文字或語音)。</span><span class="sxs-lookup"><span data-stu-id="436dd-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="436dd-232">api.selfasserted</span><span class="sxs-lookup"><span data-stu-id="436dd-232">*api.selfasserted*</span></span> | <span data-ttu-id="436dd-233">**社交帳戶註冊頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-233">**Social account sign-up page**.</span></span> <span data-ttu-id="436dd-234">此頁面包含使用者在使用社交識別提供者 (例如 Facebook 或 Google+) 的現有帳戶註冊時必須填妥的註冊表單。</span><span class="sxs-lookup"><span data-stu-id="436dd-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="436dd-235">此頁面是類似 toohello 前面社交帳戶註冊] 頁面上，除了 hello 密碼項目欄位。</span><span class="sxs-lookup"><span data-stu-id="436dd-235">This page is similar toohello preceding social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="436dd-236">api.selfasserted.profileupdate</span><span class="sxs-lookup"><span data-stu-id="436dd-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="436dd-237">**設定檔更新頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-237">**Profile update page**.</span></span> <span data-ttu-id="436dd-238">此頁面包含表單，使用者可以使用 tooupdate 其設定檔。</span><span class="sxs-lookup"><span data-stu-id="436dd-238">This page contains a form that users can use tooupdate their profile.</span></span> <span data-ttu-id="436dd-239">此頁面是類似 toohello 社交帳戶註冊] 頁面上，除了 hello 密碼項目欄位。</span><span class="sxs-lookup"><span data-stu-id="436dd-239">This page is similar toohello social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="436dd-240">api.signuporsignin</span><span class="sxs-lookup"><span data-stu-id="436dd-240">*api.signuporsignin*</span></span> | <span data-ttu-id="436dd-241">**統一的註冊或登入頁面**。</span><span class="sxs-lookup"><span data-stu-id="436dd-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="436dd-242">此頁面會處理這兩個 hello 註冊和登入的使用者可以使用企業身分識別提供者，社交身分識別提供者，例如 Facebook 或 Google + 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="436dd-242">This page handles both hello sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="436dd-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="436dd-243">Next steps</span></span>

<span data-ttu-id="436dd-244">如需有關可自訂之 UI 元素的其他資訊，請參閱[內建原則 UI 自訂參考指南](active-directory-b2c-reference-ui-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="436dd-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
