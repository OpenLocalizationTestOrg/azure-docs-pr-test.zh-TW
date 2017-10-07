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
# <a name="sign-ins-after-multiple-failures"></a>在多次失敗後登入
此報告指出在多次連續登入嘗試失敗後成功登入的使用者。 可能的原因包括：

* 使用者忘記密碼</li><li>使用者是成功密碼猜測暴力攻擊的 hello 犧牲者

這份報表的結果會顯示 hello 連續失敗的登入嘗試先前 toohello 成功登入數目，以及相關聯的時間戳記 hello 首次成功登入。

**報告設定**： 您可以設定 hello 最小數目的連續失敗的登入嘗試，而必須進行才能讓它可以顯示在 hello 報表。 當您變更 toothis 將它設定為重要 toonote，這些變更將不會套用的 tooany 現有失敗的登入目前顯示在您現有的報表中。 不過，它們將會套用的 tooall 未來的登入。變更 toothis 報表只可讓授權的系統管理員。

![在多次失敗後登入](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

