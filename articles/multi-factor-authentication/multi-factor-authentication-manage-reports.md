---
title: "為 Azure MFA 的 aaaAccess 和使用方式報表 |Microsoft 文件"
description: "這說明如何 toouse hello Azure 多重要素驗證功能的報表。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication 中的報告
Azure Multi-Factor Authentication 提供數個供您和貴組織使用的報告。 這些報表都可以透過 hello Multi-factor Authentication 管理入口網站來存取。 hello 以下是 hello 可用報表的清單：

| 報告 | 說明 |
|:--- |:--- |
| 使用量 |hello 使用量報告整體使用量、 使用者摘要和使用者詳細資料的顯示資訊。 |
| 伺服器狀態 |此報告會顯示 hello 的 Multi-factor Authentication Server 與您的帳戶相關聯的狀態。 |
| 已封鎖的使用者歷程記錄 |這些報表顯示要求 tooblock hello 歷程記錄，或解除封鎖使用者。 |
| 已略過的使用者歷程記錄 |顯示使用者的電話號碼的要求 toobypass Multi-factor Authentication 的 hello 歷程記錄。 |
| 詐騙警示 |顯示您所指定的 hello 日期範圍內已提交詐騙警示的歷程記錄。 |
| 已排入佇列 |列出已排入佇列並等候處理的報告和其狀態。 Hello 報表完成時，會提供連結或檢視表 toodownload hello 報告。 |

## <a name="view-reports"></a>檢視報告
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左側選取 Active Directory。
3. 根據您是否使用驗證提供者來遵循下列兩個選項的其中一個︰
   * **選項 1**： 按一下 hello Multi-factor Auth 提供者 索引標籤。選取您的 MFA 提供者，然後按一下 hello**管理**hello 底部的按鈕。
   * **選項 2**： 選取您的目錄，以及移 toohello**設定** 索引標籤。Hello 多因素驗證 區段下，選取**管理服務設定**。 在 hello hello MFA 服務設定 頁面底部，按一下 hello Go toohello 入口網站連結。
4. 在 hello Azure Multi-factor Authentication 管理入口網站，請從 hello 中選取您想要的報表 hello 類型**檢視報表**hello 左瀏覽一節。

<center>![雲端](./media/multi-factor-authentication-manage-reports/report.png)</center>


**其他資源**

* [適用於使用者](end-user/multi-factor-authentication-end-user.md)
* [MSDN 上的 Azure Multi-Factor Authentication](https://msdn.microsoft.com/library/azure/dn249471.aspx)
