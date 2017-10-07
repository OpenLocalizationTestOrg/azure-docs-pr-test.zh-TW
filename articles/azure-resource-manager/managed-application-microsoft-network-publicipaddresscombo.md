---
title: "aaaAzure 受管理的應用程式 PublicIpAddressCombo UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Network.PublicIpAddressCombo UI 項目"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Microsoft.Network.PublicIpAddressCombo UI 元素
選取新的或現有公用 IP 位址的控制項群組。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- 如果 hello 使用者選取 'None' 的公用 IP 位址時，會隱藏 hello 網域名稱標籤 文字方塊。
- 如果 hello 使用者選取現有的公用 IP 位址，已停用 hello 網域名稱標籤 文字方塊。 其值為 hello 選取 IP 位址的 hello 網域名稱標籤。
- 自動根據選取的 hello 位置 hello 網域名稱尾碼 (例如，westus.cloudapp.azure.com) 更新。

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>備註
- 如果`constraints.required.domainNameLabel`設定得**true**，hello 使用者必須提供網域名稱標籤，建立新的公用 IP 位址時。 無法選取沒有標籤的現有公用 IP 位址。
- 如果`options.hideNone`設定得**true**，然後 hello 選項 tooselect**無**隱藏 hello 公用 ip 位址。 hello 預設值是**false**。
- 如果`options.hideDomainNameLabel`設定得**true**，則隱藏 hello 文字方塊的網域名稱標籤。 hello 預設值是**false**。
- 如果`options.hideExisting`為 true，則 hello 使用者不能 toochoose 現有公用 IP 位址。 hello 預設值是**false**。

## <a name="sample-output"></a>範例輸出
如果 hello 使用者選取未公用 IP 位址，hello 是預期產生下列輸出：
```json
{
  "newOrExistingOrNone": "none"
}
```

如果 hello 使用者選取新的或現有的 IP 位址，hello 是預期產生下列輸出：
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- 當指定 `options.hideNone` 時，`newOrExistingOrNone` 一律會傳回 [無]。
- 當指定 `options.hideDomainNameLabel` 時，`domainNameLabel` 為未宣告。

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
