---
title: "建立 Azure 受管理的應用程式的 UI 定義 aaaUnderstand |Microsoft 文件"
description: "描述如何將 UI 定義 toocreate Azure 受管理的應用程式"
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="9a22a-103">開始使用 CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="9a22a-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="9a22a-104">本文件介紹 hello 的 CreateUiDefinition，hello Azure 入口網站 toogenerate hello 使用者介面會用它來建立受管理的應用程式的核心概念。</span><span class="sxs-lookup"><span data-stu-id="9a22a-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="9a22a-105">CreateUiDefinition 一律會包含三個屬性︰</span><span class="sxs-lookup"><span data-stu-id="9a22a-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="9a22a-106">處理常式</span><span class="sxs-lookup"><span data-stu-id="9a22a-106">handler</span></span>
* <span data-ttu-id="9a22a-107">版本</span><span class="sxs-lookup"><span data-stu-id="9a22a-107">version</span></span>
* <span data-ttu-id="9a22a-108">參數</span><span class="sxs-lookup"><span data-stu-id="9a22a-108">parameters</span></span>

<span data-ttu-id="9a22a-109">受管理的應用程式的處理常式應一律`Microsoft.Compute.MultiVm`，且最新支援的 hello 版本`0.1.2-preview`。</span><span class="sxs-lookup"><span data-stu-id="9a22a-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="9a22a-110">hello 結構描述的 hello 參數屬性取決於 hello hello 指定的處理常式和版本組合。</span><span class="sxs-lookup"><span data-stu-id="9a22a-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="9a22a-111">對於受管理的應用程式，支援的 hello 屬性是`basics`， `steps`，和`outputs`。</span><span class="sxs-lookup"><span data-stu-id="9a22a-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="9a22a-112">hello 基本概念和步驟的屬性包含 hello_元素_-例如文字方塊和下拉式清單-toobe 中顯示 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9a22a-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="9a22a-113">屬性是使用的 toomap hello 輸出值的 hello 輸出 hello hello Azure Resource Manager 部署範本指定的項目 toohello 參數。</span><span class="sxs-lookup"><span data-stu-id="9a22a-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="9a22a-114">建議包含 `$schema`，但是為選用。</span><span class="sxs-lookup"><span data-stu-id="9a22a-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="9a22a-115">如果指定，hello 值`version`必須符合 hello 版本內 hello `$schema` URI。</span><span class="sxs-lookup"><span data-stu-id="9a22a-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="9a22a-116">基本概念</span><span class="sxs-lookup"><span data-stu-id="9a22a-116">Basics</span></span>
<span data-ttu-id="9a22a-117">hello 基本步驟永遠是 hello hello 精靈時 hello Azure 入口網站會剖析 CreateUiDefinition 產生第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="9a22a-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="9a22a-118">此外 toodisplaying hello 元素指定`basics`，hello 入口網站會插入使用者 toochoose hello 訂用帳戶、 資源群組和 hello 部署位置的項目。</span><span class="sxs-lookup"><span data-stu-id="9a22a-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="9a22a-119">通常，查詢整個部署的參數，如叢集或系統管理員認證，hello 名稱的項目應該在此步驟。</span><span class="sxs-lookup"><span data-stu-id="9a22a-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="9a22a-120">如果項目的行為會取決於 hello 使用者訂用帳戶、 資源群組或位置，然後該元素不能在基本概念。</span><span class="sxs-lookup"><span data-stu-id="9a22a-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="9a22a-121">例如， **Microsoft.Compute.SizeSelector** hello 使用者的訂用帳戶和位置 toodetermine hello 清單可用的大小而定。</span><span class="sxs-lookup"><span data-stu-id="9a22a-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="9a22a-122">因此，**Microsoft.Compute.SizeSelector** 只能用於步驟中。</span><span class="sxs-lookup"><span data-stu-id="9a22a-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="9a22a-123">一般而言，只有中的項目 hello **Microsoft.Common**命名空間可用於基本概念。</span><span class="sxs-lookup"><span data-stu-id="9a22a-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="9a22a-124">雖然某些其他命名空間中的項目 (例如**Microsoft.Compute.Credentials**)，不需依賴 hello 使用者的內容，仍允許。</span><span class="sxs-lookup"><span data-stu-id="9a22a-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="9a22a-125">步驟</span><span class="sxs-lookup"><span data-stu-id="9a22a-125">Steps</span></span>
<span data-ttu-id="9a22a-126">hello 步驟屬性可以包含零或多個額外的步驟 toodisplay 基本概念，其中每一個都包含一個或多個項目之後。</span><span class="sxs-lookup"><span data-stu-id="9a22a-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="9a22a-127">請考慮將每個角色或部署的 hello 應用程式層的步驟。</span><span class="sxs-lookup"><span data-stu-id="9a22a-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="9a22a-128">例如，在叢集中加入 hello 主要節點中，輸入步驟與 hello 背景工作角色節點的步驟。</span><span class="sxs-lookup"><span data-stu-id="9a22a-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="9a22a-129">輸出</span><span class="sxs-lookup"><span data-stu-id="9a22a-129">Outputs</span></span>
<span data-ttu-id="9a22a-130">hello Azure 入口網站會使用 hello`outputs`屬性 toomap 項目從`basics`和`steps`toohello hello Azure Resource Manager 部署範本參數。</span><span class="sxs-lookup"><span data-stu-id="9a22a-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="9a22a-131">hello 索引鍵，此字典的 hello hello 範本參數，名稱，而 hello 值從 hello 參考項目 hello 輸出物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="9a22a-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="9a22a-132">Functions</span><span class="sxs-lookup"><span data-stu-id="9a22a-132">Functions</span></span>
<span data-ttu-id="9a22a-133">類似太[樣板函式](resource-group-template-functions.md)Azure 資源管理員 中 （兩者皆語法和功能），CreateUiDefinition 提供函數來處理項目的輸入和輸出，以及條件 等功能。</span><span class="sxs-lookup"><span data-stu-id="9a22a-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a22a-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a22a-134">Next steps</span></span>
<span data-ttu-id="9a22a-135">CreateUiDefinition 本身有簡單的結構描述。</span><span class="sxs-lookup"><span data-stu-id="9a22a-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="9a22a-136">它的 hello 真實深度來自所有 hello 支援項目和函式，下列文件的 hello 驚人的詳細說明：</span><span class="sxs-lookup"><span data-stu-id="9a22a-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="9a22a-137">元素</span><span class="sxs-lookup"><span data-stu-id="9a22a-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="9a22a-138">函式</span><span class="sxs-lookup"><span data-stu-id="9a22a-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="9a22a-139">以下可取得 CreateUiDefinition 目前的 JSON 結構描述︰https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json。</span><span class="sxs-lookup"><span data-stu-id="9a22a-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="9a22a-140">更新的版本將會位於 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="9a22a-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="9a22a-141">取代 hello`0.1.2-preview`部分 hello URL 和 hello`version`值想 toouse 與 hello 版本識別項。</span><span class="sxs-lookup"><span data-stu-id="9a22a-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="9a22a-142">目前支援的 hello 版本識別項是`0.0.1-preview`， `0.1.0-preview`， `0.1.1-preview`，和`0.1.2-preview`。</span><span class="sxs-lookup"><span data-stu-id="9a22a-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
