---
title: "開發適用於 Azure Stack 的應用程式 | Microsoft Docs"
description: "了解在 Azure Stack 上建立原型應用程式的開發考量"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 28bca0c94e88b31012c4c53ace47d8bfe6cbe163
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-stack"></a><span data-ttu-id="23bea-103">開發 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="23bea-103">Develop for Azure Stack</span></span>
<span data-ttu-id="23bea-104">即使您沒有 Azure Stack 環境的存取權，您也可以現在就開始開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="23bea-104">You can get started developing applications today, even if you don't have access to an Azure Stack environment.</span></span> <span data-ttu-id="23bea-105">因為 Azure Stack 會傳遞在您資料中心執行的 Microsoft Azure 服務，所以您可以使用類似工具和流程針對 Azure Stack 進行開發，就如同您為 Azure 進行開發一樣。</span><span class="sxs-lookup"><span data-stu-id="23bea-105">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes to develop against Azure Stack as you would with Azure.</span></span>  <span data-ttu-id="23bea-106">只需要跟隨下列主題的準備和指導，您就可以使用 Azure 來模擬 Azure Stack 環境：</span><span class="sxs-lookup"><span data-stu-id="23bea-106">With a bit of preparation and guidance from the following topics, you can use Azure to emulate an Azure Stack environment:</span></span>

* <span data-ttu-id="23bea-107">在 Azure 中，您可以建立 Azure Resource Manager 範本，其也將會部署至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="23bea-107">In Azure, you can create Azure Resource Manager templates that are also deployable to Azure Stack.</span></span>  <span data-ttu-id="23bea-108">請參閱《[範本考量](azure-stack-develop-templates.md)》取得開發您範本的指導並確保可攜性。</span><span class="sxs-lookup"><span data-stu-id="23bea-108">See [template considerations](azure-stack-develop-templates.md) for guidance on developing your templates to ensure portability.</span></span>
* <span data-ttu-id="23bea-109">在 Azure 和 Azure Stack 之間的服務可用性和服務版本存在差異。</span><span class="sxs-lookup"><span data-stu-id="23bea-109">There is a delta in service availability and service versioning between Azure and Azure Stack.</span></span> <span data-ttu-id="23bea-110">您可以使用 [Azure Stack 原則模組](azure-stack-policy-module.md)來限制 Azure Stack 可用的 Azure 服務可用性和資源型別。</span><span class="sxs-lookup"><span data-stu-id="23bea-110">You can use the [Azure Stack policy module](azure-stack-policy-module.md) to restrict Azure service availability and resource types to what's available in Azure Stack.</span></span> <span data-ttu-id="23bea-111">限制可用服務將可協助您的應用程式依賴 Azure Stack 可用的服務。</span><span class="sxs-lookup"><span data-stu-id="23bea-111">Constraining available services will help your application rely on services available to Azure Stack.</span></span>
* <span data-ttu-id="23bea-112">[Azure Stack 快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates)是如何開發您範本，讓其能夠部署至 Azure 和 Azure Stack 的常見情節範例。</span><span class="sxs-lookup"><span data-stu-id="23bea-112">The [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples of how to develop your templates so they can be deployed to both Azure and Azure Stack.</span></span>


