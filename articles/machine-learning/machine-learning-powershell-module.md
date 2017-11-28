---
title: "適用於 Machine Learning 的 PowerShell 模組 | Microsoft Docs"
description: "適用於 Azure Machine Learning 的 PowerShell 模組提供公開預覽模式。 您可以使用 PowerShell 來建立及管理工作區、實驗、Web 服務等。"
keywords: "實驗、線性迴歸、機器學習服務演算法、機器學習服務教學課程、預測性模型技術、資料科學實驗"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 6ea4b887428891f41ed1a4bad26148763cefabe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a><span data-ttu-id="f5201-105">適用於 Microsoft Azure Machine Learning 的 PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="f5201-105">PowerShell module for Microsoft Azure Machine Learning</span></span>
<span data-ttu-id="f5201-106">適用於 Azure Machine Learning 的 PowerShell 模組是一款功能強大的工具，它能讓您使用 Windows PowerShell 來管理工作區、實驗、資料集、傳統的 Web 服務等。</span><span class="sxs-lookup"><span data-stu-id="f5201-106">The PowerShell module for Azure Machine Learning is a powerful tool that allows you to use Windows PowerShell to manage workspaces, experiments, datasets, Classic web services, and more.</span></span>

<span data-ttu-id="f5201-107">若要檢視文件及下載模組和完整的原始程式碼，請前往 [https://aka.ms/amlps](https://aka.ms/amlps)。</span><span class="sxs-lookup"><span data-stu-id="f5201-107">You can view the documentation and download the module, along with the full source code, at [https://aka.ms/amlps](https://aka.ms/amlps).</span></span> 

> [!NOTE]
> <span data-ttu-id="f5201-108">Azure Machine Learning 的 PowerShell 模組目前為預覽模式。</span><span class="sxs-lookup"><span data-stu-id="f5201-108">The Azure Machine Learning PowerShell module is currently in preview mode.</span></span> <span data-ttu-id="f5201-109">在此預覽期間內，我們將會持續改善及擴充模組。</span><span class="sxs-lookup"><span data-stu-id="f5201-109">The module will continue to be improved and expanded during this preview period.</span></span> <span data-ttu-id="f5201-110">如需相關新聞和資訊，敬請關注 [Cortana Intelligence 和 Machine Learning 部落格](https://blogs.technet.microsoft.com/machinelearning/)。</span><span class="sxs-lookup"><span data-stu-id="f5201-110">Keep an eye on the [Cortana Intelligence and Machine Learning Blog](https://blogs.technet.microsoft.com/machinelearning/) for news and information.</span></span>

## <a name="what-is-the-machine-learning-powershell-module"></a><span data-ttu-id="f5201-111">什麼是 Machine Learning PowerShell 模組？</span><span class="sxs-lookup"><span data-stu-id="f5201-111">What is the Machine Learning PowerShell module?</span></span>
<span data-ttu-id="f5201-112">Machine Learning PowerShell 模組是以 .NET 為基礎的 DLL 模組，它能讓您從 Windows PowerShell 全權管理 Azure Machine Learning 工作區、實驗、資料集、傳統的 Web 服務及傳統的 Web 服務端點。</span><span class="sxs-lookup"><span data-stu-id="f5201-112">The Machine Learning PowerShell module is a .NET-based DLL module that allows you to fully manage Azure Machine Learning workspaces, experiments, datasets, Classic web services, and Classic web service endpoints from Windows PowerShell.</span></span> 

<span data-ttu-id="f5201-113">您可以隨著此模組一同下載完整的原始程式碼，其中包括完全分隔的 [C# API 層](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs)。</span><span class="sxs-lookup"><span data-stu-id="f5201-113">Along with the module, you can download the full source code which includes a cleanly separated [C# API layer](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs).</span></span> <span data-ttu-id="f5201-114">您可以從自己的 .NET 專案參考此 DLL，並透過 .NET 程式碼管理 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="f5201-114">You can reference this DLL from your own .NET project and manage Azure Machine Learning through .NET code.</span></span> <span data-ttu-id="f5201-115">此外，對於 DLL 仰賴的基礎 REST API，您可以從常用的用戶端中直接使用。</span><span class="sxs-lookup"><span data-stu-id="f5201-115">In addition, the DLL depends on underlying REST APIs that you can use directly from your favorite client.</span></span>

## <a name="what-can-i-do-with-the-powershell-module"></a><span data-ttu-id="f5201-116">PowerShell 模組有什麼功能？</span><span class="sxs-lookup"><span data-stu-id="f5201-116">What can I do with the PowerShell module?</span></span>
<span data-ttu-id="f5201-117">以下是一些您可以使用此 PowerShell 模組來執行的工作。</span><span class="sxs-lookup"><span data-stu-id="f5201-117">Here are some of the tasks you can perform with this PowerShell module.</span></span> <span data-ttu-id="f5201-118">如需以下功能和其他更多功能的相關資訊，請參閱 [完整文件](https://aka.ms/amlps) 。</span><span class="sxs-lookup"><span data-stu-id="f5201-118">Check out the [full documentation](https://aka.ms/amlps) for these and many more functions.</span></span>

* <span data-ttu-id="f5201-119">使用管理憑證佈建新工作區 ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))</span><span class="sxs-lookup"><span data-stu-id="f5201-119">Provision a new workspace using a management certificate ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))</span></span>
* <span data-ttu-id="f5201-120">匯出及匯入代表實驗圖形的 JSON 檔案 ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) 和 [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))</span><span class="sxs-lookup"><span data-stu-id="f5201-120">Export and import a JSON file representing an experiment graph ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) and [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))</span></span>
* <span data-ttu-id="f5201-121">執行實驗 ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))</span><span class="sxs-lookup"><span data-stu-id="f5201-121">Run an experiment ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))</span></span>
* <span data-ttu-id="f5201-122">利用預測性實驗建立 Web 服務 ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))</span><span class="sxs-lookup"><span data-stu-id="f5201-122">Create a web service out of a predictive experiment ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))</span></span>
* <span data-ttu-id="f5201-123">在發佈的 Web 服務上建立端點 ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))</span><span class="sxs-lookup"><span data-stu-id="f5201-123">Create an endpoint on a published web service ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))</span></span>
* <span data-ttu-id="f5201-124">叫用 RRS 和/或 BES Web 服務端點 ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) 和 [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))</span><span class="sxs-lookup"><span data-stu-id="f5201-124">Invoke an RRS and/or BES web service endpoint ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) and [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))</span></span>

