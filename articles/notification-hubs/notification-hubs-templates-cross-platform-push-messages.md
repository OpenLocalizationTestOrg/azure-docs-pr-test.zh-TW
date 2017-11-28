---
title: aaaTemplates
description: "本主題說明 Azure 通知中樞的範本。"
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="885a1-103">範本</span><span class="sxs-lookup"><span data-stu-id="885a1-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="885a1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="885a1-104">Overview</span></span>
<span data-ttu-id="885a1-105">範本可讓用戶端應用程式 toospecify hello 確切格式的 hello 通知它想 tooreceive。</span><span class="sxs-lookup"><span data-stu-id="885a1-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="885a1-106">使用範本，應用程式可以了解幾個不同的優點，包括下列 hello:</span><span class="sxs-lookup"><span data-stu-id="885a1-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="885a1-107">跨平台的後端</span><span class="sxs-lookup"><span data-stu-id="885a1-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="885a1-108">個人化的通知</span><span class="sxs-lookup"><span data-stu-id="885a1-108">Personalized notifications</span></span>
* <span data-ttu-id="885a1-109">用戶端版本獨立性</span><span class="sxs-lookup"><span data-stu-id="885a1-109">Client-version independence</span></span>
* <span data-ttu-id="885a1-110">容易當地語系化</span><span class="sxs-lookup"><span data-stu-id="885a1-110">Easy localization</span></span>

