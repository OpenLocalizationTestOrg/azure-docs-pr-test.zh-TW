---
title: "aaaAzure 受管理的應用程式 CredentialsCombo UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Compute.CredentialsCombo UI 項目"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="1df10-103">Microsoft.Compute.CredentialsCombo UI 元素</span><span class="sxs-lookup"><span data-stu-id="1df10-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="1df10-104">使用 Windows 和 Linux 密碼和 SSH 公開金鑰內建驗證的控制項群組。</span><span class="sxs-lookup"><span data-stu-id="1df10-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="1df10-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="1df10-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1df10-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="1df10-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="1df10-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="1df10-108">Schema</span></span>
<span data-ttu-id="1df10-109">如果`osPlatform`是**Windows**，則 hello 下列結構描述會使用：</span><span class="sxs-lookup"><span data-stu-id="1df10-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="1df10-110">如果`osPlatform`是**Linux**，則 hello 下列結構描述會使用：</span><span class="sxs-lookup"><span data-stu-id="1df10-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="1df10-111">備註</span><span class="sxs-lookup"><span data-stu-id="1df10-111">Remarks</span></span>
- <span data-ttu-id="1df10-112">必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="1df10-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="1df10-113">如果`constraints.required`設定得**true**、 然後 hello 密碼或 SSH 公用金鑰文字方塊必須包含值 toovalidate 成功。</span><span class="sxs-lookup"><span data-stu-id="1df10-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="1df10-114">hello 預設值是**true**。</span><span class="sxs-lookup"><span data-stu-id="1df10-114">hello default value is **true**.</span></span>
- <span data-ttu-id="1df10-115">如果`options.hideConfirmation`設定得**true**，則會隱藏 hello 第二個文字方塊中確認 hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="1df10-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="1df10-116">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="1df10-116">hello default value is **false**.</span></span>
- <span data-ttu-id="1df10-117">如果`options.hidePassword`設定得**true**，則會隱藏 hello 選項 toouse 密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="1df10-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="1df10-118">只有在 `osPlatform` 是 **Linux** 時才可以使用。</span><span class="sxs-lookup"><span data-stu-id="1df10-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="1df10-119">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="1df10-119">The default value is **false**.</span></span>
- <span data-ttu-id="1df10-120">Hello 的其他條件約束允許密碼可以實作使用 hello`customPasswordRegex`屬性。</span><span class="sxs-lookup"><span data-stu-id="1df10-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="1df10-121">字串中的 hello`customValidationMessage`密碼自訂的驗證失敗時顯示。</span><span class="sxs-lookup"><span data-stu-id="1df10-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="1df10-122">hello 這兩個屬性的預設值是**null**。</span><span class="sxs-lookup"><span data-stu-id="1df10-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1df10-123">範例輸出</span><span class="sxs-lookup"><span data-stu-id="1df10-123">Sample output</span></span>
<span data-ttu-id="1df10-124">如果`osPlatform`是**Windows**，或 hello 使用者提供的密碼，而不是有 SSH 公開金鑰，然後 hello 預期產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="1df10-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="1df10-125">如果 hello 使用者提供的 SSH 公開金鑰，然後 hello 是預期產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="1df10-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="1df10-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1df10-126">Next steps</span></span>
* <span data-ttu-id="1df10-127">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1df10-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1df10-128">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1df10-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1df10-129">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="1df10-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
