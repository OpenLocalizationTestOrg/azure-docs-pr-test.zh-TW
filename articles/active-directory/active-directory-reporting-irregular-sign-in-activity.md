---
title: "異常的登入活動"
description: "這份報告包含由我們的機器學習演算法識別為「異常」的登入。"
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a>異常的登入活動
異常登入是指機器學習服務演算法已經根據結合異常登入位置和裝置的「不可能的行進」條件識別的登入活動。 這可能表示駭客已經使用此帳戶成功登入。
如果我們在 30 天或更少的天數內遇到 10 個或更多異常的登入事件，我們會傳送電子郵件通知給全域管理員。 請務必將 aad-alerts-noreply@mail.windowsazure.com 納入安全寄件者清單中。

