---
title: "準備和測試優惠以部署至 Azure Marketplace | Microsoft Docs"
description: "將供應項目部署至 Azure Marketplace 之前，關於提供行銷內容、設定價格方案和測試供應項目的詳細指示。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3ccd2448-895b-477e-adf6-ab655a21d2fa
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/17/2016
ms.author: hascipio
ms.openlocfilehash: 7db86716cdf8f9eb921c3c1813970acae7a3016b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="complete-the-offer-creation-with-marketing-content"></a><span data-ttu-id="85628-103">使用行銷內容完成供應項目建立程序</span><span class="sxs-lookup"><span data-stu-id="85628-103">Complete the offer creation with marketing content</span></span>
<span data-ttu-id="85628-104">在發佈程序的這個步驟中，您需要在 Azure Marketplace 中提供特定的行銷內容，以及關於您的優惠和 (或) SKU 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="85628-104">In this step of the publishing process, you will need to provide certain marketing content and details about your offer and/or SKUs in the Azure Marketplace.</span></span> <span data-ttu-id="85628-105">例如，您將提供產品的描述、公司標誌、價目表、方案的詳細資料，以及其他將您的優惠和 (或) SKU 推送至預備環境的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="85628-105">For example, you will provide a description of your product, company logos, price plans, details of plans, and other information necessary to push your offer and/or SKU to staging.</span></span> <span data-ttu-id="85628-106">此資訊會做為 Azure 入口網站中的行銷內容。</span><span class="sxs-lookup"><span data-stu-id="85628-106">This information is used as marketing content in the Azure portal.</span></span> <span data-ttu-id="85628-107">您將在[發佈入口網站][link-pubportal]中開始進行此程序。</span><span class="sxs-lookup"><span data-stu-id="85628-107">You will begin this process in the [publishing portal][link-pubportal].</span></span>

## <a name="step-1-provide-marketplace-marketing-content"></a><span data-ttu-id="85628-108">步驟 1：提供 Marketplace 行銷內容</span><span class="sxs-lookup"><span data-stu-id="85628-108">Step 1: Provide Marketplace marketing content</span></span>
<span data-ttu-id="85628-109">**英文是預設值，並且是唯一支援的語言。**</span><span class="sxs-lookup"><span data-stu-id="85628-109">**English is the default and only supported language.**</span></span> <span data-ttu-id="85628-110">請確定欄位中提供的所有資訊都是英文。</span><span class="sxs-lookup"><span data-stu-id="85628-110">Please ensure that all information provided in the fields is in English.</span></span> <span data-ttu-id="85628-111">在您進入預備環境之前，所有資訊皆可隨時編輯。</span><span class="sxs-lookup"><span data-stu-id="85628-111">All information can be edited at any time until you push to staging.</span></span>

