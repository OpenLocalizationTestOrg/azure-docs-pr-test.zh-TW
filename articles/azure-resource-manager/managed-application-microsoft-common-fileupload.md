---
title: "aaaAzure 受管理的應用程式檔案上傳 UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Common.FileUpload UI 項目"
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Microsoft.Common.FileUpload UI 元素
允許使用者 toospecify 一或多個控制項檔案 tooupload。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>備註
- `constraints.accept`指定 hello hello 瀏覽器的 [檔案] 對話方塊中顯示的檔案類型。 請參閱 hello [HTML5 規格](http://www.w3.org/TR/html5/forms.html#attr-input-accept)針對允許的值。 hello 預設值是**null**。
- 如果`options.multiple`設定得**true**，允許 hello 使用者 tooselect 多個瀏覽器 hello 檔案對話方塊中的一個檔案。 hello 預設值是**false**。
- 這個項目支援上傳的檔案中的 hello 值為基礎的兩種模式`options.uploadMode`。 如果**檔案**指定，則 hello 輸出包含 hello hello 檔案儲存為 blob 內容。 如果**url**指定，則 hello 檔案上傳的 tooa 暫存位置，也未 hello 輸出包含 hello 的 hello blob 的 URL。 24 小時之後，就會清除暫存 blob。 hello 預設值是**檔案**。
- hello 值`options.openMode`決定 hello 檔案讀取的方式。 如果預期的 toobe 純文字 hello 檔案，指定**文字**，否則，指定**二進位**。 hello 預設值是**文字**。
- 如果`options.uploadMode`設定得**檔案**和`options.openMode`設定得**二進位**，hello 輸出是 base64 編碼。
- `options.encoding`讀取 hello 檔案時，請指定 hello 編碼 toouse。 hello 預設值是**utf-8**，並用時，才`options.openMode`設定得**文字**。

## <a name="sample-output"></a>範例輸出
如果為 true，options.multiple options.uploadMode 是檔案，輸出會包含 hello hello 檔案內容為 JSON 字串：

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

如果 options.multiple 成立 and'options.uploadMode 檔案，則輸出為 JSON 陣列包含 hello hello 檔案內容：

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

如果 options.multiple 為 false 且 options.uploadMode 為 URL，輸出就會包含 URL 作為 JSON 字串：

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

如果 options.multiple 為 true 且 options.uploadMode 為 URL，輸出就會包含 URL 清單作為 JSON 陣列：
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

當測試 CreateUiDefinition，某些瀏覽器 （例如 Google Chrome) 截斷 hello 瀏覽器主控台中的 hello Microsoft.Common.FileUpload 項目所產生的 Url。 您可能需要 tooright 按一下個別連結 toocopy hello 完整的 Url。


## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
