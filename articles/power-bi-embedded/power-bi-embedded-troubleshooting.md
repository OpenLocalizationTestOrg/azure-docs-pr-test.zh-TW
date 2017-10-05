---
title: "Microsoft Power BI Embedded Preview 疑難排解"
description: "Microsoft Power BI Embedded Preview 疑難排解"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="ea650-103">Microsoft Power BI Embedded Preview 疑難排解</span><span class="sxs-lookup"><span data-stu-id="ea650-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="ea650-104">本文提供如何疑難排解 **Power BI Embedded** 的解答。</span><span class="sxs-lookup"><span data-stu-id="ea650-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="ea650-105">設定 SQL Server 連接字串</span><span class="sxs-lookup"><span data-stu-id="ea650-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="ea650-106">若要設定 SQL Server 連接字串，您必須遵循特定的格式。</span><span class="sxs-lookup"><span data-stu-id="ea650-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="ea650-107">以下是 SQL Server 的連接字串範例。</span><span class="sxs-lookup"><span data-stu-id="ea650-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="ea650-108">若要深入了解 SQL Server 連接字串，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="ea650-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="ea650-109">SQL Server 連接字串</span><span class="sxs-lookup"><span data-stu-id="ea650-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="ea650-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="ea650-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="ea650-111">設定認證</span><span class="sxs-lookup"><span data-stu-id="ea650-111">Setting credentials</span></span>
<span data-ttu-id="ea650-112">開發或預備環境如果有需要認證的情況，如使用者名稱和密碼，您可能必須更新符合生產環境方案的認證。</span><span class="sxs-lookup"><span data-stu-id="ea650-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="ea650-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ea650-113">See Also</span></span>
* [<span data-ttu-id="ea650-114">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="ea650-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="ea650-115">什麼是 Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ea650-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

