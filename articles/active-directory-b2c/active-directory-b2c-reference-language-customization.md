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
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a><span data-ttu-id="e6dd3-102">Azure Active Directory B2C︰使用語言自訂</span><span class="sxs-lookup"><span data-stu-id="e6dd3-102">Azure Active Directory B2C: Using language customization</span></span>

>[!NOTE] 
><span data-ttu-id="e6dd3-103">這項功能處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-103">This feature is in public preview.</span></span>  <span data-ttu-id="e6dd3-104">建議您在使用這項功能時，使用測試租用戶。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-104">It is recommended that you use a test tenant when using this feature.</span></span>  <span data-ttu-id="e6dd3-105">我們不打算 hello 預覽 toohello 公開上市版本中，從任何重大變更，但保留 hello 右 toomake 這類變更 tooimprove hello 功能。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-105">We don't plan on any breaking changes from hello preview toohello general availability release, but we reserve hello right toomake such changes tooimprove hello feature.</span></span>  <span data-ttu-id="e6dd3-106">一旦您已經有機會 tootry 功能，請提供您的體驗的意見反應及如何使其更好。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-106">Once you've had a chance tootry feature, please provide feedback on your experiences and how we can make it better.</span></span>  <span data-ttu-id="e6dd3-107">您可以透過提供意見反應 hello Azure 入口網站使用上 hello 右上方的 hello 的臉正面工具。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-107">You can provide feedback through hello Azure portal with hello smiley face tool on hello top right.</span></span>   <span data-ttu-id="e6dd3-108">如果有一項業務需求為您 toogo 即時 hello 預覽階段期間使用這項功能，讓我們知道您的案例，我們可以提供您的 hello 適當指引及取得協助。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-108">If there is a business requirement for you toogo live using this feature during hello preview phase, let us know your scenarios and we can provide you with hello proper guidance and assistance.</span></span>  <span data-ttu-id="e6dd3-109">您可以透過 [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com) 來與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-109">You can contact us at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>

