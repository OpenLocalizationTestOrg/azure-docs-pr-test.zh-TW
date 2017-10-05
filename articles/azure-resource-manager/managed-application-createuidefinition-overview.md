---
title: "了解如何建立 Azure 受管理應用程式的 UI 定義 | Microsoft Docs"
description: "描述如何建立 Azure 受管理應用程式的 UI 定義"
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
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="8879f-103">開始使用 CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="8879f-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="8879f-104">本文介紹 CreateUiDefinition 的核心概念，Azure 入口網站運用這個概念來產生使用者介面，從而建立受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8879f-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="8879f-105">CreateUiDefinition 一律會包含三個屬性︰</span><span class="sxs-lookup"><span data-stu-id="8879f-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="8879f-106">處理常式</span><span class="sxs-lookup"><span data-stu-id="8879f-106">handler</span></span>
* <span data-ttu-id="8879f-107">版本</span><span class="sxs-lookup"><span data-stu-id="8879f-107">version</span></span>
* <span data-ttu-id="8879f-108">參數</span><span class="sxs-lookup"><span data-stu-id="8879f-108">parameters</span></span>

<span data-ttu-id="8879f-109">針對受管理的應用程式，處理常式應該一律為 `Microsoft.Compute.MultiVm`，而最新的支援版本是 `0.1.2-preview`。</span><span class="sxs-lookup"><span data-stu-id="8879f-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="8879f-110">parameters 屬性的結構描述取決於指定的處理常式和版本之組合。</span><span class="sxs-lookup"><span data-stu-id="8879f-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="8879f-111">針對受管理的應用程式，支援的屬性為 `basics`、`steps` 和 `outputs`。</span><span class="sxs-lookup"><span data-stu-id="8879f-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="8879f-112">basics 和 steps屬性包含要在 Azure 入口網站中顯示的_元素_ - 如同文字方塊和下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="8879f-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="8879f-113">outputs 屬性可用來將指定元素的輸出值對應至 Azure Resource Manager 部署範本的參數。</span><span class="sxs-lookup"><span data-stu-id="8879f-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="8879f-114">建議包含 `$schema`，但是為選用。</span><span class="sxs-lookup"><span data-stu-id="8879f-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="8879f-115">如果指定，`version` 的值必須符合 `$schema` URI 內的版本。</span><span class="sxs-lookup"><span data-stu-id="8879f-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="8879f-116">基本概念</span><span class="sxs-lookup"><span data-stu-id="8879f-116">Basics</span></span>
<span data-ttu-id="8879f-117">當 Azure 入口網站剖析 CreateUiDefinition 時，所產生之精靈的第一個步驟一律為 Basics 步驟。</span><span class="sxs-lookup"><span data-stu-id="8879f-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="8879f-118">除了顯示 `basics` 中指定的元素之外，入口網站會插入元素，以供使用者選擇部署的訂用帳戶、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="8879f-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="8879f-119">一般而言，查詢整個部署參數的元素 (例如叢集的名稱或管理員認證) 都應在此步驟中。</span><span class="sxs-lookup"><span data-stu-id="8879f-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="8879f-120">如果元素的行為取決於使用者的訂用帳戶、資源群組或位置，就不能在 basics 中使用該元素。</span><span class="sxs-lookup"><span data-stu-id="8879f-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="8879f-121">例如，**Microsoft.Compute.SizeSelector** 取決於使用者的訂用帳戶和位置，來判斷可用大小的清單。</span><span class="sxs-lookup"><span data-stu-id="8879f-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="8879f-122">因此，**Microsoft.Compute.SizeSelector** 只能用於步驟中。</span><span class="sxs-lookup"><span data-stu-id="8879f-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="8879f-123">一般而言，basics 中只能使用 **Microsoft.Common** 命名空間中的元素。</span><span class="sxs-lookup"><span data-stu-id="8879f-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="8879f-124">儘管其他命名空間中的某些元素 (例如 **Microsoft.Compute.Credentials**) 並非取決於使用者的內容，但仍可允許使用。</span><span class="sxs-lookup"><span data-stu-id="8879f-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="8879f-125">步驟</span><span class="sxs-lookup"><span data-stu-id="8879f-125">Steps</span></span>
<span data-ttu-id="8879f-126">steps 屬性可以包含零個或多個要在 basics 之後顯示的額外步驟，其中都各包含一個或多個元素。</span><span class="sxs-lookup"><span data-stu-id="8879f-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="8879f-127">請考慮針對每個角色或要進行部署的應用程式層新增步驟。</span><span class="sxs-lookup"><span data-stu-id="8879f-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="8879f-128">例如，針對主要節點的輸入新增一個步驟，以及針對叢集中的背景工作節點新增一個步驟。</span><span class="sxs-lookup"><span data-stu-id="8879f-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="8879f-129">輸出</span><span class="sxs-lookup"><span data-stu-id="8879f-129">Outputs</span></span>
<span data-ttu-id="8879f-130">Azure 入口網站會使用 `outputs` 屬性，將 `basics` 和 `steps` 的屬性對應至 Azure Resource Manager 部署範本的參數。</span><span class="sxs-lookup"><span data-stu-id="8879f-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="8879f-131">這個字典的金鑰是範本參數的名稱，而值則是所參照元素的輸出物件之屬性。</span><span class="sxs-lookup"><span data-stu-id="8879f-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="8879f-132">Functions</span><span class="sxs-lookup"><span data-stu-id="8879f-132">Functions</span></span>
<span data-ttu-id="8879f-133">類似於 Azure Resource Manager 中的[範本函式](resource-group-template-functions.md) (包括語法和功能)，CreateUiDefinition 提供的函式可用於元素的輸入與輸出，以及條件等功能。</span><span class="sxs-lookup"><span data-stu-id="8879f-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8879f-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8879f-134">Next steps</span></span>
<span data-ttu-id="8879f-135">CreateUiDefinition 本身有簡單的結構描述。</span><span class="sxs-lookup"><span data-stu-id="8879f-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="8879f-136">它實際的深度來自所有支援的元素和函式，下列文件將會加以詳細說明︰</span><span class="sxs-lookup"><span data-stu-id="8879f-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="8879f-137">元素</span><span class="sxs-lookup"><span data-stu-id="8879f-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="8879f-138">函式</span><span class="sxs-lookup"><span data-stu-id="8879f-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="8879f-139">以下可取得 CreateUiDefinition 目前的 JSON 結構描述︰https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json。</span><span class="sxs-lookup"><span data-stu-id="8879f-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="8879f-140">可在相同位置取得更新的版本。</span><span class="sxs-lookup"><span data-stu-id="8879f-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="8879f-141">將 URL 的 `0.1.2-preview` 部分和 `version` 值取代為您想要使用的版本識別碼。</span><span class="sxs-lookup"><span data-stu-id="8879f-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="8879f-142">目前支援的版本識別碼為 `0.0.1-preview`、`0.1.0-preview`、`0.1.1-preview` 和 `0.1.2-preview`。</span><span class="sxs-lookup"><span data-stu-id="8879f-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>