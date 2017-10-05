---
title: "範本"
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
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="efa25-103">範本</span><span class="sxs-lookup"><span data-stu-id="efa25-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="efa25-104">概觀</span><span class="sxs-lookup"><span data-stu-id="efa25-104">Overview</span></span>
<span data-ttu-id="efa25-105">範本可讓用戶端應用程式指定它要接收的確切通知格式。</span><span class="sxs-lookup"><span data-stu-id="efa25-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="efa25-106">使用範本時，app 可以獲得數個不同的好處，包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="efa25-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="efa25-107">跨平台的後端</span><span class="sxs-lookup"><span data-stu-id="efa25-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="efa25-108">個人化的通知</span><span class="sxs-lookup"><span data-stu-id="efa25-108">Personalized notifications</span></span>
* <span data-ttu-id="efa25-109">用戶端版本獨立性</span><span class="sxs-lookup"><span data-stu-id="efa25-109">Client-version independence</span></span>
* <span data-ttu-id="efa25-110">容易當地語系化</span><span class="sxs-lookup"><span data-stu-id="efa25-110">Easy localization</span></span>

<span data-ttu-id="efa25-111">本節提供兩個深入的範例，說明如何使用範本來傳送以您在所有平台的所有裝置為目標的跨平台通知，以及如何針對每部裝置將廣播通知個人化。</span><span class="sxs-lookup"><span data-stu-id="efa25-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="efa25-112">跨平台使用範本</span><span class="sxs-lookup"><span data-stu-id="efa25-112">Using templates cross-platform</span></span>
<span data-ttu-id="efa25-113">傳送推播通知的標準方式是，針對要傳送的每個通知，傳送一個特定的承載給平台通知服務 (WNS、APNS)。</span><span class="sxs-lookup"><span data-stu-id="efa25-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="efa25-114">例如，若要傳送警示給 APNS，則承載會是形式如下的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="efa25-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="efa25-115">若要在「Windows 市集」應用程式上傳送類似的快顯通知訊息，則 XML 承載如下：</span><span class="sxs-lookup"><span data-stu-id="efa25-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="efa25-116">您可以為 MPNS (Windows Phone) 和 GCM (Android) 平台建立類似的承載。</span><span class="sxs-lookup"><span data-stu-id="efa25-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="efa25-117">這項要求會強制 app 後端為每個平台產生不同的承載，而有效地讓後端負責 app 展示層的一部分。</span><span class="sxs-lookup"><span data-stu-id="efa25-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="efa25-118">一些考量包括當地語系化和圖形配置 (尤其是針對包含各種類型之磚通知的「Windows 市集」應用程式)。</span><span class="sxs-lookup"><span data-stu-id="efa25-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="efa25-119">「通知中樞」範本功能可讓用戶端 app 建立特殊的註冊 (稱為範本註冊)，其中除了包含一組標記之外，還包含一個範本。</span><span class="sxs-lookup"><span data-stu-id="efa25-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="efa25-120">「通知中樞」範本功能可讓用戶端 app 將裝置與範本建立關聯，不論您使用的是「安裝」(慣用) 還是「註冊」。</span><span class="sxs-lookup"><span data-stu-id="efa25-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="efa25-121">在前述的承載範例中，唯一的平台獨立資訊是實際的警示訊息 (Hello!)。</span><span class="sxs-lookup"><span data-stu-id="efa25-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="efa25-122">範本是「通知中樞」的一組指示，有關如何針對該特定用戶端 app 的註冊，設定平台獨立訊息的格式。</span><span class="sxs-lookup"><span data-stu-id="efa25-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="efa25-123">在前述範例中，平台獨立訊息是一個單一屬性： **message = Hello!**。</span><span class="sxs-lookup"><span data-stu-id="efa25-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="efa25-124">下圖說明上述的程序：</span><span class="sxs-lookup"><span data-stu-id="efa25-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="efa25-125">iOS 用戶端 app 註冊的範本如下：</span><span class="sxs-lookup"><span data-stu-id="efa25-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="efa25-126">對應的「Windows 市集」用戶端 app 範本是：</span><span class="sxs-lookup"><span data-stu-id="efa25-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="efa25-127">請注意，實際的訊息會替代 $(message) 運算式。</span><span class="sxs-lookup"><span data-stu-id="efa25-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="efa25-128">這個運算式會指示「通知中樞」在每次傳送訊息給這個特定的註冊時，都建立依循它的訊息並將通用值切換進來。</span><span class="sxs-lookup"><span data-stu-id="efa25-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="efa25-129">如果您使用的是「安裝」模型，則安裝 “templates” 機碼會保有多個範本的 JSON。</span><span class="sxs-lookup"><span data-stu-id="efa25-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="efa25-130">如果您使用的是「註冊」模型，則用戶端應用程式可以建立多個註冊以使用多個範本；例如，一個範本用於警示訊息，一個範本用於磚更新。</span><span class="sxs-lookup"><span data-stu-id="efa25-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="efa25-131">用戶端應用程式也可以混合使用原生註冊 (無範本的註冊) 與範本註冊。</span><span class="sxs-lookup"><span data-stu-id="efa25-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="efa25-132">「通知中樞」會針對每個範本傳送一個通知，而不會考慮它們是否屬於相同的用戶端 app。</span><span class="sxs-lookup"><span data-stu-id="efa25-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="efa25-133">這種行為可用來將平台獨立通知轉譯成更多的通知。</span><span class="sxs-lookup"><span data-stu-id="efa25-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="efa25-134">例如，對「通知中樞」而言相同的平台獨立訊息可以順暢地在快顯通知警示與磚更新中轉譯，而不需要後端知道它。</span><span class="sxs-lookup"><span data-stu-id="efa25-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="efa25-135">請注意，某些平台 (例如 iOS) 可能會將在短時間內傳送給相同裝置的多個通知摺疊起來。</span><span class="sxs-lookup"><span data-stu-id="efa25-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="efa25-136">使用範本來進行個人化</span><span class="sxs-lookup"><span data-stu-id="efa25-136">Using templates for personalization</span></span>
<span data-ttu-id="efa25-137">使用範本的另一個好處是能夠使用「通知中樞」依每一註冊執行通知個人化。</span><span class="sxs-lookup"><span data-stu-id="efa25-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="efa25-138">例如，假設有一個天氣 app，此 app 會顯示含有特定位置天氣狀況的磚。</span><span class="sxs-lookup"><span data-stu-id="efa25-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="efa25-139">使用者可以在攝氏或華氏溫度及單日或五日預測之間做選擇。</span><span class="sxs-lookup"><span data-stu-id="efa25-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="efa25-140">使用範本時，每個用戶端 app 安裝項可以註冊所需的格式 (1 日攝氏、1 日華氏、 5 日攝氏、 5 日華氏)，然後讓後端傳送一個含有填寫這些範本 (例如，使用攝氏和華氏溫度的 5 日預報) 所需之一切資訊的單一訊息。</span><span class="sxs-lookup"><span data-stu-id="efa25-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="efa25-141">使用攝氏溫度的 1 日預報範本如下：</span><span class="sxs-lookup"><span data-stu-id="efa25-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="efa25-142">傳送給「通知中樞」的訊息會包含下列所有屬性：</span><span class="sxs-lookup"><span data-stu-id="efa25-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="efa25-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="efa25-143">day1_image</span></span></td><td><span data-ttu-id="efa25-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="efa25-144">day2_image</span></span></td><td><span data-ttu-id="efa25-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="efa25-145">day3_image</span></span></td><td><span data-ttu-id="efa25-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="efa25-146">day4_image</span></span></td><td><span data-ttu-id="efa25-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="efa25-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="efa25-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="efa25-148">day1_tempC</span></span></td><td><span data-ttu-id="efa25-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="efa25-149">day2_tempC</span></span></td><td><span data-ttu-id="efa25-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="efa25-150">day3_tempC</span></span></td><td><span data-ttu-id="efa25-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="efa25-151">day4_tempC</span></span></td><td><span data-ttu-id="efa25-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="efa25-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="efa25-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="efa25-153">day1_tempF</span></span></td><td><span data-ttu-id="efa25-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="efa25-154">day2_tempF</span></span></td><td><span data-ttu-id="efa25-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="efa25-155">day3_tempF</span></span></td><td><span data-ttu-id="efa25-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="efa25-156">day4_tempF</span></span></td><td><span data-ttu-id="efa25-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="efa25-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="efa25-158">藉由使用此模式，後端只需傳送單一訊息，而不需儲存 app 使用者的特定個人化選項。</span><span class="sxs-lookup"><span data-stu-id="efa25-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="efa25-159">下圖說明這個案例：</span><span class="sxs-lookup"><span data-stu-id="efa25-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="efa25-160">如何註冊範本</span><span class="sxs-lookup"><span data-stu-id="efa25-160">How to register templates</span></span>
<span data-ttu-id="efa25-161">若要使用「安裝」模型 (慣用) 或「註冊」模型以範本進行註冊，請參閱 [註冊管理](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="efa25-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="efa25-162">範本運算式語言</span><span class="sxs-lookup"><span data-stu-id="efa25-162">Template expression language</span></span>
<span data-ttu-id="efa25-163">範本僅限於 XML 或 JSON 文件格式。</span><span class="sxs-lookup"><span data-stu-id="efa25-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="efa25-164">此外，您只能將運算式放在特定的位置；例如，如果是 XML，只能放在節點屬性或值中，如果是 JSON，則只能放在字串屬性值中。</span><span class="sxs-lookup"><span data-stu-id="efa25-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="efa25-165">下表顯示範本中允許使用的語言：</span><span class="sxs-lookup"><span data-stu-id="efa25-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="efa25-166">運算是</span><span class="sxs-lookup"><span data-stu-id="efa25-166">Expression</span></span> | <span data-ttu-id="efa25-167">說明</span><span class="sxs-lookup"><span data-stu-id="efa25-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa25-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="efa25-168">$(prop)</span></span> |<span data-ttu-id="efa25-169">具有指定名稱之事件屬性的參考。</span><span class="sxs-lookup"><span data-stu-id="efa25-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="efa25-170">屬性名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="efa25-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="efa25-171">如果屬性不存在，這個運算式就會解析成屬性的文字值或空字串。</span><span class="sxs-lookup"><span data-stu-id="efa25-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="efa25-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="efa25-172">$(prop, n)</span></span> |<span data-ttu-id="efa25-173">同上，但文字會明確裁剪成 n 字元，例如 $(title, 20) 會將 title 屬性內容裁剪成 20 個字元。</span><span class="sxs-lookup"><span data-stu-id="efa25-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="efa25-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="efa25-174">.(prop, n)</span></span> |<span data-ttu-id="efa25-175">同上，但文字會在裁剪之後，後面加上三個點。</span><span class="sxs-lookup"><span data-stu-id="efa25-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="efa25-176">裁剪的字串與字尾的總大小不會超過 n 個字元。</span><span class="sxs-lookup"><span data-stu-id="efa25-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="efa25-177">.(title, 20) 搭配 “This is the title line” 輸入屬性會產生 **This is the title...**</span><span class="sxs-lookup"><span data-stu-id="efa25-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="efa25-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="efa25-178">%(prop)</span></span> |<span data-ttu-id="efa25-179">與 $(name) 類似，但輸出是以 URI 編碼。</span><span class="sxs-lookup"><span data-stu-id="efa25-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="efa25-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="efa25-180">#(prop)</span></span> |<span data-ttu-id="efa25-181">用於 JSON 範本 (例如，用於 iOS 與 Android 範本)。</span><span class="sxs-lookup"><span data-stu-id="efa25-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="efa25-182">除了是用於 JSON 範本 (例如，Apple 範本) 之外，此函式的運作方式與先前指定的 $(prop) 完全相同。</span><span class="sxs-lookup"><span data-stu-id="efa25-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="efa25-183">在此案例中，如果此函式不是包含在 “{‘,’}” 中 (例如 ‘myJsonProperty’ : ‘#(name)’)，並且其評估結果為 Javascript 格式的數字 (例如 regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?)，則輸出 JSON 會是數字。</span><span class="sxs-lookup"><span data-stu-id="efa25-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="efa25-184">例如，‘badge : ‘#(name)’ 會變成 ‘badge’ : 40 (而不是 ‘40‘)。</span><span class="sxs-lookup"><span data-stu-id="efa25-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="efa25-185">‘text’ 或 “text”</span><span class="sxs-lookup"><span data-stu-id="efa25-185">‘text’ or “text”</span></span> |<span data-ttu-id="efa25-186">常值。</span><span class="sxs-lookup"><span data-stu-id="efa25-186">A literal.</span></span> <span data-ttu-id="efa25-187">常值包含以單引號或雙引號括住的任意文字。</span><span class="sxs-lookup"><span data-stu-id="efa25-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="efa25-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="efa25-188">expr1 + expr2</span></span> |<span data-ttu-id="efa25-189">將兩個運算式聯結成單一字串的串連運算子</span><span class="sxs-lookup"><span data-stu-id="efa25-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="efa25-190">運算式可以是前述任一形式。</span><span class="sxs-lookup"><span data-stu-id="efa25-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="efa25-191">使用串連時，整個運算式必須包含在 {} 中。</span><span class="sxs-lookup"><span data-stu-id="efa25-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="efa25-192">例如 {$(prop) + ‘ - ’ + $(prop2)}。</span><span class="sxs-lookup"><span data-stu-id="efa25-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="efa25-193">例如，以下的 XML 範本無效：</span><span class="sxs-lookup"><span data-stu-id="efa25-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="efa25-194">如上面所述，使用串連時，運算式必須包含在大括號中。</span><span class="sxs-lookup"><span data-stu-id="efa25-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="efa25-195">例如：</span><span class="sxs-lookup"><span data-stu-id="efa25-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

