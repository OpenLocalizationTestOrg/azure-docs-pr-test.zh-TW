---
title: "aaaAzure SQL Database 動態資料遮罩 |Microsoft 文件"
description: "SQL Database 動態資料遮罩會限制機密資料暴露它 toonon 權限的使用者"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>SQL Database 動態資料遮罩

SQL Database 動態資料遮罩會限制機密資料暴露其 toonon 權限的使用者。 

動態資料遮罩藉此協助防止未經授權的存取 toosensitive 資料啟用客戶 toodesignate 多少 hello 敏感性資料 tooreveal hello 應用程式層上的影響降至最低。 這是 hello hello 查詢結果集內的機密資料隱藏在指定的資料庫欄位，而 hello 資料庫中的 hello 資料不會變更以原則為基礎的安全性功能。

例如，撥接中心的服務代表可能會呼叫端識別其信用卡號碼其中幾個數字，但這些項目不應該是完整的資料公開 toohello 服務代表通話。 所有遮罩但 hello 最後四位數的 hello 任何查詢結果集內任何信用卡號碼可以定義遮罩規則。 另舉一例，適當的資料遮罩可以是定義的 tooprotect 個人識別資訊 (PII) 資料，以便開發人員可以查詢生產環境，供疑難排解之用，而不會違反法務遵循規定。

## <a name="sql-database-dynamic-data-masking-basics"></a>SQL Database 動態資料遮罩的基本概念
您設定的動態資料遮罩原則中 hello Azure 入口網站選取 hello 動態資料遮罩刀鋒視窗中設定 SQL 資料庫或設定 刀鋒視窗中的作業。

### <a name="dynamic-data-masking-permissions"></a>動態資料遮罩權限
Hello Azure 資料庫系統管理員、 伺服器管理員或安全性主管人員角色可以設定動態資料遮罩。

### <a name="dynamic-data-masking-policy"></a>動態資料遮罩原則
* **從遮罩排除 SQL 使用者**-一組 SQL 使用者或 AAD 身分識別，讓未遮罩的資料 hello SQL 查詢的結果。 系統管理員權限的使用者一律會從遮罩排除，請參閱 hello 原始資料，沒有任何遮罩。
* **遮罩規則**-一組定義指定遮罩欄位 toobe hello 和 hello 遮罩函數所使用的規則。 可以使用資料庫結構描述名稱、 資料表名稱，以及資料行名稱來定義指定欄位的 hello。
* **遮罩函數**-一組控制 hello 公開針對不同的案例資料的方法。

| 遮罩函數 | 遮罩邏輯 |
| --- | --- |
| **預設值** |**完整資料加上遮罩相應 toohello hello 的類型指定的欄位**<br/><br/>• 使用 XXXX 或如果 hello hello 欄位大小少於 4 個字元的字串資料類型 （nchar、 ntext、 nvarchar） 較少的 x。<br/>• 針對數值資料類型 (bigint、bit、decimal、int、money、numeric、smallint、smallmoney、tinyint、float、real)，使用零值。<br/>• 針對日期/時間資料類型 (date、datetime2、datetime、datetimeoffset、smalldatetime、time)，使用 01-01-1900 時間。<br/>• SQL variant，hello 型別的預設值 hello 目前會使用。<br/>• For XML hello 文件<masked/>用。<br/>• 針對特殊資料類型 (時間戳記、資料表、hierarchyid、GUID、二進位值、影像、varbinary spatial 類型)，使用空值。 |
| **信用卡** |**此遮罩方法，可公開 hello 的最後 4 位數指定欄位的 hello** ，並加入做為前置詞的信用卡 hello 形式常數字串。<br/><br/>XXXX-XXXX-XXXX-1234 |
| **電子郵件** |**此遮罩方法，可 hello 第一個字母曝光，並以 XXX.com 取代 hello 網域**使用常數字串中的前置詞 hello 形式為電子郵件地址。<br/><br/>aXX@XXXX.com |
| **隨機數字** |**此遮罩方法會產生一個隨機數字**toohello，根據選取的界限與實際的資料類型。 如果指定界限的 hello 相等，遮罩函數的 hello 是固定數目。<br/><br/>![導覽窗格](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **自訂文字** |**此遮罩的方法，公開哪些先 hello 和最後一個字元**，並在 hello 中間加入自訂填補字串。 如果 hello 原始字串小於 hello 公開前置詞和後置詞，則會使用 hello 填補字串。 <br/>prefix[padding]suffix<br/><br/>![導覽窗格](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>建議的欄位 toomask
hello DDM 建議引擎，加上旗標特定資料庫中的欄位做為可能含有機密欄位，可能是適合用來遮罩。 在 hello 動態資料遮罩刀鋒視窗中 hello 入口網站中，您會看到 hello 建議為您的資料庫資料行。 您只需要 toodo 是按一下**新增遮罩**一或多個資料行，然後**儲存**tooapply 遮罩這些欄位。

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>使用 PowerShell Cmdlet 為您的資料庫設定動態資料遮罩
請參閱 [Azure SQL Database Cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx)。

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>使用 REST API 為您的資料庫設定動態資料遮罩
請參閱 [Azure SQL Database 的作業](https://msdn.microsoft.com/library/dn505719.aspx)。

