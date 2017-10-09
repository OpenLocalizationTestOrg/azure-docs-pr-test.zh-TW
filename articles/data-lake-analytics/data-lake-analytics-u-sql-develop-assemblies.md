---
title: "Azure Data Lake Analytics 工作 aaaDevelop U-SQL 組件 |Microsoft 文件"
description: "了解 toodevelop 組件 toobe 的使用方式，並在 Data Lake Analytics 中，重複使用的工作。 "
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
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="9f586-103">針對 Azure Data Lake Analytics 作業開發 U-SQL 組件</span><span class="sxs-lookup"><span data-stu-id="9f586-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="9f586-104">了解如何 tooturn 程式碼後置到組件 toobe 用和在 Data Lake Analytics 工作中重複使用。</span><span class="sxs-lookup"><span data-stu-id="9f586-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="9f586-105">U SQL 可讓您自己的自訂程式碼的簡單 tooadd 在.Net 語言中，例如 C#、 VB.Net 或 F #。</span><span class="sxs-lookup"><span data-stu-id="9f586-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="9f586-106">您甚至可以部署您自己的執行階段 toosupport 其他語言。</span><span class="sxs-lookup"><span data-stu-id="9f586-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="9f586-107">hello 最簡單方式 toouse 自訂程式碼是 toouse hello Data Lake Tools for Visual Studio 程式碼後置功能。</span><span class="sxs-lookup"><span data-stu-id="9f586-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="9f586-108">如需詳細資訊，請參閱 [教學課程：使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9f586-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="9f586-109">使用程式碼後置有幾個缺點︰</span><span class="sxs-lookup"><span data-stu-id="9f586-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="9f586-110">每個指令碼送出 hello 原始程式碼取得上傳。</span><span class="sxs-lookup"><span data-stu-id="9f586-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="9f586-111">程式碼後置無法與其他作業共用。</span><span class="sxs-lookup"><span data-stu-id="9f586-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="9f586-112">tooaddress 這些缺點，您可以開啟程式碼後置為組件，並註冊 hello 組件 toohello Data Lake Analytics 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="9f586-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f586-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f586-113">Prerequisites</span></span>
* <span data-ttu-id="9f586-114">已安裝 Visual Studio 2017、Visual Studio 2015、Visual Studio 2013 Update 4，或具有 Visual C++ 的 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="9f586-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="9f586-115">Microsoft Azure SDK for .NET 2.5 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9f586-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="9f586-116">使用 hello Web platform installer 或 Visual Studio 安裝程式進行安裝</span><span class="sxs-lookup"><span data-stu-id="9f586-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="9f586-117">Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f586-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="9f586-118">請參閱[使用 Azure 入口網站開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9f586-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="9f586-119">請執行 hello[開始使用 Azure 資料湖分析 U-SQL Studio](data-lake-analytics-u-sql-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="9f586-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="9f586-120">連接 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="9f586-120">Connect tooAzure.</span></span>
* <span data-ttu-id="9f586-121">上傳 hello 來源資料，請參閱[開始使用 Azure 資料湖分析 U-SQL Studio](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9f586-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="9f586-122">開發 U-SQL 的組件</span><span class="sxs-lookup"><span data-stu-id="9f586-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="9f586-123">**toocreate 並提交 U SQL 作業**</span><span class="sxs-lookup"><span data-stu-id="9f586-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="9f586-124">從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="9f586-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="9f586-125">展開**已安裝**，**範本**， **Azure 資料湖**， **U-SQL(ADLA)**，選取 hello**類別庫 (如 U-SQL應用程式）**範本，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="9f586-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="9f586-126">在 Class1.cs 中撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f586-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="9f586-127">hello 如下的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="9f586-127">hello following is a code sample.</span></span>

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
4. <span data-ttu-id="9f586-128">按一下 hello**建置**功能表，然後再按一下**建置方案**toocreate hello dll。</span><span class="sxs-lookup"><span data-stu-id="9f586-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="9f586-129">註冊組件</span><span class="sxs-lookup"><span data-stu-id="9f586-129">Register assemblies</span></span>

<span data-ttu-id="9f586-130">請參閱[使用 Data Lake Analytics (U-SQL) 目錄](data-lake-analytics-use-u-sql-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="9f586-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="9f586-131">使用 hello 組件</span><span class="sxs-lookup"><span data-stu-id="9f586-131">Use hello assemblies</span></span>

<span data-ttu-id="9f586-132">請參閱[使用 hello Azure 資料湖 Tools for Visual Studio 程式碼](data-lake-analytics-data-lake-tools-for-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="9f586-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9f586-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9f586-133">See also</span></span>
* [<span data-ttu-id="9f586-134">使用 PowerShell 開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9f586-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="9f586-135">開始使用 Data Lake Analytics 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f586-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="9f586-136">使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 應用程式</span><span class="sxs-lookup"><span data-stu-id="9f586-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="9f586-137">使用 Data Lake Analytics (U-SQL) 目錄</span><span class="sxs-lookup"><span data-stu-id="9f586-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="9f586-138">使用 hello Azure 資料湖 Tools for Visual Studio 程式碼</span><span class="sxs-lookup"><span data-stu-id="9f586-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