<span data-ttu-id="e6dd3-110">語言自訂，可讓您 toochange 使用者走 tooa 不同語言 toosuit 您客戶的需求。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-110">Language customization allows you toochange your user journey tooa different language toosuit your customer needs.</span></span>  <span data-ttu-id="e6dd3-111">我們提供 36 種語言的翻譯 (請參閱[其他資訊](#additional-information))。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-111">We provide translations for 36 languages (see [Additional information](#additional-information)).</span></span>  <span data-ttu-id="e6dd3-112">即使茪擩槧槶只會提供您的體驗，您可以自訂 hello 頁面 toosuit 上的文字在您的需求。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-112">Even if your experience is only provided for a single language, you can customize any text on hello pages toosuit your needs.</span></span>  

## <a name="how-does-language-customization-work"></a><span data-ttu-id="e6dd3-113">語言自訂的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="e6dd3-113">How does Language customization work?</span></span>
<span data-ttu-id="e6dd3-114">語言自訂，可讓您 tooselect 使用者旅程是中可用哪些語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-114">Language customization allows you tooselect which languages your user journey is available in.</span></span>  <span data-ttu-id="e6dd3-115">一旦啟用 hello 功能時，您可以提供 hello 查詢字串參數，ui_locales，從您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-115">Once hello feature is enabled, you can provide hello query string parameter, ui_locales, from your application.</span></span>  <span data-ttu-id="e6dd3-116">當您呼叫 Azure AD B2C 時，我們會轉譯頁面 toohello 地區設定，您已表示。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-116">When you call into Azure AD B2C, we translate your page toohello locale that you have indicated.</span></span>  <span data-ttu-id="e6dd3-117">使用的組態類型可讓您在使用者旅程中的 hello 語言的完整控制權，並忽略 hello hello 客戶的瀏覽器的語言設定。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-117">Using type of configuration gives you complete control over hello languages in your user journey and ignores hello language settings of hello customer's browser.</span></span> <span data-ttu-id="e6dd3-118">或者，您也可能不需要對客戶會看見哪種語言擁有這種程度的控制力。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-118">Alternatively, you may not need that level of control over what languages your customer see.</span></span>  <span data-ttu-id="e6dd3-119">如果您沒有提供 ui_locales 參數，其瀏覽器的設定取決於 hello 客戶經驗。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-119">If you don't provide a ui_locales parameter, hello customer's experience is dictated by their browser's settings.</span></span>  <span data-ttu-id="e6dd3-120">您仍然可以控制哪些使用者旅途的語言轉譯 tooby 將它新增為支援的語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-120">You can still control which languages your user journey is translated tooby adding it as a supported language.</span></span>  <span data-ttu-id="e6dd3-121">如果客戶的瀏覽器設定 tooshow 語言不想 toosupport，然後選取支援的文化特性中的預設值改為所顯示的 hello 語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-121">If a customer's browser is set tooshow a language you don't want toosupport, then hello language you selected as a default in supported cultures is shown instead.</span></span>

1. <span data-ttu-id="e6dd3-122">**ui 地區設定所指定語言**-使用者旅程一旦您啟用自訂語言，是此處指定的已翻譯的 toohello 語言</span><span class="sxs-lookup"><span data-stu-id="e6dd3-122">**ui-locales specified language** - Once you enable Language customization, your user journey is translated toohello language specified here</span></span>
2. <span data-ttu-id="e6dd3-123">**瀏覽器要求語言**-如果已指定沒有 ui 地區設定，它會將轉譯 toohello 瀏覽器要求的語言，**如果它已包含在支援的語言**</span><span class="sxs-lookup"><span data-stu-id="e6dd3-123">**Browser requested language** - If no ui-locales was specified, it translates toohello browser requested language, **if it was included in Supported languages**</span></span>
3. <span data-ttu-id="e6dd3-124">**原則預設語言**-如果 hello 瀏覽器不會指定一種語言，或它不支援的其中一個指定，它會將轉譯 toohello 原則預設語言</span><span class="sxs-lookup"><span data-stu-id="e6dd3-124">**Policy default language** - If hello browser doesn't specify a language, or it specifies one that is not supported, it translates toohello policy default language</span></span>

>[!NOTE]
><span data-ttu-id="e6dd3-125">如果您使用自訂的使用者屬性，您需要 tooprovide 您自己的翻譯。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-125">If you are using custom user attributes, you need tooprovide your own translations.</span></span> <span data-ttu-id="e6dd3-126">如需詳細資訊，請參閱[自訂您的字串](#customize-your-strings)。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-126">See '[Customize your strings](#customize-your-strings)' for details.</span></span>
>

## <a name="support-uilocales-requested-languages"></a><span data-ttu-id="e6dd3-127">支援 ui_locales 所要求的語言</span><span class="sxs-lookup"><span data-stu-id="e6dd3-127">Support ui_locales requested languages</span></span> 
<span data-ttu-id="e6dd3-128">藉由啟用 '語言自訂' 的原則，您現在可以藉由加入 hello ui_locales 參數控制 hello 使用者旅程 hello 的語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-128">By enabling 'Language customization' on a policy, you can now control hello language of hello user journey by adding hello ui_locales parameter.</span></span>
1. [<span data-ttu-id="e6dd3-129">您可以依照這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-129">Follow these steps toonavigate toohello B2C features blade on hello Azure portal.</span></span>](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. <span data-ttu-id="e6dd3-130">瀏覽翻譯需 tooenable tooa 原則。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-130">Navigate tooa policy that you want tooenable for translations.</span></span>
3. <span data-ttu-id="e6dd3-131">按一下 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-131">Click **Language customization**.</span></span>
4. <span data-ttu-id="e6dd3-132">讀取 hello 仔細警告。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-132">Read hello warning carefully.</span></span>  <span data-ttu-id="e6dd3-133">啟用之後，您就無法關閉「語言自訂」。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-133">Once enabled, you cannot turn off 'Language customization'.</span></span>
5. <span data-ttu-id="e6dd3-134">開啟 hello 功能，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-134">Turn on hello feature and click **OK**.</span></span>
6. <span data-ttu-id="e6dd3-135">儲存您的原則上 hello 的左上角您**編輯原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-135">Save your policy on hello upper left corner of your **Edit policy** blade.</span></span>

## <a name="select-which-languages-your-user-journey-supports"></a><span data-ttu-id="e6dd3-136">選取您的使用者旅程所支援的語言</span><span class="sxs-lookup"><span data-stu-id="e6dd3-136">Select which languages your user journey supports</span></span> 
<span data-ttu-id="e6dd3-137">建立允許您未提供 hello ui_locales 參數時，在轉譯的使用者之旅 toobe 語言的清單。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-137">Create a list of allowed languages for your user journey toobe translated in when hello ui_locales parameter is not provided.</span></span>
1. <span data-ttu-id="e6dd3-138">透過前面的指示來確定您的原則已啟用「語言自訂」。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-138">Ensure your policy has 'Language customization' enabled from previous instructions.</span></span>
2. <span data-ttu-id="e6dd3-139">從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-139">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="e6dd3-140">即會進入 tooyour**支援的語言**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-140">You are taken tooyour **Supported languages** blade.</span></span>  <span data-ttu-id="e6dd3-141">您可以從這裡選取 [新增語言]。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-141">From here, you can select **Add language**.</span></span>
4. <span data-ttu-id="e6dd3-142">選取所有您想要支援 toobe hello 語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-142">Select all hello languages that you would like toobe supported.</span></span>  

>[!NOTE]
><span data-ttu-id="e6dd3-143">如果未提供 ui_locales 參數，然後 hello 頁面才翻譯的 toohello 客戶的瀏覽器語言其位於這份清單</span><span class="sxs-lookup"><span data-stu-id="e6dd3-143">If a ui_locales parameter is not provided, then hello page is translated toohello customer's browser language only if it is on this list</span></span>
>

5. <span data-ttu-id="e6dd3-144">按一下**確定**hello 底部</span><span class="sxs-lookup"><span data-stu-id="e6dd3-144">Click **Ok** at hello bottom</span></span>
6. <span data-ttu-id="e6dd3-145">關閉 hello**語言自訂**刀鋒視窗和**儲存**您的原則。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-145">Close hello **Language customization** blade and **save** your policy.</span></span>

## <a name="customize-your-strings"></a><span data-ttu-id="e6dd3-146">自訂您的字串</span><span class="sxs-lookup"><span data-stu-id="e6dd3-146">Customize your strings</span></span>
<span data-ttu-id="e6dd3-147">'語言自訂' 可讓您 toocustomize 使用者旅程中的任何字串。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-147">'Language customization' allows you toocustomize any string in your user journey.</span></span>
1. <span data-ttu-id="e6dd3-148">請確定您的原則有語言自訂 hello 前述的指示從啟用。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-148">Ensure your policy has 'Language customization' enabled from hello previous instructions.</span></span>
2. <span data-ttu-id="e6dd3-149">從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-149">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="e6dd3-150">從 hello 左側導覽功能表上，選取**下載內容**。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-150">From hello left-hand navigation menu, select **Download content**.</span></span>
4. <span data-ttu-id="e6dd3-151">選取您想要 tooedit hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-151">Select hello page you want tooedit.</span></span>
5. <span data-ttu-id="e6dd3-152">在 hello 下拉式清單中，選取您想要針對 tooedit hello 語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-152">In hello dropdown, select hello language you want tooedit for.</span></span>
6. <span data-ttu-id="e6dd3-153">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-153">Click **Download**.</span></span> 

<span data-ttu-id="e6dd3-154">這些步驟可讓您在 JSON 檔案，您可以使用 toostart 編輯您的字串。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-154">These steps give you a JSON file that you can use toostart editing your strings.</span></span>

### <a name="changing-any-string-on-hello-page"></a><span data-ttu-id="e6dd3-155">變更在 hello 頁面上的任何字串</span><span class="sxs-lookup"><span data-stu-id="e6dd3-155">Changing any string on hello page</span></span>
1. <span data-ttu-id="e6dd3-156">從 JSON 編輯器的前述指示，下載開啟 hello JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-156">Open hello JSON file downloaded from previous instructions in a JSON editor.</span></span>
2. <span data-ttu-id="e6dd3-157">尋找您想要 toochange 的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-157">Find hello element you want toochange.</span></span>  <span data-ttu-id="e6dd3-158">您可以找到 hello `StringId` hello 字串，您要尋找或尋找 hello 的`Value`想 toochange。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-158">You can find hello `StringId` of hello string you are looking for, or look for hello `Value` you want toochange.</span></span>
3. <span data-ttu-id="e6dd3-159">更新 hello`Value`具有您要顯示屬性。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-159">Update hello `Value` attribute with what you want displayed.</span></span>
4. <span data-ttu-id="e6dd3-160">儲存 hello 檔案，並上傳您的變更。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-160">Save hello file and upload your changes.</span></span>

### <a name="changing-extension-attributes"></a><span data-ttu-id="e6dd3-161">變更擴充屬性</span><span class="sxs-lookup"><span data-stu-id="e6dd3-161">Changing extension attributes</span></span>
<span data-ttu-id="e6dd3-162">若您要尋找 toochange hello 字串的自訂使用者屬性，或想 tooadd 一個 toohello JSON 時，則為下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6dd3-162">If you are looking toochange hello string for a custom user attribute, or want tooadd one toohello JSON, it is in hello following format:</span></span>
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
><span data-ttu-id="e6dd3-163">如果您需要 toooverride 字串時，請確定 tooset hello`Override`值太`true`。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-163">If you need toooverride a string, make sure tooset hello `Override` value too`true`.</span></span>  <span data-ttu-id="e6dd3-164">如果 hello 值不會變更，則會忽略 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-164">If hello value isn't changed, hello entry is ignored.</span></span> 
>

<span data-ttu-id="e6dd3-165">取代`<ExtensionAttribute>`hello 的自訂使用者屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-165">Replace `<ExtensionAttribute>` with hello name of your custom user attribute.</span></span>  
<span data-ttu-id="e6dd3-166">取代`<ExtensionAttributeValue>`與 hello 顯示新字串 toobe。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-166">Replace `<ExtensionAttributeValue>` with hello new string toobe displayed.</span></span>

### <a name="using-localizedcollections"></a><span data-ttu-id="e6dd3-167">使用 LocalizedCollections</span><span class="sxs-lookup"><span data-stu-id="e6dd3-167">Using LocalizedCollections</span></span>
<span data-ttu-id="e6dd3-168">如果您想要回應 tooprovide 值組清單，您需要 toocreate `LocalizedCollections`。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-168">If you want tooprovide a set list of values for responses, you need toocreate a `LocalizedCollections`.</span></span>  <span data-ttu-id="e6dd3-169">`LocalizedCollections` 是 `Name` 和 `Value` 的配對陣列。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-169">A `LocalizedCollections` is an array of `Name` and `Value` pairs.</span></span>  <span data-ttu-id="e6dd3-170">hello`Name`是會顯示 hello`Value`是 hello 宣告中傳回的內容。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-170">hello `Name` is what is displayed and hello `Value` is what is returned in hello claim.</span></span>  <span data-ttu-id="e6dd3-171">tooadd `LocalizedCollections`，它有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6dd3-171">tooadd a `LocalizedCollections`, it has hello following format:</span></span>

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
><span data-ttu-id="e6dd3-172">如果您需要 toooverride 字串時，請確定 tooset hello`Override`值太`true`。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-172">If you need toooverride a string, make sure tooset hello `Override` value too`true`.</span></span>  <span data-ttu-id="e6dd3-173">如果 hello 值不會變更，則會忽略 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-173">If hello value isn't changed, hello entry is ignored.</span></span> 
>

* <span data-ttu-id="e6dd3-174">`ElementId`是 hello 使用者屬性這`LocalizedCollections`會回應至</span><span class="sxs-lookup"><span data-stu-id="e6dd3-174">`ElementId` is hello user attribute that this `LocalizedCollections` is a response to</span></span>
* <span data-ttu-id="e6dd3-175">`Name`hello 值顯示的 toohello 使用者</span><span class="sxs-lookup"><span data-stu-id="e6dd3-175">`Name` is hello value shown toohello user</span></span>
* <span data-ttu-id="e6dd3-176">`Value`已選取此選項時傳回 hello 宣告中</span><span class="sxs-lookup"><span data-stu-id="e6dd3-176">`Value` is what is returned in hello claim when this option is selected</span></span>

### <a name="upload-your-changes"></a><span data-ttu-id="e6dd3-177">上傳您的變更</span><span class="sxs-lookup"><span data-stu-id="e6dd3-177">Upload your changes</span></span>
1. <span data-ttu-id="e6dd3-178">當您完成 hello 變更 tooyour JSON 檔案時，瀏覽後 tooyour B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-178">Once you have completed hello changes tooyour JSON file, navigate back tooyour B2C tenant.</span></span>
2. <span data-ttu-id="e6dd3-179">從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-179">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="e6dd3-180">從 hello 左側導覽功能表上，選取**內容上傳**。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-180">From hello left-hand navigation menu, select **Upload content**.</span></span>
4. <span data-ttu-id="e6dd3-181">選取您想做的變更 tooupload hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-181">Select hello page you want tooupload your changes for.</span></span>
5. <span data-ttu-id="e6dd3-182">如果您想 tooupload 您先前提供的 JSON 的語言，您會需要 toodelete hello 前一個項目。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-182">If you want tooupload a language that you've previously provided a JSON for, you need toodelete hello previous entry.</span></span>  <span data-ttu-id="e6dd3-183">您可以將它刪除即可 hello`...`在 hello 該語言的右邊，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-183">You can delete it by clicking hello `...` on hello right of that language and select **Delete**.</span></span>
6. <span data-ttu-id="e6dd3-184">按一下**新增**hello 左上方。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-184">Click **Add** on hello upper left.</span></span>
7. <span data-ttu-id="e6dd3-185">選取在 JSON 檔案 hello 語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-185">Select hello language of your JSON file.</span></span>
8. <span data-ttu-id="e6dd3-186">按一下 上 hello 右 hello 資料夾 按鈕，瀏覽您的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-186">Click hello folder button on hello right and browse for your JSON file.</span></span>
9. <span data-ttu-id="e6dd3-187">按一下 hello**上傳**上 hello hello 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-187">Click hello **Upload** button on hello bottom of hello blade.</span></span>
10. <span data-ttu-id="e6dd3-188">返回 tooyour**編輯原則**刀鋒視窗，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-188">Go back tooyour **Edit policy** blade and click **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="e6dd3-189">其他資訊</span><span class="sxs-lookup"><span data-stu-id="e6dd3-189">Additional information</span></span>
### <a name="recommendations-for-language-customization"></a><span data-ttu-id="e6dd3-190">「語言自訂」的建議</span><span class="sxs-lookup"><span data-stu-id="e6dd3-190">Recommendations for 'Language customization'</span></span>
<span data-ttu-id="e6dd3-191">我們建議僅將放在字串的項目 tooyour 語言資源您明確地想 tooreplace。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-191">We recommend only putting in entries tooyour Language resources for strings you explicitly want tooreplace.</span></span>  <span data-ttu-id="e6dd3-192">我們會強制執行編譯 JSON 翻譯超出大小限制 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-192">We enforce a size limit toohello file that is compiled out of all your JSON translations.</span></span>  <span data-ttu-id="e6dd3-193">如果您的檔案太大，它會影響使用者旅程 hello 的效能。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-193">If your files get too large, it impacts hello performance of your user journey.</span></span>
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a><span data-ttu-id="e6dd3-194">「語言自訂」啟用後，系統就會移除頁面 UI 自訂標籤</span><span class="sxs-lookup"><span data-stu-id="e6dd3-194">Page UI customization labels are removed once 'Language customization' is enabled</span></span>
<span data-ttu-id="e6dd3-195">當您啟用「語言自訂」時，系統會移除您先前使用頁面 UI 自訂對標籤所進行的編輯，但自訂使用者屬性除外。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-195">When you enable 'Language customization', your previous edits for labels using Page UI customization are removed except for custom user attributes.</span></span>  <span data-ttu-id="e6dd3-196">這項變更是 tooavoid 衝突，您可以在其中編輯您的字串。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-196">This change is done tooavoid conflicts in where you can edit your strings.</span></span>  <span data-ttu-id="e6dd3-197">您可以繼續 toochange 標籤和其他字串上傳 '語言自訂' 中的語言資源。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-197">You can continue toochange your labels and other strings by uploading language resources in 'Language customization'.</span></span>
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a><span data-ttu-id="e6dd3-198">Microsoft 於貴用戶使用的認可的 tooprovide hello 最新翻譯</span><span class="sxs-lookup"><span data-stu-id="e6dd3-198">Microsoft is committed tooprovide hello most up-to-date translations for your use</span></span>
<span data-ttu-id="e6dd3-199">我們會持續改善翻譯，並讓它們符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-199">We will continuously improve translations and keep them in compliance for you.</span></span>  <span data-ttu-id="e6dd3-200">我們會找出錯誤和全域詞彙中的變更，使用者旅程中順暢地進行運作的 hello 更新。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-200">We will identify bugs and changes in global terminology and make hello updates that will work seamlessly in your user journey.</span></span>
### <a name="support-for-right-to-left-languages"></a><span data-ttu-id="e6dd3-201">支援從右至左的語言</span><span class="sxs-lookup"><span data-stu-id="e6dd3-201">Support for right-to-left languages</span></span>
<span data-ttu-id="e6dd3-202">不支援由右至左的語言，如果您需要此功能，請在 [Azure 意見反應](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag)投票給這項功能。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-202">There is no support for right-to-left languages, if you require this feature please vote for this feature on [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).</span></span>
### <a name="social-identity-provider-translations"></a><span data-ttu-id="e6dd3-203">社交識別提供者的翻譯</span><span class="sxs-lookup"><span data-stu-id="e6dd3-203">Social Identity provider translations</span></span>
<span data-ttu-id="e6dd3-204">我們提供 hello ui_locales OIDC 參數 toosocial 登入，但有些社交身分識別提供者，包括 Facebook 和 Google 程式並不接受。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-204">We provide hello ui_locales OIDC parameter toosocial logins but they are not honored by some social identity providers, including Facebook and Google.</span></span> 
### <a name="browser-behavior"></a><span data-ttu-id="e6dd3-205">瀏覽器行為</span><span class="sxs-lookup"><span data-stu-id="e6dd3-205">Browser behavior</span></span>
<span data-ttu-id="e6dd3-206">Chrome 和 Firefox 同時要求其設定的語言，而且如果是支援的語言，它會顯示 hello 預設之前。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-206">Chrome and Firefox both request for their set language and if it is a supported language, it is displayed before hello default.</span></span>  <span data-ttu-id="e6dd3-207">邊緣目前沒有要求的語言，且會直接 toohello 預設語言。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-207">Edge currently does not request a language and goes straight toohello default language.</span></span>
### <a name="known-issues"></a><span data-ttu-id="e6dd3-208">已知問題</span><span class="sxs-lookup"><span data-stu-id="e6dd3-208">Known issues</span></span>
* <span data-ttu-id="e6dd3-209">目前無法使用上傳設定檔編輯的原則中的 hello MFA 頁面的語言資源。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-209">Uploading language resources for hello MFA page in a Profile Edit policy is currently unavailable.</span></span>
* <span data-ttu-id="e6dd3-210">`LocalizedCollections`不是值會產生 hello 回應類型視需要</span><span class="sxs-lookup"><span data-stu-id="e6dd3-210">`LocalizedCollections` aren't generated for values when it is required by hello response type</span></span>
### <a name="what-if-i-want-a-language-that-isnt-supported"></a><span data-ttu-id="e6dd3-211">如果我想使用的語言不受支援會如何？</span><span class="sxs-lookup"><span data-stu-id="e6dd3-211">What if I want a language that isn't supported?</span></span>
<span data-ttu-id="e6dd3-212">我們計劃 tooprovide 的這項功能，可讓您 tooupload 朝向 '自訂語言' JSON 資源擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-212">We are planning tooprovide an extension of this feature that allows you tooupload a JSON resource towards 'custom languages'.</span></span>  <span data-ttu-id="e6dd3-213">hello 功能可讓您 toospecify hello 名稱以及語言的任何語言程式碼，並提供*所有*hello 該語言的翻譯。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-213">hello feature allows you toospecify hello name and language code for any language and provide *all* hello translations for that language.</span></span>  <span data-ttu-id="e6dd3-214">如果您需要這項功能，請將您的情況傳送給我們：[aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="e6dd3-214">If you need this feature, send us your scenario at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>  

### <a name="what-languages-are-supported"></a><span data-ttu-id="e6dd3-215">支援哪些語言？</span><span class="sxs-lookup"><span data-stu-id="e6dd3-215">What languages are supported?</span></span>

| <span data-ttu-id="e6dd3-216">語言</span><span class="sxs-lookup"><span data-stu-id="e6dd3-216">Language</span></span>              | <span data-ttu-id="e6dd3-217">語言代碼</span><span class="sxs-lookup"><span data-stu-id="e6dd3-217">Language code</span></span> |
|-----------------------|---------------|
| <span data-ttu-id="e6dd3-218">孟加拉文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-218">Bangla</span></span>                | <span data-ttu-id="e6dd3-219">bn</span><span class="sxs-lookup"><span data-stu-id="e6dd3-219">bn</span></span>            |
| <span data-ttu-id="e6dd3-220">捷克文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-220">Czech</span></span>                 | <span data-ttu-id="e6dd3-221">cs</span><span class="sxs-lookup"><span data-stu-id="e6dd3-221">cs</span></span>            |
| <span data-ttu-id="e6dd3-222">丹麥文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-222">Danish</span></span>                | <span data-ttu-id="e6dd3-223">da</span><span class="sxs-lookup"><span data-stu-id="e6dd3-223">da</span></span>            |
| <span data-ttu-id="e6dd3-224">德文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-224">German</span></span>                | <span data-ttu-id="e6dd3-225">de</span><span class="sxs-lookup"><span data-stu-id="e6dd3-225">de</span></span>            |
| <span data-ttu-id="e6dd3-226">希臘文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-226">Greek</span></span>                 | <span data-ttu-id="e6dd3-227">el</span><span class="sxs-lookup"><span data-stu-id="e6dd3-227">el</span></span>            |
| <span data-ttu-id="e6dd3-228">English</span><span class="sxs-lookup"><span data-stu-id="e6dd3-228">English</span></span>               | <span data-ttu-id="e6dd3-229">en</span><span class="sxs-lookup"><span data-stu-id="e6dd3-229">en</span></span>            |
| <span data-ttu-id="e6dd3-230">西班牙文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-230">Spanish</span></span>               | <span data-ttu-id="e6dd3-231">es</span><span class="sxs-lookup"><span data-stu-id="e6dd3-231">es</span></span>            |
| <span data-ttu-id="e6dd3-232">芬蘭文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-232">Finnish</span></span>               | <span data-ttu-id="e6dd3-233">fi</span><span class="sxs-lookup"><span data-stu-id="e6dd3-233">fi</span></span>            |
| <span data-ttu-id="e6dd3-234">法文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-234">French</span></span>                | <span data-ttu-id="e6dd3-235">fr</span><span class="sxs-lookup"><span data-stu-id="e6dd3-235">fr</span></span>            |
| <span data-ttu-id="e6dd3-236">古吉拉特文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-236">Gujarati</span></span>              | <span data-ttu-id="e6dd3-237">gu</span><span class="sxs-lookup"><span data-stu-id="e6dd3-237">gu</span></span>            |
| <span data-ttu-id="e6dd3-238">北印度文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-238">Hindi</span></span>                 | <span data-ttu-id="e6dd3-239">hi</span><span class="sxs-lookup"><span data-stu-id="e6dd3-239">hi</span></span>            |
| <span data-ttu-id="e6dd3-240">克羅埃西亞文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-240">Croatian</span></span>              | <span data-ttu-id="e6dd3-241">hr</span><span class="sxs-lookup"><span data-stu-id="e6dd3-241">hr</span></span>            |
| <span data-ttu-id="e6dd3-242">匈牙利文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-242">Hungarian</span></span>             | <span data-ttu-id="e6dd3-243">hu</span><span class="sxs-lookup"><span data-stu-id="e6dd3-243">hu</span></span>            |
| <span data-ttu-id="e6dd3-244">義大利文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-244">Italian</span></span>               | <span data-ttu-id="e6dd3-245">it</span><span class="sxs-lookup"><span data-stu-id="e6dd3-245">it</span></span>            |
| <span data-ttu-id="e6dd3-246">日文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-246">Japanese</span></span>              | <span data-ttu-id="e6dd3-247">ja</span><span class="sxs-lookup"><span data-stu-id="e6dd3-247">ja</span></span>            |
| <span data-ttu-id="e6dd3-248">坎那達文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-248">Kannada</span></span>               | <span data-ttu-id="e6dd3-249">kn</span><span class="sxs-lookup"><span data-stu-id="e6dd3-249">kn</span></span>            |
| <span data-ttu-id="e6dd3-250">韓文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-250">Korean</span></span>                | <span data-ttu-id="e6dd3-251">ko</span><span class="sxs-lookup"><span data-stu-id="e6dd3-251">ko</span></span>            |
| <span data-ttu-id="e6dd3-252">馬來亞拉姆文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-252">Malayalam</span></span>             | <span data-ttu-id="e6dd3-253">ml</span><span class="sxs-lookup"><span data-stu-id="e6dd3-253">ml</span></span>            |
| <span data-ttu-id="e6dd3-254">馬拉提文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-254">Marathi</span></span>               | <span data-ttu-id="e6dd3-255">mr</span><span class="sxs-lookup"><span data-stu-id="e6dd3-255">mr</span></span>            |
| <span data-ttu-id="e6dd3-256">馬來文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-256">Malay</span></span>                 | <span data-ttu-id="e6dd3-257">ms</span><span class="sxs-lookup"><span data-stu-id="e6dd3-257">ms</span></span>            |
| <span data-ttu-id="e6dd3-258">挪威文 (巴克摩)</span><span class="sxs-lookup"><span data-stu-id="e6dd3-258">Norwegian Bokmal</span></span>      | <span data-ttu-id="e6dd3-259">nb</span><span class="sxs-lookup"><span data-stu-id="e6dd3-259">nb</span></span>            |
| <span data-ttu-id="e6dd3-260">荷蘭文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-260">Dutch</span></span>                 | <span data-ttu-id="e6dd3-261">nl</span><span class="sxs-lookup"><span data-stu-id="e6dd3-261">nl</span></span>            |
| <span data-ttu-id="e6dd3-262">旁遮普文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-262">Punjabi</span></span>               | <span data-ttu-id="e6dd3-263">pa</span><span class="sxs-lookup"><span data-stu-id="e6dd3-263">pa</span></span>            |
| <span data-ttu-id="e6dd3-264">波蘭文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-264">Polish</span></span>                | <span data-ttu-id="e6dd3-265">pl</span><span class="sxs-lookup"><span data-stu-id="e6dd3-265">pl</span></span>            |
| <span data-ttu-id="e6dd3-266">葡萄牙文 - 巴西</span><span class="sxs-lookup"><span data-stu-id="e6dd3-266">Portuguese - Brazil</span></span>   | <span data-ttu-id="e6dd3-267">pt-br</span><span class="sxs-lookup"><span data-stu-id="e6dd3-267">pt-br</span></span>         |
| <span data-ttu-id="e6dd3-268">葡萄牙文 - 葡萄牙</span><span class="sxs-lookup"><span data-stu-id="e6dd3-268">Portuguese - Portugal</span></span> | <span data-ttu-id="e6dd3-269">pt-pt</span><span class="sxs-lookup"><span data-stu-id="e6dd3-269">pt-pt</span></span>         |
| <span data-ttu-id="e6dd3-270">羅馬尼亞文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-270">Romanian</span></span>              | <span data-ttu-id="e6dd3-271">ro</span><span class="sxs-lookup"><span data-stu-id="e6dd3-271">ro</span></span>            |
| <span data-ttu-id="e6dd3-272">俄文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-272">Russian</span></span>               | <span data-ttu-id="e6dd3-273">ru</span><span class="sxs-lookup"><span data-stu-id="e6dd3-273">ru</span></span>            |
| <span data-ttu-id="e6dd3-274">斯洛伐克文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-274">Slovak</span></span>                | <span data-ttu-id="e6dd3-275">sk</span><span class="sxs-lookup"><span data-stu-id="e6dd3-275">sk</span></span>            |
| <span data-ttu-id="e6dd3-276">瑞典文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-276">Swedish</span></span>               | <span data-ttu-id="e6dd3-277">sv</span><span class="sxs-lookup"><span data-stu-id="e6dd3-277">sv</span></span>            |
| <span data-ttu-id="e6dd3-278">坦米爾文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-278">Tamil</span></span>                 | <span data-ttu-id="e6dd3-279">ta</span><span class="sxs-lookup"><span data-stu-id="e6dd3-279">ta</span></span>            |
| <span data-ttu-id="e6dd3-280">特拉古文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-280">Telugu</span></span>                | <span data-ttu-id="e6dd3-281">te</span><span class="sxs-lookup"><span data-stu-id="e6dd3-281">te</span></span>            |
| <span data-ttu-id="e6dd3-282">泰文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-282">Thai</span></span>                  | <span data-ttu-id="e6dd3-283">th</span><span class="sxs-lookup"><span data-stu-id="e6dd3-283">th</span></span>            |
| <span data-ttu-id="e6dd3-284">土耳其文</span><span class="sxs-lookup"><span data-stu-id="e6dd3-284">Turkish</span></span>               | <span data-ttu-id="e6dd3-285">tr</span><span class="sxs-lookup"><span data-stu-id="e6dd3-285">tr</span></span>            |
| <span data-ttu-id="e6dd3-286">中文 - 簡體</span><span class="sxs-lookup"><span data-stu-id="e6dd3-286">Chinese - Simplified</span></span>  | <span data-ttu-id="e6dd3-287">zh-hans</span><span class="sxs-lookup"><span data-stu-id="e6dd3-287">zh-hans</span></span>       |
| <span data-ttu-id="e6dd3-288">中文 - 繁體</span><span class="sxs-lookup"><span data-stu-id="e6dd3-288">Chinese - Traditional</span></span> | <span data-ttu-id="e6dd3-289">zh-hant</span><span class="sxs-lookup"><span data-stu-id="e6dd3-289">zh-hant</span></span>       |