1. <span data-ttu-id="85628-112">移至發佈入口網站 [https://publish.windowsazure.com](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="85628-112">Go to the publishing portal, [https://publish.windowsazure.com](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="85628-113">在左側功能表上，按一下 [行銷]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="85628-113">On the left menu, click the **Marketing** tab.</span></span>
3. <span data-ttu-id="85628-114">在主面板中，按一下 [英文 (美國)]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="85628-114">In the main panel, click the **English (US)** button.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="85628-115">所有欄位都必須填入內容 (包含影像)，才能推送至預備環境。</span><span class="sxs-lookup"><span data-stu-id="85628-115">All fields must have entries, including the images, for you to be able to push to staging.</span></span>
   > 
   > 

### <a name="details-and-plans"></a><span data-ttu-id="85628-116">詳細資料和方案</span><span class="sxs-lookup"><span data-stu-id="85628-116">Details and plans</span></span>
1. <span data-ttu-id="85628-117">在 [詳細資料]  索引標籤下方，輸入優惠標題 (最多 50 個字元)、優惠摘要 (最多 100 個字元)、優惠完整摘要 (最多 256 個字元)、優惠描述 (最多 1300 個字元)、標誌</span><span class="sxs-lookup"><span data-stu-id="85628-117">Enter the offer title (maximum 50 characters), offer summary (maximum 100 characters), offer long summary (maximum 256 characters), offer description (maximum 1300 characters), logos under the **Details** tab</span></span>
2. <span data-ttu-id="85628-118">在 [方案]  索引標籤下方，輸入方案標題 (最多 50 個字元)、方案摘要 (最多 100 個字元)、方案描述 (最多 2000 個字元)。</span><span class="sxs-lookup"><span data-stu-id="85628-118">Enter plan title (maximum 50 characters), plan summary (maximum 100 characters), plan description (maximum 2000 characters) under the **Plans** tab.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="85628-119">您可以使用下列 HTML 標記來格式化供應項目與方案的摘要、完整摘要及描述。</span><span class="sxs-lookup"><span data-stu-id="85628-119">You can use the following HTML tags to format the summary, long summary and description of the offer and plans.</span></span> <span data-ttu-id="85628-120">允許的 HTML 標記為 h1、h2、h3、h4、h5、p、ol、ul、li、a[target|href]、strong、em、b、i。</span><span class="sxs-lookup"><span data-stu-id="85628-120">The allowed HTML tags are h1, h2, h3, h4, h5, p, ol, ul, li, a[target|href], strong, em, b, i.</span></span>
   > 
   > 
3. <span data-ttu-id="85628-121">請不要在供應項目和方案描述下方輸入重複文字。</span><span class="sxs-lookup"><span data-stu-id="85628-121">Do not enter duplicate text under offer and plan description.</span></span>
4. <span data-ttu-id="85628-122">請不要在方案標題和供應項目完整摘要下方輸入重複文字。</span><span class="sxs-lookup"><span data-stu-id="85628-122">Do not enter duplicate text under plan’s title and offer long summary.</span></span>
5. <span data-ttu-id="85628-123">請不要在方案標題和供應項目摘要下方輸入重複文字。</span><span class="sxs-lookup"><span data-stu-id="85628-123">Do not enter duplicate text under plan title and offer summary.</span></span>
6. <span data-ttu-id="85628-124">對於含有多個方案的供應項目，請勿輸入相同的方案標題。</span><span class="sxs-lookup"><span data-stu-id="85628-124">Do not enter identical plan titles for an offer with multiple plans.</span></span>
7. <span data-ttu-id="85628-125">以 PNG 格式上傳必要規格的影像 (在發佈入口網站中提及)，每種大小各一個。</span><span class="sxs-lookup"><span data-stu-id="85628-125">Upload images of the required specifications (mentioned in the Publishing Portal) in PNG format, one for each size.</span></span>
8. <span data-ttu-id="85628-126">請確定標誌遵循下面所提及的 Azure Marketplace 標誌指導方針。</span><span class="sxs-lookup"><span data-stu-id="85628-126">Ensure that the logos follow the Azure Marketplace logo guidelines mentioned below.</span></span>
   
   ![繪圖](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-details-02.png)

<span data-ttu-id="85628-128">**Azure Marketplace 標誌指導方針**</span><span class="sxs-lookup"><span data-stu-id="85628-128">**Azure Marketplace Logo Guidelines**</span></span>

<span data-ttu-id="85628-129">發佈入口網站中所上傳的所有標誌都應該遵循下列指導方針︰</span><span class="sxs-lookup"><span data-stu-id="85628-129">All the logos uploaded in the Publishing Portal should follow the below guidelines:</span></span>

* <span data-ttu-id="85628-130">Azure 設計具有簡單的調色盤。</span><span class="sxs-lookup"><span data-stu-id="85628-130">The Azure design has a simple color palette.</span></span> <span data-ttu-id="85628-131">請保持標誌上具有最少的主要和次要色彩數目。</span><span class="sxs-lookup"><span data-stu-id="85628-131">Keep the number of primary and secondary colors on your logo low.</span></span>
* <span data-ttu-id="85628-132">Azure 入口網站的佈景主題色彩是白色與黑色。</span><span class="sxs-lookup"><span data-stu-id="85628-132">The theme colors of the Azure portal are white and black.</span></span> <span data-ttu-id="85628-133">因此請避免使用這些色彩做為您標誌的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="85628-133">Hence avoid using these colors as the background color of your logos.</span></span> <span data-ttu-id="85628-134">請使用會讓您的標誌在 Azure 入口網站顯得突出的某些色彩。</span><span class="sxs-lookup"><span data-stu-id="85628-134">Use some color that would make your logos prominent in the Azure portal.</span></span> <span data-ttu-id="85628-135">建議您使用簡單的主要色彩。</span><span class="sxs-lookup"><span data-stu-id="85628-135">We recommend simple primary colors.</span></span> <span data-ttu-id="85628-136">**如果您使用透明背景，請確定標誌/文字不是白色、黑色或藍色。**</span><span class="sxs-lookup"><span data-stu-id="85628-136">**If you are using transparent background, then make sure that the logos/text are not white or black or blue.**</span></span>
* <span data-ttu-id="85628-137">請不要在標誌上使用漸層背景。</span><span class="sxs-lookup"><span data-stu-id="85628-137">Do not use a gradient background on the logo.</span></span>
* <span data-ttu-id="85628-138">避免在標誌上放置文字 (甚至是公司或品牌名稱)。</span><span class="sxs-lookup"><span data-stu-id="85628-138">Avoid placing text, even your company or brand name, on the logo.</span></span> <span data-ttu-id="85628-139">您標誌的外觀與風格應該是「一般」，而且應該避免漸層。</span><span class="sxs-lookup"><span data-stu-id="85628-139">The look and feel of your logo should be 'flat' and should avoid gradients.</span></span>
* <span data-ttu-id="85628-140">標誌不應該自動進行縮放。</span><span class="sxs-lookup"><span data-stu-id="85628-140">The logo should not be stretched.</span></span>
* <span data-ttu-id="85628-141">小型標誌的大小應該是 40 X 40 像素</span><span class="sxs-lookup"><span data-stu-id="85628-141">Small logo should be of size 40 X 40 px</span></span>
* <span data-ttu-id="85628-142">中型標誌的大小應該是 90 X 90 像素</span><span class="sxs-lookup"><span data-stu-id="85628-142">Medium logo should be of size 90 X 90 px</span></span>
* <span data-ttu-id="85628-143">大型標誌的大小應該是 115 X 115 像素</span><span class="sxs-lookup"><span data-stu-id="85628-143">Large logo should be of size 115 X 115 px</span></span>
* <span data-ttu-id="85628-144">寬標誌的大小應該是 255 X 115 像素</span><span class="sxs-lookup"><span data-stu-id="85628-144">Wide logo should be of size 255 X 115 px</span></span>
* <span data-ttu-id="85628-145">主圖標誌的大小應該是 815 X 290 像素</span><span class="sxs-lookup"><span data-stu-id="85628-145">Hero logo should be of size 815 X 290 px</span></span>

> [!NOTE]
> <span data-ttu-id="85628-146">主圖標誌為選用項。</span><span class="sxs-lookup"><span data-stu-id="85628-146">The Hero logo is optional.</span></span> <span data-ttu-id="85628-147">發行者可以選擇不上傳主圖標誌。</span><span class="sxs-lookup"><span data-stu-id="85628-147">The publisher can choose not to upload a Hero logo.</span></span> <span data-ttu-id="85628-148">但主圖圖示一旦上傳，即無法從發佈入口網站中刪除。</span><span class="sxs-lookup"><span data-stu-id="85628-148">However once uploaded the hero icon cannot be deleted from the Publishing portal.</span></span> <span data-ttu-id="85628-149">屆時合作夥伴必須遵循主圖圖示的 Azure Marketplace 指導方針。</span><span class="sxs-lookup"><span data-stu-id="85628-149">At that time, the partner must follow the Azure Marketplace guidelines for Hero icons.</span></span>
> 
> 

  ![繪圖](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-details-03.png)

<span data-ttu-id="85628-151">**主圖標誌圖示的其他指導方針 (選擇性)**</span><span class="sxs-lookup"><span data-stu-id="85628-151">**Additional guidelines for the Hero logo icon (optional)**</span></span>

* <span data-ttu-id="85628-152">主圖標誌為選用項。</span><span class="sxs-lookup"><span data-stu-id="85628-152">The Hero logo is optional.</span></span> <span data-ttu-id="85628-153">發行者可以選擇不上傳主圖標誌。</span><span class="sxs-lookup"><span data-stu-id="85628-153">The publisher can choose not to upload a Hero logo.</span></span> <span data-ttu-id="85628-154">**但主圖圖示一旦上傳，即無法從發佈入口網站中刪除。屆時合作夥伴必須遵循主圖圖示的 Azure Marketplace 指導方針，否則供應項目將無法核准進入生產環境。**</span><span class="sxs-lookup"><span data-stu-id="85628-154">**However once uploaded the hero icon cannot be deleted from the Publishing portal. At that time, the partner must follow the Azure Marketplace guidelines for Hero icons else the offer will not be approved to production.**</span></span>
* <span data-ttu-id="85628-155">發行者顯示名稱、方案標題和供應項目完整摘要會以白色字型色彩顯示。</span><span class="sxs-lookup"><span data-stu-id="85628-155">The Publisher Display Name, plan title and the offer long summary are displayed in white font color.</span></span> <span data-ttu-id="85628-156">因此，您應避免在主圖圖示的背景使用淺色系。</span><span class="sxs-lookup"><span data-stu-id="85628-156">Hence you should avoid keeping any light color in the background of the Hero Icon.</span></span> <span data-ttu-id="85628-157">主圖圖示不允許使用黑色、白色和透明背景。</span><span class="sxs-lookup"><span data-stu-id="85628-157">Black, white and transparent background is not allowed for Hero icons.</span></span>
* <span data-ttu-id="85628-158">供應項目列出之後，會以程式設計方式將發行者顯示名稱、方案標題、供應項目完整摘要和 [建立] 按鈕內嵌在主圖標誌內。</span><span class="sxs-lookup"><span data-stu-id="85628-158">The publisher display name, plan title, the offer long summary and the create button are embedded programmatically inside the Hero logo once the offer goes listed.</span></span> <span data-ttu-id="85628-159">因此您在設計主圖標誌時不應輸入任何文字。</span><span class="sxs-lookup"><span data-stu-id="85628-159">So you should not enter any text while you are designing the Hero logo.</span></span> <span data-ttu-id="85628-160">您只需在右邊留下空白空間，因為我們會以程式設計方式於該處內嵌文字 (也就是</span><span class="sxs-lookup"><span data-stu-id="85628-160">Just leave empty space on the right because the text (i.e.</span></span> <span data-ttu-id="85628-161">發行者顯示名稱、方案標題、供應項目完整摘要)。</span><span class="sxs-lookup"><span data-stu-id="85628-161">publisher display name, plan title, the offer long summary) will be included programmatically by us over there.</span></span> <span data-ttu-id="85628-162">文字右側的空白空間應為 415 x 100 (從左邊開始位移 370px)。</span><span class="sxs-lookup"><span data-stu-id="85628-162">The empty space for the text should be 415x100 on the right (and it is offset by 370px from the left).</span></span>
  
  ![繪圖](media/marketplace-publishing-push-to-staging/pubportal-herobanner.png)

### <a name="links"></a><span data-ttu-id="85628-164">連結</span><span class="sxs-lookup"><span data-stu-id="85628-164">Links</span></span>
<span data-ttu-id="85628-165">在左側工具列的 [連結]  索引標籤上，輸入任何可能對客戶有幫助的資訊連結。</span><span class="sxs-lookup"><span data-stu-id="85628-165">On the **Links** tab on the left bar, enter any links with information that may help customers.</span></span> <span data-ttu-id="85628-166">輸入每個連結的名稱和 URL。</span><span class="sxs-lookup"><span data-stu-id="85628-166">Enter a name and URL for each link.</span></span>

![繪圖](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-link-01.png)

### <a name="sample-images-optional"></a><span data-ttu-id="85628-168">範例影像 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="85628-168">Sample images (optional)</span></span>
> [!NOTE]
> <span data-ttu-id="85628-169">加入範例影像是選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="85628-169">Including a sample image is an optional step.</span></span>
> <span data-ttu-id="85628-170">雖然您可以在發佈入口網站上傳多個範例影像，但只有一個影像會顯示在 Azure 入口網站 (系統隨機選取)。</span><span class="sxs-lookup"><span data-stu-id="85628-170">Even though you can upload multiple sample images in the Publishing portal, only one image (randomly selected by the system) gets displayed in the Azure portal.</span></span> <span data-ttu-id="85628-171">基於這個理由，建議您最多上傳一個範例影像。</span><span class="sxs-lookup"><span data-stu-id="85628-171">For this reason, we recommend uploading at most one sample image.</span></span>
> 
> 

<span data-ttu-id="85628-172">在左側功能表的 [範例影像] 索引標籤上，按一下 [上傳新的影像] 以上傳新的影像。</span><span class="sxs-lookup"><span data-stu-id="85628-172">On the **Sample Images** tab on the left menu, upload a new image by clicking **Upload a new image**.</span></span> <span data-ttu-id="85628-173">如果目前已有影像而您想要取代它，請按一下 [取代影像] 。</span><span class="sxs-lookup"><span data-stu-id="85628-173">If you have an existing image and you would like to replace it, click **Replace image**.</span></span>

![繪圖](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-sampleimg-01.png)

### <a name="legal"></a><span data-ttu-id="85628-175">法律</span><span class="sxs-lookup"><span data-stu-id="85628-175">Legal</span></span>
<span data-ttu-id="85628-176">在 [法律聲明]  索引標籤上，提供您的使用原則/條款連結。</span><span class="sxs-lookup"><span data-stu-id="85628-176">On the **Legal** tab, provide a link to your policies/terms of use.</span></span> <span data-ttu-id="85628-177">在大型 [使用條款]  方塊中輸入或貼上條款。</span><span class="sxs-lookup"><span data-stu-id="85628-177">Enter or paste the terms in the large **Terms of Use** box.</span></span> <span data-ttu-id="85628-178">法律使用條款的字元限制為 1,000,000 個字元。</span><span class="sxs-lookup"><span data-stu-id="85628-178">The character limit for the legal terms of use is 1,000,000 characters.</span></span>

![繪圖](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-legal-01.png)

<span data-ttu-id="85628-180"> 對於「虛擬機器」供應項目，一旦供應項目/SKU於 Azure 入口網站預備完成，您就無法變更以下欄位：</span><span class="sxs-lookup"><span data-stu-id="85628-180">**Note:** For Virtual Machine offers, once an offer/SKU is staged in the Azure Portal, you cannot change the fields given below:</span></span>

* <span data-ttu-id="85628-181">**供應項目識別碼︰**[發佈入口網站 -> 虛擬機器 -> 您的供應項目 -> VM 映像索引標籤 -> 供應項目識別碼]</span><span class="sxs-lookup"><span data-stu-id="85628-181">**Offer Identifier:** [Publishing portal -> Virtual Machines -> your Offer -> VM Images tab -> Offer Identifier]</span></span>
* <span data-ttu-id="85628-182">**SKU 識別碼︰**[發佈入口網站 -> 虛擬機器 -> 選取您的供應項目 -> SKU 索引標籤 -> 新增 SKU]</span><span class="sxs-lookup"><span data-stu-id="85628-182">**SKU Identifier:** [Publishing portal -> Virtual Machines -> Select your Offer -> SKUs tab -> Add a SKU]</span></span>
* <span data-ttu-id="85628-183">**發行者命名空間︰**[發佈入口網站 -> 虛擬機器 -> 逐步解說索引標籤 -> 告知我們您的公司 (請見「步驟 2：註冊您的公司」) -> 發行者命名空間 -> 命名空間]</span><span class="sxs-lookup"><span data-stu-id="85628-183">**Publisher Namespace:** [Publishing portal -> Virtual Machines -> Walkthrough tab -> Tell Us About Your Company (Found Under “Step 2 Register Your Company”) -> Publisher Namespace ->Namespace]</span></span>

<span data-ttu-id="85628-184">對於「虛擬機器」供應項目，一旦供應項目/SKU 列於 Azure Marketplace，您就無法變更以下欄位：</span><span class="sxs-lookup"><span data-stu-id="85628-184">For Virtual Machine offers, once the offer/SKU is listed in the Azure Marketplace, you cannot change the fields given below:</span></span>

* <span data-ttu-id="85628-185">**供應項目識別碼︰**[發佈入口網站 -> 虛擬機器 -> 選取您的供應項目 -> VM 映像 -> 供應項目識別碼]</span><span class="sxs-lookup"><span data-stu-id="85628-185">**Offer Identifier:** [Publishing portal -> Virtual Machines -> select your Offer -> VM Images -> Offer Identifier]</span></span>
* <span data-ttu-id="85628-186">**SKU 識別碼︰**[發佈入口網站 -> 虛擬機器 -> 選取您的供應項目 -> SKU 索引標籤 -> 新增 SKU]</span><span class="sxs-lookup"><span data-stu-id="85628-186">**SKU Identifier:** [Publishing portal -> Virtual Machines -> Select your Offer -> SKUs tab -> Add a SKU]</span></span>
* <span data-ttu-id="85628-187">**發行者命名空間︰**[發佈入口網站 -> 虛擬機器 -> 逐步解說索引標籤 -> 告知我們您的公司 (請見「步驟 2：註冊」) -> 發行者命名空間 -> 命名空間]</span><span class="sxs-lookup"><span data-stu-id="85628-187">**Publisher Namespace:** [Publishing portal -> Virtual Machines -> Walkthrough tab -> Tell Us About Your Company (Found Under Step 2 Register) Publisher Namespace ->Namespace]</span></span>
* <span data-ttu-id="85628-188">**連接埠：**[發佈入口網站 -> 虛擬機器 -> 您的供應項目 -> VM 映像索引標籤 -> 開啟連接埠]</span><span class="sxs-lookup"><span data-stu-id="85628-188">**Ports:** [Publishing portal -> Virtual Machines -> your Offer -> VM Images tab -> Open Ports]</span></span>
* <span data-ttu-id="85628-189">**已列出 SKU 的價格變更**</span><span class="sxs-lookup"><span data-stu-id="85628-189">**Pricing Change of listed SKU(s)**</span></span>
* <span data-ttu-id="85628-190">**已列出 SKU 的計費模式變更**</span><span class="sxs-lookup"><span data-stu-id="85628-190">**Billing Model Change of listed SKU(s)**</span></span>
* <span data-ttu-id="85628-191">**移除已列出 SKU 的計費區域**</span><span class="sxs-lookup"><span data-stu-id="85628-191">**Removal of billing regions of listed SKU(s)**</span></span>
* <span data-ttu-id="85628-192">**變更已列出 SKU 的資料磁碟計數**</span><span class="sxs-lookup"><span data-stu-id="85628-192">**Changing the data disk count of listed SKU(s)**</span></span>

## <a name="step-2-set-your-prices"></a><span data-ttu-id="85628-193">步驟 2：設定價格</span><span class="sxs-lookup"><span data-stu-id="85628-193">Step 2: Set your prices</span></span>
### <a name="pricing-models"></a><span data-ttu-id="85628-194">定價模式</span><span class="sxs-lookup"><span data-stu-id="85628-194">Pricing models</span></span>
| <span data-ttu-id="85628-195">定價模式</span><span class="sxs-lookup"><span data-stu-id="85628-195">Pricing model</span></span> | <span data-ttu-id="85628-196">說明</span><span class="sxs-lookup"><span data-stu-id="85628-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85628-197">基本</span><span class="sxs-lookup"><span data-stu-id="85628-197">Base</span></span> |<span data-ttu-id="85628-198">購買時支付的每月分期費率，例如 $10 美元/月</span><span class="sxs-lookup"><span data-stu-id="85628-198">Flat monthly rate paid at time of purchase; e.g., $10/month.</span></span> |
| <span data-ttu-id="85628-199">耗用量 (又稱為</span><span class="sxs-lookup"><span data-stu-id="85628-199">Consumption (a.k.a.</span></span> <span data-ttu-id="85628-200">使用量、計量器)</span><span class="sxs-lookup"><span data-stu-id="85628-200">usage, meter)</span></span> |<span data-ttu-id="85628-201">每次使用付費，由供應項目發行者定義。</span><span class="sxs-lookup"><span data-stu-id="85628-201">Pay per use, which is defined by the publisher of the offer.</span></span> <span data-ttu-id="85628-202">無法定義每一基座、每位使用者等等的超額部分，因為並沒有使用者分數的概念，也沒有比例分攤的功能。</span><span class="sxs-lookup"><span data-stu-id="85628-202">Overage cannot be defined per seat, per user, etc., as there is no concept of a fraction of a user or capability to do proration.</span></span> <span data-ttu-id="85628-203">使用量由合作夥伴每小時報告一次。</span><span class="sxs-lookup"><span data-stu-id="85628-203">Usage is reported by the partner on an hourly basis.</span></span> <span data-ttu-id="85628-204">客戶依每月計費週期付款，而非預付式的月繳方案。</span><span class="sxs-lookup"><span data-stu-id="85628-204">Customer pays at the of monthly billing cycle, as opposed to up front like monthly plans.</span></span> |
| <span data-ttu-id="85628-205">免費試用</span><span class="sxs-lookup"><span data-stu-id="85628-205">Free trial</span></span> |<span data-ttu-id="85628-206">客戶在一段有限期間內可以免費使用，之後就依正常費率付費。</span><span class="sxs-lookup"><span data-stu-id="85628-206">Customer may use for free, for a limited time, and then pay normal rates thereafter.</span></span> |
| <span data-ttu-id="85628-207">免費層</span><span class="sxs-lookup"><span data-stu-id="85628-207">Free tier</span></span> |<span data-ttu-id="85628-208">方案一律免費。</span><span class="sxs-lookup"><span data-stu-id="85628-208">Plan is always free.</span></span> |
| <span data-ttu-id="85628-209">方案移轉 (又稱為</span><span class="sxs-lookup"><span data-stu-id="85628-209">Migration (a.k.a.</span></span> <span data-ttu-id="85628-210">轉換或升級/降級)</span><span class="sxs-lookup"><span data-stu-id="85628-210">conversion or upgrade/downgrade) of plan</span></span> |<span data-ttu-id="85628-211">使用者從目前方案改用另一種可接受方案的概念，由合作夥伴定義。</span><span class="sxs-lookup"><span data-stu-id="85628-211">Concept of a user moving from their current plan to another acceptable plan; defined by partner.</span></span> |

<span data-ttu-id="85628-212">**依供應項目類型的價格模式**</span><span class="sxs-lookup"><span data-stu-id="85628-212">**Pricing models available by offer type**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85628-213">依供應項目類型可用的某些價格模式。</span><span class="sxs-lookup"><span data-stu-id="85628-213">Availability of certain pricing models vary by offer type.</span></span> <span data-ttu-id="85628-214">請參閱下表。</span><span class="sxs-lookup"><span data-stu-id="85628-214">See the table below.</span></span>
> 
> 

|  | <span data-ttu-id="85628-215">僅基本</span><span class="sxs-lookup"><span data-stu-id="85628-215">Base only</span></span> | <span data-ttu-id="85628-216">僅耗用量</span><span class="sxs-lookup"><span data-stu-id="85628-216">Consumption only</span></span> | <span data-ttu-id="85628-217">基本 + 耗用量</span><span class="sxs-lookup"><span data-stu-id="85628-217">Base + consumption</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="85628-218">虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="85628-218">Virtual machine image</span></span> |<span data-ttu-id="85628-219">否</span><span class="sxs-lookup"><span data-stu-id="85628-219">No</span></span> |<span data-ttu-id="85628-220">是</span><span class="sxs-lookup"><span data-stu-id="85628-220">Yes</span></span> |<span data-ttu-id="85628-221">否</span><span class="sxs-lookup"><span data-stu-id="85628-221">No</span></span> |
| <span data-ttu-id="85628-222">開發人員服務</span><span class="sxs-lookup"><span data-stu-id="85628-222">Developer service</span></span> |<span data-ttu-id="85628-223">是</span><span class="sxs-lookup"><span data-stu-id="85628-223">Yes</span></span> |<span data-ttu-id="85628-224">是</span><span class="sxs-lookup"><span data-stu-id="85628-224">Yes</span></span> |<span data-ttu-id="85628-225">是</span><span class="sxs-lookup"><span data-stu-id="85628-225">Yes</span></span> |

### <a name="21-set-your-vm-prices"></a><span data-ttu-id="85628-226">2.1.</span><span class="sxs-lookup"><span data-stu-id="85628-226">2.1.</span></span> <span data-ttu-id="85628-227">設定 VM 價格</span><span class="sxs-lookup"><span data-stu-id="85628-227">Set your VM prices</span></span>
<span data-ttu-id="85628-228">目前對於虛擬機器，我們提供下列 **3 種計費模式**</span><span class="sxs-lookup"><span data-stu-id="85628-228">Presently for virtual machines, we have the following **3 types of billing models:**</span></span>

* <span data-ttu-id="85628-229">**每小時︰** 依據發行者針對 VM 大小設定的費率，以每小時為基礎向客戶收費。</span><span class="sxs-lookup"><span data-stu-id="85628-229">**Hourly:** Customers get charged on a per-hour basis based on the rates set by the publishers on the VM sizes.</span></span> <span data-ttu-id="85628-230">如果是 SKU 的 **每小時計費** 模式，總價格會是發行者收取的軟體成本和 Microsoft 收取的基礎結構成本的總和。</span><span class="sxs-lookup"><span data-stu-id="85628-230">In case of **hourly billing** model of the SKUs, the total price will be the summation of the software cost charged by the publisher and the infrastructure cost charged by Microsoft.</span></span> <span data-ttu-id="85628-231">當客戶考慮購買時，總成本將顯示為每小時和每月價格以供客戶參考 (請參閱以下螢幕擷取畫面)。</span><span class="sxs-lookup"><span data-stu-id="85628-231">This total cost will be displayed to the customer as an hourly and monthly price when they are considering the purchase (see the screenshot below).</span></span> <span data-ttu-id="85628-232">**發行者會收取 80% 的應收軟體成本。**</span><span class="sxs-lookup"><span data-stu-id="85628-232">**Publisher receives 80% of the software cost charged by them.**</span></span> <span data-ttu-id="85628-233">因此，在您設定 SKU 的價格之前，請先以此作計算。</span><span class="sxs-lookup"><span data-stu-id="85628-233">Hence please make the calculation accordingly before setting prices for your SKUs.</span></span>
  
    ![繪圖](media/marketplace-publishing-push-to-staging/img2.1-01.png)
* <span data-ttu-id="85628-235">**免費試用版︰** 這是「每小時」模式的另一項好處。</span><span class="sxs-lookup"><span data-stu-id="85628-235">**Free Trial:** This is another flavor of the Hourly model.</span></span> <span data-ttu-id="85628-236">此模式的客戶在 VM 部署後的前 30 天不需負擔任何軟體成本 (免費)。</span><span class="sxs-lookup"><span data-stu-id="85628-236">Here the customer doesn’t get charged for software cost for the first 30 days(Free) after deploying the VM.</span></span> <span data-ttu-id="85628-237">在 30 天過後，他們就必須依據發行者在每小時模型中設定的費率，以每小時為基礎付費。</span><span class="sxs-lookup"><span data-stu-id="85628-237">After 30days they get charged on a per-hour basis based on the rates set by the publishers in the hourly model.</span></span>
* <span data-ttu-id="85628-238">**自備授權 (BYOL)：** 發行者管理 VM 上所執行軟體的授權。</span><span class="sxs-lookup"><span data-stu-id="85628-238">**Bring-Your-Own-License (BYOL):** The publishers manage the licensing of the software running on the VM.</span></span>

<span data-ttu-id="85628-239">**重要：** 一旦供應項目/SKU 列於 Azure Marketplace，您就無法變更以下欄位。</span><span class="sxs-lookup"><span data-stu-id="85628-239">**Important:** Once the offer/SKU is listed in the Azure Marketplace, you cannot change the fields given below.</span></span>

* <span data-ttu-id="85628-240">**已列出 SKU 的價格變更**</span><span class="sxs-lookup"><span data-stu-id="85628-240">**Pricing Change of listed SKU(s)**</span></span>
* <span data-ttu-id="85628-241">**已列出 SKU 的計費模式變更**</span><span class="sxs-lookup"><span data-stu-id="85628-241">**Billing Model Change of listed SKU(s)**</span></span>
* <span data-ttu-id="85628-242">**移除已列出 SKU 的計費區域**</span><span class="sxs-lookup"><span data-stu-id="85628-242">**Removal of billing regions of listed SKU(s)**</span></span>
* <span data-ttu-id="85628-243">**變更已列出 SKU 的資料磁碟計數**</span><span class="sxs-lookup"><span data-stu-id="85628-243">**Changing the data disk count of listed SKU(s)**</span></span>
* <span data-ttu-id="85628-244">**供應項目識別碼︰**[發佈入口網站 -> 虛擬機器 -> 選取您的供應項目 -> VM 映像 -> 供應項目識別碼]</span><span class="sxs-lookup"><span data-stu-id="85628-244">**Offer Identifier:** [Publishing portal -> Virtual Machines -> select your Offer -> VM Images -> Offer Identifier]</span></span>
* <span data-ttu-id="85628-245">**SKU 識別碼︰**[發佈入口網站 -> 虛擬機器 -> 選取您的供應項目 -> SKU 索引標籤 -> 新增 SKU]</span><span class="sxs-lookup"><span data-stu-id="85628-245">**SKU Identifier:** [Publishing portal -> Virtual Machines -> Select your Offer -> SKUs tab -> Add a SKU]</span></span>
* <span data-ttu-id="85628-246">**發行者命名空間︰**[發佈入口網站 -> 虛擬機器 -> 逐步解說索引標籤 -> 告知我們您的公司 (請見「步驟 2：註冊」) -> 發行者命名空間 -> 命名空間]</span><span class="sxs-lookup"><span data-stu-id="85628-246">**Publisher Namespace:** [Publishing portal -> Virtual Machines -> Walkthrough tab -> Tell Us About Your Company (Found Under Step 2 Register) Publisher Namespace -> Namespace]</span></span>
* <span data-ttu-id="85628-247">**連接埠：**[發佈入口網站 -> 虛擬機器 -> 您的供應項目 -> VM 映像索引標籤 -> 開啟連接埠]</span><span class="sxs-lookup"><span data-stu-id="85628-247">**Ports:** [Publishing portal -> Virtual Machines -> your Offer -> VM Images tab -> Open Ports]</span></span>

### <a name="sell-to-countries-of-the-sku"></a><span data-ttu-id="85628-248">SKU 的銷往國家/地區</span><span class="sxs-lookup"><span data-stu-id="85628-248">“Sell-to” countries of the SKU</span></span>
<span data-ttu-id="85628-249">您必須仔細考慮要公開發行您的 SKU 的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="85628-249">You need to carefully consider where you make your SKUs available.</span></span> <span data-ttu-id="85628-250">某些國家/地區歸類為「Microsoft 免稅」，其他則歸類為「ISV 免稅」。</span><span class="sxs-lookup"><span data-stu-id="85628-250">Some countries are classified as “Microsoft remit” and others are classified as “ISV remit.”</span></span>

* <span data-ttu-id="85628-251">在「Microsoft 免稅」國家/地區，Microsoft 會收集客戶的稅款並繳納 (免除) 給政府的稅款。</span><span class="sxs-lookup"><span data-stu-id="85628-251">In “Microsoft remit” countries, Microsoft collects taxes from customers and pays (remits) taxes to the government.</span></span>
* <span data-ttu-id="85628-252">在「ISV 免稅」國家/地區，則是由合作夥伴負責收集客戶的稅款並繳納給政府。</span><span class="sxs-lookup"><span data-stu-id="85628-252">In “ISV remit” countries, partners are responsible for collecting taxes customers and paying taxes to the government.</span></span> <span data-ttu-id="85628-253">如果您選擇在「ISV 免稅」國家/地區銷售，您必須有計算及繳納您所選國家/地區稅款的能力。</span><span class="sxs-lookup"><span data-stu-id="85628-253">If you choose to sell in “ISV remit” countries, you must have the capability to calculate and pay taxes in the countries you select.</span></span>

> [!NOTE]
> <span data-ttu-id="85628-254">除非您已在 [發佈入口網站](https://publish.windowsazure.com)設定您的 SKU 價格，否則將無法在那些國家/地區公開發行。</span><span class="sxs-lookup"><span data-stu-id="85628-254">Your SKU will not be available in the countries unless you set their pricing in the [Publishing portal](https://publish.windowsazure.com).</span></span> <span data-ttu-id="85628-255">以下是設定「每小時」和 BYOL SKU 價格的指引。</span><span class="sxs-lookup"><span data-stu-id="85628-255">Guidance to get set the pricing of Hourly and BYOL SKUs is given below.</span></span>
> 
> 

### <a name="211-how-to-setup-hourly-pricing-model-for-a-sku"></a><span data-ttu-id="85628-256">2.1.1 如何設定 SKU 的每小時定價模式</span><span class="sxs-lookup"><span data-stu-id="85628-256">2.1.1 How to setup hourly pricing model for a SKU</span></span>
<span data-ttu-id="85628-257">請依照下列步驟來設定 SKU 的「每小時」定價模式︰</span><span class="sxs-lookup"><span data-stu-id="85628-257">Please follow the steps given below to setup Hourly pricing model for a SKU:</span></span>

1. <span data-ttu-id="85628-258">登入 [發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="85628-258">Login to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="85628-259">瀏覽至 [虛擬機器]  索引標籤並選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="85628-259">Navigate to the **VIRTUAL MACHINES** tab and select your offer.</span></span>
3. <span data-ttu-id="85628-260">從左側功能表，按一下 [SKU]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="85628-260">From the left hand side menu, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="85628-261">請確定 SKU 標示為「每小時計費模式」。</span><span class="sxs-lookup"><span data-stu-id="85628-261">Ensure that the SKU is marked as “Hourly Billing Model”.</span></span> <span data-ttu-id="85628-262">如果不是，請按一下 [編輯]  按鈕來還原計費模式。</span><span class="sxs-lookup"><span data-stu-id="85628-262">If not, then click on the **EDIT** button to revert the billing model.</span></span> <span data-ttu-id="85628-263">隨即開啟一個視窗。</span><span class="sxs-lookup"><span data-stu-id="85628-263">A window will open.</span></span> <span data-ttu-id="85628-264">取消核取 [計費與授權於 Azure 外部進行 (亦即自備授權)] 核取方塊並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="85628-264">Uncheck the checkbox ‘Billing and licensing is done externally from Azure (aka Bring Your Own License)’ and save the changes.</span></span>
5. <span data-ttu-id="85628-265">如果您想要啟用 SKU 部署前 30 天的免費試用版，請針對 [是否提供免費試用版?] 問題選取 [一個月] 選項。</span><span class="sxs-lookup"><span data-stu-id="85628-265">If you want to enable Free trial for the first 30days of SKU deployment, then select the option “One Month” for the question “Is a free trial available?”</span></span> <span data-ttu-id="85628-266">否則請選取 [無試用版] 選項。</span><span class="sxs-lookup"><span data-stu-id="85628-266">Otherwise, select the option “No Trial”.</span></span> <span data-ttu-id="85628-267">現在請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="85628-267">Now follow the steps given below.</span></span>
6. <span data-ttu-id="85628-268">從左側功能表，按一下 [價格]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="85628-268">From the left hand side menu, click the **PRICING** tab.</span></span>
7. <span data-ttu-id="85628-269">選取您的基本區域。</span><span class="sxs-lookup"><span data-stu-id="85628-269">Select your base region.</span></span>
   
   ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.1_07.png)
8. <span data-ttu-id="85628-271">設定所有核心的價格。</span><span class="sxs-lookup"><span data-stu-id="85628-271">Set the prices for all cores.</span></span> <span data-ttu-id="85628-272">**即使您的 SKU 不支援，您仍然必須提供 SKU 所有核心的價格。**</span><span class="sxs-lookup"><span data-stu-id="85628-272">**You must provide price for all the cores of a SKU even if your SKU does not support it.**</span></span>
   
    ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.1_08.png)
9. <span data-ttu-id="85628-274">手動設定其他區域的價格，或者您可以使用「自動定價」精靈，依據基本區域設定其他區域的價格。</span><span class="sxs-lookup"><span data-stu-id="85628-274">Set the prices for the other regions manually or you can use the AUTOPRICE wizard to set the prices of other regions based on the base region.</span></span> <span data-ttu-id="85628-275">若要使用「自動定價」精靈，請按一下 [依據美國價格自動訂定其他市場價格] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="85628-275">To use the AUTOPRICE wizard click on the button **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES.**</span></span> <span data-ttu-id="85628-276"> 視選取的區域而定，按鈕的標籤可能會不同。</span><span class="sxs-lookup"><span data-stu-id="85628-276">**Note:** The button’s label may be different depending on the region which you have selected.</span></span> <span data-ttu-id="85628-277">由於我們在建立這份文件時選取美國，因此以下螢幕擷取畫面中的按鈕標示為 [依據美國價格自動訂定其他市場價格]。</span><span class="sxs-lookup"><span data-stu-id="85628-277">Since we have selected United States while creating this document, so the button is labeled as “Auto price other markets based on prices in United States” in the screenshot below.</span></span>
   
   ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.1_09.png)