<span data-ttu-id="f5201-125">以下是使用 PowerShell 執行現有實驗的簡單範例︰</span><span class="sxs-lookup"><span data-stu-id="f5201-125">Here's a quick example of using PowerShell to run an existing experiment:</span></span>

        #Find the first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run the Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

<span data-ttu-id="f5201-126">如需更深入的使用案例，請參閱以下有關使用 PowerShell 模組將普遍要求之工作自動化的文章：[使用 PowerShell，從一個實驗中建立許多機器學習服務模型和 Web 服務端點](machine-learning-create-models-and-endpoints-with-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="f5201-126">For a more in-depth use case, see this article on using the PowerShell module to automate a commonly-requested task: [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).</span></span>

## <a name="how-do-i-get-started"></a><span data-ttu-id="f5201-127">如何開始使用？</span><span class="sxs-lookup"><span data-stu-id="f5201-127">How do I get started?</span></span>
<span data-ttu-id="f5201-128">若要開始使用 Machine Learning PowerShell，請從 GitHub 下載[發行套件](https://github.com/hning86/azuremlps/releases)並遵循[安裝指示](https://github.com/hning86/azuremlps/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="f5201-128">To get started with Machine Learning PowerShell, download the [release package](https://github.com/hning86/azuremlps/releases) from GitHub and follow the [instructions for installation](https://github.com/hning86/azuremlps/blob/master/README.md).</span></span> <span data-ttu-id="f5201-129">指示說明如何解除封鎖已下載/解壓縮的 DLL，然後再匯入 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="f5201-129">The instructions explain how to unblock the downloaded/unzipped DLL and then import it into your PowerShell environment.</span></span> <span data-ttu-id="f5201-130">大部分的 Cmdlet 都會要求您提供工作區識別碼、工作區授權權杖，以及工作區所在的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="f5201-130">Most of the cmdlets require that you supply the workspace ID, the workspace authorization token, and the Azure region that the workspace is in.</span></span> <span data-ttu-id="f5201-131">提供值最簡單的方式是透過預設的 config.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="f5201-131">The simplest way to provide the values is through a default config.json file.</span></span> <span data-ttu-id="f5201-132">指示中也會說明如何設定這個檔案。</span><span class="sxs-lookup"><span data-stu-id="f5201-132">The instructions also explain how to configure this file.</span></span> 

<span data-ttu-id="f5201-133">如果您想要，也可以使用 Visual Studio 複製 git 樹狀結構，然後在本機修改它。</span><span class="sxs-lookup"><span data-stu-id="f5201-133">And if you want, you can clone the git tree, modify the code, and compile it locally using Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5201-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5201-134">Next steps</span></span>
<span data-ttu-id="f5201-135">您可以在 [https://aka.ms/amlps](https://aka.ms/amlps) 找到完整的 PowerShell 模組文件。</span><span class="sxs-lookup"><span data-stu-id="f5201-135">You can find the full documentation for the PowerShell module at [https://aka.ms/amlps](https://aka.ms/amlps).</span></span> 

<span data-ttu-id="f5201-136">如需如何在真實案例中使用此模組的延伸範例，請看深入使用案例[使用 PowerShell，從一個實驗中建立許多 Machine Learning 模型和 Web 服務端點](machine-learning-create-models-and-endpoints-with-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="f5201-136">For an extended example of how to use the module in a real-world scenario, check out the in-depth use case, [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).</span></span>
