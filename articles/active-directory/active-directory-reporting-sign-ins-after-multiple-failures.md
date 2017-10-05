---
title: "在多次失敗後登入"
description: "指出在多次連續登入嘗試失敗後成功登入的使用者的報告。"
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="52280-103">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="52280-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="52280-104">此報告指出在多次連續登入嘗試失敗後成功登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="52280-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="52280-105">可能的原因包括：</span><span class="sxs-lookup"><span data-stu-id="52280-105">Possible causes include:</span></span>

* <span data-ttu-id="52280-106">使用者忘記密碼</span><span class="sxs-lookup"><span data-stu-id="52280-106">User had forgotten their password</span></span></li><li><span data-ttu-id="52280-107">使用者是成功密碼猜測暴力密碼破解攻擊的受害者</span><span class="sxs-lookup"><span data-stu-id="52280-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="52280-108">這份報告的結果將顯示您在成功登入之前所做的連續失敗登入嘗試次數，以及與第一次成功登入相關聯的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="52280-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="52280-109">**報告設定**︰您可以設定最小的連續失敗登入嘗試次數，必須達到此數目才會顯示於報告中。</span><span class="sxs-lookup"><span data-stu-id="52280-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="52280-110">當您變更此設定時，請務必注意這些變更將不會套用到目前顯示於現有報表中的任何現有失敗登入。</span><span class="sxs-lookup"><span data-stu-id="52280-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="52280-111">不過，會將它們套用到未來所有的登入。</span><span class="sxs-lookup"><span data-stu-id="52280-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="52280-112">只有經過授權的管理員才可以變更此報告。</span><span class="sxs-lookup"><span data-stu-id="52280-112">Changes to this report can only be made by licensed admins.</span></span>

![在多次失敗後登入](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