10. <span data-ttu-id="85628-279">自動定價精靈隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="85628-279">The auto price wizard will open.</span></span> <span data-ttu-id="85628-280">第 1 頁會顯示基本市場的選項。</span><span class="sxs-lookup"><span data-stu-id="85628-280">The first page displays the selection for base market.</span></span> <span data-ttu-id="85628-281">選擇您的區域，然後按一下 "->" 按鈕移至下一頁。</span><span class="sxs-lookup"><span data-stu-id="85628-281">Make your section and move to the next page by clicking on the “->” button.</span></span>
    
    ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.1_10.png)
11. <span data-ttu-id="85628-283">選取核心和方案的選項將顯示在第 2 頁。</span><span class="sxs-lookup"><span data-stu-id="85628-283">Option for selecting the cores and plans will be displayed on the page 2.</span></span> <span data-ttu-id="85628-284">選取所需的方案，然後按一下 [->] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="85628-284">Select the desired plans and click “->” button.</span></span> <span data-ttu-id="85628-285">按一下 [全部切換] 按鈕以選取所有**服務方案**和**計量器**，或您可以手動選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="85628-285">Click the **Toggle All** button to select all the **Service plans** and **Meters** or you can manually check the checkboxes.</span></span> <span data-ttu-id="85628-286">**即使您的 SKU 不支援，您仍然必須提供 SKU 所有核心的價格。**</span><span class="sxs-lookup"><span data-stu-id="85628-286">**You must provide price for all the cores of a SKU even if your SKU does not support it.**</span></span> <span data-ttu-id="85628-287">因此，請確定已選取所有核心大小。</span><span class="sxs-lookup"><span data-stu-id="85628-287">Hence ensure that all the core sizes are selected.</span></span>
    
    ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.1_11.png)
