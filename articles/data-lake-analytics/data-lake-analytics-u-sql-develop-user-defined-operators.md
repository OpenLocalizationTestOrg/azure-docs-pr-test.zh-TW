---
title: "aaaDevelop U-SQL 使用者定義運算子 (Udo) |Microsoft 文件"
description: "了解 toodevelop 使用者定義運算子 toobe 的使用方式，並在 Data Lake Analytics 中，重複使用的工作。 "
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
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a>開發 U-SQL 使用者定義的運算子 (UDO)
了解如何 toodevelop 使用者定義運算子 tooprocess 資料 U-SQL 作業中的。

如需有關開發 U-SQL 一般用途組件的指示，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a>在 U-SQL 中定義和使用使用者定義的運算子
**toocreate 並提交 U SQL 作業**

1. 從 Visual Studio hello 選取**檔案 > 新增 > 專案 > U-SQL 專案**。
2. 按一下 [確定] 。 Visual Studio 會建立具有 Script.usql 檔案的解決方案。
3. 在 [方案總管] 中展開 Script.usql，然後按兩下 **Script.usql.cs**。
4. 貼上下列程式碼到 hello 檔案 hello:

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
6. 開啟**Script.usql**，並貼上 hello 遵循 U-SQL 指令碼：

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
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. 指定 hello Data Lake Analytics 帳戶、 資料庫和結構描述。
8. 從 方案總管 中，在 Script.usql 上按一下滑鼠右鍵，然後按一下建置指令碼。
9. 從 方案總管 中，在 Script.usql 上按一下滑鼠右鍵，然後按一下提交指令碼。
10. 如果您尚未連接 tooyour Azure 訂用帳戶，您將會提示的 tooenter 您的 Azure 帳戶的認證。
11. 按一下 [提交] 。 送出結果和工作連結可用 hello [結果] 視窗中完成 hello 送出。
12. 按一下 hello**重新整理**按鈕 toosee hello 最新作業的狀態並重新整理囉 」 畫面。

**toosee hello 輸出**

1. 從**伺服器總管**，依序展開**Azure**，依序展開**Data Lake Analytics**，依序展開您的資料湖分析帳戶**的儲存體帳戶**hello 預設儲存體，以滑鼠右鍵按一下，然後按**總管**。
2. 展開範例、展開輸出，然後按兩下 [Drivers.csv] 。

## <a name="see-also"></a>另請參閱
* [使用 PowerShell 開始使用 Data Lake Analytics](data-lake-analytics-get-started-powershell.md)
* [開始使用 Data Lake Analytics 使用 hello Azure 入口網站](data-lake-analytics-get-started-portal.md)
* [使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 應用程式](data-lake-analytics-data-lake-tools-get-started.md)
