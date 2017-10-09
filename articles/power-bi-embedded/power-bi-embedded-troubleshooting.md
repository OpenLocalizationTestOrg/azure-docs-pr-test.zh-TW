---
title: "aaaMicrosoft Power BI Embedded Preview 疑難排解"
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
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="f552a-103">Microsoft Power BI Embedded Preview 疑難排解</span><span class="sxs-lookup"><span data-stu-id="f552a-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="f552a-104">本文章提供如何回答 tootroubleshoot **Power BI Embedded**。</span><span class="sxs-lookup"><span data-stu-id="f552a-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="f552a-105">設定 SQL Server 連接字串</span><span class="sxs-lookup"><span data-stu-id="f552a-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="f552a-106">tooset 的 SQL Server 連接字串，您需要 toofollow 特定格式。</span><span class="sxs-lookup"><span data-stu-id="f552a-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="f552a-107">以下是 SQL Server 的連接字串範例。</span><span class="sxs-lookup"><span data-stu-id="f552a-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="f552a-108">toolearn 進一步了解 SQL Server 的連接字串，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="f552a-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="f552a-109">SQL Server 連接字串</span><span class="sxs-lookup"><span data-stu-id="f552a-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="f552a-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="f552a-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="f552a-111">設定認證</span><span class="sxs-lookup"><span data-stu-id="f552a-111">Setting credentials</span></span>
<span data-ttu-id="f552a-112">在您有包含用於開發或預備環境，使用者名稱和密碼等認證的 hello 情況中，您可能需要符合生產環境方案 tooupdate 認證。</span><span class="sxs-lookup"><span data-stu-id="f552a-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="f552a-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f552a-113">See Also</span></span>
* [<span data-ttu-id="f552a-114">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="f552a-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="f552a-115">什麼是 Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f552a-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

