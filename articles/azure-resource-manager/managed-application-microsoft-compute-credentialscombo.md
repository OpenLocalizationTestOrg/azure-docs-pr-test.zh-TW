---
title: "Azure 受管理的應用程式 CredentialsCombo UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Compute.CredentialsCombo UI 元素"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="cfd02-103">Microsoft.Compute.CredentialsCombo UI 元素</span><span class="sxs-lookup"><span data-stu-id="cfd02-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="cfd02-104">使用 Windows 和 Linux 密碼和 SSH 公開金鑰內建驗證的控制項群組。</span><span class="sxs-lookup"><span data-stu-id="cfd02-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="cfd02-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="cfd02-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="cfd02-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="cfd02-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="cfd02-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="cfd02-108">Schema</span></span>
<span data-ttu-id="cfd02-109">如果 `osPlatform` 是 **Windows**，則會使用下列結構描述︰</span><span class="sxs-lookup"><span data-stu-id="cfd02-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="cfd02-110">如果 `osPlatform` 是 **Linux**，則會使用下列結構描述︰</span><span class="sxs-lookup"><span data-stu-id="cfd02-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="cfd02-111">備註</span><span class="sxs-lookup"><span data-stu-id="cfd02-111">Remarks</span></span>
- <span data-ttu-id="cfd02-112">必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="cfd02-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="cfd02-113">如果將 `constraints.required` 設為 **true**，則密碼或 SSH 公開金鑰文字方塊必須包含值，才能順利通過驗證。</span><span class="sxs-lookup"><span data-stu-id="cfd02-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="cfd02-114">預設值為 **true**。</span><span class="sxs-lookup"><span data-stu-id="cfd02-114">The default value is **true**.</span></span>
- <span data-ttu-id="cfd02-115">如果將 `options.hideConfirmation` 設為 **true**，就會將確認使用者密碼的第二個文字方塊加以隱藏。</span><span class="sxs-lookup"><span data-stu-id="cfd02-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="cfd02-116">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="cfd02-116">The default value is **false**.</span></span>
- <span data-ttu-id="cfd02-117">如果將 `options.hidePassword` 設為 **true**，就會將使用密碼驗證的選項加以隱藏。</span><span class="sxs-lookup"><span data-stu-id="cfd02-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="cfd02-118">只有在 `osPlatform` 是 **Linux** 時才可以使用。</span><span class="sxs-lookup"><span data-stu-id="cfd02-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="cfd02-119">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="cfd02-119">The default value is **false**.</span></span>
- <span data-ttu-id="cfd02-120">可使用 `customPasswordRegex` 屬性將允許密碼上的其他條件約束加以實作。</span><span class="sxs-lookup"><span data-stu-id="cfd02-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="cfd02-121">密碼無法自訂驗證時，就會顯示 `customValidationMessage` 中的字串。</span><span class="sxs-lookup"><span data-stu-id="cfd02-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="cfd02-122">這兩個屬性的預設值是 **null**。</span><span class="sxs-lookup"><span data-stu-id="cfd02-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="cfd02-123">範例輸出</span><span class="sxs-lookup"><span data-stu-id="cfd02-123">Sample output</span></span>
<span data-ttu-id="cfd02-124">如果 `osPlatform` 是 **Windows**，或是使用者提供了密碼而不是 SSH 公開金鑰，則預期會產生下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="cfd02-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="cfd02-125">如果使用者提供了 SSH 公開金鑰，則預期會產生下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="cfd02-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="cfd02-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cfd02-126">Next steps</span></span>
* <span data-ttu-id="cfd02-127">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cfd02-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="cfd02-128">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cfd02-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="cfd02-129">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="cfd02-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