12. <span data-ttu-id="85628-289">第 3 頁會顯示市場/區域。</span><span class="sxs-lookup"><span data-stu-id="85628-289">Page 3 displays the markets/regions.</span></span> <span data-ttu-id="85628-290">按一下 [全部切換] 按鈕以選取所有區域，或手動選取區域的方塊。</span><span class="sxs-lookup"><span data-stu-id="85628-290">Click the **Toggle All** button to select all regions or manually check the boxes for region.</span></span> <span data-ttu-id="85628-291">按一下 [->] 按鈕移至下一頁。</span><span class="sxs-lookup"><span data-stu-id="85628-291">Click on the “->” button to move to the next page.</span></span> <span data-ttu-id="85628-292">**注意：**「Microsoft 免稅國家/地區」以房屋形狀的符號表示。</span><span class="sxs-lookup"><span data-stu-id="85628-292">**Note:** Microsoft Tax Remitted Countries are denoted by a house like symbol.</span></span> <span data-ttu-id="85628-293">如需詳細資訊，請參閱此頁面的＜SKU 的銷往國家/地區＞一節。</span><span class="sxs-lookup"><span data-stu-id="85628-293">For more details please refer to the section “Sell-to” countries of the SKU of this page.</span></span>
    
    ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.1_12.png)
