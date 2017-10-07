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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="8b60f-103">Azure 資源原則產生的 RequestDisallowedByPolicy 錯誤</span><span class="sxs-lookup"><span data-stu-id="8b60f-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="8b60f-104">本文說明 hello hello RequestDisallowedByPolicy 錯誤原因，它也提供這項錯誤的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8b60f-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="8b60f-105">徵狀</span><span class="sxs-lookup"><span data-stu-id="8b60f-105">Symptom</span></span>

<span data-ttu-id="8b60f-106">當您嘗試 toodo 在部署期間的動作時，您可能會收到**RequestDisallowedByPolicy**執行會阻止 hello 動作的錯誤。</span><span class="sxs-lookup"><span data-stu-id="8b60f-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="8b60f-107">hello 下面是 hello 錯誤的範例：</span><span class="sxs-lookup"><span data-stu-id="8b60f-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="8b60f-108">疑難排解</span><span class="sxs-lookup"><span data-stu-id="8b60f-108">Troubleshooting</span></span>

<span data-ttu-id="8b60f-109">tooretrieve 封鎖、 以部署的 hello 原則的詳細資料會使用下列其中一種 hello 方法 hello:</span><span class="sxs-lookup"><span data-stu-id="8b60f-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="8b60f-110">方法 1</span><span class="sxs-lookup"><span data-stu-id="8b60f-110">Method 1</span></span>

<span data-ttu-id="8b60f-111">在 PowerShell 中，提供該原則識別碼，則為 hello**識別碼**封鎖部署的 hello 原則的相關參數 tooretrieve 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8b60f-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="8b60f-112">方法 2</span><span class="sxs-lookup"><span data-stu-id="8b60f-112">Method 2</span></span> 

<span data-ttu-id="8b60f-113">在 Azure CLI 2.0 中，提供 hello hello 原則定義名稱：</span><span class="sxs-lookup"><span data-stu-id="8b60f-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="8b60f-114">方案</span><span class="sxs-lookup"><span data-stu-id="8b60f-114">Solution</span></span>

<span data-ttu-id="8b60f-115">基於安全性或合規性等因素，您的 IT 部門可能會強制執行資源原則，以禁止建立公用 IP 位址、網路安全性群組、使用者定義的路由或路由表。</span><span class="sxs-lookup"><span data-stu-id="8b60f-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="8b60f-116">Hello 原則在 hello 範例中的 hello 錯誤訊息： hello < 症狀 > 一節所述，命名為**regionPolicyDefinition**，但是可能會不同。</span><span class="sxs-lookup"><span data-stu-id="8b60f-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="8b60f-117">tooresolve 這個問題，請與您的 IT 部門 tooreview hello 資源原則，並決定如何 tooperform hello 要求符合這些原則的動作。</span><span class="sxs-lookup"><span data-stu-id="8b60f-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="8b60f-118">如需詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="8b60f-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="8b60f-119">資源原則概觀</span><span class="sxs-lookup"><span data-stu-id="8b60f-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="8b60f-120">常見的部署錯誤：RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="8b60f-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


