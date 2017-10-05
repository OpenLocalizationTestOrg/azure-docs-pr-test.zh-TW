---
title: "Azure 受管理的應用程式建立 UI 定義函式 | Microsoft Docs"
description: "描述建構 Azure 受管理應用程式的 UI 定義時要使用的函式"
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
ms.openlocfilehash: 635e44a7ec6f9244f5fe75eb5ad947cdd8ae59a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="createuidefinition-elements"></a><span data-ttu-id="a0b49-103">CreateUiDefinition 元素</span><span class="sxs-lookup"><span data-stu-id="a0b49-103">CreateUiDefinition elements</span></span>
<span data-ttu-id="a0b49-104">本文描述 CreateUiDefinition 所有支援元素的結構描述和屬性。</span><span class="sxs-lookup"><span data-stu-id="a0b49-104">This article describes the schema and properties for all supported elements of a CreateUiDefinition.</span></span> <span data-ttu-id="a0b49-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用這些元素。</span><span class="sxs-lookup"><span data-stu-id="a0b49-105">You use these elements when [creating an Azure Managed Application](managed-application-publishing.md).</span></span> <span data-ttu-id="a0b49-106">大部分元素的結構描述如下所示︰</span><span class="sxs-lookup"><span data-stu-id="a0b49-106">The schema for most elements is as follows:</span></span>

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit the [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| <span data-ttu-id="a0b49-107">屬性</span><span class="sxs-lookup"><span data-stu-id="a0b49-107">Property</span></span> | <span data-ttu-id="a0b49-108">必要</span><span class="sxs-lookup"><span data-stu-id="a0b49-108">Required</span></span> | <span data-ttu-id="a0b49-109">說明</span><span class="sxs-lookup"><span data-stu-id="a0b49-109">Description</span></span> |
| -------- | -------- | ----------- |
| <span data-ttu-id="a0b49-110">名稱</span><span class="sxs-lookup"><span data-stu-id="a0b49-110">name</span></span> | <span data-ttu-id="a0b49-111">是</span><span class="sxs-lookup"><span data-stu-id="a0b49-111">Yes</span></span> | <span data-ttu-id="a0b49-112">要參考元素特定執行個體的內部識別碼。</span><span class="sxs-lookup"><span data-stu-id="a0b49-112">An internal identifier to reference a specific instance of an element.</span></span> <span data-ttu-id="a0b49-113">元素名稱的最常見用法是在 `outputs`，其中指定元素的輸出值會對應到範本的參數。</span><span class="sxs-lookup"><span data-stu-id="a0b49-113">The most common usage of the element name is in `outputs`, where the output values of the specified elements are mapped to the parameters of the template.</span></span> <span data-ttu-id="a0b49-114">您也可以使用它，將元素的輸出值繫結至另一個元素的 `defaultValue`。</span><span class="sxs-lookup"><span data-stu-id="a0b49-114">You can also use it to bind the output value of an element to the `defaultValue` of another element.</span></span> |
| <span data-ttu-id="a0b49-115">類型</span><span class="sxs-lookup"><span data-stu-id="a0b49-115">type</span></span> | <span data-ttu-id="a0b49-116">是</span><span class="sxs-lookup"><span data-stu-id="a0b49-116">Yes</span></span> | <span data-ttu-id="a0b49-117">要呈現元素的 UI 控制項。</span><span class="sxs-lookup"><span data-stu-id="a0b49-117">The UI control to render for the element.</span></span> <span data-ttu-id="a0b49-118">如需支援類型的清單，請參閱[元素](#elements)。</span><span class="sxs-lookup"><span data-stu-id="a0b49-118">For a list of supported types, see [Elements](#elements).</span></span> |
| <span data-ttu-id="a0b49-119">標籤</span><span class="sxs-lookup"><span data-stu-id="a0b49-119">label</span></span> | <span data-ttu-id="a0b49-120">是</span><span class="sxs-lookup"><span data-stu-id="a0b49-120">Yes</span></span> | <span data-ttu-id="a0b49-121">元素的顯示文字。</span><span class="sxs-lookup"><span data-stu-id="a0b49-121">The display text of the element.</span></span> <span data-ttu-id="a0b49-122">某些元素類型會包含多個標籤，因此值可能是包含多個字串的物件。</span><span class="sxs-lookup"><span data-stu-id="a0b49-122">Some element types contain multiple labels, so the value could be an object containing multiple strings.</span></span> |
| <span data-ttu-id="a0b49-123">defaultValue</span><span class="sxs-lookup"><span data-stu-id="a0b49-123">defaultValue</span></span> | <span data-ttu-id="a0b49-124">否</span><span class="sxs-lookup"><span data-stu-id="a0b49-124">No</span></span> | <span data-ttu-id="a0b49-125">元素的預設值。</span><span class="sxs-lookup"><span data-stu-id="a0b49-125">The default value of the element.</span></span> <span data-ttu-id="a0b49-126">某些元素類型支援複雜的預設值，因此值可能是物件。</span><span class="sxs-lookup"><span data-stu-id="a0b49-126">Some element types support complex default values, so the value could be an object.</span></span> |
| <span data-ttu-id="a0b49-127">工具提示</span><span class="sxs-lookup"><span data-stu-id="a0b49-127">toolTip</span></span> | <span data-ttu-id="a0b49-128">否</span><span class="sxs-lookup"><span data-stu-id="a0b49-128">No</span></span> | <span data-ttu-id="a0b49-129">要顯示在元素之工具提示的文字。</span><span class="sxs-lookup"><span data-stu-id="a0b49-129">The text to display in the tool tip of the element.</span></span> <span data-ttu-id="a0b49-130">類似於 `label`，某些元素可支援多個工具提示字串。</span><span class="sxs-lookup"><span data-stu-id="a0b49-130">Similar to `label`, some elements support multiple tool tip strings.</span></span> <span data-ttu-id="a0b49-131">您可以使用 Markdown 語法將內嵌連結進行內嵌。</span><span class="sxs-lookup"><span data-stu-id="a0b49-131">Inline links can be embedded using Markdown syntax.</span></span>
| <span data-ttu-id="a0b49-132">條件約束</span><span class="sxs-lookup"><span data-stu-id="a0b49-132">constraints</span></span> | <span data-ttu-id="a0b49-133">否</span><span class="sxs-lookup"><span data-stu-id="a0b49-133">No</span></span> | <span data-ttu-id="a0b49-134">用於自訂元素驗證行為的一個或多個屬性。</span><span class="sxs-lookup"><span data-stu-id="a0b49-134">One or more properties that are used to customize the validation behavior of the element.</span></span> <span data-ttu-id="a0b49-135">支援的條件約束屬性會依元素類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a0b49-135">The supported properties for constraints vary by element type.</span></span> <span data-ttu-id="a0b49-136">某些元素類型不支援自訂驗證行為，因此沒有任何 constraints 屬性。</span><span class="sxs-lookup"><span data-stu-id="a0b49-136">Some element types do not support customization of the validation behavior, and thus have no constraints property.</span></span> |
| <span data-ttu-id="a0b49-137">options</span><span class="sxs-lookup"><span data-stu-id="a0b49-137">options</span></span> | <span data-ttu-id="a0b49-138">否</span><span class="sxs-lookup"><span data-stu-id="a0b49-138">No</span></span> | <span data-ttu-id="a0b49-139">自訂元素行為的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="a0b49-139">Additional properties that customize the behavior of the element.</span></span> <span data-ttu-id="a0b49-140">類似於 `constraints`，支援的屬性會依元素類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a0b49-140">Similar to `constraints`, the supported properties vary by element type.</span></span> |
| <span data-ttu-id="a0b49-141">可見</span><span class="sxs-lookup"><span data-stu-id="a0b49-141">visible</span></span> | <span data-ttu-id="a0b49-142">否</span><span class="sxs-lookup"><span data-stu-id="a0b49-142">No</span></span> | <span data-ttu-id="a0b49-143">指出是否要顯示元素。</span><span class="sxs-lookup"><span data-stu-id="a0b49-143">Indicates whether the element is displayed.</span></span> <span data-ttu-id="a0b49-144">如果為 `true`，就會顯示元素和適用的子元素。</span><span class="sxs-lookup"><span data-stu-id="a0b49-144">If `true`, the element and applicable child elements are displayed.</span></span> <span data-ttu-id="a0b49-145">預設值為 `true`。</span><span class="sxs-lookup"><span data-stu-id="a0b49-145">The default value is `true`.</span></span> <span data-ttu-id="a0b49-146">使用[邏輯函式](managed-application-createuidefinition-functions.md#logical-functions)以動態方式控制這個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="a0b49-146">Use [logical functions](managed-application-createuidefinition-functions.md#logical-functions) to dynamically control this property's value.</span></span>

## <a name="elements"></a><span data-ttu-id="a0b49-147">元素</span><span class="sxs-lookup"><span data-stu-id="a0b49-147">Elements</span></span>

<span data-ttu-id="a0b49-148">每個元素的文件中包含元素行為的 UI 範例、結構描述、註解 (通常是關於驗證和支援的自訂) 以及範例輸出。</span><span class="sxs-lookup"><span data-stu-id="a0b49-148">The documentation for each element contains a UI sample, schema, remarks on the behavior of the element (usually concerning validation and supported customization), and sample output.</span></span>

- [<span data-ttu-id="a0b49-149">Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="a0b49-149">Microsoft.Common.DropDown</span></span>](managed-application-microsoft-common-dropdown.md)
- [<span data-ttu-id="a0b49-150">Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="a0b49-150">Microsoft.Common.FileUpload</span></span>](managed-application-microsoft-common-fileupload.md)
- [<span data-ttu-id="a0b49-151">Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="a0b49-151">Microsoft.Common.OptionsGroup</span></span>](managed-application-microsoft-common-optionsgroup.md)
- [<span data-ttu-id="a0b49-152">Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="a0b49-152">Microsoft.Common.PasswordBox</span></span>](managed-application-microsoft-common-passwordbox.md)
- [<span data-ttu-id="a0b49-153">Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="a0b49-153">Microsoft.Common.Section</span></span>](managed-application-microsoft-common-section.md)
- [<span data-ttu-id="a0b49-154">Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="a0b49-154">Microsoft.Common.TextBox</span></span>](managed-application-microsoft-common-textbox.md)
- [<span data-ttu-id="a0b49-155">Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="a0b49-155">Microsoft.Compute.CredentialsCombo</span></span>](managed-application-microsoft-compute-credentialscombo.md)
- [<span data-ttu-id="a0b49-156">Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="a0b49-156">Microsoft.Compute.SizeSelector</span></span>](managed-application-microsoft-compute-sizeselector.md)
- [<span data-ttu-id="a0b49-157">Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="a0b49-157">Microsoft.Compute.UserNameTextBox</span></span>](managed-application-microsoft-compute-usernametextbox.md)
- [<span data-ttu-id="a0b49-158">Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="a0b49-158">Microsoft.Network.PublicIpAddressCombo</span></span>](managed-application-microsoft-network-publicipaddresscombo.md)
- [<span data-ttu-id="a0b49-159">Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="a0b49-159">Microsoft.Network.VirtualNetworkCombo</span></span>](managed-application-microsoft-network-virtualnetworkcombo.md)
- [<span data-ttu-id="a0b49-160">Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="a0b49-160">Microsoft.Storage.MultiStorageAccountCombo</span></span>](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [<span data-ttu-id="a0b49-161">Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="a0b49-161">Microsoft.Storage.StorageAccountSelector</span></span>](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a><span data-ttu-id="a0b49-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0b49-162">Next steps</span></span>
* <span data-ttu-id="a0b49-163">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a0b49-163">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a0b49-164">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a0b49-164">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
