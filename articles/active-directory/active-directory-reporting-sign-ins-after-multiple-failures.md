---
title: "aaaSign 集在多個失敗之後"
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
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="ebec5-103">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="ebec5-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="ebec5-104">此報告指出在多次連續登入嘗試失敗後成功登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="ebec5-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="ebec5-105">可能的原因包括：</span><span class="sxs-lookup"><span data-stu-id="ebec5-105">Possible causes include:</span></span>

* <span data-ttu-id="ebec5-106">使用者忘記密碼</span><span class="sxs-lookup"><span data-stu-id="ebec5-106">User had forgotten their password</span></span></li><li><span data-ttu-id="ebec5-107">使用者是成功密碼猜測暴力攻擊的 hello 犧牲者</span><span class="sxs-lookup"><span data-stu-id="ebec5-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="ebec5-108">這份報表的結果會顯示 hello 連續失敗的登入嘗試先前 toohello 成功登入數目，以及相關聯的時間戳記 hello 首次成功登入。</span><span class="sxs-lookup"><span data-stu-id="ebec5-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="ebec5-109">**報告設定**： 您可以設定 hello 最小數目的連續失敗的登入嘗試，而必須進行才能讓它可以顯示在 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="ebec5-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="ebec5-110">當您變更 toothis 將它設定為重要 toonote，這些變更將不會套用的 tooany 現有失敗的登入目前顯示在您現有的報表中。</span><span class="sxs-lookup"><span data-stu-id="ebec5-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="ebec5-111">不過，它們將會套用的 tooall 未來的登入。變更 toothis 報表只可讓授權的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ebec5-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![在多次失敗後登入](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

