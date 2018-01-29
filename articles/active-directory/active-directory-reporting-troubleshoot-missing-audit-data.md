---
title: "疑難排解︰Azure Active Directory 活動記錄中的遺漏資料 | Microsoft Docs"
description: "列出 Azure Active Directory 的各種可用報告"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 55587fb4ff6d8a2130eb838782a65788fb2dd2b3
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2018
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a>找不到我在 Azure Active Directory 活動記錄中執行的某些動作


## <a name="symptoms"></a>徵兆

我在 Azure 入口網站中執行某些動作，並預期要在 `Activity logs > Audit Logs` 刀鋒視窗中查看這些動作的稽核記錄，但卻找不到。

 ![報告](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a>原因

動作不會立即出現在活動稽核記錄中。 從執行作業的時間起，可能要花 15 分鐘到 1 小時才可在入口網站中看到稽核記錄。

## <a name="resolution"></a>解決方案

等候 15 分鐘到 1 小時的時間，檢查動作是否出現在記錄中。 如果您仍看不到它們，請向我們提出支援票證，我們將探討它。


## <a name="next-steps"></a>後續步驟
請參閱 [Azure Active Directory 報告常見問題集](active-directory-reporting-faq.md)。

