---
title: "開發 U-SQL 使用者定義的運算子 (UDO) | Microsoft Docs"
description: "了解如何開發使用者定義的運算子，以用於和重複用於 Data Lake Analytics 作業中。 "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: fdee02fb60b633c26704fc1774dfc3a7825b5e0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="a9a7c-103">開發 U-SQL 使用者定義的運算子 (UDO)</span><span class="sxs-lookup"><span data-stu-id="a9a7c-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="a9a7c-104">了解如何開發使用者定義的運算子來處理 U-SQL 作業中的資料。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-104">Learn how to develop user-defined operators to process data in a U-SQL job.</span></span>

<span data-ttu-id="a9a7c-105">如需有關開發 U-SQL 一般用途組件的指示，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="a9a7c-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="a9a7c-106">在 U-SQL 中定義和使用使用者定義的運算子</span><span class="sxs-lookup"><span data-stu-id="a9a7c-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="a9a7c-107">**建立和提交 U-SQL 工作**</span><span class="sxs-lookup"><span data-stu-id="a9a7c-107">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="a9a7c-108">從 Visual Studio 中，選取 [檔案] > [新增] > [專案] > [U-SQL 專案]。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-108">From the Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="a9a7c-109">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-109">Click **OK**.</span></span> <span data-ttu-id="a9a7c-110">Visual Studio 會建立具有 Script.usql 檔案的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="a9a7c-111">在 [方案總管] 中展開 Script.usql，然後按兩下 **Script.usql.cs**。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="a9a7c-112">將下列程式碼貼到檔案中：</span><span class="sxs-lookup"><span data-stu-id="a9a7c-112">Paste the following code into the file:</span></span>

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. <span data-ttu-id="a9a7c-113">開啟 **Script.usql**，並貼上下列 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="a9a7c-113">Open **Script.usql**, and paste the following U-SQL script:</span></span>

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="a9a7c-114">指定 Data Lake Analytics 帳戶、資料庫和結構描述。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-114">Specify the Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="a9a7c-115">從 [方案總管] 中，在 [Script.usql] 上按一下滑鼠右鍵，然後按一下 [建置指令碼]。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="a9a7c-116">從 [方案總管] 中，在 [Script.usql] 上按一下滑鼠右鍵，然後按一下 [提交指令碼]。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="a9a7c-117">如果您尚未連線至 Azure 訂用帳戶，系統會提示您輸入 Azure 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-117">If you haven't connected to your Azure subscription, you will be prompted to enter your Azure account credentials.</span></span>
11. <span data-ttu-id="a9a7c-118">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-118">Click **Submit**.</span></span> <span data-ttu-id="a9a7c-119">提交作業完成時，提交結果和工作連結都可以在 [結果] 視窗中取得。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-119">Submission results and job link are available in the Results window when the submission is completed.</span></span>
12. <span data-ttu-id="a9a7c-120">按一下 [重新整理] 按鈕，以查看最新的作業狀態並重新整理畫面。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-120">Click the **Refresh** button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="a9a7c-121">**查看輸出**</span><span class="sxs-lookup"><span data-stu-id="a9a7c-121">**To see the output**</span></span>

1. <span data-ttu-id="a9a7c-122">從 [伺服器總管] 依序展開 [Azure]、[Data Lake Analytics]、您的 Data Lake Analytics 帳戶、[儲存體帳戶]，以滑鼠右鍵按一下 [預設儲存體]，然後按一下 [總管]。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="a9a7c-123">展開範例、展開輸出，然後按兩下 [Drivers.csv] 。</span><span class="sxs-lookup"><span data-stu-id="a9a7c-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="a9a7c-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a9a7c-124">See also</span></span>
* [<span data-ttu-id="a9a7c-125">使用 PowerShell 開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a9a7c-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="a9a7c-126">使用 Azure 入口網站開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a9a7c-126">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a9a7c-127">使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 應用程式</span><span class="sxs-lookup"><span data-stu-id="a9a7c-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
