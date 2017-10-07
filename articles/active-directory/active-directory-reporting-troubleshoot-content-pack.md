---
title: "對 Azure Active Directory 活動記錄內容套件錯誤進行疑難排解 | Microsoft Docs"
description: "您提供的錯誤訊息的 hello Azure Active Directory 活動內容組件和步驟 toofix 清單它們。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>對 Azure Active Directory 活動記錄內容套件錯誤進行疑難排解 


使用 Azure Active Directory preview hello Power BI 內容套件，它時可能遇到下列錯誤 hello: 

- [重新整理失敗](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [失敗的 tooupdate 資料來源認證](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [匯入資料的時間太長](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
本主題將提供您 hello 的可能原因的相關資訊及如何 toofix 這些錯誤。
 
## <a name="refresh-failed"></a>重新整理失敗 
 
**此錯誤會顯示如何**： 從 Power BI 或 hello 重新整理記錄中的失敗的狀態的電子郵件。 


| 原因 | 如何 toofix |
| ---   | ---        |
| 重新整理的失敗時已重設 hello hello 連線的使用者 toohello 內容套件的認證，但不是會在 hello hello hello 內容套件的連接設定更新，可能導致錯誤。 | 在 Power BI 中，找出 hello 資料集對應 toohello Azure Active Directory 活動記錄檔儀表板 （Azure Active Directory 活動記錄檔），選擇 排程重新整理，然後輸入您的 Azure AD 認證。 |
| 重新整理可能會在基礎內容套件的 hello toodata 問題而失敗。 | 提出支援票證。 如需詳細資訊，請參閱[tooget 如何支援 Azure Active directory](active-directory-troubleshooting-support-howto.md)。|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>失敗的 tooupdate 資料來源認證 
 
**此錯誤會顯示如何**： 在 Power BI 中，當您連線 toohello Azure Active Directory 活動記錄 （預覽） 內容套件。 

| 原因 | 如何 toofix |
| ---   | ---        |
| hello 連接的使用者是既不是全域管理員也不安全讀取器或安全性管理員。 | 使用全域管理員或安全性讀取器或安全性管理員 tooaccess hello 內容套件的帳戶。 |
| 您的租用戶不是 Premium 租用戶，或者沒有任何具備 Premium 授權檔案的使用者。 | 提出支援票證。 如需詳細資訊，請參閱[tooget 如何支援 Azure Active directory](active-directory-troubleshooting-support-howto.md)。|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>匯入資料的時間太長 
 
**此錯誤會顯示如何**： 在 Power BI 中，一旦您已經連接您的內容套件 hello 資料匯入程序啟動 tooprepare 儀表板的 Azure Active Directory 活動記錄檔。 您會看到 hello 訊息: 「*匯入資料...*"  

| 原因 | 如何 toofix |
| ---   | ---        |
| 取決於您的租用戶的 hello 規模、 此步驟可能需要幾分鐘 too30 分鐘。 | 請耐心等候。 如果 hello 訊息不會變更 tooshowing 儀表板在一小時內，請提出支援票證。 如需詳細資訊，請參閱[tooget 如何支援 Azure Active directory](active-directory-troubleshooting-support-howto.md)。|

## <a name="next-steps"></a>後續步驟

按一下 tooinstall hello Azure Active Directory 預覽的 Power BI 內容套件[這裡](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/)。