13. <span data-ttu-id="85628-295">第 4 頁會顯示匯率。</span><span class="sxs-lookup"><span data-stu-id="85628-295">Page 4 displays the exchange rates.</span></span> <span data-ttu-id="85628-296">按一下 [完成] 按鈕以完成步驟。</span><span class="sxs-lookup"><span data-stu-id="85628-296">Click on the finish button to complete the steps.</span></span>

### <a name="212-how-to-setup-byol-pricing-model-for-a-sku"></a><span data-ttu-id="85628-297">2.1.2 如何設定 SKU 的 BYOL 定價模式</span><span class="sxs-lookup"><span data-stu-id="85628-297">2.1.2 How to setup BYOL pricing model for a SKU</span></span>
<span data-ttu-id="85628-298">請依照下列步驟來設定 SKU 的 BYOL 定價模式︰</span><span class="sxs-lookup"><span data-stu-id="85628-298">Please follow the steps given below to setup BYOL pricing model for a SKU:</span></span>

1. <span data-ttu-id="85628-299">登入 [發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="85628-299">Login to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="85628-300">瀏覽至 [虛擬機器]  索引標籤並選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="85628-300">Navigate to the **VIRTUAL MACHINES** tab and select your offer.</span></span>
3. <span data-ttu-id="85628-301">從左側功能表，按一下 [SKU]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="85628-301">From the left hand side menu, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="85628-302">請確定 SKU 標示為「自備授權 SKU」。</span><span class="sxs-lookup"><span data-stu-id="85628-302">Ensure that the SKU is marked as “Bring your own license SKU”.</span></span> <span data-ttu-id="85628-303">如果不是，請按一下 [編輯] 按鈕來還原計費模式。</span><span class="sxs-lookup"><span data-stu-id="85628-303">If not, then click on the EDIT button to revert the billing model.</span></span> <span data-ttu-id="85628-304">隨即開啟一個視窗。</span><span class="sxs-lookup"><span data-stu-id="85628-304">A window will open.</span></span> <span data-ttu-id="85628-305">核取 [計費與授權於 Azure 外部進行 (亦即自備授權)] 核取方塊並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="85628-305">Check the checkbox ‘Billing and licensing is done externally from Azure (aka Bring Your Own License)’ and save the changes.</span></span>
   
   ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.2_04.png)
