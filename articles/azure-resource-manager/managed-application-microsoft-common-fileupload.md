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
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="803a6-103">Microsoft.Common.FileUpload UI 元素</span><span class="sxs-lookup"><span data-stu-id="803a6-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="803a6-104">允許使用者 toospecify 一或多個控制項檔案 tooupload。</span><span class="sxs-lookup"><span data-stu-id="803a6-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="803a6-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="803a6-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="803a6-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="803a6-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="803a6-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="803a6-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="803a6-109">備註</span><span class="sxs-lookup"><span data-stu-id="803a6-109">Remarks</span></span>
- <span data-ttu-id="803a6-110">`constraints.accept`指定 hello hello 瀏覽器的 [檔案] 對話方塊中顯示的檔案類型。</span><span class="sxs-lookup"><span data-stu-id="803a6-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="803a6-111">請參閱 hello [HTML5 規格](http://www.w3.org/TR/html5/forms.html#attr-input-accept)針對允許的值。</span><span class="sxs-lookup"><span data-stu-id="803a6-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="803a6-112">hello 預設值是**null**。</span><span class="sxs-lookup"><span data-stu-id="803a6-112">hello default value is **null**.</span></span>
- <span data-ttu-id="803a6-113">如果`options.multiple`設定得**true**，允許 hello 使用者 tooselect 多個瀏覽器 hello 檔案對話方塊中的一個檔案。</span><span class="sxs-lookup"><span data-stu-id="803a6-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="803a6-114">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="803a6-114">hello default value is **false**.</span></span>
- <span data-ttu-id="803a6-115">這個項目支援上傳的檔案中的 hello 值為基礎的兩種模式`options.uploadMode`。</span><span class="sxs-lookup"><span data-stu-id="803a6-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="803a6-116">如果**檔案**指定，則 hello 輸出包含 hello hello 檔案儲存為 blob 內容。</span><span class="sxs-lookup"><span data-stu-id="803a6-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="803a6-117">如果**url**指定，則 hello 檔案上傳的 tooa 暫存位置，也未 hello 輸出包含 hello 的 hello blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="803a6-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="803a6-118">24 小時之後，就會清除暫存 blob。</span><span class="sxs-lookup"><span data-stu-id="803a6-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="803a6-119">hello 預設值是**檔案**。</span><span class="sxs-lookup"><span data-stu-id="803a6-119">hello default value is **file**.</span></span>
- <span data-ttu-id="803a6-120">hello 值`options.openMode`決定 hello 檔案讀取的方式。</span><span class="sxs-lookup"><span data-stu-id="803a6-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="803a6-121">如果預期的 toobe 純文字 hello 檔案，指定**文字**，否則，指定**二進位**。</span><span class="sxs-lookup"><span data-stu-id="803a6-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="803a6-122">hello 預設值是**文字**。</span><span class="sxs-lookup"><span data-stu-id="803a6-122">hello default value is **text**.</span></span>
- <span data-ttu-id="803a6-123">如果`options.uploadMode`設定得**檔案**和`options.openMode`設定得**二進位**，hello 輸出是 base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="803a6-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="803a6-124">`options.encoding`讀取 hello 檔案時，請指定 hello 編碼 toouse。</span><span class="sxs-lookup"><span data-stu-id="803a6-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="803a6-125">hello 預設值是**utf-8**，並用時，才`options.openMode`設定得**文字**。</span><span class="sxs-lookup"><span data-stu-id="803a6-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="803a6-126">範例輸出</span><span class="sxs-lookup"><span data-stu-id="803a6-126">Sample output</span></span>
<span data-ttu-id="803a6-127">如果為 true，options.multiple options.uploadMode 是檔案，輸出會包含 hello hello 檔案內容為 JSON 字串：</span><span class="sxs-lookup"><span data-stu-id="803a6-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="803a6-128">如果 options.multiple 成立 and'options.uploadMode 檔案，則輸出為 JSON 陣列包含 hello hello 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="803a6-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="803a6-129">如果 options.multiple 為 false 且 options.uploadMode 為 URL，輸出就會包含 URL 作為 JSON 字串：</span><span class="sxs-lookup"><span data-stu-id="803a6-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="803a6-130">如果 options.multiple 為 true 且 options.uploadMode 為 URL，輸出就會包含 URL 清單作為 JSON 陣列：</span><span class="sxs-lookup"><span data-stu-id="803a6-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="803a6-131">當測試 CreateUiDefinition，某些瀏覽器 （例如 Google Chrome) 截斷 hello 瀏覽器主控台中的 hello Microsoft.Common.FileUpload 項目所產生的 Url。</span><span class="sxs-lookup"><span data-stu-id="803a6-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="803a6-132">您可能需要 tooright 按一下個別連結 toocopy hello 完整的 Url。</span><span class="sxs-lookup"><span data-stu-id="803a6-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="803a6-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="803a6-133">Next steps</span></span>
* <span data-ttu-id="803a6-134">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="803a6-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="803a6-135">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="803a6-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="803a6-136">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="803a6-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
