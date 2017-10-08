---
title: "aaaAzure 受管理的應用程式建立使用者定義函式 |Microsoft 文件"
description: "描述 hello 函式 toouse 建構 Azure 受管理的應用程式的 UI 定義時"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>CreateUiDefinition 元素
本文說明 hello 結構描述和屬性的所有支援的 CreateUiDefinition 項目。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用這些元素。 hello 結構描述的大部分項目如下所示：

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| 屬性 | 必要 | 說明 |
| -------- | -------- | ----------- |
| 名稱 | 是 | 內部識別碼 tooreference 元素的特定執行個體。 hello hello 項目名稱的最常見的用法是在`outputs`，其中 hello hello 輸出值會指定項目是對應的 toohello hello 範本參數。 您也可以使用它 toobind hello 輸出值的項目 toohello`defaultValue`另一個項目。 |
| 類型 | 是 | hello UI 控制 toorender hello 項目。 如需支援類型的清單，請參閱[元素](#elements)。 |
| 標籤 | 是 | hello 顯示 hello 項目的文字。 某些項目型別包含多個標籤，因此 hello 值可以包含多個字串的物件。 |
| defaultValue | 否 | hello hello 項目的預設值。 某些項目類型支援複雜的預設值，因此 hello 值可以是物件。 |
| 工具提示 | 否 | hello 項目的 hello 工具提示中的 hello 文字 toodisplay。 類似太`label`，某些項目支援多個工具提示字串。 您可以使用 Markdown 語法將內嵌連結進行內嵌。
| 條件約束 | 否 | 一或多個屬性都使用的 toocustomize hello 驗證行為的 hello 項目。 項目類型會因條件約束的 hello 支援屬性。 某些項目類型不支援自訂 hello 驗證行為，並因此會有任何條件約束屬性。 |
| options | 否 | 自訂 hello 元素 hello 行為的其他屬性。 類似太`constraints`，支援的 hello 屬性會因項目類型。 |
| 可見 | 否 | 指出是否要顯示 hello 項目。 如果`true`，會顯示 hello 項目和適用的子項目。 hello 預設值是`true`。 使用[邏輯函數](managed-application-createuidefinition-functions.md#logical-functions)toodynamically 控制這個屬性的值。

## <a name="elements"></a>元素

hello 文件結構描述中，每個項目包含 UI 範例，註解在 hello 行為 hello 項目 （通常是關於驗證和支援的自訂） 和輸出範例。

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
