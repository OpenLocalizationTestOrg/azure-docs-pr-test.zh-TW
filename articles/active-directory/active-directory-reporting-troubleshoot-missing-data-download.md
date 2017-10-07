---
title: "疑難排解： 下載 Azure Active Directory 活動記錄在 hello 遺漏資料 |Microsoft 文件"
description: "您提供下載的 Azure Active Directory 活動記錄檔中解析 toomissing 資料。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>我找不到任何資料已下載的 hello Azure Active Directory 活動記錄檔中


## <a name="symptoms"></a>徵兆

我下載 hello 活動記錄檔 （稽核或登入），而且我沒看到所有 hello 記錄 hello 我所選擇的時間。 原因為何？ 

 ![報告](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>原因

當您下載 hello Azure 入口網站中的活動記錄檔時，我們會限制 hello 標尺 too120K 記錄，依照最新。 

## <a name="resolution"></a>解決方案

您可以利用[Azure AD 報告 Api](active-directory-reporting-api-getting-started.md) toofetch tooa 百萬個記錄，在任何給定時間點。 我們建議的方法是的 toorun 上呼叫 hello 報告 Api toofetch 以排程為基礎的指令碼以增量方式記錄一段時間 （例如，每日或每週）。

## <a name="next-steps"></a>後續步驟
請參閱 hello [reporting 常見問題集的 Azure Active Directory](active-directory-reporting-faq.md)。

