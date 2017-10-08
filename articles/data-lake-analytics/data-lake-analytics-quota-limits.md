---
title: "資料湖分析配額限制 aaaAzure |Microsoft 文件"
description: "了解如何 tooadjust 並增加配額會限制在 Azure 資料湖分析 (ADLA) 帳戶。"
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Azure Data Lake Analytics 配額限制

了解如何 tooadjust 並增加配額會限制在 Azure 資料湖分析 (ADLA) 帳戶。 了解這些限制可幫助您了解 U-SQL 作業的行為。 所有配額限制都是軟性的因此您可以增加觸角 toous hello 最大限制。

## <a name="azure-subscriptions-limits"></a>Azure 訂用帳戶限制

**每個訂用帳戶的 ADLA 帳戶最大數目︰**5

 這是 hello ADLA 帳戶，您可以建立每個訂閱的數目上限。 如果 toocreate 第六個 ADLA 帳戶再試一次，您會收到錯誤 「 您已在訂用帳戶名稱的區域中達到 hello Data Lake Analytics 帳戶允許 (5) 的數目上限 」。 在此情況下，刪除任何未使用的 ADLA 帳戶，或是聯繫 toous 由[開啟支援票證](#increase-maximum-quota-limits)。

## <a name="adla-account-limits"></a>ADLA 帳戶限制

**每個帳戶分析單位 (AU) 的最大數目︰**250

這是 hello 可以同時在您的帳戶中執行的澳洲的數目上限。 如果您的所有作業加起來的執行中 AU 總數超過此限制，系統會自動將較新的工作排入佇列。 例如：

* 如果您有只有一個工作執行與 250 澳洲，當您送出第二個工作它 hello 第一個工作完成之前會等候 hello 工作佇列中。
* 如果您已經有五個執行的作業，而且每個都使用 50 澳洲，當您送出第六個工作需要 20 澳洲它會等候 hello 工作佇列中有 20 澳洲可用。

**每個帳戶的並行 U-SQL 作業最大數目︰**20

這是 hello 可以同時在您的帳戶中執行的作業數目上限。 超過此值，新的工作會自動排入佇列。

## <a name="adjust-adla-quota-limits-per-account"></a>調整每個帳戶的 ADLA 配額限制

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇現有的 ADLA 帳戶。
3. 按一下 [內容] 。
4. 調整**平行處理原則**和**並行作業**toosuit 您的需求。

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>增加配額限制上限

1. 在 Azure 入口網站中開啟支援要求。

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. 選取問題類型排序 hello**配額**。
3. 選取您的 [訂用帳戶] \(請確定它不是「試用」的訂用帳戶\)。
4. 選取 [Data Lake Analytics] 配額類型。

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. 在 hello 問題 刀鋒視窗中，說明您要求的增加數目限制，而且具有**詳細資料**的為何需要這個額外的容量。

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. 請確認您的連絡資訊，然後建立 hello 支援要求。

Microsoft 會檢閱您的要求，並嘗試您的業務需求儘速 tooaccommodate。

## <a name="next-steps"></a>後續步驟

* [Microsoft Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* [使用 Azure PowerShell 管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-powershell.md)
* [使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 作業](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
