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
# <a name="createuidefinition-elements"></a><span data-ttu-id="bf907-103">CreateUiDefinition 元素</span><span class="sxs-lookup"><span data-stu-id="bf907-103">CreateUiDefinition elements</span></span>
<span data-ttu-id="bf907-104">本文說明 hello 結構描述和屬性的所有支援的 CreateUiDefinition 項目。</span><span class="sxs-lookup"><span data-stu-id="bf907-104">This article describes hello schema and properties for all supported elements of a CreateUiDefinition.</span></span> <span data-ttu-id="bf907-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用這些元素。</span><span class="sxs-lookup"><span data-stu-id="bf907-105">You use these elements when [creating an Azure Managed Application](managed-application-publishing.md).</span></span> <span data-ttu-id="bf907-106">hello 結構描述的大部分項目如下所示：</span><span class="sxs-lookup"><span data-stu-id="bf907-106">hello schema for most elements is as follows:</span></span>

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
| <span data-ttu-id="bf907-107">屬性</span><span class="sxs-lookup"><span data-stu-id="bf907-107">Property</span></span> | <span data-ttu-id="bf907-108">必要</span><span class="sxs-lookup"><span data-stu-id="bf907-108">Required</span></span> | <span data-ttu-id="bf907-109">說明</span><span class="sxs-lookup"><span data-stu-id="bf907-109">Description</span></span> |
| -------- | -------- | ----------- |
| <span data-ttu-id="bf907-110">名稱</span><span class="sxs-lookup"><span data-stu-id="bf907-110">name</span></span> | <span data-ttu-id="bf907-111">是</span><span class="sxs-lookup"><span data-stu-id="bf907-111">Yes</span></span> | <span data-ttu-id="bf907-112">內部識別碼 tooreference 元素的特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="bf907-112">An internal identifier tooreference a specific instance of an element.</span></span> <span data-ttu-id="bf907-113">hello hello 項目名稱的最常見的用法是在`outputs`，其中 hello hello 輸出值會指定項目是對應的 toohello hello 範本參數。</span><span class="sxs-lookup"><span data-stu-id="bf907-113">hello most common usage of hello element name is in `outputs`, where hello output values of hello specified elements are mapped toohello parameters of hello template.</span></span> <span data-ttu-id="bf907-114">您也可以使用它 toobind hello 輸出值的項目 toohello`defaultValue`另一個項目。</span><span class="sxs-lookup"><span data-stu-id="bf907-114">You can also use it toobind hello output value of an element toohello `defaultValue` of another element.</span></span> |
| <span data-ttu-id="bf907-115">類型</span><span class="sxs-lookup"><span data-stu-id="bf907-115">type</span></span> | <span data-ttu-id="bf907-116">是</span><span class="sxs-lookup"><span data-stu-id="bf907-116">Yes</span></span> | <span data-ttu-id="bf907-117">hello UI 控制 toorender hello 項目。</span><span class="sxs-lookup"><span data-stu-id="bf907-117">hello UI control toorender for hello element.</span></span> <span data-ttu-id="bf907-118">如需支援類型的清單，請參閱[元素](#elements)。</span><span class="sxs-lookup"><span data-stu-id="bf907-118">For a list of supported types, see [Elements](#elements).</span></span> |
| <span data-ttu-id="bf907-119">標籤</span><span class="sxs-lookup"><span data-stu-id="bf907-119">label</span></span> | <span data-ttu-id="bf907-120">是</span><span class="sxs-lookup"><span data-stu-id="bf907-120">Yes</span></span> | <span data-ttu-id="bf907-121">hello 顯示 hello 項目的文字。</span><span class="sxs-lookup"><span data-stu-id="bf907-121">hello display text of hello element.</span></span> <span data-ttu-id="bf907-122">某些項目型別包含多個標籤，因此 hello 值可以包含多個字串的物件。</span><span class="sxs-lookup"><span data-stu-id="bf907-122">Some element types contain multiple labels, so hello value could be an object containing multiple strings.</span></span> |
| <span data-ttu-id="bf907-123">defaultValue</span><span class="sxs-lookup"><span data-stu-id="bf907-123">defaultValue</span></span> | <span data-ttu-id="bf907-124">否</span><span class="sxs-lookup"><span data-stu-id="bf907-124">No</span></span> | <span data-ttu-id="bf907-125">hello hello 項目的預設值。</span><span class="sxs-lookup"><span data-stu-id="bf907-125">hello default value of hello element.</span></span> <span data-ttu-id="bf907-126">某些項目類型支援複雜的預設值，因此 hello 值可以是物件。</span><span class="sxs-lookup"><span data-stu-id="bf907-126">Some element types support complex default values, so hello value could be an object.</span></span> |
| <span data-ttu-id="bf907-127">工具提示</span><span class="sxs-lookup"><span data-stu-id="bf907-127">toolTip</span></span> | <span data-ttu-id="bf907-128">否</span><span class="sxs-lookup"><span data-stu-id="bf907-128">No</span></span> | <span data-ttu-id="bf907-129">hello 項目的 hello 工具提示中的 hello 文字 toodisplay。</span><span class="sxs-lookup"><span data-stu-id="bf907-129">hello text toodisplay in hello tool tip of hello element.</span></span> <span data-ttu-id="bf907-130">類似太`label`，某些項目支援多個工具提示字串。</span><span class="sxs-lookup"><span data-stu-id="bf907-130">Similar too`label`, some elements support multiple tool tip strings.</span></span> <span data-ttu-id="bf907-131">您可以使用 Markdown 語法將內嵌連結進行內嵌。</span><span class="sxs-lookup"><span data-stu-id="bf907-131">Inline links can be embedded using Markdown syntax.</span></span>
| <span data-ttu-id="bf907-132">條件約束</span><span class="sxs-lookup"><span data-stu-id="bf907-132">constraints</span></span> | <span data-ttu-id="bf907-133">否</span><span class="sxs-lookup"><span data-stu-id="bf907-133">No</span></span> | <span data-ttu-id="bf907-134">一或多個屬性都使用的 toocustomize hello 驗證行為的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="bf907-134">One or more properties that are used toocustomize hello validation behavior of hello element.</span></span> <span data-ttu-id="bf907-135">項目類型會因條件約束的 hello 支援屬性。</span><span class="sxs-lookup"><span data-stu-id="bf907-135">hello supported properties for constraints vary by element type.</span></span> <span data-ttu-id="bf907-136">某些項目類型不支援自訂 hello 驗證行為，並因此會有任何條件約束屬性。</span><span class="sxs-lookup"><span data-stu-id="bf907-136">Some element types do not support customization of hello validation behavior, and thus have no constraints property.</span></span> |
| <span data-ttu-id="bf907-137">options</span><span class="sxs-lookup"><span data-stu-id="bf907-137">options</span></span> | <span data-ttu-id="bf907-138">否</span><span class="sxs-lookup"><span data-stu-id="bf907-138">No</span></span> | <span data-ttu-id="bf907-139">自訂 hello 元素 hello 行為的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="bf907-139">Additional properties that customize hello behavior of hello element.</span></span> <span data-ttu-id="bf907-140">類似太`constraints`，支援的 hello 屬性會因項目類型。</span><span class="sxs-lookup"><span data-stu-id="bf907-140">Similar too`constraints`, hello supported properties vary by element type.</span></span> |
| <span data-ttu-id="bf907-141">可見</span><span class="sxs-lookup"><span data-stu-id="bf907-141">visible</span></span> | <span data-ttu-id="bf907-142">否</span><span class="sxs-lookup"><span data-stu-id="bf907-142">No</span></span> | <span data-ttu-id="bf907-143">指出是否要顯示 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="bf907-143">Indicates whether hello element is displayed.</span></span> <span data-ttu-id="bf907-144">如果`true`，會顯示 hello 項目和適用的子項目。</span><span class="sxs-lookup"><span data-stu-id="bf907-144">If `true`, hello element and applicable child elements are displayed.</span></span> <span data-ttu-id="bf907-145">hello 預設值是`true`。</span><span class="sxs-lookup"><span data-stu-id="bf907-145">hello default value is `true`.</span></span> <span data-ttu-id="bf907-146">使用[邏輯函數](managed-application-createuidefinition-functions.md#logical-functions)toodynamically 控制這個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="bf907-146">Use [logical functions](managed-application-createuidefinition-functions.md#logical-functions) toodynamically control this property's value.</span></span>

## <a name="elements"></a><span data-ttu-id="bf907-147">元素</span><span class="sxs-lookup"><span data-stu-id="bf907-147">Elements</span></span>

<span data-ttu-id="bf907-148">hello 文件結構描述中，每個項目包含 UI 範例，註解在 hello 行為 hello 項目 （通常是關於驗證和支援的自訂） 和輸出範例。</span><span class="sxs-lookup"><span data-stu-id="bf907-148">hello documentation for each element contains a UI sample, schema, remarks on hello behavior of hello element (usually concerning validation and supported customization), and sample output.</span></span>

- [<span data-ttu-id="bf907-149">Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="bf907-149">Microsoft.Common.DropDown</span></span>](managed-application-microsoft-common-dropdown.md)
- [<span data-ttu-id="bf907-150">Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="bf907-150">Microsoft.Common.FileUpload</span></span>](managed-application-microsoft-common-fileupload.md)
- [<span data-ttu-id="bf907-151">Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="bf907-151">Microsoft.Common.OptionsGroup</span></span>](managed-application-microsoft-common-optionsgroup.md)
- [<span data-ttu-id="bf907-152">Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="bf907-152">Microsoft.Common.PasswordBox</span></span>](managed-application-microsoft-common-passwordbox.md)
- [<span data-ttu-id="bf907-153">Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="bf907-153">Microsoft.Common.Section</span></span>](managed-application-microsoft-common-section.md)
- [<span data-ttu-id="bf907-154">Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="bf907-154">Microsoft.Common.TextBox</span></span>](managed-application-microsoft-common-textbox.md)
- [<span data-ttu-id="bf907-155">Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="bf907-155">Microsoft.Compute.CredentialsCombo</span></span>](managed-application-microsoft-compute-credentialscombo.md)
- [<span data-ttu-id="bf907-156">Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="bf907-156">Microsoft.Compute.SizeSelector</span></span>](managed-application-microsoft-compute-sizeselector.md)
- [<span data-ttu-id="bf907-157">Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="bf907-157">Microsoft.Compute.UserNameTextBox</span></span>](managed-application-microsoft-compute-usernametextbox.md)
- [<span data-ttu-id="bf907-158">Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="bf907-158">Microsoft.Network.PublicIpAddressCombo</span></span>](managed-application-microsoft-network-publicipaddresscombo.md)
- [<span data-ttu-id="bf907-159">Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="bf907-159">Microsoft.Network.VirtualNetworkCombo</span></span>](managed-application-microsoft-network-virtualnetworkcombo.md)
- [<span data-ttu-id="bf907-160">Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="bf907-160">Microsoft.Storage.MultiStorageAccountCombo</span></span>](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [<span data-ttu-id="bf907-161">Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="bf907-161">Microsoft.Storage.StorageAccountSelector</span></span>](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a><span data-ttu-id="bf907-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf907-162">Next steps</span></span>
* <span data-ttu-id="bf907-163">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bf907-163">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="bf907-164">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bf907-164">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
