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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Microsoft Power BI Embedded Preview 疑難排解
本文提供如何疑難排解 **Power BI Embedded** 的解答。

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>設定 SQL Server 連接字串
若要設定 SQL Server 連接字串，您必須遵循特定的格式。 以下是 SQL Server 的連接字串範例。

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

若要深入了解 SQL Server 連接字串，請參閱下列文章︰

* [SQL Server 連接字串](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>設定認證
開發或預備環境如果有需要認證的情況，如使用者名稱和密碼，您可能必須更新符合生產環境方案的認證。

## <a name="see-also"></a>另請參閱
* [開始使用範例](power-bi-embedded-get-started-sample.md)
* [什麼是 Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

