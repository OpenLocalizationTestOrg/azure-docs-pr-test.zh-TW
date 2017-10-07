---
title: "使用 Azure 資源原則 aaaRequestDisallowedByPolicy 錯誤 |Microsoft 文件"
description: "描述 hello hello RequestDisallowedByPolicy 錯誤原因。"
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Azure 資源原則產生的 RequestDisallowedByPolicy 錯誤

本文說明 hello hello RequestDisallowedByPolicy 錯誤原因，它也提供這項錯誤的解決方案。

## <a name="symptom"></a>徵狀

當您嘗試 toodo 在部署期間的動作時，您可能會收到**RequestDisallowedByPolicy**執行會阻止 hello 動作的錯誤。 hello 下面是 hello 錯誤的範例：

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>疑難排解

tooretrieve 封鎖、 以部署的 hello 原則的詳細資料會使用下列其中一種 hello 方法 hello:

### <a name="method-1"></a>方法 1

在 PowerShell 中，提供該原則識別碼，則為 hello**識別碼**封鎖部署的 hello 原則的相關參數 tooretrieve 詳細資料。

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>方法 2 

在 Azure CLI 2.0 中，提供 hello hello 原則定義名稱： 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>方案

基於安全性或合規性等因素，您的 IT 部門可能會強制執行資源原則，以禁止建立公用 IP 位址、網路安全性群組、使用者定義的路由或路由表。 Hello 原則在 hello 範例中的 hello 錯誤訊息： hello < 症狀 > 一節所述，命名為**regionPolicyDefinition**，但是可能會不同。
tooresolve 這個問題，請與您的 IT 部門 tooreview hello 資源原則，並決定如何 tooperform hello 要求符合這些原則的動作。


如需詳細資訊，請參閱下列文章 hello:

- [資源原則概觀](resource-manager-policy.md)
- [常見的部署錯誤：RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


