---
title: "Azure Active Directory B2C︰使用語言自訂 | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: 3c7c49ee5fbd98762da0eef6f02e7c2f036453cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a><span data-ttu-id="ffbf2-102">Azure Active Directory B2C︰使用語言自訂</span><span class="sxs-lookup"><span data-stu-id="ffbf2-102">Azure Active Directory B2C: Using language customization</span></span>

>[!NOTE] 
><span data-ttu-id="ffbf2-103">這項功能處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-103">This feature is in public preview.</span></span>  <span data-ttu-id="ffbf2-104">建議您在使用這項功能時，使用測試租用戶。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-104">It is recommended that you use a test tenant when using this feature.</span></span>  <span data-ttu-id="ffbf2-105">預覽版在進入到公開上市版時應該不會有重大變更，但我們保留進行這類變更以便改進功能的權利。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-105">We don't plan on any breaking changes from the preview to the general availability release, but we reserve the right to make such changes to improve the feature.</span></span>  <span data-ttu-id="ffbf2-106">在您有機會試用功能後，請將關於使用體驗及如何讓它更加完善的意見提供給我們。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-106">Once you've had a chance to try feature, please provide feedback on your experiences and how we can make it better.</span></span>  <span data-ttu-id="ffbf2-107">您可以透過 Azure 入口網站右上方的笑臉圖示工具來提供意見。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-107">You can provide feedback through the Azure portal with the smiley face tool on the top right.</span></span>   <span data-ttu-id="ffbf2-108">如果您在預覽期間因為有商務需求而需要正式上線使用這項功能，請讓我們知道您的情況，以便我們能為您提供適當的指引與協助。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-108">If there is a business requirement for you to go live using this feature during the preview phase, let us know your scenarios and we can provide you with the proper guidance and assistance.</span></span>  <span data-ttu-id="ffbf2-109">您可以透過 [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com) 來與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-109">You can contact us at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>