5. <span data-ttu-id="85628-307">從左側功能表，按一下 [價格]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="85628-307">From the left hand side menu, click the **PRICING** tab.</span></span>
6. <span data-ttu-id="85628-308">選取您的基本區域，在 [外部授權的 (BYOL) SKU 可用性] 區段下方核取該 SKU 的核取方塊，以在該區域公開發行 SKU (請參閱以下螢幕擷取畫面)。</span><span class="sxs-lookup"><span data-stu-id="85628-308">Select your base region and make the SKU available in the region by checking the checkbox against the SKU under the section EXTERNALLY-LICENSED (BYOL) SKU AVAILABILITY (see the screenshot below).</span></span>
   
   ![繪圖](media/marketplace-publishing-push-to-staging/img2.1.2_06.png)
7. <span data-ttu-id="85628-310">您可以手動設定於其他區域公開發行 SKU，也可以使用「自動定價」精靈來設定。</span><span class="sxs-lookup"><span data-stu-id="85628-310">Make the SKU available in the other regions manually or you can use the AUTOPRICE wizard for this purpose.</span></span> <span data-ttu-id="85628-311">請參閱此頁面的 **2.1.1 如何設定 SKU 的每小時定價模式** 一節，其中第 9 到 13 點說明「自動定價」精靈的使用方式。</span><span class="sxs-lookup"><span data-stu-id="85628-311">Refer to the points #9 to #13 (which explains the use of the AUTOPRICE wizard) in the section **“2.1.1 How to setup Hourly pricing model for a SKU”** of this page.</span></span>

