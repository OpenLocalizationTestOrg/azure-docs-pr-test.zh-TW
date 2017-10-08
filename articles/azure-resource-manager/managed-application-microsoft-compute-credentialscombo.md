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
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Microsoft.Compute.CredentialsCombo UI 元素
使用 Windows 和 Linux 密碼和 SSH 公開金鑰內建驗證的控制項群組。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>結構描述
如果`osPlatform`是**Windows**，則 hello 下列結構描述會使用：
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

如果`osPlatform`是**Linux**，則 hello 下列結構描述會使用：
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

## <a name="remarks"></a>備註
- 必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。
- 如果`constraints.required`設定得**true**、 然後 hello 密碼或 SSH 公用金鑰文字方塊必須包含值 toovalidate 成功。 hello 預設值是**true**。
- 如果`options.hideConfirmation`設定得**true**，則會隱藏 hello 第二個文字方塊中確認 hello 使用者的密碼。 hello 預設值是**false**。
- 如果`options.hidePassword`設定得**true**，則會隱藏 hello 選項 toouse 密碼驗證。 只有在 `osPlatform` 是 **Linux** 時才可以使用。 預設值為 **false**。
- Hello 的其他條件約束允許密碼可以實作使用 hello`customPasswordRegex`屬性。 字串中的 hello`customValidationMessage`密碼自訂的驗證失敗時顯示。 hello 這兩個屬性的預設值是**null**。

## <a name="sample-output"></a>範例輸出
如果`osPlatform`是**Windows**，或 hello 使用者提供的密碼，而不是有 SSH 公開金鑰，然後 hello 預期產生下列輸出：

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

如果 hello 使用者提供的 SSH 公開金鑰，然後 hello 是預期產生下列輸出：
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
