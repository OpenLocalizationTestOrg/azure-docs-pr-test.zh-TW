---
title: "Azure 受管理的應用程式 FileUpload UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Common.FileUpload UI 元素"
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
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="516f7-103">Microsoft.Common.FileUpload UI 元素</span><span class="sxs-lookup"><span data-stu-id="516f7-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="516f7-104">控制項可讓使用者指定要上傳的一個或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="516f7-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="516f7-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="516f7-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="516f7-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="516f7-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="516f7-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="516f7-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="516f7-109">備註</span><span class="sxs-lookup"><span data-stu-id="516f7-109">Remarks</span></span>
- <span data-ttu-id="516f7-110">`constraints.accept` 會指定在瀏覽器的 [檔案] 對話方塊中顯示的檔案類型。</span><span class="sxs-lookup"><span data-stu-id="516f7-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="516f7-111">請參閱 [HTML5 規格](http://www.w3.org/TR/html5/forms.html#attr-input-accept) 以取得允許的值。</span><span class="sxs-lookup"><span data-stu-id="516f7-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="516f7-112">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="516f7-112">The default value is **null**.</span></span>
- <span data-ttu-id="516f7-113">如果將 `options.multiple` 設為 **true**，使用者就允許在瀏覽器的 [檔案] 對話方塊中選取一個以上的檔案。</span><span class="sxs-lookup"><span data-stu-id="516f7-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="516f7-114">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="516f7-114">The default value is **false**.</span></span>
- <span data-ttu-id="516f7-115">這個元素會根據 `options.uploadMode` 的值，支援兩種檔案上傳模式。</span><span class="sxs-lookup"><span data-stu-id="516f7-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="516f7-116">如果是指定 **file**，輸出就會包含檔案內容作為 blob。</span><span class="sxs-lookup"><span data-stu-id="516f7-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="516f7-117">如果是指定 **url**，檔案就會上傳至暫存位置，而輸出會包含 blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="516f7-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="516f7-118">24 小時之後，就會清除暫存 blob。</span><span class="sxs-lookup"><span data-stu-id="516f7-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="516f7-119">預設值為 **file**。</span><span class="sxs-lookup"><span data-stu-id="516f7-119">The default value is **file**.</span></span>
- <span data-ttu-id="516f7-120">`options.openMode` 的值會決定讀取檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="516f7-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="516f7-121">如果預期是純文字檔案，則指定為 **text**；否則，指定為 **binary**。</span><span class="sxs-lookup"><span data-stu-id="516f7-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="516f7-122">預設值為 **text**。</span><span class="sxs-lookup"><span data-stu-id="516f7-122">The default value is **text**.</span></span>
- <span data-ttu-id="516f7-123">如果將 `options.uploadMode` 設為 **file**，且將 `options.openMode` 設為 **binary**，輸出就會是 base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="516f7-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="516f7-124">`options.encoding` 會指定讀取檔案時要使用的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="516f7-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="516f7-125">預設值為 **UTF-8**，且僅在 `options.openMode` 設為 **text** 時才會使用。</span><span class="sxs-lookup"><span data-stu-id="516f7-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="516f7-126">範例輸出</span><span class="sxs-lookup"><span data-stu-id="516f7-126">Sample output</span></span>
<span data-ttu-id="516f7-127">如果 options.multiple 為 false 且 options.uploadMode 為 file，輸出就會包含檔案內容作為 JSON 字串：</span><span class="sxs-lookup"><span data-stu-id="516f7-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="516f7-128">如果 options.multiple 為 true 且 options.uploadMode 為 file，輸出就會包含檔案內容作為 JSON 陣列：</span><span class="sxs-lookup"><span data-stu-id="516f7-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="516f7-129">如果 options.multiple 為 false 且 options.uploadMode 為 URL，輸出就會包含 URL 作為 JSON 字串：</span><span class="sxs-lookup"><span data-stu-id="516f7-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="516f7-130">如果 options.multiple 為 true 且 options.uploadMode 為 URL，輸出就會包含 URL 清單作為 JSON 陣列：</span><span class="sxs-lookup"><span data-stu-id="516f7-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="516f7-131">測試 CreateUiDefinition 時，某些瀏覽器 (例如 Google Chrome) 會將瀏覽器主控台的 Microsoft.Common.FileUpload 元素所產生的 URL 截斷。</span><span class="sxs-lookup"><span data-stu-id="516f7-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="516f7-132">您可能需要以滑鼠右鍵按一下個別連結來複製完整的 URL。</span><span class="sxs-lookup"><span data-stu-id="516f7-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="516f7-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="516f7-133">Next steps</span></span>
* <span data-ttu-id="516f7-134">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="516f7-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="516f7-135">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="516f7-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="516f7-136">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="516f7-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