<span data-ttu-id="ffbf2-110">語言自訂可讓您將使用者旅程變更為不同語言，以符合您客戶的需求。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-110">Language customization allows you to change your user journey to a different language to suit your customer needs.</span></span>  <span data-ttu-id="ffbf2-111">我們提供 36 種語言的翻譯 (請參閱[其他資訊](#additional-information))。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-111">We provide translations for 36 languages (see [Additional information](#additional-information)).</span></span>  <span data-ttu-id="ffbf2-112">即使您的體驗僅提供單一語言，您也可以自訂頁面上的任何文字以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-112">Even if your experience is only provided for a single language, you can customize any text on the pages to suit your needs.</span></span>  

## <a name="how-does-language-customization-work"></a><span data-ttu-id="ffbf2-113">語言自訂的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="ffbf2-113">How does Language customization work?</span></span>
<span data-ttu-id="ffbf2-114">語言自訂可讓您選取使用者旅程所適用的語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-114">Language customization allows you to select which languages your user journey is available in.</span></span>  <span data-ttu-id="ffbf2-115">此功能啟用後，您就可以從應用程式提供查詢字串參數 ui_locales。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-115">Once the feature is enabled, you can provide the query string parameter, ui_locales, from your application.</span></span>  <span data-ttu-id="ffbf2-116">當您呼叫 Azure AD B2C 時，我們會將您的頁面轉譯為您指定的地區設定。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-116">When you call into Azure AD B2C, we translate your page to the locale that you have indicated.</span></span>  <span data-ttu-id="ffbf2-117">使用組態類型可讓您完整控制使用者旅程的語言，並忽略客戶瀏覽器的語言設定。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-117">Using type of configuration gives you complete control over the languages in your user journey and ignores the language settings of the customer's browser.</span></span> <span data-ttu-id="ffbf2-118">或者，您也可能不需要對客戶會看見哪種語言擁有這種程度的控制力。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-118">Alternatively, you may not need that level of control over what languages your customer see.</span></span>  <span data-ttu-id="ffbf2-119">如果您沒有提供 ui_locales 參數，則客戶的使用體驗會由其瀏覽器的設定來決定。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-119">If you don't provide a ui_locales parameter, the customer's experience is dictated by their browser's settings.</span></span>  <span data-ttu-id="ffbf2-120">您仍可將各種語言新增為支援的語言，以控制要將使用者旅程轉譯為何種語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-120">You can still control which languages your user journey is translated to by adding it as a supported language.</span></span>  <span data-ttu-id="ffbf2-121">如果客戶瀏覽器所設定要顯示的語言不是您想要支援的語言，則系統會改為顯示您選取作為支援之文化特性預設值的語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-121">If a customer's browser is set to show a language you don't want to support, then the language you selected as a default in supported cultures is shown instead.</span></span>

1. <span data-ttu-id="ffbf2-122">**ui_locales 所指定的語言** - 在啟用語言自訂後，您的使用者旅程會轉譯為此處指定的語言</span><span class="sxs-lookup"><span data-stu-id="ffbf2-122">**ui-locales specified language** - Once you enable Language customization, your user journey is translated to the language specified here</span></span>
2. <span data-ttu-id="ffbf2-123">**瀏覽器所要求的語言** - 如果未指定 ui_locales，則語言會轉譯為瀏覽器所要求的語言 (**如果支援的語言中有包括此語言**)</span><span class="sxs-lookup"><span data-stu-id="ffbf2-123">**Browser requested language** - If no ui-locales was specified, it translates to the browser requested language, **if it was included in Supported languages**</span></span>
3. <span data-ttu-id="ffbf2-124">**原則的預設語言** - 如果瀏覽器未指定語言，或指定不支援的語言，語言就會轉譯為原則的預設語言</span><span class="sxs-lookup"><span data-stu-id="ffbf2-124">**Policy default language** - If the browser doesn't specify a language, or it specifies one that is not supported, it translates to the policy default language</span></span>

>[!NOTE]
><span data-ttu-id="ffbf2-125">如果您使用自訂使用者屬性，則必須提供自己的翻譯。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-125">If you are using custom user attributes, you need to provide your own translations.</span></span> <span data-ttu-id="ffbf2-126">如需詳細資訊，請參閱[自訂您的字串](#customize-your-strings)。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-126">See '[Customize your strings](#customize-your-strings)' for details.</span></span>
>

## <a name="support-uilocales-requested-languages"></a><span data-ttu-id="ffbf2-127">支援 ui_locales 所要求的語言</span><span class="sxs-lookup"><span data-stu-id="ffbf2-127">Support ui_locales requested languages</span></span> 
<span data-ttu-id="ffbf2-128">藉由對原則啟用「語言自訂」，您現在可以藉由新增 ui_locales 參數來控制使用者旅程的語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-128">By enabling 'Language customization' on a policy, you can now control the language of the user journey by adding the ui_locales parameter.</span></span>
1. [<span data-ttu-id="ffbf2-129">遵循下列步驟以瀏覽至 Azure 入口網站上的 B2C 功能刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-129">Follow these steps to navigate to the B2C features blade on the Azure portal.</span></span>](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. <span data-ttu-id="ffbf2-130">瀏覽至您想要啟用轉譯的原則。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-130">Navigate to a policy that you want to enable for translations.</span></span>
3. <span data-ttu-id="ffbf2-131">按一下 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-131">Click **Language customization**.</span></span>
4. <span data-ttu-id="ffbf2-132">仔細閱讀警告文字。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-132">Read the warning carefully.</span></span>  <span data-ttu-id="ffbf2-133">啟用之後，您就無法關閉「語言自訂」。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-133">Once enabled, you cannot turn off 'Language customization'.</span></span>
5. <span data-ttu-id="ffbf2-134">開啟該功能，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-134">Turn on the feature and click **OK**.</span></span>
6. <span data-ttu-id="ffbf2-135">在 [編輯原則] 刀鋒視窗的左上角儲存您的原則。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-135">Save your policy on the upper left corner of your **Edit policy** blade.</span></span>

## <a name="select-which-languages-your-user-journey-supports"></a><span data-ttu-id="ffbf2-136">選取您的使用者旅程所支援的語言</span><span class="sxs-lookup"><span data-stu-id="ffbf2-136">Select which languages your user journey supports</span></span> 
<span data-ttu-id="ffbf2-137">建立允許語言清單，以供使用者旅程在您未提供 ui_locales 參數時可進行轉譯。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-137">Create a list of allowed languages for your user journey to be translated in when the ui_locales parameter is not provided.</span></span>
1. <span data-ttu-id="ffbf2-138">透過前面的指示來確定您的原則已啟用「語言自訂」。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-138">Ensure your policy has 'Language customization' enabled from previous instructions.</span></span>
2. <span data-ttu-id="ffbf2-139">從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-139">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="ffbf2-140">系統會將您帶往 [支援的語言] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-140">You are taken to your **Supported languages** blade.</span></span>  <span data-ttu-id="ffbf2-141">您可以從這裡選取 [新增語言]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-141">From here, you can select **Add language**.</span></span>
4. <span data-ttu-id="ffbf2-142">選取您想要支援的所有語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-142">Select all the languages that you would like to be supported.</span></span>  

>[!NOTE]
><span data-ttu-id="ffbf2-143">如果您未提供 ui_locales 參數，則頁面會轉譯為客戶的瀏覽器語言 (但前提是該語言有在此清單上)</span><span class="sxs-lookup"><span data-stu-id="ffbf2-143">If a ui_locales parameter is not provided, then the page is translated to the customer's browser language only if it is on this list</span></span>
>

5. <span data-ttu-id="ffbf2-144">按一下底部的 [確定]</span><span class="sxs-lookup"><span data-stu-id="ffbf2-144">Click **Ok** at the bottom</span></span>
6. <span data-ttu-id="ffbf2-145">關閉 [語言自訂] 刀鋒視窗，然後**儲存**原則。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-145">Close the **Language customization** blade and **save** your policy.</span></span>

## <a name="customize-your-strings"></a><span data-ttu-id="ffbf2-146">自訂您的字串</span><span class="sxs-lookup"><span data-stu-id="ffbf2-146">Customize your strings</span></span>
<span data-ttu-id="ffbf2-147">「語言自訂」可讓您自訂使用者旅程中的任何字串。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-147">'Language customization' allows you to customize any string in your user journey.</span></span>
1. <span data-ttu-id="ffbf2-148">透過前面的指示來確定您的原則已啟用「語言自訂」。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-148">Ensure your policy has 'Language customization' enabled from the previous instructions.</span></span>
2. <span data-ttu-id="ffbf2-149">從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-149">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="ffbf2-150">從左側導覽功能表選取 [下載內容]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-150">From the left-hand navigation menu, select **Download content**.</span></span>
4. <span data-ttu-id="ffbf2-151">選取您想要編輯的頁面。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-151">Select the page you want to edit.</span></span>
5. <span data-ttu-id="ffbf2-152">在下拉式清單中，選取您想要編輯的語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-152">In the dropdown, select the language you want to edit for.</span></span>
6. <span data-ttu-id="ffbf2-153">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-153">Click **Download**.</span></span> 

<span data-ttu-id="ffbf2-154">上述步驟會向您提供 JSON 檔案，以供您用來開始編輯字串。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-154">These steps give you a JSON file that you can use to start editing your strings.</span></span>

### <a name="changing-any-string-on-the-page"></a><span data-ttu-id="ffbf2-155">變更頁面上的任何字串</span><span class="sxs-lookup"><span data-stu-id="ffbf2-155">Changing any string on the page</span></span>
1. <span data-ttu-id="ffbf2-156">在 JSON 編輯器中開啟透過前面的指示所下載的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-156">Open the JSON file downloaded from previous instructions in a JSON editor.</span></span>
2. <span data-ttu-id="ffbf2-157">尋找您想要變更的元素。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-157">Find the element you want to change.</span></span>  <span data-ttu-id="ffbf2-158">您可以尋找您要尋找之字串的 `StringId`，或尋找您要變更的 `Value`。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-158">You can find the `StringId` of the string you are looking for, or look for the `Value` you want to change.</span></span>
3. <span data-ttu-id="ffbf2-159">以您想要顯示的內容來更新 `Value` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-159">Update the `Value` attribute with what you want displayed.</span></span>
4. <span data-ttu-id="ffbf2-160">儲存檔案，並上傳您的變更。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-160">Save the file and upload your changes.</span></span>

### <a name="changing-extension-attributes"></a><span data-ttu-id="ffbf2-161">變更擴充屬性</span><span class="sxs-lookup"><span data-stu-id="ffbf2-161">Changing extension attributes</span></span>
<span data-ttu-id="ffbf2-162">如果您想要變更自訂使用者屬性的字串，或想要將字串新增到 JSON 中，它的格式如下︰</span><span class="sxs-lookup"><span data-stu-id="ffbf2-162">If you are looking to change the string for a custom user attribute, or want to add one to the JSON, it is in the following format:</span></span>
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
><span data-ttu-id="ffbf2-163">如果您需要覆寫字串，請務必將 `Override` 值設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-163">If you need to override a string, make sure to set the `Override` value to `true`.</span></span>  <span data-ttu-id="ffbf2-164">如果該值未變更，則系統會忽略您的輸入。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-164">If the value isn't changed, the entry is ignored.</span></span> 
>

<span data-ttu-id="ffbf2-165">以自訂使用者屬性的名稱來取代 `<ExtensionAttribute>`。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-165">Replace `<ExtensionAttribute>` with the name of your custom user attribute.</span></span>  
<span data-ttu-id="ffbf2-166">以要顯示的新字串來取代 `<ExtensionAttributeValue>`。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-166">Replace `<ExtensionAttributeValue>` with the new string to be displayed.</span></span>

### <a name="using-localizedcollections"></a><span data-ttu-id="ffbf2-167">使用 LocalizedCollections</span><span class="sxs-lookup"><span data-stu-id="ffbf2-167">Using LocalizedCollections</span></span>
<span data-ttu-id="ffbf2-168">如果您想要提供設定好的回應值清單，您需要建立 `LocalizedCollections`。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-168">If you want to provide a set list of values for responses, you need to create a `LocalizedCollections`.</span></span>  <span data-ttu-id="ffbf2-169">`LocalizedCollections` 是 `Name` 和 `Value` 的配對陣列。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-169">A `LocalizedCollections` is an array of `Name` and `Value` pairs.</span></span>  <span data-ttu-id="ffbf2-170">`Name` 是所顯示的內容，`Value` 則是宣告中所傳回的內容。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-170">The `Name` is what is displayed and the `Value` is what is returned in the claim.</span></span>  <span data-ttu-id="ffbf2-171">若要新增 `LocalizedCollections`，其格式如下︰</span><span class="sxs-lookup"><span data-stu-id="ffbf2-171">To add a `LocalizedCollections`, it has the following format:</span></span>

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
><span data-ttu-id="ffbf2-172">如果您需要覆寫字串，請務必將 `Override` 值設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-172">If you need to override a string, make sure to set the `Override` value to `true`.</span></span>  <span data-ttu-id="ffbf2-173">如果該值未變更，則系統會忽略您的輸入。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-173">If the value isn't changed, the entry is ignored.</span></span> 
>

* <span data-ttu-id="ffbf2-174">`ElementId` 是使用者屬性，而其回應則是這個 `LocalizedCollections`</span><span class="sxs-lookup"><span data-stu-id="ffbf2-174">`ElementId` is the user attribute that this `LocalizedCollections` is a response to</span></span>
* <span data-ttu-id="ffbf2-175">`Name` 是向使用者顯示的值</span><span class="sxs-lookup"><span data-stu-id="ffbf2-175">`Name` is the value shown to the user</span></span>
* <span data-ttu-id="ffbf2-176">`Value` 是選取此選項時在宣告中所傳回的內容</span><span class="sxs-lookup"><span data-stu-id="ffbf2-176">`Value` is what is returned in the claim when this option is selected</span></span>

### <a name="upload-your-changes"></a><span data-ttu-id="ffbf2-177">上傳您的變更</span><span class="sxs-lookup"><span data-stu-id="ffbf2-177">Upload your changes</span></span>
1. <span data-ttu-id="ffbf2-178">對 JSON 檔案變更完成後，請瀏覽回到 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-178">Once you have completed the changes to your JSON file, navigate back to your B2C tenant.</span></span>
2. <span data-ttu-id="ffbf2-179">從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-179">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="ffbf2-180">從左側導覽功能表選取 [上傳內容]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-180">From the left-hand navigation menu, select **Upload content**.</span></span>
4. <span data-ttu-id="ffbf2-181">選取您要上傳其變更的頁面。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-181">Select the page you want to upload your changes for.</span></span>
5. <span data-ttu-id="ffbf2-182">如果您要上傳的語言先前已提供過 JSON，您必須刪除先前的項目。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-182">If you want to upload a language that you've previously provided a JSON for, you need to delete the previous entry.</span></span>  <span data-ttu-id="ffbf2-183">您可以按一下該語言右側的 `...`，然後選取 [刪除] 來加以刪除。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-183">You can delete it by clicking the `...` on the right of that language and select **Delete**.</span></span>
6. <span data-ttu-id="ffbf2-184">按一下左上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-184">Click **Add** on the upper left.</span></span>
7. <span data-ttu-id="ffbf2-185">選取 JSON 檔案的語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-185">Select the language of your JSON file.</span></span>
8. <span data-ttu-id="ffbf2-186">按一下右邊的資料夾按鈕並瀏覽您的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-186">Click the folder button on the right and browse for your JSON file.</span></span>
9. <span data-ttu-id="ffbf2-187">按一下刀鋒視窗底部的 [上傳] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-187">Click the **Upload** button on the bottom of the blade.</span></span>
10. <span data-ttu-id="ffbf2-188">返回 [編輯原則] 刀鋒視窗，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-188">Go back to your **Edit policy** blade and click **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="ffbf2-189">其他資訊</span><span class="sxs-lookup"><span data-stu-id="ffbf2-189">Additional information</span></span>
### <a name="recommendations-for-language-customization"></a><span data-ttu-id="ffbf2-190">「語言自訂」的建議</span><span class="sxs-lookup"><span data-stu-id="ffbf2-190">Recommendations for 'Language customization'</span></span>
<span data-ttu-id="ffbf2-191">我們建議您只將輸入項目放入您明確要取代之字串的語言資源內。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-191">We recommend only putting in entries to your Language resources for strings you explicitly want to replace.</span></span>  <span data-ttu-id="ffbf2-192">我們對於出自您所有 JSON 翻譯的編譯檔案大小套用了強制的限制。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-192">We enforce a size limit to the file that is compiled out of all your JSON translations.</span></span>  <span data-ttu-id="ffbf2-193">過大的檔案會影響使用者旅程的效能。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-193">If your files get too large, it impacts the performance of your user journey.</span></span>
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a><span data-ttu-id="ffbf2-194">「語言自訂」啟用後，系統就會移除頁面 UI 自訂標籤</span><span class="sxs-lookup"><span data-stu-id="ffbf2-194">Page UI customization labels are removed once 'Language customization' is enabled</span></span>
<span data-ttu-id="ffbf2-195">當您啟用「語言自訂」時，系統會移除您先前使用頁面 UI 自訂對標籤所進行的編輯，但自訂使用者屬性除外。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-195">When you enable 'Language customization', your previous edits for labels using Page UI customization are removed except for custom user attributes.</span></span>  <span data-ttu-id="ffbf2-196">進行這項變更是為了避免您可以在其中編輯字串的位置發生衝突。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-196">This change is done to avoid conflicts in where you can edit your strings.</span></span>  <span data-ttu-id="ffbf2-197">您可以上傳「語言自訂」中的語言資源，來繼續變更您的標籤和其他字串。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-197">You can continue to change your labels and other strings by uploading language resources in 'Language customization'.</span></span>
### <a name="microsoft-is-committed-to-provide-the-most-up-to-date-translations-for-your-use"></a><span data-ttu-id="ffbf2-198">Microsoft 致力於提供最新的翻譯來供您使用</span><span class="sxs-lookup"><span data-stu-id="ffbf2-198">Microsoft is committed to provide the most up-to-date translations for your use</span></span>
<span data-ttu-id="ffbf2-199">我們會持續改善翻譯，並讓它們符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-199">We will continuously improve translations and keep them in compliance for you.</span></span>  <span data-ttu-id="ffbf2-200">我們會找出全域術語中的錯誤和變更，並製作可在使用者旅程中順暢運作的更新。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-200">We will identify bugs and changes in global terminology and make the updates that will work seamlessly in your user journey.</span></span>
### <a name="support-for-right-to-left-languages"></a><span data-ttu-id="ffbf2-201">支援從右至左的語言</span><span class="sxs-lookup"><span data-stu-id="ffbf2-201">Support for right-to-left languages</span></span>
<span data-ttu-id="ffbf2-202">不支援由右至左的語言，如果您需要此功能，請在 [Azure 意見反應](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag)投票給這項功能。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-202">There is no support for right-to-left languages, if you require this feature please vote for this feature on [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).</span></span>
### <a name="social-identity-provider-translations"></a><span data-ttu-id="ffbf2-203">社交識別提供者的翻譯</span><span class="sxs-lookup"><span data-stu-id="ffbf2-203">Social Identity provider translations</span></span>
<span data-ttu-id="ffbf2-204">我們為社交登入提供了 ui_locales OIDC 參數，但某些社交識別提供者 (包括 Facebook 和 Google) 並未加以採用。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-204">We provide the ui_locales OIDC parameter to social logins but they are not honored by some social identity providers, including Facebook and Google.</span></span> 
### <a name="browser-behavior"></a><span data-ttu-id="ffbf2-205">瀏覽器行為</span><span class="sxs-lookup"><span data-stu-id="ffbf2-205">Browser behavior</span></span>
<span data-ttu-id="ffbf2-206">Chrome 和 Firefox 皆會要求自設的語言，如果該語言受支援，則會顯示該語言而不會顯示預設語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-206">Chrome and Firefox both request for their set language and if it is a supported language, it is displayed before the default.</span></span>  <span data-ttu-id="ffbf2-207">Edge 目前未要求語言，而是會直接使用預設語言。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-207">Edge currently does not request a language and goes straight to the default language.</span></span>
### <a name="known-issues"></a><span data-ttu-id="ffbf2-208">已知問題</span><span class="sxs-lookup"><span data-stu-id="ffbf2-208">Known issues</span></span>
* <span data-ttu-id="ffbf2-209">您目前無法在設定檔編輯原則中上傳 MFA 頁面的語言資源。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-209">Uploading language resources for the MFA page in a Profile Edit policy is currently unavailable.</span></span>
* <span data-ttu-id="ffbf2-210">若要求者為回應類型，系統就不會為值產生 `LocalizedCollections`</span><span class="sxs-lookup"><span data-stu-id="ffbf2-210">`LocalizedCollections` aren't generated for values when it is required by the response type</span></span>
### <a name="what-if-i-want-a-language-that-isnt-supported"></a><span data-ttu-id="ffbf2-211">如果我想使用的語言不受支援會如何？</span><span class="sxs-lookup"><span data-stu-id="ffbf2-211">What if I want a language that isn't supported?</span></span>
<span data-ttu-id="ffbf2-212">我們打算提供這項功能的擴充功能，以讓您向「自訂語言」上傳 JSON 資源。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-212">We are planning to provide an extension of this feature that allows you to upload a JSON resource towards 'custom languages'.</span></span>  <span data-ttu-id="ffbf2-213">此功能可讓您指定任何語言的名稱和語言代碼，並提供該語言的「所有」翻譯。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-213">The feature allows you to specify the name and language code for any language and provide *all* the translations for that language.</span></span>  <span data-ttu-id="ffbf2-214">如果您需要這項功能，請將您的情況傳送給我們：[aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ffbf2-214">If you need this feature, send us your scenario at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>  

### <a name="what-languages-are-supported"></a><span data-ttu-id="ffbf2-215">支援哪些語言？</span><span class="sxs-lookup"><span data-stu-id="ffbf2-215">What languages are supported?</span></span>

| <span data-ttu-id="ffbf2-216">語言</span><span class="sxs-lookup"><span data-stu-id="ffbf2-216">Language</span></span>              | <span data-ttu-id="ffbf2-217">語言代碼</span><span class="sxs-lookup"><span data-stu-id="ffbf2-217">Language code</span></span> |
|-----------------------|---------------|
| <span data-ttu-id="ffbf2-218">孟加拉文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-218">Bangla</span></span>                | <span data-ttu-id="ffbf2-219">bn</span><span class="sxs-lookup"><span data-stu-id="ffbf2-219">bn</span></span>            |
| <span data-ttu-id="ffbf2-220">捷克文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-220">Czech</span></span>                 | <span data-ttu-id="ffbf2-221">cs</span><span class="sxs-lookup"><span data-stu-id="ffbf2-221">cs</span></span>            |
| <span data-ttu-id="ffbf2-222">丹麥文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-222">Danish</span></span>                | <span data-ttu-id="ffbf2-223">da</span><span class="sxs-lookup"><span data-stu-id="ffbf2-223">da</span></span>            |
| <span data-ttu-id="ffbf2-224">德文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-224">German</span></span>                | <span data-ttu-id="ffbf2-225">de</span><span class="sxs-lookup"><span data-stu-id="ffbf2-225">de</span></span>            |
| <span data-ttu-id="ffbf2-226">希臘文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-226">Greek</span></span>                 | <span data-ttu-id="ffbf2-227">el</span><span class="sxs-lookup"><span data-stu-id="ffbf2-227">el</span></span>            |
| <span data-ttu-id="ffbf2-228">English</span><span class="sxs-lookup"><span data-stu-id="ffbf2-228">English</span></span>               | <span data-ttu-id="ffbf2-229">en</span><span class="sxs-lookup"><span data-stu-id="ffbf2-229">en</span></span>            |
| <span data-ttu-id="ffbf2-230">西班牙文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-230">Spanish</span></span>               | <span data-ttu-id="ffbf2-231">es</span><span class="sxs-lookup"><span data-stu-id="ffbf2-231">es</span></span>            |
| <span data-ttu-id="ffbf2-232">芬蘭文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-232">Finnish</span></span>               | <span data-ttu-id="ffbf2-233">fi</span><span class="sxs-lookup"><span data-stu-id="ffbf2-233">fi</span></span>            |
| <span data-ttu-id="ffbf2-234">法文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-234">French</span></span>                | <span data-ttu-id="ffbf2-235">fr</span><span class="sxs-lookup"><span data-stu-id="ffbf2-235">fr</span></span>            |
| <span data-ttu-id="ffbf2-236">古吉拉特文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-236">Gujarati</span></span>              | <span data-ttu-id="ffbf2-237">gu</span><span class="sxs-lookup"><span data-stu-id="ffbf2-237">gu</span></span>            |
| <span data-ttu-id="ffbf2-238">北印度文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-238">Hindi</span></span>                 | <span data-ttu-id="ffbf2-239">hi</span><span class="sxs-lookup"><span data-stu-id="ffbf2-239">hi</span></span>            |
| <span data-ttu-id="ffbf2-240">克羅埃西亞文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-240">Croatian</span></span>              | <span data-ttu-id="ffbf2-241">hr</span><span class="sxs-lookup"><span data-stu-id="ffbf2-241">hr</span></span>            |
| <span data-ttu-id="ffbf2-242">匈牙利文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-242">Hungarian</span></span>             | <span data-ttu-id="ffbf2-243">hu</span><span class="sxs-lookup"><span data-stu-id="ffbf2-243">hu</span></span>            |
| <span data-ttu-id="ffbf2-244">義大利文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-244">Italian</span></span>               | <span data-ttu-id="ffbf2-245">it</span><span class="sxs-lookup"><span data-stu-id="ffbf2-245">it</span></span>            |
| <span data-ttu-id="ffbf2-246">日文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-246">Japanese</span></span>              | <span data-ttu-id="ffbf2-247">ja</span><span class="sxs-lookup"><span data-stu-id="ffbf2-247">ja</span></span>            |
| <span data-ttu-id="ffbf2-248">坎那達文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-248">Kannada</span></span>               | <span data-ttu-id="ffbf2-249">kn</span><span class="sxs-lookup"><span data-stu-id="ffbf2-249">kn</span></span>            |
| <span data-ttu-id="ffbf2-250">韓文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-250">Korean</span></span>                | <span data-ttu-id="ffbf2-251">ko</span><span class="sxs-lookup"><span data-stu-id="ffbf2-251">ko</span></span>            |
| <span data-ttu-id="ffbf2-252">馬來亞拉姆文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-252">Malayalam</span></span>             | <span data-ttu-id="ffbf2-253">ml</span><span class="sxs-lookup"><span data-stu-id="ffbf2-253">ml</span></span>            |
| <span data-ttu-id="ffbf2-254">馬拉提文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-254">Marathi</span></span>               | <span data-ttu-id="ffbf2-255">mr</span><span class="sxs-lookup"><span data-stu-id="ffbf2-255">mr</span></span>            |
| <span data-ttu-id="ffbf2-256">馬來文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-256">Malay</span></span>                 | <span data-ttu-id="ffbf2-257">ms</span><span class="sxs-lookup"><span data-stu-id="ffbf2-257">ms</span></span>            |
| <span data-ttu-id="ffbf2-258">挪威文 (巴克摩)</span><span class="sxs-lookup"><span data-stu-id="ffbf2-258">Norwegian Bokmal</span></span>      | <span data-ttu-id="ffbf2-259">nb</span><span class="sxs-lookup"><span data-stu-id="ffbf2-259">nb</span></span>            |
| <span data-ttu-id="ffbf2-260">荷蘭文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-260">Dutch</span></span>                 | <span data-ttu-id="ffbf2-261">nl</span><span class="sxs-lookup"><span data-stu-id="ffbf2-261">nl</span></span>            |
| <span data-ttu-id="ffbf2-262">旁遮普文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-262">Punjabi</span></span>               | <span data-ttu-id="ffbf2-263">pa</span><span class="sxs-lookup"><span data-stu-id="ffbf2-263">pa</span></span>            |
| <span data-ttu-id="ffbf2-264">波蘭文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-264">Polish</span></span>                | <span data-ttu-id="ffbf2-265">pl</span><span class="sxs-lookup"><span data-stu-id="ffbf2-265">pl</span></span>            |
| <span data-ttu-id="ffbf2-266">葡萄牙文 - 巴西</span><span class="sxs-lookup"><span data-stu-id="ffbf2-266">Portuguese - Brazil</span></span>   | <span data-ttu-id="ffbf2-267">pt-br</span><span class="sxs-lookup"><span data-stu-id="ffbf2-267">pt-br</span></span>         |
| <span data-ttu-id="ffbf2-268">葡萄牙文 - 葡萄牙</span><span class="sxs-lookup"><span data-stu-id="ffbf2-268">Portuguese - Portugal</span></span> | <span data-ttu-id="ffbf2-269">pt-pt</span><span class="sxs-lookup"><span data-stu-id="ffbf2-269">pt-pt</span></span>         |
| <span data-ttu-id="ffbf2-270">羅馬尼亞文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-270">Romanian</span></span>              | <span data-ttu-id="ffbf2-271">ro</span><span class="sxs-lookup"><span data-stu-id="ffbf2-271">ro</span></span>            |
| <span data-ttu-id="ffbf2-272">俄文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-272">Russian</span></span>               | <span data-ttu-id="ffbf2-273">ru</span><span class="sxs-lookup"><span data-stu-id="ffbf2-273">ru</span></span>            |
| <span data-ttu-id="ffbf2-274">斯洛伐克文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-274">Slovak</span></span>                | <span data-ttu-id="ffbf2-275">sk</span><span class="sxs-lookup"><span data-stu-id="ffbf2-275">sk</span></span>            |
| <span data-ttu-id="ffbf2-276">瑞典文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-276">Swedish</span></span>               | <span data-ttu-id="ffbf2-277">sv</span><span class="sxs-lookup"><span data-stu-id="ffbf2-277">sv</span></span>            |
| <span data-ttu-id="ffbf2-278">坦米爾文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-278">Tamil</span></span>                 | <span data-ttu-id="ffbf2-279">ta</span><span class="sxs-lookup"><span data-stu-id="ffbf2-279">ta</span></span>            |
| <span data-ttu-id="ffbf2-280">特拉古文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-280">Telugu</span></span>                | <span data-ttu-id="ffbf2-281">te</span><span class="sxs-lookup"><span data-stu-id="ffbf2-281">te</span></span>            |
| <span data-ttu-id="ffbf2-282">泰文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-282">Thai</span></span>                  | <span data-ttu-id="ffbf2-283">th</span><span class="sxs-lookup"><span data-stu-id="ffbf2-283">th</span></span>            |
| <span data-ttu-id="ffbf2-284">土耳其文</span><span class="sxs-lookup"><span data-stu-id="ffbf2-284">Turkish</span></span>               | <span data-ttu-id="ffbf2-285">tr</span><span class="sxs-lookup"><span data-stu-id="ffbf2-285">tr</span></span>            |
| <span data-ttu-id="ffbf2-286">中文 - 簡體</span><span class="sxs-lookup"><span data-stu-id="ffbf2-286">Chinese - Simplified</span></span>  | <span data-ttu-id="ffbf2-287">zh-hans</span><span class="sxs-lookup"><span data-stu-id="ffbf2-287">zh-hans</span></span>       |
| <span data-ttu-id="ffbf2-288">中文 - 繁體</span><span class="sxs-lookup"><span data-stu-id="ffbf2-288">Chinese - Traditional</span></span> | <span data-ttu-id="ffbf2-289">zh-hant</span><span class="sxs-lookup"><span data-stu-id="ffbf2-289">zh-hant</span></span>       |
