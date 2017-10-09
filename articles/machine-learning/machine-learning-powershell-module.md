---
title: "機器學習 aaaPowerShell 模組 |Microsoft 文件"
description: "在公開預覽模式中使用 Azure Machine Learning 的 hello PowerShell 模組。 使用 PowerShell toocreate 和管理工作區、 實驗、 web 服務等等。"
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
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>適用於 Microsoft Azure Machine Learning 的 PowerShell 模組
Azure Machine Learning 的 hello PowerShell 模組是功能強大的工具，可讓您 toouse Windows PowerShell toomanage 工作區、 實驗、 資料集、 傳統 web 服務等等。

您可以檢視 hello 文件，並從下列網址下載 hello 模組，以及 hello 完整的原始程式碼， [https://aka.ms/amlps](https://aka.ms/amlps)。 

> [!NOTE]
> hello Azure 機器學習 PowerShell 模組目前為預覽模式。 hello 模組將會繼續 toobe 增強並擴充此預覽期間。 請注意 hello [Cortana 智慧和機器學習部落格](https://blogs.technet.microsoft.com/machinelearning/)新聞及資訊。

## <a name="what-is-hello-machine-learning-powershell-module"></a>什麼是 hello 機器學習 PowerShell 模組？
hello 機器學習 PowerShell 模組。NET 基礎 DLL 模組，可讓您 toofully 管理 Azure Machine Learning 工作區中，實驗、 資料集、 傳統 web 服務和傳統 web 服務端點從 Windows PowerShell。 

Hello 模組，以及您可以下載 hello 完整的原始程式碼包括完全分隔[C# API 層](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs)。 您可以從自己的 .NET 專案參考此 DLL，並透過 .NET 程式碼管理 Azure Machine Learning。 此外，hello DLL 取決於基礎的 REST Api 可讓您直接從您喜愛的用戶端。

## <a name="what-can-i-do-with-hello-powershell-module"></a>我可以用 hello PowerShell 模組來做什麼？
以下是一些您可以使用此 PowerShell 模組執行 hello 工作。 簽出 hello[完整文件](https://aka.ms/amlps)針對這些與許多的多個函式。

* 使用管理憑證佈建新工作區 ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* 匯出及匯入代表實驗圖形的 JSON 檔案 ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) 和 [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* 執行實驗 ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* 利用預測性實驗建立 Web 服務 ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* 在發佈的 Web 服務上建立端點 ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* 叫用 RRS 和/或 BES Web 服務端點 ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) 和 [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

以下是使用 PowerShell toorun 現有實驗的簡單的範例：

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

更深入的使用案例，請參閱這篇文章，需使用 hello PowerShell 模組 tooautomate 常要求的工作：[許多機器學習模型和 web 服務端點從建立一個使用 PowerShell 的實驗](machine-learning-create-models-and-endpoints-with-powershell.md)。

## <a name="how-do-i-get-started"></a>如何開始使用？
tooget 開始使用機器學習 PowerShell，請下載 hello[發行套件](https://github.com/hning86/azuremlps/releases)從 GitHub 和後續 hello[安裝指示](https://github.com/hning86/azuremlps/blob/master/README.md)。 hello 指示說明如何 toounblock hello 下載/解壓縮 DLL，並再將它匯入到您的 PowerShell 環境。 大部分的 hello cmdlet 需要您提供 hello 工作區識別碼 hello 工作區中的授權權杖，並 hello hello 工作區的 Azure 區域內。 hello 最簡單方式 tooprovide hello 值都是透過預設 config.json 檔案。 hello 指示也說明如何 tooconfigure 這個檔案。 

如果您想，您可以複製 hello git 樹狀結構、 修改 hello 程式碼，並使用 Visual Studio 在本機進行編譯。

## <a name="next-steps"></a>後續步驟
您可以找到 hello hello 位於 PowerShell 模組的完整文件[https://aka.ms/amlps](https://aka.ms/amlps)。 

如需如何 toouse hello 真實世界的實例中模組的延伸範例中，簽出 hello 深入了解使用案例，[許多機器學習模型和 web 服務端點從建立一個使用 PowerShell 的實驗](machine-learning-create-models-and-endpoints-with-powershell.md)。
