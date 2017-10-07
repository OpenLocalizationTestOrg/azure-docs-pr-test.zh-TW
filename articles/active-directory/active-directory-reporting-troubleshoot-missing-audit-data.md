---
title: "疑難排解： 遺漏 hello Azure Active Directory 活動記錄檔中的資料 |Microsoft 文件"
description: "列出 Azure Active Directory 的 hello 各種可用的報表"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 7bbec94ab42eb5b54a7e65e124060d057b4a1a34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-hello-azure-active-directory-activity-log"></a>我找不到我 hello Azure Active Directory 活動記錄檔中執行某些動作


## <a name="symptoms"></a>徵兆

我在 hello Azure 入口網站中執行某些動作，而且預期 toosee hello 的稽核記錄，這些動作在 hello`Activity logs > Audit Logs`刀鋒視窗中，但是無法找到它們。

 ![報告](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a>原因

動作不會立即出現 hello 活動稽核記錄檔。 它可以需要 15 分鐘 tooan 小時 toosee hello 稽核記錄在 hello 入口網站，從 hello hello 作業的時間。

## <a name="resolution"></a>解決方案

等候 15 分鐘 tooan 小時，請參閱是否 hello 動作會出現在 hello 記錄檔。 如果您仍看不到它們，請向我們提出支援票證，我們將探討它。


## <a name="next-steps"></a>後續步驟
請參閱 hello [reporting 常見問題集的 Azure Active Directory](active-directory-reporting-faq.md)。

