---
title: "Azure API 管理原則範例 - 以 JWT 宣告為基礎的授權存取 | Microsoft Docs"
description: "Azure API 管理原則範例 - 示範如何在以 JWT 宣告為基礎的 API 上授權存取特定的 HTTP 方法。"
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 15bd99eeda35161b15e110c3bde0b0bb08fe6d64
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="authorize-access-based-on-jwt-claims"></a>以 JWT 宣告為基礎的授權存取

本文會說明 Azure API 管理原則範例，示範如何在以 JWT 宣告為基礎的 API 上授權存取特定的 HTTP 方法。 若要設定或編輯原則程式碼，請依照[設定或編輯原則](../set-edit-policies.md)中所述的步驟執行。 若要查看其他範例，請參閱[原則範例](../policy-samples.md)。

## <a name="policy"></a>原則

將程式碼貼至 [輸入] 區塊。

[!code-xml[Main](../../../api-management-policy-samples/Snippets/Pre-authorize requests based on HTTP method with validate-jwt.policy.xml)]

## <a name="next-steps"></a>後續步驟

深入了解 APIM 原則：

+ [轉換原則](../api-management-transformation-policies.md)
+ [原則範例](../policy-samples.md)

