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
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>針對 Azure Data Lake Analytics 作業開發 U-SQL 組件
了解如何 tooturn 程式碼後置到組件 toobe 用和在 Data Lake Analytics 工作中重複使用。 

U SQL 可讓您自己的自訂程式碼的簡單 tooadd 在.Net 語言中，例如 C#、 VB.Net 或 F #。 您甚至可以部署您自己的執行階段 toosupport 其他語言。

hello 最簡單方式 toouse 自訂程式碼是 toouse hello Data Lake Tools for Visual Studio 程式碼後置功能。 如需詳細資訊，請參閱 [教學課程：使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。 使用程式碼後置有幾個缺點︰

- 每個指令碼送出 hello 原始程式碼取得上傳。
- 程式碼後置無法與其他作業共用。

tooaddress 這些缺點，您可以開啟程式碼後置為組件，並註冊 hello 組件 toohello Data Lake Analytics 類別目錄。

## <a name="prerequisites"></a>必要條件
* 已安裝 Visual Studio 2017、Visual Studio 2015、Visual Studio 2013 Update 4，或具有 Visual C++ 的 Visual Studio 2012。
* Microsoft Azure SDK for .NET 2.5 版或更新版本。  使用 hello Web platform installer 或 Visual Studio 安裝程式進行安裝
* Data Lake Analytics 帳戶。  請參閱[使用 Azure 入口網站開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。
* 請執行 hello[開始使用 Azure 資料湖分析 U-SQL Studio](data-lake-analytics-u-sql-get-started.md)教學課程。
* 連接 tooAzure。
* 上傳 hello 來源資料，請參閱[開始使用 Azure 資料湖分析 U-SQL Studio](data-lake-analytics-u-sql-get-started.md)。 

## <a name="develop-assemblies-for-u-sql"></a>開發 U-SQL 的組件

**toocreate 並提交 U SQL 作業**

1. 從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。
2. 展開**已安裝**，**範本**， **Azure 資料湖**， **U-SQL(ADLA)**，選取 hello**類別庫 (如 U-SQL應用程式）**範本，然後再按一下**確定**。
3. 在 Class1.cs 中撰寫程式碼。  hello 如下的程式碼範例。

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
4. 按一下 hello**建置**功能表，然後再按一下**建置方案**toocreate hello dll。

## <a name="register-assemblies"></a>註冊組件

請參閱[使用 Data Lake Analytics (U-SQL) 目錄](data-lake-analytics-use-u-sql-catalog.md)。


## <a name="use-hello-assemblies"></a>使用 hello 組件

請參閱[使用 hello Azure 資料湖 Tools for Visual Studio 程式碼](data-lake-analytics-data-lake-tools-for-vscode.md)。

## <a name="see-also"></a>另請參閱
* [使用 PowerShell 開始使用 Data Lake Analytics](data-lake-analytics-get-started-powershell.md)
* [開始使用 Data Lake Analytics 使用 hello Azure 入口網站](data-lake-analytics-get-started-portal.md)
* [使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 應用程式](data-lake-analytics-data-lake-tools-get-started.md)
* [使用 Data Lake Analytics (U-SQL) 目錄](data-lake-analytics-use-u-sql-catalog.md)
* [使用 hello Azure 資料湖 Tools for Visual Studio 程式碼](data-lake-analytics-data-lake-tools-for-vscode.md)
