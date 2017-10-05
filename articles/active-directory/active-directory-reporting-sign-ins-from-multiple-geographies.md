---
title: "從多個地理區域登入"
description: "這份報告指出使用者有兩次登入似乎來自不同的地區，且使用者不可能在登入間的時間內在這兩個區域之間移動。"
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="5b06c-103">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="5b06c-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="5b06c-104">這份報告包含使用者的成功登入，而其中有兩次登入似乎來自不同的區域，且使用者不可能在登入間的時間內在這兩個區域之間移動。</span><span class="sxs-lookup"><span data-stu-id="5b06c-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="5b06c-105">可能的原因包括：</span><span class="sxs-lookup"><span data-stu-id="5b06c-105">Possible causes include:</span></span>

* <span data-ttu-id="5b06c-106">使用者與其他使用者共用其密碼</span><span class="sxs-lookup"><span data-stu-id="5b06c-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="5b06c-107">使用者正在使用遠端桌面啟動 Web 瀏覽器來登入</span><span class="sxs-lookup"><span data-stu-id="5b06c-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="5b06c-108">駭客已從不同的國家/地區登入使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="5b06c-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="5b06c-109">使用者使用 VPN 或 Proxy</span><span class="sxs-lookup"><span data-stu-id="5b06c-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="5b06c-110">使用者同時從多個裝置登入 (例如桌上型電腦和行動電話)，而行動電話的 IP 位址異常。</span><span class="sxs-lookup"><span data-stu-id="5b06c-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="5b06c-111">這份報表的結果會顯示成功登入事件，以及登入間的時間、登入疑似源自哪些區域，以及這些區域間估計的移動時間。</span><span class="sxs-lookup"><span data-stu-id="5b06c-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="5b06c-112">顯示的移動時間只是估計值，而且可能不同於位置之間的實際移動時間。</span><span class="sxs-lookup"><span data-stu-id="5b06c-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![從多個地理區域登入](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