### <a name="22-set-your-developer-service-prices"></a><span data-ttu-id="85628-312">2.2.</span><span class="sxs-lookup"><span data-stu-id="85628-312">2.2.</span></span> <span data-ttu-id="85628-313">設定開發人員服務價格</span><span class="sxs-lookup"><span data-stu-id="85628-313">Set your Developer service prices</span></span>
<span data-ttu-id="85628-314">方案可以是基本 + 耗用量的任意組合，其中基本是每月價格，而超額部分是每次使用付費價格</span><span class="sxs-lookup"><span data-stu-id="85628-314">Plans can be any combination of base + consumption, where base is the monthly price and overage is the pay-per-use price.</span></span> <span data-ttu-id="85628-315">(詳細資訊請見下文)。</span><span class="sxs-lookup"><span data-stu-id="85628-315">(See below for more details.)</span></span>

<span data-ttu-id="85628-316">**範例：**Contoso 開發人員服務供應項目</span><span class="sxs-lookup"><span data-stu-id="85628-316">**Example:**  Contoso developer service offering</span></span>

| <span data-ttu-id="85628-317">規劃</span><span class="sxs-lookup"><span data-stu-id="85628-317">Plan</span></span> | <span data-ttu-id="85628-318">價格</span><span class="sxs-lookup"><span data-stu-id="85628-318">Price</span></span> | <span data-ttu-id="85628-319">包括</span><span class="sxs-lookup"><span data-stu-id="85628-319">Includes</span></span> | <span data-ttu-id="85628-320">移轉路徑</span><span class="sxs-lookup"><span data-stu-id="85628-320">Migration path</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="85628-321">免費</span><span class="sxs-lookup"><span data-stu-id="85628-321">Free</span></span> |<span data-ttu-id="85628-322">$0 美元/月</span><span class="sxs-lookup"><span data-stu-id="85628-322">$0/month</span></span> |<span data-ttu-id="85628-323">基本功能。</span><span class="sxs-lookup"><span data-stu-id="85628-323">Basic functionality.</span></span> |<span data-ttu-id="85628-324">可以移轉至其他方案</span><span class="sxs-lookup"><span data-stu-id="85628-324">Can migrate to any other plan</span></span> |
| <span data-ttu-id="85628-325">Bronze</span><span class="sxs-lookup"><span data-stu-id="85628-325">Bronze</span></span> |<span data-ttu-id="85628-326">$10 美元/月</span><span class="sxs-lookup"><span data-stu-id="85628-326">$10/month</span></span> |<span data-ttu-id="85628-327">基本功能和 1,000 個功能 X 的配額。</span><span class="sxs-lookup"><span data-stu-id="85628-327">Basic functionality and a quota of 1,000 of feature X.</span></span> |<span data-ttu-id="85628-328">可以移轉至 Bronze Plus、Silver 和 Gold 方案</span><span class="sxs-lookup"><span data-stu-id="85628-328">Can migrate to Bronze Plus, Silver, and Gold plans</span></span> |
| <span data-ttu-id="85628-329">Bronze Plus</span><span class="sxs-lookup"><span data-stu-id="85628-329">Bronze Plus</span></span> |<span data-ttu-id="85628-330">免費試用期間：$0 美元/月 + $0 美元/meter01</span><span class="sxs-lookup"><span data-stu-id="85628-330">Free trial period: $0/month + $0/meter01</span></span> |<span data-ttu-id="85628-331">基本功能和 10,000 個功能 X 的配額。功能 X 配額用完時，客戶可以透過 meter01，依每次使用付費。</span><span class="sxs-lookup"><span data-stu-id="85628-331">Basic functionality and a quota of 10,000 of feature X.  Once feature X quota is used, the customer can pay per use via meter01.</span></span> |<span data-ttu-id="85628-332">可以移轉至 Silver Plus 和 Gold 方案</span><span class="sxs-lookup"><span data-stu-id="85628-332">Can migrate to Silver Plus and Gold plans</span></span> |
| <span data-ttu-id="85628-333">Bronze Plus</span><span class="sxs-lookup"><span data-stu-id="85628-333">Bronze Plus</span></span> |<span data-ttu-id="85628-334">付費期間 (也稱為</span><span class="sxs-lookup"><span data-stu-id="85628-334">Paid period (a.k.a.</span></span> <span data-ttu-id="85628-335">免費試用版已過期)：$10/每月 + $0.05/meter01</span><span class="sxs-lookup"><span data-stu-id="85628-335">free trial expired): $10/month + $0.05/meter01</span></span> |<span data-ttu-id="85628-336">基本功能和 10,000 個功能 X 的配額。功能 X 配額用完時，客戶可以透過 meter01，依每次使用付費。</span><span class="sxs-lookup"><span data-stu-id="85628-336">Basic functionality and a quota of 10,000 of feature X.  Once feature X quota is used, the customer can pay per use via meter01.</span></span> |<span data-ttu-id="85628-337">可以移轉至 Silver Plus 和 Gold 方案</span><span class="sxs-lookup"><span data-stu-id="85628-337">Can migrate to Silver Plus and Gold plans</span></span> |
| <span data-ttu-id="85628-338">Silver</span><span class="sxs-lookup"><span data-stu-id="85628-338">Silver</span></span> |<span data-ttu-id="85628-339">$0.15 美元/meter01</span><span class="sxs-lookup"><span data-stu-id="85628-339">$0.15/meter01</span></span> |<span data-ttu-id="85628-340">客戶可以透過 meter01 (適用於 X 功能)，依每次使用付費。</span><span class="sxs-lookup"><span data-stu-id="85628-340">The customer can pay per use via meter01, which is for feature X.</span></span> |<span data-ttu-id="85628-341">可以移轉至 Bronze 和 Gold 方案</span><span class="sxs-lookup"><span data-stu-id="85628-341">Can migrate to Bronze and Gold plans</span></span> |
| <span data-ttu-id="85628-342">Silver Plus</span><span class="sxs-lookup"><span data-stu-id="85628-342">Silver Plus</span></span> |<span data-ttu-id="85628-343">$20 美元/月 + $0.15 美元/meter01 + $0.01 美元/meter02</span><span class="sxs-lookup"><span data-stu-id="85628-343">$20/month + $0.15/meter01 + $0.01/meter02</span></span> |<span data-ttu-id="85628-344">基本功能及 10,000 個功能 X 和 100 個功能 Y 的配額。功能 X 配額用完時，客戶可以透過 meter01，依每次使用付費。</span><span class="sxs-lookup"><span data-stu-id="85628-344">Basic functionality and a quota of 10,000 of feature X and 100 of feature Y.  Once the feature X quota is used, the customer can pay per use via meter01.</span></span>  <span data-ttu-id="85628-345">功能 Y 配額用完時，客戶可以透過 meter02，依每次使用付費。</span><span class="sxs-lookup"><span data-stu-id="85628-345">Once the feature Y quota is used, the customer can pay per use via meter02.</span></span> |<span data-ttu-id="85628-346">可以移轉至 Bronze Plus 和 Gold 方案</span><span class="sxs-lookup"><span data-stu-id="85628-346">Can migrate to Bronze Plus and Gold plans</span></span> |
| <span data-ttu-id="85628-347">Gold</span><span class="sxs-lookup"><span data-stu-id="85628-347">Gold</span></span> |<span data-ttu-id="85628-348">$1000 美元/月</span><span class="sxs-lookup"><span data-stu-id="85628-348">$1,000/month</span></span> |<span data-ttu-id="85628-349">10,000 個功能 X、1,000 個功能 Y 和無限制的功能 Z 的配額。</span><span class="sxs-lookup"><span data-stu-id="85628-349">Quota of 10,000 of feature X, 1,000 of feature Y, and unlimited of feature Z.</span></span> |<span data-ttu-id="85628-350">可以移轉至所有方案，免費除外</span><span class="sxs-lookup"><span data-stu-id="85628-350">Can migrate to all plans except free</span></span> |

