---
title: "Azure Machine Learning 新增功能 | Microsoft Docs"
description: "Azure Machine Learning 中可用的新功能。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: ddc716ed-2615-4806-bf27-6c9a5662a7f2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 551b977b90612ddbfa1514a9c2358ebf8179c385
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-machine-learning"></a><span data-ttu-id="268d7-103">Azure Machine Learning 新增功能</span><span class="sxs-lookup"><span data-stu-id="268d7-103">What's New in Azure Machine Learning</span></span>

### <a name="the-march-2017-release-of-microsoft-azure-machine-learning-updates-provides-the-following-feature"></a><span data-ttu-id="268d7-104">2017 年 3 月發行的 Microsoft Azure Machine Learning 更新提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="268d7-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span></span>



* <span data-ttu-id="268d7-105">Azure Machine Learning BES 作業專用的容量</span><span class="sxs-lookup"><span data-stu-id="268d7-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span></span>

    <span data-ttu-id="268d7-106">Machine Learning 批次集區處理會使用 [Azure Batch](../batch/batch-technical-overview.md) 服務，提供客戶管理的 Azure Machine Learning 批次執行服務級別。</span><span class="sxs-lookup"><span data-stu-id="268d7-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="268d7-107">批次集區處理可讓您建立 Azure Batch 集區，以便提交批次作業，並讓它們以預期的方式執行。</span><span class="sxs-lookup"><span data-stu-id="268d7-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span></span>

    <span data-ttu-id="268d7-108">如需詳細資訊，請參閱[適用於 Machine Learning 作業的 Azure Batch 服務](machine-learning-dedicated-capacity-for-bes-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="268d7-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span></span>


### <a name="the-august-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="268d7-109">2016 年 8 月發行的 Microsoft Azure Machine Learning 更新提供下列功能︰</span><span class="sxs-lookup"><span data-stu-id="268d7-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="268d7-110">新的 [Microsoft Azure Machine Learning Web 服務](https://services.azureml.net/)入口網站可集中管理 Web 服務的所有層面，現在可以在此入口網站中管理傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="268d7-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>    
  * <span data-ttu-id="268d7-111">它提供 Web 服務 [使用量統計資料](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="268d7-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
  * <span data-ttu-id="268d7-112">使用範例資料來簡化測試 Azure Machine Learning 遠端要求呼叫。</span><span class="sxs-lookup"><span data-stu-id="268d7-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
  * <span data-ttu-id="268d7-113">提供新的批次執行服務測試頁面，有範例資料和作業提交歷程記錄可用。</span><span class="sxs-lookup"><span data-stu-id="268d7-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>
  * <span data-ttu-id="268d7-114">提供更輕鬆的端點管理。</span><span class="sxs-lookup"><span data-stu-id="268d7-114">Provides easier endpoint management.</span></span>

### <a name="the-july-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="268d7-115">2016 年 7 月發行的 Microsoft Azure Machine Learning 更新提供下列功能︰</span><span class="sxs-lookup"><span data-stu-id="268d7-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="268d7-116">現在 Web 服務是透過 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 介面管理為 Azure 資源，有下列增強功能︰</span><span class="sxs-lookup"><span data-stu-id="268d7-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span></span>
  * <span data-ttu-id="268d7-117">有新的 [REST API](https://msdn.microsoft.com/library/azure/Dn950030.aspx) 可部署和管理以 Resource Manager 為基礎的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="268d7-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span></span>
  * <span data-ttu-id="268d7-118">新的 [Microsoft Azure Machine Learning Web 服務](https://services.azureml.net/)入口網站可集中管理 Web 服務的所有層面。</span><span class="sxs-lookup"><span data-stu-id="268d7-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>
* <span data-ttu-id="268d7-119">使用以 Resource Manager 為基礎的 API，運用 Web 服務的 Resource Manager 資源提供者 ，加入以新的訂用帳戶為基礎、多區域 Web 服務的部署模型。</span><span class="sxs-lookup"><span data-stu-id="268d7-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span></span>
* <span data-ttu-id="268d7-120">使用新的 Resource Manager RP 進行計費，引入新的 [定價方案](https://azure.microsoft.com/pricing/details/machine-learning/) 和方案管理功能。</span><span class="sxs-lookup"><span data-stu-id="268d7-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span></span>
  * <span data-ttu-id="268d7-121">您現在可以[將您的 Web 服務部署到多個區域](machine-learning-how-to-deploy-to-multiple-regions.md)而不需要在每個區域中建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="268d7-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span></span>
* <span data-ttu-id="268d7-122">提供 Web 服務 [使用量統計資料](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="268d7-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
* <span data-ttu-id="268d7-123">使用範例資料來簡化測試 Azure Machine Learning 遠端要求呼叫。</span><span class="sxs-lookup"><span data-stu-id="268d7-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
* <span data-ttu-id="268d7-124">提供新的批次執行服務測試頁面，有範例資料和作業提交歷程記錄可用。</span><span class="sxs-lookup"><span data-stu-id="268d7-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>

<span data-ttu-id="268d7-125">此外，Machine Learning Studio 已更新，可讓您部署到新式 Web 服務模型，或繼續部署到傳統 Web 服務模型。</span><span class="sxs-lookup"><span data-stu-id="268d7-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span></span> 

