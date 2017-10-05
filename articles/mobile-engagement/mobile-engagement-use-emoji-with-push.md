---
title: "在 Azure Mobile Engagement 內使用 Emoji 表情符號"
description: "如何在推播通知內使用 Emoji 表情符號"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="2d17b-103">在推播通知內使用 Emoji 表情符號</span><span class="sxs-lookup"><span data-stu-id="2d17b-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="2d17b-104">只要幾個簡單步驟，您就可以在推播通知中加入 Emoji 表情符號：</span><span class="sxs-lookup"><span data-stu-id="2d17b-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="2d17b-105">首先您需要尋找要在訊息中傳送的 Emoji。</span><span class="sxs-lookup"><span data-stu-id="2d17b-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="2d17b-106">請確定您要選取的 Emoji 可受目標裝置支援，因為裝置製造商需要一些時間才能將新核准的 Emoji 新增至裝置平台。</span><span class="sxs-lookup"><span data-stu-id="2d17b-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="2d17b-107">在 **Windows** 上 - 您可以瀏覽這個 [連結](http://apps.timwhitlock.info/emoji/tables/unicode) ，並複製 'Native' 圖示。</span><span class="sxs-lookup"><span data-stu-id="2d17b-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="2d17b-108">在 **Mac** 上 - 您可以在字典應用程式中的 [編輯] -> [表情與符號] 中找到表情符號。</span><span class="sxs-lookup"><span data-stu-id="2d17b-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="2d17b-109">現在，請移至 Azure Mobile Engagement 入口網站的 [觸達]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2d17b-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="2d17b-110">選取您的推播通知類型 (通知、投票等等)。</span><span class="sxs-lookup"><span data-stu-id="2d17b-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="2d17b-111">對於此範例，我們選擇公告推播。</span><span class="sxs-lookup"><span data-stu-id="2d17b-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="2d17b-112">指定通知的不同欄位，直到您到達通知的文字。</span><span class="sxs-lookup"><span data-stu-id="2d17b-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="2d17b-113">這就是您加入 Emoji 表情符號的位置。</span><span class="sxs-lookup"><span data-stu-id="2d17b-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="2d17b-114">您可以選擇將它放在標題、訊息或兩者中。</span><span class="sxs-lookup"><span data-stu-id="2d17b-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="2d17b-115">您必須拖放或複製您從上述位置找到的表情符號。</span><span class="sxs-lookup"><span data-stu-id="2d17b-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="2d17b-116">完成通知的其他欄位，然後儲存。</span><span class="sxs-lookup"><span data-stu-id="2d17b-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="2d17b-117">當您執行測試或啟動公告時，您會看到具有指定表情符號的通知。</span><span class="sxs-lookup"><span data-stu-id="2d17b-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="2d17b-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="2d17b-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