## <a name="step-3-provide-support-information"></a><span data-ttu-id="85628-351">步驟 3：提供支援資訊</span><span class="sxs-lookup"><span data-stu-id="85628-351">Step 3: Provide support information</span></span>
<span data-ttu-id="85628-352">合約詳細資料僅用於合作夥伴與 Microsoft 之間的內部通訊。</span><span class="sxs-lookup"><span data-stu-id="85628-352">The contact details are used for internal communications between the partner and Microsoft only.</span></span> <span data-ttu-id="85628-353">支援 URL 可供一般客戶使用。</span><span class="sxs-lookup"><span data-stu-id="85628-353">The support URL will be available to the end customers.</span></span>

1. <span data-ttu-id="85628-354">移至發佈入口網站左側的 [支援]  標題。</span><span class="sxs-lookup"><span data-stu-id="85628-354">Go to the **Support** heading on the left side of the publishing portal.</span></span>
2. <span data-ttu-id="85628-355">在 [工程連絡人] 下方輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="85628-355">Enter information under **Engineering Contact**.</span></span>
3. <span data-ttu-id="85628-356">在 [客戶支援] 下方輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="85628-356">Enter information under **Customer Support**.</span></span> <span data-ttu-id="85628-357">如果您只提供電子郵件支援，請輸入虛設的電話號碼，該內容會改用您提供的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="85628-357">If you provide only email support, enter a dummy phone number, and your provided email will be used instead.</span></span>
4. <span data-ttu-id="85628-358">輸入支援 URL。</span><span class="sxs-lookup"><span data-stu-id="85628-358">Enter the support URL.</span></span>

## <a name="step-4-choose-azure-marketplace-categories"></a><span data-ttu-id="85628-359">步驟 4：選擇 Azure Marketplace 類別</span><span class="sxs-lookup"><span data-stu-id="85628-359">Step 4: Choose Azure Marketplace categories</span></span>
<span data-ttu-id="85628-360">[類別]  索引標籤會提供選取項目的陣列。</span><span class="sxs-lookup"><span data-stu-id="85628-360">The **Categories** tab provides an array of selections.</span></span> <span data-ttu-id="85628-361">您的優惠可能會落在這些選取項目中，而且您最多可選取五個類別。</span><span class="sxs-lookup"><span data-stu-id="85628-361">Your offer may fall under these, and you may select up to five categories.</span></span>

## <a name="how-your-marketing-will-appear"></a><span data-ttu-id="85628-362">行銷活動的呈現方式</span><span class="sxs-lookup"><span data-stu-id="85628-362">How your marketing will appear</span></span>
<span data-ttu-id="85628-363">以下是如何在 [Azure Marketplace 網站](https://azure.microsoft.com/marketplace/)上和 [Azure 入口網站](https://portal.azure.com)中使用供應項目行銷資訊的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="85628-363">Below is a detailed view of how the offer marketing information is used on the [Azure Marketplace website](https://azure.microsoft.com/marketplace/) and in the [Azure portal](https://portal.azure.com).</span></span>

### <a name="azure-marketplace-website"></a><span data-ttu-id="85628-364">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="85628-364">Azure Marketplace website</span></span>
![繪圖](media/marketplace-publishing-push-to-staging/acom-catalog-01.png)

![繪圖](media/marketplace-publishing-push-to-staging/acom-catalog-02.png)

<span data-ttu-id="85628-367">*Azure.com Marketplace 網站上的優惠清單*</span><span class="sxs-lookup"><span data-stu-id="85628-367">*Listing of offers on the Azure Marketplace website*</span></span>

![繪圖](media/marketplace-publishing-push-to-staging/acom-listing-details-01.png)

<span data-ttu-id="85628-369">*Azure.com Marketplace 網站上的優惠描述詳細資料*</span><span class="sxs-lookup"><span data-stu-id="85628-369">*Offer description details on the Azure Marketplace website*</span></span>

![繪圖](media/marketplace-publishing-push-to-staging/acom-listing-details-02.png)

<span data-ttu-id="85628-371">*Azure.com Marketplace 網站上的優惠定價詳細資料*</span><span class="sxs-lookup"><span data-stu-id="85628-371">*Offer description pricing details on the Azure Marketplace website*</span></span>

### <a name="azure-portal"></a><span data-ttu-id="85628-372">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="85628-372">Azure Portal</span></span>
![繪圖](media/marketplace-publishing-push-to-staging/azureportal-galleryblade-01.png)

<span data-ttu-id="85628-374">*Azure 入口網站中的優惠清單*</span><span class="sxs-lookup"><span data-stu-id="85628-374">*Listing of offers in the Azure Portal*</span></span>

![繪圖](media/marketplace-publishing-push-to-staging/azureportal-galleryblade-02.png)

<span data-ttu-id="85628-376">*Azure 入口網站中的優惠描述詳細資料*</span><span class="sxs-lookup"><span data-stu-id="85628-376">*Offer description details in the Azure portal*</span></span>

## <a name="next-steps"></a><span data-ttu-id="85628-377">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85628-377">Next steps</span></span>
<span data-ttu-id="85628-378">既然已載入您的 Marketplace 內容，讓我們繼續在預備環境中測試您的優惠。</span><span class="sxs-lookup"><span data-stu-id="85628-378">Now that your Marketplace content is loaded, let's move forward with testing your offer in staging.</span></span> <span data-ttu-id="85628-379">不過，您必須從下列清單選取適當的優惠類型，因為步驟會隨著優惠類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="85628-379">However, you must select the appropriate offer type from the list below, as steps vary by offer type.</span></span>

* [<span data-ttu-id="85628-380">在預備環境中測試您的 VM 優惠</span><span class="sxs-lookup"><span data-stu-id="85628-380">Test your VM offer in staging</span></span>](marketplace-publishing-vm-image-test-in-staging.md)
* [<span data-ttu-id="85628-381">在預備環境中測試您的解決方案範本供應項目</span><span class="sxs-lookup"><span data-stu-id="85628-381">Test your Solution template offer in staging</span></span>](marketplace-publishing-solution-template-test-in-staging.md)

## <a name="see-also"></a><span data-ttu-id="85628-382">另請參閱</span><span class="sxs-lookup"><span data-stu-id="85628-382">See also</span></span>
* [<span data-ttu-id="85628-383">使用者入門：如何將供應項目發佈至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="85628-383">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-map-acom]:media/marketplace-publishing-push-to-staging/pubportal-mapping-acom.jpg
[img-map-portal]:media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg
[img-map-link]:media/marketplace-publishing-push-to-staging/marketing-content-guide-links.jpg
[img-map-logo]:media/marketplace-publishing-push-to-staging/marketing-content-guide-logos.jpg
[img-map-title]:media/marketplace-publishing-push-to-staging/marketing-content-guide-publisher-offer.png

[link-pubportal]:https://publish.windowsazure.com
[link-push-to-production]:marketplace-publishing-push-to-production.md
