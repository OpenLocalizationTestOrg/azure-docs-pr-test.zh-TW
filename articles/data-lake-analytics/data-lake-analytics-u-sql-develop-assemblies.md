---
title: "針對 Azure Data Lake Analytics 作業開發 U-SQL 組件 | Microsoft Docs"
description: "了解如何開發要用於和重複用於 Data Lake Analytics 作業中的組件。 "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="8842c-103">針對 Azure Data Lake Analytics 作業開發 U-SQL 組件</span><span class="sxs-lookup"><span data-stu-id="8842c-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="8842c-104">了解如何將程式碼後置轉換成可用於和重複用於 Data Lake Analytics 作業中的組件。</span><span class="sxs-lookup"><span data-stu-id="8842c-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="8842c-105">U-SQL 可讓您輕鬆地以 .Net 語言來新增您自己的程式碼，例如 C#、VB.Net 或 F #。</span><span class="sxs-lookup"><span data-stu-id="8842c-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="8842c-106">您甚至可以部署自己的執行階段以支援其他語言。</span><span class="sxs-lookup"><span data-stu-id="8842c-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="8842c-107">使用自訂程式碼最簡單的方法是使用 Data Lake Tools for Visual Studio 的程式碼後置功能。</span><span class="sxs-lookup"><span data-stu-id="8842c-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="8842c-108">如需詳細資訊，請參閱 [教學課程：使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8842c-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="8842c-109">使用程式碼後置有幾個缺點︰</span><span class="sxs-lookup"><span data-stu-id="8842c-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="8842c-110">每次提交指令碼時都會上傳原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="8842c-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="8842c-111">程式碼後置無法與其他作業共用。</span><span class="sxs-lookup"><span data-stu-id="8842c-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="8842c-112">若要解決這些缺點，您可以將程式碼後置轉換成組件，再將組件註冊到 Data Lake Analytics 目錄。</span><span class="sxs-lookup"><span data-stu-id="8842c-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8842c-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="8842c-113">Prerequisites</span></span>
* <span data-ttu-id="8842c-114">已安裝 Visual Studio 2017、Visual Studio 2015、Visual Studio 2013 Update 4，或具有 Visual C++ 的 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="8842c-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="8842c-115">Microsoft Azure SDK for .NET 2.5 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8842c-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="8842c-116">使用 Web 平台安裝程式或 Visual Studio 安裝程式來安裝它。</span><span class="sxs-lookup"><span data-stu-id="8842c-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="8842c-117">Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8842c-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="8842c-118">請參閱[使用 Azure 入口網站開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8842c-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="8842c-119">請參閱 [開始使用 Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="8842c-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="8842c-120">連接到 Azure。</span><span class="sxs-lookup"><span data-stu-id="8842c-120">Connect to Azure.</span></span>
* <span data-ttu-id="8842c-121">上傳來源資料，請參閱[開始使用 Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8842c-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="8842c-122">開發 U-SQL 的組件</span><span class="sxs-lookup"><span data-stu-id="8842c-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="8842c-123">**建立和提交 U-SQL 工作**</span><span class="sxs-lookup"><span data-stu-id="8842c-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="8842c-124">從 [檔案] 功能表中，按一下 [新增]，再按 [專案]。</span><span class="sxs-lookup"><span data-stu-id="8842c-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="8842c-125">展開 [已安裝]、[範本]、[Azure Data Lake]、[U-SQL(ADLA)]，選取 [類別庫 (適用於 U-SQL 應用程式)] 範本，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8842c-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="8842c-126">在 Class1.cs 中撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="8842c-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="8842c-127">以下是程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="8842c-127">The following is a code sample.</span></span>

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. <span data-ttu-id="8842c-128">按一下 [建置] 功能表，然後按一下 [建置方案] 來建立 dll。</span><span class="sxs-lookup"><span data-stu-id="8842c-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="8842c-129">註冊組件</span><span class="sxs-lookup"><span data-stu-id="8842c-129">Register assemblies</span></span>

<span data-ttu-id="8842c-130">請參閱[使用 Data Lake Analytics (U-SQL) 目錄](data-lake-analytics-use-u-sql-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="8842c-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="8842c-131">使用組件</span><span class="sxs-lookup"><span data-stu-id="8842c-131">Use the assemblies</span></span>

<span data-ttu-id="8842c-132">請參閱[使用 Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="8842c-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8842c-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8842c-133">See also</span></span>
* [<span data-ttu-id="8842c-134">使用 PowerShell 開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8842c-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="8842c-135">使用 Azure 入口網站開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8842c-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8842c-136">使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 應用程式</span><span class="sxs-lookup"><span data-stu-id="8842c-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="8842c-137">使用 Data Lake Analytics (U-SQL) 目錄</span><span class="sxs-lookup"><span data-stu-id="8842c-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="8842c-138">使用 Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8842c-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)