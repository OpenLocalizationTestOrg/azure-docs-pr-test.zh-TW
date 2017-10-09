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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Microsoft Power BI Embedded Preview 疑難排解
本文章提供如何回答 tootroubleshoot **Power BI Embedded**。

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>設定 SQL Server 連接字串
tooset 的 SQL Server 連接字串，您需要 toofollow 特定格式。 以下是 SQL Server 的連接字串範例。

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn 進一步了解 SQL Server 的連接字串，請參閱下列文章 hello:

* [SQL Server 連接字串](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>設定認證
在您有包含用於開發或預備環境，使用者名稱和密碼等認證的 hello 情況中，您可能需要符合生產環境方案 tooupdate 認證。

## <a name="see-also"></a>另請參閱
* [開始使用範例](power-bi-embedded-get-started-sample.md)
* [什麼是 Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