<span data-ttu-id="885a1-111">本節提供如何為您的裝置目標跨平台和 toopersonalize toouse 範本 toosend 無從驗證平台通知廣播通知 tooeach 裝置的兩個深入了解範例。</span><span class="sxs-lookup"><span data-stu-id="885a1-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="885a1-112">跨平台使用範本</span><span class="sxs-lookup"><span data-stu-id="885a1-112">Using templates cross-platform</span></span>
<span data-ttu-id="885a1-113">hello 標準方式 toosend 推播通知是 toosend，每個通知的傳送，toobe 特定裝載 tooplatform 通知服務 （WNS、 APNS）。</span><span class="sxs-lookup"><span data-stu-id="885a1-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="885a1-114">範例，toosend 警示的 tooAPNS hello 裝載為 Json 物件的下列形式的 hello:</span><span class="sxs-lookup"><span data-stu-id="885a1-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="885a1-115">toosend 類似的快顯訊息上的 Windows 市集應用程式，hello XML 裝載如下所示：</span><span class="sxs-lookup"><span data-stu-id="885a1-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="885a1-116">您可以為 MPNS (Windows Phone) 和 GCM (Android) 平台建立類似的承載。</span><span class="sxs-lookup"><span data-stu-id="885a1-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="885a1-117">這項需求會強制 hello 應用程式後端 tooproduce 不同的裝載的每個平台，並有效地讓 hello 後端負責 hello 展示層的 hello 應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="885a1-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="885a1-118">一些考量包括當地語系化和圖形配置 (尤其是針對包含各種類型之磚通知的「Windows 市集」應用程式)。</span><span class="sxs-lookup"><span data-stu-id="885a1-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="885a1-119">hello 通知中樞範本功能可讓用戶端應用程式 toocreate 特殊登錄，稱為另外包含 toohello 組標記，範本的範本註冊。</span><span class="sxs-lookup"><span data-stu-id="885a1-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="885a1-120">hello 通知中樞範本功能可讓用戶端應用程式 tooassociate 裝置範本是否正在使用的安裝 （慣用） 或註冊。</span><span class="sxs-lookup"><span data-stu-id="885a1-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="885a1-121">由於 hello 前面裝載範例 hello 平台無關的唯一資訊是，hello 實際警示訊息 (Hello ！)。</span><span class="sxs-lookup"><span data-stu-id="885a1-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="885a1-122">範本是一組的 hello 通知中樞上如何 tooformat 平台獨立訊息 hello 註冊該特定用戶端應用程式的指示。</span><span class="sxs-lookup"><span data-stu-id="885a1-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="885a1-123">在上述範例中的 hello，hello 平台獨立訊息是單一的屬性：**訊息 = Hello ！**。</span><span class="sxs-lookup"><span data-stu-id="885a1-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="885a1-124">下列圖片的 hello 說明上述程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="885a1-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="885a1-125">hello iOS 用戶端應用程式註冊的 hello 範本如下所示：</span><span class="sxs-lookup"><span data-stu-id="885a1-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="885a1-126">hello 對應 hello Windows 市集用戶端應用程式範本是：</span><span class="sxs-lookup"><span data-stu-id="885a1-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="885a1-127">請注意，hello 實際的訊息是要替換 hello 運算式 $（訊息）。</span><span class="sxs-lookup"><span data-stu-id="885a1-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="885a1-128">這個運算式會指示 hello 通知中樞時傳送訊息 toothis 特定註冊，toobuild 遵循它和交換器 hello 共通的值中的訊息。</span><span class="sxs-lookup"><span data-stu-id="885a1-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="885a1-129">如果您正在使用安裝模型，hello 安裝 「 範本 」 金鑰會保留多個範本的 JSON。</span><span class="sxs-lookup"><span data-stu-id="885a1-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="885a1-130">如果您正在使用的註冊模型，hello 用戶端應用程式可以建立多個註冊順序 toouse 中多個範本。例如，警示訊息的範本和磚範本更新。</span><span class="sxs-lookup"><span data-stu-id="885a1-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="885a1-131">用戶端應用程式也可以混合使用原生註冊 (無範本的註冊) 與範本註冊。</span><span class="sxs-lookup"><span data-stu-id="885a1-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="885a1-132">hello 通知中樞傳送一則通知之每個範本，而不考慮 toohello 所屬相同的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="885a1-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="885a1-133">此行為可使用的 tootranslate 平台獨立通知到多個通知。</span><span class="sxs-lookup"><span data-stu-id="885a1-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="885a1-134">例如，hello 通知中樞可以順暢地轉譯在快顯通知和磚更新，而不需要知道它的 hello 後端 toobe 相同平台獨立訊息 toohello。</span><span class="sxs-lookup"><span data-stu-id="885a1-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="885a1-135">請注意，某些平台 (例如，iOS) 可能會摺疊多個通知 toohello 相同的裝置，如果在短時間內進行傳送。</span><span class="sxs-lookup"><span data-stu-id="885a1-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="885a1-136">使用範本來進行個人化</span><span class="sxs-lookup"><span data-stu-id="885a1-136">Using templates for personalization</span></span>
<span data-ttu-id="885a1-137">另一個優點 toousing 範本是 hello 能力 toouse 通知中樞 tooperform 註冊每個個人化的通知。</span><span class="sxs-lookup"><span data-stu-id="885a1-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="885a1-138">例如，請考慮天氣應用程式，以顯示磚與 hello 天氣的特定位置。</span><span class="sxs-lookup"><span data-stu-id="885a1-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="885a1-139">使用者可以在攝氏或華氏溫度及單日或五日預測之間做選擇。</span><span class="sxs-lookup"><span data-stu-id="885a1-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="885a1-140">使用範本，每個用戶端應用程式安裝可以註冊所需的 hello 格式 (1 天攝氏、 1 天華氏，5 天攝氏，5 天華氏)，而且有傳送單一訊息，其中包含所有 hello 資訊所需 toofill 那些 hello 後端範本 （例如，五天預測與攝氏和華氏度為單位）。</span><span class="sxs-lookup"><span data-stu-id="885a1-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="885a1-141">hello 範本 hello 一天預測與攝氏溫度如下所示：</span><span class="sxs-lookup"><span data-stu-id="885a1-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="885a1-142">hello 訊息傳送 toohello 通知中樞會包含下列屬性的所有 hello:</span><span class="sxs-lookup"><span data-stu-id="885a1-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="885a1-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="885a1-143">day1_image</span></span></td><td><span data-ttu-id="885a1-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="885a1-144">day2_image</span></span></td><td><span data-ttu-id="885a1-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="885a1-145">day3_image</span></span></td><td><span data-ttu-id="885a1-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="885a1-146">day4_image</span></span></td><td><span data-ttu-id="885a1-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="885a1-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="885a1-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="885a1-148">day1_tempC</span></span></td><td><span data-ttu-id="885a1-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="885a1-149">day2_tempC</span></span></td><td><span data-ttu-id="885a1-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="885a1-150">day3_tempC</span></span></td><td><span data-ttu-id="885a1-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="885a1-151">day4_tempC</span></span></td><td><span data-ttu-id="885a1-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="885a1-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="885a1-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="885a1-153">day1_tempF</span></span></td><td><span data-ttu-id="885a1-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="885a1-154">day2_tempF</span></span></td><td><span data-ttu-id="885a1-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="885a1-155">day3_tempF</span></span></td><td><span data-ttu-id="885a1-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="885a1-156">day4_tempF</span></span></td><td><span data-ttu-id="885a1-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="885a1-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="885a1-158">藉由使用此模式，hello 後端只傳送單一訊息而不需要 toostore hello 應用程式使用者的特定個人化選項。</span><span class="sxs-lookup"><span data-stu-id="885a1-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="885a1-159">下列圖片的 hello 說明這種情況：</span><span class="sxs-lookup"><span data-stu-id="885a1-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="885a1-160">如何 tooregister 範本</span><span class="sxs-lookup"><span data-stu-id="885a1-160">How tooregister templates</span></span>
<span data-ttu-id="885a1-161">tooregister 範本使用 hello 安裝模型 （慣用） 或 hello 註冊模型，請參閱[註冊管理](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="885a1-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="885a1-162">範本運算式語言</span><span class="sxs-lookup"><span data-stu-id="885a1-162">Template expression language</span></span>
<span data-ttu-id="885a1-163">範本是有限的 tooXML 或 JSON 文件格式。</span><span class="sxs-lookup"><span data-stu-id="885a1-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="885a1-164">此外，您只能將運算式放在特定的位置；例如，如果是 XML，只能放在節點屬性或值中，如果是 JSON，則只能放在字串屬性值中。</span><span class="sxs-lookup"><span data-stu-id="885a1-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="885a1-165">hello 下表顯示允許範本中的 hello 語言：</span><span class="sxs-lookup"><span data-stu-id="885a1-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="885a1-166">運算是</span><span class="sxs-lookup"><span data-stu-id="885a1-166">Expression</span></span> | <span data-ttu-id="885a1-167">說明</span><span class="sxs-lookup"><span data-stu-id="885a1-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="885a1-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="885a1-168">$(prop)</span></span> |<span data-ttu-id="885a1-169">參考 tooan hello 給定名稱的事件屬性。</span><span class="sxs-lookup"><span data-stu-id="885a1-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="885a1-170">屬性名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="885a1-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="885a1-171">如果沒有 hello 屬性，這個運算式會解析至 hello 屬性的文字值或空字串。</span><span class="sxs-lookup"><span data-stu-id="885a1-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="885a1-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="885a1-172">$(prop, n)</span></span> |<span data-ttu-id="885a1-173">如以上所述，但 hello 文字已明確地裁剪成 n 個字元，例如 $（標題，20） 裁剪的 hello title 屬性的 hello 內容在 20 個字元。</span><span class="sxs-lookup"><span data-stu-id="885a1-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="885a1-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="885a1-174">.(prop, n)</span></span> |<span data-ttu-id="885a1-175">為更新版本，但 hello 文字的後置字元三個點時，它會裁剪。</span><span class="sxs-lookup"><span data-stu-id="885a1-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="885a1-176">hello hello 的大小總計裁剪字串，而且 hello 後置詞不會超過 n 個字元。</span><span class="sxs-lookup"><span data-stu-id="885a1-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="885a1-177">.（標題，20）"This is hello 標題列 」 結果中的輸入屬性與**hello 標題...**</span><span class="sxs-lookup"><span data-stu-id="885a1-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="885a1-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="885a1-178">%(prop)</span></span> |<span data-ttu-id="885a1-179">除了該 hello 輸出類似 too$(name) 是 URI 編碼。</span><span class="sxs-lookup"><span data-stu-id="885a1-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="885a1-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="885a1-180">#(prop)</span></span> |<span data-ttu-id="885a1-181">用於 JSON 範本 (例如，用於 iOS 與 Android 範本)。</span><span class="sxs-lookup"><span data-stu-id="885a1-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="885a1-182">此函式運作方式完全 hello 相同為 $(prop) 先前指定 JSON 範本 （例如，Apple 範本） 中使用時除外。</span><span class="sxs-lookup"><span data-stu-id="885a1-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="885a1-183">在此情況下，如果此函式不會圍繞著"{'，'}"(，例如 'myJsonProperty': '# （名稱）')，它會評估 Javascript 格式，例如 regexp tooa 數字和: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 &#93;*))(\.&#91; 0-9 &#93; +)？((&#124;E) (+ &#124;-) 嗎？ （& s) #91; 0-9 &#93; +)？，hello 輸出 JSON 是數字，然後。</span><span class="sxs-lookup"><span data-stu-id="885a1-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="885a1-184">例如，‘badge : ‘#(name)’ 會變成 ‘badge’ : 40 (而不是 ‘40‘)。</span><span class="sxs-lookup"><span data-stu-id="885a1-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="885a1-185">‘text’ 或 “text”</span><span class="sxs-lookup"><span data-stu-id="885a1-185">‘text’ or “text”</span></span> |<span data-ttu-id="885a1-186">常值。</span><span class="sxs-lookup"><span data-stu-id="885a1-186">A literal.</span></span> <span data-ttu-id="885a1-187">常值包含以單引號或雙引號括住的任意文字。</span><span class="sxs-lookup"><span data-stu-id="885a1-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="885a1-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="885a1-188">expr1 + expr2</span></span> |<span data-ttu-id="885a1-189">hello 串連運算子結合成單一字串的兩個運算式。</span><span class="sxs-lookup"><span data-stu-id="885a1-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="885a1-190">hello 運算式可以是任何 hello 前面表單。</span><span class="sxs-lookup"><span data-stu-id="885a1-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="885a1-191">當使用串連，必須與 {} 括住 hello 整個運算式。</span><span class="sxs-lookup"><span data-stu-id="885a1-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="885a1-192">例如 {$(prop) + ‘ - ’ + $(prop2)}。</span><span class="sxs-lookup"><span data-stu-id="885a1-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="885a1-193">例如，hello 以下不是有效的 XML 範本：</span><span class="sxs-lookup"><span data-stu-id="885a1-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="885a1-194">如上面所述，使用串連時，運算式必須包含在大括號中。</span><span class="sxs-lookup"><span data-stu-id="885a1-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="885a1-195">例如：</span><span class="sxs-lookup"><span data-stu-id="885a1-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

